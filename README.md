# AI Code

## 项目分析

AI Code 是一个创新性的开源项目，展示了 AI 辅助开发的未来潜力。通过深入分析项目结构和代码，我们可以看到以下关键特点：

### 技术架构分析

- **双语言架构**：项目采用 Python 和 Rust 双语言实现，Python 提供灵活的开发体验和丰富的生态系统，Rust 则提供高性能的底层实现，两者互补形成强大的技术栈。这种设计充分利用了 Python 的快速开发能力和 Rust 的安全性与性能优势。

- **模块化设计**：项目采用高度模块化的架构，将功能划分为多个子系统，包括助手、引导、桥接、伙伴、CLI、组件等，每个子系统都有明确的职责和边界。这种设计使得代码结构清晰，易于维护和扩展。

- **移植策略**：项目正在从 TypeScript 系统移植到 Python，通过奇偶性审计确保功能对等，同时保留核心功能和架构设计。移植过程中注重保持功能的一致性和代码的质量。

- **工具链集成**：项目集成了丰富的工具链，包括命令管理、会话管理、远程模式等，提供了完整的开发和运行环境。这些工具相互协作，形成了一个强大的开发生态系统。

- **AI 驱动**：项目由 lobsters/claws 系统自主维护，通过并行编码会话、事件驱动的编排和机器可读的通道状态实现持续开发。这种 AI 驱动的开发模式展示了未来软件开发的新方向。

### 核心组件分析

- **命令系统**：通过 `commands.py` 和 `command_graph.py` 实现，支持丰富的命令行接口和命令执行。命令系统提供了统一的接口，方便用户与系统进行交互。

- **工具系统**：通过 `tools.py` 和 `tool_pool.py` 实现，集成了多种工具，支持不同的操作和功能。工具系统是项目的核心，提供了各种实用的功能模块。

- **运行时系统**：通过 `runtime.py` 和 `remote_runtime.py` 实现，提供了核心的运行时环境和远程操作能力。运行时系统负责管理系统的生命周期和资源分配。

- **会话系统**：通过 `session_store.py` 实现，支持会话的创建、保存和加载，提供持久化的用户体验。会话系统确保用户可以在不同的会话之间保持工作状态。

- **查询引擎**：通过 `query_engine.py` 实现，提供了强大的查询和分析能力。查询引擎帮助用户快速找到所需的信息和资源。

- **权限系统**：通过 `permissions.py` 实现，提供了细粒度的权限控制，确保系统的安全性。权限系统保护了系统资源和用户数据的安全。

- **成本跟踪系统**：通过 `costHook.py` 和 `cost_tracker.py` 实现，帮助用户了解资源使用情况和成本。成本跟踪系统使得用户可以更好地管理资源和控制成本。

### 项目价值分析

- **技术创新**：展示了如何通过 AI 辅助开发实现自主、公开、高速的软件构建。这种创新的开发模式为软件开发行业提供了新的思路和方法。

- **开源贡献**：提供了一个开源的编码框架，为其他项目提供参考和借鉴。开源模式促进了知识共享和社区协作。

- **学习资源**：作为一个双语言实现的项目，为开发者提供了学习 Python 和 Rust 的宝贵资源。项目的模块化设计和清晰的代码结构使得它成为一个理想的学习案例。

- **社区建设**：通过 UltraWorkers Discord 社区，促进了开发者之间的交流和合作。社区的存在使得项目能够不断改进和发展。

- **行业影响**：项目展示了 AI 在软件开发领域的潜力，可能会对未来的软件开发方式产生深远的影响。这种影响可能会延伸到其他领域，推动整个行业的发展。

## 项目介绍

### 项目概述

AI Code 是一个由 AI 自主维护的开源编码框架项目，旨在展示如何通过 AI 辅助开发，实现自主、公开、高速的软件构建。项目由 lobsters/claws 维护，采用 Python 和 Rust 双语言实现，正在从 TypeScript 系统移植到 Python。

项目的核心目标是创建一个完全由 AI 自主维护的开源编码框架，通过并行编码会话、事件驱动的编排和机器可读的通道状态，实现软件的持续开发和维护，展示 AI 在软件开发领域的潜力。

### 项目愿景

项目的愿景是打造一个革命性的软件开发平台，通过 AI 辅助开发，实现软件的自主构建和维护。具体来说，项目希望：

- 建立一个开放、透明的 AI 辅助开发生态系统
- 展示如何通过 AI 实现软件的持续开发和维护
- 为开发者提供一个强大、灵活的编码框架
- 推动 AI 在软件开发领域的应用和发展
- 促进开源社区的协作和知识共享

### 项目特点

- **AI 自主维护**：由 lobsters/claws 系统自主维护，通过并行编码会话、事件驱动的编排和机器可读的通道状态实现持续开发。系统能够自动处理代码审查、测试、部署等任务。

- **双语言实现**：同时提供 Python 和 Rust 实现，Python 为主，Rust 为高性能补充。这种设计充分利用了两种语言的优势，提供了既灵活又高效的解决方案。

- **开放透明**：完全开源，公开构建过程，展示 AI 辅助开发的潜力。项目的所有代码和开发过程都对公众开放，鼓励社区参与和贡献。

- **模块化设计**：采用高度模块化的架构，包含多个子系统和组件。每个模块都有明确的职责和边界，使得代码结构清晰，易于维护和扩展。

- **完整工具链**：提供丰富的命令行工具和功能，支持会话管理、远程模式等。工具链的完整性使得用户可以在一个统一的环境中完成各种任务。

- **扩展性强**：通过插件系统和技能注册表，支持功能的扩展和定制。用户可以根据自己的需求添加新的功能和工具。

- **安全性高**：通过权限系统和安全机制，确保系统的安全性。系统对所有操作进行权限检查，保护用户数据和系统资源。

- **成本可控**：通过成本跟踪系统，帮助用户了解资源使用情况和成本。用户可以根据成本情况调整资源使用，优化系统性能。

### 核心功能

- **移植管理**：从 TypeScript 系统移植到 Python，保持功能对等。移植过程中注重保持功能的一致性和代码的质量。

- **命令管理**：提供丰富的命令行接口，支持各种操作和查询。命令系统提供了统一的接口，方便用户与系统进行交互。

- **工具集成**：集成多种工具，支持不同的操作和功能。工具系统是项目的核心，提供了各种实用的功能模块。

- **会话管理**：支持会话的创建、保存和加载，提供持久化的用户体验。会话系统确保用户可以在不同的会话之间保持工作状态。

- **远程模式**：支持远程控制、SSH、teleport 等多种远程操作模式。远程模式使得用户可以在不同的环境中访问和控制系统。

- **审计功能**：提供奇偶性审计，确保移植的准确性。审计功能帮助用户验证系统的正确性和完整性。

- **成本跟踪**：通过 cost_tracker.py 实现成本跟踪，帮助用户了解资源使用情况。成本跟踪系统使得用户可以更好地管理资源和控制成本。

- **权限管理**：通过 permissions.py 实现权限管理，确保系统安全。权限系统保护了系统资源和用户数据的安全。

- **插件系统**：支持插件的加载和管理，扩展系统功能。插件系统使得用户可以根据自己的需求添加新的功能。

- **技能系统**：支持技能的注册和使用，提供更丰富的功能。技能系统为系统添加了更多的智能能力。

- **查询系统**：通过 query_engine.py 实现强大的查询和分析能力。查询系统帮助用户快速找到所需的信息和资源。

- **运行时管理**：通过 runtime.py 实现核心的运行时环境管理。运行时系统负责管理系统的生命周期和资源分配。

### 技术栈

- **主要语言**：Python、Rust
- **构建工具**：Cargo (Rust)、Python 标准库
- **依赖管理**：Cargo.toml (Rust)、Python 包管理
- **测试框架**：Python unittest
- **版本控制**：Git
- **AI 工具**：clawhip、oh-my-openagent、oh-my-claudecode、oh-my-codex
- **通信协议**：SSE (Server-Sent Events)
- **API 集成**：Anthropic API、OpenAI 兼容 API

### 应用场景

- **软件开发**：作为一个编码框架，用于开发各种软件项目
- **AI 辅助开发**：展示如何通过 AI 辅助实现软件的自主开发和维护
- **教育学习**：作为学习 Python 和 Rust 的教学资源
- **研究实验**：用于研究 AI 在软件开发领域的应用
- **开源贡献**：为开源社区提供一个有价值的项目

### 未来发展

- **功能完善**：继续完善系统功能，提高系统的稳定性和性能
- **生态扩展**：扩展系统的生态系统，增加更多的插件和技能
- **社区建设**：加强社区建设，鼓励更多的开发者参与和贡献
- **技术创新**：探索新的 AI 辅助开发技术和方法
- **行业合作**：与行业伙伴合作，推动 AI 在软件开发领域的应用

### 如何参与

- **贡献代码**：通过 GitHub 提交 Pull Request
- **报告问题**：在 GitHub 上提交 Issue
- **加入社区**：加入 UltraWorkers Discord 社区
- **提供反馈**：通过社区渠道提供反馈和建议
- **分享经验**：分享使用 AI Code 的经验和案例

## 仓库结构

```text
.
├── src/                                # Python 移植工作区
│   ├── __init__.py
│   ├── assistant/                       # 助手子系统
│   ├── bootstrap/                       # 引导子系统
│   ├── bridge/                          # 桥接子系统
│   ├── buddy/                           # 伙伴子系统
│   ├── cli/                             # CLI 子系统
│   ├── components/                      # 组件子系统
│   ├── constants/                       # 常量子系统
│   ├── coordinator/                     # 协调器子系统
│   ├── entrypoints/                     # 入口点子系统
│   ├── hooks/                           # 钩子子系统
│   ├── keybindings/                     # 键绑定子系统
│   ├── memdir/                          # 内存目录子系统
│   ├── migrations/                      # 迁移子系统
│   ├── moreright/                       # Moreright 子系统
│   ├── native_ts/                       # 原生 TS 子系统
│   ├── outputStyles/                    # 输出样式子系统
│   ├── plugins/                         # 插件子系统
│   ├── reference_data/                  # 参考数据
│   ├── remote/                          # 远程子系统
│   ├── schemas/                         # 模式子系统
│   ├── screens/                         # 屏幕子系统
│   ├── server/                          # 服务器子系统
│   ├── services/                        # 服务子系统
│   ├── skills/                          # 技能子系统
│   ├── state/                           # 状态子系统
│   ├── types/                           # 类型子系统
│   ├── upstreamproxy/                   # 上游代理子系统
│   ├── utils/                           # 工具子系统
│   ├── vim/                             # Vim 子系统
│   ├── voice/                           # 语音子系统
│   ├── QueryEngine.py                   # 查询引擎
│   ├── Tool.py                          # 工具定义
│   ├── bootstrap_graph.py               # 引导图
│   ├── command_graph.py                 # 命令图
│   ├── commands.py                      # 命令
│   ├── context.py                       # 上下文
│   ├── costHook.py                      # 成本钩子
│   ├── cost_tracker.py                  # 成本跟踪器
│   ├── deferred_init.py                 # 延迟初始化
│   ├── dialogLaunchers.py               # 对话启动器
│   ├── direct_modes.py                  # 直接模式
│   ├── execution_registry.py            # 执行注册表
│   ├── history.py                       # 历史记录
│   ├── ink.py                           # Ink
│   ├── interactiveHelpers.py            # 交互助手
│   ├── main.py                          # 主入口点
│   ├── models.py                        # 模型
│   ├── parity_audit.py                  # 奇偶性审计
│   ├── permissions.py                   # 权限
│   ├── port_manifest.py                 # 移植清单
│   ├── prefetch.py                      # 预取
│   ├── projectOnboardingState.py        # 项目入职状态
│   ├── query.py                         # 查询
│   ├── query_engine.py                  # 查询引擎
│   ├── remote_runtime.py                # 远程运行时
│   ├── replLauncher.py                  # REPL 启动器
│   ├── runtime.py                       # 运行时
│   ├── session_store.py                 # 会话存储
│   ├── setup.py                         # 设置
│   ├── system_init.py                   # 系统初始化
│   ├── task.py                          # 任务
│   ├── tasks.py                         # 任务
│   ├── tool_pool.py                     # 工具池
│   ├── tools.py                         # 工具
│   └── transcript.py                    # 转录
├── tests/                              # Python 验证
├── rust/                                # Rust 实现
│   ├── crates/                          # Rust crates
│   ├── scripts/                         # Rust 脚本
│   └── README.md                        # Rust README
├── assets/                              # 资产
│   ├── omx/                             # OmX 工作流截图
│   └── clawd-hero.jpeg                  # 英雄图像
├── 2026-03-09-is-legal-the-same-as-legitimate-ai-reimplementation-and-the-erosion-of-copyleft.md
├── CLAUDE.md                            # CLAUDE.md
├── PARITY.md                            # 奇偶性文档
├── PHILOSOPHY.md                        # 理念
├── README.md                            # 本 README
├── ROADMAP.md                           # 路线图
└── USAGE.md                             # 使用指南
```

## 快速开始

### 渲染 Python 移植摘要

```bash
python3 -m src.main summary
```

### 打印当前 Python 工作区清单

```bash
python3 -m src.main manifest
```

### 列出当前 Python 模块

```bash
python3 -m src.main subsystems --limit 16
```

### 运行验证

```bash
python3 -m unittest discover -s tests -v
```

### 运行奇偶性审计

```bash
python3 -m src.main parity-audit
```

### 检查命令和工具清单

```bash
python3 -m src.main commands --limit 10
python3 -m src.main tools --limit 10
```

## 项目背景

Project Claw Code 由 Bellman / Yeachan Heo 和像 Yeongyu 这样的朋友发起，但仓库本身是由自主的 claw 工作流推动的。项目的存在是为了证明一个开放的编码框架可以自主、公开、高速地构建 — 由人类设定方向，由 AI 完成具体工作。

项目使用了多种工具和技术，包括 clawhip、oh-my-openagent、oh-my-claudecode 和 oh-my-codex 等，通过 AI 辅助的方式实现持续开发和维护。

## 移植状态

主要源代码树现在以 Python 为主。`src/` 包含活跃的 Python 移植工作区，`tests/` 验证当前的 Python 工作区，公开的快照不再是跟踪的仓库状态的一部分。

当前的 Python 工作区还不是原始系统的完整一对一替代品，但主要的实现表面现在是 Python。

## 社区

加入 UltraWorkers Discord 社区，与其他开发者交流关于 LLMs、框架工程、代理工作流和自主软件开发的话题：

[![Discord](https://img.shields.io/badge/Join%20Discord-UltraWorkers-5865F2?logo=discord&style=for-the-b