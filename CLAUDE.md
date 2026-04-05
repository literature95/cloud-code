# CLAUDE.md

本文件为 Claude Code (claude.ai/code) 提供在本仓库中工作时的指导。

## 检测到的技术栈

- 语言：Rust。
- 框架：未从支持的启动标记中检测到。

## 验证

- 从 `rust/` 目录运行 Rust 验证：`cargo fmt`、`cargo clippy --workspace --all-targets -- -D warnings`、`cargo test --workspace`
- `src/` 和 `tests/` 目录均存在；当行为变更时，同时更新这两个表面。

## 仓库结构

- `rust/` 包含 Rust 工作区和活跃的 CLI/运行时实现。
- `src/` 包含应与生成的指导和测试保持一致的源文件。
- `tests/` 包含应与代码变更一起审查的验证表面。

## 工作协议

- 优先选择小而可审查的变更，并保持生成的引导文件与实际仓库工作流一致。
- 将共享默认值保存在 `.claude.json` 中；将 `.claude/settings.local.json` 保留给机器本地覆盖。
- 不要自动覆盖现有的 `CLAUDE.md` 内容；当仓库工作流变更时，有意更新它。

