# CHANGELOG_GEMINI.md - 项目变更日志

本文件记录了由 Gemini CLI 助手执行的所有代码修改及系统调整。

## [2026-03-05] - 初始设置与产业分类页面真实化

### 新增 (Added)
- 创建了 `GEMINI.md`：详细记录了项目的技术栈、目录结构、运行指令及开发规范，作为后续对话的上下文基础。

### 修改 (Changed)
- **后端 API (`project/server.js`)**:
    - 扩展了 `/api/industry/companies` 接口的 SQL 查询，新增返回字段：`total_score` (综合评分), `address_detail` (详细地址), `enterprise_type` (企业类型), `qualifications` (资质), `is_small_micro` (小微企业标识)。
- **前端页面 (`project/src/pages/IndustryClass/IndustryClass.tsx`)**:
    - **移除 Mock 数据**：删除了所有静态 Mock 常量（如技术领域、融资轮次）。
    - **对接真实元数据**：将筛选行（企业类型、科技属性、专利类型、应用场景、融资轮次、街道地区）全部改为从后端 `metaData` 接口动态提取。
    - **动态统计逻辑**：更新了推荐位（Precise Block）的统计逻辑，使其基于当前搜索结果列表动态计算集团数、上市公司数和高新企业数。
    - **UI 数据同步**：
        - 列表项和卡片现在展示真实的综合评分。
        - 地址栏优先展示 `address_detail` 详细地址。
        - 增加了真实的融资轮次标签和联系方式（电话、邮箱）的空值处理。

---
*注：记录将按日期倒序追加。*
