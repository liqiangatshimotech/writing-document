# 当前已接受路线
计划：PLAN-04d0d0cf06cdf3ae6ac90ffb
目标：围绕 https://www.anthropic.com/research/glm-5-3-and-the-spread-of-advanced-cyber-capabilities 的议题完成原创中文深度研究和两份成稿。严格由Codex总编调度，worker-1 Claude资料研究员实际联网搜索核实，worker-2 Pi主笔写作，worker-3 Codex独立编辑审查验收；主Agent不得代替指定作者写正文。
仅规划两个有依赖的纯documentation任务、document输出，以文件产物包artifact_delivered交付：
任务1交给research能力的Claude：阅读指定原文，检索至少6个相关一手来源，优先Anthropic、NIST/CAISI、ExploitBench论文、Z.ai官方资料与可信防守建议。输出research/sources.md（标题、发布者、日期、URL、证据摘要与局限）和research/fact-check.md（关键数字/分母、实测与模拟区别、争议与不确定性）。无法访问来源应如实标注，不伪造阅读或引用。
任务2依赖任务1验收交付，交给writing能力的Pi，依据受控依赖资料输出：articles/wechat.md，3000至4500中文字符的公众号深度文，含3个备选标题、摘要、完整正文与参考来源；articles/douyin.md，约3至5分钟的科普口播稿，含3个标题、前5秒开场、完整可朗读正文、分段画面提示与来源。
讨论能力提升、可获得性、补丁窗口、开放权重利弊、评测局限和防守启示。原创综合分析，不逐段翻译或改写单篇来源；英文逐字引用每个来源不超过25词。数字可追溯，区分厂商说法/独立证据、事实/推论。特别核对64%/92%/100%的模拟有害请求响应指标，不能称为真实攻击成功率；不同评测分数/分母不可混用，不写“人人一键攻破所有系统”。不提供攻击代码、复现漏洞或绕过安全措施的操作教程。
写入范围仅research/与articles/。验收采用artifact文件哈希（artifact-hash-report）与独立内容审查（review.md），核对来源、事实、长度、可读性和文件完整性；纯文档不需虚构代码测试命令。研究先验收交付，Pi再写作；修改由原执行者完成。不合并main、不部署，不向公众号或抖音发布。最终提供两篇成稿和研究资料位置。
授权范围：仅提议两个串行、有依赖的纯 documentation 任务，由 main Codex 总编调度，worker-1 Claude 实际联网研究并核实，worker-2 Pi 根据研究验收交付的受控文件撰写两份成稿，worker-3 Codex 通过 Runtime 独立审查两阶段产物。主 Agent 不代写正文，修改由原执行者完成。业务文件写入仅限 research/ 与 articles/，交付类型仅为 artifact_delivered；不合并 main、不部署、不向公众号或抖音发布。Runtime 收集真实业务文件并生成 artifact-hash-report 和 review.md，工作者不制作验收报告。当前反馈未提供待处理审查或授权事项；执行调度与实时依赖核查以 SQLite Runtime 为准，本计划不授予进程、shell、审批或交付权限。

先处理现有待审结果；只推进已接受任务。没有可执行任务时等待事件。
