---
layout: post
title: "AI solver for 2048 Game"
date: 2016-09-14
---
Some time back, I saw a friend playing the 2048 game. 
One go at it, and I have been hooked on ever since. 
Sadly though, I haven't been able to get the 2048 tile and win it. 
It was really frustrating, so I decided to write an artificial intelligence to solve the game. 
In this post, I will discuss my approach for writing the solver.
### DEMO

<p align="center">
  <img src="https://anurag14.github.io/images/2048 - Google Chrome 5_30_2019 6_35_53 PM.gif"/>
</p>

### Watch it [here!](https://anurag14.github.io/2048/)

### Screenshot

<p align="center">
  <img src="https://cloud.githubusercontent.com/assets/1175750/8614312/280e5dc2-26f1-11e5-9f1f-5891c3ca8b26.png" alt="Screenshot"/>
</p>

# *Goal of the game*

2048 is played on a 4 X 4 grid, with four possible moves up, left, down and right. The objective of the game is to slide numbered tiles on the grid to combine them and create a tile with the number 2048.

There are four possible moves from which a player can choose at each turn. After each move, a new tile is inserted into the grid at a random empty position. The value of the tile can be either 2 or 4.

From the source code of the game, it was clear that the value is 2 with a probability 0.9. From the source code of the game,
```javascript
var value = Math.random() < 0.9 ? 2 : 4;  
```
# *Algorithm*

I used a depth bounded expectimax search to write the AI. At every turn, the AI explores all the four possible directions and then decides the best one. The recurrence relation that it follows is

The max node is the one in which the player chooses a move (out of the four directions), and the chance node is the one in which the board inserts a random tile. The max node decides the correct move by maximising the score of its children, which are the chance nodes.

Due to space and time restrictions, it is obviously not possible to explore the complete search space. The search is bounded by a depth, at which the AI evaluates the score of the state (the leaf node) using some heuristic.

Now I will try and explain the approach using a python code as it is easy to digest 
```python
def optimalMove(grid, depth, agent):  
    if depth is 0:
        return score(grid)
    elif agent is BOARD:
        score = 0
        for tile in grid.emptyTiles():
            newGrid = grid.clone()
            newGrid.insert(tile, 2)
            score += 0.9 * bestMove(grid, depth - 1, PLAYER)
            newGrid = grid.clone()
            newGrid.insert(tile, 4)
            score += 0.1 * optimalMove(grid, depth - 1, PLAYER)
        return score/len(grid.emptyTiles())
    elif agent is PLAYER:
        score = 0
        for dir in [left, up, right, down]:
            newGrid = grid.clone()
            newGrid.move(dir)
            score = max(score, bestMove(newGrid, depth - 1, BOARD)
        return score
```
