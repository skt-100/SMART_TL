# 🚦 SMART_TL — Smart Traffic Light using Reinforcement Learning

> An intelligent traffic-control system that uses **Deep Reinforcement Learning (DQN)** to manage a traffic light at a 4-way intersection — reducing congestion and waiting time. Built with **Python**, **PyTorch**, and the **SUMO** traffic simulator.

---

## 📖 Description

**SMART_TL** replaces a traditional fixed-timing traffic signal with an AI agent that *learns* how to control an intersection. Instead of switching lights on a fixed schedule, the agent observes the live state of all four approaching roads and dynamically chooses which signal phase to activate, learning the optimal policy through trial and error.

The agent is a **Deep Q-Network (DQN)** — a Multi-Layer Perceptron that maps an 80-value traffic state into one of four signal actions. Through training over many simulated episodes, it learns to minimize the cumulative waiting time of all vehicles. The project lets you directly compare a **traditional traffic light** against the **smart RL agent** in the same intersection scenario.

---

## 📂 Project Structure

```
SMART_TL/
├── main.py                 # Training entry point (trains the DQN agent)
├── test.py                 # Testing entry point (runs the trained agent)
├── agent.py                # RL Agent: action selection (epsilon-greedy) + experience replay
├── model.py                # Neural network (MLP) + Model class (train / predict / save)
├── env.py                  # SUMO environment: state, reward, action execution
├── episode.py              # Runs a single simulation episode & records experience
├── memory.py               # Experience Replay buffer (Memory + Sample)
├── generator.py            # Generates random vehicle routes for each episode
├── settings.py             # Loads YAML settings (training / testing)
├── constants.py            # Phases, actions, state encoding & lane mappings
│
├── training_settings.yaml  # Training hyperparameters & simulation config
├── testing_settings.yaml   # Testing configuration
├── trained_model.pt        # Pre-trained DQN model
│
├── intersection/
│   ├── environment.net.xml     # SUMO road network (4-way intersection)
│   ├── episode_routes.rou.xml  # Generated vehicle routes
│   └── sumo_config.sumocfg     # SUMO configuration file
│
├── presentation/
│   ├── TL_presentation.pptx              # Project slides
│   ├── comparsion.mp4                    # Traditional vs RL comparison video
│   └── while_training_in_one_episode.mp4 # Training episode recording
│
└── README.txt
```

---

## ✨ Key Features

- 🧠 **Deep Q-Network (DQN)** — an MLP with 4 hidden layers (400 neurons each) that maps traffic state → optimal action.
- 🚥 **Adaptive Signal Control** — 4 actions: NS Green, NS-Left Green, EW Green, EW-Left Green.
- 🛣️ **Smart State Encoding** — each incoming lane is divided into logical cells by distance from the light, giving the agent a detailed view of queued cars (80-value state).
- 🔁 **Experience Replay** — a memory buffer (up to 50,000 samples) for stable, efficient learning.
- 🎲 **Epsilon-Greedy Exploration** — balances random exploration and learned exploitation, with epsilon decay over time.
- 🎯 **Reward Function** — penalizes long waiting times and queue lengths to encourage smooth traffic flow.
- 🚗 **Realistic Simulation** — powered by SUMO with 1,000 generated vehicles per episode on straight and turning routes.
- ⚖️ **Traditional vs Smart Comparison** — run a fixed-timing baseline and the trained RL agent on the same scenario.
- ⚙️ **YAML-Configurable** — all hyperparameters and simulation settings are easily tunable.

---

## 🛠️ Tech Stack

| Component | Technology |
|-----------|-----------|
| Language | Python |
| Deep Learning | PyTorch |
| Simulation | SUMO (Simulation of Urban MObility) |
| Algorithm | Deep Q-Learning (DQN) |
| Config | YAML |

---

## 🚀 Getting Started

### 1. Install SUMO
Download and install the SUMO simulator from the official site:
👉 [https://sumo.dlr.de/docs/Downloads.php](https://sumo.dlr.de/docs/Downloads.php)

Make sure the `SUMO_HOME` environment variable is set after installation.

### 2. Install Python dependencies

```bash
pip install torch numpy pyyaml
```

### 3. Run the project

**▶️ Traditional Traffic Light (baseline):**
```bash
sumo-gui intersection/sumo_config.sumocfg
```

**🤖 Smart RL Traffic Light (trained agent):**
```bash
python test.py
```

**🏋️ Train your own model from scratch:**
```bash
python main.py
```

> 💡 Set `gui: true` in the YAML settings files to watch the simulation live.

---

## 📊 Results & Demo

Comparison and training videos are available in the [`presentation/`](presentation/) folder:

- `comparsion.mp4` — Traditional signal vs Smart RL agent
- `while_training_in_one_episode.mp4` — The agent learning during a training episode
- `TL_presentation.pptx` — Full project presentation

---

## ⚙️ Key Hyperparameters

| Parameter | Value |
|-----------|-------|
| Episodes | 100 |
| Max steps / episode | 5,400 |
| Cars generated | 1,000 |
| Hidden layers | 4 × 400 |
| Learning rate | 0.001 |
| Gamma (discount) | 0.95 |
| Batch size | 100 |
| Memory size | 500 – 50,000 |

---

*Built as a graduation project — applying AI & Reinforcement Learning to real-world traffic management.*
