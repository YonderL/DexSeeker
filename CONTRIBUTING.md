# Contributing to DexSeeker

🎉 Thank you for your interest in the DexSeeker community!  
We are building an open-source embodied AI framework for real household scenarios. This guide helps you quickly get started with environment setup, development, and PR submission.

## Table of Contents

- [How Can I Contribute?](#how-can-i-contribute)
- [Development Setup](#development-setup)
- [Edge Device Notes (Jetson AGX Orin)](#edge-device-notes-jetson-agx-orin)
- [Build and Run](#build-and-run)
- [Style Guides](#style-guides)
- [Pull Request Process](#pull-request-process)
- [Getting Help](#getting-help)

## How Can I Contribute?

We welcome the following types of contributions:

### 1) Reporting Bugs

Please open a GitHub Issue and include:

- What happened vs. what you expected
- Minimal reproducible steps (step-by-step)
- Logs and stack traces (screenshots or text)
- Runtime environment:
  - OS (for example, Ubuntu 22.04)
  - ROS 2 version (for example, Humble)
  - Python version
  - GPU/edge device model (for example, RTX 4090 / Jetson AGX Orin)
  - CUDA / TensorRT versions (if applicable)

### 2) Suggesting Enhancements

New ideas are welcome. We strongly recommend discussing them in an Issue before implementation.  
Please describe:

- Use case and pain point
- Proposed solution (optional)
- Related modules (navigation, memory, manipulation, etc.)

### 3) Code Contribution

Current priority areas (aligned with the Roadmap):

- `V0.1` Semantic navigation and local LLM intent parsing
- `V0.2` Desktop visual search and robotic manipulation policies
- `V0.3` Episodic memory recording and retrieval
- `V1.0` Full-stack orchestration (navigation + memory + active perception + dexterous manipulation)

## Development Setup

> We strongly recommend using Docker first to keep development and deployment environments consistent.

### Prerequisites

- Ubuntu `22.04+`
- ROS 2 `Humble`
- Python `3.10+`
- Docker + Docker Compose
- NVIDIA Driver + NVIDIA Container Toolkit

### 1) Fork and clone the repository

```bash
git clone https://github.com/<your-username>/DexSeeker.git
cd DexSeeker
```

### 2) Start the containerized development environment

```bash
docker-compose up -d --build
```

### 3) Enter the development container

```bash
docker exec -it dexseeker-dev bash
```

If your container name is not `dexseeker-dev`, list containers first:

```bash
docker ps --format "table {{.Names}}\t{{.Status}}"
```

### 4) Install Python dependencies (if required by your module)

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

## Edge Device Notes (Jetson AGX Orin)

If you run local inference on Jetson or other edge platforms, verify:

- JetPack / L4T version matches your CUDA version
- TensorRT version matches your model export format (ONNX / engine)
- CUDA visibility is consistent inside and outside containers (`nvidia-smi` / `tegrastats`)
- Prefer FP16 / INT8 inference when accuracy requirements allow
- Plan VRAM budget and concurrency carefully to avoid latency spikes from contention between navigation and inference

Please include your edge hardware/software setup in Issues or PRs for easier reproduction and performance alignment.

## Build and Run

For a ROS 2 workspace (`colcon`):

```bash
# Run in your ROS 2 workspace root
source /opt/ros/humble/setup.bash
colcon build --symlink-install
source install/setup.bash
```

Example: run tests

```bash
colcon test
colcon test-result --verbose
```

If your module uses `pytest`:

```bash
pytest -q
```

## Style Guides

### Python

- Follow PEP 8
- Recommended tools:

```bash
black .
flake8
```

### ROS 2

- Keep `Topic` / `Service` / `Action` naming clear and consistent
- Avoid hard-coded namespaces; prefer relative names + launch-time parameter injection
- Use the ROS parameter system instead of scattering config values as code constants

### Commit Message Format

We recommend Conventional Commits:

- `feat: add local LLM reasoning node`
- `fix: resolve memory leak in Nav2`
- `docs: update CONTRIBUTING setup steps`
- `refactor: simplify memory query pipeline`

## Pull Request Process

1. Fork and clone your repository
2. Create a feature branch (do not develop directly on `main`)
3. Ensure all local tests pass
4. Keep PRs atomic: one PR should solve one issue/feature
5. In the PR description, include:
   - Motivation and context
   - Main changes
   - Test method and results
   - Related Issue (for example, `Closes #12`)
6. Wait for maintainer review and iterate based on feedback

Suggested PR template:

```md
## What
- 

## Why
- 

## How to Test
- [ ] Unit tests
- [ ] Integration tests
- [ ] Manual validation

## Related Issue
Closes #
```

## Getting Help

If you get blocked during development, you can ask for help via:

- GitHub Issues: bug reports and feature requests
- GitHub Discussions: architecture, design trade-offs, and Roadmap discussions

When asking questions, please include logs, environment details, and reproduction steps whenever possible.  
Thanks again for contributing and helping DexSeeker grow into a sustainable, long-term embodied AI open-source project.
