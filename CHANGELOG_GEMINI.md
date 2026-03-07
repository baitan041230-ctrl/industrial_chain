# CHANGELOG_GEMINI.md - 项目变更日志

本文件记录了由 Gemini CLI 助手执行的所有代码修改及系统调整。

## [2026-03-05] - 修复产业树标签点击失效（实现递归查询）

### 修复 (Fixed)
- **后端 API (`project/server.js`)**:
    - **新增递归函数**：增加了 `getAllSubIndustryIds` 辅助函数，能够递归获取指定行业节点下的所有子孙节点 ID。
    - **实现父节点查询**：更新了 `/api/industry/companies` 接口逻辑。当用户点击父节点时，后端现在会查询该节点及其所有子节点下的关联企业，解决了点击高层级标签结果为空的问题。
    - **优化 SQL 逻辑**：修正了 `IN` 子句的参数绑定方式，并确保 `stageKey`（上下游）过滤也支持递归子节点。

## [2026-03-05] - 修复产业分类筛选功能失效问题

### 修复 (Fixed)
- **后端 API (`project/server.js`)**:
    - 修复了基础字段（企业类型、街道、融资轮次）的匹配逻辑，由精确匹配改为 `LIKE` 模糊匹配，解决了数据库数据后缀不一致导致的筛选失效。
    - 补全了 `techAttr` (科技属性) 和 `scenario` (应用场景) 的关联查询。

## [2026-03-05] - 初始设置与产业分类页面真实化

### 新增 (Added)
- 创建了 `GEMINI.md`：记录项目基础信息。
- 实现了 `CHANGELOG_GEMINI.md`：记录演进日志。

### 修改 (Changed)
- **后端 API (`project/server.js`)**: 扩展了字段返回。
- **前端页面 (`project/src/pages/IndustryClass/IndustryClass.tsx`)**: 对接真实元数据与动态统计逻辑。

---
*注：记录将按日期倒序追加。*
