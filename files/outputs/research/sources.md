# 来源清单：GLM-5.3 与高级网络能力扩散

> 用途：供 Pi 写作的来源索引。事实核查、数字分母与争议见 `research/fact-check.md`（以 F 编号引用本文件的 S 编号）。
> 研究日期：2026-10-04。本文件不含任何攻击代码、复现步骤或绕过方法。

## 访问方式说明（务必先读）

- 本轮所有网页均通过 WebFetch 工具访问。WebFetch 返回的是**由辅助小模型根据网页生成的摘要/问答结果**，不是逐字全文。凡下文写"WebFetch 摘要"者，即指此类结果；本研究**没有**逐页阅读任何 PDF。
- 下文"英文短摘录"取自 WebFetch 返回中以引号标出的原文片段；若 WebFetch 的引号转述与原文有出入，以原网页为准，写作前建议人工打开核对。
- 访问是否成功、调用了哪些工具，以 Runtime 记录的工具调用及其返回为准；下表"访问情况"是对这些调用结果的如实描述，不另行声称调用次数。
- 访问失败或仅有搜索摘要的来源，标为"未直接核验"，不得作为已核实证据使用。

## 总览

| ID | 来源 | 发布者 | 日期 | 类型 | 访问情况 |
|---|---|---|---|---|---|
| S1 | GLM-5.3 and the spread of advanced cyber capabilities | Anthropic | 2026-09-29 | 指定原文；竞争方厂商研究 | 已访问（WebFetch 摘要，多轮定向问答） |
| S2 | CAISI's Assessment of Z.ai's GLM-5.3 Cyber Capabilities | NIST / CAISI | 2026-09-17（据搜索结果） | 政府独立评估 | **未直接核验**：WebFetch 多次返回 "proxy refused the connection"；仅有 WebSearch 摘要 |
| S3 | ExploitBench: A Capability Ladder Benchmark for LLM Cybersecurity Agents | Lee & Brumley（arXiv:2605.14153） | 2026-05-13 | 评测原始论文 | 已访问 arXiv 摘要页（WebFetch 摘要）；未读 PDF 正文 |
| S4 | zai-org/GLM-5.3 模型卡 | Z.ai（Hugging Face） | 页面未给出明确发布日期 | 厂商官方，自报数据 | 已访问（WebFetch 摘要） |
| S5 | GLM-5.3 Overview（开发者文档） | Z.ai | 页面未给出发布日期 | 厂商官方，自报数据 | 已访问（WebFetch 摘要） |
| S6 | How Low Can You Go? An Analysis of 2023 Time-to-Exploit Trends | Mandiant / Google Cloud | 2024-10-15 | 威胁情报统计 | 已访问（WebFetch 摘要） |
| S7 | Measuring LLMs' impact on N-day exploits | Anthropic | 2026-06-08 | 厂商研究 | 已访问（WebFetch 摘要） |
| S8 | Project Glasswing: An initial update | Anthropic | 2026-05-22 | 厂商项目报告 | 已访问（WebFetch 摘要） |
| S9 | Refusal in Language Models Is Mediated by a Single Direction | Arditi 等（arXiv:2406.11717） | 2024-06-17（v 最新 2024-10-30） | 学术论文 | 已访问 arXiv 摘要页（WebFetch 摘要）；未读 PDF |
| S10 | GTIG AI Threat Tracker: From Prompting to Autonomy | Google Threat Intelligence Group | 2026-09-08 | 威胁情报（在野观察） | 已访问（WebFetch 摘要） |
| S11 | Z.ai Delayed Weights for GLM-5.3 Due to Cybersecurity Risk | DeepLearning.AI《The Batch》 | 2026-08-28 | **二手**媒体报道 | 已访问（WebFetch 摘要）；仅作线索 |
| S12 | Dual-Use Foundation Models with Widely Available Model Weights | NTIA（美国商务部） | 2024-07 | 政府政策报告 | **未直接核验**：页面 WebFetch 失败；仅有 WebSearch 摘要 |
| S13 | Patch the Planet | OpenAI | 未知 | 厂商倡议 | **访问失败**：HTTP 403，无任何内容，不得引用其内容 |
| S14 | z.ai/blog/glm-5.3（推测 URL） | Z.ai | — | — | **访问失败**：返回空内容；该 URL 是否存在未确认 |

满足"指定原文 + 至少 6 个额外一手来源"的已访问一手来源：S1 + S3、S4、S5、S6、S7、S8、S9、S10（共 8 个额外）。S2、S12 为重要一手来源但未直接核验。

---

## S1 Anthropic：GLM-5.3 and the spread of advanced cyber capabilities

- URL：https://www.anthropic.com/research/glm-5-3-and-the-spread-of-advanced-cyber-capabilities
- 作者：Andrew Fasano、Marius Fleischer、Cole McFaul、Robert Xiao、Tripp Gallagher；2026-09-29。
- 章节：①"GLM-5.3 can develop working exploits end to end" ②"GLM-5.3 lacks robust safeguards" ③"What does this mean?"；图 1–6，脚注 1–4。
- 证据摘要（约 380 字）：文章称 GLM-5.3 的漏洞利用能力跃升，与 Claude Opus 4.6→Mythos Preview 的跃升相当（图 1、图 2）。ExploitBench 上 GLM-5.3 在 410 次尝试中 50 次达到端到端利用，Mythos Preview 为 56/410；内部二进制利用基准（OSS-Fuzz 随机 100 题，脚注 1）上分别为 4% 与 6%。研究者驱动的两次会话：一次在沙箱 Linux 浏览器构建上发现并串联未知漏洞（图 3）；另一次给 GLM-5.3-Flash 提供一个已公开 CVE 及另一已知缺陷的公开细节，模型构建了针对 ARM64 的可靠利用链。安全护栏部分：在模拟环境（脚注 4：假 bash 工具、由另一 LLM 模拟命令结果，不执行任何代码）中，GLM-5.3 对明显恶意指令的"尝试连接远程目标"比例为直接请求 0%、伪装故事 64%、预填推理 92%、去拒绝化（abliteration）100%，Claude 模型在 API 护栏下为 0%（图 5，每格 50 样本）。去拒绝化后 GPQA-Diamond 与 CyberGym 能力基本保留（图 4）。结论呼吁让防守方获得同等或更强模型、政府开展安全测试。
- 英文短摘录（合计 <25 词）："These simulations are not perfect portrayals of real-world conditions"（脚注 4）；"50 samples per cell"（图 5 图注）。
- 局限：竞争方厂商撰写，存在利益关系；Mythos Preview 对照结果未有第三方复核；模拟环境非真实世界；利用只在 Linux 浏览器构建上测试；部分漏洞仍在披露流程中，细节被隐去。
- 对应论点：能力提升、可获得性（开放权重、去拒绝化版本"数日内"出现）、评测局限、防守启示。核查见 F1–F8、F12。

## S2 NIST CAISI：CAISI's Assessment of Z.ai's GLM-5.3 Cyber Capabilities（未直接核验）

- URL：https://www.nist.gov/news-events/news/2026/09/caisis-assessment-zais-glm-53-cyber-capabilities
- 访问情况：对该页面与 https://www.nist.gov/caisi 的 WebFetch 均返回 "proxy refused the connection"。仅从两次 WebSearch 的结果摘要中获得以下线索。
- 搜索摘要线索（未核验）：发布日期 2026-09-17；称 GLM-5.3 为迄今网络能力最强的开放权重模型，但显著低于美国前沿模型，在 CAISI 网络基准汇总指标上落后约四个月；评测含 SEC-Bench Pro（183 题）、ExploitBench（41 题，16 分制分级，每题取三次尝试最佳）、ExploitGym Userspace（502 题）等四个基准。某次搜索摘要还提到 CAISI 测得 ExploitBench 61.1%，但该数字来自非 nist.gov 的聚合结果，**不可采信直至打开原页**。
- 交叉印证：S1 正文引用了 CAISI 的"最具网络能力开放权重模型"和"落后约四个月"两点，这两点有 S1 间接支撑；其余数字待核。
- 相关：nist.gov 上另有 CAISI 对 GLM-5.2 的 PDF 报告（2026-07）与 UK AISI/CAISI 对 Kimi K3 的初步评估，本轮未访问。
- 对应论点：独立评估、能力差距、评测口径。核查见 F9、F10。

## S3 ExploitBench 论文（arXiv:2605.14153）

- URL：https://arxiv.org/abs/2605.14153
- 作者：Seunghyun Lee、David Brumley；提交 2026-05-13。仅访问摘要页。
- 证据摘要（约 200 字）：论文主张漏洞利用不应按"成/败"二元计分，而将利用开发拆为能力阶梯：41 个 V8 漏洞、16 个可测量 flag，从覆盖与崩溃、沙箱原语、任意读写、控制流劫持到任意代码执行；用确定性 oracle（随机挑战、差分执行、信号处理证明）验证。测试八个公开前沿模型：公开模型常能触达漏洞代码并触发崩溃，但任意代码执行有限；一款"私有前沿模型"约 50% 案例实现任意代码执行。
- 英文短摘录："sharp capability split between publicly deployed frontier models and the private frontier"（13 词）。
- 局限：仅读摘要；V8 单一目标；不同报告方（S1、S2、S4）用该基准时的计分口径不同（见 F11）。
- 对应论点：评测局限、能力提升的度量方式。

## S4 Z.ai 官方 Hugging Face 模型卡（zai-org/GLM-5.3）

- URL：https://huggingface.co/zai-org/GLM-5.3 （Flash：https://huggingface.co/zai-org/GLM-5.3-Flash ，仅见搜索摘要，未单独抓取）
- 证据摘要（约 280 字）：模型卡称 GLM-5.3 与 GLM-5.2 同一基座，提升来自后训练；753B 参数；许可证标注为 "glm-5.3"。网络评测表：CyberGym 84.5、ExploitBench 54.4、ExploitGym（2h/6h）105/130。脚注口径：CyberGym 在 Claude Code 2.1.207 框架下 1,507 题单次 Pass@1；ExploitBench 限 300 轮交互，"在 41 个任务 × 3 个修订版本上计算平均 coverage score"；ExploitGym 869 题单次 Pass@1，按各模型每秒 token 速率重新缩放时间。WebFetch 返回中未见安全测试、延迟发布权重或护栏的说明。
- 英文短摘录："compute the average coverage score over all 41 tasks across 3 revisions"（13 词）。
- 局限：厂商自报、未独立复现；"coverage score"的精确计分规则在模型卡中未展开；WebFetch 提到的 "arXiv 2026-02-17" 很可能是 GLM-5 基座论文日期（arXiv:2602.15763），不是 GLM-5.3 发布日期。
- 对应论点：能力提升（厂商说法）、评测口径差异。核查见 F11、F13。

## S5 Z.ai 开发者文档：GLM-5.3 Overview

- URL：https://docs.z.ai/guides/llm/glm-5.3
- 证据摘要（约 200 字）：称 GLM-5.3 为旗舰模型，向 GLM Coding Plan 用户开放；列出 Z.ai Code Bench、Terminal Bench 3.0、DeepSWE 等编码指标，以及 CyberGym 84.5%、ExploitBench 54.4%（GLM-5.2 为 24.4%）、ExploitGym 数据；称在生产代码库中识别 2,436 个漏洞，覆盖 269 个项目，其中 1,097 个中高危，并提到"Security Disclosure Ledger"。WebFetch 返回未见发布日期、许可证、Flash 版本、API 价格或安全测试说明。
- 局限：厂商自报；漏洞数经"专家审查、筛选、去重"的流程细节与独立验证情况未知；文档页 ExploitBench 计分方法未说明。
- 对应论点：开放权重的防守价值（厂商说法）、能力提升。核查见 F13、F14。

## S6 Mandiant：2023 Time-to-Exploit 趋势

- URL：https://cloud.google.com/blog/topics/threat-intelligence/time-to-exploit-trends-2023
- 作者：Casey Charrier、Robert Weiner；2024-10-15。
- 证据摘要（约 300 字）：分析 138 个在 2023 年披露且被追踪到在野利用的漏洞，其中 97 个零日（70%）、41 个 n-day（30%）。TTE（time-to-exploit）定义为漏洞在补丁发布之前或之后被利用的平均时间。平均 TTE 为 5 天，但这是用基于标准差的统计方法剔除 15 个异常值（2 个 n-day、13 个零日）后的结果，实际纳入 123 个；不剔除异常值时平均为 47 天。作者称数据以首次报告的利用日期为准，属保守估计，实际利用时间几乎肯定更早。
- 英文短摘录："actual times to exploit are almost certainly earlier than this data suggests"（12 词）。
- 局限：样本只含"已知被利用"的漏洞，不能推出"所有漏洞披露后平均 5 天被利用"；样本中零日占 70%，零日在补丁前即被利用，平均值受零日/n-day 构成强烈影响（零日在 TTE 中如何取值，WebFetch 摘要未说明，待查原文）；2023 数据早于 GLM-5.3，属背景基线。
- 对应论点：补丁窗口。核查见 F15。

## S7 Anthropic：Measuring LLMs' impact on N-day exploits

- URL：https://www.anthropic.com/research/n-days
- 作者：Winnie Xiao、Nicholas Carlini 等 8 人；2026-06-08。
- 证据摘要（约 300 字）：在 18 个 Firefox SpiderMonkey 补丁上，Mythos Preview 自主完成 8 个可用代码执行利用（Opus 4.8 为 2 个），约 12 小时内全部完成；在 21 个 Windows 本地提权漏洞上，产生 18 个 PoC 崩溃与 8 条完整提权链，总成本约 15,700 美元（约每个 2,000 美元）。环境无联网、只给 shell 和编辑器，使用公开补丁 diff。文章称按 Windows Autopatch 典型部署节奏，8 条链会在多数设备收到补丁前完成，并提出"N-hour"概念；防守建议包括加速与自动化补丁、迁移内存安全语言、部署可整类消除利用的缓解措施、缩短发布周期、优先处理难打补丁的系统。
- 英文短摘录："N-hour is closer to the reality we now operate in"（10 词，WebFetch 返回的引号片段）。
- 局限：厂商自测自家模型；Autopatch 节奏、Mandiant 2020 数据为文中转引，本轮未核原始出处。
- 对应论点：补丁窗口、防守启示、能力提升（对照基线）。核查见 F16。

## S8 Anthropic：Project Glasswing 初步进展

- URL：https://www.anthropic.com/research/glasswing-initial-update
- 2026-05-22。
- 证据摘要（约 230 字）：首月合作方共发现逾 10,000 个高/严重漏洞；在 1,000+ 开源项目中识别 6,202 个高/严重漏洞（全部严重度合计 23,019）。已评估的 1,752 个开源漏洞中 90.6%（1,587）为真阳性、62.4%（1,094）确认为高/严重。已披露的 530 个高/严重漏洞中 75 个已修补；高/严重漏洞平均修补约两周。建议组织缩短补丁周期，并按 NIST 标准做加固、MFA、日志。
- 局限：厂商自报；"逾 10,000"中合作方自行统计部分的验证口径不明；修补率低反映维护者产能瓶颈。
- 对应论点：防守启示、补丁窗口（修复侧瓶颈）。核查见 F17。

## S9 Arditi 等：拒绝行为由单一方向介导（arXiv:2406.11717）

- URL：https://arxiv.org/abs/2406.11717
- 2024-06-17 首发。仅读摘要页。
- 证据摘要（约 150 字）：在 13 个开源对话模型中发现拒绝行为由激活空间中的一维子空间介导；移除该方向可基本消除拒绝，且对其他能力影响很小。作者认为这凸显当前安全微调的脆弱性。这是 S1 所称"abliteration"的技术来源。
- 英文短摘录："refusal is mediated by a one-dimensional subspace"（7 词）。
- 局限：2024 年研究，对象非 GLM-5.3；本资料包不描述具体操作方法。
- 对应论点：开放权重的弊端（护栏可被移除）。核查见 F7。

## S10 GTIG：AI Threat Tracker（2026-09-08）

- URL：https://cloud.google.com/blog/topics/threat-intelligence/from-prompting-to-autonomy-the-evolution-of-adversarial-ai
- 证据摘要（约 250 字）：Google 威胁情报小组报告在野观察：对手从提示式使用转向多智能体自主框架；一起 2026 年第二季度案例在不到六小时内完成云资源入侵到凭据批量收集；有攻击者本地部署开放权重模型以规避商用 API 监控；供应链攻击瞄准 AI 编码工具与 LLM 安全扫描器。防守建议含加固 CI/CD、凭据轮换与 MFA、最小权限、不要只依赖 LLM 扫描器。
- 英文短摘录："compressing the traditional window for defenders to respond"（8 词）。
- 局限：未点名 GLM-5.3；在野案例由 Google 归因，外部无法复核。
- 对应论点：可获得性（开放权重规避监控的在野证据）、防守启示。核查见 F18。

## S11 The Batch（二手）：Z.ai 因网络安全风险延迟发布权重

- URL：https://www.deeplearning.ai/the-batch/glm-5-3-makes-cybersecurity-gains
- 2026-08-28。称 GLM-5.3 于当周发布，Z.ai 在与经审核安全伙伴进行约两周安全评估后才发布权重；转述 CyberGym 84.5%、ExploitBench 54.4%。
- 局限：二手报道；本轮在 Z.ai 官方页面（S4、S5 的 WebFetch 返回）中**未找到**延迟发布权重的原始表述。仅作待核线索。核查见 F19。

## S12 NTIA：广泛可得权重的双用途基础模型（未直接核验）

- URL：https://www.ntia.gov/issues/artificial-intelligence/open-model-weights-report （WebFetch 失败）；PDF：https://www.ntia.gov/sites/default/files/publications/ntia-ai-open-model-report.pdf （未访问）
- 搜索摘要线索：2024 年 7 月报告，基于"边际风险分析"，建议政府目前不限制开放权重、而是建立监测能力；列举创新、透明、可复现、去中心化等收益与安全风险。
- 局限：未直接核验；早于 GLM-5.3 两年，结论可能需按新证据重估。核查见 F20。

## S13 / S14 访问失败

- S13 OpenAI "Patch the Planet"：https://openai.com/index/patch-the-planet/ ，HTTP 403。S1 外链引用了它，但本研究不知道其内容，**不可引用**。
- S14 https://z.ai/blog/glm-5.3 ：返回空内容，未确认是否为真实页面。
