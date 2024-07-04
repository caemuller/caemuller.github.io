<script> MathJax = { tex: { inlineMath: [['$', '$'], ['\\(', '\\)']] } }; </script> <script type="text/javascript" id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"> </script> <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"> </script>

# GANs and other image generation Models
Please Download the presentation doing the entire derivation of Diffusion Models loss function, Original GANs loss function, Variational AutoEncoders and a quick introduction to Kullback-Leibler Divergence.

<a href="[https://raw.githubusercontent.com/caemuller/caemuller.github.io/Cae-diffusion-models.pdf](https://github.com/caemuller/caemuller.github.io/blob/main/Cae-diffusion-models.pdf)" </a>



# Distance Functions 😲


## nn.CosineSimilarity 

Returns the cosine similarity between $\mathbf{x}_1$ and $\mathbf{x}_2$, computed along a specified dimension.

Mathematically, cosine similarity is defined as:

$\[
\text{Cosine Similarity}(\mathbf{x}_1, \mathbf{x}_2) = \frac{\mathbf{x}_1 \cdot \mathbf{x}_2}{\|\mathbf{x}_1\| \|\mathbf{x}_2\|}
\]$

where $\cdot$ denotes the dot product and $\|\cdot\|$ denotes the Euclidean norm.

### Demonstration

Vector Cosine similarity can be displayed in this little html code snippet (i honeslty suck at HTML) to get the idea of how it works and perhaps show the main issue in this distance metric i.e it is aware of magnitude changes. So if a vector $v$ has the same angle of a vector $u$ even though $v$ has five times the magnitude of $u$ the similarity is maximal. you can play with it in the code below.

<iframe srcdoc="<html><head><style>body{font-family: Arial, sans-serif;}canvas{border:1px solid #000;width:400px;height:400px;margin-bottom:20px;}</style></head><body><div><label for='magnitude'>Magnitude:</label><input type='range' id='magnitude' min='0' max='200' value='100'></div><div><label for='angle'>Angle:</label><input type='range' id='angle' min='0' max='360' value='45'></div><canvas id='canvas'></canvas><div id='similarity'></div><script>const canvas=document.getElementById('canvas');const ctx=canvas.getContext('2d');const magnitudeInput=document.getElementById('magnitude');const angleInput=document.getElementById('angle');const similarityDisplay=document.getElementById('similarity');let baseVector={x:1,y:1};let varyingVector={x:1,y:1};let magnitude=100;function drawVectors(){ctx.clearRect(0,0,canvas.width,canvas.height);ctx.beginPath();ctx.moveTo(0,canvas.height/2);ctx.lineTo(canvas.width,canvas.height/2);ctx.stroke();ctx.beginPath();ctx.moveTo(canvas.width/2,0);ctx.lineTo(canvas.width/2,canvas.height);ctx.stroke();ctx.beginPath();ctx.moveTo(canvas.width/2,canvas.height/2);ctx.lineTo(canvas.width/2+baseVector.x*20,canvas.height/2-baseVector.y*20);ctx.strokeStyle='blue';ctx.stroke();ctx.beginPath();ctx.moveTo(canvas.width/2,canvas.height/2);ctx.lineTo(canvas.width/2+varyingVector.x*20,canvas.height/2-varyingVector.y*20);ctx.strokeStyle='red';ctx.stroke();const dotProduct=baseVector.x*varyingVector.x+baseVector.y*varyingVector.y;const magnitude1=Math.sqrt(baseVector.x**2+baseVector.y**2);const magnitude2=Math.sqrt(varyingVector.x**2+varyingVector.y**2);const cosineSimilarity=dotProduct/(magnitude1*magnitude2);similarityDisplay.textContent=`Cosine Similarity: ${cosineSimilarity.toFixed(2)}`;}function updateVector(){magnitude=parseFloat(magnitudeInput.value);const angle=parseFloat(angleInput.value);varyingVector.x=Math.cos(angle*Math.PI/180)*magnitude;varyingVector.y=Math.sin(angle*Math.PI/180)*magnitude;drawVectors();}magnitudeInput.addEventListener('input',updateVector);angleInput.addEventListener('input',updateVector);drawVectors();</script></body></html>" width="400" height="450"></iframe>


### Code example with pytorch
#### First of all import pytorch and some other libraries
```python
# import pytorch
import torch
import matplotlib.pyplot as plt
import numpy as np
```

```python
# test cosine similarity with torch
# create two vectors of size n with random numbers
n = 2
a = torch.randn(n)
b = torch.randn(n)
print(a)
print(b)
# calculate cosine similarity
cos = torch.nn.functional.cosine_similarity(a, b, dim=0)
print(cos)

#plot the vectors

plt.plot(a.numpy(), label='a', color='b')
plt.plot(b.numpy(), label='b', color='r')
plt.legend()
plt.savefig('cosine_similarity.png')
plt.show()
```

output:
```text
tensor([0.1961, 0.8413])
tensor([0.0160, 0.2070])
tensor(0.9885)
```
![Cosine similarity in random vectors](cosine_similarity.png)


testing the same code but with orthognalized vectors so that the output tends to zero
```python
# use gram-schmidt to orthogonalize the vectors
# create a matrix with the two vectors
A = torch.stack([a, b], dim=0)
print(A)

# orthogonalize the vectors
Q, R = torch.qr(A.T)
print(Q)
print(R)

# plot the vectors
plt.plot([0, Q[0, 0]], [0, Q[1, 0]], 'b', label='a')
plt.plot([0, Q[0, 1]], [0, Q[1, 1]], 'r', label='b')
plt.legend()
plt.savefig('orthogonal_vectors.png')

# calculate cosine similarity rounded to 5 decimal places
cos = torch.nn.functional.cosine_similarity(Q[:, 0], Q[:, 1], dim=0)
print(round(cos.item(), 5))
```

output:
```text
tensor([[0.1961, 0.8413],
        [0.0160, 0.2070]])
tensor([[-0.2270, -0.9739],
        [-0.9739,  0.2270]])
tensor([[-0.8638, -0.2052],
        [ 0.0000,  0.0314]])
0.0
```
![Cosine similarity in orthogonal vectors](orthogonal_vectors.png)

## nn.PairwiseDistance

Computes the pairwise distance between input vectors or between columns of input matrices.

Mathematically, pairwise distance is often computed using the Euclidean distance formula:

$$
\[
\text{Pairwise Distance}(\mathbf{x}_1, \mathbf{x}_2) = \sqrt{\sum_{i=1}^{n} (\mathbf{x}_{1i} - \mathbf{x}_{2i})^2} 
\]
$$

where $n$ is the dimensionality of the vectors $\mathbf{x}_1$ and $\mathbf{x}_2$, and $\mathbf{x}_{1i}$ and $\mathbf{x}_{2i}$ are the $i$-th components of $\mathbf{x}_1$ and $\mathbf{x}_2$, respectively.

### Demonstration

Pairwise distance can be visualized using this simple HTML code snippet It helps demonstrate a key issue with this distance metric: it only considers the spatial separation between points, disregarding any differences in magnitude. For example, if one point has five times the magnitude of another but the same angle, the distance between them remains the same. You can interact with the code below to explore this concept further 😡.

<iframe srcdoc="<html><head><style>body{font-family: Arial, sans-serif;}canvas{border:1px solid #000;width:400px;height:400px;margin-bottom:20px;}</style></head><body><div><label for='x1'>Point 1 - X Coordinate:</label><input type='number' id='x1' value='1'><label for='y1'>Y Coordinate:</label><input type='number' id='y1' value='1'></div><div><label for='x2'>Point 2 - X Coordinate:</label><input type='number' id='x2' value='2'><label for='y2'>Y Coordinate:</label><input type='number' id='y2' value='2'></div><canvas id='canvas'></canvas><div id='distance'></div><script>const canvas=document.getElementById('canvas');const ctx=canvas.getContext('2d');const x1Input=document.getElementById('x1');const y1Input=document.getElementById('y1');const x2Input=document.getElementById('x2');const y2Input=document.getElementById('y2');const distanceDisplay=document.getElementById('distance');let point1={x:parseFloat(x1Input.value),y:parseFloat(y1Input.value)};let point2={x:parseFloat(x2Input.value),y:parseFloat(y2Input.value)};function drawPoints(){ctx.clearRect(0,0,canvas.width,canvas.height);ctx.beginPath();ctx.arc(point1.x*20+canvas.width/2,-point1.y*20+canvas.height/2,5,0,Math.PI*2);ctx.fillStyle='blue';ctx.fill();ctx.beginPath();ctx.arc(point2.x*20+canvas.width/2,-point2.y*20+canvas.height/2,5,0,Math.PI*2);ctx.fillStyle='red';ctx.fill();ctx.beginPath();ctx.moveTo(point1.x*20+canvas.width/2,-point1.y*20+canvas.height/2);ctx.lineTo(point2.x*20+canvas.width/2,-point2.y*20+canvas.height/2);ctx.strokeStyle='black';ctx.stroke();const distance=Math.sqrt((point2.x-point1.x)**2+(point2.y-point1.y)**2);distanceDisplay.textContent=`Distance: ${distance.toFixed(2)}`;}function updatePoints(){point1.x=parseFloat(x1Input.value);point1.y=parseFloat(y1Input.value);point2.x=parseFloat(x2Input.value);point2.y=parseFloat(y2Input.value);drawPoints();}x1Input.addEventListener('input',updatePoints);y1Input.addEventListener('input',updatePoints);x2Input.addEventListener('input',updatePoints);y2Input.addEventListener('input',updatePoints);drawPoints();</script></body></html>" width="400" height="450"></iframe>

### Code example with pytorch
#### import pytorch and some other libraries
```python
# import pytorch
import torch
import matplotlib.pyplot as plt
import numpy as np
```

```python
# test pair-wise similarity with torch
# create two vectors of size n with random numbers

n = 2
a = torch.randn(n)
b = torch.randn(n)

# create a matrix with the two vectors
A = torch.stack([a, b], dim=0)
print(A)

# calculate pair-wise cosine similarity
cos = torch.nn.functional.pairwise_distance(A, A, p=2)
print(cos)

# plot the vectors
plt.plot(a.numpy(), label='a', color='b')
plt.plot(b.numpy(), label='b', color='r')
plt.legend()
plt.savefig('pairwise_similarity.png')
plt.show()
```

output:
```text
tensor([[-0.8835, -0.9965],
        [-1.2604,  1.7584]])
tensor([1.4142e-06, 1.4142e-06])
```


![pair-wise similarity in random vectors](pairwise_similarity.png)


## References
[Pythorch](https://pytorch.org/docs/stable/nn.html)

[Deep NLP](http://www.deepnlp.org/blog/probability-distribution-formulas)
