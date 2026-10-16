# Sprint 1：环境、运行与自动构建

截止：**2026 年 10 月 18 日 23:59，Asia/Shanghai**。Release 1 meeting：**10 月 26 日**。Sprint 2 为 10 月 19–25 日，计划一个基础功能，实施前先与 TA 讨论。后续更新以课程公告为准。

## 目标与验收

> As a student developer, I want a reproducible development environment and an automatically built, runnable Kiwix Android APK, so that the team can develop and verify future changes smoothly.

Supporting requirements：新成员能依据仓库文档配置开发环境；代码变更通过 PR 和多人 review；main 更新后 CI 自动生成 APK；其他成员可以获得该 APK 并安装、运行应用。

验收标准：

- [ ] 团队课程仓库已导入可追溯的 Kiwix Android 源码，保留上游许可证及来源说明。
- [ ] 文档说明所需开发工具、构建和运行步骤；另一位成员按说明完成独立复现。
- [ ] 一个实际合入 main 的改动触发 CI 并成功生成可下载 APK；记录对应 commit 和运行链接。
- [ ] 下载该次 main CI 的 APK，在 Android 测试设备或模拟器安装，启动并进入 Library，记录结果。
- [ ] 关联 Issue 记录任务负责人、story points、验收、PR、review 和 demo 证据。
- [ ] PR 经过两位非作者 review，交付 tag `Sprint1` 指向已验证的 main commit。
- [ ] 仓库可见性为课程要求的 Private，命名符合课程要求；owner 完成设置核对。

仓库可见性调整按当前安排稍后处理，仍是课程要求中的待办；不要在调整前将这一项勾选完成。

## 在 GitHub 上怎么安排

已建立 [Sprint 1 Issue #1](https://github.com/wjin027/Data-science-project/issues/1) 和 [Sprint 1 (Release 1) milestone](https://github.com/wjin027/Data-science-project/milestone/1)，截止日期为 2026-10-18。以 Issue 内的任务 checklist 跟进实际认领与进展，下面的分工用于规划。

| 任务 | 建议负责人 | 完成证据 |
| --- | --- | --- |
| 导入源码，保留来源和许可证 | @hxu129 | 已 review 的源码导入 PR、上游来源说明 |
| 配置构建与 CI，main 自动生成 APK | @hxu129 | 配置 PR、main Actions 成功运行与 APK artifact |
| 配置仓库、milestone 与必要权限 | @wjin027 | 实际设置核对，未完成项明确保留 |
| 按开发文档独立复现环境 | @Sli266 | 实际步骤、工具版本、结果及文档修复 PR |
| 安装 CI APK，完成运行验收和 demo | @Sli266 | 对应 commit、安装与启动结果、截图或视频 |
| 汇总交付、核对 tag 和后续计划 | @wjin027 | 交付记录、`Sprint1` tag、Sprint 2 候选需求 |

这些是**初始建议**，成员应在 Issue 中确认或调整，并共同给 story 和任务估点，填写 `1 / 2 / 3 / 5 / 8`。不预先把“建议负责人”当成已认领，不把示例点数当成真实估算。具体流程见 [协作指南](COLLABORATION.md)。

## 最小 demo

1. 打开 Sprint 1 Issue，说明目标和验收标准。
2. 展示一个已合入 main 的 PR，指出它关联的任务、两位成员 review 和 Checks。
3. 打开对应的 main Actions 运行，下载 APK artifact，核对 commit。
4. 安装 APK 并启动 Kiwix，进入 Library，展示运行结果。空书库不代表运行失败；离线阅读若没有测试 ZIM 内容，应明确说明尚未检查。
5. 展示开发文档、已知限制、`Sprint1` tag 与 Sprint 2 的候选基础功能。候选功能在与 TA 确认前保持“计划”状态。

## 交付记录：验收后填写

不要把此前的本地验证自动填成 GitHub CI 或其他成员的验收。

| 项目 | 实际结果 / 链接 |
| --- | --- |
| Sprint 1 Issue / milestone | [Issue #1](https://github.com/wjin027/Data-science-project/issues/1) / [milestone](https://github.com/wjin027/Data-science-project/milestone/1) |
| 交付 main commit | 待补充 |
| 已合并的实现 / 文档 PR | 待补充 |
| 两位成员 review | 待补充 |
| main CI 运行与 APK | 待补充 |
| 独立环境复现人员、步骤与结果 | 待补充 |
| 安装运行的 Android 版本与结果 | 待补充 |
| demo 截图或视频 | 待补充 |
| `Sprint1` tag | 待补充 |
| 仓库设置核对及未完成事项 | 待补充 |
| 本地基线预检 | 上游 `111a92799fb17da7728ea829bb04a36c53b66d78`：Debug APK 构建、2210 项 core/app 单测（0 失败/错误/跳过）、API 30 安装并进入 Library；GitHub CI 与独立队友验收另行记录 |
| 已知限制、失败检查与下一步负责人 | 未验证 ZIM 阅读或完整上游 instrumentation / benchmark 矩阵；main CI、队友 review、独立验收与私有设置仍待完成 |
| AI 辅助内容与实际人工验证 | 待补充 |

## 课程来源

- [Sprint 1 作业与截止时间](https://hkust-gz.instructure.com/courses/3865/assignments/29334)
- [Sprint 1 公告](https://hkust-gz.instructure.com/courses/3865/discussion_topics/33937)
- [Sprint 1 详细指南](https://docs.google.com/document/d/1uRzBApciEz4IH1_8lwjQ-E6G4wRbv4X509zdLIPSN-k/edit)
- [GitHub 使用要求](https://docs.google.com/document/d/18ynuiH46dA5RqgOv8XKfh29hleetVW7bUd-yUtekmSA/edit)
