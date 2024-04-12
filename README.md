## nn.L1Loss

Creates a criterion that measures the mean absolute error (MAE) between each element in the input $\mathbf{x}$ and target $\mathbf{y}$.

**Formula (LaTeX):**
$ \text{L1Loss}(\mathbf{x}, \mathbf{y}) = \frac{1}{n} \sum_{i=1}^{n} |x_i - y_i| $

**PyTorch Command:**
```python
loss_function = nn.L1Loss()
```

---

## nn.PoissonNLLLoss

Negative log likelihood loss with Poisson distribution of target.

**Formula (LaTeX):**
Not available.

**PyTorch Command:**
```python
loss_function = nn.PoissonNLLLoss()
```

---

## nn.GaussianNLLLoss

Gaussian negative log likelihood loss.

**Formula (LaTeX):**
Not available.

**PyTorch Command:**
```python
loss_function = nn.GaussianNLLLoss()
```

---

## nn.KLDivLoss

The Kullback-Leibler divergence loss.

**Formula (LaTeX):**
Not available.

**PyTorch Command:**
```python
loss_function = nn.KLDivLoss()
```

---

## nn.BCELoss

Creates a criterion that measures the Binary Cross Entropy between the target and the input probabilities:

**Formula (LaTeX):**
Not available.

**PyTorch Command:**
```python
loss_function = nn.BCELoss()
```

---

## nn.BCEWithLogitsLoss

This loss combines a Sigmoid layer and the BCELoss in one single class.

**Formula (LaTeX):**
Not available.

**PyTorch Command:**
```python
loss_function = nn.BCEWithLogitsLoss()
```

---

## nn.MarginRankingLoss

Creates a criterion that measures the loss given inputs $\mathbf{x_1}$, $\mathbf{x_2}$, two 1D mini-batch or 0D Tensors, and a label 1D mini-batch or 0D Tensor $\mathbf{y}$ (containing 1 or -1).

**Formula (LaTeX):**
Not available.

**PyTorch Command:**
```python
loss_function = nn.MarginRankingLoss()
```

---

## nn.HingeEmbeddingLoss

Measures the loss given an input tensor $\mathbf{x}$ and a labels tensor $\mathbf{y}$ (containing 1 or -1).

**Formula (LaTeX):**
Not available.

**PyTorch Command:**
```python
loss_function = nn.HingeEmbeddingLoss()
```

---

## nn.MultiLabelMarginLoss

Creates a criterion that optimizes a multi-class multi-classification hinge loss (margin-based loss) between input $\mathbf{x}$ (a 2D mini-batch Tensor) and output $\mathbf{y}$ (which is a 2D Tensor of target class indices).

**Formula (LaTeX):**
Not available.

**PyTorch Command:**
```python
loss_function = nn.MultiLabelMarginLoss()
```

---

## nn.HuberLoss

Creates a criterion that uses a squared term if the absolute element-wise error falls below delta and a delta-scaled L1 term otherwise.

**Formula (LaTeX):**
Not available.

**PyTorch Command:**
```python
loss_function = nn.HuberLoss()
```

---

## nn.SmoothL1Loss

Creates a criterion that uses a squared term if the absolute element-wise error falls below beta and an L1 term otherwise.

**Formula (LaTeX):**
Not available.

**PyTorch Command:**
```python
loss_function = nn.SmoothL1Loss()
```

---

## nn.SoftMarginLoss

Creates a criterion that optimizes a two-class classification logistic loss between input tensor $\mathbf{x}$ and target tensor $\mathbf{y}$ (containing 1 or -1).

**Formula (LaTeX):**
Not available.

**PyTorch Command:**
```python
loss_function = nn.SoftMarginLoss()
```

---

## nn.MultiLabelSoftMarginLoss

Creates a criterion that optimizes a multi-label one-versus-all loss based on max-entropy, between input $\mathbf{x}$ and target $\mathbf{y}$ of size $(N,C)$.

**Formula (LaTeX):**
Not available.

**PyTorch Command:**
```python
loss_function = nn.MultiLabelSoftMarginLoss()
```

---

## nn.CosineEmbeddingLoss

Creates a criterion that measures the loss given input tensors $\mathbf{x_1}$, $\mathbf{x_2}$ and a Tensor label $\mathbf{y}$ with values 1 or -1.

**Formula (LaTeX):**
Not available.

**PyTorch Command:**
```python
loss_function = nn.CosineEmbeddingLoss()
```

---

## nn.MultiMarginLoss

Creates a criterion that optimizes a multi-class classification hinge loss (margin-based loss) between input $\mathbf{x}$ (a 2D mini-batch Tensor) and output $\mathbf{y}$ (which is a 1D tensor of target class indices, $0 ≤ y ≤ x.size(1)−1$).

**Formula (LaTeX):**
Not available.

**PyTorch Command:**
```python
loss_function = nn.MultiMarginLoss()
```

---

## nn.TripletMarginLoss

Creates a criterion that measures the triplet loss given an input tensors $\mathbf{x_1}$, $\mathbf{x_2}$, $\mathbf{x_3}$ and a margin with a value greater than $0$.

**Formula (LaTeX):**
Not available.

**PyTorch Command:**
```python
loss_function = nn.TripletMarginLoss()
```

---

## nn.TripletMarginWithDistanceLoss

Creates a criterion that measures the triplet loss given input tensors $\mathbf{a}$, $\mathbf{p}$, and $\mathbf{n}$ (representing anchor, positive, and negative examples, respectively), and a nonnegative, real-valued function ("distance function") used to compute the relationship between the anchor and positive example ("positive distance") and the anchor and negative example ("negative distance").

**Formula (LaTeX):**
Not available.

**PyTorch Command:**
```python
loss_function = nn.TripletMarginWithDistanceLoss()
```

