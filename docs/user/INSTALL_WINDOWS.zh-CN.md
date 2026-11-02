<!-- Modified by Suxifang for Amitoufo (2026); based on JWM0203/MeetingCopilot. See NOTICE and MODIFICATIONS.md. -->
# Windows 安装与更新

请使用 [Suxifang/Amitoufo-Releases](https://github.com/Suxifang/Amitoufo-Releases/releases) 中的安装包。这是公开下载仓库，已发布的安装包无需登录；开发源码在另一个私有仓库维护。

- 推荐 `Amitoufo-<版本>-win-x64-setup.exe`：按当前用户安装，创建桌面／开始菜单入口。
- 免安装版为 `Amitoufo-<版本>-win-x64-portable.exe`。
- 首次配置转录与回答服务；普通云方案无需另装 Node.js 或 Python。
- 升级前退出旧进程并备份 `%APPDATA%\MeetingCopilot`，再运行新安装包。不要删除个人资料目录。
- Ctrl+B 呼出已运行程序；首次 r21 解压目录及旧快捷方式需在确认新版后自行清理。
- 对照 SHA256SUMS.txt 或同名 .sha256 校验下载，未签名版本的系统提示请先核对来源，不要关闭系统防护。

beta.4 及更早版本需手动覆盖安装一次 beta.5 或更高版本，切换更新地址。无需先卸载或重填现有配置；不要清理 AppData。之后点击软件名下方“更新”，检查、下载并退出安装。免安装版继续手动更新。

完整操作、数据位置、功能与限制见[安装与使用手册](../USER_GUIDE.zh-CN.md)。下载仓库的 `Source code` 仅是说明文档压缩包，不是安装程序或应用源码。
