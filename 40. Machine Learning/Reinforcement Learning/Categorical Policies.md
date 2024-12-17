#rl 

> [!warning]  Disclaimer
> Contents of this file are references from the nicely curated resource by OpenAI: Spinning Up in Deep RL https://spinningup.openai.com/en/latest/user/introduction.html

> [!tip]
> A categorical policy is like a classifier over discrete actions.

###### Creating the Categorical Policy
 You build the neural network for a categorical policy the same way you would for a classifier:
 1. the input is the observation, followed by
 2. some number of layers (possibly convolutional or densely-connected, depending on the kind of input), followed by
 3. a final linear layer that gives you logits for each actions, followed by
 4. a softmax activation layer to convert the logits into probabilities

###### (1) Sampling the Actions from the Policy
Given the probabilities for each action, frameworks like PyTorch and TensorFlow have built-in tools for sampling. For example: [Categorical distributions in PyTorch](https://pytorch.org/docs/stable/distributions.html#categorical), [torch.multinomial](https://pytorch.org/docs/stable/torch.html#torch.multinomial), [tf.distributions.Categorical](https://www.tensorflow.org/versions/r1.15/api_docs/python/tf/distributions/Categorical), or [tf.multinomial](https://www.tensorflow.org/versions/r1.15/api_docs/python/tf/random/multinomial).

###### (2) Log-Likelihood
Denote the last layer of probabilities as: $$P_\theta(s)$$It is a vector with however many entries as there are actions, so we can treat the actions as indices for the vector. The $log$ likelihood for an action $a$ can then be obtained by indexing into the vector:
$$\log\pi_\theta(a|s)=\log[P_\theta(s)]_a$$

