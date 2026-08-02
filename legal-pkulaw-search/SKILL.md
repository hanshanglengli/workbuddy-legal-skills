---
name: legal-pkulaw-search
description: 北大法宝中国法检索执行型技能。agent 直接调 pkulaw MCP 搜中国法规、司法解释、裁判文书，运用间隔字数语法与企业名反查，并按案例效力位阶排序结果。触发词：查法规、查司法解释、查案例、裁判规则、类案检索、间隔字数、结果中检索、企业名反查、裁判文书、北大法宝。
agent_created: true
---

# legal-pkulaw-search（北大法宝中国法检索 · agent 执行型）

## 定位

agent 用 pkulaw MCP **直接搜**中国法规与案例，不是教人去网页操作。负责"中国法怎么搜"的执行层，为 `legal-contract-search`（场景层）提供法规/案例检索能力。

## 与套件其他技能的分工

- 本技能 = 中国法检索的**工具层**（pkulaw MCP 调用 + 语法 + 结果排序）
- `legal-contract-search` = 合同场景层，调用本技能做步骤2/4（规范检索+裁判规则检索）
- `legal-due-diligence-foreign` = 主体尽调与域外法（WebFetch 为主，不依赖 pkulaw）

## 触发条件

用户要查中国法规/司法解释/案例/裁判规则/类案，或提到"间隔字数""结果中检索""企业名反查""北大法宝"。

## agent 执行动作

> **工具名提示**：下文工具名基于当前环境北大法宝连接器（前缀 `mcp__pkulaw__...`）。不同环境连接器 ID 可能不同，**以你实际连接器的工具名为准**；能力对照（搜法规、取正文、搜案例）不受影响。若工具未激活，先 ToolSearch 加载。未连接 pkulaw 时本 skill 不可用，请改用 `legal-research` 的通用搜索降级路径。

### 动作 1 · 法规/司法解释检索
调用 pkulaw 法规 MCP（若工具未激活，先 ToolSearch 加载）：
- `mcp__pkulaw__mcp-law-search-service.search_article` — 按关键词搜法规条文
- `mcp__pkulaw__mcp-law-search-service.get_article` — 获取指定条文详情
- `mcp__pkulaw__mcp-law.get_law_list` — 获取法律法规列表

执行：广搜关键词 → 在结果中加词缩小 → 配合效力级别筛选（司法解释/法律/行政法规）。

### 动作 2 · 案例/裁判文书检索
调用 pkulaw 案例 MCP：
- `mcp__pkulaw__mcp-case-search-service.search_case` — 按关键词搜案例
- `mcp__pkulaw__mcp-case.get_case_list` — 获取案例列表

### 动作 3 · 间隔字数语法（超长间隔检索）
- **MCP 路径**：若 MCP 支持距离/间隔参数，直接设置（如留置权条款 `约定~200留置`）。
- **网页端路径（MCP 不支持时）**：告知用户去北大法宝**普通检索大搜索框**（非高级检索界面）用波浪符 `~` 语法，可突破高级检索 99 字限制：
  ```
  商铺租赁合同 法院认为 第~10约定 约定~200留置
  ```
  - `第~10约定`：间隔 ≤10 字，命中"第X条约定"结构
  - `约定~200留置`：间隔 ≤200 字，确保同条款内
- 详见 `references/pkulaw-syntax.md`。

### 动作 4 · 企业名反查（首尾呼应）
- 用企业名（如"万达""星巴克"）在案例库做结果中检索
- 命中该企业合同纠纷文书 → 提取法官对条款的评价 → 反推合同改进点
- 这是 `legal-contract-search` 四步法第4步的执行方式

### 动作 5 · 结果排序（按效力位阶）
检索到多个类案后，按 `references/case-hierarchy.md` 的 9 级位阶排序标注，优先输出高顺位案例。

## 环境适配

| 动作 | 工具 | 可执行 |
|------|------|--------|
| 法规/案例检索 | pkulaw MCP（已连接） | ✅ |
| 间隔字数超长检索 | MCP 参数或网页端 | ⚠️ MCP 不支持时引导网页端 |
| Lexis/Westlaw 外文 | 无 MCP + 付费墙 | ❌ 见 legal-due-diligence-foreign 附注 |

## references

- `references/pkulaw-syntax.md` — 北大法宝间隔字数语法（波浪符）+ 结果中检索 + 企业名反查 + 单字思维；附 Lexis 通配符/W/n/W/S、判例效力彩色标识（外文，仅指导）
- `references/case-hierarchy.md` — 案例效力位阶 9 级排序 + 类案识别（distinguish）比对法

## 来源

内容整理自黄文旭《法律检索在涉外法律实务中的应用》讲座（湖南师范大学国际法系主任）。
