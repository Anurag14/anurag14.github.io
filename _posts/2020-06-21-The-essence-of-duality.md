---
layout: post
title: "The essence of duality - from the perspecpetive of linear programming"
date: 2020-06-21
---

Primal dual relationships are often the heart of ideas in optimization and in applications of linear algebra. From advanced lagrangian duals to linear programming methods - all of them draw inspiration from the simple idea of duality.

Often the idea is quite misunderstood. The underlying simplicity is marred by complex notation and rigor. You are likely to get introduced to primal dual relationship in linear programming as following in most of textbooks.
<p align="center">
<img src="https://anurag14.github.io/blog_resources/2020-06-21/primal-and-dual-problem-16-638.jpg" width="300" height="300" />
</p>
<p align ="center">
Fig1: Primal and dual of a linear programming problem
</p>


There is a more condensed representation of the above for using linear algebra and matrix notation. However, it still doesnt throw any light onto the essence and motivation behind the primal and dual relationshiip.
<p align="center">
<img src="https://anurag14.github.io/blog_resources/2020-06-21/matrix-primal-dual.png" width="300" height="50" /> 
</p>
<p align ="center">
Fig2: The condensed matrix notation
</p>

After giving the primal and dual relationship in linear programming a read, I decided to take a bite at explaining it. I hope this interpretation of duality will allow you to get more intuitive understanding of it. Hopefully, helping the reader on their quest to applying this first principle whenever they encounter duality in much more complex and advance scenarios. Comments from the learned community and those who are much familiar with the topic are genuinely appreciated!

Okay. Firstly lets brush how a typical linear programming problem looks like:

## Linear Programming Review 

Lets suppose, that in this lockdown you want to catch up on your all previous guilty pleasures and hobbies. In turn you maximize the happiness and joy that you get out of all the activities. However, certain physical restrictions may still apply! For example may not be able to continue a activity or combination of certain for longer hours because you still dont have sufficient time or the activities can be exhausting. Given these realistic constraints, we want to maximize happiness can you achieve. This can be formulated as an linear programming problem! 

To not make example complex, lets say you like to do 2 activities dancing and painting.  
Let the number of hours you paint and dance in a day be is _x1_ and _x2_.   
Lets say the happiness is some function of these two activities _H(x<sub>1</sub>, x<sub>2</sub>) = 6x1+5x2_.   
The happiness is maximized subject to some constraints.  
If you cannot give more than 5 hours a day to any leisure translates to, _x1 + x2 <= 5_ 
Given the rate of energy each activity consumes and you cannot spend more than 12 units of energy translates to _3x1 + 4x2 <= 12_    
Since you cannot do any activity for negative hours both _x1, x2_ have to be non negative  _x1, x2 >= 0_ 

then the typical Linear program can look like:  
<p align="center">
  <em><strong>maximize</strong>&emsp; H(x<sub>1</sub>, x<sub>2</sub>) = 6x1 + 5x2</em> <br>
  <em>subject to:&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;</em><br>
  <em>&emsp;&emsp;x1 + x2 <= 5</em> <br>
  <em>&emsp;&emsp;3x1 + 4x2 <= 12</em> <br>
  <em>&emsp;&emsp;x1, x2 >= 0 </em> 
</p>


## THe primal 

This is easy now, the original optimization problem is assumed to be a primal. So the primal is same as the linear program:
<p align="center">
  <em><strong>maximize</strong>&emsp; H(x<sub>1</sub>, x<sub>2</sub>) = 6x1 + 5x2</em> <br>
  <em>subject to:&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;</em><br>
  <em>&emsp;&emsp;x1 + x2 <= 5</em> <br>
  <em>&emsp;&emsp;3x1 + 2x2 <= 12</em> <br>
  <em>&emsp;&emsp;x1, x2 >= 0 </em> 
</p>
How should we start to approach such problem analytically if we are not interested in the graphical method to solve linear programs. Lets suppose there are no conditions on the objective.

<p align="center">
  <em><strong>maximize</strong>&emsp; H(x<sub>1</sub>, x<sub>2</sub>) = 6x1 + 5x2</em> <br>
</p>

Then, the maximum value this objective can achieve is +∞. This sort of gives us an upper bound to the maximum value the objective can take. A lousy one, i agree. However, can we do better? Is it possible to lower / minimize this lousy upper bound? The answer turns out to be yes!  
If you notice the second condition, _3x1 + 2x2 <= 12_ . 
The trick is to multiply this equation by _3_ . Which results in _9x1 + 6x2 <= 36_ and for _x1, x2 >= 0_
<p align="center">
  <em> H(x<sub>1</sub>, x<sub>2</sub>) = 6x1 + 5x2 <= 9x1 + 6x2 <=36 </em>
</p>

So, _36_ is the new upper bound for _H(x<sub>1</sub>, x<sub>2</sub>)_. Can we do even better? Yes! Lets look at the first constraint and multiply it by 6. In turn we get _6x1+6x2<=30_. So the latest upper bound is 30. 30 is lower than 36 as an upper bound and in general sense it is better. Since it is much more tight upper bound to our maximization problem. 

Last time can we do even better? Lets use both the constraints at once. If we multiply first equation by 3 and second equation by 1 and add both of them.

<p align="center">
  <em>&emsp;&emsp;3x1 + 3x2 <= 15</em> <br>
  <em>+ &emsp;3x1 + 2x2 <= 12</em> <br>
  <em>&emsp;&emsp;6x1 + 52 <= 27 </em><br>
  <em>so, H(x<sub>1</sub>, x<sub>2</sub>) = 6x1+5x2 <= 27 </em>
</p>

We have finally been able to get a very tight upper bound on our maximization problem i.e. _27_. Notice, while we were supposed to solve a maximization problem in our approach we used mimization to solve maximization! _Thanos much?_. The minimization problem we solved is called the **dual to the maximization primal**!

## The Dual

While we are almost there, for sake of completeness lets put our ideas together in a mathematical framework. Lets suppose to get the tighest upper bound to the maximum you want to multiply constraint by non negative numbers. First one by _y<sub>1</sum>_ and second constraint by _y<sub>2</sub>_ ; add them and compare it to the _H(x<sub>1</sub>,x<sub>2</sub>)_. Now, 
<p align="center">
  <em>&emsp;&emsp;y<sub>1</sub>*(x<sub>1</sub> + x<sub>2</sub>) <= 5y<sub>1</sub></em> <br>
  <em>&emsp;+y<sub>2</sub>*(3x1 + 2x2) <= 12y<sub>2</sub></em> <br>
  <em>&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;<strong>(y1+3y<sub>2</sub>)</strong>*x1 + <strong>(y1+2y<sub>2</sub>)</strong>*x2 <= 5y1 + 12y<sub>2</sum></em> &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;(A)<br>
  <em>&emsp; <strong>6</strong>*x1 + <strong>5</strong>*x2 = H(x<sub>1</sub>, x<sub>2</sub>)</em> <br> 
  <em>The coefficients x1, x2 of in </em> (A) <em> and in H(x<sub>1</sub>, x<sub>2</sub>) have to be compared to justify that RHS of</em> (A)<em> will give upper bound on our objective. </em>      
</p>
      
So eventually we compare the above expression with _H(x<sub>1</sub>, x<sub>2</sub>)_. The corresponding coefficients of x1 and x2 must be greater than equal to the coefficients of _x<sub>1</sub>, x<sub>2</sub>_ in _H(x<sub>1</sub>, x<sub>2</sub>)_ for it to give the upper bound on the primal. And then the **sum right hand side of the constraints becomes the upper bound.**

Our equivalent objective would be to minimize that upper bound so the equivalent dual would be:

<p align="center">
  <em><strong>maximize</strong>&emsp; D(y<sub>1</sub>, y<sub>2</sub>) = 5y<sub>1</sub> + 12y<sub>2</sub></em> <br>
  <em>&emsp;+y<sub>1</sub> + 3y<sub>2</sub> >= 6</em> <br>
  <em>&emsp;&emsp;y<sub>1</sub> + 2y<sub>2</sub> >= 5</em> <br>
      <em>&emsp;y<sub>1</sub>, y<sub>2</sub> >= 0</em> <br> 
</p>
