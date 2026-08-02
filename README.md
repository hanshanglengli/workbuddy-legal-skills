# workbuddy-legal-skills

WorkBuddy 法律检索实战 Skill 集合（当前收录：`legal-research` + 三技能套件）。

## Skills 一览

| Skill | 定位 | 核心能力 |
|-------|------|----------|
| **legal-research** | 通用法律检索与事实核查 | 防 AI 幻觉（四核对 / 失败分级）、搜"搜不到"的信息、AI 报告核验 |
| **legal-contract-search** | 合同起草检索 | 八大类合同路由映射、标的/公司池检索、条款骨架获取 |
| **legal-pkulaw-search** | 北大法宝中国法检索 | MCP 调用、间隔字数语法、案例 9 级效力位阶 |
| **legal-due-diligence-foreign** | 涉外尽调与域外法查明 | 香港查册 / SEC 年报 / WorldLII / 域外法查明路径 |

> 后三个由原 `legal-search-practice` 拆分而来，各司其职、独立触发，可单独使用也可组合。

---

## legal-research —— 法律检索与事实核查

为法律检索（判例 / 法条 / 法规政策）提供「搜得到」+「不信 AI 幻觉」的实战方法论。

### 两大目标

1. **搜到"搜不到"的法律与信息**：高级检索命令、官网改版绕过、Wayback 存档、多维线索定位主体。
2. **杜绝 AI 幻觉**：四核对、失败分级 A–E、置信度分级、数据库冲突处理、时效性强校验。

### 目录结构

```
legal-research/
├── SKILL.md            # 决策索引 + 工作流（先读这个）
├── CHANGELOG.md
└── references/         # 各主题详解
    ├── ai-hallucination.md        # 幻觉类型、识别、评测数据
    ├── ai-report-verification.md  # 最高频：核验一份 AI 法律报告
    ├── finding-unfindable.md      # 搜不到时的进阶方法
    ├── search-syntax.md           # 高级检索命令
    ├── ship-tracking.md           # IMO 船舶追踪等垂直检索
    └── evidence-preservation.md   # 网页证据固定
```

---

## legal-contract-search —— 合同起草检索

接到合同任务时，按合同类型路由映射表，主动调 WebFetch（巨潮/SEC/港交所）+ pkulaw MCP + Law Insider 搜真实合同范本、法规、裁判文书条款原文，交付可参考的合同素材包。

```
legal-contract-search/
├── SKILL.md
└── references/
    └── contract-type-mapping.md   # 八大类合同映射表（租赁/投资/股权转让/合资/劳动/借贷/买卖/服务）
```

---

## legal-pkulaw-search —— 北大法宝中国法检索

直接调 pkulaw MCP 搜中国法规、司法解释、裁判文书，运用间隔字数语法与企业名反查，并按案例效力位阶排序结果。

```
legal-pkulaw-search/
├── SKILL.md
└── references/
    ├── pkulaw-syntax.md            # 间隔字数 / 同段 / 同句等高级语法
    └── case-hierarchy.md           # 案例 9 级效力位阶表
```

---

## legal-due-diligence-foreign —— 涉外尽调与域外法查明

用 WebFetch 自由资源主动查境内企业 / 香港公司 / 美国上市公司 / 国内上市公司股权，并用 WorldLII / Globlaws 查外国法。AI 线索 + 官方源验证。

```
legal-due-diligence-foreign/
├── SKILL.md
└── references/
    ├── due-diligence-paths.md      # 各主体类型尽调路径
    ├── foreign-law-paths.md        # 域外法查明渠道（含港澳台检索渠道）
    └── ai-assist.md                # AI 线索定位 + 官方源验证方法论
```

---

## 环境依赖

- **推荐**：连接北大法宝（pkulaw）专业库，`legal-pkulaw-search` 和 `legal-research` 能力最完整。
- **可选降级**：未连接专业库时，`legal-research` 可用通用搜索做线索级检索；`legal-pkulaw-search` 不可用（需 pkulaw 连接器）。
- `legal-contract-search` 和 `legal-due-diligence-foreign` 主要用 WebFetch / WebSearch，无硬性 MCP 依赖。

## 安装到 WorkBuddy

将需要的 skill 目录（如 `legal-research/`）整个放入 `~/.workbuddy/skills/`（用户级），或 `<项目>/.workbuddy/skills/`（项目级），重启会话即可在对话中触发。

## 免责声明

本仓库为**方法论与工具辅助**，不构成法律意见。AI 生成或引用的法条、判例须由使用者自行通过专业法律数据库（北大法宝 / 裁判文书网 / 官方公报）核验，重要事项请咨询执业律师。因依赖本工具输出产生的任何后果，作者不承担责任。

## License

[MIT](./LICENSE)
