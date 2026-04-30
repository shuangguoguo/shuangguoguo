# 依赖功能清单 (Dependencies)


## 1. 富文本编辑器与文档处理
* **编辑器框架**:
    * **`slate` / `slate-react` / `slate-history`**: 现代富文本底层的无头框架，定制性极强。
    * **`draft-js` / `react-draft-wysiwyg`**: 基于 React 的富文本编辑器。
    * **`quill` / `react-quill`**: 简单、API 驱动的经典富文本编辑器。
    * **`tinymce` / `@tinymce/tinymce-react`**: 功能极全的企业级富文本编辑器。
    * **`aieditor`**: 融入 AI 能力的下一代富文本编辑器。
* **Markdown 相关**:
    * **`react-markdown` / `markdown-it` / `marked`**: Markdown 内容的解析与 React 渲染。
    * **`turndown`**: 将 HTML 转换回 Markdown 格式。
    * **`remark-gfm` / `unified`**: 用于处理 Markdown 的插件生态（如支持表格等）。
* **文档转换与导出**:
    * **`docx` / `docxtemplater`**: 在前端生成、填充并下载 Word (.docx) 文件。
    * **`mammoth`**: 将 Word 文档安全地转换为 HTML。
    * **`jspdf` / `html2pdf.js` / `pdfmake`**: 浏览器端生成 PDF 文档的多种方案。
    * **`@onlyoffice/document-editor-react`**: 集成 OnlyOffice 在线文档协作编辑器。

## 3. 数据可视化与图形图表
* **`echarts` / `echarts-for-react`**: 强大的数据可视化图表库及其 React 封装。
* **`@antv/x6` / `@antv/x6-react-shape`**: 蚂蚁金服出品的流程图、图编辑引擎。
* **`mermaid`**: 通过简单的文本语法生成流程图、序列图、甘特图。
* **`lottie-web`**: 渲染 Adobe After Effects 制作的动画 (JSON 格式)。
* **`flv.js`**: HTML5 FLV 视频播放器，支持直播流。

## 4. 地图与地理空间 (GIS)
* **`maplibre-gl` / `@vis.gl/react-maplibre`**: 高性能开源地图渲染引擎。
* **`@turf/turf`**: 处理地理空间计算的 JavaScript 工具库（如测距、围栏判断）。

## 5. 高性能表格与代码编辑器
* **`ag-grid-community` / `ag-grid-react`**: 极高性能的数据表格，支持百万级数据处理。
* **`handsontable` / `@handsontable/react`**: 类似 Excel 操作体验的在线电子表格。
* **`codemirror` / `@codemirror/...`**: 专业级代码编辑器，支持 Java, Python, SQL 等语法。
* **`react-syntax-highlighter` / `highlight.js`**: 网页代码块的语法高亮显示。

## 6. 通用工具与状态管理
* **网络与状态**:
    * **`axios`**: 基于 Promise 的 HTTP 请求客户端。
    * **`mobx` / `mobx-react-lite`**: 简单、可扩展的响应式状态管理。
    * **`ahooks`**: 阿里巴巴出品的常用 React Hooks 库。
* **数据处理**:
    * **`dayjs` / `moment`**: 日期和时间处理库。
    * **`papaparse` / `react-papaparse`**: 高性能的 CSV 文件解析。
    * **`crypto-js` / `jsencrypt`**: 前端数据加密、签名（AES, RSA 等）。
    * **`uuid`**: 生成唯一标识符。
    * **`loadsh`**: (lodash) JavaScript 实用工具函数库。
* **浏览器增强**:
    * **`file-saver`**: 文件下载与保存工具。
    * **`react-copy-to-clipboard`**: 快捷实现剪贴板复制功能。
    * **`web-storage-cache`**: 增强型本地存储缓存，支持有效期设置。
    * **`version-polling`**: 实时监测前端版本更新并提醒。

 plugin-web-update-notification 负责检测项目部署代码更新，提示用户刷新页面。








