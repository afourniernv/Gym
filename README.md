# NeMo Gym

[![PyPI](https://img.shields.io/pypi/v/nemo-gym)](https://pypi.org/project/nemo-gym/)
[![Python](https://img.shields.io/pypi/pyversions/nemo-gym)](https://pypi.org/project/nemo-gym/)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![CI](https://github.com/NVIDIA-NeMo/Gym/actions/workflows/unit-tests.yml/badge.svg)](https://github.com/NVIDIA-NeMo/Gym/actions/workflows/unit-tests.yml)
[![Docs](https://img.shields.io/badge/docs-NVIDIA-brightgreen)](https://docs.nvidia.com/nemo/gym/main/about/)

**[Requirements](#-requirements)** • **[Quick Start](#-quick-start)** • **[Environment Tutorials](#-environment-tutorials)** • **[Available Environments](#-available-environments)** • **[Documentation & Resources](#-documentation--resources)** • **[Community & Support](#-community--support)** • **[Citations](#-citations)**

NeMo Gym is a library for evaluating and improving models and agents using environments. NeMo Gym provides infrastructure to develop environments, scalably run evaluation and training, and a collection of popular benchmarks and training environments.

An environment is the complete system an agent interacts with to complete a task. It consists of a dataset (tasks to solve), an agent harness (how the model interacts with the world), a verifier (task completion scoring), and state (per-task execution context).

## 🎯 When to Use NeMo Gym

- You need to **evaluate models or agents** in stateful environments (e.g. code execution, tool calling, sandboxes)
- You want **reproducible evaluation** across teams using shared environments and verifiers
- You need to use environments **at scale** — multiple repeats per task, or thousands of concurrent requests for training
- You want to **seamlessly transition** between evaluation, agent optimization, and training

If you're scoring model outputs with a stateless check and don't need scale or training, a script is probably sufficient.

## 🏆 What NeMo Gym Provides

- Modular, extensible interfaces for agents, environments, tasks, and verifiers
- Environment hub of popular benchmarks and training environments
- Use your own agents or choose from built-in harnesses
- Scale to thousands of concurrent environments
- Train with the RL framework of your choice
- Battle-tested in production Nemotron training

![NeMo Gym Product Overview](fern/assets/images/product_overview.png)

## 🌎 Ecosystem

NeMo Gym is a component of [NVIDIA NeMo](https://docs.nvidia.com/nemo/gym/main/about/ecosystem#related-nemo-libraries), a GPU-accelerated platform for training generative AI models and optimizing AI agents. NeMo Gym is integrated with the broader agentic ecosystem - see the [Ecosystem](https://docs.nvidia.com/nemo/gym/main/about/ecosystem) page for more details.

**Environment Libraries:** Seamlessly combine environments and benchmarks from other libraries alongside NeMo Gym environments. Examples:
[Aviary](https://github.com/NVIDIA-NeMo/Gym/tree/main/resources_servers/aviary) • [Harbor](https://github.com/NVIDIA-NeMo/Gym/tree/main/responses_api_agents/harbor_agent) • [OpenEnv](https://github.com/NVIDIA-NeMo/Gym/tree/main/resources_servers/openenv) • [Reasoning Gym](https://github.com/NVIDIA-NeMo/Gym/tree/main/resources_servers/reasoning_gym) • [Verifiers](https://github.com/NVIDIA-NeMo/Gym/tree/main/responses_api_agents/verifiers_agent)

**Training Framework Libraries:** Use environments for SFT and RL training.
[NeMo RL](https://docs.nvidia.com/nemo/gym/tutorials/training-tutorials/nemo-rl-grpo) • [Unsloth](https://docs.nvidia.com/nemo/gym/tutorials/training-tutorials/unsloth) • [VeRL](https://docs.nvidia.com/nemo/gym/tutorials/training-tutorials)

**Agent Harnesses:** Agent harnesses for evaluation and training available out of the box. Examples:
[OpenHands](https://github.com/NVIDIA-NeMo/Gym/tree/main/responses_api_agents/swe_agents) • [Mini SWE Agent](https://github.com/NVIDIA-NeMo/Gym/tree/main/responses_api_agents/mini_swe_agent) • [LangGraph](https://github.com/NVIDIA-NeMo/Gym/tree/main/responses_api_agents/langgraph_agent)

> [!IMPORTANT]
> NeMo Gym is currently in early development. You should expect evolving APIs, incomplete documentation, and occasional bugs. We welcome contributions and feedback - for any changes, please open an issue first to kick off discussion!

## 📣 News

* **[08/06/2026]** [Release v0.5.0](https://github.com/NVIDIA-NeMo/Gym/releases#release-v0.5.0):
  Highlights:
  - Seven sandbox providers: Docker, Daytona, ECS Fargate, Enroot, and OpenShell join OpenSandbox and Apptainer; large-scale OpenSandbox reliability significantly improved
  - Four new agent harnesses: Codex CLI, KiloCode, RemoteAgent, and anyswe_agent
  - Recompute rewards from stored rollouts without re-running inference with `gym eval reverify`
  - Rollout observability joined end-to-end: model-call capture, agent observations, and a standardized `ng_trajectory` schema
  - 21 new environments across six domains: Agentic, Knowledge and instruction following, Long context, Science and coding, Translation and multilingual, and Reasoning

<details>
<summary>Previous News</summary>

* **[07/01/2026]** [Release v0.4.0](https://github.com/NVIDIA-NeMo/Gym/releases/tag/v0.4.0): Unified `gym` CLI, BLADE diagnostics, agent skill evaluation, pluggable sandboxes, more agent harnesses (OpenCode, OpenClaw, Pi), hosted inference providers, and new benchmarks.

* **[06/04/2026]** [Release v0.3.0](https://github.com/NVIDIA-NeMo/Gym/releases/tag/v0.3.0): 70+ new environments, Nemotron 3 Ultra training datasets, VeRL integration, and out-of-the-box harnesses including Claude Code and Hermes.

</details>

## 📋 Requirements

NeMo Gym is designed to run on standard development machines:

| Hardware Requirements | Software Requirements |
| --------------------- | --------------------- |
| **GPU**: Not required for NeMo Gym library operation<br>• GPU may be needed for specific resources servers or model inference (see individual server documentation) | **Operating System**:<br>• Linux (Ubuntu 20.04+, or equivalent)<br>• macOS (11.0+ for x86_64, 12.0+ for Apple Silicon)<br>• Windows (via WSL2) |
| **CPU**: Any modern x86_64 or ARM64 processor (e.g., Intel, AMD, Apple Silicon) | **Python**: 3.13.14 or higher |
| **RAM**: Minimum 8 GB (16 GB+ recommended for larger environments) | **Git**: For cloning the repository |
| **Storage**: Minimum 5 GB free disk space for installation and basic usage | **Internet Connection**: Required for downloading dependencies and API access |

**Additional Requirements**

- **API Keys**: OpenAI API key with available credits (for the quickstart examples)
  - Other model providers supported (Azure OpenAI, self-hosted models via vLLM)
- **Ray**: Automatically installed as a dependency (no separate setup required)

## 🚀 Quick Start

Requires Python 3.13.14+ on x86_64 or ARM64 (Linux, macOS, Windows via WSL2). No GPU required. See the [Getting Started](https://docs.nvidia.com/nemo/gym/main/get-started) docs for a more comprehensive walkthrough.

**Install NeMo Gym:**

Requires [uv](https://docs.astral.sh/uv/getting-started/installation/) and Python 3.13.14+.

```bash
git clone git@github.com:NVIDIA-NeMo/Gym.git
cd Gym
uv venv --python 3.13.14 && source .venv/bin/activate
uv sync
```

**Configure your model:**

This quickstart uses OpenAI. NeMo Gym supports local and hosted inference — see [Configure Model](https://docs.nvidia.com/nemo/gym/main/model-server) for vLLM, Fireworks, OpenRouter, and others.

Create `env.yaml` in the project root:
```yaml
policy_base_url: https://api.openai.com/v1
policy_api_key: <your-openai-api-key>
policy_model_name: gpt-4.1-2025-04-14
```

### Run Evaluation

Run your agent on a set of tasks and score the results. This example uses a simple tool calling agent [`simple_agent`](responses_api_agents/simple_agent/README.md) with the [`mcqa`](resources_servers/mcqa/README.md) (multiple-choice Q&A) environment and its included example data.

**1. Start servers**

NeMo Gym uses local servers to coordinate your model, agent, and task verification. Start them first:

```bash
gym env start \
    --resources-server mcqa \
    --model-type openai_model
```

You should see three server instances starting:

```text
[1] mcqa (resources_servers/mcqa)
[2] mcqa_simple_agent (responses_api_agents/simple_agent)
[3] policy_model (responses_api_models/openai_model)
```

**2. Evaluate your agent**

In a new terminal, run your agent on a single task to verify everything works:

```bash
source .venv/bin/activate

gym eval run --no-serve \
    --agent mcqa_simple_agent \
    --input resources_servers/mcqa/data/example.jsonl \
    --output results/mcqa_rollouts.jsonl \
    --limit 5 \
    --num-repeats 1
```

You should see a progress bar followed by aggregate metrics:

```text
Collecting rollouts: 100%|██████| 5/5 [01:22<00:00, 16.44s/it]

Key metrics for mcqa_simple_agent:
{
    "mean/reward": 0.8,
    "pass@1[avg-of-1]/accuracy": 80.0,
    "pass@1/accuracy": 80.0
}
Finished rollout collection! View results at:
Fully materialized inputs: results/mcqa_rollouts_materialized_inputs.jsonl
Rollouts: results/mcqa_rollouts.jsonl
Aggregate metrics: results/mcqa_rollouts_aggregate_metrics.json
```

For per-task pass rates, see the [`gym eval profile`](https://docs.nvidia.com/nemo/gym/main/reference/cli-commands) command.

### Using the NeMo-Gym Container with VLM or Audio/Video Benchmarks

The NeMo-Gym container omits packages with bundled codec libraries
(`opencv-python-headless`, `torchvision`, `torchaudio`) to avoid shipping
royalty-bearing binaries. If you are running VLM or audio/video benchmarks
inside the container, restore them first:

```bash
bash docker/install_codec_deps.sh
```

This installs the packages at the same versions used during the container
build. It is safe to run multiple times.

### Next Steps

- **[Browse Environments](#-available-environments)** — Browse available environments for evaluation and training.
- **[Agents](https://docs.nvidia.com/nemo/gym/main/agent-server)** — Explore available agent harnesses and learn how to integrate your own.
- **[Training](https://docs.nvidia.com/nemo/gym/tutorials/training-tutorials)** — Improve your agent or model with RL or fine-tuning.
- **[Build Custom Environments](https://docs.nvidia.com/nemo/gym/main/environment-tutorials)** — Create your own evaluation or training environments.

## 🧭 Environment Tutorials

Learn how to build custom environments through hands-on tutorials. Here are popular starting points:

| Name | Demonstrates |
| ---- | ------------ |
| [Single Step](https://docs.nvidia.com/nemo/gym/main/environment-tutorials/single-step-environment) | Basic single-step tool calling |
| [Multi Step](https://docs.nvidia.com/nemo/gym/main/environment-tutorials/multi-step-environment) | Multi-step tool calling |
| [Session State](https://docs.nvidia.com/nemo/gym/main/environment-tutorials/stateful-environment) | Session state management (in-memory) |
| [Multi Reward](https://docs.nvidia.com/nemo/gym/main/build-verifiers/multi-reward-verification) | Multiple reward components for evaluation and multi-objective RL (e.g. GDPO) |

See all [environment tutorials](https://docs.nvidia.com/nemo/gym/main/environment-tutorials) for additional patterns and advanced topics.

## 📦 Available Environments

Environments for training and evaluation.

Each resources server includes example data, configuration files, and tests. See each server's README for details.

The Dataset column links to publicly available datasets (e.g., on HuggingFace). A `-` means the train/validation data has not been publicly released yet, or that it is procedurally generated using a provided script. If no data is released yet, new data can be generated, or the environment can be used as a reference. Each server includes 5 example tasks in `data/example.jsonl`.

<!-- START_TRAINING_SERVERS_TABLE -->
| Environment       | Domain | Description                                                                                                                                                  | Value                                                                                                 | Train | Validation | License    | Config                                                                                                                        | Dataset                                                                      |
| ----------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------- | ----- | ---------- | ---------- | ----------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| Anyswe Agent      | coding | SWE-bench run by Claude Code natively inside the task container.                                                                                             | Eval software engineering capabilities on SWE-bench with any Gym agent.                               | -     | -          | -          | <a href='responses_api_agents/anyswe_agent/configs/anyswe_claude_code.yaml'>anyswe_claude_code.yaml</a>                       | -                                                                            |
| Anyswe Agent      | coding | SWE-bench run by Hermes Agent natively inside the task container.                                                                                            | Eval software engineering capabilities on SWE-bench with any Gym agent.                               | -     | -          | -          | <a href='responses_api_agents/anyswe_agent/configs/anyswe_hermes.yaml'>anyswe_hermes.yaml</a>                                 | -                                                                            |
| Anyswe Agent      | coding | SWE-bench run by OpenClaw natively inside the task container.                                                                                                | Eval software engineering capabilities on SWE-bench with any Gym agent.                               | -     | -          | -          | <a href='responses_api_agents/anyswe_agent/configs/anyswe_openclaw.yaml'>anyswe_openclaw.yaml</a>                             | -                                                                            |
| Anyswe Agent      | coding | SWE-bench run by OpenCode inside the task container.                                                                                                         | Eval software engineering capabilities on SWE-bench with any Gym agent.                               | -     | -          | -          | <a href='responses_api_agents/anyswe_agent/configs/anyswe_opencode.yaml'>anyswe_opencode.yaml</a>                             | -                                                                            |
| Anyswe Agent      | coding | SWE-bench run by Pi inside the task container.                                                                                                               | Eval software engineering capabilities on SWE-bench with any Gym agent.                               | -     | -          | -          | <a href='responses_api_agents/anyswe_agent/configs/anyswe_pi.yaml'>anyswe_pi.yaml</a>                                         | -                                                                            |
| Anyswe Agent      | coding | SWE-bench run by the Cline CLI natively inside the task container.                                                                                           | Eval software engineering capabilities on SWE-bench with any Gym agent.                               | -     | -          | -          | <a href='responses_api_agents/anyswe_agent/configs/anyswe_cline.yaml'>anyswe_cline.yaml</a>                                   | -                                                                            |
| Anyterminal Agent | coding | Terminal Bench run by claude-code natively inside the task container.                                                                                        | Evaluate terminal-task capabilities on Terminal Bench with any Gym agent.                             | -     | -          | -          | <a href='responses_api_agents/anyterminal_agent/configs/anyterminal_claude_code.yaml'>anyterminal_claude_code.yaml</a>        | -                                                                            |
| Anyterminal Agent | coding | Terminal Bench run by OpenClaw natively inside the task container.                                                                                           | Evaluate terminal-task capabilities on Terminal Bench with any Gym agent.                             | -     | -          | -          | <a href='responses_api_agents/anyterminal_agent/configs/anyterminal_openclaw.yaml'>anyterminal_openclaw.yaml</a>              | -                                                                            |
| Anyterminal Agent | coding | Terminal Bench run by the Hermes agent inside the task container.                                                                                            | Evaluate terminal-task capabilities on Terminal Bench with any Gym agent.                             | -     | -          | -          | <a href='responses_api_agents/anyterminal_agent/configs/anyterminal_hermes.yaml'>anyterminal_hermes.yaml</a>                  | -                                                                            |
| Harbor Agent      | agent  | Fast local smoketest task (trivial 1-turn task, no LLM judge) for iterating on the Gym<->Harbor bridge.                                                      | -                                                                                                     | ✓     | -          | -          | <a href='responses_api_agents/harbor_agent/configs/harbor_agent_smoketest_docker.yaml'>harbor_agent_smoketest_docker.yaml</a> | -                                                                            |
| Harbor Agent      | agent  | Harbor integration for agent harnesses and environments.                                                                                                     | Improve models in popular agentic environments supported by Harbor such as Terminus2.                 | -     | -          | -          | <a href='responses_api_agents/harbor_agent/configs/harbor_agent_opensandbox.yaml'>harbor_agent_opensandbox.yaml</a>           | -                                                                            |
| Harbor Agent      | agent  | Harbor integration for agent harnesses and environments.                                                                                                     | Improve models in popular agentic environments supported by Harbor such as Terminus2.                 | ✓     | -          | -          | <a href='responses_api_agents/harbor_agent/configs/harbor_agent.yaml'>harbor_agent.yaml</a>                                   | -                                                                            |
| Harbor Agent      | agent  | Harbor integration for agent harnesses and environments.                                                                                                     | Improve models in popular agentic environments supported by Harbor such as Terminus2.                 | ✓     | -          | -          | <a href='responses_api_agents/harbor_agent/configs/harbor_agent_daytona.yaml'>harbor_agent_daytona.yaml</a>                   | -                                                                            |
| Legal Agent Bench |        | -                                                                                                                                                            | -                                                                                                     | ✓     | -          | -          | <a href='benchmarks/legal_agent_bench/config.yaml'>config.yaml</a>                                                            | -                                                                            |
| Legal Agent Bench | agent  | Harbor-native integration of <a href='https://github.com/harveyai/harvey-labs/tree/f46ef86e4788545622db25dcffa3aebb7a139929'>Legal Agent Benchmark (LAB)</a> | Improve legal-agent document review, drafting, and analysis capability                                | ✓     | -          | -          | <a href='resources_servers/legal_agent_bench/configs/legal_agent_bench.yaml'>legal_agent_bench.yaml</a>                       | -                                                                            |
| Mini Swe Agent    | coding | Software engineering tasks driven by mini-swe agent harness.                                                                                                 | Improve agentic software engineering capabilities.                                                    | ✓     | ✓          | MIT        | <a href='responses_api_agents/mini_swe_agent/configs/mini_swe_agent.yaml'>mini_swe_agent.yaml</a>                             | <a href='https://huggingface.co/datasets/SWE-Gym/SWE-Gym'>SWE-Gym</a>        |
| Osworld Agent     | agent  | Real desktop-computer tasks driven by the OSWorld harness (DesktopEnv + inline evaluator).                                                                   | Improve agentic computer-use capabilities (GUI navigation, multi-app workflows, OS-level operations). | ✓     | ✓          | Apache 2.0 | <a href='benchmarks/osworld/config.yaml'>config.yaml</a>                                                                      | <a href='https://huggingface.co/datasets/xlangai/osworld'>osworld</a>        |
| Pinchbench        | agent  | PinchBench benchmark integration                                                                                                                             | Evaluate a model as the brain of an OpenClaw agent on real-world tasks.                               | -     | -          | -          | <a href='responses_api_agents/pinchbench/configs/pinchbench.yaml'>pinchbench.yaml</a>                                         | -                                                                            |
| Swe Agents        |        | -                                                                                                                                                            | -                                                                                                     | ✓     | ✓          | Apache 2.0 | <a href='responses_api_agents/swe_agents/configs/swebench_multi_tools.yaml'>swebench_multi_tools.yaml</a>                     | -                                                                            |
| Swe Agents        |        | -                                                                                                                                                            | -                                                                                                     | ✓     | ✓          | Apache 2.0 | <a href='responses_api_agents/swe_agents/configs/swebench_openhands.yaml'>swebench_openhands.yaml</a>                         | -                                                                            |
| Swe Agents        | coding | SWE-bench driven by the opencode agent framework.                                                                                                            | Eval software engineering capabilities on SWE-bench using opencode.                                   | ✓     | ✓          | Apache 2.0 | <a href='responses_api_agents/swe_agents/configs/swebench_opencode.yaml'>swebench_opencode.yaml</a>                           | -                                                                            |
| Tau2              | agent  | Tau2 benchmark integration                                                                                                                                   | Evaluate multi-turn agentic capability with user simulation.                                          | -     | -          | -          | <a href='responses_api_agents/tau2/configs/tau2_agent.yaml'>tau2_agent.yaml</a>                                               | -                                                                            |
| Tau2              | agent  | Tau2 benchmark integration with a 10-agent-step limit                                                                                                        | Evaluate multi-turn agentic capability with user simulation and a turn limit.                         | -     | -          | -          | <a href='responses_api_agents/tau2/configs/tau2_agent_turn_limit.yaml'>tau2_agent_turn_limit.yaml</a>                         | -                                                                            |
| Vcqa Agent        | coding | Verified Code QA - investigate a per-task repo snapshot or git bundle, then answer against a must-have rubric graded by an LLM judge.                        | Code investigation across fileset and git-history tasks.                                              | ✓     | ✓          | Apache 2.0 | <a href='responses_api_agents/vcqa_agent/configs/vcqa_agent.yaml'>vcqa_agent.yaml</a>                                         | <a href='https://huggingface.co/datasets/appliedcompute/vcqa-v1'>vcqa-v1</a> |
| Verifiers Agent   | math   | Prime intellect verifiers and environments hub integration, ace-reason math environment example.                                                             | Improve math reasoning capabilities.                                                                  | ✓     | -          | -          | <a href='responses_api_agents/verifiers_agent/configs/acereason-math.yaml'>acereason-math.yaml</a>                            | -                                                                            |
<!-- END_TRAINING_SERVERS_TABLE -->

## 📖 Documentation & Resources

- **[Documentation](https://docs.nvidia.com/nemo/gym/main)** - Technical reference docs
- **[Environment Tutorials](https://docs.nvidia.com/nemo/gym/main/environment-tutorials)** - Build custom environments
- **[Training Tutorials](https://docs.nvidia.com/nemo/gym/tutorials/training-tutorials)** - Train with NeMo Gym environments
- **[API Reference](https://docs.nvidia.com/nemo/gym/main/api/reference/api-reference)** - Complete class and function reference


## 🤝 Community & Support

We'd love your contributions! Here's how to get involved:

- **[Report Issues](https://github.com/NVIDIA-NeMo/Gym/issues)** - Bug reports and feature requests
- **[Contributing Guide](https://docs.nvidia.com/nemo/gym/main/contribute)** - How to contribute code, docs, new environments, or training framework integrations

## 📚 Citations

If you use NeMo Gym in your research, please cite it using the following BibTeX entry:

```bibtex
@misc{nemo-gym,
  title = {NeMo Gym: An Open Source Library for Scaling Reinforcement Learning Environments for LLM},
  howpublished = {\url{https://github.com/NVIDIA-NeMo/Gym}},
  author={NVIDIA},
  year = {2025},
  note = {GitHub repository},
}
```
