## Dropout Layers

### Introduction

Dropout is a regularization technique used in neural networks to prevent overfitting by randomly dropping out (i.e., setting to zero) a proportion of input units during training. This prevents units from co-adapting too much to each other and encourages robust representations to emerge.

### Original Paper

Srivastava et al. introduced dropout in their paper titled ["Dropout: A Simple Way to Prevent Neural Networks from Overfitting"](http://www.jmlr.org/papers/volume15/srivastava14a/srivastava14a.pdf), published in the *Journal of Machine Learning Research* in 2014.

### Dropout layers overview

Dropout is implemented as a layer in neural networks, typically applied after fully connected layers or convolutional layers. The key idea is to randomly deactivate a fraction of neurons during each training iteration. This is done by multiplying the activations of the neurons by a binary mask, where each element of the mask is set to either 0 or 1 with a specified probability.

#### Dropout Procedure

1. **During Training**: 
   - For each training example, a binary mask is sampled from a Bernoulli distribution with a given probability:
<img src="https://render.githubusercontent.com/render/math?math=f(k;p)%20=%20%0A%20%20%20%20%5Cbegin%7Bcases%7D%0A%20%20%20%20%20%20p%20%20%20%20%20%20%26%20%5Ctext%7Bif%20%7D%20k%20%3D%201%2C%20%5C%5C%0A%20%20%20%20%20%201%20-%20p%20%26%20%5Ctext%7Bif%20%7D%20k%20%3D%200.%0A%20%20%20%20%5Cend%7Bcases%7D">


     
   - The binary mask is multiplied element-wise with the activations of the neurons in the layer.
   - The result is passed to the next layer for further processing.

2. **During Testing**:
   - No dropout is applied during testing. Instead, the activations are scaled by \( (1 - p) \) to compensate for the dropout applied during training. This ensures that the expected output remains approximately the same during training and testing.

#### Benefits of Dropout

- **Regularization**: Dropout acts as a form of regularization by preventing overfitting. It discourages complex co-adaptations of neurons, forcing the network to learn more robust features.
  
- **Ensemble Learning**: Dropout can be interpreted as training multiple models with shared parameters. Each sampled binary mask corresponds to a different subnetwork, and averaging their predictions during testing resembles ensemble learning.

- **Efficient Training**: Dropout can speed up training by effectively sampling from an exponential number of different network architectures, thereby reducing the risk of getting stuck in local minima.

### Dropout Layers in Pytorch


# References
[Pythorch Dropout layers](https://pytorch.org/docs/stable/nn.html#dropout-layers)
[Deep NLP](http://www.deepnlp.org/blog/probability-distribution-formulas)
