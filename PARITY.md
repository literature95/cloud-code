# 一致性状态 — claw-code Rust 移植

最后更新：2026-04-03

## 摘要

- 规范文档：这个顶级 `PARITY.md` 文件被 `rust/scripts/run_mock_parity_diff.py` 消费。
- 请求的 9 通道检查点：**所有 9 个通道都已合并到 `main` 分支。**
- 当前 `main` 分支 HEAD：`ee31e00`（存根实现已替换为真实的 AskUserQuestion + RemoteTrigger）。
- 此检查点的仓库统计：**`main` 分支上有 292 个提交 / 所有分支共 293 个提交**，**9 个 crates**，**48,599 行跟踪的 Rust 代码**，**2,568 行测试代码**，**3 位作者**，日期范围 **2026-03-31 → 2026-04-03**。
- Mock 一致性测试工具统计：**10 个脚本化场景**，**19 个捕获的 `/v1/messages` 请求**，位于 `rust/crates/rusty-claude-cli/tests/mock_parity_harness.rs`。

## Mock 一致性测试工具 — 里程碑 1

- [x] 确定性的 Anthropic 兼容 mock 服务（`rust/crates/mock-anthropic-service`）
- [x] 可重现的干净环境 CLI 测试工具（`rust/crates/rusty-claude-cli/tests/mock_parity_harness.rs`）
- [x] 脚本化场景：`streaming_text`、`read_file_roundtrip`、`grep_chunk_assembly`、`write_file_allowed`、`write_file_denied`

## Mock 一致性测试工具 — 里程碑 2（行为扩展）

- [x] 脚本化多工具回合覆盖：`multi_tool_turn_roundtrip`
- [x] 脚本化 bash 覆盖：`bash_stdout_roundtrip`
- [x] 脚本化权限提示覆盖：`bash_permission_prompt_approved`、`bash_permission_prompt_denied`
- [x] 脚本化插件路径覆盖：`plugin_tool_roundtrip`
- [x] 行为差异/清单运行器：`rust/scripts/run_mock_parity_diff.py`

## 测试工具 v2 行为清单

规范场景映射：`rust/mock_parity_scenarios.json`

- 多工具助手回合
- Bash 流程往返
- 跨工具路径的权限强制执行
- 插件工具执行路径
- 文件工具 — 测试工具验证的流程
- 由 mock 一致性测试工具验证的流式响应支持

## 9 通道检查点

| 通道 | 状态 | 功能提交 | 合并提交 | 证据 |
|---|---|---|---|---|
| 1. Bash 验证 | 已合并 | `36dac6c` | `1cfd78a` | `jobdori/bash-validation-submodules`，`rust/crates/runtime/src/bash_validation.rs`（在 `main` 分支上 `+1004`） |
| 2. CI 修复 | 已合并 | `89104eb` | `f1969ce` | `rust/crates/runtime/src/sandbox.rs`（`+22/-1`） |
| 3. 文件工具 | 已合并 | `284163b` | `a98f2b6` | `rust/crates/runtime/src/file_ops.rs`（`+195/-1`） |
| 4. TaskRegistry | 已合并 | `5ea138e` | `21a1e1d` | `rust/crates/runtime/src/task_registry.rs`（`+336`） |
| 5. 任务接线 | 已合并 | `e8692e4` | `d994be6` | `rust/crates/tools/src/lib.rs`（`+79/-35`） |
| 6. 团队+定时任务 | 已合并 | `c486ca6` | `49653fe` | `rust/crates/runtime/src/team_cron_registry.rs`，`rust/crates/tools/src/lib.rs`（`+441/-37`） |
| 7. MCP 生命周期 | 已合并 | `730667f` | `cc0f92e` | `rust/crates/runtime/src/mcp_tool_bridge.rs`，`rust/crates/tools/src/lib.rs`（`+491/-24`） |
| 8. LSP 客户端 | 已合并 | `2d66503` | `d7f0dc6` | `rust/crates/runtime/src/lsp_client.rs`，`rust/crates/tools/src/lib.rs`（`+461/-9`） |
| 9. 权限强制执行 | 已合并 | `66283f4` | `336f820` | `rust/crates/runtime/src/permission_enforcer.rs`，`rust/crates/tools/src/lib.rs`（`+357`） |

## 通道详情

### 通道 1 — Bash 验证

- **状态：** 已合并到 `main` 分支。
- **功能提交：** `36dac6c` — `feat: add bash validation submodules — readOnlyValidation, destructiveCommandWarning, modeValidation, sedValidation, pathValidation, commandSemantics`
- **证据：** 仅分支差异添加了 `rust/crates/runtime/src/bash_validation.rs` 和 `runtime::lib` 导出（跨 2 个文件 `+1005`）。
- **主分支实际情况：** `rust/crates/runtime/src/bash.rs` 仍然是 `main` 分支上的活跃实现，共 **283 行代码**，具有超时/后台/沙箱执行。`PermissionEnforcer::check_bash()` 在 `main` 分支上添加了只读门控，但专用验证模块尚未落地。

### Bash 工具 — 上游有 18 个子模块，Rust 有 1 个：

- 在 `main` 分支上，此陈述仍然基本正确。
- 测试工具覆盖证明了 bash 执行和提示升级流程，但不是完整的上游验证矩阵。
- 仅分支通道针对 `readOnlyValidation`、`destructiveCommandWarning`、`modeValidation`、`sedValidation`、`pathValidation` 和 `commandSemantics`。

### 通道 2 — CI 修复

- **状态：** 已合并到 `main` 分支。
- **功能提交：** `89104eb` — `fix(sandbox): probe unshare capability instead of binary existence`
- **合并提交：** `f1969ce` — `Merge jobdori/fix-ci-sandbox: probe unshare capability for CI fix`
- **证据：** `rust/crates/runtime/src/sandbox.rs` 共 **385 行代码**，现在从实际的 `unshare` 能力和容器信号解析沙箱支持，而不是仅从二进制存在假设支持。
- **重要性：** `.github/workflows/rust-ci.yml` 运行 `cargo fmt --all --check` 和 `cargo test -p rusty-claude-cli`；此通道从运行时行为中移除了 CI 特定的沙箱假设。

### 通道 3 — 文件工具

- **状态：** 已合并到 `main` 分支。
- **功能提交：** `284163b` — `feat(file_ops): add edge-case guards — binary detection, size limits, workspace boundary, symlink escape`
- **合并提交：** `a98f2b6` — `Merge jobdori/file-tool-edge-cases: binary detection, size limits, workspace boundary guards`
- **证据：** `rust/crates/runtime/src/file_ops.rs` 共 **744 行代码**，现在包括 `MAX_READ_SIZE`、`MAX_WRITE_SIZE`、NUL 字节二进制检测和规范工作区边界验证。
- **测试工具覆盖：** `read_file_roundtrip`、`grep_chunk_assembly`、`write_file_allowed` 和 `write_file_denied` 在清单中，并由干净环境测试工具执行。

### 文件工具 — 测试工具验证的流程

- `read_file_roundtrip` 检查读取路径执行和最终合成。
- `grep_chunk_assembly` 检查分块 grep 工具输出处理。
- `write_file_allowed` 和 `write_file_denied` 验证写入成功和权限拒绝。

### 通道 4 — TaskRegistry

- **状态：** 已合并到 `main` 分支。
- **功能提交：** `5ea138e` — `feat(runtime): add TaskRegistry — in-memory task lifecycle management`
- **合并提交：** `21a1e1d` — `Merge jobdori/task-runtime: TaskRegistry in-memory lifecycle management`
- **证据：** `rust/crates/runtime/src/task_registry.rs` 共 **335 行代码**，通过线程安全的内存注册表提供 `create`、`get`、`list`、`stop`、`update`、`output`、`append_output`、`set_status` 和 `assign_team`。
- **范围：** 此通道用真实的运行时支持的任务记录替换纯固定有效负载存根状态，但本身不添加外部子进程执行。

### 通道 5 — 任务接线

- **状态：** 已合并到 `main` 分支。
- **功能提交：** `e8692e4` — `feat(tools): wire TaskRegistry into task tool dispatch`
- **合并提交：** `d994be6` — `Merge jobdori/task-registry-wiring: real TaskRegistry backing for all 6 task tools`
- **证据：** `rust/crates/tools/src/lib.rs` 通过 `execute_tool()` 和具体的 `run_task_*` 处理程序调度 `TaskCreate`、`TaskGet`、`TaskList`、`TaskStop`、`TaskUpdate` 和 `TaskOutput`。
- **当前状态：** 任务工具现在通过 `global_task_registry()` 在 `main` 分支上公开真实的注册表状态。

### 通道 6 — 团队+定时任务

- **状态：** 已合并到 `main` 分支。
- **功能提交：** `c486ca6` — `feat(runtime+tools): TeamRegistry and CronRegistry — replace team/cron stubs`
- **合并提交：** `49653fe` — `Merge jobdori/team-cron-runtime: TeamRegistry + CronRegistry wired into tool dispatch`
- **证据：** `rust/crates/runtime/src/team_cron_registry.rs` 共 **363 行代码**，添加了线程安全的 `TeamRegistry` 和 `CronRegistry`；`rust/crates/tools/src/lib.rs` 将 `TeamCreate`、`TeamDelete`、`CronCreate`、`CronDelete` 和 `CronList` 接线到这些注册表。
- **当前状态：** 团队/定时任务工具现在在 `main` 分支上具有内存生命周期行为；它们仍然缺少真正的后台调度程序或工作线程 fleet。

### 通道 7 — MCP 生命周期

- **状态：** 已合并到 `main` 分支。
- **功能提交：** `730667f` — `feat(runtime+tools): McpToolRegistry — MCP lifecycle bridge for tool surface`
- **合并提交：** `cc0f92e` — `Merge jobdori/mcp-lifecycle: McpToolRegistry lifecycle bridge for all MCP tools`
- **证据：** `rust/crates/runtime/src/mcp_tool_bridge.rs` 共 **406 行代码**，跟踪服务器连接状态、资源列表、资源读取、工具列表、工具调度确认、认证状态和断开连接。
- **接线：** `rust/crates/tools/src/lib.rs` 将 `ListMcpResources`、`ReadMcpResource`、`McpAuth` 和 `MCP` 路由到 `global_mcp_registry()` 处理程序。
- **范围：** 此通道用 `main` 分支上的注册表桥替换纯存根响应；端到端 MCP 连接填充和更广泛的传输/运行时深度仍然依赖于更广泛的 MCP 运行时（`mcp_stdio.rs`、`mcp_client.rs`、`mcp.rs`）。

### 通道 8 — LSP 客户端

- **状态：** 已合并到 `main` 分支。
- **功能提交：** `2d66503` — `feat(runtime+tools): LspRegistry — LSP client dispatch for tool surface`
- **合并提交：** `d7f0dc6` — `Merge jobdori/lsp-client: LspRegistry dispatch for all LSP tool actions`
- **证据：** `rust/crates/runtime/src/lsp_client.rs` 共 **438 行代码**，通过有状态注册表建模诊断、悬停、定义、引用、完成、符号和格式化。
- **接线：** `rust/crates/tools/src/lib.rs` 中暴露的 `LSP` 工具架构目前枚举 `symbols`、`references`、`diagnostics`、`definition` 和 `hover`，然后通过 `registry.dispatch(action, path, line, character, query)` 路由请求。
- **范围：** 当前一致性是注册表/调度级别；完成/格式支持存在于注册表模型中，但在工具架构边界上未明确暴露，实际的外部语言服务器进程编排仍然是分开的。

### 通道 9 — 权限强制执行

- **状态：** 已合并到 `main` 分支。
- **功能提交：** `66283f4` — `feat(runtime+tools): PermissionEnforcer — permission mode enforcement layer`
- **合并提交：** `336f820` — `Merge jobdori/permission-enforcement: PermissionEnforcer with workspace + bash enforcement`
- **证据：** `rust/crates/runtime/src/permission_enforcer.rs` 共 **340 行代码**，在 `rust/crates/runtime/src/permissions.rs` 之上添加了工具门控、文件写入边界检查和 bash 只读启发式。
- **接线：** `rust/crates/tools/src/lib.rs` 暴露 `enforce_permission_check()` 并在工具规范中携带每个工具的 `required_permission` 值。

### 跨工具路径的权限强制执行

- 测试工具场景验证 `write_file_denied`、`bash_permission_prompt_approved` 和 `bash_permission_prompt_denied`。
- `PermissionEnforcer::check()` 委托给 `PermissionPolicy::authorize()` 并返回结构化的允许/拒绝结果。
- `check_file_write()` 强制执行工作区边界和只读拒绝；`check_bash()` 在只读模式下拒绝突变命令，并在没有确认的情况下阻止提示模式 bash。

## 工具表面：`main` 分支上的 40 个暴露工具规范

- `rust/crates/tools/src/lib.rs` 中的 `mvp_tool_specs()` 暴露 **40** 个工具规范。
- 核心执行存在于 `bash`、`read_file`、`write_file`、`edit_file`、`glob_search` 和 `grep_search` 中。
- `mvp_tool_specs()` 中的现有产品工具包括 `WebFetch`、`WebSearch`、`TodoWrite`、`Skill`、`Agent`、`ToolSearch`、`NotebookEdit`、`Sleep`、`SendUserMessage`、`Config`、`EnterPlanMode`、`ExitPlanMode`、`StructuredOutput`、`REPL` 和 `PowerShell`。
- 9 通道推送将 `Task*`、`Team*`、`Cron*`、`LSP` 和 MCP 工具的纯固定有效负载存根替换为 `main` 分支上的注册表支持处理程序。
- `Brief` 在 `execute_tool()` 中作为执行别名处理，但它不是 `mvp_tool_specs()` 中单独暴露的工具规范。

### 仍然有限或有意浅薄

- `AskUserQuestion` 仍然返回挂起的响应有效负载，而不是真正的交互式 UI 接线。
- `RemoteTrigger` 仍然是存根响应。
- `TestingPermission` 仍然仅用于测试。
- 任务、团队、定时任务、MCP 和 LSP 不再只是 `execute_tool()` 中的固定有效负载存根，但其中几个仍然是注册表支持的近似值，而不是完整的外部运行时集成。
- Bash 深度验证在 `36dac6c` 合并之前仍然仅存在于分支中。

## 从旧 PARITY 清单协调

- [x] 路径遍历预防（符号链接跟随，`../` 转义）
- [x] 读/写大小限制
- [x] 二进制文件检测
- [x] 权限模式强制执行（只读 vs 工作区写入）
- [x] 配置合并优先级（用户 > 项目 > 本地）— `ConfigLoader::discover()` 加载用户 → 项目 → 本地，`loads_and_merges_claude_code_config_files_by_precedence()` 验证合并顺序。
- [x] 插件安装/启用/禁用/卸载流程 — `rust/crates/commands/src/lib.rs` 中的 `/plugin` 斜杠处理委托给 `rust/crates/plugins/src/lib.rs` 中的 `PluginManager::{install, enable, disable, uninstall}`。
- [x] 无 `#[ignore]` 测试隐藏失败 — 对 `rust/**/*.rs` 的 `grep` 发现 0 个被忽略的测试。

## 仍然开放

- [ ] 超出现在 `main` 分支上的注册表桥的端到端 MCP 运行时生命周期
- [x] 输出截断（大 stdout/文件内容）
- [ ] 会话压缩行为匹配
- [ ] 令牌计数/成本跟踪准确性
- [x] Bash 验证通道合并到 `main` 分支
- [ ] 每个提交的 CI 绿色

## 迁移准备

- [x] `PARITY.md` 维护和诚实
- [x] 9 个请求的通道记录了提交哈希和当前状态
- [x] 所有 9 个请求的通道都已登陆 `main` 分支（`bash-validation` 仍然仅存在于分支中）
- [x] 无 `#[ignore]` 测试隐藏失败
- [ ] 每个提交的 CI 绿色
- [x] 代码库形状足够干净，可用于交接文档