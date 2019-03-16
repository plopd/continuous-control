
## Learning Algorithm

The agent is trained with [DDPG, Lillicrap, Timothy P., et al. "Continuous control with deep reinforcement learning." arXiv preprint arXiv:1509.02971 (2015)](https://arxiv.org/pdf/1509.02971.pdf).

**Neural Network Architectures**

#### Actor

```markdown
----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
            Linear-1                  [-1, 256]           8,704
       BatchNorm1d-2                  [-1, 256]             512
            Linear-3                  [-1, 128]          32,896
       BatchNorm1d-4                  [-1, 128]             256
            Linear-5                    [-1, 4]             516
================================================================
Total params: 42,884
Trainable params: 42,884
Non-trainable params: 0
----------------------------------------------------------------
Input size (MB): 0.00
Forward/backward pass size (MB): 0.01
Params size (MB): 0.16
Estimated Total Size (MB): 0.17
----------------------------------------------------------------
```

- Linear(33, 256) - ReLU - BatchNorm - Linear(256, 128) -  ReLU - BatchNorm - Linear(128, 4) - Tanh

#### Critic

```markdown
----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
            Linear-1                  [-1, 256]           8,704
       BatchNorm1d-2                  [-1, 256]             512
            Linear-3                  [-1, 128]          33,408
            Linear-4                    [-1, 1]             129
================================================================
Total params: 42,753
Trainable params: 42,753
Non-trainable params: 0
----------------------------------------------------------------
Input size (MB): 0.00
Forward/backward pass size (MB): 0.00
Params size (MB): 0.16
Estimated Total Size (MB): 0.17
----------------------------------------------------------------
```

- Linear(33, 256) - ReLU - BatchNorm - Linear(256+4, 128) -  ReLU - Linear(128, 1)


- **Weight initialization**: 
  - Uniform in range (-1/sqrt(fan-in), 1/sqrt(fan-in))
  - Last layer uniform in range (-3e-3, 3e-3)


**Other hyperparameters**

```
buffer_size = int(1e5) # capacity of replay buffer
batch_size = 128 # batch-size
gamma = 0.99 # discount factor
tau = 1e-3 # soft-update factor (when updating the target network weights) 
lr_actor = 1e-4 # learning rate for training the Actor with SGD
lr_critic = 1e-3 # learning rate for training the Critic with SGD
optimizer = Adam
maximum_timesteps = 1000 # maximum number of timesteps within one episode.
number_episodes = 2000 # number of episodes to train
weight_decay = 0 # weight decay (L2 penalty) for Adam optimizer
seed = 2 # for reproducibility
```

## Plot of Rewards

Average reward (over 100 consecutive episodes, and over all agents)

![Scores](./results/avg_scores.png)

```
Environment solved in 100 episodes!	Average Score: 37.89
```

## Notes

- Adding a different (standard normally distributed) noise to each agent's action using the *Ornstein-Uhlenbeck process* accelerated and improved learning. Adding uniform noise makes learning slow.

- Addign batch normalization for Actor and Critic improved learning speed.  

## Ideas for Future Work

- [DDPG](https://arxiv.org/pdf/1509.02971.pdf)
  - Train each agent with a different Actor/Critic
  - Try PER (see https://ieeexplore.ieee.org/document/8122622/)
  

- Solve the environment using [PPO](https://arxiv.org/pdf/1707.06347.pdf).

