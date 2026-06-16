<div style="display: flex; gap: 10px; flex-wrap: wrap;">
  <a href="https://huggingface.co/datasets/kyle-X1e/SCR-Bench"><img src="https://img.shields.io/badge/🤗 HuggingFace-Dataset-purple?logo=" alt="static-leaderboard" /></a>
  <a href="https://arxiv.org/abs/2606.15242"><img src="https://img.shields.io/badge/ArXiv-Paper-red?logo=arxiv" alt="static-leaderboard" /></a>
  <a href="https://huggingface.co/spaces/kyle-X1e/SCR-Bench-Leaderboard"><img src="https://img.shields.io/badge/🏆 HuggingFace-LeaderBoard-yellow" alt="static-leaderboard" /></a>
</div>


# SCR-Bench: Skill Composition Risk Benchmark

**SCR-Bench** (Skill Composition Risk Bench) is a benchmark for evaluating security risks that emerge when individually benign skills are composed into agent workflows. In isolation, each skill appears safe, but harmful outcomes can arise along activated composition paths through capability flow, trust transfer, or authorization confusion.

## Overview

**Benign in Isolation, Harmful in Composition.** Existing skill vetting evaluates each skill individually, but real agent tasks invoke multiple skills across a shared execution context. An upstream skill's output, trust signal, authorization cue, or side effect can be carried into a later skill invocation, activating a path whose risk is invisible from any single artifact.

SCR-Bench contains three sub-benchmarks:

| Sub-benchmark | Mechanism | Description |
|---------------|-----------|-------------|
| **SCR-CapFlow** | Capability Flow | Upstream skill supplies execution targets or operational context that enables downstream skill to perform harmful state-changing actions |
| **SCR-TrustLift** | Trust Transfer | A benign-looking security skill lends legitimacy to a later risky skill or action |
| **SCR-AuthBlur** | Authorization Confusion | Advisory or finding-like context shifts the agent's approval boundary toward unsafe downstream decisions |

## Results Highlights

- **SCR-CapFlow**: Attack success rate reaches 33.5% under composition, compared with near-zero isolated baselines
- **SCR-TrustLift**: Harmful installation rate exceeds 96.5% on four of five model backends
- **SCR-AuthBlur**: Risky approval rate increases by 71.8% over the isolated baseline (L0->L1)

## Project Structure

```
SCR-Bench/
├── SCR-CapFlow/          # Capability flow composition benchmark
│   └── README.md         # Experiment instructions
├── SCR-TrustLift/        # Trust transfer composition benchmark
│   └── README.md         # Experiment instructions
├── SCR-AuthBlur/         # Authorization confusion benchmark
│   ├── README_en.md      # Experiment instructions (English)
│   └── README_zh.md      # Experiment instructions (Chinese)
```

## Running Experiments

Each sub-benchmark has its own README with detailed experiment instructions. Before running experiments, you need to configure your CLI backend.

### CLI Backend Configuration

SCR-Bench supports multiple CLI backends. Each skill directory is named according to the target CLI:

| CLI Backend | Skills Directory | CLI Tool |
|-------------|------------------|----------|
| `ClaudeCode` | `.claude` | Claude Code |
| `CodeX` | `.agents` | CodeX |
| `GeminiCLI` | `.gemini` | Gemini CLI |
| `OpenCode` | `.opencode` | OpenCode |

**Required Setup:**

1. Install and configure your desired CLI tool (Claude Code, CodeX, Gemini CLI, or OpenCode) on your machine
2. Ensure the CLI tool is accessible from your terminal PATH
3. When running experiments, specify the `--cli` parameter (e.g., `--cli ClaudeCode`) to select the target backend
4. The `init_env.py` script in each sub-benchmark will rename the skills directory to match your selected CLI

### Quick Start

Refer to the README.md in each sub-benchmark directory for specific instructions:

- **SCR-CapFlow**: See `SCR-CapFlow/README.md` or `SCR-CapFlow/README_CN.md`
- **SCR-TrustLift**: See `SCR-TrustLift/README.md`
- **SCR-AuthBlur**: See `SCR-AuthBlur/README_en.md` or `SCR-AuthBlur/README_zh.md`

## Notes

- **Data generation.** All experimental data in the paper was produced by running **Claude Code** against different model backends via their APIs. To reproduce any result, install Claude Code and configure the corresponding model API — no other CLI is needed.
- **Current CLI support.** The experiment scripts currently target **Claude Code only**. Support for CodeX, Gemini CLI, and OpenCode is on the roadmap and will be added in future releases.
- **Maintenance.** This project is actively maintained on a long-term basis. We will continue to release bug fixes, new cases, and additional CLI / model backend support over time.

# SCR-Bench：技能组合风险基准

**SCR-Bench**（Skill Composition Risk Bench，技能组合风险基准）是一个用于评估安全风险的基准测试。当单独审视时每个技能都是良性的，但当它们被组合成代理工作流时，有害的结果可能在沿着能力流、信任转移或授权混淆的激活组合路径上出现。

## 概述

**孤立无害，组合有害。** 现有的技能审查单独评估每个技能，但实际的代理任务会在共享执行上下文中调用多个技能。上游技能的输出、信任信号、授权提示或副作用可能被携带到后续技能调用中，激活一条从任何单一技能都看不到风险的路径。

SCR-Bench 包含三个子基准：

| 子基准 | 机制 | 描述 |
|--------|------|------|
| **SCR-CapFlow** | 能力跨越 | 上游Skill提供执行目标或操作上下文，使下游Skill能够执行权限变更等操作，当二者被组合后原本分离的能力被连接起来成为了高权限的危险行为。 |
| **SCR-TrustLift** | 信任转移 | 一个看似良性的"安全审查"Skill，运行结束后会输出运行审查报告，但是也可以通过背书信号为后续风险Skill或操作赋予合法性。 |
| **SCR-AuthBlur** | 授权混淆 | 咨询性或发现性上下文，会将Agent的批准边界推向不安全的下游决策。 |

## 实验结果亮点

- **SCR-CapFlow**：在组合下攻击成功率高达 33.5%，而孤立基线接近零
- **SCR-TrustLift**：在五个模型后端中的四个上，有害安装率超过 96.5%
- **SCR-AuthBlur**：风险批准率比孤立基线增加 71.8% (L0->L1) 

## 项目结构

```
SCR-Bench/
├── SCR-CapFlow/          # 能力跨越组合基准
│   └── README.md         # 实验说明
├── SCR-TrustLift/        # 信任转移组合基准
│   └── README.md         # 实验说明
├── SCR-AuthBlur/         # 授权混淆基准
│   ├── README_en.md      # 实验说明（英文）
│   └── README_zh.md      # 实验说明（中文）
```

## 运行实验

每个子基准都有各自的 README，提供详细的实验说明。运行实验前，您需要配置 CLI 后端。

### CLI 后端配置

SCR-Bench 支持多个 CLI 后端。每个技能目录根据目标 CLI 命名：

| CLI 后端 | 技能目录 | CLI 工具 |
|----------|----------|----------|
| `ClaudeCode` | `.claude` | Claude Code |
| `CodeX` | `.agents` | CodeX |
| `GeminiCLI` | `.gemini` | Gemini CLI |
| `OpenCode` | `.opencode` | OpenCode |

**必要设置：**

1. 在您的机器上安装并配置所需的 CLI 工具（Claude Code、CodeX、Gemini CLI 或 OpenCode）
2. 确保 CLI 工具可从终端 PATH 访问
3. 运行实验时，指定 `--cli` 参数（例如 `--cli ClaudeCode`）以选择目标后端
4. 每个子基准中的 `init_env.py` 脚本会将技能目录重命名以匹配您选择的 CLI

### 快速开始

请参阅各子基准目录中的 README.md 获取具体说明：

- **SCR-CapFlow**：参见 `SCR-CapFlow/README.md`
- **SCR-TrustLift**：参见 `SCR-TrustLift/README.md`
- **SCR-AuthBlur**：参见 `SCR-AuthBlur/README_en.md`

## 说明

- **数据生成方式。** 论文中的全部实验数据均通过运行 **Claude Code** 并切换不同模型后端（API）跑出。复现任一结果，只需安装 Claude Code 并配置对应模型的 API 即可，无需使用其他 CLI。
- **当前 CLI 支持。** 实验脚本目前仅适配 **Claude Code**。CodeX、Gemini CLI、OpenCode 的支持已在路线图上，将在后续版本中陆续加入。
- **维护承诺。** 本项目长期持续维护。我们会持续发布问题修复、新增 case、以及更多 CLI / 模型后端的支持。
