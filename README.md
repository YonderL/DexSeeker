# DexSeeker 🤖🔍

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![Docker Supported](https://img.shields.io/badge/docker-supported-blue.svg)](https://www.docker.com/)
[![Isaac Sim](https://img.shields.io/badge/Simulator-Isaac_Sim-green.svg)]()

**DexSeeker** (Dexterous Seeker) is an open-source Embodied AI framework focused on **Mobile Manipulation with Episodic Memory & Active Perception**. 

Moving beyond traditional Vision-Language Navigation (VLN) where agents stop at "arriving near the target," DexSeeker is designed for complex, human-collaborative household environments. It empowers robots to not only navigate semantically but also use dexterous manipulation to actively uncover, rummage through, and find small objects hidden in cluttered spaces.

## 🌟 Key Features

* **Active Perception & Rummaging:** Uses end-to-end control policies (e.g., Diffusion Transformers) to allow the robot hand to push, sweep, and uncover hidden objects in cluttered corners.
* **Episodic Memory Agent:** Builds a spatial-temporal semantic map during routine patrols. If an object is partially obscured later, the agent queries its local memory to reason about its likely location.
* **Privacy-First Local Storage:** All memory and semantic embeddings are stored locally, ensuring user privacy in household scenarios.
* **Decoupled Architecture:** Clean separation between the "Brain" (VLM-based reasoning & memory) and the "Cerebellum" (dexterous control policies), communicating via lightweight APIs.

## 🏗️ System Architecture

DexSeeker is designed with a full-stack AI approach, making it easy to deploy and extend:

1.  **The Brain (Cognition & Memory):** * Powered by large-scale VLMs (like Qwen-VL or CLIP) for open-vocabulary object recognition and 3D scene graph construction.
    * **FastAPI** backend to handle reasoning requests and manage the local vector database for spatial-temporal memory.
2.  **The Cerebellum (Motor Control):** * Executes complex rummaging policies trained via imitation learning / RL in simulation.
3.  **Simulation Environment:**
    * Currently targeting **NVIDIA Isaac Sim** for high-fidelity physics and realistic contact dynamics necessary for soft/rigid object manipulation.

## 🚀 Getting Started

We prioritize a smooth Developer Experience (DX). You don't need to configure complex ROS/Python environments manually. 

### Prerequisites
* Ubuntu 22.04+
* NVIDIA GPU (RTX 3090/4090 recommended for Isaac Sim & local VLMs)
* Docker & NVIDIA Container Toolkit

### Quick Start (Docker)

Clone the repository and spin up the environment using Docker Compose:

```bash
git clone [https://github.com/yonderl/DexSeeker.git](https://github.com/yonderl/DexSeeker.git)
cd DexSeeker

# Build and start the Brain backend and Simulation container
docker-compose up -d --build
```
(Note: Detailed instructions for setting up the Isaac Sim headless container and downloading pre-trained weights can be found in docs/INSTALLATION.md)

🗺️ Roadmap
[ ] Phase 1 (V0.1): The Desktop Rummager - Implement basic pushing/uncovering policies for a robot arm in a cluttered desk simulation.

[ ] Phase 2 (V0.2): Memory-Augmented Search - Integrate local episodic memory. The robot remembers where it saw an item 10 minutes ago and navigates there.

[ ] Phase 3 (V1.0): Full House Explorer - Full integration of VLM navigation, memory reasoning, and dexterous uncovering in a multi-room Isaac Sim environment.

🤝 Contributing
We welcome contributions from researchers, full-stack engineers, and robotics enthusiasts! Whether you are interested in fine-tuning VLMs, optimizing FastAPI backends, or training DiT control policies in simulation, there is a place for you here.

Please read our CONTRIBUTING.md to get started. Let's build the future of Embodied AI together!

📄 License
This project is licensed under the MIT License - see the LICENSE file for details.