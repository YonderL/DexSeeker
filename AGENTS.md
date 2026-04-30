# AGENTS.md

This file provides guidance to Codex (Codex.ai/code) when working with this repository.

## Project Overview

DexSeeker is an open-source embodied AI framework for mobile manipulation with episodic memory and active perception. It targets household environments where robots must navigate semantically and use dexterous manipulation to uncover hidden objects in cluttered spaces.

## Architecture

The system follows a decoupled "Brain/Cerebellum" design:

| Module | Role | Tech Stack |
| :--- | :--- | :--- |
| **The Brain** | Cognition, reasoning, spatial-temporal memory | Qwen-VL / CLIP, FastAPI, Vector DB |
| **The Cerebellum** | Executes rummaging policies (IL/RL) | PyTorch, Diffusion Transformers (DiT) |
| **Simulation** | High-fidelity physics and contact dynamics | NVIDIA Isaac Sim |

Key design principles:
- Clean separation between reasoning (Brain) and control (Cerebellum)
- Communication via lightweight APIs
- Privacy-first local storage for memory and embeddings
- Docker-based development environment

## Development Commands

```bash
# Start the full environment
docker-compose up -d --build

# (Future) Run tests
pytest

# (Future) Lint
ruff check .
```

## Roadmap

- **Phase 1 (V0.1):** Semantic Pathfinder — local LLM intent parsing and semantic navigation over a known topological map
- **Phase 2 (V0.2):** Desktop Rummager — visual search plus pushing/uncovering policies for cluttered desktop environments
- **Phase 3 (V0.3):** Memory-Augmented Search — local episodic memory recording and retrieval for object search
- **Phase 4 (V1.0):** Full House Explorer — integrated navigation, memory reasoning, active perception, and dexterous manipulation in multi-room Isaac Sim environments

## Key Constraints

- Target platform: Ubuntu 22.04+ with NVIDIA GPU (RTX 3090/4090 recommended)
- All memory/embeddings stored locally (no cloud)
- Isaac Sim runs headless in Docker containers
