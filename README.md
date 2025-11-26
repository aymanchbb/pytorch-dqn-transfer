# Transfer Learning Experiment: CartPole to Acrobot

This project explores the concept of Transfer Learning in Deep Reinforcement Learning.

The core idea is similar to a tennis player switching from singles (1v1) to doubles (2v2). The rules and the court dimensions change slightly, but the player doesn't need to relearn how to hit the ball. They transfer their core skills (physics, timing, stamina) to the new context.

I wanted to test if a Deep Q-Network (DQN) could do the same: learn the laws of physics on a simple environment (CartPole) and reuse that knowledge to learn a harder task (Acrobot) faster.

## Project Overview

The project is divided into progressive phases:

### Phase 1: Solving CartPole-v1 (Completed)
Before attempting any transfer, I needed a solid baseline. I implemented a DQN agent from scratch using PyTorch (no high-level RL libraries).
* **Architecture:** 3 fully connected hidden layers (128 units each).
* **Key components:** Experience Replay, Target Network, Epsilon-Greedy exploration.
* **Results:** The agent solves the environment consistently, reaching the max score of 500 around episode 350.

### Phase 2: Transfer with Differential Fine-Tuning (In progress)
**Goal:** Reuse the physics knowledge (weights) acquired by the CartPole agent while quickly adapting to the new Acrobot control system.
* **Method:** We perform initial "Network Surgery" (replacing the input and output layers to match the new dimensions: 4→6 and 2→3). The entire network is then trained using a **Differential Learning Rate** strategy.
    * The "new" layers (Input/Output) use a high Learning Rate to learn quickly from scratch.
    * The "transferred" core layers (Hidden Layers) use a very low Learning Rate to gently fine-tune the learned physics features without destroying the original knowledge.
     
* **Key components:** (Not yet)
* **Results:** (Not Yet)
  
### Phase 3: Pre & Post-processing Layers (Not yet Started)
**Goal:** Improve the quality of the transfer by adapting the signal *before* it reaches the pre-trained core.
* **Hypothesis:** Direct connection between raw Acrobot states and the CartPole hidden layers is suboptimal.
* **Method:** We will add dedicated **Adapter Layers** (pre/post-processing layers) to the architecture. These layers will also be trained with a high Learning Rate to learn how to efficiently "translate" Acrobot's complex angle/velocity inputs into the specific format that the original CartPole brain is best at processing.
* **Key components :**
* **Results:**

### Phase 4: Dual-Network Architecture (The Consultant) (Not yet started)
**Goal:** Train a completely new network for Acrobot that uses the old network as a tool.
* **Method:** I will create a fresh network for Acrobot. However, the frozen CartPole network will run in parallel. The new network will receive the Acrobot state *AND* the output of the CartPole network as inputs.
* **Concept:** The old brain acts as a "consultant" or a feature extractor. The new brain decides whether to listen to it or not.
* **Key components :**
* **Results:**
## Installation

Install the required dependencies:

```bash
pip install -r requirements.txt
```

## 📝 Author's Note
This project was developed during my **Undergraduate studies**. 
It represents an educational exploration where I aimed to build algorithms manually (without high-level libraries) to deeply understand the mechanics of Loss Functions, Backpropagation, and Gradient Descent in Reinforcement Learning.
