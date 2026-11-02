# skyline654654

## 置顶项目

### [BiliSail · 仓颉 / 原生鸿蒙适配](https://github.com/skyline654654/BiliSail)

对标 [CKopoer/BiliSail](https://github.com/CKopoer/BiliSail)（Flutter + Dart 的第三方哔哩哔哩客户端）的
**仓颉语言 + HarmonyOS 原生**适配分支。在保留上游全部功能的前提下新增：

| 能力 | 说明 |
| --- | --- |
| 底栏中间「+」 | 与哔哩哔哩手机版一致的创作入口，可发**视频**与**图文**，含草稿校验与上传进度 |
| 鸿蒙沉浸光感 | 全局生效：只在 `ThemeData` 的 chrome 槽位改写，所有 Material 系统组件自动获得玻璃层；鸿蒙端底栏改由 **ArkUI 系统组件**渲染（`SymbolGlyph` + `backgroundBlurStyle` + API 26 `systemMaterial`） |
| 广告屏蔽 | 推荐/搜索/动态移除 commerce 卡片（`AdCardClassifier`），弹幕广告过滤 |
| AI 视频广告跳过 | 社区片段（BilibiliSponsorBlock）+ 弹幕「空降」时间码聚类（`AirstrikeDetector`），支持手动/自动跳过与置信度门控 |
| 仓颉核心 | `cangjie/` cjpm 工程，`@C` 导出片段合并与边界聚类，C ABI 只传 `Int64` |
| 原生鸿蒙工程 | `harmony/` Stage 模型：沉浸式窗口、避让区监听（`TYPE_SYSTEM` + `TYPE_NAVIGATION_INDICATOR`）、原生底栏、`bindSheet` 创作面板 |

**技术要点**：适配方案全部落在 ArkUI 原生壳 + Flutter 内容的双层结构上，Dart 侧通过
`describe()` 能力协商决定是否绘制自己的底栏，非鸿蒙平台行为与上游一致。

**验证状态**：Dart 侧已通过 `dart format` 解析与 import 闭合检查；ArkTS 与仓颉侧**尚未编译**
（本机无 DevEco Studio / 仓颉 SDK），详见仓库 `docs/validation/adaptation-status-2026-11-02.md`。

---

*其他：* [AQUA-API](https://github.com/skyline654654/AQUA-API)
