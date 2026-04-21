# Endfield 风格改造说明

## 目标
在不破坏 GrtBlog 既有前端架构的前提下，把首页视觉从“温润个人博客”推进到“冷暗工业科幻 / 档案叙事”方向。

## 与官方前端文档保持一致的约束
参考：`https://grtblog.js.org/dev/frontend`

本次改造保持以下原则不变：

1. **页面只做编排**
   - 仍以 `routes/+page.svelte` 负责组装。
   - 风格改动主要落在 `lib/features/home/*` 与 `routes/layout.css`。

2. **不改数据分层**
   - 没有把业务逻辑塞回页面层。
   - 没有改变 `+page.server.ts` / 客户端查询职责。

3. **不破坏 Svelte 5 Runes 用法**
   - 仅调整文案、结构层与样式。
   - 不引入违背现有组件写法的状态管理方式。

4. **设计系统仍以 `src/routes/layout.css` 为中心**
   - 全局基调、背景、阴影在 `layout.css` 收口。
   - 模块级终端卡片效果放在对应 feature 组件内。

## 当前已做
### 第一阶段，改气质
- 全局背景改为冷暗工业渐变底。
- Hero 区增加：
  - 网格 overlay
  - 切角 frame
  - 左右辉光
  - 更偏档案/信号的标题文案

### 第二阶段，统一首页模块
- `InspirationGrid.svelte`
  - 卡片改为终端面板式深色玻璃层
  - 增加顶部冷光与更克制的边框
- `SubscribeSection.svelte`
  - 改为深色控制台式订阅面板
- `HomeArticleItem.svelte`
  - 文章 hover 改成冷蓝强调
- `HomeMomentItem.svelte`
  - 手记 hover 改成偏粉红的情绪强调

### 第三阶段，扩展到列表页入口
- `PageHeader.svelte`
  - 列表页头部统一为档案面板式标题区
  - 加入网格背景、冷蓝标签、全大写标题节奏
- `PostList.svelte`
  - 文章列表 hover 背板改为冷暗档案高亮
- `MomentListPage.svelte`
  - 手记列表加入整体区域框线，让内容区不再悬空

## 详情页精修清单

### 文章详情
- [x] 详情页 Header 改成档案面板式结构
- [x] 详情页正文主容器改成深色收纳壳
- [x] Markdown 区增加轨道线 / 档案阅读感
- [x] Action Bar 纳入统一冷暗体系
- [x] TOC Sidebar 统一终端风格
- [x] AI 摘要模块统一终端风格
- [x] 评论区与相关文章区统一边框/背景语言
- [ ] lead-in / footer / related moments 细节统一

### 手记详情
- [x] 手记详情主纸面改成深色档案壳
- [x] 手记头部信息区进一步终端化
- [ ] 手记底部印章区改成更一致的系统标识
- [ ] 手记评论区边界语言统一
- [ ] 手记 TOC / related 区块统一

### 跨详情页共用
- [ ] 统一详情页内链接、分隔线、引用块、代码块的视觉 token
- [ ] 统一标签、徽标、统计数字的高亮逻辑
- [ ] 清理残留的旧博客浅色 hover / border / text token
- [ ] 评估是否加入轻量 reveal，但不引入重型动效依赖

## 后续建议
### 可继续做
1. 统一全站 section 标题样式
2. 列表页和详情页加入档案框线语言
3. 增加轻量滚动 reveal，而不是重型视差
4. 补一套更明确的色板 token，例如：
   - signal-blue
   - archive-white
   - warning-amber
   - trace-pink

### 暂时不要急着做
1. 大量背景视频
2. 全站重型滚动联动
3. 大规模引入新动画库

## 原则
这个方向的关键不是“动得多”，而是：

- 冷
- 克制
- 像档案系统，不像炫技模板
- 保留内容可读性
