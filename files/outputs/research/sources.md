# 来源清单（GLM-5.3 与高级网络能力扩散）

> 用途：供 Pi 撰稿的来源索引。核查日期：2026-10-04。
> 访问情况以本次 Runtime 中的工具调用和返回为准。WebFetch 返回的是模型生成的页面摘要，不是逐字全文，所以下面的“原文位置”是按摘要报告的章节或图表标注，引用前建议人工打开原页复核。
> 每个来源的英文逐字引用合计不超过 25 词，其余均为中文转述。
> 关键数字及其分母集中写在 `fact-check.md`，本文件只放元数据和简述。

图例：**[已访问]** 本次成功获取并阅读；**[未能访问]** 本次获取失败，不作为已核实证据。

---

## S1 指定原文：Anthropic 研究文章 [已访问]

- **标题**：GLM-5.3 and the spread of advanced cyber capabilities
- **发布者 / 作者**：Anthropic；Andrew Fasano、Marius Fleischer、Cole McFaul、Robert Xiao、Tripp Gallagher
- **日期**：2026-09-29
- **URL**：<https://www.anthropic.com/research/glm-5-3-and-the-spread-of-advanced-cyber-capabilities>
- **原文结构**：引言；“GLM-5.3 can develop working exploits end to end”（Figure 2，含 GLM-5.3-Flash 案例）；“GLM-5.3 lacks robust safeguards”（Figure 5）；“What does this mean?”（建议部分）
- **简述（约 120 字）**：Anthropic 认为，开放权重模型 GLM-5.3 在其漏洞利用评测上接近 Claude Mythos Preview；Flash 版在沙箱里、研究者提供已知漏洞信息的情况下做出了利用链；在模拟环境中，GLM-5.3 的防护措施容易被提示词、预填充和去拒绝化手段削弱。文章建议防守方尽快采用 AI 工具，政府对后继模型开展安全测试。数字见 F1–F4。
- **性质与局限**：这是同时开发竞品模型的厂商的自评，属于“厂商说法”，但给出了方法细节。文章自己也承认，模拟环境不能完全代表现实条件。

## S2 NIST/CAISI 对 GLM-5.3 的评估 [未能访问]

- **URL**：<https://www.nist.gov/news-events/news/2026/09/caisis-assessment-zais-glm-53-cyber-capabilities>（标题“CAISI's Assessment of Z.ai's GLM-5.3 Cyber Capabilities”由搜索结果得到）
- **访问情况**：本次 WebFetch 返回“proxy refused the connection”，正文未读到。
- **可用范围**：只能写“S1 称 CAISI 于 9 月 17 日发布评估，结论是 GLM-5.3 为迄今网络能力最强的开放权重模型，落后美国前沿约四个月”，并注明为**转引、未直接核验**。搜索摘要里提到的发布日期、基准数量等细节不作为论据。

## S3 ExploitBench 原始评测论文 [已访问：arXiv 摘要页 + HTML 全文页]

- **标题**：ExploitBench: A Capability Ladder Benchmark for LLM Cybersecurity Agents
- **作者**：Seunghyun Lee、David Brumley
- **日期**：arXiv v1 提交于 2026-05-13（arXiv:2605.14153）
- **URL**：<https://arxiv.org/abs/2605.14153>（HTML：<https://arxiv.org/html/2605.14153>）
- **原文位置**：摘要；§1 Introduction（批评以往框架只给单一通过/失败）；§2.3 “Capability Ladder”（五个层级共 16 个 flag，单次运行的奖励是一个 flag 位图）；Tables 1–3（模型停在中间层级的结果）；§5 Discussion 的“Limitations”小节（“1-day-with-patch”设定会把覆盖信号泄露给低层能力）。
- **证据摘要**：这个基准把漏洞利用拆成从代码覆盖、崩溃到控制流劫持、任意代码执行的分级能力，所以“拿到部分 flag”和“完成端到端利用”是两种口径。
- **局限**：论文页没有出现 GLM-5.3，S1 的 410 次尝试不来自这篇论文。作者自承带补丁的设定会给低层级带来人为优势。

## S4 Z.ai 官方 Hugging Face 模型卡 [已访问]

- **标题**：zai-org/GLM-5.3
- **发布者**：Z.ai（zai-org）
- **日期**：模型卡正文未写发布日期。**不用仓库创建日期推断发布日期**；摘要中关联的 arXiv 2602.15763 日期也不代表 GLM-5.3 的发布时间。
- **URL**：<https://huggingface.co/zai-org/GLM-5.3>
- **原文位置**：页面元数据（License、参数量、张量类型）；章节“Serve GLM-5.3 Locally”（列出 SGLang、vLLM、Transformers 等本地部署框架）。
- **可直接核验的信息**：权重可公开下载（safetensors 格式，BF16/F8_E4M3/F32），约 753B 参数，许可证字段标为“GLM-5.3”（具体条款未读到），页面支持本地部署。
- **局限**：本次没有在模型卡中看到明确的安全或滥用声明，也没有提到 Flash 版本。卡中“网络能力领先”等表述属于厂商说法，本资料包不采用其中的基准分数。

## S5 Z.ai 官方开发者文档 [已访问]

- **标题**：GLM-5.3（docs.z.ai 指南页）
- **发布者**：Z.ai
- **日期**：页面未写日期
- **URL**：<https://docs.z.ai/guides/llm/glm-5.3>
- **原文位置**：Overview（与 GLM-5.2 同一基座，改进来自后训练）；Capability Support（1M 上下文、最大 128K 输出、仅文本输入、强制思考模式）；Key Advancements（称漏洞利用类基准得分是 GLM-5.2 的两倍以上，提到“Z.ai Security Disclosure Ledger”）。
- **证据摘要**：说明这个模型同时通过 API 或订阅计划提供，厂商自己也把网络安全能力当作卖点。
- **局限**：均为**厂商说法**，未见独立复核；页面未列明价格（S1 的 20.40 美元按“Zhipu API 价格”估算，两者无法互相印证）。

## S6 Mandiant / Google Cloud：2023 年利用时间趋势 [已访问]

- **标题**：How Low Can You Go? An Analysis of 2023 Time-to-Exploit Trends
- **作者**：Casey Charrier、Robert Weiner（Mandiant，Google Cloud 威胁情报博客）
- **日期**：2024-10-15
- **URL**：<https://cloud.google.com/blog/topics/threat-intelligence/time-to-exploit-trends-2023>
- **原文位置**：“Time-to-Exploit”章节（TTE 定义、5 天 / 47 天、历年对比）；零日与 n-day 比例段落；n-day 利用时间线段落；方法说明段（称数据是保守估计）。
- **证据摘要**：这是独立的在野观测数据，说明补丁窗口在 AI 因素之前就已经很短。核心口径见 F6。
- **局限**：2023 年的样本无法说明 AI 的影响。首次利用日期常常模糊，作者按最晚可能日期计，所以作者认为真实的利用时间更早。

## S9 Arditi 等：拒绝行为由单一方向介导 [已访问]

- **标题**：Refusal in Language Models Is Mediated by a Single Direction
- **作者**：Andy Arditi、Oscar Obeso、Aaquib Syed、Daniel Paleka、Nina Panickssery、Wes Gurnee、Neel Nanda
- **日期**：v1 2024-06-17；v3 2024-10-30
- **URL**：<https://arxiv.org/abs/2406.11717>
- **原文位置**：摘要（13 个开源对话模型，最大 72B；去掉某一激活方向后拒绝行为消失，增强该方向后连无害请求也会被拒绝）。
- **证据摘要**：这是独立同行研究，解释了 S1 所说“abliterated（去拒绝化）版本”为什么可行：一旦拿到开放权重，安全微调可以被定向移除。
- **局限**：研究对象是 2024 年的较小模型，没有测试 GLM-5.3。本资料只引用机制层面的结论，不涉及任何操作细节。

## S10 Google Threat Intelligence Group：AI 威胁追踪 [已访问]

- **标题**：GTIG AI Threat Tracker: From Prompting to Autonomy – The Evolution of Adversarial AI
- **发布者**：Google Threat Intelligence Group
- **日期**：2026-09-08
- **URL**：<https://cloud.google.com/blog/topics/threat-intelligence/from-prompting-to-autonomy-the-evolution-of-adversarial-ai>
- **原文位置**：Executive Summary；“Threat Actors Experiment with Agentic AI and AI-Enabled Automation”；“Threat Actors Integrate AI into Multiple Attack Lifecycle Stages”；“How Google Protects Against AI Abuse”（防守措施）。
- **证据摘要**：在野观察显示，威胁行为者正从简单提示走向智能体化、自动化的工作流（报告提到一次凭证窃取活动在六小时内完成规划与执行）。防守侧举措包括把威胁监测结果反馈给安全分类器、封禁滥用账户，以及 AI 辅助修复。
- **局限**：报告**没有提到 GLM-5.3**，在野案例**不能当作 GLM-5.3 被滥用的证据**。报告以 Gemini 为主，也是厂商视角（同时在推广自家防御产品）。

---

## 拓展链接（不作为本稿论据）

- S7、S8 在上一轮出现过（N-days 额外实验、Glasswing 初步更新），按收口要求已删除，不引用其中数字。
- 搜索中出现的二手报道（GIGAZINE、TNW、Notebookcheck、Business Standard 等）只说明公众关注度，不作为证据。
