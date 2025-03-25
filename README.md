# Maze Generator and Solver

This project implements a maze generator and solver using different algorithms. The goal is to generate a random maze, solve it using various algorithms, and visualize the results.

## Features

- **Maze Generation**: Generate a maze using **Prim's Algorithm** or **Recursive Backtracking**.
- **Maze Solving**: Solve the generated maze using the following algorithms:
  - **A* Algorithm** (A Star)
  - **Right Hand Rule (RH)**
  - **Left Hand Rule (LH)**
  - **Breadth-First Search (BFS)**
  - **Depth-First Search (DFS)**
  
- **Maze Visualization**: Display the maze in a console-based graphical format, showing walls, paths, and visited cells.


## Search Algorithm Visualization

This section includes GIFs demonstrating how different search algorithms solve mazes with varying levels of complexity. The GIFs show the following algorithms in action:

The order of the algorithms in each GIF is as follows: On the first row, the algorithms are DFS, BFS, and A*; on the second row, the algorithms are RH and LH.

### 1. Single Path Maze
This GIF demonstrates the algorithm solving a maze with only one valid path. In this scenario, the algorithm should be able to find the only available solution. All five algorithms are visualized solving the same maze.

![Single Path Maze](gif/O%20cale.gif)

### 2. Medium Density Maze
This GIF shows the algorithm solving a maze with a medium density of walls. In this case, there are two or more possible paths or solutions. The algorithms need to choose between the available options. All five algorithms are visualized solving the same maze.

![Medium Density Maze](gif/densitatea%20medie.gif)

### 3. Low Density Maze
This GIF shows the algorithm solving a maze with a low density of walls, resulting in a large number of possible paths or solutions. The algorithm's efficiency and choice of the optimal path can be observed here. All five algorithms are visualized solving the same maze.

![Low Density Maze](gif/densitate%20scazuta.gif)

## Structure

### `Cell` Structure

Each cell in the maze is represented by the following attributes:

- **visited**: Marks if the cell has been visited.
- **row** and **col**: Coordinates of the cell in the maze.
- **northWall** and **eastWall**: Indicates whether the north and east walls of the cell are present (walls shared between adjacent cells).
- **path**: Marks if the cell is part of the solution path.
- **search**: Marks if the cell is currently being searched.
- **pathIndexes**: A vector storing path indexes used for solving.
- **open** and **closed**: Used in the A* algorithm to mark if the cell is open or closed.
- **hCost**: Heuristic cost for the A* algorithm (estimated cost from the current cell to the target).
- **gCost**: Actual cost from the start cell to the current cell.
- **fCost**: Total cost (gCost + hCost) used in A* algorithm.
- **parent**: Pointer to the parent cell, used in A* for path reconstruction.

### `Maze` Class

The `Maze` class handles the generation and solving of the maze. The maze is represented as a 2D vector of `Cell` objects.

#### Methods:

- **Constructor**: Initializes the maze with a given height and width.
- **`displayMazeDimensions`**: Displays the maze's height and width.
- **`initialiseMaze`**: Initializes all cells in the maze.
- **`displayMaze`**: Displays the maze visually.
- **`generateMaze`**: Generates a random maze.
- **`generateMazePrim`**: Generates a maze using Prim’s Algorithm.
- **`solveMazeAStar`**: Solves the maze using the A* algorithm.
- **`solveMazeRH`**: Solves the maze using the Right Hand Rule (RH).
- **`solveMazeLH`**: Solves the maze using the Left Hand Rule (LH).
- **`solveMazeBFS`**: Solves the maze using Breadth-First Search (BFS).
- **`solveMazeDFS`**: Solves the maze using Depth-First Search (DFS).
- **`resetMaze`**: Resets the maze to its initial state.
- **`modifyMaze`**: Allows modification of the maze (e.g., changing walls).
- **`nullmaze`**: Resets the maze to an empty state.
- **`determinatePath`**: Determines the path by tracking the current cell and previous index.
- **`determinatePathLength`**: Determines the length of the solution path.
- **`search`**: Searches for a cell within a set of cells.
- **`deteminateCellVisited`**: Returns the count of visited cells.

## Performance Analysis

### Table 3.1 - Best Case Scenario: Running Algorithms 10 Times for 5000 Nodes to Highlight Algorithm Stability

| Algorithm | 1      | 2      | 3      | 4      | 5      | 6      | 7      | 8      | 9      | 10     | Average Operations |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|--------|--------|--------------------|
| **A***    | 910553 | 659782 | 577507 | 544397 | 342279 | 292149 | 575341 | 1049987| 435511 | 475839 | 586335             |
| **LH**    | 244461 | 209256 | 187580 | 301513 | 299442 | 103595 | 188017 | 278333 | 147435 | 159102 | 211873             |
| **RH**    | 309498 | 317759 | 353372 | 200162 | 130410 | 386794 | 356471 | 320313 | 100640 | 120185 | 259560             |
| **DFS**   | 370476 | 287265 | 302489 | 332420 | 153396 | 187496 | 343331 | 467517 | 202474 | 317529 | 296439             |
| **BFS**   | 174318 | 127713 | 113264 | 106388 | 67025  | 58134  | 113384 | 202992 | 83752  | 92806  | 113978             |

**Conclusion for Table 3.1:**
- **A\*** is the most resource-intensive, with higher operation counts in both best and average cases.
- **LH** and **RH** show better efficiency, with lower operation counts, particularly in the average case.
- **DFS** and **BFS** perform consistently with fewer operations, with **DFS** being slightly more efficient than **BFS**.

### Table 3.2 - Average Case Scenario: Running Algorithms 10 Times for 5000 Nodes to Highlight Algorithm Stability

| Algorithm | 1      | 2      | 3      | 4      | 5      | 6      | 7      | 8      | 9      | 10     | Average Operations |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|--------|--------|--------------------|
| **A***    | 1862514 | 1889930 | 1893670 | 1901266 | 1952765 | 1816589 | 1943361 | 1899432 | 1772725 | 1947196 | 1887945            |
| **LH**    | 45523  | 33779  | 45349  | 45463  | 33501  | 44436  | 35543  | 32469  | 35139  | 37515  | 38872              |
| **RH**    | 39940  | 44862  | 43271  | 39699  | 59037  | 34507  | 32292  | 41617  | 38406  | 40669  | 41430              |
| **DFS**   | 233473 | 105588 | 75022  | 53786  | 152441 | 84819  | 82311  | 67539  | 226938 | 112791 | 119471             |
| **BFS**   | 217060 | 217092 | 216569 | 216848 | 217103 | 217099 | 216653 | 213639 | 217083 | 216934 | 216608             |

**Conclusion for Table 3.2:**
- **A\*** is the most resource-intensive, with a consistent operation count of around 1.9 million.
- **LH** and **RH** are much more efficient in terms of operation count, suggesting better resource management.
- **DFS** and **BFS** maintain consistent operation counts, with **DFS** being slightly more efficient than **BFS**.

### Table 3.3 - Worst Case Scenario: Path Length Based on Cell Count

| Algorithm | 1000  | 2000  | 3000  | 4000  | 5000  | 6000  | 7000  | 8000  | 9000  | 10000 | 
|-----------|-------|-------|-------|-------|-------|-------|-------|-------|-------|-------|
| **A***    | 70    | 99    | 120   | 138   | 153   | 167   | 180   | 193   | 202   | 211   |
| **LH**    | 136   | 189   | 234   | 284   | 301   | 345   | 375   | 400   | 404   | 448   |
| **RH**    | 129   | 186   | 221   | 267   | 292   | 322   | 348   | 378   | 394   | 422   |
| **DFS**   | 99    | 153   | 187   | 223   | 260   | 287   | 314   | 337   | 341   | 387   |
| **BFS**   | 70    | 99    | 120   | 138   | 153   | 167   | 180   | 193   | 202   | 211   |

**Conclusion for Table 3.3:**
- **A\*** and **BFS** show consistent path lengths, with **A\*** maintaining a steady increase as the number of nodes increases.
- **LH** and **RH** show a steeper increase in path length as the number of nodes grows.
- **DFS** shows moderate growth, similar to **A\***, but with slightly higher path lengths.

## Conclusion

The conclusions of this work reflect the results and observations obtained during the development and implementation of algorithms for solving the maze problem. The A*, RH, LH, BFS, and DFS algorithms were employed to navigate through maze environments, with each algorithm being optimized for various maze configurations. A* proved effective in finding the shortest path, while RH and LH offered direction-based strategies, and BFS and DFS highlighted the differences in solution-finding approaches. The analysis showed the strengths and limitations of each algorithm, with performance, operation count, and adaptability being key metrics. Overall, the work emphasizes the importance of selecting the right algorithm based on the maze's specific characteristics, with future research needed to further optimize and expand current approaches.

  
## Example Usage

```cpp
int main() {
    // Create a maze with 10 rows and 10 columns
    Maze maze(10, 10);

    // Initialize the maze
    maze.initialiseMaze();

    // Generate the maze using Prim's algorithm
    maze.generateMazePrim();

    // Solve the maze using A* algorithm
    maze.solveMazeAStar();

    // Display the maze and the solution path
    maze.displayMaze();
    
    return 0;
}
```
