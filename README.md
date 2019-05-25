# Getting Started

## BFS

### *200. Number of Islands*

Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

>```
Input:
11110
11010
11000
00000
Output: 1
```

**Example 2:**

>```
Input:
11000
11000
00100
00011
Output: 3
```

**Solution**
```Java
class Solution {
  public int numIslands(char[][] grid) {
    if (grid == null || grid.length == 0) {
      return 0;
    }

    if (grid[0] == null || grid[0].length == 0) {
      return 0;
    }

    int num = 0;
    int n = grid.length;
    int m = grid[0].length;

    for (int i = 0; i < n; i++) {
      for (int j = 0; j < m; j++) {
        if (grid[i][j] == '1') {
          num++;
          markByBFS(grid, i, j);
        }
      }
    }

    return num;
  }

  private void markByBFS(char[][] grid, int x, int y) {
    if (!inBound(grid, x, y)) {
      return;
    }

    if (grid[x][y] == '0') {
      return;
    }

    int[] dx = {0, 0, 1, -1};
    int[] dy = {1, -1, 0, 0};

    Queue<Point> queue = new LinkedList<>();
    queue.offer(new Point(x, y));
    grid[x][y] = '0';

    while (!queue.isEmpty()) {
      Point curr = queue.poll();
      for (int i = 0; i < 4; i++) {
        Point next = new Point(curr.x + dx[i], curr.y + dy[i]);
        if (inBound(grid, next.x, next.y) && grid[next.x][next.y] == '1') {
          queue.offer(next);
          grid[next.x][next.y] = '0';
        }
      }
    }
  }

  private boolean inBound(char[][] grid, int x, int y) {
    if (grid == null || grid.length == 0) {
      return false;
    }

    if (grid[0] == null || grid[0].length == 0) {
      return false;
    }

    int n = grid.length;
    int m = grid[0].length;
    return x >= 0 && x < n && y >= 0 && y < m;
  }
}

class Point {
  int x;
  int y;
  public Point(int x, int y) {
    this.x = x;
    this.y = y;
  }
}
```
