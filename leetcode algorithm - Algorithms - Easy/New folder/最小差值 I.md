给定一个整数数组 A，对于每个整数 A[i]，我们可以选择任意 x 满足 -K <= x <= K，并将 x 加到 A[i] 中。

在此过程之后，我们得到一些数组 B。

返回 B 的最大值和 B 的最小值之间可能存在的最小差值。

 

示例 1：

输入：A = [1], K = 0
输出：0
解释：B = [1]
示例 2：

输入：A = [0,10], K = 2
输出：6
解释：B = [2,8]
示例 3：

输入：A = [1,3,6], K = 3
输出：0
解释：B = [3,3,3] 或 B = [4,4,4]
 

提示：

1 <= A.length <= 10000
0 <= A[i] <= 10000
0 <= K <= 10000


方法 1：数学
想法和算法

假设 A 是原始数组，B 是修改后的数组，我们需要最小化 max(B) - min(B)，也就是分别最小化 max(B) 和最大化 min(B)。

max(B) 最小可能为 max(A) - K，因为 max(A) 不可能再变得更小。同样，min(B) 最大可能为 min(A) + K。所以结果 max(B) - min(B) 至少为 ans = (max(A) - K) - (min(A) + K)。

我们可以用一下修改方式获得结果（如果 ans >= 0）：

如果 A[i] \leq \min(A) + KA[i]≤min(A)+K，那么 B[i] = \min(A) + KB[i]=min(A)+K
如果 A[i] \geq \max(A) - KA[i]≥max(A)−K，那么 B[i] = \max(A) - KB[i]=max(A)−K
否则 B[i] = A[i]B[i]=A[i]。
如果 ans < 0，最终结果会有 ans = 0，同样利用上面的修改方式。

JavaPython
class Solution {
    public int smallestRangeI(int[] A, int K) {
        int min = A[0], max = A[0];
        for (int x: A) {
            min = Math.min(min, x);
            max = Math.max(max, x);
        }
        return Math.max(0, max - min - 2*K);
    }
}
复杂度分析

时间复杂度：O(N)O(N)，其中 NN 是 A 的长度。
空间复杂度：O(1)O(1)。

作者：LeetCode
链接：https://leetcode-cn.com/problems/smallest-range-i/solution/zui-xiao-chai-zhi-i-by-leetcode/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。