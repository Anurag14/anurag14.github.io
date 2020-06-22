---
layout: post
title: "The essence of duality - from the perspective of linear programming"
date: 2020-06-21
---

Primal dual relationships are often at the heart of ideas in optimization and in applications of linear algebra. From advanced lagrangian duals to linear programming methods - all of them draw inspiration from the simple idea of duality.

Often the idea is quite misunderstood. The underlying simplicity is marred by complex notation and rigor. You are likely to get introduced to primal dual relationship in linear programming as following, in most textbooks:
<p align="center">
<img src="https://anurag14.github.io/blog_resources/2020-06-21/primal-and-dual-problem-16-638.jpg" width="300" height="300" />
</p>
<p align ="center">
Fig1: Primal and dual of a linear programming problem
</p>


There is a more condensed representation of the above using linear algebra and matrix notation. However, it still doesn't throw any light on the essence and motivation behind the primal and dual relationship.
<p align="center">
<img src="https://anurag14.github.io/blog_resources/2020-06-21/matrix-primal-dual.png" width="300" height="50" /> 
</p>
<p align ="center">
Fig2: The condensed matrix notation
</p>

After giving the primal and dual relationship in linear programming a read, I decided to take a bite at explaining it. I hope this interpretation of duality will allow you to get a more intuitive understanding of it. Hopefully, helping the reader on their quest to apply this first principle whenever they encounter duality in much more complex and advanced scenarios. Comments from the learned community and those who are familiar with the topic are genuinely appreciated!

Okay, firstly lets brush up what a _typical_ linear programming problem looks like:

## Linear Programming Review 

Let us suppose that during this lockdown you want to catch up on all your previous guilty pleasures and hobbies. In turn you wish to the maximize happiness and joy from all these activities. However, certain physical restrictions may still apply! For example, one may not be able to continue an activity or combination of certain activities for an extended period because you still don't have sufficient time or the activities can be exhausting. Given these realistic constraints, you wish to maximize the happiness that can be achieved. This can be formulated as a linear programming problem! 

To not make our example complex, let's say you like to engage in two activities: dancing and painting. 
Let the number of hours you paint and dance in a day be _x<sub>1</sub>_ and _x<sub>2</sub>_ resp.   
Let's say the happiness is some function of these two activities _H(x<sub>1</sub>, x<sub>2</sub>) = 6x<sub>1</sub>+5x<sub>2</sub>_.   
The happiness is maximized subject to some constraints.  
If you cannot give more than five hours a day to any leisure, it translates to, _x<sub>1</sub> + x<sub>2</sub> <= 5_ 
Given the rate of energy each activity consumes and given you cannot spend more than 12 units of energy, translates to _3x<sub>1</sub> + 4x<sub>2</sub> <= 12_    
Since you cannot do any activity for negative hours both _x<sub>1</sub>, x<sub>2</sub>_ have to be non negative  _x<sub>1</sub>, x<sub>2</sub> >= 0_ 

Then the typical linear program can look like:  
<p align="center">
  <em><strong>maximize</strong>&emsp; H(x<sub>1</sub>, x<sub>2</sub>) = 6x<sub>1</sub> + 5x<sub>2</sub></em> <br>
  <em>subject to:&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;</em><br>
  <em>&emsp;&emsp;x<sub>1</sub> + x<sub>2</sub> <= 5</em> <br>
  <em>&emsp;&emsp;3x<sub>1</sub> + 4x<sub>2</sub> <= 12</em> <br>
  <em>&emsp;&emsp;x<sub>1</sub>, x<sub>2</sub> >= 0 </em> 
</p>


## The primal problem 

Now, this is easy. The original optimization problem is assumed to be a primal. So the primal is the same as the linear program:
<p align="center">
  <em><strong>maximize</strong>&emsp; H(x<sub>1</sub>, x<sub>2</sub>) = 6x<sub>1</sub> + 5x<sub>2</sub></em> <br>
  <em>subject to:&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;</em><br>
  <em>&emsp;&emsp;x<sub>1</sub> + x<sub>2</sub> <= 5</em> <br>
  <em>&emsp;&emsp;3x<sub>1</sub> + 2x<sub>2</sub> <= 12</em> <br>
  <em>&emsp;&emsp;x<sub>1</sub>, x<sub>2</sub> >= 0 </em> 
</p>
How should we begin to approach such a problem analytically if we are not interested in the graphical method to solve linear programs? Let's suppose there are no conditions on the objective

<p align="center">
  <em><strong>maximize</strong>&emsp; H(x<sub>1</sub>, x<sub>2</sub>) = 6x<sub>1</sub> + 5x<sub>2</sub></em> <br>
</p>

Then, the maximum value this objective can achieve is +∞. This sort of gives us an upper bound to the maximum value the objective can take. Although a lousy one, I agree. However, can we do better? Is it possible to reduce or minimize this lousy upper bound? The answer turns out to be yes!  
If you notice the second condition, _3x<sub>1</sub> + 2x<sub>2</sub> <= 12_ . 
The trick is to multiply this equation by _3_ . Which results in _9x<sub>1</sub> + 6x<sub>2</sub> <= 36_ and for non-negative variables i.e. _x<sub>1</sub>, x<sub>2</sub> >= 0_. If the coefficients of these variables in the inequality is greater than the coefficients of corresponding variables in the objective then the right hand side acts as the **upper bound**.  
<p align="center">
  <em> H(x<sub>1</sub>, x<sub>2</sub>) = 6x<sub>1</sub> + 5x<sub>2</sub> <= 9x<sub>1</sub> + 6x<sub>2</sub> <=36 </em>
</p>

So, _36_ is the new upper bound for _H(x<sub>1</sub>, x<sub>2</sub>)_. Can we do even better? Yes! Let's look at the first constraint and multiply it by 6. In turn we get _6x<sub>1</sub> + 6x<sub>2</sub> <=30_. So the latest upper bound is 30. 30 is lower than 36 as an upper bound. In general sense, it is better since it is much more tight upper bound to our maximization problem. 

Last time, can we do even better? Let's use both the constraints at once. If we multiply first equation by 3 and second equation by 1 and add both of them.

<p align="center">
  <em>&emsp;&emsp;3x<sub>1</sub> + 3x<sub>2</sub> <= 15</em> <br>
  <em>+ &emsp;3x<sub>1</sub> + 2x<sub>2</sub> <= 12</em> <br>
  <em>&emsp;&emsp;6x<sub>1</sub> + 5x<sub>2</sub> <= 27 </em><br>
  <em>so, H(x<sub>1</sub>, x<sub>2</sub>) = 6x<sub>1</sub>+5x<sub>2</sub> <= 27 </em>
</p>

We have finally been able to get a very tight upper bound on our maximization problem i.e. _27_. Notice while we were supposed to solve a maximization problem in our approach, we used mimization to solve maximization! _Thanos much?_. The minimization problem we solved is called the **dual to the maximization primal**!

## The Dual problem

While we are almost there, for sake of completeness let's put our ideas together in a mathematical framework. Suppose to get the tighest upper bound to the maximum, you want to multiply constraint by non-negative numbers. First one by _y<sub>1</sub>_ and second constraint by _y<sub>2</sub>_ ; add them and compare it to the _H(x<sub>1</sub>,x<sub>2</sub>)_. Now, 
<p align="center">
  <em>&emsp;&emsp;y<sub>1</sub>*(x<sub>1</sub> + x<sub>2</sub>) <= 5y<sub>1</sub></em> <br>
  <em>&emsp;+y<sub>2</sub>*(3x<sub>1</sub> + 2x<sub>2</sub>) <= 12y<sub>2</sub></em> <br>
  <em>&emsp;<strong>(y1+3y<sub>2</sub>)</strong>*x1 + <strong>(y<sub>1</sub>+2y<sub>2</sub>)</strong>*x2 <= 5y<sub>1</sub> + 12y<sub>2</sub></em> (A)<br>
  <em>&emsp; <strong>6</strong>*x<sub>1</sub> + <strong>5</strong>*x<sub>2</sub> = H(x<sub>1</sub>, x<sub>2</sub>)</em> <br> 
  <em>The coefficients x<sub>1</sub>, x<sub>2</sub> of in </em> (A) <em> and in H(x<sub>1</sub>, x<sub>2</sub>) have to be compared to justify that RHS of</em> (A)<em> will give upper bound on our objective. </em>      
</p>
      
So, eventually we compare the above expression with _H(x<sub>1</sub>, x<sub>2</sub>)_. The corresponding coefficients of x<sub>1</sub> and x<sub>2</sub> must be greater than equal to the coefficients of _x<sub>1</sub>, x<sub>2</sub>_ in _H(x<sub>1</sub>, x<sub>2</sub>)_ for it to give the upper bound on the primal. And then the **sum right hand side of the constraints becomes the upper bound.**

Our equivalent objective would be to minimize that upper bound so the equivalent dual would be:

<p align="center">
  <em><strong>minimize</strong>&emsp; D(y<sub>1</sub>, y<sub>2</sub>) = 5y<sub>1</sub> + 12y<sub>2</sub></em> <br>
  <em>&emsp;+y<sub>1</sub> + 3y<sub>2</sub> >= 6</em> <br>
  <em>&emsp;&emsp;y<sub>1</sub> + 2y<sub>2</sub> >= 5</em> <br>
      <em>&emsp;y<sub>1</sub>, y<sub>2</sub> >= 0</em> <br> 
</p>

## Takeaways!

Every problem can be thought of as a primal or dual problem. The conjugate of the primal is the dual and vice versa. In essence, a dual of maximization problem can be thought of as trying to get a tight bound for the maximum i.e. trying to minimize the upper bound from infinity to the maximum, slowly. Which becomes a minimization problem. Similarly for a minimization primal the dual would be to approach it as maximizing the lower bound to achieve tight lower bounds!

Needless to say, careful readers may wonder as we make the bounds increasingly tighter, does the bound ever equal to the answer of the original problem? The answer is yes and that's what is called **weak duality**. Which is left to future discussion!
