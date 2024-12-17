#rl 

> [!warning]  Disclaimer
> Contents of this file are references from the nicely curated resource by OpenAI: Spinning Up in Deep RL https://spinningup.openai.com/en/latest/user/introduction.html

> [!note] Definition
> A multivariate Gaussian distribution (multivariate normal distribution) is described by a mean vector, $\mu$, and a covariance matrix, $\Sigma$. 
> - Covariance matrix $\Sigma$: A square matrix giving the covariance between each pair of elements of a given random vector, e.g.:
> $${\displaystyle {\begin{bmatrix}1&0.5\\0.5&1\end{bmatrix}}}$$
> 
> A diagonal Gaussian distribution is a **special case** where the covariance matrix only has entries on the diagonal. As a result, we can represent it by a vector.

A diagonal Gaussian policy always has a neural network that maps from observations to mean actions:
$$\mu_\theta(s) = f_\theta(s),$$
where $f$ denotes the neural network that maps from observation $s \in \mathbb{R}^n$ to $\mu\in\mathbb{R}^m$.
