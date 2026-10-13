# VPS000 Clients

公开下载仓库。安装包与 APK 都在 [Releases](https://github.com/VPS668/clients/releases)。

源码在私有仓库，不在本仓库。客户端「检查更新」读取本仓库 Releases，并按平台过滤。

## 最新下载

### Windows 10 / 11

当前版本 **v2.4.1.2** · [Release 说明](https://github.com/VPS668/clients/releases/tag/v2.4.1.2)

- [VPS000Client-2.4.1.2-Setup.exe](https://github.com/VPS668/clients/releases/download/v2.4.1.2/VPS000Client-2.4.1.2-Setup.exe)
- [VPS000Client-2.4.1.2-win-x64.zip](https://github.com/VPS668/clients/releases/download/v2.4.1.2/VPS000Client-2.4.1.2-win-x64.zip)

### Windows 7 / 8

当前版本 **win7-2.4.1.2** · [Release 说明](https://github.com/VPS668/clients/releases/tag/win7-2.4.1.2)

- [VPS000Client-win7-2.4.1.2-Setup.exe](https://github.com/VPS668/clients/releases/download/win7-2.4.1.2/VPS000Client-win7-2.4.1.2-Setup.exe)
- [VPS000Client-win7-2.4.1.2-win7-win8-x64.zip](https://github.com/VPS668/clients/releases/download/win7-2.4.1.2/VPS000Client-win7-2.4.1.2-win7-win8-x64.zip)

### Android

当前版本 **android-v2.4.1.26** · [Release 说明](https://github.com/VPS668/clients/releases/tag/android-v2.4.1.26)

- [VPS000Client-android-2.4.1.26.apk](https://github.com/VPS668/clients/releases/download/android-v2.4.1.26/VPS000Client-android-2.4.1.26.apk)

### macOS

当前版本 **macos-v2.4.1.1** · [Release 说明](https://github.com/VPS668/clients/releases/tag/macos-v2.4.1.1)

- [VPS000Client-2.4.1-macos-arm64.pkg](https://github.com/VPS668/clients/releases/download/macos-v2.4.1.1/VPS000Client-2.4.1-macos-arm64.pkg)（Apple Silicon 安装包）
- [VPS000Client-2.4.1-macos-arm64.dmg](https://github.com/VPS668/clients/releases/download/macos-v2.4.1.1/VPS000Client-2.4.1-macos-arm64.dmg)（Apple Silicon 拖拽安装）
- [VPS000Client-2.4.1-macos-x64.pkg](https://github.com/VPS668/clients/releases/download/macos-v2.4.1.1/VPS000Client-2.4.1-macos-x64.pkg)（Intel 安装包）
- [VPS000Client-2.4.1-macos-x64.dmg](https://github.com/VPS668/clients/releases/download/macos-v2.4.1.1/VPS000Client-2.4.1-macos-x64.dmg)（Intel 拖拽安装）


### CPE 路由器（ZBT-Z8103AX）

当前版本 **cpe-z8103ax-v2.4.1.5** · [Release 说明](https://github.com/VPS668/clients/releases/tag/cpe-z8103ax-v2.4.1.5)

> 查找 CPE 固件请打开 [带 cpe-z8103ax 过滤的 Releases](https://github.com/VPS668/clients/releases?q=cpe-z8103ax&expanded=true)。**不要**使用仓库的 `/releases/latest`（会指向桌面/手机客户端）。

**首次从原厂刷入（推荐）**

- [OEM Web 验签包（原厂网页升级用）](https://github.com/VPS668/clients/releases/download/cpe-z8103ax-v2.4.1.5/openwrt-25.12-snapshot-vps000-2.4.1.5-mediatek-filogic-zbtlink_zbt-z8103ax-c-oem-web-sysupgrade.bin) — 在原厂「固件升级」页上传
- 备用：[factory-single.bin（U-Boot Reset，单系统）](https://github.com/VPS668/clients/releases/download/cpe-z8103ax-v2.4.1.5/openwrt-25.12-snapshot-vps000-2.4.1.5-mediatek-filogic-zbtlink_zbt-z8103ax-c-squashfs-factory-single.bin)

**已安装后升级**

- [sysupgrade.bin](https://github.com/VPS668/clients/releases/download/cpe-z8103ax-v2.4.1.5/openwrt-25.12-snapshot-vps000-2.4.1.5-mediatek-filogic-zbtlink_zbt-z8103ax-c-squashfs-sysupgrade.bin)

**刷机后默认**

- Web：`http://192.168.1.1` · admin / admin
- Wi‑Fi：`VPS000` / `VPS000-5G` · **开放无密码**（请尽快加密；并核对本机 MAC，勿连错附近同名热点）
- SSH：root / `vps000@root`

默认**单系统**；双系统可在管理界面「更新」页按需启用。

完整步骤（含原厂 Web 验签说明与 U-Boot 备用）：**[网页版刷机说明](docs/cpe-flash.md)**

新手推荐：**[原厂 Web 刷机图文教程（每步截图）](docs/cpe-flash-oem-web-illustrated.md)**

**sha256**

- oem-web: `702f85d0d11f9a714921477269d28a9f02e6f335036067f59d8a804d3c427e53`
- factory-single: `2964497c0e637fe9fad76056f8adb0ba1fbc00b5c0fc849c0d0d38885d081cf8`
- factory（双系统启用用）: `fdf5902d1606cec20f7bf265d5059ffba3a6f9b6a69e3d37fa104b68b67ba428`
- sysupgrade: `0f6b2ce1ebc2a08184ae3fa4be29475ff12da7f73aea1d49b51ef9b75564f0e7`

完整清单见 Release 的 `manifest.json` / `SHA256SUMS`。


### iOS

当前版本 **2.4.1** · [TestFlight 安装](https://testflight.apple.com/join/kqYjeWeD)

---

本页由发版脚本自动更新。
