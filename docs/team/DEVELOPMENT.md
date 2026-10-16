# 开发和验证

应用基线是 Kiwix Android 3.14.0，上游 commit 为 [`111a92799fb17da7728ea829bb04a36c53b66d78`](https://github.com/kiwix/kiwix-android/commit/111a92799fb17da7728ea829bb04a36c53b66d78)。课程协作规则见 [COLLABORATION.md](COLLABORATION.md)，当前交付见 [SPRINT1.md](SPRINT1.md)。

## 准备工具链

需要 JDK 21、Android SDK command-line tools、platform-tools、SDK platform 36、Build Tools 36.0.0 和 NDK 27.3.13750724。仓库自带 Gradle 9.5 wrapper；使用 `./gradlew`，无需另装系统 Gradle。

确认 `JAVA_HOME` 指向 JDK 21，`ANDROID_HOME` 指向自己的 SDK 目录，且 command-line tools 和 platform-tools 在 PATH 中。然后安装所需组件：

```bash
java -version
sdkmanager 'platform-tools' 'platforms;android-36' 'build-tools;36.0.0' 'ndk;27.3.13750724'
```

SDK 的实际路径属于个人环境。如果 IDE 需要 `local.properties`，仅在本机填写 `sdk.dir`。不要提交个人路径、凭据、生产签名文件、工具缓存或构建产物。构建 Debug APK 无需生产签名凭据。

## 构建和测试

在仓库根目录执行：

```bash
./gradlew --max-workers=2 -Dorg.gradle.jvmargs=-Xmx4g :app:assembleDebug
./gradlew --max-workers=2 -Dorg.gradle.jvmargs=-Xmx4g :core:testDebugUnitTest :app:testDebugUnitTest
```

APK 为 `app/build/outputs/apk/debug/app-debug.apk`。测试 HTML 报告为 `core/build/reports/tests/testDebugUnitTest/index.html` 和 `app/build/reports/tests/testDebugUnitTest/index.html`。首次执行会下载依赖，后续构建通常使用缓存。

格式或静态检查可以按改动范围运行 `./gradlew ktlintCheck`、`./gradlew detektDebug` 和 `./gradlew :app:lintDebug`；上游 pre-commit hook 也会运行质量检查。记录实际执行的命令和结果，跳过的检查不能写成已通过。

## 安装和 demo

使用 Android 7.1 / API 25 或以上的测试设备。已有运行环境可直接安装；例如 API 30 模拟器：

```bash
adb devices
adb -s <device-serial> install -r app/build/outputs/apk/debug/app-debug.apk
adb -s <device-serial> shell am start -W -n org.kiwix.kiwixmobile/.main.KiwixMainActivity
```

首次启动完成引导后进入 Library。Sprint 1 的基础 demo 可以使用空书库；这验证安装和启动，不能据此宣称 ZIM 下载、搜索或阅读全部通过。验收时记录 APK 的来源 commit SHA、设备/API、操作步骤、期望结果、实际结果和截图。

## GitHub 自动构建

`.github/workflows/course-ci.yml` 在针对 main 的 PR 和 main 更新时运行：

- **Build debug APK**：构建并上传 `kiwix-debug-<sha>`。
- **Unit tests**：执行 core/app 完整 Debug 单元测试并上传 `unit-test-reports-<sha>`。

两项检查都通过后才进入合并验收。Artifact 是测试用 Debug APK，不是 Play Store 发布，也不是生产签名 release。

下载步骤：仓库 **Actions → Course Android CI → 对应的成功 run → Artifacts → kiwix-debug-<sha>**。先核对该 run 属于 main 且 commit SHA 正确，再解压下载包并安装其中的 APK。PR run 测试的是 GitHub 生成的合并候选，标识以该 run 显示的信息为准；Sprint demo 使用合并后 main 的成功 run。

原 Kiwix 的三份上游 workflow 保存在 `.github/upstream-workflows/`，不在自动执行目录中。它们包含上游发布与多设备矩阵；课程仓库当前只启用上述课程 CI。

## 已有验证与 CI 的区别

引入基线前已完成 Debug APK 构建、25 项定向单测（LanguageTest 10 项，Fat32CheckerTest 15 项），以及 API 30 模拟器安装、冷启动与进入 Library 的验证；检查时崩溃缓冲区为空。随后对同一基线执行完整 core/app Debug 单元测试：core 1491 项、app 719 项，共 2210 项，0 失败、错误或跳过。GitHub CI 的结果以 setup PR 的实际 run 和报告为准。未执行完整上游 instrumentation / benchmark 矩阵，也未据此宣称 ZIM 阅读已验证。

Codex 辅助核对配置、执行环境与运行验证，并准备本次协作文件和 CI。项目报告应持续记录后续 AI 辅助的具体范围与验证结果。
