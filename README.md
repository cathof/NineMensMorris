# Nine Men's Morris – Reinforcement Learning Agent

This repository contains a reinforcement learning project for **Nine Men’s Morris (Mill)**.
An agent is trained via **self-play** using **Maskable PPO** and evaluated with and without
**potential-based reward shaping (PBRS)**.

The focus of this project is a **fair comparison between sparse rewards and shaped rewards**
while keeping the game dynamics identical.

---

## Contents

- `muehle_V1.ipynb`  
  Final notebook containing:
  - Environment implementation (`MillEnv`)
  - Action masking and legality handling
  - Fixed-opponent self-play wrapper
  - Potential-based reward shaping (optional)
  - Training and evaluation code
  - Sparse vs. PBRS comparison

---

## Game Environment

- Full implementation of **Nine Men’s Morris**
- Three phases: placement, move, fly
- Illegal moves are prevented via **action masking**
- Draw detection via no-capture counter
- Deterministic and reproducible evaluation

---

## Reward Design

Two reward settings are supported:

### Sparse Rewards
- Win: `+10`
- Loss: `-10`
- Draw: `0`
- Minor step rewards (mill formation, capture)

### Potential-Based Reward Shaping (PBRS)
- Shaping term:  
  \[
  r'(s,a,s') = r(s,a,s') + \gamma \Phi(s') - \Phi(s)
  \]
- Potential function includes:
  - material advantage
  - number of mills
  - number of open mills
- Shaping is **disabled during evaluation** for fairness

---

## Training

- Algorithm: **Maskable PPO (sb3-contrib)**
- Self-play with snapshot pool of past agents
- Deterministic opponent switching
- Metrics logged via a custom callback

Two final models were trained:
- `maskable_selfplay_mill_sparse.zip`
- `maskable_selfplay_mill_pbrs.zip`

---

## Evaluation

- Agents are evaluated **against each other**
- Both player roles (+1 / -1) are tested
- Shaping is **turned off during evaluation**
- Metrics include:
  - win / loss / draw rate
  - mills and captures
  - terminal reasons
  - episode length

---

## Requirements

- Python 3.10+
- gymnasium
- stable-baselines3
- sb3-contrib
- numpy

---

## Author

Catherine Hofstetter  
