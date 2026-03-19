# 🚀 前端项目 AI 协作全栈手册 (Architecture-First Template)

本手册定义了与 AI 协作从零构建生产级前端系统的标准协议。每个文件都应作为独立的 `.md` 存在于项目根目录下。

---

## 🤖 0. 启动指令 (The Master Prompt)

**在开始任何代码生成前，请先将以下内容发给 AI：**

> "你现在是一名精通常驻架构的前端专家。我已经为你准备了 6 份核心文档（README, ARCHITECTURE, CONVENTIONS, API_CONTRACT, UI_SPEC, TASK）。
>
> **你的工作流程如下（针对 MCP 调用次数进行了优化）：**
>
> 1. **理解阶段**：先阅读所有文档，指出潜在冲突。
> 2. **一次性扫描 (Batch MCP Strategy)**：检查是否已启用 **Figma MCP**。如果已启用，请在 Phase 0 **一次性读取**所有必要的 Tokens、Icons 和核心页面布局，并将关键标注记录在 `UI_SPEC.md` 的缓存区，严禁在后续开发中重复调用。
> 3. **执行阶段**：严格按照 `TASK.md` 的 Phase 顺序执行，UI 实现应参考已缓存的设计数据。
> 4. **合规检查**：每完成一个任务，必须对照 `CONVENTIONS.md` 自检。
> 5. **实时同步**：更新 `TASK.md` 进度后再进行下一步。
> 6. **特别注意**：本项目采用 React 19 + TanStack Router，请确保所有路由和数据流都是类型安全的。"

---

## 📑 1. README.md (项目总纲)

### 模版内容示例：

```markdown
# 项目名称：[输入项目名] - 企业级后台管理系统

## 1. 业务目标
[描述系统解决什么问题]

## 2. 核心技术栈 (2026 Golden Stack)
- **Runtime**: React 19 + Vite + TS
- **Routing**: TanStack Router (Type-safe)
- **Data Fetching**: TanStack Query v5 + Axios
- **State**: Zustand (with Persist)
- **UI**: Tailwind CSS + Shadcn UI + Lucide React
- **Validation**: Zod + React Hook Form
- **Caching**: React Activation (Keep-alive)
- **Design Source**: Figma (Optimized MCP Batching)

## 3. 环境变量
- `NEXT_PUBLIC_API_URL`: 后端网关地址
```

---

## 🏗️ 2. ARCHITECTURE.md (架构蓝图)

### 模版内容示例：

```markdown
# 架构设计蓝图

## 1. 模块化目录职责 (Feature-Based)
- `src/api/`: 全局 Axios 实例与拦截器配置。
- `src/components/layout/`: 侧边栏、顶栏、多标签页 (TabsBar) 实现。
- `src/modules/`: **核心业务模块**。每个子文件夹（如 /user）包含特定的 api.ts, schema.ts 和页面。
- `src/routes/`: TanStack Router 定义（包含 __root.tsx 布局与 _auth.tsx 保安路由）。

## 2. 核心机制设计
- **身份验证 (Auth Guard)**: 在 `_auth.tsx` 中拦截，未登录重定向至 `/login`。
- **状态保持 (Keep-alive)**: 利用 `React Activation` 缓存标签页组件状态。
- **多标签页 (Tabs)**: Zustand 存储路由数组，关闭标签时需调用 `dropScope` 清理缓存。

## 3. 错误边界 (Error Boundary)
- 路由层使用 TanStack Router 的 `errorComponent` 保持侧边栏可操作。
```

---

## 📏 3. CONVENTIONS.md (开发规范)

### 模版内容示例：

```markdown
# 开发约定

## 1. 命名与规范
- **路由文件**: 必须遵循 TanStack Router 的文件路由规范。
- **样式**: 严禁硬编码颜色，必须使用 Tailwind 变量。

## 2. 数据安全 (Zod First)
- **所有 API 返回值必须通过 Zod Schema 校验**。
- 格式：`const data = OrderSchema.parse(response.data)`。

## 3. 异步处理
- 401 错误由 Axios 响应拦截器统一处理（清空 Token + 跳转登录）。
```

---

## 🔌 4. API_CONTRACT.md (接口契约)

### 模版内容示例：

```markdown
# API 契约与数据模型

## 1. 响应结构定义
```typescript
interface ApiResponse<T> {
  success: boolean;
  data: T;
  error?: { code: string; message: string };
}
```

## 2. Zod Schema 示例
```typescript
const UserSchema = z.object({
  id: z.string(),
  name: z.string(),
  roles: z.array(z.string())
});
```
```

---

## 🎨 5. UI_SPEC.md (视觉与交互 - Figma MCP 优化版)

### 模版内容示例：

```markdown
# UI 规范与设计源 (Design Source)

## 1. Figma 联动配置 (MCP 节流模式)
- **Design URL**: [粘贴你的 Figma 文件链接]
- **策略**: 仅在初始化时调用 MCP。
- **真相源声明**: 以 **Figma Inspect 数据**为准。

## 2. 设计数据缓存 (Design Cache - 由 AI 扫描后填充)
> 注意：AI 请将 Phase 0 读取到的数据记录在此，以减少重复调用。
- **Tokens**: [在此记录 Colors, Typography, Shadow]
- **Spacing**: [在此记录统一的间距阶梯]
- **SVG Assets**: [在此提取关键 SVG 代码]

## 3. 设计变量同步
- 优先从上述 **Design Cache** 中读取数据。
- 严禁在没有明确指令的情况下反复调用 MCP。
```

---

## 📅 6. TASK.md (动态任务计划)

### 模版内容示例：

```markdown
# 🛠 迭代清单

## Phase 0: 深度扫描与数据持久化 (Single MCP Call) [Priority: P0]
- [ ] 调用 Figma MCP 执行 Full Document Scan（读取所有样式）。
- [ ] 将提取的 Tokens 写入 `tailwind.config.js`，同步数据至 `UI_SPEC.md`。
- [ ] 离线化所有自定义图标。

## Phase 1: 系统骨架 (P0)
- [ ] 初始化 Vite + TanStack Router。
- [ ] 搭建 `__root.tsx` (侧边栏 + 顶栏 + 标签栏)。

## Phase 2: 业务模块实现 (P1)
- [ ] 开发用户管理模块（包含列表、分页、Zod 校验）。
- [ ] 实现标签页缓存逻辑 (React Activation)。
```

---

## 🚩 架构师终极自查表

1. **MCP 效率**: 是否实现了“一次读取，全程复用”？
2. **类型安全**: 路由参数和 API 返回是否都有类型推导？
3. **视觉还原度**: UI 是否严格对齐了缓存的设计数据？
4. **性能**: 切换标签页时内容是否无损（Keep-alive）？

---
