#apuntes #mates #howto 
___
> [!info] Para ver como se aplica esta formula a código consulta [[Distancia más corta de un punto a un segmento en código]]

Let's go through the **step-by-step derivation** of the formula to compute the **shortest distance from a point $c$** to a **line segment $ab$**, starting from only the coordinates:
- Point $c=(c_{x},c_{y})$
- Segment endpoint $a=(a_{x},a_{y})$ and $b=(b_{x},b_{y})$

## Step 1: Represent Vectors

Start by constructing vectors from the given points:

- **Vector from $a$ to $b$:**$$\vec{ab} =(b_{x}−a_{x},b_{y}−a_{y})$$
- **Vector from $a$ to $c$:**  $$\vec{ac} =(c_{x}−a_{x},c_{y}−a_{y})$$
## Step 2: Project $\vec{ac}$  onto $\vec{ab}$

We want to project the vector $\vec{ac}$  onto $\vec{ab}$. This tells us **how far along the segment** the perpendicular projection of $c$ lies.

### Scalar projection (dot product):
$$t=\frac{\vec{ac} \cdot \vec{ab}}{|\vec{ab}^{2}|}​ = \frac{(c_{x}-a_{x})(b_{x}-a_{x})+(c_{y}-a_{y})(b_{y}-a_{y})}{(b_{x}-a_{x})^2+(b_{y}-a_{y})^2}$$
This scalar $t$ tells us:
- **If t<0:** the projection is **before** point $a$
- **If 0≤t≤1:** the projection lies **on the segment**
- **If t>1:** the projection is **after** point $b$

## Step 3: Determine the Closest Point

Now we use the value of $t$ to determine the **closest point $p$** on the segment to $c$:

- If $0≤t≤1$ , then the closest point is the **projection** on the segment: $p_{x}=a_{x}+t(b_{x}-a_{x})$  , $p_{y}=a_{y}+t(b_{y}-a_{y})$
- If $t<0,$ then the closest point is just point $a$
- If $t>1$, then the closest point is point $b$

## Step 4: Compute the Distance

Finally, compute the Euclidean distance between point $c=(c_{x},c_{y})$ and the closest point $p=(px,py)$:$$d=\sqrt{(c_{x} - p_{x})^2 + (c_{y} - p_{y})^2}$$
## Final Combined Formula:
Let:

$$t=\frac{(c_x - a_x)(b_x - a_x) + (c_y - a_y)(b_y - a_y)}{(b_x - a_x)^2 + (b_y - a_y)^2}$$

Then:

$$d= \begin{cases} \sqrt{(c_x - (a_x + t(b_x - a_x)))^2 + (c_y - (a_y + t(b_y - a_y)))^2}, & \text{if } 0 \le t \le 1 \\ \sqrt{(c_x - a_x)^2 + (c_y - a_y)^2}, & \text{if } t < 0 \\ \sqrt{(c_x - b_x)^2 + (c_y - b_y)^2}, & \text{if } t > 1 \end{cases}$$

