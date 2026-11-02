# skyline654654

## 置顶项目

### [bili easy · 仓颉 / 原生鸿蒙适配](https://github.com/skyline654654/BiliSail)

对标 [CKopoer/BiliSail](https://github.com/CKopoer/BiliSail)（Flutter + Dart 的第三方哔哩哔哩客户端）的
**仓颉语言 + HarmonyOS 原生**适配分支，应用名 **bili easy**（包名 `dev.bilisail.client`）。
在保留上游全部功能的前提下新增：

| 能力 | 说明 |
| --- | --- |
| 底栏中间「+」 | 与哔哩哔哩手机版一致的创作入口，可发**视频**与**图文**，含草稿校验与上传进度 |
| 鸿蒙沉浸光感 | 全局生效：只在 `ThemeData` 的 chrome 槽位改写，所有 Material 系统组件自动获得玻璃层；鸿蒙端底栏由 **ArkUI 系统组件**渲染（`SymbolGlyph` + `backgroundBlurStyle` + API 26 `systemMaterial`） |
| 广告屏蔽 | 推荐/搜索/动态移除 commerce 卡片（`AdCardClassifier`），弹幕广告过滤 |
| AI 视频广告跳过 | 社区片段（BilibiliSponsorBlock）+ 弹幕「空降」时间码聚类（`AirstrikeDetector`），支持手动/自动跳过与置信度门控 |
| 仓颉核心 | `cangjie/` cjpm 工程，`@C` 导出片段合并与边界聚类，C ABI 只传 `Int64` |
| 原生鸿蒙工程 | `harmony/` Stage 模型：沉浸式窗口、避让区监听（`TYPE_SYSTEM` + `TYPE_NAVIGATION_INDICATOR`）、原生底栏、`bindSheet` 创作面板 |

## 实测证据（2026-11-02）

| 项 | 状态 |
| --- | --- |
| Dart 适配层 | `flutter analyze` **0 issues**（13 个改动/新增文件）；`verify/domain-checks.dart` **24/24**；组件测试 **4/4** |
| 仓颉核心 | `cjpm build` 通过；与 Dart 实现 **8/8 逐行等价**（同一份 fixture 对比） |
| 原生鸿蒙 | `hvigorw assembleHap` **BUILD SUCCESSFUL**；`codelinter` Errors **0** |
| 签名 | AGC 发布证书 + 发布 Profile；官方 `hap-sign-tool verify-app` → **Verify success**（314,749 B） |
| 真机/云调试 | **未运行**（尚未安装到设备，见仓库 `docs/harmony-conformance.md` 第 5 节） |

**技术要点**：适配方案落在 ArkUI 原生壳 + Flutter 内容的双层结构上，Dart 侧通过 `describe()`
能力协商决定是否绘制自己的底栏，非鸿蒙平台行为与上游一致。接口选型逐条对照华为官方文档，
并单列「明确不用 + 原因」，见 `docs/harmony-conformance.md`。

**开源引用**：上游与协议参考的许可状态、构建工具（不随仓库分发）说明见
`docs/references-adaptation.md`。

---

*其他：* [AQUA-API](https://github.com/skyline654654/AQUA-API)