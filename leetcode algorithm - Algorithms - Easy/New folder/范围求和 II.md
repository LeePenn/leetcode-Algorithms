给定一个初始元素全部为 0，大小为 m*n 的矩阵 M 以及在 M 上的一系列更新操作。

操作用二维数组表示，其中的每个操作用一个含有两个正整数 a 和 b 的数组表示，含义是将所有符合 0 <= i < a 以及 0 <= j < b 的元素 M[i][j] 的值都增加 1。

在执行给定的一系列操作后，你需要返回矩阵中含有最大整数的元素个数。

示例 1:

输入: 
m = 3, n = 3
operations = [[2,2],[3,3]]
输出: 4
解释: 
初始状态, M = 
[[0, 0, 0],
 [0, 0, 0],
 [0, 0, 0]]

执行完操作 [2,2] 后, M = 
[[1, 1, 0],
 [1, 1, 0],
 [0, 0, 0]]

执行完操作 [3,3] 后, M = 
[[2, 2, 1],
 [2, 2, 1],
 [1, 1, 1]]

M 中最大的整数是 2, 而且 M 中有4个值为2的元素。因此返回 4。
注意:

m 和 n 的范围是 [1,40000]。
a 的范围是 [1,m]，b 的范围是 [1,n]。
操作数目不超过 10000。


My Submit Solution
class Solution {
    public int maxCount(int m, int n, int[][] ops) {
        if(ops.length==0) return m*n;
        int row_min = Integer.MAX_VALUE, col_min = Integer.MAX_VALUE;
        for(int[] op : ops) {
            row_min = Math.min(row_min, op[0]);
            col_min = Math.min(col_min, op[1]);
        }
        if(row_min==0 && col_min==0) return 1;
        if(row_min==0 || col_min==0) return row_min==0 ? col_min : row_min;
        return row_min*col_min;
        
    }
}


方法 1：暴力 [Time Limit Exceeded]
最简单的方法是创建一个 m * nm∗n 的二维数组 arrarr，对所有操作都逐一将范围内的元素加一，最后数一遍最大元素的数目。由于我们知道所有操作总是会影响到 (0,0)(0,0)，所以元素 arr[0][0]arr[0][0] 总是最大的。在所有操作执行完之后，我们数有多少个跟 arr[0][0]arr[0][0] 一样大的元素就是答案。

Java
public class Solution {
    public int maxCount(int m, int n, int[][] ops) {
        int[][] arr = new int[m][n];
        for (int[] op: ops) {
            for (int i = 0; i < op[0]; i++) {
                for (int j = 0; j < op[1]; j++) {
                    arr[i][j] += 1;
                }
            }
        }
        int count = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (arr[i][j] == arr[0][0])
                    count++;
            }
        }
        return count;
    }
}
复杂度分析

时间复杂度：O(x \times m \times n)O(x×m×n)。数组被更新 xx 次，xx 是操作的次数，也就是 ops.lenthops.lenth。

空间复杂度：O(m \times n)O(m×n)。使用了大小为 m \times nm×n 的数组。

方法 2：一遍遍历 [Accepted]
算法

正如题目描述，所有操作都是在一个初始元素全为 0 的子矩阵上进行。每个矩形的左上角坐标都是 (0,0)(0,0) 而右下角坐标是 每个操作给出的坐标 (i,j)(i,j)。

最大元素是所有操作都会影响到的一个元素，下图是在初始 MM 矩阵上执行了 2 次操作的一个示例图。



从这张图中，我们可以观察到最大元素会是两个操作对应矩阵的交集区域。我们还可以发现要求这块区域，我们不需要将操作区域一个一个加一，我们只需要记录交集区域的右下角即可。这个角的计算方法为 \big(x, y\big) = \big(\text{min}(op[0]), \text{min}(op[1])\big)(x,y)=(min(op[0]),min(op[1]))， 其中 \text{min}(op[i])min(op[i]) 表示所有操作的 op[i]op[i] 中的最小值。

这样，最大元素的数目就是 x \times yx×y。

Java
public class Solution {
    public int maxCount(int m, int n, int[][] ops) {
        for (int[] op: ops) {
            m = Math.min(m, op[0]);
            n = Math.min(n, op[1]);
        }
        return m * n;
    }
}
复杂度分析

时间复杂度：O(x)O(x)。只需要遍历所有操作一次，xx 是操作的数目。

空间复杂度：O(1)O(1)。不需要额外的数组空间。

作者：LeetCode
链接：https://leetcode-cn.com/problems/range-addition-ii/solution/fan-wei-qiu-he-ii-by-leetcode/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。