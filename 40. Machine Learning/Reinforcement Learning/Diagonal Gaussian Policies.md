#rl 

> [!warning]  Disclaimer
> Contents of this file are references from the nicely curated resource by OpenAI: Spinning Up in Deep RL https://spinningup.openai.com/en/latest/user/introduction.html

> [!note] Prelude
> A multivariate Gaussian distribution (multivariate normal distribution) is described by a mean vector, $\mu$, and a covariance matrix, $\Sigma$. 
> - Covariance matrix $\Sigma$: A square matrix giving the covariance between each pair of elements of a given random vector, e.g.:
> $${\displaystyle {\begin{bmatrix}1&0.5\\0.5&1\end{bmatrix}}}$$

> [!note] Definition
>  A diagonal Gaussian distribution is a **special case** where the covariance matrix only has entries on the diagonal. As a result, we can represent it by a vector.

#### Implementing Diagonal Gaussion Policies
---
##### 1. Representing the Mean Actions Vector $\mu$
A diagonal Gaussian policy always has a neural network that maps from observations to mean actions:
$$\mu_\theta(s) = f_\theta(s),$$
where $f$ denotes the neural network that maps from observation, $s \in \mathbb{R}^n$ to mean actions, $\mu\in\mathbb{R}^m$.
##### 2. Representing the Covariance Matric $\Sigma$
There are <mark style="background: #ABF7F7A6;">two ways</mark> in which the covariance matrix for a diagonal gaussian policy is typically represented:
1. The first way involves using single vector to represent log standard deviations, $\log\sigma$. In this case, $\log\sigma$ are standalone parameters. <mark style="background: #ABF7F7A6;">They are not a function of state</mark>. 
$$Σ = diag(σ₁², σ₂², ..., σₙ²)$$
2. The second way is to use a <mark style="background: #ABF7F7A6;">neural network</mark> that maps from states to log standard deviations: $$\log\sigma_\theta(s)=f_\theta(s),$$where $f$ denotes the neural network that maps states, $s \in \mathbb{R}^n$ to log standard deviations, $\log|\sigma\in\mathbb{R}^m|$.

> [!tip] 
> Note that in both cases we output **log standard deviations** $\log\sigma$ instead of standard deviations $\sigma$ (, or also variances $\sigma^2$ for that matter).
> 
> The reason is that:
> 1. It makes it easier for us to compute the sampling equation in the next step,
> 2. Using logarithmic values ensures better numerical stability, removing the need to enforce non-negativity contraints during training:
> 	- $\log\sigma$ can take on any real value $(-\infty,\infty)$, while
> 	- $\sigma$ must be non-negative.
##### 3. Bringing everything together - Action Sampling
Given the mean action $\mu_\theta(s)$ and standard deviation $\sigma_\theta(s)$ *(the gaussian distribution component)*, and a vector $z$ of noise from a spherical Gaussian $(z \sim \mathcal{N}(0, I))$, an action sample can be computed with:
$$a=\mu_\theta(s)+\sigma_\theta(s)\odot z,$$
where $\odot$ denotes the element-wise product of two vectors.
###### To Generate Noise...
Standard frameworks have built-in ways to generate the noise vectors, such as `torch.normal` or `tf.random_normal`. Alternatively, using distribution objects like `torch.distributions.Normal` or `tf.distributions.Normal` can be advantageous in the sense that you can also directly calculate log-likelihoods with them. 
###### _huh?_... 
> [!error] Math for Dummies like me 
> $(z \sim \mathcal{N}(0, I))$: 
> - "$z$ is sampled from a multivariate normal distribution $\mathcal{N}$, 
> - with $\mu=0$ and Covariance Matrix $= I$, 
> - where $I$ denotes the Identity Matrix.
> - Implying that all dimensions have variance, $\sigma^2 = 1$,
> - and there is no correlation between the dimensions (diagonal matrix)"
> ![[Diagonal Gaussian Policies-20241220194410700.png|435]]

##### A1. Computing the Likelihood
The log-likehood of a $k$-dimensional action $a$, for a diagonal Gaussian with mean $\mu=\mu_\theta(s)$ and standard deviation $\sigma=\sigma_\theta(s)$, is given by
$$\log\pi_\theta(a|s)=-{1\over2}\left(\sum\limits_{i=1}^{k}\left({\left(a_i-\mu_i\right)^2\over \sigma_i^2}+2\log\sigma_i\right)+k\log2\pi\right).$$
Note that we do not need to compute the log-likehood when simply sampling actions from a diagonal gaussian policy. In practical implementations like PPO, the actual steps only involve the retrieval of $\mu$ and $\sigma$ from the policy network, the action sampling, and finally the application of the sampled action.

*(Claude 3.5 Sonnet) The log-likelihood formula is mainly used:*
- When you want to analytically compute the likelihood of an action to be sampled
- For the sake of theoretically deriving the algorithm
- When you need to compute specific policy gradient terms

#### Intuitively Understanding Diagonal Gaussian Distributions
##### Diagonal Covariance = Only Variances $\sigma^2$
![[Diagonal Gaussian Policies-20241220185100885.png|601]]