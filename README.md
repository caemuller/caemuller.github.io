### Distance Functions

#### nn.CosineSimilarity

Returns the cosine similarity between $\mathbf{x}_1$ and $\mathbf{x}_2$, computed along a specified dimension.

Mathematically, cosine similarity is defined as:

\[
\text{Cosine Similarity}(\mathbf{x}_1, \mathbf{x}_2) = \frac{\mathbf{x}_1 \cdot \mathbf{x}_2}{\|\mathbf{x}_1\| \|\mathbf{x}_2\|}
\]

where $\cdot$ denotes the dot product and $\|\cdot\|$ denotes the Euclidean norm.

#### nn.PairwiseDistance

Computes the pairwise distance between input vectors or between columns of input matrices.

Mathematically, pairwise distance is often computed using the Euclidean distance formula:

\[
\text{Pairwise Distance}(\mathbf{x}_1, \mathbf{x}_2) = \sqrt{\sum_{i=1}^{n} (\mathbf{x}_{1i} - \mathbf{x}_{2i})^2}
\]

where $n$ is the dimensionality of the vectors $\mathbf{x}_1$ and $\mathbf{x}_2$, and $\mathbf{x}_{1i}$ and $\mathbf{x}_{2i}$ are the $i$-th components of $\mathbf{x}_1$ and $\mathbf{x}_2$, respectively.

# References
[Pythorch](https://pytorch.org/docs/stable/nn.html)

[Deep NLP](http://www.deepnlp.org/blog/probability-distribution-formulas)
