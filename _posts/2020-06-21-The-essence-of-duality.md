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
Lets say the happiness is some function of these two activities _H(x1,x2) = 6x1+5x2_.   
The happiness is maximized subject to some constraints.  
If you cannot give more than 5 hours a day to any leisure translates to, _x1 + x2 <= 5_ 
Given the rate of energy each activity consumes and you cannot spend more than 12 units of energy translates to _3x1 + 4x2 <= 12_    
Since you cannot do any activity for negative hours both _x1, x2_ have to be non negative  _x1, x2 >= 0_ 

then the typical Linear program can look like:  
<p align="center">
  <em><strong>maximize</strong>&emsp; H(x1,x2) = 6x1 + 5x2</em> <br>
  <em>subject to:&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;</em><br>
  <em>&emsp;&emsp;x1 + x2 <= 5</em> <br>
  <em>&emsp;&emsp;3x1 + 4x2 <= 12</em> <br>
  <em>&emsp;&emsp;x1, x2 >= 0 </em> 
</p>


## THe primal 

This is easy now, the original optimization problem is assumed to be a primal. So the primal is 
