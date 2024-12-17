#rl 

> [!warning]  Disclaimer
> Contents of this file are references from the nicely curated resource by OpenAI: Spinning Up in Deep RL https://spinningup.openai.com/en/latest/user/introduction.html

### The Basis of Reinforcement Learning
![[Key Concepts in Reinforcement Learning-20241217134517518.png]]
>[! info] Definition  
>The basis of RL are formed by the **Agent** that interacts with the **Environment**.

#### 1. **Agents** perceive **Rewards** in **Environments** 
##### 1.1 Environment
This is the world that the agent lives in and interacts with. At every step of **interaction**, the agent sees an **observation** of the state of the world. Based on that observation, the agent determines the next **action** to take.

When the agent acts on the environment, it may change. It may also change on its own.

##### 1.2 Reward
The agent perceives a reward signal from the environment, which tells it how *good* or *bad* the current world state is. In a general sense, <mark style="background: #ABF7F7A6;">the agent's goal is to maximize its cumulative reward</mark> - a.k.a **return**.

Different reinforcement learning methods embody the different ways that the agent can learn behaviors to achieve this goal.

#### 2. How **States** and **Observations** define environments
A **state** $s$ is a *complete* description of the state of the world, meaning that there is no information about the world which is hidden from the state. 
- When the agent is able to observe the complete state of the environment, we say that the environment is <mark style="background: #ADCCFFA6;">fully observed</mark>

An **observation** $o$ is not a complete description. At least not necessarily. It is a *partial* description of a state, meaning that it may omit information.
- When the agent is only able to observe a partial state of the environment, we say that the environment is <mark style="background: #ADCCFFA6;">partially observed</mark>

Both states and observations are almost always represented by a <mark style="background: #ABF7F7A6;">real-valued vector</mark>, a <mark style="background: #ABF7F7A6;">matrix</mark>, or by a <mark style="background: #ABF7F7A6;">higher-order tensor</mark>. For instance,
- a **visual observation** could be represented by the **RGB matrix** of its pixel values
- a **state representation of a robot** may be defined by its **joint angles and velocities** 

> [!tip] 
> Reinforcement learning notation sometimes puts the symbol for state, $s$, in places where it would be technically more appropriate to write the symbol for observation, $o$. Specifically, this happens when talking about how the agent decides an action: we often signal in notation that the action is conditioned on the state, when in practice, the action is conditioned on the observation because the agent does not have access to the state.

#### 3. **Actions** and **Policies** for Agents to take
##### 3.1 Action Spaces
Different environments allow for different kinds of actions. The *set of all valid actions in a given environment* is defined as the **action space**.
- Some environments, like Atari and Go, have <mark style="background: #ADCCFFA6;">discrete actions spaces</mark>, where only a finite number of actions are available to the agent
- Other environments, e.g. one where the agent controls a robot in a physical world, have <mark style="background: #ADCCFFA6;">continuous action spaces</mark>, where actions are real-values vectors

> [!tip]
> This distinction is consequential for methods in deep RL! Some families of algorithms can be directly applied in one case, and would have to be reworked for the other.

##### 3.2 Policies
A policy is a *rule* used by an agent to decide what actions to take. 

It can either be <mark style="background: #ADCCFFA6;">deterministic</mark>, in which case it is usually denoted by $\mu$:
$$a_t=\mu(s_t),$$
or it may be <mark style="background: #ADCCFFA6;">stochastic</mark>, in which case it is usually denoted by $\pi$:
$$a_t \sim\pi(\cdot | s_t).$$

> [!tip] 
> Since the policy is essentially the agent's *brain*, it is not uncommon to substitute the word **"policy"** for **"agent"**, e.g. saying: *"The policy is trying to maximize reward"*

Specifically in deep RL, we deal with <mark style="background: #ADCCFFA6;">parameterized policies</mark>: policies whose outputs are computable functions that depend on a set of parameters (e.g. the weights and biases of a neural network). These policies are adjusted via some optimization algorithm to change the behavior of the agent.

We denote parameters of such a policy by $\theta$ (theta) or $\phi$ (phi), and then write this as a subscript on the policy symbol to highlight the connection:
$$a_t=\mu_\theta(s_t)$$
$$a_t\sim\pi_\theta(\cdot|s_t)$$
###### 3.1 a) Deterministic Policies
The following is a code snippet for building a simple deterministic policy for a continuous action space in PyTorch, using the `torch.nn` package:
```python
# https://spinningup.openai.com/en/latest/spinningup/rl_intro.html#deterministic-policies

pi_net = nn.Sequential(
	nn.Linear(obs_dim, 64),
	nn.Tanh(),
	nn.Linear(64, 64),
	nn.Tanh(),
	nn.Linear(64, act_dim)
)
```
This builds a multi-layer perceptron (MLP) network with two hidden layers of size 64 and `tanh` activation functions. If `obs` is an `ndarray` containing a batch of observations, `pi_net` can be used to obtain a batch of actions as follows:
```python
obs_tensor = torch.as_tensor(obs, dtype=torch.float32)
actions = pi_net(obs_tensor)
```

###### 3.1 b) Stochastic Policies
The two most common kinds of stochastic policies in deep RL are <mark style="background: #ADCCFFA6;">categorical policies</mark> and <mark style="background: #ADCCFFA6;">diagonal Gaussian policies</mark>.
1. [categorial](https://en.wikipedia.org/wiki/Categorical_distribution) policies can be used in **discrete action spaces**, 
2. diagonal [Gaussian](https://en.wikipedia.org/wiki/Multivariate_normal_distribution) policies can be used in **continuous actions spaces**

The employment and training of stochastic policies involve **two key computations**:
1. sampling actions from the policy,
2. computing $log$ likelihoods of particular actions, $\log\pi_\theta(a|s)$.

In the following linked pages, these computations are described for each of the kinds of stochastic policies: [[Categorical Policies]], [[Diagonal Gaussian Policies]]

