# **A* Pathfinding Algorithm in Python**

## **Project Overview**
This project implements the **A* (A-Star) pathfinding algorithm** in Python. A* is a widely used algorithm for **finding the shortest path** in grid-based environments, commonly used in **AI, robotics, and game development**.

## **Algorithm Explanation**
A* finds the optimal path by calculating:  
- **G-cost**: Distance from the start node.  
- **H-cost**: Estimated distance (heuristic) to the goal.  
- **F-cost**: Sum of G-cost and H-cost (**F = G + H**).  

The algorithm selects the node with the lowest **F-cost**, ensuring an efficient and shortest path to the goal.

## **Implementation Details**
- The grid is represented as a **2D list** where:  
  ✅ `0` = Walkable path  
  ❌ `1` = Obstacle  
- The algorithm uses **Manhattan Distance** as the heuristic function.
- Implemented with **heapq (priority queue)** for efficient node selection.

## **Grid Example**

[0, 1, 0, 0, 0] [0, 1, 0, 1, 0] [0, 0, 0, 1, 0] [1, 1, 0, 1, 0] [0, 0, 0, 0, 0]


## **Expected Output**
When executed, the program finds the shortest path from **(0,0) (top-left)** to **(4,4) (bottom-right)**, avoiding obstacles.  
Example output:
Path: [(0, 0), (1, 0), (2, 0), (2, 1), (2, 2), (3, 2), (4, 2), (4, 3), (4, 4)

