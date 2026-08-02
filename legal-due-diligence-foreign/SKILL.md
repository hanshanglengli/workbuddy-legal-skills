---
name: legal-due-diligence-foreign
description: 涉外主体尽调与域外法查明执行型技能。agent 用 WebFetch 自由资源主动查境内企业/香港公司/美国上市公司/国内上市公司股权，并用 WorldLII/Globlaws 查外国法，AI线索+官方源验证。触发词：股权穿透、查公司、香港查册、SEC年报、20-F、外国法、域外法、一带一路法律、港澳台法律、WorldLII、Globlaws、尽调。
agent_created: true
---

# legal-due-diligence-foreign（涉外尽调与域外法 · agent 执行型）

## 定位

agent 用 WebFetch 公开资源**主动查**主体股权与外国法，不依赖付费库。负责"涉外场景怎么搜"的执行层。

## 与套件其他技能的分工

- 本技能 = 主体尽调 + 域外法（WebFetch 为主）
- `legal-pkulaw-search` = 中国法检索（pkulaw MCP 为主）
- `legal-contract-search` = 合同场景，调用本技能做涉外主体尽调

## 触发条件

用户要查公司股权/穿透、香港查册、SEC年报、外国法、一带一路法律、港澳台法律，或提到尽调、WorldLII、Globlaws。

## agent 执行动作 · 主体尽调

按主体注册地选路径（见 `references/due-diligence-paths.md`）：

| 主体类型 | agent 动作 | 可执行 |
|----------|-----------|--------|
| 境内企业 | WebFetch 国家企业信用信息公示系统 | ✅ |
| 香港公司 | WebFetch 香港查册中心（标注需付费调档 23-160 港元） | ⚠️ 部分 |
| 美国上市公司 | WebFetch SEC EDGAR 20-F，Ctrl+F 式定位股东/子公司 | ✅ |
| 国内上市公司 | WebFetch 巨潮资讯网年报子公司章节 | ✅ |
| 境外非上市 | WebFetch OS 系导航站 | ✅ |

### 零成本反查技巧
查香港公司难穿透时，找**关联上市主体**反查：
- 例：华住（美国上市）20-F 年报 Ctrl+F 搜"ACL" → 确认华住全资子公司股权关系，免费且权威
- 原则：换一个信息披露更充分的关联主体间接获取

## agent 执行动作 · 域外法查明

按国家/地区选数据库（见 `references/foreign-law-paths.md`）：

1. **选数据库**：免费优先 WorldLII / 商务部 Globlaws；已订阅则 Lexis/Nexis
2. **用检索语法**：通配符 `!` + 间隔 `W/n` + 同句 `W/S`（Lexis 语法，见 legal-pkulaw-search 的 pkulaw-syntax.md 附注）
3. **看判例效力标识**：Lexis 彩色标志筛有效判例
4. **验证时效性**：WebSearch 必应确认法规是否有修订版（如马来西亚仲裁法 2018 修订）
5. **交叉验证**：至少两个独立来源（Globlaws + WorldLII）相互印证

### 一带一路小语种路径
- 老挝：Globlaws → 亚洲 → 老挝 → 国际劳工组织老挝立法 → 民事诉讼法（英文PDF）
- 马来西亚：WorldLII → 马来西亚 → 成文法 → 仲裁法 2005 → 必应确认 2018 修订
- 吉尔吉斯斯坦：Globlaws → 亚洲 → 一般法律规定 → 民法典（93页英文版）

## AI 辅助（agent 自身就是 AI 时的注意）

agent 用自身/Web AI 获取股权链线索时，**铁律：AI 只指路不做证**：
- 线索必须用官方源验证（SEC 20-F / 巨潮 / 公示系统）
- 未经官方源验证前一律视为未证实
- 详见 `references/ai-assist.md`

## references

- `references/due-diligence-paths.md` — 主体尽调路径表（按主体类型）+ 香港查册难点 + 零成本反查方案
- `references/foreign-law-paths.md` — 域外法数据库选择 + 一带一路路径 + 港澳台检索 + 实证研究选题
- `references/ai-assist.md` — AI辅助尽调的验证铁律 + 自然语言检索趋势

## 来源

内容整理自黄文旭《法律检索在涉外法律实务中的应用》讲座（湖南师范大学国际法系主任）。
