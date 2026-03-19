# 🚀 前端项目 AI 协作全栈手册 (Architecture-First Template)

本手册定义了与 AI 协作从零构建生产级前端系统的标准协议。每个文件都应作为独立的 `.md` 存在于项目根目录下。

---

## 🤖 0. 启动指令 (The Master Prompt)

**在开始任何代码生成前，请先将以下内容发给 AI：**

> "你现在是一名精通常驻架构的前端专家。我已经为你准备了 6 份核心文档（README, ARCHITECTURE, CONVENTIONS, API_CONTRACT, UI_SPEC, TASK）。
>
> **你的工作流程如下：**
>
> 1. **理解阶段**：先阅读所有文档，指出潜在冲突。
> 2. **环境自检**：检查是否已启用 **Figma MCP**。如果已启用，请在生成 UI 代码前调用 MCP 读取设计稿。
> 3. **执行阶段**：严格按照 `TASK.md` 的 Phase 顺序执行。
> 4. **合规检查**：每完成一个任务，必须对照 `CONVENTIONS.md` 自检。
> 5. **实时同步**：更新 `TASK.md` 进度后再进行下一步。"

---

## 📑 1. README.md (项目总纲)

### 模版内容示例：

```markdown
# 项目名称：[输入项目名] - 企业级后台管理系统

## 1. 业务目标
[描述系统解决什么问题]

## 2. 核心技术栈
- **Runtime**: React 19 + Vite + TS
- **Routing**: TanStack Router
- **Data Fetching**: TanStack Query v5
- **UI**: Tailwind CSS + Shadcn UI
- **Design Source**: Figma (Enabled via MCP)
```

---

## 🏗️ 2. ARCHITECTURE.md (架构蓝图)

### 模版内容示例：

```markdown
# 架构设计蓝图

## 1. 模块化目录职责
- `src/modules/`: 核心业务模块。
- `src/routes/`: 路由定义。

## 2. 核心机制设计
- **身份验证**: `_auth.tsx` 保安路由。
- **状态保持**: `React Activation` 缓存。
```

---

## 📏 3. CONVENTIONS.md (开发规范)

### 模版内容示例：

```markdown
# 开发约定

## 1. 命名与规范
- 路由必须遵循 TanStack Router 规范。

## 2. 数据安全
- 所有接口必须经过 Zod Schema 校验。
```

---

## 🔌 4. API_CONTRACT.md (接口契约)

### 模版内容示例：

```markdown
# API 契约与数据模型

## 1. 响应结构定义
...
```

---

## 🎨 5. UI_SPEC.md (视觉与交互 - Figma MCP 集成)

### 模版内容示例：

```markdown
# UI 规范与设计源 (Design Source)

## 1. Figma 联动配置 (MCP)
- **Design URL**: [粘贴你的 Figma 文件链接]
- **MCP Action**: 请使用 Figma MCP 插件读取上述 URL 中的 `Tokens` 和 `Components`。
- **真相源声明**: 当本文件中的描述与 Figma 设计稿冲突时，以 **Figma 设计稿中的 CSS Inspect 数据**为准。

## 2. 设计变量同步
- **Colors/Typography**: 请优先从 Figma 的 Local Styles 中读取。
- **Spacing**: 严格遵守 Figma 中的 Auto Layout 间距，转化为 Tailwind 的对应阶梯（如 16px -> p-4）。

## 3. 交互行为
- 所有图标优先使用 `Lucide React`，如果 Figma 中使用了自定义图标，请通过 MCP 提取 SVG 代码。
```

---

## 📅 6. TASK.md (动态任务计划)

### 模版内容示例：

```markdown
# 🛠 迭代清单

## Phase 0: 设计对齐 (MCP Setup) [Priority: P0]
- [ ] 运行 Figma MCP 扫描指定设计稿 URL
- [ ] 导出全局 Design Tokens (Colors, Font Sizes) 并同步至 `tailwind.config.js`
- [ ] 验证原子组件（Button, Input）与 Figma 视觉稿的一致性

## Phase 1: 系统骨架 (P0)
- [ ] 初始化 Vite + TanStack Router
- [ ] 搭建 `__root.tsx` 布局

## Phase 2: 业务开发 (P1)
- [ ] 根据 Figma 中的 Page 设计稿实现登录页逻辑
- [ ] 实现模块化业务页面，并确保响应式断点与 Figma 标注一致
```

---

## 🚩 架构师终极自查表

1. **视觉还原度**: 是否已通过 MCP 读取了 Figma 最新的边距、颜色和阴影？
2. **类型安全**: 接口返回是否经过了 Zod 校验？
3. **性能**: 是否实现了 Keep-alive 缓存？

---
