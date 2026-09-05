# Prophecy · 预感校准本

记录 → 到期验证 → 校准曲线的直觉训练工具。单文件 HTML，零依赖、纯离线、数据只存本机。

## 两种用法

### 1) 浏览器直接用（最省事）
双击根目录 `预感校准本.html`，或用浏览器打开即可。也可把 www 目录部署到任意静态托管。

### 2) 装成安卓 App（APK）

本仓库用 [Capacitor](https://capacitorjs.com/) 把 `www/index.html` 包成原生 WebView APK，
构建由 GitHub Actions 云完成，本机不需要装任何安卓工具链。

**打一次包：**
1. 把代码推到本仓库 main 分支
2. 打开仓库页面 → **Actions** 标签 → 左侧 **Build Android APK**
3. 右侧 **Run workflow** → 绿色按钮，等约 5~10 分钟
4. 跑完后进该次运行的页面 → 底部 **Artifacts** → 下载 `预感校准本-apk`
5. 手机（安卓 8.0+）上安装：需允许"安装未知来源应用"；debug 签名包仅用于自用/测试

**打正式发布版（可选）：** 推一个形如 `v1.0.0` 的 tag，同一流程会自动把 APK 挂到 GitHub Release 页面。

## 自定义

| 想改什么 | 改哪里 |
|---|---|
| 应用名 / 包名（applicationId） | `capacitor.config.json` 的 `appName` / `appId`（appId 起过一次不要重复用同一签名旧包覆盖安装） |
| 界面与功能 | 改 `预感校准本.html`（源码），再同步到 `www/index.html`：Git Bash: `cp 预感校准本.html www/index.html`；PowerShell: `Copy-Item 预感校准本.html www/index.html -Force` |
| 桌面图标 | 替换 APK 后按 Capacitor 指南生成：先加 `assets/icon.png`（1024×1024），本地装好依赖后 `npx capacitor-assets generate` |

## 数据说明

- 记录保存在 App 的 localStorage，卸载 App / 清除应用数据会丢失——**定期在「数据」页做 JSON 备份**。
- APK 内点导出走系统"保存/分享"面板（内置 Filesystem+Share 插件）；浏览器打开则直接下载文件。
- 数据不上传任何服务器。

## 技术栈

- 应用本体：单文件 HTML + 原生 JS（无框架、无 CDN、可离线）
- 打包：Capacitor 7 + GitHub Actions（ubuntu-latest，自带 Android SDK）
