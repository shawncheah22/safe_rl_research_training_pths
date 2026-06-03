# SafeRL Research — Training Checkpoints

Training state files (.pth) from my MEng Master thesis on Safe Reinforcement Learning at Imperial College London.

## Overview

This repository contains checkpoint files for all agents trained in the SafeRL Research project. Each `.pth` file stores the full training state — episode number, model weights, and per-episode metrics history (rewards, costs, collisions, goals reached).

The agents are trained on the **SafetyPointGoal1-v0** environment from [Safety Gymnasium](https://github.com/PKU-Alignment/safety-gymnasium), where a point robot must navigate to goals while avoiding hazards.

## Files

| File                                                      | Agent                                         | Episodes |
| --------------------------------------------------------- | --------------------------------------------- | -------- |
| `ppo_training_state.pth`                                  | Standard PPO (no safety constraint)           | 1100     |
| `ppo_lagrangian_training_state.pth`                       | PPO-Lagrangian (Lagrangian safety constraint) | 1100     |
| `ppo_llm_shield_training_state.pth`                       | PPO + LLM Shield — Iteration 1 (Qwen)         | 630      |
| `ppo_llm_shield_iter2_training_state.pth`                 | PPO + LLM Shield — Iteration 2 (Qwen)         | 630      |
| `ppo_llm_shield_iter2_anthropic_haiku_training_state.pth` | PPO + LLM Shield — Iteration 2 (Claude Haiku) | 620      |

## Loading a Checkpoint

```python
import torch

state = torch.load('ppo_llm_shield_iter2_training_state.pth', map_location='cpu', weights_only=False)

rewards   = state['rewards_per_episode']
costs     = state['costs_per_episode']
episodes  = state['episode']  # last completed episode index
```
