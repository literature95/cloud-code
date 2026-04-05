# 重写 Project Claw Code

<p align="center">
  <strong>⭐ 历史上最快突破 50K 星标的仓库，发布后仅 2 小时就达到了这一里程碑 ⭐</strong>
</p>

<p align="center">
  <a href="https://star-history.com/#ultraworkers/claw-code&Date">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=ultraworkers/claw-code&type=Date&theme=dark" />
      <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=ultraworkers/claw-code&type=Date" />
      <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=ultraworkers/claw-code&type=Date" width="600" />
    </picture>
  </a>
</p>

<p align="center">
  <img src="assets/clawd-hero.jpeg" alt="Claw" width="300" />
</p>

<p align="center">
  <strong>由 lobsters/claws 自主维护 — 非人工维护</strong>
</p>

<p align="center">
  <a href="https://github.com/Yeachan-Heo/clawhip">clawhip</a> ·
  <a href="https://github.com/code-yeongyu/oh-my-openagent">oh-my-openagent</a> ·
  <a href="https://github.com/Yeachan-Heo/oh-my-claudecode">oh-my-claudecode</a> ·
  <a href="https://github.com/Yeachan-Heo/oh-my-codex">oh-my-codex</a> ·
  <a href="https://discord.gg/6ztZB9jvWq">UltraWorkers Discord</a>
</p>

> [!IMPORTANT]
> 活跃的 Rust 工作区现在位于 [`rust/`](./rust) 目录。请先查看 [`USAGE.md`](./USAGE.md) 了解构建、认证、CLI、会话和奇偶性测试工作流，然后查看 [`rust/README.md`](./rust/README.md) 获取 crate 级别的详细信息。

> 想了解这个仓库背后的更大理念？请阅读 [`PHILOSOPHY.md`](./PHILOSOPHY.md) 和 Sigrid Jin 的公开解释：https://x.com/realsigridjin/status/2039472968624185713

> 鸣谢为这个仓库提供支持的 UltraWorkers 生态系统：[clawhip](https://github.com/Yeachan-Heo/clawhip)、[oh-my-openagent](https://github.com/code-yeongyu/oh-my-openagent)、[oh-my-claudecode](https://github.com/Yeachan-Heo/oh-my-claudecode)、[oh-my-codex](https://github.com/Yeachan-Heo/oh-my-codex) 和 [UltraWorkers Discord](https://discord.gg/6ztZB9jvWq)。

---

## 项目背景

这个仓库由 **lobsters/claws** 维护，而不是由传统的纯人工开发团队维护。

系统背后的人员包括 [Bellman / Yeachan Heo](https://github.com/Yeachan-Heo) 和像 [Yeongyu](https://github.com/code-yeongyu) 这样的朋友，但仓库本身是由自主的 claw 工作流推动的：并行编码会话、事件驱动的编排、恢复循环和机器可读的通道状态。

实际上，这意味着这个项目不仅仅是 *关于* 编码代理 — 它正在 **由它们积极构建**。功能、测试、遥测、文档和工作流加固都是通过 claw 驱动的循环实现的，使用 [clawhip](https://github.com/Yeachan-Heo/clawhip)、[oh-my-openagent](https://github.com/code-yeongyu/oh-my-openagent)、[oh-my-claudecode](https://github.com/Yeachan-Heo/oh-my-claudecode) 和 [oh-my-codex](https://github.com/Yeachan-Heo/oh-my-codex)。

这个仓库的存在是为了证明一个开放的编码框架可以 **自主、公开、高速** 地构建 — 由人类设定方向，由 claws 完成具体工作。

查看公开的构建故事：

https://x.com/realsigridjin/status/2039472968624185713

![Tweet screenshot](assets/tweet-screenshot.png)

---

## 移植状态

主要源代码树现在以 Python 为主。

- `src/` 包含活跃的 Python 移植工作区
- `tests/` 验证当前的 Python 工作区
- 公开的快照不再是跟踪的仓库状态的一部分

当前的 Python 工作区还不是原始系统的完整一对一替代品，但主要的实现表面现在是 Python。

## 为什么进行这次重写

我最初研究公开的代码库是为了了解它的框架、工具连接和代理工作流。在花更多时间研究法律和道德问题后 — 以及阅读下面链接的文章后 — 我不希望公开的快照本身仍然是主要的跟踪源代码树。

现在这个仓库专注于 Python 移植工作。

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

## Python 工作区概览

新的 Python `src/` 树目前提供：

- **`port_manifest.py`** — 总结当前 Python 工作区结构
- **`models.py`** — 子系统、模块和积压状态的数据类
- **`commands.py`** — Python 端命令移植元数据
- **`tools.py`** — Python 端工具移植元数据
- **`query_engine.py`** — 从活跃工作区渲染 Python 移植摘要
- **`main.py`** — 清单和摘要输出的 CLI 入口点

## 快速开始

渲染 Python 移植摘要：

```bash
python3 -m src.main summary
```

打印当前 Python 工作区清单：

```bash
python3 -m src.main manifest
```

列出当前 Python 模块：

```bash
python3 -m src.main subsystems --limit 16
```

运行验证：

```bash
python3 -m unittest discover -s tests -v
```

针对本地忽略的归档运行奇偶性审计（当存在时）：

```bash
python3 -m src.main parity-audit
```

检查镜像的命令/工具清单：

```bash
python3 -m src.main commands --limit 10
python3 -m src.main tools --limit 10
```

## 当前奇偶性检查点

移植现在更紧密地镜像了归档的根条目文件表面、顶级子系统名称和命令/工具清单。然而，它 **尚未** 成为原始 TypeScript 系统的完整运行时等效替代品；Python 树仍然包含比归档源更少的可执行运行时切片。


## 使用 `oh-my-codex` 构建

这个仓库的重组和文档工作是由 Yeachan Heo 的 [oh-my-codex (OmX)](https://github.com/Yeachan-Heo/oh-my-codex) 在 Codex 之上编排的 AI 辅助工作。

- **`$team` 模式：** 用于协调并行审查和架构反馈
- **`$ralph` 模式：** 用于持久执行、验证和完成纪律
- **Codex 驱动的工作流：** 用于将主要 `src/` 树转变为 Python 优先的移植工作区

### OmX 工作流截图

![OmX workflow screenshot 1](assets/omx/omx-readme-review-1.png)

*在终端窗格中审查 README 和文章上下文时的 Ralph/团队编排视图。*

![OmX workflow screenshot 2](assets/omx/omx-readme-review-2.png)

*在最终 README 措辞过程中的分窗格审查和验证流程。*

## 社区

<p align="center">
  <a href="https://discord.gg/6ztZB9jvWq"><img src="https://img.shields.io/badge/UltraWorkers-Discord-5865F2?logo=discord&style=for-the-badge" alt="UltraWorkers Discord" /></a>
</p>

加入 [**UltraWorkers Discord**](https://discord.gg/6ztZB9jvWq) — clawhip、oh-my-openagent、oh-my-claudecode、oh-my-codex 和 claw-code 的社区。来聊聊 LLMs、框架工程、代理工作流和自主软件开发。

[![Discord](https://img.shields.io/badge/Join%20Discord-UltraWorkers-5865F2?logo=discord&style=for-the-badge)](https://discord.gg/6ztZB9jvWq)

## 星标历史

请查看本 README 顶部的图表。

## 所有权/关联免责声明

- 本仓库 **不** 声称拥有原始 Claude Code 源材料的所有权。
- 本仓库 **不** 与 Anthropic 相关联、不被其认可、也不由其维护。
