# 阿弥陀佛｜官方下载与更新

**这是公开下载仓库：只放安装包、更新文件和使用说明。开发源码在另一个私有仓库维护。** GitHub 自动显示的 `Source code` 压缩包仅包含此下载仓库的文档，不是程序源码，也不是安装包。

## 下载和安装

当前版本：[**手机 AI 接口的最后一版本 · 1.0.0-beta.21**](https://github.com/Suxifang/Amitoufo-Releases/releases/tag/v1.0.0-beta.21)。后续开发计划集中维护电脑端；需要手机模式的用户可保留本版。

进入版本页，选择 **`Amitoufo-<版本>-win-x64-setup.exe`**。无需 GitHub 登录；不要下载 `Source code` 作为安装程序。[历史发布](https://github.com/Suxifang/Amitoufo-Releases/releases)继续保留。

- 适用 Windows 10/11 x64。安装后从桌面“阿弥陀佛”打开。
- 首次使用配置自己的语音转录与回答服务 Key，并导入自己的材料。分享包不携带维护者的个人资料。
- 免安装版 `portable.exe` 需要手动更换文件；推荐使用安装版。
- 下载后可对照同版本 `SHA256SUMS.txt` 或 `.sha256`；安装器目前未作代码签名。

## 更新与旧版迁移

**从 beta.5 起，软件在这个公开仓库检查和下载更新。** 点击软件名下方“更新”，依次检查、下载、退出并安装。

beta.4 及更早版本仍使用旧地址；请先从本页手动安装一次 beta.5 或更高版本。正常覆盖安装，无需先卸载，不要清理 `%APPDATA%\MeetingCopilot`，以保留 Key、简历/JD 与会话。切换完成后，后续使用应用内更新。

| 文件 | 用途 |
|---|---|
| `setup.exe` | 推荐安装版及覆盖升级 |
| `portable.exe` | 手动使用的免安装版 |
| `latest.yml` / `beta.yml` | 软件读取的更新信息，普通用户不用打开 |
| `USER_GUIDE.zh-CN.html` | 离线使用手册 |
| `SHA256SUMS.txt` / `.sha256` | 下载校验 |
| `BUILD-INFO.json` | 构建版本和校验记录，供维护核对 |

## 功能与使用说明

提供电脑声音／麦克风转录、结合个人背景的回答、翻译及Windows窗口采集保护。顶部默认一行，点击“⋯”展开收音、简洁／详细、会话和资料；窗口可拖出屏幕边缘，隐藏后重新呼出会移回可见范围。

电脑会议模式从系统声音转录对方问题并自动回答，本人麦克风记录实际回答供上下文参考；手机外放模式由电脑麦克风混录双方，默认手动答。题目完整后点“答最新题”或使用已配置快捷键（默认F8，可在设置修改）。手机混录依靠话轮及文本选题，有限案例不保证任意口语都能正确区分。

电脑、手机和打字共用回答规则与简洁／详细设置，重点是切题、长题完整、多问点答全及上下文衔接；参考回答允许围绕简历主线加工。具体检查范围和剩余限制见本版发布说明。

[完整使用手册](docs/USER_GUIDE.zh-CN.md) · [Windows安装与更新](docs/user/INSTALL_WINDOWS.zh-CN.md) · [服务Key教程](docs/user/API_KEYS.zh-CN.md) · [故障排查](docs/user/TROUBLESHOOTING.zh-CN.md) · [问题反馈](https://github.com/Suxifang/Amitoufo-Releases/issues)

窗口保护效果取决于系统、设备与采集方式；使用前按实际场景检查截图、录屏和会议接收端。云服务数据发送给使用者自行配置的服务商，使用须符合所在场景要求。

## 出处、许可与自用说明

由 Suxifang 基于 [JWM0203/MeetingCopilot](https://github.com/JWM0203/MeetingCopilot) `v0.2.0-beta.1` 修改维护；本仓库不是上游作者的发布仓库。保留上游署名、[Apache-2.0许可证](LICENSE)与[NOTICE](NOTICE)。

个人维护，供个人自用、学习和合法辅助交流；无商业服务或效果保证。使用者应核对所在场景规则。本说明不缩减许可证赋予的权利，许可及责任限制以LICENSE为准。
