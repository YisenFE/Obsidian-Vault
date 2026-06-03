# LLM Wiki Schema

本 vault 按 [[Karpathy wiki 方法论]] 中的三层模型维护：

1. `raw/` — 原始资料层。只读、不可改；新剪藏/论文/访谈/图片先放这里。
2. `wiki/` — LLM 维护的知识层。摘要、概念、实体、主题、问题、综合分析都在这里持续演化。
3. `AGENTS.md` — schema / 操作规范。每次 ingest、query、lint 都先遵守本文件。

## 目录约定

```text
raw/
  inbox/        # 临时放入、尚未整理的新资料
  assets/       # 本地图片、PDF、网页附件等
  *.md          # 已进入 raw 层的原始资料，原则上不修改

wiki/
  index.md      # 内容目录；每次 ingest/query 产出新页面后更新
  log.md        # 追加式操作日志；不要重写旧记录
  overview.md   # 当前领域总览/演化中的高层综合
  sources/      # 每个 raw 来源对应一篇 LLM 摘要页
  concepts/     # 概念页，例如 Agent Harness、Harness Engineering
  entities/
    people/        # 人物页
    organizations/ # 组织页
    products/      # 产品/项目/工具页
  themes/       # 横向主题页
  questions/    # 被问过且值得沉淀的问题/答案
  syntheses/    # 多来源综合、比较、判断
  claims/       # 重要论断、冲突、证据链、待验证项
  outputs/
    slides/     # Marp/演示稿
    charts/     # 图表/数据产物

templates/      # 供 LLM 复制使用的页面模板
```

## Wiki 写作原则

### 语言与术语规范

- `wiki/` 中的正文、摘要、综合、问题回答、日志说明默认使用中文。
- 核心英文名词可以保留，但首次出现或不易懂时必须给中文解释，推荐格式：`中文解释（English Term）`；如果英文是更常用的术语，可写作 `English Term（中文解释）`。
- 来源标题、产品名、组织名、人名、文件名、API/CLI/代码标识符保留原文，不强行翻译。
- 概念页标题可以保留英文 canonical name，但定义段必须先用中文解释它是什么、为什么重要。
- 避免整段英文照搬到 wiki 层；引用原文只保留必要短句，其余用中文转述。
- 对高频但不直观的术语维护中文释义，例如：`harness（智能体工作支架/运行环境）`、`feedforward guides（生成前引导）`、`feedback sensors（生成后反馈检测器）`、`middleware（中间件/调用拦截层）`、`trace（执行轨迹）`、`session handoff（跨会话交接）`、`compaction（上下文压缩）`。

- 保持 Obsidian 原生：优先使用 `[[wiki/路径/页面名]]` 双链；外部来源使用 Markdown 链接。
- `raw/` 是事实来源，不在 ingest 中改写；如发现 raw 元数据错误，先在 `wiki/log.md` 记录，再询问是否修正。
- `wiki/` 页面可以被 LLM 持续修改，但修改必须有来源依据或明确标记为推断。
- 每篇 wiki 页面尽量包含 YAML frontmatter：`type`、`status`、`created`、`updated`、`sources`、`tags`。
- 页面命名优先中文；若英文术语是领域内 canonical name，可保留英文标题，但页面开头必须给出中文解释。同一概念只保留一个 canonical page，其他名称用别名/重定向说明。
- 不确定内容标记为 `待验证`，不要伪装成结论。
- 多来源冲突要写进 `wiki/claims/` 或相关页面的“冲突/待验证”段落。

## Ingest 工作流

当用户要求处理一个新来源：

1. 读取对应 `raw/` 文件；若有本地图片，必要时一起查看。
2. 在 `wiki/sources/` 创建或更新来源摘要页，使用 `templates/source-summary.md`。
3. 抽取并更新相关概念页、实体页、主题页、论断页。
4. 更新 `wiki/index.md`：新增页面、状态、1 行摘要。
5. 如有总览变化，更新 `wiki/overview.md`。
6. 向 `wiki/log.md` 追加一条 `## [YYYY-MM-DD] ingest | 标题` 记录。
7. 最后报告：创建/更新了哪些文件、关键结论、待验证事项。

## Query 工作流

当用户提问：

1. 先读 `wiki/index.md`，再读相关 wiki 页面；必要时回到 `raw/` 查证。
2. 回答中区分：已由来源支持的结论、推断、待验证项。
3. 如果答案有长期价值，询问或直接沉淀到 `wiki/questions/` 或 `wiki/syntheses/`。
4. 产出新页面时同步更新 `wiki/index.md` 和 `wiki/log.md`。

## Lint 工作流

定期检查：

- 孤立页面、重复概念、断链、未建实体页。
- 新来源是否推翻旧结论。
- `wiki/index.md` 是否遗漏页面。
- `wiki/log.md` 是否保持追加式格式。
- 哪些重要概念只在 raw 中出现但还没有 wiki 页面。

建议日志标题格式：

```md
## [YYYY-MM-DD] ingest | Source Title
## [YYYY-MM-DD] query | Question Title
## [YYYY-MM-DD] lint | Scope
```
