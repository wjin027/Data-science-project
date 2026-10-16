# 团队协作指南

本指南用于 DSAA2044 的 Kiwix Android 课程仓库。我们在一个 Issue 中写清目标、验收和任务，再由分支上的 PR 实现；main 保存团队已 review、能够交付的版本。Kiwix 的上游贡献说明仍然适用；向上游投稿前另行核对其最新要求。

## 成员与初始分工

以下是根据当前仓库成员提出的 Sprint 1 初始安排，供三人确认和调整，不代表成员已经接受任务。后续 Sprint 轮换实现、验收和 review 角色，让每位成员都有实际参与记录。

| 成员 | Sprint 1 建议负责 | 需要留下的结果 |
| --- | --- | --- |
| @hxu129 | 构建环境、自动构建与故障修复 | 可复现的开发步骤、CI PR 和运行链接 |
| @wjin027 | 仓库管理、Sprint 协调与交付版本 | 设置检查、milestone、review 和交付 tag |
| @Sli266 | 独立安装验收、运行检查与 demo | 使用交付 APK 的验收记录、截图或视频、demo 步骤 |

任务的实际负责人写在 Issue 的 checklist 中。Issue 的 assignee 负责跟进整体进度；它不替代每项任务的负责人。管理权限属于 @wjin027，需要管理员权限的设置由 owner 处理。

## 1. 开始工作：先把目标写进 Issue

在 **Issues → New issue** 选择 User story、Bug 或 Setup / task 模板。先搜索已有 Issue，避免重复工作。

- **功能**使用 user story：`As a [角色], I want [目标], so that [收益]`。先描述使用者得到的结果。
- **Supporting requirements** 描述具体行为和质量要求，例如空结果怎么显示、失败后能否重试。
- **验收标准**描述别人怎样判断完成，写成可执行的操作及预期结果。
- **任务 checklist**拆出实现、测试、文档和 demo 等具体工作，每项注明 `@负责人`。直接在同一个 Issue 中维护，无需为每个小步骤另开 Issue。
- **Bug**写最小复现步骤、预期与实际结果；**setup**写需要得到的环境或交付结果及完成标准。

一个功能示例（仅演示格式，尚未选定为课程功能）：

> As a reader, I want to see a clear empty-library message, so that I know how to add my first offline book.
>
> Supporting requirement：书库为空时显示引导；已有图书时显示原有书库；引导操作进入现有的添加内容入口。
>
> 验收：在空书库启动可见引导且入口可点击；导入一本测试图书后，引导消失且图书可打开。

这里的“用哪个控件、修改哪个类”可以在技术讨论或任务中记录，不应代替用户目标。

Issue 选择类型 label（`feature`、`bug`、`setup` 或 `documentation`），加入对应 milestone，例如 `Sprint 1 (Release 1)`。Sprint 开始前共同讨论范围及估点；不确定的功能先与 TA 确认。

### Story points 怎么用

使用 `1 / 2 / 3 / 5 / 8` 比较工作量、复杂度和不确定性。先给整个 story 估点；依照 Sprint 1 指南，在 checklist 每项后也补充任务点数，并说明整体估点是否采用任务之和。避免把两种数字重复算入统计。

`1` 可代表已知的小改动，`3` 可代表需要实现与验证的一般工作，`8` 表示范围或不确定性较大，应考虑缩小。数值需要团队讨论；它们不是小时数，也不能用来衡量个人贡献。模板中的点数占位不是已完成的估算。

## 2. 实现：一个目标，一条分支，一个 PR

先确认自己没有覆盖其他人的未提交修改，然后从最新 main 创建分支。以下的 `123` 是示例 Issue 编号，请替换成实际编号。

```bash
git switch main
git pull --ff-only
git switch -c codex/123-empty-library
```

默认使用 `codex/<Issue编号>-<简短主题>`；团队另有约定时在 Issue 中写明。避免多人直接在同一条工作分支修改相同文件；需要接手时先在 Issue 中说明。

首次提交前检查 Git 身份：

```bash
git config user.name
git config user.email
```

邮箱应为自己 GitHub 账号中已登记并验证的邮箱，或 GitHub 提供的个人 noreply 邮箱，确保贡献记录归属正确。不要把个人邮箱、token、签名密钥、`local.properties` 或本机环境路径写进仓库文档。个人环境配置留在本地；共享配置用无密钥的示例。

每次提交只处理相关改动，在提交信息中引用 Issue，并在正文说明对应任务。例如（编号仍为示例）：

```bash
git add <本次相关文件>
git commit -m "#123 Add empty-library guidance"
git push -u origin codex/123-empty-library
```

在 GitHub 新建 PR，base 选 `main`，填写自动出现的 PR 模板。PR 完整解决 Issue 时写 `Closes #123`；只完成其中一项任务时写 `Refs #123` 并注明任务，避免提前关闭整个 story。配对开发或共同决策应按真实参与情况记录，不能代替独立 review。

空仓库建立 main 必须有一个起始提交；仓库仅用最小 README 完成这一次 bootstrap。之后的源码导入、配置、功能、修复和文档修改全部通过 PR 合入 main。

## 3. Review：三人组由作者之外的两人检查

作者完成相关本地验证后，把 PR 设为 Ready for review，并邀请另外两位成员 review。比如 @hxu129 的 PR 由 @wjin027 和 @Sli266 review；其他作者依此轮换。AI 辅助检查不能替代两位成员的 review。

Reviewer 至少确认：

- 改动解决了关联 Issue 的目标，验收步骤足以复现结果。
- 关键行为正确，已有功能未受到明显影响；必要的单测与失败情况得到检查。
- PR 的 Checks 与测试说明一致，没有把跳过的测试写成通过。
- 文档能帮助下一位成员操作，日志和截图没有密钥或私人信息。

在 **Files changed** 提出具体问题；阻止合并的问题选 **Request changes**，检查完成且无阻塞项后选 **Approve**。作者回应并修复问题；新增实质改动后，请 reviewer 再确认相关部分。不要为了凑 review 数直接批准未读的 PR。

满足以下条件才合入 main：两位非作者完成 review、阻塞讨论解决、所需 CI checks 成功、验收和文档已更新。合并时采用仓库可用的正常 PR 合并方式，保留 Issue/PR 关联；合并后可删除已完成分支。

Owner 可在 **Settings → Rules → Rulesets**（或 **Branches** 的保护规则）针对 main 配置：要求 PR、两位 approval、解决 review 讨论和必要 status checks，并限制绕过规则。是否支持这些设置取决于仓库可见性及 GitHub 套餐。必须实际检查生效状态；仅有本指南、reviewer 请求或 CODEOWNERS 文件都不等于强制两人 approval。若暂不能强制，仍按上述团队约定操作，并明确记录限制。

## 4. CI 和 APK：用 main 的真实产物验收

PR 页的 **Checks** 是自动验证结果；失败时打开 job 日志定位第一处有效错误，修复后推送到同一分支。绿色构建只能证明该 workflow 执行的步骤成功；它不自动证明模拟器安装、界面或用户行为正常。

课程使用 [Course Android CI](../../.github/workflows/course-ci.yml)。`Build debug APK` 和 `Unit tests` 两个 job 都成功后才满足本指南的 CI 合并条件；测试报告 artifact 为 `unit-test-reports-<sha>`。本机准备和构建命令见 [开发指南](DEVELOPMENT.md)。

PR 合并后：

1. 打开 **Actions**，进入 **Course Android CI** workflow。
2. 选择这次合并产生的 **main** 运行，核对 commit 与交付版本一致。
3. 等待两个 job 成功，打开运行页面底部 **Artifacts**，下载 `kiwix-debug-<sha>` APK artifact 并解压。
4. 在测试设备或模拟器安装 APK，按 Issue 的验收步骤检查。记录设备 Android 版本、APK 对应 commit、预期和实际结果。
5. 把 Actions 运行链接、必要截图或视频和验收结论补充到 Issue / PR。产物下载需要 GitHub 登录，且 artifact 有保留期限；交付前确认仍可获取。

PR 检查通过后，仍需核对合并后 main 的实际运行和产物；workflow 文件存在本身不代表 CI/CD 完成。自动生成测试 APK 与发布正式应用是不同的交付步骤；不要提交正式签名密钥。

## 5. 完成 story 和 Sprint

Story 完成前：勾选实际完成的任务，记录验证结果和 demo 步骤，链接对应 PR。存在未完成项就保留 Issue 打开；把阻塞原因和下一步负责人写清楚。

Sprint 结束时：

1. 核对 milestone 中每项 Issue 的验收状态，未完成的工作如实记录并重新安排。
2. 按 [Sprint 1 交付清单](SPRINT1.md) 汇总交付 commit、main CI 运行、可下载 APK、demo 和已知限制。
3. 核对交付内容已经过 PR review 后，由负责交付的成员在已验证的 main commit 上建立 tag（Sprint 1 使用 `Sprint1`），并推送 tag。先确认 tag 不存在；已有 tag 不覆盖、不移动。
4. Sprint / release 报告通过 Issue、PR、review、CI 和 demo 的链接说明实际完成工作，并准确披露 AI 辅助内容与人工验证。报告不把计划、排队任务或本地成功当成团队已验收。

示例命令中的 `<verified-main-commit>` 必须替换成实际核对的完整提交号：

```bash
git fetch origin --tags
git tag -a Sprint1 <verified-main-commit> -m "Sprint 1 verified delivery"
git push origin Sprint1
```

线下讨论产生需求或技术决定后，把结论、理由、待确认项补到相关 Issue，避免重要信息只留在聊天里。无需另开一套管理工具。

## 课程来源

- [DSAA2044 课程主页](https://hkust-gz.instructure.com/courses/3865)
- [Using GitHub for DSAA2044](https://docs.google.com/document/d/18ynuiH46dA5RqgOv8XKfh29hleetVW7bUd-yUtekmSA/edit)：Issue、任务、估点、PR、多人 review 与 tag 要求。
- [Sprint 1 详细指南](https://docs.google.com/document/d/1uRzBApciEz4IH1_8lwjQ-E6G4wRbv4X509zdLIPSN-k/edit)：运行环境与 main 自动生成 APK。

本指南中的三人分工、估点尺度和操作约定为团队建议；课程后续公告或 TA 的明确要求优先。
