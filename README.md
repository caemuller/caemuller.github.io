### Distance Functions

#### nn.CosineSimilarity

Returns the cosine similarity between $\mathbf{x}_1$ and $\mathbf{x}_2$, computed along a specified dimension.

Mathematically, cosine similarity is defined as:

$\[
\text{Cosine Similarity}(\mathbf{x}_1, \mathbf{x}_2) = \frac{\mathbf{x}_1 \cdot \mathbf{x}_2}{\|\mathbf{x}_1\| \|\mathbf{x}_2\|}
\]$

where $\cdot$ denotes the dot product and $\|\cdot\|$ denotes the Euclidean norm.

## demonstration

Vector Cosine similarity can be displayed in this little html code snippet (i honeslty suck at HTML) to get the idea of how it works and perhaps show the main issue in this distance metric i.e it is aware of magnitude changes. So if a vector $v$ has the same angle of a vector $u$ even though $v$ has five times the magnitude of $u$ the similarity is maximal. you can play with it in the code below. (I honestly hope so)

<iframe srcdoc="<html><head><style>body{font-family: Arial, sans-serif;}canvas{border:1px solid #000;width:400px;height:400px;margin-bottom:20px;}</style></head><body><div><label for='magnitude'>Magnitude:</label><input type='range' id='magnitude' min='0' max='200' value='100'></div><div><label for='angle'>Angle:</label><input type='range' id='angle' min='0' max='360' value='45'></div><canvas id='canvas'></canvas><div id='similarity'></div><script>const canvas=document.getElementById('canvas');const ctx=canvas.getContext('2d');const magnitudeInput=document.getElementById('magnitude');const angleInput=document.getElementById('angle');const similarityDisplay=document.getElementById('similarity');let baseVector={x:1,y:1};let varyingVector={x:1,y:1};let magnitude=100;function drawVectors(){ctx.clearRect(0,0,canvas.width,canvas.height);ctx.beginPath();ctx.moveTo(0,canvas.height/2);ctx.lineTo(canvas.width,canvas.height/2);ctx.stroke();ctx.beginPath();ctx.moveTo(canvas.width/2,0);ctx.lineTo(canvas.width/2,canvas.height);ctx.stroke();ctx.beginPath();ctx.moveTo(canvas.width/2,canvas.height/2);ctx.lineTo(canvas.width/2+baseVector.x*20,canvas.height/2-baseVector.y*20);ctx.strokeStyle='blue';ctx.stroke();ctx.beginPath();ctx.moveTo(canvas.width/2,canvas.height/2);ctx.lineTo(canvas.width/2+varyingVector.x*20,canvas.height/2-varyingVector.y*20);ctx.strokeStyle='red';ctx.stroke();const dotProduct=baseVector.x*varyingVector.x+baseVector.y*varyingVector.y;const magnitude1=Math.sqrt(baseVector.x**2+baseVector.y**2);const magnitude2=Math.sqrt(varyingVector.x**2+varyingVector.y**2);const cosineSimilarity=dotProduct/(magnitude1*magnitude2);similarityDisplay.textContent=`Cosine Similarity: ${cosineSimilarity.toFixed(2)}`;}function updateVector(){magnitude=parseFloat(magnitudeInput.value);const angle=parseFloat(angleInput.value);varyingVector.x=Math.cos(angle*Math.PI/180)*magnitude;varyingVector.y=Math.sin(angle*Math.PI/180)*magnitude;drawVectors();}magnitudeInput.addEventListener('input',updateVector);angleInput.addEventListener('input',updateVector);drawVectors();</script></body></html>" width="400" height="450"></iframe>


#### nn.PairwiseDistance

Computes the pairwise distance between input vectors or between columns of input matrices.

Mathematically, pairwise distance is often computed using the Euclidean distance formula:

$\[
\text{Pairwise Distance}(\mathbf{x}_1, \mathbf{x}_2) = \sqrt{\sum_{i=1}^{n} (\mathbf{x}_{1i} - \mathbf{x}_{2i})^2}
\]$

where $n$ is the dimensionality of the vectors $\mathbf{x}_1$ and $\mathbf{x}_2$, and $\mathbf{x}_{1i}$ and $\mathbf{x}_{2i}$ are the $i$-th components of $\mathbf{x}_1$ and $\mathbf{x}_2$, respectively.

# References
[Pythorch](https://pytorch.org/docs/stable/nn.html)

[Deep NLP](http://www.deepnlp.org/blog/probability-distribution-formulas)
