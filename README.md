# workbuddy-legal-skills

WorkBuddy 法律检索实战 Skill 集合（当前收录：`legal-research`）。

## legal-research —— 法律检索与事实核查

为法律检索（判例 / 法条 / 法规政策）提供「搜得到」+「不信 AI 幻觉」的实战方法论。

### 两大目标

1. **搜到"搜不到"的法律与信息**：高级检索命令、官网改版绕过、Wayback 存档、多维线索定位主体。
2. **杜绝 AI 幻觉**：四核对、失败分级 A–E、置信度分级、数据库冲突处理、时效性强校验。

### 适用人群

- 法学学生（Lexis / 北大法宝类作业检索）
- 执业律师 / 法务（案例核验、文书判例支撑）
- 任何需要让 AI 输出"可引证"法律结论的研究者

### 环境依赖

- **推荐**：连接北大法宝（pkulaw）专业库，能力最完整。
- **可选降级**：未连接专业库时，仅用通用搜索（WebSearch / WebFetch）也能做线索级检索；结论只能到"线索 / 待核"，不能下法律定论（详见 SKILL.md「环境适配」）。
- 仅在使用 python-docx 生成文书时才需安装该依赖。

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

### 安装到 WorkBuddy

将 `legal-research/` 整个目录放入 `~/.workbuddy/skills/`（用户级），或 `<项目>/.workbuddy/skills/`（项目级），重启会话即可在对话中触发。

### 免责声明

本仓库为**方法论与工具辅助**，不构成法律意见。AI 生成或引用的法条、判例须由使用者自行通过专业法律数据库（北大法宝 / 裁判文书网 / 官方公报）核验，重要事项请咨询执业律师。因依赖本工具输出产生的任何后果，作者不承担责任。

### License

[MIT](./LICENSE)
