# Mineradio-fix_SMTC

![Mineradio 暗场启动页](./docs/assets/readme/cinema-beat-smoke.png)

> 本项目是 [XxHuberrr/Mineradio](https://github.com/XxHuberrr/Mineradio) 的 Fork，由 [Minecraftmc22](https://github.com/Minecraftmc22) 维护。
>
> 在原版基础上增加了 **SMTC（System Media Transport Controls）** 支持——Windows 系统级媒体控制（音量混合器、锁屏、任务栏悬停）现在可以显示当前播放歌曲信息并进行播放控制。

Mineradio 是一款 Windows 桌面沉浸式音乐播放器，把天气电台、搜索播放、歌词舞台、粒子视觉和 3D 歌单架组合成一个更接近现场感的私人音乐空间。

## 本 Fork 的改动

### SMTC 系统媒体控制集成

使用 Chromium 内置的 `navigator.mediaSession` API 实现，无需额外原生模块，自动与 Windows SMTC 集成。

**功能：**

- 播放时在 Windows 音量混合器、锁屏、任务栏显示歌曲标题、艺术家、专辑和封面
- 支持系统级播放/暂停/上一首/下一首/进度跳转控制
- 进度条实时同步（200ms 节流）
- 清空播放队列时自动清除 SMTC 元数据

**支持的 SMTC 动作：** play、pause、previoustrack、nexttrack、seekto、seekbackward、seekforward、stop

详见 [SMTC 集成说明](#)。

## 立即下载

| 下载入口 | 链接 |
| --- | --- |
| 本 Fork Release | [Minecraftmc22/Mineradio-fix_SMTC Releases](https://github.com/Minecraftmc22/Mineradio-fix_SMTC/releases) |
| 原版 Release | [XxHuberrr/Mineradio Releases](https://github.com/XxHuberrr/Mineradio/releases) |

安装时只需要下载并运行 `Mineradio-1.1.1-Setup.exe`。不要下载 `Source code`、`.blockmap`、`latest.yml`，也不要把 `win-unpacked` 当成正式安装包。

## 下载或安装被拦截怎么办

小众 Electron 桌面软件、未签名安装包有时会被浏览器、Windows Defender 或 SmartScreen 提示风险。请先确认安装包来自上面的 GitHub Release 官方入口。

1. 浏览器下载栏提示风险时，打开下载列表，点这条下载右侧的 `...` 三个点，选择 `保留` / `仍要保留` / `显示更多` 后继续保留。
2. Windows SmartScreen 弹出蓝色拦截窗口时，点 `更多信息`，再点 `仍要运行`。
3. 如果杀毒软件明确显示木马、高危或已经隔离，不要强行运行；删除该文件后重新下载。

## 当前版本

当前版本：`1.1.1`

状态：1.1.1 + SMTC 集成。

## 核心特性

- **SMTC 系统媒体控制**（本 Fork 新增）—— Windows 锁屏、音量混合器显示歌曲信息和控制按钮
- Open-Meteo 天气电台，根据当前位置、城市和天气 mood 生成更合适的播放队列
- 首页包含天气电台、每日推荐、私人电台、继续听、听歌画像和我的歌单入口
- Wallpaper 银河首页背景，未播放状态保持干净的星河氛围
- 播放后切换到 Emily / 默认播放态视觉，歌词舞台与粒子舞台同步工作
- 基于节奏的电影镜头视觉系统
- 面向长播客和 DJ 曲目的专属视觉模式
- 歌词舞台、自定义歌词、歌词位置与视觉控制
- 自定义专辑封面上传与裁剪
- 右键唤起 3D 歌单架，支持歌单队列浏览
- 网易云音乐账号、搜索、歌单、播客等体验接入
- QQ 音乐搜索、登录态与音源补充接入
- GitHub Releases 更新检测与下载入口
- 首次启动内置「默认测试」视觉用户存档，软件内默认视觉参数与该存档一致

## 使用说明

Windows 用户可以在 GitHub Releases 中下载安装包。

正式分发以 `Mineradio-1.1.1-Setup.exe` 为准，不建议直接下载 `win-unpacked` 目录作为正式分发包。安装包会创建桌面快捷方式；直接运行打包版 `Mineradio.exe` 时，应用也会在首次启动时补创建桌面快捷方式。

## 开发运行

```bash
npm install
npm start
npm run build:win
```

> **Electron 下载慢？** 使用国内镜像加速：
> ```bash
> ELECTRON_MIRROR=https://npmmirror.com/mirrors/electron/ npm install
> ```

桌面版入口由 Electron 主进程加载本地服务。`npm run build:win` 会生成 Windows NSIS 安装包，产物位于 `dist/`。

## 更新机制

Mineradio 会请求 GitHub Releases latest 检测新版本。远端版本高于本地版本时，应用内更新入口会展示 Release 内容、下载安装包到本机用户数据目录，并通过系统打开安装包。

本地验证更新链路时，可以通过 `MINERADIO_UPDATE_MANIFEST` 指向一个本地 manifest JSON 或 HTTP 地址来模拟线上 Release。

## 第三方音乐平台说明

Mineradio 不是网易云音乐、QQ 音乐或腾讯音乐娱乐集团的官方客户端，也不隶属于任何音乐平台。

项目中的第三方平台接入仅用于个人学习、本地客户端体验和用户自有账号的播放辅助。请遵守对应平台的用户协议、版权规则和会员权益规则。项目不会提供绕过付费、绕过会员、破解音质或重新分发音乐内容的能力。

## 用户数据与隐私

登录 Cookie、搜索历史、自定义封面、自定义歌词、节奏分析缓存等数据只应保存在本机用户数据目录或浏览器本地存储中，不应提交到仓库。

更多说明见 [PRIVACY.md](./PRIVACY.md)。

## 致谢

- **原项目**：[Mineradio](https://github.com/XxHuberrr/Mineradio) 由 [XxHuberrr](https://github.com/XxHuberrr) 主要设计与打造。
- emily 作为早期视觉底层想法与 `emily` 视觉预设改进方向的共创者和灵感来源之一，特此感谢。
- 同时感谢小天才e宝、应春日、锋将军、軌跡、林中、骊、风痕、花椰菜🥦在早期体验、测试反馈和发布准备中的帮助。
- 本 Fork 的 SMTC 集成由 [Minecraftmc22](https://github.com/Minecraftmc22) 完成。

## 版权与授权

Copyright (C) 2026 XxHuberrr.

本项目采用 GPL-3.0 授权。详见 [LICENSE](./LICENSE)。

MR Logo、Mineradio 名称、界面视觉设计与原创视觉表达归原作者所有；第三方依赖和第三方服务分别遵循其各自授权与服务条款。
