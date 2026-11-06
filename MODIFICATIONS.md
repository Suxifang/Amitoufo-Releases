# 修改清单

当前交付版本：beta.20（2026-11-06），收录下方已验收的单次生成、完整组题、多问点和换题边界修复。后续条目为各阶段当时状态；源码归档、安装及草稿以本轮交付记录为准。当前回答实现与最终18条真实语音事件入口案例的被测实现相同，本轮只升级版本和交付文档。

当前补充（2026-11-06，电脑语音优先验收）：真实隔离程序回放发现系统声音转录会先在 `appendSegment` 合并“跳过的旧题＋100ms后显式下一个问题”，实际模型因而先答旧体育题再答新学习题。新增回归先失败，现将显式换题判定复用于转录展示合并和组题，保留独立话题边界；相关8文件193项及完整76文件902项JS/TS、8项Python、20项分发、类型/构建通过。原失败实际请求/答案与后续原生语音验收结果见同一重点修复报告及 `priority-native-*` 证据；不能以打字测试替代语音事件入口，也不能将事件重放称为真实音频识别测试。

当前未发布修复（2026-11-06，上午手机AI面原任务续验）：移除组题24片段/2400字和补充题尾截1200字的静默丢前文，保留话轮/来源/时长边界；情境前提跨自然停顿保留，显式换题终止拼接。多问点追问不再被“只答第一步”限制，提示按原题顺序覆盖各问点。10项决定性回归修复前全部失败；修复后7文件173项及完整验证76文件900项JS/TS、8项Python、20项分发、类型和构建通过。固定三案例、两种模式修复前后共12次真实 `deepseek-flash` 请求；长三问题修复前两档漏第一问，修复后6条均切题并覆盖所有问点。项目与源码规则明确允许根据简历主线包装、每次回答逻辑更新须真实验收，并要求手机/电脑/打字共用回答逻辑；验收电脑语音优先、手机其次，手机覆盖双方发言混转录；不再以严格细节越界为质量门槛。详见 `../reviews/2026-11-06-上午实测问题重点修复与验收.md`。尚未覆盖日常安装、Git提交/推送和公开发布，历史结果按下文保留。

以下为此前阶段记录，以顶部当前记录及对应报告为准。

未发布续验与记录（2026-11-06）：单次生成候选增加 `ANSWER/NEED_BACKGROUND` 首行协议及相应解析/分流测试、后台模拟响应；缺背景仅显示中性资料提示。最新56条真实文本逐题审读为39参考、14仅资料提示、3失败，整体质量未通过；明确分工误拦和未知被否定仍在。E09显式否定补提示、E10方法参考均未合入，失败证据保留。上一阶段程序检查863项JS/TS、8项Python、20项分发及构建通过，本次留痕未重跑。项目根及源码AGENTS补追溯规则，唯一问题台账保留根因、反例、实验取舍和复验条件；完整续验记录位于 `../reviews/2026-11-06-回答修复续验与追溯记录.md`。本轮未打包、安装、提交/推送、更新草稿或发布，日常仍为旧beta.19。

未发布修复（2026-11-06，手机AI面复盘）：按“保留经历主线、允许合理细节加工”的通用规则，将共用回答链改为 `electron/llm/answerGeneration.ts` 单次生成和流式呈现，移除默认独立事实核验及简历摘录替换。精简提示，补齐礼貌情境问法、独立新题上下文隔离和短追问范围。真实调用工具记录请求编号、实际提示指纹、完成原因与人工审读状态；程序检查不代替最终回答验收。资料缺失时过度否定、混合收音误认等边界仍需处理，本条不表示已安装或已通过发布验收。

beta.19 补充（2026-11-06）：新增 `electron/llm/answerGrounding.ts`，在共用回答入口用同一所选服务核验个人经历，隐藏未核验草稿；修订仅能选择带来源的原始事实，通用解释不能再增加第一人称经历。新增核验路由、资格限定、取消、失败及显示隔离测试，以及 `tools/answer-quality-live.ts` 和完全虚构的多背景样例。更新后台回归的本机核验服务响应；实际模型、用量和延迟单独实测，不将后台模拟视为质量验收。

未发布补充（2026-11-05）：新增 `electron/asr/speechActivity.ts` 与 `shared/speechActivity.ts`，将按声道的讲话状态及成功转录完成信号传至共用回答队列；组装同话轮分句、阻挡未讲完及未转录完整的题目，补齐F8无文字尾音。共用提示构建补充追问新增条件、完整经历题与有界旧稿来源限制。新增话轮单测及 `tools/spoken-turn-regression.mjs`，维护连续负载检查的转录时间边界和旧稿标签断言。窗口采集保护实现未改。

beta.11 补充：新增 `shared/continuousAnswerQueue.ts` 保存各独立终稿及等待截止时间，自动答改为逐题调度；去重记录覆盖多个终稿，清空转录同步取消旧待答。新增纯逻辑和真实打包程序回归，并接入候选构建检查；后台启动工具统一清理继承的 Electron Node 模式及旧 MC 测试标记。连续负载检查同时核对题目内容、顺序和保存标签，避免只数请求漏掉替换或重复。未修改提示词或窗口采集保护。

beta.10 补充：新增 `src/components/AnswerText.tsx` 收紧段间距，存储及复制保留原文；增加阅读与重复操作回归，扩展跨模型交叉检查。取消测试按具体问题等待断流，收音测试显式隐藏托盘、禁用回答热键，不修改日常配置。

beta.9 补充：增加全局回答篇幅与主界面快捷切换，设置和全部输入使用同一保存项；共用提示构建器适配两档篇幅与追问。新增 `shared/answerDetail.ts`、`test/answerDetail.spec.ts` 和 `tools/answer-detail-restart.mjs`，扩充三输入与设置回归。

本项目基于 JWM0203/MeetingCopilot v0.2.0-beta.1。以下为首个独立发布版本相对本地上游基线 12ef779 的修改／新增文件，后续变化继续记录在 Git 历史和 CHANGELOG.md。保留原有许可证和署名。

beta.3 补充：统一日常打字与语音面试回答入口、增加名称下方更新入口、调整材料栏换行；新增 `tools/unified-answer-regression.mjs`，并纳入发布检查。

beta.4 补充：修复配置向导的系统声音权限与异步采集取消，新增 `electron/capturePermission.ts`、对应单测及 `tools/setup-audio-regression.mjs`，并纳入发布检查。beta.3 候选未正式发布，由 beta.4 一并交付。

beta.5 补充：将私有源码与公开下载分仓，新增 `shared/releaseRepository.ts`、`deploy/public-release.mjs`、公开下载 README 和发布边界回归；修改更新源、帮助链接、构建元数据、发布工作流及文档。安装标识与用户资料位置保持原值，不修改收音、回答或窗口采集保护逻辑。

beta.6 补充：将回答模型、回答语言和延迟 HUD 移入设置；设置独占内容区、正文滚动、固定保存栏并保留面试阅读状态。新增设置布局的真实程序后台回归；HUD 偏好使用兼容旧配置的可选字段，不改变收音和回答提示词。

beta.7 补充：统一文本模型配置与思考参数，读取后台模型及能力元数据；保留原推荐引导，删除高级设置中的重复文本模型字段。三种输入、连接测试、预热及翻译共享参数处理；新增地址变更时的 Key 保护、旧配置兼容与真实程序回归。不改变窗口采集保护与回答提示词。

beta.8 补充：修复软件更新布局；按服务地址分别保存加密 Key 与模型配置，并保留切换草稿。缺少能力元数据时使用服务商默认，手动值标为未验证；解析模型专属的强度错误并阻止已知无效选择。新增服务切换、密钥隔离、强度错误与更新页面布局回归。

## 修改的上游文件

- `build/icon.ico`
- `build/icon.png`
- `resources/tray/tray.png`
- `resources/tray/tray@2x.png`
- `resources/tray/trayTemplate.png`
- `resources/tray/trayTemplate@2x.png`
- `tools/make-tray-icons.py`
- `.github/workflows/ci.yml`
- `.github/workflows/release.yml`
- `.gitignore`
- `README.md`
- `README.zh-CN.md`
- `docs/user/INSTALL_WINDOWS.en.md`
- `docs/user/INSTALL_WINDOWS.zh-CN.md`
- `docs/user/QUICK_START.en.md`
- `docs/user/QUICK_START.zh-CN.md`
- `docs/user/TROUBLESHOOTING.en.md`
- `docs/user/TROUBLESHOOTING.zh-CN.md`
- `docs/windows/SETUP.md`
- `electron-builder.yml`
- `electron.vite.config.ts`
- `electron/asr/aliyunRealtimeEngine.ts`
- `electron/asr/cloudEngine.ts`
- `electron/asr/contract.ts`
- `electron/asr/worker.ts`
- `electron/asrHost.ts`
- `electron/diagnostics.ts`
- `electron/funasrSidecar.ts`
- `electron/knowledge.ts`
- `electron/llm/adapter.ts`
- `electron/llm/prompts.ts`
- `electron/llm/vision.ts`
- `electron/main.ts`
- `electron/preload.ts`
- `electron/sessions.ts`
- `electron/settings.ts`
- `electron/setupWindow.ts`
- `electron/tray.ts`
- `electron/uiStrings.ts`
- `package-lock.json`
- `package.json`
- `shared/docsLinks.ts`
- `shared/platform.ts`
- `shared/protocol.ts`
- `shared/providerCatalog.ts`
- `shared/textHeuristics.ts`
- `shared/transcript.ts`
- `shared/trayMenu.ts`
- `src/App.tsx`
- `src/audio/loopbackCapture.ts`
- `src/audio/micCapture.ts`
- `src/components/AnswerSession.tsx`
- `src/components/DiagnosticsPanel.tsx`
- `src/components/HelpPanel.tsx`
- `src/components/SettingsPanel.tsx`
- `src/components/StatusBar.tsx`
- `src/components/TranscriptPanel.tsx`
- `src/i18n.tsx`
- `src/index.html`
- `src/main.tsx`
- `src/onboarding/OnboardingApp.tsx`
- `src/onboarding/i18n.ts`
- `src/onboarding/steps/ConnectionStep.tsx`
- `src/public/pcm-worklet.js`
- `src/setup.html`
- `src/styles.css`
- `test/diagnostics.spec.ts`
- `test/docsLinks.spec.ts`
- `test/llm.spec.ts`
- `test/platform.spec.ts`
- `test/settings.spec.ts`
- `test/transcript.spec.ts`
- `tools/packaged-smoke.mjs`
- `tools/seed-asr.cjs`
- `tsconfig.web.json`

## 新增文件

- `build/README.md`
- `build/icon.svg`
- `build/icon-small.svg`
- `build/icon-frames/icon-{16,20,24,32,40,48,64,96,128,256}.png`
- `tools/make-app-icons.py`
- `.gitattributes`
- `CHANGELOG.md`
- `MODIFICATIONS.md`
- `NOTICE`
- `deploy/Start-Amitoufo.cmd`
- `deploy/Verify-Package.ps1`
- `deploy/build-windows.ps1`
- `deploy/release-files.mjs`
- `deploy/render-manual.py`
- `deploy/sync-version.mjs`
- `deploy/verify-release.mjs`
- `docs/ANSWER_QUALITY.zh-CN.md`
- `docs/DEPLOYMENT.zh-CN.md`
- `docs/PRIVACY_FORK.zh-CN.md`
- `docs/PRIVACY_VALIDATION.zh-CN.md`
- `docs/RELEASING.zh-CN.md`
- `docs/STABILITY_VALIDATION.zh-CN.md`
- `docs/USER_GUIDE.zh-CN.md`
- `docs/releases/1.0.0-beta.1.md`
- `docs/upstream/README.md`
- `docs/upstream/README.zh-CN.md`
- `electron/hotkeys.ts`
- `electron/llm/followupContext.ts`
- `electron/llm/materialSelection.ts`
- `electron/llm/requestLifetime.ts`
- `electron/native.d.ts`
- `electron/native/WheelBridge.cs`
- `electron/qaSession.ts`
- `electron/regionPreload.ts`
- `electron/shutdown.ts`
- `electron/storageSafety.ts`
- `electron/wheelBridge.ts`
- `electron/windowDrag.ts`
- `electron/windowProtection.ts`
- `shared/answerSubmission.ts`
- `shared/answerTiming.ts`
- `shared/buildInfo.ts`
- `shared/continuousAnswer.ts`
- `shared/interviewContext.ts`
- `shared/mouseRouting.ts`
- `shared/pendingAnswer.ts`
- `shared/questionAssembly.ts`
- `shared/settingsSnapshot.ts`
- `shared/storageRecovery.ts`
- `shared/windowSize.ts`
- `src/audio/pcmCapture.ts`
- `src/components/InWindowSelect.tsx`
- `src/components/InWindowTooltip.tsx`
- `src/components/MousePassthrough.tsx`
- `src/components/ProtectedCursor.tsx`
- `src/components/WheelRouting.tsx`
- `src/components/WindowSizeControl.tsx`
- `src/components/overlayControls.css`
- `src/components/useAnswerReading.ts`
- `src/useSettingsSnapshot.ts`
- `test/answerFailureDisplay.spec.tsx`
- `test/answerLatency.spec.ts`
- `test/answerQuality.spec.ts`
- `test/answerReading.spec.tsx`
- `test/asrHost.spec.ts`
- `test/asrStability.spec.ts`
- `test/asrWorkerLifecycle.spec.ts`
- `test/audioCapture.spec.tsx`
- `test/audioInterruption.spec.tsx`
- `test/autoStartBoundary.spec.ts`
- `test/cloudAsrTimeout.spec.ts`
- `test/complexQuestions.spec.ts`
- `test/continuousAnswer.spec.ts`
- `test/followupContext.spec.ts`
- `test/globalAnswerQuality.spec.ts`
- `test/interviewContext.spec.ts`
- `test/llmStability.spec.ts`
- `test/materialSelection.spec.ts`
- `test/mouseRouting.spec.ts`
- `test/overlayPrivacy.spec.tsx`
- `test/pcmWorklet.spec.ts`
- `test/phoneManual.spec.ts`
- `test/qaSession.spec.ts`
- `test/questionAssembly.spec.ts`
- `test/requestLifetime.spec.ts`
- `test/sessionRecovery.spec.ts`
- `test/settingsSnapshot.spec.ts`
- `test/shutdown.spec.ts`
- `test/sidecarLifecycle.spec.ts`
- `test/storageSafety.spec.ts`
- `test/trayPrivacy.spec.ts`
- `test/visionStability.spec.ts`
- `test/wheelBridge.spec.ts`
- `test/windowDrag.spec.ts`
- `test/windowProtection.spec.ts`
- `test/windowSize.spec.ts`
- `tools/asr-origin-regression.mjs`
- `tools/autostart-regression.mjs`
- `tools/device-regression.mjs`
- `tools/phone-hotkey-regression.mjs`
- `tools/privacy-audit-helpers.mjs`
- `tools/privacy-region-regression.mjs`
- `tools/request-lifecycle-regression.mjs`
- `tools/session-close-regression.mjs`
- `tools/stability-soak.mjs`
- `tools/startup-regression.mjs`

- 1.0.0-beta.2：加入由用户发起的 Windows 安装版更新流程与更新元数据；检查与下载不涉及个人数据，保留原窗口保护机制。
- 1.0.0-beta.5：在 `build/installer.nsh` 加入原生文件占用预检，在旧版卸载前报告被占用文件；`tools/installer-file-lock-regression.mjs` 使用真实 NSIS 与隔离虚构文件核验阻止安装和释放后重试。
