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


There is a more condensed representation of the above for using linear algebra and matrix notation. However, it still doesnt throw any insight into the workings and motivation behind the primal and dual relationshiip.
<p align="center">
<img src="https://anurag14.github.io/blog_resources/2020-06-21/matrix-primal-dual.png" width="300" height="50" /> 
</p>
<p align ="center">
Fig2: The condensed matrix notation
</p>

After giving the primal and dual relationship in linear programming a self read I decided to take a bite at explaining it. I hope this interpretation of duality will allow you to get more intuitive understanding of it. Hopefully, helping the reader on their quest to applying this first principle whenever they encounter duality in much more complex and advance scenarios. Comments from the learned community and those who are much familiar with the topic are genuinely appreciated!

Okay. Firstly lets brush how a typical linear programming problem looks like:

## Linear Programming Review 

Lets suppose, that you've turned let go of the conscious in this lockdown - you now want to catch up on your all previous guilty pleasures and hobbies. In turn you maximize the happiness and joy that you get out of all the activities. However, certain physical restrictions and commitments may still apply! In turn you may not be able to continue a activity or combination of certain for longer hours because they could be for example-exhausting. Given these realistic constraints how should we find out how much maximum happiness can you achieve? This can be formulated as an linear programming problem. 

To not digress much lets say you like to do 2 activities dancing and painting the number of hours you paint and dance in a day can be assumed as x1 and x2. 
Lets say the happiness is some function of these two activities then the typical Linear program can look like:

maximize 6x1 + 5x2 subject to some conditions 
conditions can be given as 
x1 + x2 <= 5 You cannot give more than 5 hours a day to any leisure
3x1 + 4x2 <= 12 Given the rate of energy each activity consumes and you cannot spend more than 12 units of energy.
x1 >= 0 and x2 >= 0 becuase you cannot do any activity for negative hours. 

