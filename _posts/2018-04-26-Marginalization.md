---
title: 'Why do we need marginalization in BA?'
date: 2018-04-26
permalink: /post/2018-04-04-marginalization
tags:
  - Marginalization
  - Bundle Adjustment
  - Structureless approach 
---

A common practice in Bundle Adjustment is to reduce the state dimension by marginalizing structure or pose states to improve the optimization speed.



In case 3d points(structure) <span>$\textbf{p}\_i$</span> are marginalized out as follows, <span>$\textbf{p}_i$</span> are triangulated to calculate residual $\textbf{e}$.

<div>$$\textbf{e} = \textbf{z}_{ij} - \pi(\textbf{T}_j\textbf{p}_i)$$</div>

where <span>$\textbf{T}_j\in SE(3), \textbf{p}_i\in R^3$</span> are the states we want to estimate and <span>$\textbf{z}_{ij}$</span> is the observed feature in $R^2$.

And just optimize the pose related terms only.

<div>$$\begin{bmatrix}
 \textbf{H}_{cc}& \textbf{H}_{cs} \\ 
\textbf{H}_{sc} & \textbf{H}_{ss} 
\end{bmatrix}
\begin{bmatrix}
 \mathbf{\xi}_c \\ 
\textbf{p}_s 
\end{bmatrix}=
\begin{bmatrix}
 \textbf{g}_{c} \\ 
\textbf{g}_{s}  
\end{bmatrix}$$</div>



<div>$$\bar{\textbf{H}}_{cc}=\textbf{H}_{cc}-\textbf{H}_{cs}{\textbf{H}_{ss}}^{-1}\textbf{H}_{sc}$$</div>

<div>$$\bar{\textbf{g}}_{c}=\textbf{g}_{c}-\textbf{H}_{cs}{\textbf{H}_{ss}}^{-1}\textbf{g}_{s}$$</div>

<div>$$\bar{\textbf{H}}_{cc}\mathbf{\xi}_c =\bar{\textbf{g}}_{c}$$</div>

Here my question arises. If we can calculate 3d points <span>$\textbf{p}_i$ by the triangulation, only $\textbf{T}_j$</span> are the state variable to be estimated. 

Then, why are we bothered to calculate marginalization related terms <span>$-\textbf{H}\_{cs}{\textbf{H}\_{ss}}^{-1}\textbf{H}\_{sc}$</span> and <span>$-\textbf{H}\_{cs}{\textbf{H}\_{ss}}^{-1}\textbf{g}\_{s}$</span> instead of optimizing only poses by <span>${\textbf{H}}\_{cc}\mathbf{\xi}\_c ={\textbf{g}}\_{c}$</span> (note that H and g are without bar).

I guess  <span>${\textbf{H}}\_{cc}\mathbf{\xi}\_c ={\textbf{g}}\_{c}$</span> is enough to find the optimal poses <span>$\textbf{T}\_j$</span>.

So, my question was why do we use <span>$\bar{\textbf{H}}\_{cc}\mathbf{\xi}\_c =\bar{\textbf{g}}\_{c}$</span> instead of <span>${\textbf{H}}\_{cc}\mathbf{\xi}\_c ={\textbf{g}}\_{c}$</span>?

Answer is simple. 

Let's have a look at the Hessian H of simulated BA.
![1](http://copark86.github.io/images/Hessian.jpg)

Yello represents non zero element and upper 60 by 60 matrix represent <span>${\textbf{H}}\_{cc}$</span>. When a structure is observed over multiple poses, Hessian make correlation terms.

![2](http://copark86.github.io/images/Marginalization.jpg)

Obiously, <span>${\textbf{H}}\_{cc}\mathbf{\xi}\_c ={\textbf{g}}\_{c}$</span> ignores the correlation terms. Therefore, each poses loose information of linkage, whereas in <span>$\bar{\textbf{H}}\_{cc}\mathbf{\xi}\_c =\bar{\textbf{g}}\_{c}$</span> off diagonal terms are added to Hessian which represents the rumped relationship miginalized from <span>$-\textbf{H}\_{cs}{\textbf{H}\_{ss}}^{-1}\textbf{H}\_{sc}$</span>.

The benefit are faster convergence and low final error in optimization. 



