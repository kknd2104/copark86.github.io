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



In case 3d points(structure) <div>$\textbf{p}_i$</div> are marginalized out as follows, <div>$\textbf{p}_i$</div> are triangulated to calculate residual $\textbf{e}$.

<div>$$\textbf{e} = \textbf{z}_{ij} - \pi(\textbf{T}_j\textbf{p}_i)$$</div>

where <div>$\textbf{T}_j\in SE(3), \textbf{p}_i\in R^3$</div> are the states we want to estimate and <div>$\textbf{z}_{ij}$</div> is the observed feature in $R^2$.

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

Here my question arises. If we can calculate 3d points $\textbf{p}_i$ by the triangulation, only $\textbf{T}_j$ are the state variable to be estimated. 

Then, why are we bothered to calculate marginalization related terms <div>$-\textbf{H}_{cs}{\textbf{H}_{ss}}^{-1}\textbf{H}_{sc}$ and $-\textbf{H}_{cs}{\textbf{H}_{ss}}^{-1}\textbf{g}_{s}$</div> instead of optimizing only poses by ${\textbf{H}}_{cc}\mathbf{\xi}_c ={\textbf{g}}_{c}$ (note that H and g are without bar).

I guess  <div>${\textbf{H}}_{cc}\mathbf{\xi}_c ={\textbf{g}}_{c}$</div> is enough to find the optimal poses $\textbf{T}_j$.

So, my question was why do we use <div>$\bar{\textbf{H}}_{cc}\mathbf{\xi}_c =\bar{\textbf{g}}_{c}$</div> instead of ${\textbf{H}}_{cc}\mathbf{\xi}_c ={\textbf{g}}_{c}$?

Answer is simple. 
