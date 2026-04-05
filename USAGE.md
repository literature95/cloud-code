# AI Code 使用指南

本指南涵盖了 `rust/` 目录下的当前 Rust 工作区和 `claw` CLI 二进制文件。

## 前提条件

- 带有 `cargo` 的 Rust 工具链
- 以下之一：
  - 用于直接 API 访问的 `ANTHROPIC_API_KEY`
  - 用于基于 OAuth 认证的 `claw login`
- 可选：当目标为代理或本地服务时使用 `ANTHROPIC_BASE_URL`

## 构建工作区

```bash
cd rust
cargo build --workspace
```

调试构建后，CLI 二进制文件位于 `rust/target/debug/claw`。

## 快速开始

### 交互式 REPL

```bash
cd rust
./target/debug/claw
```

### 一次性提示

```bash
cd rust
./target/debug/claw prompt "总结此仓库"
```

### 简写提示模式

```bash
cd rust
./target/debug/claw "解释 rust/crates/runtime/src/lib.rs"
```

### 用于脚本的 JSON 输出

```bash
cd rust
./target/debug/claw --output-format json prompt "status"
```

## 模型和权限控制

```bash
cd rust
./target/debug/claw --model sonnet prompt "审查此差异"
./target/debug/claw --permission-mode read-only prompt "总结 Cargo.toml"
./target/debug/claw --permission-mode workspace-write prompt "更新 README.md"
./target/debug/claw --allowedTools read,glob "检查 runtime crate"
```

支持的权限模式：

- `read-only`（只读）
- `workspace-write`（工作区写入）
- `danger-full-access`（危险的完全访问）

CLI 当前支持的模型别名：

- `opus` → `claude-opus-4-6`
- `sonnet` → `claude-sonnet-4-6`
- `haiku` → `claude-haiku-4-5-20251213`

## 认证

### API 密钥

```bash
export ANTHROPIC_API_KEY="sk-ant-..."
```

### OAuth

```bash
cd rust
./target/debug/claw login
./target/debug/claw logout
```

## 常见操作命令

```bash
cd rust
./target/debug/claw status
./target/debug/claw sandbox
./target/debug/claw agents
./target/debug/claw mcp
./target/debug/claw skills
./target/debug/claw system-prompt --cwd .. --date 2026-04-04
```

## 会话管理

REPL 回合会持久化在当前工作区的 `.claw/sessions/` 目录下。

```bash
cd rust
./target/debug/claw --resume latest
./target/debug/claw --resume latest /status /diff
```

有用的交互式命令包括 `/help`、`/status`、`/cost`、`/config`、`/session`、`/model`、`/permissions` 和 `/export`。

## 配置文件解析顺序

运行时配置按以下顺序加载，后面的条目会覆盖前面的条目：

1. `~/.claw.json`
2. `~/.config/claw/settings.json`
3. `<repo>/.claw.json`
4. `<repo>/.claw/settings.json`
5. `<repo>/.claw/settings.local.json`

## Mock 一致性测试工具

工作区包含一个确定性的 Anthropic 兼容的 mock 服务和一致性测试工具。

```bash
cd rust
./scripts/run_mock_parity_harness.sh
```

手动启动 mock 服务：

```bash
cd rust
cargo run -p mock-anthropic-service -- --bind 127.0.0.1:0
```

## 验证

```bash
cd rust
cargo test --workspace
```

## 工作区概览

当前 Rust crates：

- `api`
- `commands`
- `compat-harness`
- `mock-anthropic-service`
- `plugins`
- `runtime`
- `rusty-claude-cli`
- `telemetry`
- `tools`

