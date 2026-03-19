🚀 前端项目 AI 协作全栈手册 (Architecture-First Template)  
本手册定义了与 AI 协作从零构建生产级前端系统的标准协议。每个文件都应作为独立的 .md 存在于项目根目录下。  
🤖 0. 启动指令 (The Master Prompt)在开始任何代码生成前，请先将以下内容发给 AI："你现在是一名精通常驻架构的前端专家。我已经为你准备了 6 份核心文档（README, ARCHITECTURE, CONVENTIONS, API_CONTRACT, UI_SPEC, TASK）。  
你的工作流程如下：  
理解阶段： 先阅读所有文档，指出潜在冲突。  
执行阶段： 严格按照 TASK.md 的 Phase 顺序执行。  
合规检查： 每完成一个任务，必须对照 CONVENTIONS.md 自检。  
实时同步： 更新 TASK.md 进度后再进行下一步。  
特别注意： 本项目采用 React 19 + TanStack Router，请确保所有路由和数据流都是类型安全的。  
📑 1. README.md (项目总纲)  
模版内容示例：
````markdown
# 项目名称：[输入项目名] - 企业级后台管理系统

## 1. 业务目标
[例如：支持多租户、动态权限、多标签页缓存的高性能管理后台]

## 2. 核心技术栈 (2026 Golden Stack)
- **Runtime:** React 19 + Vite + TS
- **Routing:** TanStack Router (Type-safe)
- **Data Fetching:** TanStack Query v5 + Axios
- **State:** Zustand (with Persist)
- **UI:** Tailwind CSS + Shadcn UI + Lucide React
- **Validation:** Zod + React Hook Form
- **Caching:** React Activation (Keep-alive)

## 3. 环境变量
- `NEXT_PUBLIC_API_URL`: 后端网关地址
````
🏗️ 2. ARCHITECTURE.md (架构蓝图)
模版内容示例：
````markdown
# 架构设计蓝图
## 1. 模块化目录职责 (Feature-Based)
- `src/api/`: 全局 Axios 实例与拦截器配置。
- `src/components/layout/`: 侧边栏、顶栏、多标签页 (TabsBar) 实现。
- `src/modules/`: **核心业务模块**。每个子文件夹（如 `/user`）包含：
  - `components/`: 该模块特有组件。
  - `api.ts`: 模块请求函数。
  - `schema.ts`: Zod 校验规则。
  - `index.tsx`: 页面入口（包裹 KeepAlive）。
- `src/routes/`: TanStack Router 定义（包含 `__root.tsx` 布局与 `_auth.tsx` 保安路由）。

## 2. 核心机制设计
- **身份验证 (Auth Guard):** 在 `_auth.tsx` 中拦截请求。未登录重定向至 `/login`；无权限重定向至 `/403`。
- **状态保持 (Keep-alive):** 切换标签页时，利用 `React Activation` 缓存组件状态。
- **多标签页 (Tabs):** Zustand 存储当前已打开的路由数组，关闭标签时需调用 `dropScope` 清理缓存。

## 3. 错误边界 (Error Boundary)
- 路由层使用 TanStack Router 的 `errorComponent` 捕获模块级崩溃，保持侧边栏可操作。
````
📏 3. CONVENTIONS.md (开发规范)
模版内容示例：
````markdown
# 开发约定

## 1. 命名与规范
- **路由文件:** 必须遵循 TanStack Router 的文件路由规范。
- **样式:** 严禁在代码中写硬编码颜色，必须使用 Tailwind 变量。

## 2. 数据安全 (Zod First)
- **所有 API 返回值必须通过 Zod Schema 校验**。
- 格式：`const data = OrderSchema.parse(response.data)`。
- 目的：在开发阶段捕获后端字段变更，防止线上悄悄崩溃。

## 3. 异步处理
- 所有 Mutation 操作必须显示全局 Loading 和 Sonner 消息提示。
- 401 错误由 Axios 响应拦截器统一处理（清空 Token + 跳转登录）。
````
🔌 4. API_CONTRACT.md (接口契约)
模版内容示例：
````markdown
# API 契约与数据模型

## 1. 响应结构
```typescript
interface ApiResponse<T> {
  success: boolean;
  data: T;
  error?: { code: string; message: string };
}
2. Zod Schema 示例const UserSchema = z.object({
  id: z.string(),
  name: z.string(),
  roles: z.array(z.string())
});
3. 用户与权限GET /api/v1/user/info: 获取当前用户信息及权限 Code 列表。
```
````

## 🎨 5. UI_SPEC.md (视觉与交互)

### 模版内容示例：
```markdown
# UI 规范与交互细节

## 1. 设计系统
- **配色:** Shadcn UI 默认主题 (Dark/Light 适配)。
- **间距:** 严格遵循 Tailwind 阶梯 (p-4, m-2 等)。

## 2. 反馈机制
- **Button:** 提交中显示 Spinner，且 `disabled=true`。
- **Skeleton:** 表格加载中展示 5 行骨架屏占位。
- **Tabs:** 标签页超出容器宽度时支持鼠标滚轮横向滚动。
📅 6. TASK.md (动态任务计划)模版内容示例：# 🛠 迭代清单

## Phase 1: 系统骨架 (P0)
- [ ] 初始化 Vite + TS + TanStack Router 环境
- [ ] 配置 Axios 拦截器与 Zustand 持久化存储
- [ ] 搭建 `__root.tsx` (侧边栏 + 顶栏 + 标签栏)

## Phase 2: 权限与登录 (P0)
- [ ] 实现登录页逻辑与 `_auth.tsx` 保安路由
- [ ] 接入 `MSW` 模拟用户信息接口

## Phase 3: 业务模块 (P1)
- [ ] 开发用户管理模块（包含列表、分页、Zod 校验）
- [ ] 实现标签页缓存逻辑 (React Activation)
````
🚩 架构师终极自查表类型安全: 
TanStack Router 的路由参数是否有类型推导？
数据防腐: 接口返回是否经过了 Zod 校验？
用户体验: 切换标签页时，之前的填单内容是否丢失（Keep-alive）？
容错能力: 某个页面挂了，侧边栏还能点吗？
