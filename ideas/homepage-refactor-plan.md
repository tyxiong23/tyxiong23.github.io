# Homepage Refactor Plan

## Final Decision

不再继续基于当前 `Minimal Mistakes` 的首页页面结构做修补。

新的方案是：

1. 保留 Jekyll 作为站点生成和内容管理工具。
2. 首页不再依赖 `about.md`。
3. 新增一个独立的 `home` layout 和 `index.html`。
4. `about.md` 回归普通内容页。
5. 参考 `academic-homepage` 的组织方式，但不照搬它的默认视觉。

---

## Why

我们已经确认两个限制会持续拖累首页效果：

- 旧模板的 layout / sidebar / page 结构太强
- Markdown 不适合承载展示型首页

所以更合适的做法是：

- 首页直接写 HTML
- 内容页继续保留 Markdown
- 样式系统按首页需求重新组织

---

## Implemented

本轮已经完成：

### 1. New homepage entry

- 新增 `index.html` 作为真正的首页入口
- 新增 `_layouts/home.html` 作为首页专用 layout

### 2. Homepage architecture rewrite

- 首页改为 HTML 驱动
- 不再把展示逻辑塞进 `about.md`
- 首页采用更接近学术主页的双栏结构：
  - 左侧主叙事和 CTA
  - 右侧 profile card
  - 下方内容模块化展开

### 3. Content sections on homepage

首页目前包含：

- hero
- news
- selected publications
- education
- experience
- logo row
- visitor map

### 4. About page separation

- `about.md` 已改回 `/about/`
- 现在它是普通 About 页面，而不是首页本体

### 5. Navigation and footer cleanup

- 导航增加了 `About`
- footer 改成更简洁的版本

### 6. Visual direction reset

已经放弃上一版偏暖色、重卡片、重圆角的方案，改为：

- 白底
- 深灰正文
- 更克制的导航
- 更少装饰
- 更强调排版和结构

---

## Files Changed

- `index.html`
- `_layouts/home.html`
- `_pages/about.md`
- `_sass/_custom.scss`
- `_config.yml`
- `_data/navigation.yml`
- `_includes/footer.html`

---

## Verification Note

代码结构已经完成切换，但本地仍然无法直接跑 `jekyll build`。

当前阻塞不是页面代码本身，而是环境问题：

- 当前环境没有可用的 `jekyll` 可执行文件
- 之前尝试安装依赖时也遇到 Ruby 版本和 `ffi` 依赖兼容问题

因此，这一轮的验证以代码层静态检查为主。
