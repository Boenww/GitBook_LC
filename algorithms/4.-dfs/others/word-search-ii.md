# word search I && II

## I

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

```text
Example:
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

Given word = "ABCCED", return true.
Given word = "SEE", return true.
Given word = "ABCB", return false.
```

{% tabs %}
{% tab title="Notes" %}
* Time O\(m\*n\*4^k\), k: the word length; Space O\(k\)
{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    public int[] deltaX = {0, 0, 1, -1};
    public int[] deltaY = {1, -1, 0, 0};

    public boolean exist(char[][] board, String word) {
        boolean[][] visited = new boolean[board.length][board[0].length];
        
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                if (dfs(board, i, j, visited, "", word)) {
                    return true;
                }
            }
        }
        
        return false;
    }
    
    public boolean dfs(char[][] board, int x, int y, boolean[][] visited, String cur, String word) {
        if (cur.equals(word)) {
            return true;
        }
        
        if (!inBound(board, x, y) || visited[x][y] || board[x][y] != word.charAt(cur.length())) {
            return false;
        }
        
        boolean res = false;
        visited[x][y] = true;
        for (int dir = 0; dir < 4; dir++) {
            res |= dfs(board, x + deltaX[dir], y + deltaY[dir], visited, cur + board[x][y], word);
            if (res) {
                return res;
            }
        }
        visited[x][y] = false;
        return res;
    }
    
    public boolean inBound(char[][] board, int x, int y) {
        return x >= 0 && x < board.length && y >= 0 && y < board[0].length;
    }
}
```
{% endtab %}
{% endtabs %}

## II



