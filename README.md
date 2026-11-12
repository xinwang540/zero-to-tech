# zero-to-tech

一个前后端分离的全栈个人 Web 应用，包含**个人主页**与**文字实验室**两个模块：个人主页通过接口动态渲染个人介绍与作品入口；文字实验室面向中文文本处理场景，提供文本输入、异步接口提交与结构化结果展示。

> 本人独立完成前端架构设计、后端 RESTful API 设计与实现、前后端联调与响应式适配。

---

## 功能特性

- **个人主页**
  - 首屏通过 `GET /api/profile` 异步加载个人资料（标题、副标题、精选作品、座右铭）；
  - 本地静态数据兜底 + 异常捕获，后端不可用时页面仍可正常渲染。
- **文字实验室**
  - 中文文本输入区：实时字数统计、提交错误提示；
  - 结果区：与原文、拼音、情感分数、情感标签等结果字段联动展示；
  - 分数滚动动画、卡片交错入场动效。
- **工程与体验**
  - Next.js App Router 文件夹路由，组件化拆分，内容配置化管理（数据与视图分离）；
  - 区分服务端组件与客户端组件边界；
  - CSS 设计令牌 + Grid 栅格，多断点响应式，兼容桌面 / 平板 / 移动端。

## 技术栈

| 端 | 技术 |
|---|---|
| 前端 | Next.js（App Router）、React、JavaScript、anime.js、原生 CSS（变量 / Grid / 响应式） |
| 后端 | Python、FastAPI、Pydantic、Uvicorn、CORS 中间件 |
| 工程 | Git、npm、Next.js 静态导出（`output: 'export'`） |

## 快速开始

### 1. 启动后端

```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --reload --port 8000
```

接口默认运行在 `http://localhost:8000`。

### 2. 启动前端

```bash
npm install
npm run dev
```

浏览器打开 `http://localhost:3000`。

前端通过环境变量访问后端，在项目根目录新建 `.env.local`：

```bash
NEXT_PUBLIC_API_BASE_URL=http://localhost:8000
```

## 接口说明

| 方法 | 路径 | 说明 |
|---|---|---|
| `GET` | `/api/profile` | 返回主页结构化资料数据 |
| `POST` | `/api/analyze` | 提交文本，返回原文、拼音、情感分数、情感标签等结构化结果（分析逻辑持续迭代中） |

请求体示例：

```json
{ "text": "今天的风很轻，适合把脑海里的想法慢慢写下来。" }
```

## 项目结构

```
app/                     # Next.js App Router：文件夹即路由
  layout.jsx             # 全站外壳
  page.jsx               # /         个人主页
  text-lab/page.jsx      # /text-lab 文字实验室
components/              # Nav / HomeView / TextLabView / InputCard / ResultCard 等组件
data/site.js             # 站点内容配置（数据与视图分离）
css/                     # reset / variables / layout / cards / lab / responsive 等样式模块
backend/
  main.py                # FastAPI 应用与路由
  requirements.txt
```

## 说明

- 拼音标注与情感分析模块处于接口结构预留阶段，正在接入 `pypinyin` 与情感词典实现；
- 项目为个人全栈练手项目，前端已配置静态导出，后续将部署上线并补充在线访问地址。
