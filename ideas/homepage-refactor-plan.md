# Homepage Refactor Plan

## Goal

在尽量保留当前 GitHub 主页的信息架构和主要页面布局逻辑的前提下，对首页和全站视觉做一次系统性重构。

目标不是“推翻重做”，而是：

1. 保留你现在网站的核心结构和内容分区。
2. 去掉目前比较旧、杂、散的视觉感受。
3. 让首页变得更简约、干净、有研究者个人主页应有的高级感。
4. 为后续继续加内容预留一个更稳定的样式架构。

---

## Final Direction

已经和你确认的方向是：

### Core decision

- 明显焕新，但不换原本架构
- 保留现有主页的信息组织方式
- 允许一起调整 sidebar
- ClustrMaps 保留，但用更美观、低干扰的方式融入页面

### Visual direction

- warm neutral academic
- clean and airy
- restrained contrast
- content-first, but designed

这意味着这次改动不是换模板，而是把现有主页升级成一套更统一的设计语言。

---

## Current Problems

基于我刚刚看的代码，当前不美观的原因主要不是内容，而是下面这些问题叠加在一起：

### 1. 首页样式是“内容里直接写视觉”

`_pages/about.md` 里直接写了很多内联 HTML 和内联样式，比如：

- `News` 区块直接用 `style=""`
- logo 区域直接用 `100vw + flex + inline style`
- 一些颜色、间距、字号是局部拍脑袋式定义

这会导致：

- 页面缺乏统一视觉语言
- 小地方很难一起调
- 以后继续改会越来越乱

### 2. 主题底层比较老，但目前没有做“现代化皮肤”

站点还是 Minimal Mistakes 的默认风格为主，当前 `_sass/_variables.scss` 的字体、颜色、间距都偏旧：

- 默认系统字体栈比较普通
- 主色和链接色偏旧主题感
- 页面层次比较依赖默认边框、默认 spacing

这类主题本身不是不能用，但如果不重新整理视觉 tokens，就很容易像“学术模板站”而不是“精致个人主页”。

### 3. 首页缺少统一的视觉节奏

当前首页虽然有：

- 自我介绍
- News
- Education
- Awards
- Industry Experience

但这些模块之间缺少统一的：

- section spacing
- 标题层级
- 卡片/容器逻辑
- 信息密度控制

所以读起来像“内容堆上去”，而不是“经过设计的页面”。

### 4. 局部元素风格不一致

比如：

- 正文是 Markdown 风格
- News 是蓝色块状提示框
- logo 是全宽横向展示
- 页面底部还有访客地图脚本

这些元素彼此都能成立，但放在一个页面里没有形成同一个设计系统。

---

## Refactor Direction

我的建议是采用一种：

**简约、明亮、克制、偏学术高级感** 的方向。

关键词：

- clean
- airy
- modern
- minimal
- calm
- research-focused

不是做成花哨 landing page，也不是做成极度冷淡的极简白板，而是做成：

“内容依然是主角，但视觉终于配得上内容。”

---

## Design Principles

### 1. 保留现有信息架构

你说“架构可以是类似的（界面）”，我理解为：

- 仍然保留侧边个人信息/profile
- 仍然保留首页作为主要 landing page
- 仍然保留 News / Education / Awards / Experience 这些信息分区
- 不把站点改成完全不同的博客/作品集模板

也就是说我们主要重构的是：

- 视觉系统
- 组件表达
- 首页内容编排

而不是站点信息组织本身。

### 2. 先统一系统，再美化局部

如果只改首页几个 div，会短期变好看一点，但不稳。

更好的路径是先建立：

- 颜色体系
- 字体体系
- 容器和间距规则
- section 组件
- card / tag / meta 文本样式

然后再把首页各模块迁移过去。

### 3. 少即是多

这次不建议加入太多：

- 花里胡哨的动效
- 渐变过重的背景
- 大量装饰图形
- 过多强调色

重点应该是：

- 留白
- 对齐
- 字重层次
- 柔和的灰阶
- 少量精确的强调色

---

## Proposed Scope

我建议第一轮 refactor 范围控制在下面这些：

### A. Homepage First

优先重构首页 `/_pages/about.md`：

- 重写 hero/introduction 区域的表达
- 把 `News` 改成统一风格的模块
- 把 `Education / Awards / Industry Experience` 做成统一 section
- 优化 logo 展示区
- 决定是否保留底部访客地图，或者弱化它的视觉权重

### B. Shared Theme Cleanup

同步调整全站共享样式：

- `_sass/_variables.scss`
- 可能新增一个自定义 partial，例如 `_sass/_custom.scss`
- 更新 `assets/css/main.scss` 引入新的样式层

目标是保证：

- 首页改完不是孤岛
- Publications / Misc / Talks 等页面不会显得完全两套皮肤

### C. Optional Sidebar Polish

当前侧边栏个人卡片也偏旧，可以顺手优化：

- 头像尺寸和裁切
- 名字/邮箱/链接层级
- social links 的密度
- Follow 按钮是否保留

这个部分我建议做，但优先级略低于首页主体。

---

## Concrete Implementation Plan

### Phase 1. Visual Foundation

先做全局设计 token 和基础排版整理：

- 定义新的背景色、正文色、边框色、强调色
- 调整全局字体栈
- 优化标题字号层级和 section spacing
- 统一链接样式、卡片边框、圆角、阴影强度

这一步完成后，哪怕还没重写首页，站点底子也会先变干净。

Status: completed

### Phase 2. Homepage Componentization

把 `about.md` 里面的内联样式清掉，替换成更可维护的结构：

- `hero` 区
- `news panel`
- `section block`
- `experience list`
- `logo strip`

重点是从“页面里写样式”改成“页面只写语义结构，样式在 Sass 里统一管理”。

Status: completed

### Phase 3. Fine-tuning

最后再做审美精修：

- 调 section 之间距离
- 调标题与正文的节奏
- 调新闻列表密度
- 调 logo 的大小、灰度、对齐
- 调移动端展示

这一步会决定页面是不是“真的高级”。

Status: completed for first full implementation pass

---

## Implementation Summary

本轮已经完成的实现包括：

### 1. Global visual refresh

- 更新全局字体、背景、文字、边框、强调色 token
- 引入新的自定义样式层 `_sass/_custom.scss`
- 统一页面容器、圆角、阴影、留白和导航观感

### 2. Homepage rebuild without changing structure

- 保留首页原有信息架构
- 将原本大量 inline style 的首页内容改成语义化 section
- 重做 hero、news、education、awards、industry experience、logo strip、visitor map

### 3. Sidebar polish

- 去掉原本比较突兀的 `Follow` 按钮
- 将侧边栏整理成更像 profile card 的视觉形式
- 优化头像、文字层级和链接密度

### 4. ClustrMaps cleanup

- 保留 visitor map
- 降低视觉噪音
- 调整配色，使其和整站风格更一致

---

## Files Involved

- `_pages/about.md`
- `_sass/_variables.scss`
- `_sass/_custom.scss`
- `assets/css/main.scss`
- `_includes/author-profile.html`
- `_layouts/single.html`

---

## Remaining Note

当前实现已经完成，但本地没有成功跑通 Jekyll build，不是代码逻辑问题，而是环境问题：

- 当前系统 Ruby 是 `2.6.10`
- 依赖解析过程中拉到了需要 Ruby `>= 3.0` 的 `ffi` 版本
- 因此 `bundle install` / `jekyll build` 没法在当前环境直接通过

如果后面需要，我可以继续帮你处理 Ruby/Jekyll 本地预览环境，或者直接进入下一轮审美微调。

---

## Visual Style Proposal

我建议先从下面这个方向出发：

### Option A. Warm Neutral Academic

特点：

- 白底或极浅暖灰底
- 深灰文字，不用纯黑
- 一种非常克制的蓝灰/墨绿色作为强调色
- 容器轻边框，几乎不依赖阴影

适合：

- 学术主页
- 内容密度高的页面
- 想显得专业、稳定、耐看

这是我目前最推荐的方向。

### Option B. Ultra Minimal Editorial

特点：

- 更强留白
- 更少边框
- 更像个人研究名片页
- 视觉更高级，但对内容排版要求更高

风险：

- 如果不控制好内容长度，会显得空
- 比较考验 section 组织

### Option C. Soft Card-based Minimal

特点：

- 各 section 放在轻卡片里
- 更容易显得整洁
- 对旧主题兼容友好

风险：

- 如果卡片感过强，会变成常见模板风

我建议优先走 `Option A`，必要时吸收一点 `Option C` 的结构优点。

---

## What I Would Change Specifically

如果我们继续往下做，我预计会改这些具体点：

### 首页

- 让开头自我介绍更像一个有呼吸感的 hero，而不是普通段落
- 给 `News` 做一个更克制、更现代的滚动信息模块
- 统一 section 标题样式，去掉现在这种“原始 Markdown 标题 + 自定义块”的割裂感
- 把 `Industry Experience` 的 logo 区做得更整齐，不再用很硬的全屏拉伸

### 全局

- 改基础字体和颜色 token
- 调整 masthead/navigation 的 spacing
- 让 link、button、sidebar 风格更统一
- 让页面宽度、空白、模块边界更舒服

### 工程层

- 减少 `about.md` 中的 HTML inline style
- 将样式沉到 Sass
- 尽量做成可复用 class，后续其他页面也能套

---

## Risks / Things To Decide Together

在真正开工前，我们最好一起确定这几个点：

### 1. 你想保守重构，还是明显变好看

两个方向都能做：

- 保守版：结构几乎不动，只做高级清爽化
- 进阶版：结构类似，但首页会更像精心设计过的 landing page

我个人建议选中间路线：

**结构不大动，但视觉上要有明显提升。**

### 2. Sidebar 要不要一起升级

如果只改主内容区，不改 sidebar，最终可能会有一点“两张皮”。

我倾向于：

- 首页主体优先
- 但顺手把 sidebar 也做一轮简洁升级

### 3. ClustrMaps 是否保留

这个小组件比较容易破坏整体高级感。

我建议：

- 要么移到更靠后的位置
- 要么视觉降权
- 要么先去掉，后面再决定

---

## Suggested Next Step

如果你认可这个计划，下一步我建议我直接做两件事：

1. 先出一个首页视觉方案草稿版
2. 同时把基础 Sass 结构搭起来

这样我们能很快看到第一版效果，而不是停留在抽象讨论里。

---

## My Current Recommendation

我目前推荐的执行策略是：

**保留现有站点结构 + 首页重新编排 + 建立统一简约视觉系统 + 顺手修 sidebar。**

如果一句话概括，就是：

**不是换模板，而是把现在这个主页“设计化、系统化、精致化”。**
