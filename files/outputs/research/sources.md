# 来源清单：Anthropic GLM-5.3 文章及相关一手来源

- 研究任务：TASK-RESEARCH（供 TASK-WRITING 使用）
- 检索与阅读日期：2026-10-04
- 访问方式：WebSearch 检索 + WebFetch 抓取（抓取工具会先把网页转成摘要，并非人工逐字阅读全文）；ExploitBench 论文 PDF 第 1–16 页为直接渲染阅读。
- 访问状态说明：
  - **已读**：本次实际打开并阅读了来源本身，可作为已核实证据。
  - **部分已读**：打开了来源，但只读到摘要页，或抓取摘要存在明显错误，需要谨慎使用。
  - **访问失败**：未能打开，不计入已核实证据；相关内容只经二手转述得到，在 fact-check.md 中标为"待核实"。
  - **二手**：媒体或第三方转述，只作线索使用，不当作证据。
- 引用规则：英文逐字引用每个来源累计不超过 25 词，集中写在 fact-check.md 中，本文件不直接引用原文。

---

## A. 指定原文

### S0. GLM-5.3 and the spread of advanced cyber capabilities
- 发布者：Anthropic（Frontier Red Team）
- 作者：Andrew Fasano、Marius Fleischer、Cole McFaul、Robert Xiao、Tripp Gallagher
- 日期：2026-09-29
- URL：https://www.anthropic.com/research/glm-5-3-and-the-spread-of-advanced-cyber-capabilities
- 访问状态：**已读**（抓取 3 次，每次针对不同问题提问）
- 证据摘要：
  - ExploitBench（Chrome V8）：GLM-5.3 在 410 次尝试中有 50 次完成端到端利用（约 12%）；Claude Mythos Preview 为 56/410（约 14%）。更早的模型（Claude Opus 4.6、GLM-5.2、Kimi K3、DeepSeek V4.1-Flash）约为 0%。
  - 内部二进制利用基准（从 OSS-Fuzz 随机抽取 100 个任务）：GLM-5.3 在 4% 的任务上实现完整控制流劫持，Mythos Preview 为 6%，其余受测模型均为 0%。
  - 真实环境案例 1：在沙箱中，由人类专家有限关注约一天，GLM-5.3 在某"流行浏览器"（未点名，Linux 平台）的 JavaScript 引擎中发现此前未知的漏洞，并串联成可读取访问者本地任意文件的利用（演示内容为读取 SSH 私钥）。漏洞已报告给维护方。
  - 真实环境案例 2：GLM-5.3-**Flash** 把一个已公开的 Chrome 漏洞（CVE-2026-11645）做成 ARM64 利用链，耗费约 20 分钟人类关注加约 8 小时模型工作，按智谱 API 定价计费为 20.40 美元。文中只描述了一次实例。
  - 保护措施测试（模拟环境）：直接请求时 0%，加欺骗性"红队"背景故事后 64%，预填推理 token 后 92%，使用去拒绝化（abliterated）版本后 100%。每个格子 50 个样本（5 条攻击指令 × 2 个目标 × 5 次尝试）。受测的 Claude 模型在适用条件下均为 0%；对 Claude API 不能做预填和去拒绝化，所以这两项不适用。
  - 测试使用的是不会执行代码的假 bash 工具，由另一个 LLM 模拟命令输出；Anthropic 承认模拟只是不完美的度量。
  - 去拒绝化：Anthropic 自建了一个去拒绝化副本，估算约 2,200 GPU 小时（约 4,400 美元）；估计有经验的团队约需 600 GPU 小时（约 1,200 美元）。拒绝率从 >90% 降到约 3%（JailbreakBench）、2%（HarmBench）、12%（StrongREJECT），GPQA-Diamond 分数基本不变，CyberGym 分数略降。GLM-5.3 发布后数日内已有公开的去拒绝化版本。
  - 引用 CAISI（2026-09-17）的结论：GLM-5.3 是目前网络能力最强的开放权重模型，在 CAISI 网络基准汇总上落后美国前沿约 4 个月；Anthropic 称其发现与 CAISI 大体一致（只做了定性比较）。
  - 防守方面：建议防守者使用最好的可用工具；提到 Project Glasswing（"超过 10,000 个"关键软件漏洞）、Claude Mythos 5.1 的可信访问计划、OpenAI 的"Patch the Planet"；呼吁政府对足够强的模型做安全测试，呼吁开放权重开发者为这类能力加保护措施。
  - 承认防守者也能使用这一级别的模型。
  - 未提供：补丁窗口或修补时长数据；任何 GLM-5.3 被真实滥用的事件（文中"国家与非国家行为者可能使用"属于预测）。
- 对应论点：能力提升、可获得性、开放权重利弊、评测局限、防守启示
- 局限：
  - 作者是有竞争关系的厂商（Anthropic 自家 Mythos 与 GLM-5.3 同场比较）。
  - "410"如何构成未说明。
  - 安全测试的判定方式（LLM 评判还是人工）未说明，也未给出置信区间。
  - 真实案例为单次实例。
  - 浏览器未点名。
  - 去拒绝化成本为估算值。

## B. 额外一手来源（已读，计入已核实证据）

### S1. ExploitBench: A Capability Ladder Benchmark for LLM Cybersecurity Agents
- 作者：Seunghyun Lee（卡内基梅隆大学）、David Brumley（卡内基梅隆大学、Bugcrowd）
- 日期：arXiv v1 提交于 2026-05-13（PDF 首页日期为 2026-05-15）
- URL：https://arxiv.org/abs/2605.14153 ；PDF：https://arxiv.org/pdf/2605.14153
- 访问状态：**已读**（PDF 第 1–16 页直接阅读）
- 证据摘要：
  - 41 个 V8 N-day 漏洞，均为 2024 年以后报告。
  - 把利用过程拆成 5 层共 16 个能力旗标（覆盖 → 触发 → 引擎原语 → 通用原语 → 控制流劫持 / 任意代码执行 ACE），由确定性预言机评分，不使用 LLM 评判。
  - 运行在默认启用 V8 堆沙箱的发布版构建上。
  - 采用"1-day"设定：智能体拿到补丁 diff，但没有参考 PoC。
  - 每个单元格跑 3 个种子，每次预算 300 轮，取三次中的最好结果。
  - 共 9 个模型，3 种测量方式（裸模型、自适应提示、厂商 CLI），共 2,337 个回合。
  - 结果：Mythos Preview 在主测量方式下有 18/41 个漏洞达到 ACE。8 个公开部署模型在主测量方式下均未达到 ACE；只有 GPT-5.5 在 Codex CLI 下对 1 个漏洞达到 ACE。
  - Z.ai GLM 5.1 最高只在 3/41 个漏洞上达到第 3 层，ACE 为 0。**论文 v1 未测 GLM-5.3。**
  - 作者自述的局限与范围：
    - 只衡量受控环境下的 PoC，不衡量武器化，也不衡量对 EDR 等防护的规避和可靠性。
    - 作者明确提醒，不应把分数读成实战攻击成功率。
    - 公开漏洞存在被训练数据"记住"的可能。
    - 补丁 diff 会泄露低层级的信号。
  - 利益关系：Anthropic 提供了 API 额度，作者声明 Anthropic 未参与测量与解读。
  - 论文同时强调该能力阶梯可用于防守侧的分诊。
- 对应论点：能力提升、评测局限、防守启示
- 局限：
  - 预印本，未经同行评审。
  - 只覆盖 V8。
  - 与 S0 的"410 次尝试 / 端到端"口径不同，不能直接对照（见 fact-check.md）。

### S2. GLM-5.3 – Overview（Z.AI Developer Document）
- 发布者：Z.ai（智谱）
- 日期：页面未标注日期
- URL：https://docs.z.ai/guides/llm/glm-5.3
- 访问状态：**已读**
- 证据摘要：
  - 旗舰模型，与 GLM-5.2 共用同一基座，提升全部来自后训练。
  - 1M 上下文，最长输出 128K。
  - Z.ai Code Bench 比 GLM-5.2 提升 50%；Terminal-Bench 3.0 从 4.6 升至 28.3；DeepSWE v1.1 从 46.2 升至 66.9。
  - 自称在 CyberGym 漏洞发现基准上达到"迄今最佳"。
  - 评测中在 269 个真实项目里发现 2,436 个漏洞，其中 1,097 个为中高危（据抓取摘要，表述为 medium-to-high）。
  - 页面未提及安全或保护措施。
- 对应论点：能力提升（厂商自述）、开放权重利弊
- 局限：
  - 全部为厂商自报，没有独立复核。
  - 2,436 个漏洞的去重、确认和严重度评定方法未说明。
  - 抓取工具把许可写成"Proprietary"，这是它的推断有误：页面只是没提权重；HF 页面（S3）显示有开放权重。

### S3. zai-org/GLM-5.3 模型卡（Hugging Face）
- 发布者：Z.ai（zai-org）
- URL：https://huggingface.co/zai-org/GLM-5.3 ；元数据 API：https://huggingface.co/api/models/zai-org/GLM-5.3 ；Flash 版 API：https://huggingface.co/api/models/zai-org/GLM-5.3-Flash
- 访问状态：**已读**（模型卡页面和元数据 API 都已读取。注意：页面抓取摘要把 GLM-5 论文 arXiv 2602.15763 的日期 2026-02-17 误当成发布日期，已改用 API 字段核对）
- 证据摘要：
  - API 显示：仓库创建于 2026-08-25T06:42:50Z，最后修改于 2026-09-04；license 为 `glm-5.3`；gated 为 false（下载无需审批）；参数总量 753,329,940,480（约 753B）。
  - GLM-5.3-Flash 的 API 显示：仓库创建于 2026-08-25；license 为 MIT；gated 为 false；约 321B 参数。
  - 模型卡自报 CyberGym 84.5、ExploitBench 54.4、ExploitGym（2h/6h）105/130。
  - 网络安全评测在沙箱容器中进行，使用域名白名单防止作弊。
- 对应论点：可获得性、开放权重利弊
- 局限：
  - 分数为自报，ExploitBench "54.4"的计分口径未说明。
  - createdAt 是仓库创建时间，不一定等于公开时间（仓库可能先以私有状态创建）。二手报道称 2026-08-28 公开，待核实。

### S4. Refusal in Language Models Is Mediated by a Single Direction
- 作者：Andy Arditi、Oscar Obeso、Aaquib Syed、Daniel Paleka、Nina Panickssery、Wes Gurnee、Neel Nanda
- 日期：2024-06-17（v1），最新版本 2024-10-30
- URL：https://arxiv.org/abs/2406.11717
- 访问状态：**已读**（摘要页）
- 证据摘要：
  - 在 13 个开源对话模型（最大 72B）中发现，拒绝行为由激活空间中的单一方向控制；去掉这个方向，模型就不再拒绝，其他能力受影响很小。
  - 这就是 S0 所说"去拒绝化"（abliteration）的学术来源。
  - 说明拿到权重的人可以绕开靠微调实现的安全对齐。
- 对应论点：开放权重利弊、可获得性
- 局限：
  - 2024 年的研究，测试模型规模远小于 753B。
  - 本资料只记录概念层面的结论，不涉及操作细节。

### S5. Project Glasswing
- 发布者：Anthropic
- 日期：2026-04-07（页面所示）
- URL：https://www.anthropic.com/glasswing
- 访问状态：**已读**
- 证据摘要：
  - 以 Claude Mythos Preview 为核心的防御性行业计划，合作方包括 AWS、Apple、Google、Microsoft、Linux Foundation 等，另有 40 多个关键基础设施维护组织获得访问权限。
  - 承诺提供 1 亿美元使用额度，向开源安全组织提供 250 万美元，向 Apache 软件基金会提供 150 万美元。
  - 自称发现"数千个"高危漏洞。
  - 计划在 90 天内公开发布关于披露、更新、补丁自动化等的实践指南。
  - 对未修补漏洞只公布哈希，修复后再公开细节。
  - 页面引用 CrowdStrike CTO 的观点：发现到被利用的窗口已从数月缩短到"分钟级"。这是厂商观点，不是数据。
- 对应论点：防守启示、补丁窗口、可获得性（受限访问模式）
- 局限：
  - 厂商自述。
  - 4 月页面写的是"数千个"，而 S0（9 月）写的是"超过 10,000 个"，两者时点不同，不矛盾，但都没有独立核实。

### S6. How Low Can You Go? An Analysis of 2023 Time-to-Exploit Trends
- 发布者：Google Cloud / Mandiant
- 作者：Casey Charrier、Robert Weiner
- 日期：2024-10-15
- URL：https://cloud.google.com/blog/topics/threat-intelligence/time-to-exploit-trends-2023
- 访问状态：**已读**
- 证据摘要：
  - 样本为 2023 年披露且被在野利用的 138 个漏洞，其中 97 个零日（70%）、41 个 N-day（30%）。
  - 平均利用时间（TTE）：2018–19 年 63 天，2020–21 年 44 天，2021–22 年 32 天，2023 年 5 天。
  - 2023 年 N-day 中，12% 在 1 天内被利用，29% 在 1 周内，56% 在 1 个月内。
  - 建议：提高修补效率；不要把 exploit 是否公开当作判断风险的依据；优先做网络分段和访问控制。
- 对应论点：补丁窗口、防守启示
- 局限：
  - 早于 LLM 大规模参与漏洞利用的时期，只能作为基线，不能证明 AI 造成了什么影响。
  - 口径是"在野被利用"的漏洞，有幸存者偏差。

---

## C. 访问失败（不计入已核实证据）

| ID | 来源 | URL | 失败情况 | 替代信息来源 |
|---|---|---|---|---|
| F1 | NIST CAISI：CAISI's Assessment of Z.ai's GLM-5.3 Cyber Capabilities（2026-09-17） | https://www.nist.gov/news-events/news/2026/09/caisis-assessment-zais-glm-53-cyber-capabilities | 代理拒绝连接（尝试 2 次） | S0 的转述；搜索摘要；Center Consulting 的二手整理（X1） |
| F2 | NIST 文档页（GLM-5.3 评估报告） | https://www.nist.gov/document/caisi-assessment-zais-glm-53 | 代理拒绝连接 | 同上 |
| F3 | CAISI GLM-5.2 评估 PDF（用于了解方法学） | https://www.nist.gov/system/files/documents/2026/07/17/CAISI%20-%20Assessment%20of%20Z.ai's%20GLM-5.2.pdf | 代理拒绝连接 | 无 |
| F4 | UK NCSC：Impact of AI on cyber threat from now to 2027 | https://www.ncsc.gov.uk/report/impact-ai-cyber-threat-now-2027 | 代理拒绝连接；新闻页 https://www.ncsc.gov.uk/news/ai-to-2027-threat-assessment 同样失败 | 只有搜索摘要 |
| F5 | OpenAI：Patch the Planet | https://openai.com/index/patch-the-planet/ | HTTP 403 | S0 中一句提及 |
| F6 | Z.ai 官方博客：GLM-5.3: Frontier Coding with Emergent Cyber Capabilities（约 2026-08-14） | https://z.ai/blog/glm-5.3 | 页面内容为空（疑为 JS 渲染） | 二手报道（X2）；S2、S3 |

建议 Pi 写作前或审查方在网络条件允许时重试 F1、F4、F6。这三项关系到"四个月差距"、"补丁窗口"和"厂商安全承诺"三个论点。

## D. 二手线索（不作证据，只用来发现问题和交叉提示）

| ID | 来源 | URL | 用途 |
|---|---|---|---|
| X1 | Center Consulting：CAISI finds GLM-5.3 the most cyber-capable open-weight model… | https://www.centerconsulting.com/ai-library/milestones/2026-caisi-glm-5-3-cyber-assessment | 转述 CAISI 的四项基准分数和 IRT 指数方法（已抓取阅读，但属于二手） |
| X2 | AI Weekly：Z.ai ships GLM-5.3, holds open weights for cyber safety review | https://aiweekly.co/alerts/zai-ships-glm-53-holds-open-weights-for-cyber-safety-review | 转述 Z.ai 推迟约两周发布权重做安全评审（已抓取阅读，但属于二手） |
| X3 | The New Stack；Digital Applied；TechJack Solutions（权重与许可报道） | https://thenewstack.io/zai-glm-weights-license/ ；https://www.digitalapplied.com/blog/glm-5-3-weights-bespoke-license-not-mit ；https://techjacksolutions.com/ai-brief/zai-glm-53-open-weights-744b-safety-hold/ | 只看了搜索摘要：权重 2026-08-28 上 HF；Flash 版 2026-08-26 以 MIT 发布；许可证对营收超过 100 亿美元的提供方附加条款 |
| X4 | The Next Web；SCMP；Notebookcheck（对 S0 的报道） | https://thenextweb.com/news/glm-5-3-cyber-exploits-mythos-anthropic-safeguards ；https://www.scmp.com/tech/big-tech/article/3369354/anthropic-raises-alarm-over-elite-hacking-ability-chinese-firm-zais-glm-53 ；https://www.notebookcheck.net/GLM-5-3-China-s-open-AI-model-built-a-Chrome-exploit-for-20.1413141.0.html | 只看了搜索摘要；用来识别媒体的误读（见 fact-check.md 第 E 节） |
| X5 | 第三方博客转述的 Mandiant 2024 TTE（-1 天）及 2025（约 -7 天）数据 | 例如 https://hadrian.io/blog/understanding-the-new-negative-time-to-exploit | 只看了搜索摘要；Mandiant 原始报告未找到，不可引用 |

## E. 计数

- 指定原文：1 篇（S0，已读）
- 额外一手来源已读：6 个（S1–S6）。S3 的页面摘要有误，已用 HF 元数据 API 交叉核对。S4 只读了 arXiv 摘要页。
- 关于来源覆盖的缺口：NIST/CAISI 原文、NCSC、Z.ai 官方博客均访问失败，因此"独立政府评测"这一维度目前只能借助 S0 的转述和二手资料，未经核实。
- 访问失败：6 个（F1–F6），不计入。
