---
title: 'Latex Note'
date: 2018-04-22
permalink: /post/2018-04-22-LatexNote
tags:
  - latex
---
Latex note 

<div></div>
Upper & underbrace
-------------------------------

	\usepackage{amsmath}
	
	z = \overbrace{
	\underbrace{x}_\text{real} +
	\underbrace{iy}_\text{imaginary}
	}^\text{complex number}
  
<div>$z = \overbrace{\underbrace{x}_\text{real} +\underbrace{iy}_\text{imaginary}}^\text{complex number}$</div>


Parentheses
-------------------------------
    \Biggl(\biggl(\Bigl(\bigl((x)\bigr)\Bigr)\biggr)\Biggr)
	
<div>$\Biggl(\biggl(\Bigl(\bigl((x)\bigr)\Bigr)\biggr)\Biggr)$</div>

Markdown
-------------------------------
    $\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$


<div>$\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$</div>

    $$\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$$
 
<div>$$\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$$</div>
