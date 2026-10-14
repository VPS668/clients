# ZBT-Z8103AX CPE 刷机说明（网页版）

适用型号：**ZBT-Z8103AX-C / ZBT-Z8103AX-D**（MT7981，SPI-NAND 128M）  
固件发布页：[cpe-z8103ax 最新 Release](https://github.com/VPS668/clients/releases?q=cpe-z8103ax&expanded=true)（不要用仓库总最新 `/releases/latest`，那会命中桌面/手机客户端）

> 刷机有风险。请确认型号与机身 MAC，不要把别的机器的备份刷到本机。  
> **不要**把本机与附近其它同类热点搞混——出厂 SSID 含本机 MAC 后 6 位，请对照机身/包装上的 MAC。

## 下载哪个文件？

| 场景 | 文件 | 说明 |
|------|------|------|
| **原厂固件首次刷入（推荐）** | `*-oem-web-sysupgrade.bin`（或名称含 `vendor-web` / `oem-web`） | 在**原厂 Web 管理页 → 固件升级**上传。已按原厂验签格式封装。**默认单系统**。 |
| 原厂 Web 被拒时的备用 | `*-squashfs-factory-single.bin`（优先）或 `*-squashfs-factory.bin` | 用 **U-Boot Web Failsafe**（按住 Reset 上电）上传。**首次请优先 single**；不含 `single` 的 factory 为双分区镜像，仅在「更新」页主动启用双系统时使用。 |
| 已在跑 VPS000 / OpenWrt 后升级 | `*-squashfs-sysupgrade.bin` | LuCI / VPS UI「更新」或 `sysupgrade`。 |
| 可选：启用双系统 | 双分区 `*-factory.bin`（非 single）+ `02-fip-dualboot-*.bin`（kind: fip） | 在管理界面 **更新 → 双系统（可选）** 按提示操作（2.4.1.14+ 含 FIP 安装器；不写 BL2）。不是默认必选项。 |

发布页同时提供 `sha256`（Release 说明或 `manifest.json`）。下载后请校验：

```bash
shasum -a 256 <下载的文件>
```

## 推荐路径 A：原厂 Web 升级（OEM 验签包）

> 📷 每步带截图的版本：**[原厂 Web 刷机图文教程](cpe-flash-oem-web-illustrated.md)**

原厂 ZBT 固件（如 26.08.06）的 Web 升级会做 OpenWrt 标准校验：

1. **fwtool 元数据** `supported_devices` 需含原厂 board：`mediatek,mt7981-spim-snand-rfb-z8103ax`
2. **usign/ucert 验签**：公钥指纹 `c14cf35a2c57b897`（ZBT SDK key-build）
3. 包内目录名 / `BOARD=` 需为 `mt7981-spim-nand-rfb-z8103ax`

我们发布的 **OEM Web 过渡包**已按上述格式重新封装并签名，因此可直接在原厂页面升级（只重写 UBI 的 kernel/rootfs，**不改 BL2/FIP**）。

### 步骤

1. 电脑网口接 CPE **LAN**，电脑设静态 IP `192.168.1.10/24`（网关可空）。
2. 浏览器打开 `http://192.168.1.1`，登录原厂后台（默认常见为 admin/admin，以机身标签为准）。
3. 进入 **系统 → 固件升级**（或同类菜单），**取消「保留配置」**。
4. 上传 `*-oem-web-sysupgrade.bin`，确认后等待 **3～5 分钟**，勿断电。
5. 完成后设备应出现开放 Wi‑Fi（固件 **2.4.1.13+**）：`VPS000_<MAC后6位>` / `VPS000_<MAC后6位>-5G`（大写十六进制、无冒号；例 MAC `f8:5e:3c:a7:fc:a4` → `VPS000_A7FCA4` / `VPS000_A7FCA4-5G`），**加密无 / 空密码**。管理地址仍为 `http://192.168.1.1`。

登录管理界面：

- Web：用户名/密码 **admin / admin**
- SSH：`root` / `vps000@root`
- Wi‑Fi：开放网络，**首次登录后请立刻在「设置 / Wi‑Fi」中加密并改密**

## 备用路径 B：U-Boot Reset（Failsafe）

当原厂 Web 拒绝升级包时使用。

1. 断电；按住 **Reset** 再上电，保持约 **5～10 秒**（或串口 bootmenu 选 `Start Web failsafe`）。
2. 电脑静态 IP `192.168.1.10/24`，浏览器打开 `http://192.168.1.1`。
3. 上传 **`*-squashfs-factory.bin`**（整盘 factory / UBI 镜像），等待完成。
4. 同上：连接开放 Wi‑Fi `VPS000_<MAC后6位>` / `VPS000_<MAC后6位>-5G`，打开 `http://192.168.1.1`。

## 以后升级

已在 VPS000 固件上时，下载 **sysupgrade** 包，在 Web「更新」页操作，或：

```sh
sysupgrade -n /tmp/sysupgrade.bin   # -n 不保留配置；去掉 -n 则尽量保留
```

双分区机型会写入**非活动槽**并切换启动；连续启动失败会自动回退。

**升级不会覆盖用户已自定义的 Wi‑Fi**（名称 / 密码 / 加密）；仅出厂或重置后的空/OpenWrt 默认无线才会被写成上述 MAC SSID 开放网络。

## 刷机后默认值

| 项 | 默认 |
|----|------|
| 管理 Web | `http://192.168.1.1` · admin / admin |
| SSH | root / `vps000@root` |
| Wi‑Fi 2.4G | SSID `VPS000_<MAC后6位>` · **开放（加密 none / 无密码）** |
| Wi‑Fi 5G | SSID `VPS000_<MAC后6位>-5G` · **开放（加密 none / 无密码）** |

MAC 后 6 位：去掉冒号后取末 6 个十六进制字符并**大写**（例 `f8:5e:3c:a7:fc:a4` → `A7FCA4` → `VPS000_A7FCA4` / `VPS000_A7FCA4-5G`）。固件 **2.4.1.13+**。

⚠️ 开放 Wi‑Fi 仅方便首次接入。**请尽快设置密码**，并按 MAC 后缀确认连的是本机热点。

## 语言

管理界面右上角可切换 **中文 / English**，偏好保存在浏览器本地。

点击左上角 Logo /「威伯斯云」可回到概览页。


## v2.4.1.14 文件校验（sha256）

| 文件 | sha256 |
|------|--------|
| oem-web-sysupgrade.bin | `aef2d195909d641605a74bb024c8a62bc17aa3b776af6c482607d0f26fca5669` |
| factory-single.bin | `4edaa5fc23f5e1ed8627b77e648237ac9cf22afbd58e4c031b1067ddb609cb70` |
| factory.bin | `87e1aac4c5f69e521f7ae91d6e8776e980747d23ce509c3a496b4fbe703849a6` |
| sysupgrade.bin | `e7adf1ea041837ec49b33e17fa9e0b8362cc4fbdd252630d41b574ee7dfa0cdf` |
| FIP（双系统，不写 BL2） | `2f0a455707620964fcb6bdd3d736b646184cd5d4ee00087cc8d29a3ac65a2c28` |

> **2.4.1.14 双系统说明**：一键启用会 plant keep + 早启 restore；FIP 只由镜像内 `install-fip.sh` 写入名为 `FIP` 的 MTD（不写 BL2）。发行说明含 `keep-proven` 前，factory 步骤后密码/VPN **可能重置**。已是双分区布局的设备（如 A7FCA4）升级后一般只需 FIP 步骤。支持双→单回退（刷 `factory-single`，不改 FIP）。
|--------|
| oem-web-sysupgrade.bin | `fd2eae5fcf5e19c139ea30eef31a19161d81da6cb1e06366397b18be03597d92` |
| factory-single.bin | `bbac75ec22c94467c972df87b8acd2a82d7ff5fbcd0ebf18c1f768bf8a8d1e48` |
| factory.bin | `63c1b8ccb0404a953a724d0423474b3105dd1ccb9736be93d204d935d888b70f` |
| sysupgrade.bin | `cd37a496a0b3f02de38fc618634c96e17fcd4612733e94674c9cb629496b8c02` |
