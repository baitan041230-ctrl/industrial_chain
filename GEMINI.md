# GEMINI.md - Chaoyang District Industrial Chain Insight Platform (朝阳区产业链洞察平台)

## Project Overview

This project is a comprehensive industrial chain analysis platform designed for the Chaoyang District. it provides tools for visualizing industrial structures, profiling industries and enterprises, and leveraging AI for decision support. It features an interactive "Panoramic Industrial Chain Tree" (全景产业链树谱) and an AI-powered chat assistant.

### Key Technologies

- **Frontend:** React 19, Vite 7, TypeScript, Ant Design (v6), ECharts, Ant Design Charts/Plots.
- **Backend:** Node.js, Express (v5), MySQL (`mysql2/promise`).
- **AI Integration:** 暂时使用 DeepSeek API 作为智能诊断模块的 DEMO 示例，落地时将使用团队自己微调的模型替代.
- **State Management:** React Hooks, React Router DOM (v7).

## Project Structure

- `project/`: 平台的前后端代码.
  - `server.js`: Unified Express backend handling API requests, database interactions, and AI chat integration.
  - `src/`: Main frontend source directory.
    - `layouts/MainLayout.tsx`: Primary application layout with navigation.
    - `pages/`: Page-level components organized by feature (Home, IndustryPortrait, IndustryScore, SystemMgmt, etc.).
    - `components/`: Reusable UI components for dashboards and lists.
  - `vite.config.ts`: Vite configuration with backend proxy (`/api` -> `http://localhost:3001`).
- `data/`: 平台将要内置的数据，以及配套的 sql 代码.
  - `example/`: 部分数据的原型和示例.
  - `sql/`: 在 MySQL 中运行的 sql 代码，便于平台在多个设备上复现.

## Getting Started

### Prerequisites

- Node.js installed.
- MySQL database named `industrial_chain` running locally.
- Execute `data/sql/init.sql` to initialize the database schema and sample data.

### Building and Running

```bash
cd project
```

1. **Install Dependencies:**
   ```bash
   npm install
   ```
2. **Start Backend Server:**
   ```bash
   node server.js
   ```
   _Note: Ensure MySQL credentials in `server.js` match your local setup._
3. **Start Frontend (Vite):**
   ```bash
   npm run dev
   ```
4. **Build for Production:**
   ```bash
   npm run build
   ```

## Development Conventions

- **Naming:** Follow PascalCase for React components and camelCase for functions/variables.
- **Styling:** Use Ant Design components. Custom styles should be kept in separate `.css` files or as cleanly managed inline styles for specific layout adjustments.
- **Type Safety:** Maintain strict TypeScript typing. Update `project/src/types.d.ts` as needed.
- **API Requests:** Frontend requests to `/api/*` are automatically proxied to the backend at port 3001.
- **Routing:** Use `react-router-dom` defined in `project/src/App.tsx`.

## Core Features

- **Advanced Search (高级搜索):** Multi-dimensional filtering for enterprises.
- **Industry Portrait (行业画像):** Detailed scoring and visualization of specific industry segments.
- **Enterprise Profile (企业画像):** Comprehensive data view for individual companies.
- **Smart Diagnosis (智能诊断):** AI-driven chat interface for exploring industrial data.
- **Tag Library Management (标签体系库):** Systematic management of industry and enterprise tags.

## TODO / Roadmap

- 之前 `project/` 前后端代码中的示例数据、调取的 MySQL 数据是过时的，需要根据 `data/` 中的数据重构平台后端、数据库.
  - `data/example/数据原型 V1.xml` 中的 **行业分类**，是产业链树谱新的多级标签.
  - `data/example/数据原型 V1.xml` 中的设计既用于企业多维数据，也用于企业多维标签 (用于高级搜索、画像、系统管理等功能).
  - `data/example/data_example100.xlsx` 中是平台将要内置的很小一部分 (100 条) 企业数据，结构是基于 `data/example/数据原型 V1.xml` 的
- User 已经多次使用 `data/sql/init.sql` 在 MySQL 中反复删建库，并与前后端打通
  - 如果要修改 `data/sql/init.sql`，请保持已有的代码不变，并在此基础上修改 (不要无法实际运行的简洁版，只要完整版)
- 如果没有明确说**优化前端**，则保持平台前端设计不变.
- **便于协作与复现**: 便于团队其他成员用最少的时间成本从 Github 复现和开发.
