[//]: # (Image References)

# Continuous Control

## Introduction

### Objective

Train a double-jointed arm to move its hand to the goal location, and keep it there by using policy-based (and value-based) methods.

![Trained Agent](./results/trained_agent.gif)

### Background

The project solves the [Reacher](https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Learning-Environment-Examples.md#reacher) environment.

In this environment, a double-jointed arm can move to target locations. A reward of +0.1 is provided for each step that the agent's hand is in the goal location. Thus, the goal of your agent is to maintain its position at the target location for as many time steps as possible.

The observation space consists of 33 variables corresponding to position, rotation, velocity, and angular velocities of the arm. Each action is a vector with four numbers, corresponding to torque applicable to two joints. Every entry in the action vector should be a number between -1 and 1.


#### Distributed Training

The project contains the environment version contains 20 identical agents, each with its own copy of the environment.
The second version is useful for algorithms like PPO, A3C, and D4PG that use multiple (non-interacting, parallel) copies of the same agent to distribute the task of gathering experience.

#### Solving the Environment

The agents must get an average score of +30 (over 100 consecutive episodes, and over all agents). Specifically,

- After each episode, we add up the rewards that each agent received (without discounting), to get a score for each agent. This yields 20 (potentially different) scores. We then take the average of these 20 scores.
- This yields an average score for each episode (where the average is over all 20 agents).
As an example, consider the plot below, where we have plotted the average score (over all 20 agents) obtained with each episode.

## Getting Started

### Setup

0. Clone the repository
```bash
https://github.com/plopd/continuous-control.git
cd continuous-control
```

1. Create and activate a new environment with Python 3.6.

	- __Linux__ or __Mac__: 
	```bash
	conda create --name continuous_control python=3.6
	source activate continuous_control
	```
	- __Windows__: 
	```bash
	conda create --name continuous_control python=3.6 
	activate continuous_control
	```
	
2. Clone and install the openai-gym repository
```bash
cd ..
git clone https://github.com/openai/gym.git
cd gym
pip install -e .
```

3. Create an [IPython kernel](http://ipython.readthedocs.io/en/stable/install/kernel_install.html) for the `continuous_control` environment.  
```bash
python -m ipykernel install --user --name navigation --display-name "continuous_control"
```

4. Start (local) jupyter notebook server
```bash
cd ../continuous-control
jupyter-notebook
```

**2. Download the Unity Environment**

1. Download the environment from one of the links below.  You need only select the environment that matches your operating system:

    - **_Version 1: One (1) Agent_**
        - Linux: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Linux.zip)
        - Mac OSX: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher.app.zip)
        - Windows (32-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Windows_x86.zip)
        - Windows (64-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Windows_x86_64.zip)

    - **_Version 2: Twenty (20) Agents_**
        - Linux: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Linux.zip)
        - Mac OSX: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher.app.zip)
        - Windows (32-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Windows_x86.zip)
        - Windows (64-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Windows_x86_64.zip)

2. Place the file in the root of this repo, and unzip (or decompress) the file.

### Instructions

To train an agent run `python train.py`. The python file contains many useful command line arguments:

```
    parser.add_argument("-env_fp", "--environment_filepath", help="Filepath to environment to load.",
                        default='env/Reacher.app')
    parser.add_argument("-no_gr", "--no_graphics", help="Whether to display the environment.",
                        action="store_true", default=True)
    parser.add_argument("-n_episodes", "--number_episodes", help="Number of episodes to train.",
                        default=2000, type=int)
    parser.add_argument("-max_t", "--maximum_timesteps", help="Maximum number of timesteps within one episode.",
                        default=1000, type=int)
    parser.add_argument("-seed", "--seed", help="Random seed for reproducibility.",
                        default=2, type=int)
    parser.add_argument("-save_every_nth", "--save_every_nth", help="Save checkpoint every nth episode",
                        default=25, type=int)
    parser.add_argument("-bfsz", "--buffer_size", help="Buffer size of the replay memory.",
                        default=int(1e5), type=int)
    parser.add_argument("-bsz", "--batch_size", help="Batch size of experience to sample from replay buffer.",
                        default=128, type=int)
    parser.add_argument("-gamma", "--gamma", help="Discount factor for the cumulative rewards.",
                        default=.99, type=float)
    parser.add_argument("-tau", "--tau", help="Interpolation factor for soft update model parameters.",
                        default=1e-3, type=float)
    parser.add_argument("-lr_actor", "--learning_rate_actor", help="Learning rate for SGD on actor's parameters.",
                        default=1e-4, type=float)
    parser.add_argument("-lr_critic", "--learning_rate_critic", help="Learning rate for SGD on critic's parameters.",
                        default=1e-3, type=float)
    parser.add_argument("-weight_decay", "--weight_decay", help="Weight decay (L2 penalty) for Adam optimizer.",
                        default=0, type=float)

```

##### Code

`results` - camera-ready graphs and figures highlighting the results of the training as well as checkpoints of the trained agent.

`utils` - helper methods (e.g. saving checkpoints, plotting, ...)

`Continuous_Control.ipynb` - notebook with environment setup and demo of a smart agent.

`REPORT.md` - outlines details on the algorithms used to train the agent


