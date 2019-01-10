# n queens

The _n_-queens puzzle is the problem of placing _n_ queens on an _n_×_n_ chessboard such that no two queens attack each other.

![](https://assets.leetcode.com/uploads/2018/10/12/8-queens.png)

Given an integer _n_, return all distinct solutions to the _n_-queens puzzle.

Each solution contains a distinct board configuration of the _n_-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space respectively.

```text
Example
Input: 4
Output: 2
Explanation: There are two distinct solutions to the 4-queens puzzle as shown below.
[
 [".Q..",  // Solution 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // Solution 2
  "Q...",
  "...Q",
  ".Q.."]
]
```

{% tabs %}
{% tab title="Notes" %}
```java
//4 x 4
col 0 1 2 3
    0 1 0 0 
    0 0 0 1
    1 0 0 0
    0 0 1 0
cols: 1 3 0 2

col 0 1 2 3
    0 0 1 0 
    1 0 0 0
    0 0 0 1
    0 1 0 0
cols: 2 0 3 1 
```

* good video explanation: [https://www.youtube.com/watch?v=0DeznFqrgAI](https://www.youtube.com/watch?v=0DeznFqrgAI)
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> res = new ArrayList<>();
        
        dfs(n, new ArrayList<>(), res);
        return res;
    }
    
    public void dfs(int n, List<Integer> cols, List<List<String>> res) {
        if (cols.size() == n) {
            res.add(draw(cols));
            return;
        }
        
        for (int colIndex = 0; colIndex < n; colIndex++) {
            if (!isValid(cols, colIndex)) { 
                continue;
            }
            
            cols.add(colIndex);
            dfs(n, cols, res);
            cols.remove(cols.size() - 1);
        }
    }
    
    public boolean isValid(List<Integer> cols, int colIndex) {
        int numOfRow = cols.size();
        //check the columns of the existing rows
        for (int rowIndex = 0; rowIndex < numOfRow; rowIndex++) {
            if (cols.get(rowIndex) == colIndex) {
                return false;
            }
            
            if (cols.get(rowIndex) + rowIndex == colIndex  + numOfRow) {
                return false;
            }
            
            if (cols.get(rowIndex) - rowIndex == colIndex - numOfRow) {
                return false;
            }
        }
        
        return true;
    }
    
    public List<String> draw(List<Integer> cols) {
        List<String> res = new ArrayList<>();
        int n = cols.size();
        
        for (int rowIndex = 0; rowIndex < n; rowIndex++) {
            String row = "";
            for (int colIndex = 0; colIndex < n; colIndex++) {
                if (colIndex == cols.get(rowIndex)) {
                    row += "Q";
                } else {
                    row += ".";
                }
            }
            res.add(row);
        }
        
        return res;
    }
}
```
{% endtab %}
{% endtabs %}

