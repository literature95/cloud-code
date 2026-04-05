# 重写 Project Claw Code

## 项目介绍

Project Claw Code 是一个由 AI 自主维护的开源编码框架项目，旨在展示如何通过 AI 辅助开发，实现自主、公开、高速的软件构建。项目由 lobsters/claws 维护，采用 Python 和 Rust 双语言实现，正在从 TypeScript 系统移植到 Python。

### 项目特点

- **AI 自主维护**：由 lobsters/claws 系统自主维护，通过并行编码会话、事件驱动的编排和机器可读的通道状态实现持续开发
- **双语言实现**：同时提供 Python 和 Rust 实现，Python 为主，Rust 为高性能补充
- **开放透明**：完全开源，公开构建过程，展示 AI 辅助开发的潜力
- **模块化设计**：采用高度模块化的架构，包含多个子系统和组件
- **完整工具链**：提供丰富的命令行工具和功能，支持会话管理、远程模式等

### 核心功能

- **移植管理**：从 TypeScript 系统移植到 Python，保持功能对等
- **命令管理**：提供丰富的命令行接口，支持各种操作和查询
- **工具集成**：集成多种工具，支持不同的操作和功能
- **会话管理**：支持会话的创建、保存和加载
- **远程模式**：支持远程控制、SSH、 teleport 等多种远程操作模式
- **审计功能**：提供奇偶性审计，确保移植的准确性

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

##

<br />

<br />

