<div align="center">

# 🤖🔍 DexSeeker (Dexterous Seeker)

**An Open-Source Embodied AI Framework for Mobile Manipulation with Episodic Memory & Active Perception.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![Docker Supported](https://img.shields.io/badge/docker-supported-blue.svg)](https://www.docker.com/)
[![Simulator: Isaac Sim](https://img.shields.io/badge/Simulator-Isaac_Sim-green.svg)]()

<br>

<table>
  <tr>
    <td align="center" width="50%">
      <img src="https://raw.githubusercontent.com/isaac-sim/IsaacGymEnvs/main/docs/images/rl_franka.png" width="100%" style="max-width:420px" alt="Franka arm RL demo (Isaac Gym Envs)"/>
      <br/>
      <sub><b>Arm manipulation</b> · Franka task suite</sub>
    </td>
    <td align="center" width="50%">
      <img src="https://raw.githubusercontent.com/isaac-sim/IsaacGymEnvs/main/docs/images/rl_allegro.png" width="100%" style="max-width:420px" alt="Allegro hand RL demo (Isaac Gym Envs)"/>
      <br/>
      <sub><b>Dexterous control</b> · Allegro hand RL</sub>
    </td>
  </tr>
</table>

<sub>Still frames from <a href="https://github.com/isaac-sim/IsaacGymEnvs"><code>isaac-sim/IsaacGymEnvs</code></a> docs (NVIDIA Isaac ecosystem). Older GIF URLs in many READMEs now 404 after the repo move and asset refresh.</sub>

</div>

<br>

> **Moving beyond traditional Vision-Language Navigation (VLN)...**
> DexSeeker is designed for complex, human-collaborative household environments. It empowers robots to not only navigate semantically but also use dexterous manipulation to **actively uncover, rummage through, and find small objects hidden in cluttered spaces.**

---

## ✨ Key Features

* 🦾 **Active Perception & Rummaging:** Uses end-to-end control policies (e.g., Diffusion Transformers) to allow the robot hand to push, sweep, and uncover hidden objects in cluttered corners.
* 🧠 **Episodic Memory Agent:** Builds a spatial-temporal semantic map during routine patrols. If an object is partially obscured later, the agent queries its local memory to reason about its likely location.
* 🔒 **Privacy-First Local Storage:** All memory and semantic embeddings are stored locally, ensuring user privacy in household scenarios.
* 🧩 **Decoupled Architecture:** Clean separation between the "Brain" (VLM-based reasoning & memory) and the "Cerebellum" (dexterous control policies), communicating via lightweight APIs.

## 🏗️ System Architecture

DexSeeker is designed with a full-stack AI approach, making it easy to deploy, test, and extend:

| Module | Description | Tech Stack |
| :--- | :--- | :--- |
| **🧠 The Brain** | Cognition, reasoning, and spatial-temporal memory. | `Qwen-VL` / `CLIP`, `FastAPI`, `Vector DB` |
| **🦾 The Cerebellum** | Executes complex rummaging policies (IL/RL). | `PyTorch`, `Diffusion Transformers (DiT)` |
| **🌍 Simulation** | High-fidelity physics and realistic contact dynamics. | `NVIDIA Isaac Sim` |

## 🚀 Getting Started

We prioritize a smooth Developer Experience (DX). You don't need to configure complex ROS/Python environments manually.

### Prerequisites

* **OS:** Ubuntu 22.04+
* **Hardware:** NVIDIA GPU (RTX 3090/4090 highly recommended for Isaac Sim & local VLMs)
* **Environment:** Docker & NVIDIA Container Toolkit

### Quick Start (Docker)

Clone the repository and spin up the environment using Docker Compose:

```bash
git clone https://github.com/YonderL/DexSeeker.git
cd DexSeeker

# Build and start the Brain backend and Simulation container
docker-compose up -d --build
```

**Note:** Detailed instructions for setting up the Isaac Sim headless container and downloading pre-trained weights can be found in `docs/INSTALLATION.md`.

## 🗺️ Roadmap

| Phase | Milestone | Description |
| :---: | :--- | :--- |
| 1 | **V0.1 · The Desktop Rummager** | Implement basic pushing/uncovering policies for a robot arm in a cluttered desk simulation. |
| 2 | **V0.2 · Memory-Augmented Search** | Integrate local episodic memory. The robot remembers where it saw an item minutes ago and navigates there. |
| 3 | **V1.0 · Full House Explorer** | Full integration of VLM navigation, memory reasoning, and dexterous uncovering in a multi-room Isaac Sim environment. |

**Checklist (sync with the table above)**

- [ ] Phase 1 — V0.1 · The Desktop Rummager
- [ ] Phase 2 — V0.2 · Memory-Augmented Search
- [ ] Phase 3 — V1.0 · Full House Explorer

When a phase is **done**, mark it `- [x]` and wrap the phase label in `~~strikethrough~~`, e.g. `- [x] ~~Phase 1 — V0.1 · The Desktop Rummager~~`. Omit `~~` if you prefer a plain checked item only.

## 🤝 Contributing

We welcome contributions from researchers, full-stack engineers, and robotics enthusiasts.

Whether you are interested in fine-tuning VLMs, optimizing FastAPI backends, or training DiT control policies in simulation, there is a place for you here. Please read our `CONTRIBUTING.md` to get started. Let's build the future of Embodied AI together.

## 📄 License

This project is licensed under the MIT License — see the `LICENSE` file for details.
