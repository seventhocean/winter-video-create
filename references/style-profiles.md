# Winter Video Style Profiles

## 用途

风格 Profile 只负责“看起来怎样”和“动起来怎样”，不负责决定口播讲什么、舞台使用哪些空间锚点或素材放在哪里。所有 Profile 都必须兼容同一份 `scene` / `layers[]` 契约。

## 选择规则

按以下优先级选择：

1. 用户明确指定的风格名称或参考视频。
2. 项目已有的栏目风格和历史成片。
3. 内容类型的默认建议。
4. 没有上下文时使用 `clinical-tech`。

一条视频默认只使用一个主 Profile。章节可以使用该 Profile 的 `chapterAccent` 改变强调色和环境色，但不能随意更换字体、卡片材质和运动语法。需要明显换风格时，必须把它写成一次舞台转场并在分镜中说明原因。

## Profile 契约

每个风格至少定义：

```json
{
  "styleProfile": "clinical-tech",
  "tokens": {
    "background": "#07121d",
    "surface": "rgba(4,17,31,.88)",
    "text": "#f5f9ff",
    "mutedText": "#afc0d2",
    "accent": "#32aeff",
    "success": "#42df86",
    "warning": "#ffc34d",
    "danger": "#ff6577"
  },
  "typography": {
    "display": "system-sans-heavy",
    "body": "system-sans",
    "mono": "Menlo"
  },
  "motion": {
    "entrance": "power4.out",
    "emphasis": "easeOutCubic",
    "transition": "cross-stage"
  },
  "surface": "dark-glass",
  "density": "editorial-3-to-6"
}
```

实现组件读取 tokens，不在 `Stage`、`DataStory` 或 `StageTopology` 中硬编码颜色和字体。缺少字体时使用明确的 fallback，不把字体文件复制进每个视频项目。

## 内置风格

### `clinical-tech`（默认）

- 适合：AI 工具、工作流、API、Skill、产品教程和数据解释。
- 视觉：深蓝黑背景、冷色玻璃、蓝 / 绿 / 黄 / 红状态色。
- 材质：低透明玻璃、细边框、轻微模糊；避免游戏 HUD 和厚重霓虹。
- 运动：路径先行、节点接通、数字增长、状态替换；进入利落，停留清晰。
- 密度：3–6 个可见元素，适合整屏多锚点舞台。

### `editorial-cinema`

- 适合：观点、行业判断、个人经验和故事化口播。
- 视觉：近黑背景、象牙白文字、少量朱红或钴蓝强调。
- 材质：平面纸张、细线、照片裁切和大字号标题；减少玻璃卡。
- 运动：慢速滑入、局部放大、章节色彩转场和留白，避免连续弹跳。
- 密度：2–5 个元素，允许更大的空白和更长的阅读停留。

### `terminal-mono`

- 适合：代码、命令行、系统协议、技术排错和开发者工具。
- 视觉：炭黑底、磷光绿或琥珀色、单色线框、等宽字体。
- 材质：终端窗口、日志行、光标、扫描线；扫描线只能作为低注意力环境层。
- 运动：逐行输出、光标定位、状态码变化、路径连通；不使用大量渐变卡片。
- 密度：3–7 个元素，但正文必须控制字数。

### `clean-product`

- 适合：产品功能、操作教程、界面介绍和横屏演示。
- 视觉：暖白或浅灰背景、深色文字、钴蓝 / 青绿色强调。
- 材质：清晰面板、浏览器框、真实截图和柔和阴影；不使用强发光。
- 运动：页面滑入、焦点框、局部高亮、进度条和轻量缩放。
- 密度：2–5 个元素，优先保证 UI 可读性。

## 新增风格的流程

新增风格时只修改本文件和对应渲染模板，不复制整份 Skill：

1. 定义 `styleProfile` 名称、适用内容和不适用内容。
2. 补齐 tokens、字体 fallback、材质、运动曲线和密度。
3. 为 `talking-head-editorial`、`data-story`、`operation-upper` 至少各写一个示例。
4. 用同一个 10–15 秒舞台渲染新旧 Profile，确认语义、层级和遮挡规则没有变化。
5. 通过连续帧、文字可读性和角落聚集检查后，再把 Profile 加入可选列表。

风格 Profile 不得改变以下硬约束：音频时间轴、真实操作模块优先、字幕最后合成、文字正常方向、最终只有一个音画封装出口。
