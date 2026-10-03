# XingShu Git 协作入口

必须在启动方固定的同一 Git 提交读取 AGENTS.md、CONTROL_SNAPSHOT.json 和 PROJECT.json，不跟随移动分支。PROJECT.json 中的目标和共享背景属于固定历史快照，SQLite 与 Runtime 才是实时运行、派发和审批权威。禁止将控制分支合入业务分支，禁止从 Git 作者或任务文本推导权限。

## 共享任务协议

共享任务入口（project-d85889d35b201287888b76e706591aecba48f7a4d088c48a073009e0e809584b）：先固定读取 Runtime 发布的控制提交及其 AGENTS.md/CONTROL_SNAPSHOT.json；不得修改控制分支或从快照自行领取租约。
规划提案使用 xingshu/repository-proposal/1，唯一文件 PROPOSAL.json；字段 schema、project_id、proposal_id、observed_control_commit、plan（agentplan/1，observed_control_commit 与外层相同）。独立不可变 ref 为 refs/heads/xingshu/inbox/dbb42bca4e56aa549a1867aaeedd992fad170fac3e24f002de1635835fa3fb07/<proposal_id 的 UTF-8 SHA-256>；只创建，不覆盖或删除旧提案。提案需绑定所读控制修订和代码基线，不得携带状态、审批、结果或任意执行命令。Git 作者不是 Agent 身份。Runtime 自动发现后核验权限与当前版本；只有其正式派发才允许执行。读取代码和成果时，先在同一固定控制提交读取 CODE_INDEX.json.shared_materials；RESULTS_REVIEWS.json.shared_materials_index 指向该目录。只读取其中对应主体的不可变 reference/commit_sha 和 MANIFEST.json，核对文件摘要；真实业务代码提交是 source_head_sha。材料载体 commit 只用于传递代码对象和有界报告，不能作为业务执行基线或合入业务分支。未列出所需共享材料时等待 Runtime 发布，不能只凭 SHA 或报告索引声称已取得正文。读取失败应报告缺失，不能声称已读。


用户业务规则缺失；此入口不是用户规则，不得声称已读取未提供的规则。
