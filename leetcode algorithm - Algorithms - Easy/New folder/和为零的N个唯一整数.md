给你一个整数 n，请你返回 任意 一个由 n 个 各不相同 的整数组成的数组，并且这 n 个数相加和为 0 。

 

示例 1：

输入：n = 5
输出：[-7,-1,1,3,4]
解释：这些数组也是正确的 [-5,-1,1,2,3]，[-3,-1,2,-2,4]。
示例 2：

输入：n = 3
输出：[-1,0,1]
示例 3：

输入：n = 1
输出：[0]
 

提示：

1 <= n <= 1000


方法一：构造
我们首先将最小的 n - 1 个自然数 0, 1, 2, ..., n - 2 放入数组中，它们的和为 sum。对于剩下的 1 个数，我们可以令其为 -sum，此时这 n 个数的和为 0，并且：

当 n = 1 时，我们构造的答案中只有唯一的 1 个数 0；

当 n > 1 时，我们构造的答案中包含 n - 1 个互不相同的自然数和 1 个负数；

因此这 n 个数互不相同，即我们得到了一个满足要求的数组。

C++Python3
class Solution {
public:
    vector<int> sumZero(int n) {
        vector<int> ans;
        int sum = 0;
        for (int i = 0; i < n - 1; ++i) {
            ans.push_back(i);
            sum += i;
        }
        ans.push_back(-sum);
        return ans;
    }
};
复杂度分析

时间复杂度：O(N)O(N)。

空间复杂度：O(1)O(1)，除了存储答案的数组 ans 之外，额外的空间复杂度是 O(1)O(1)。

作者：LeetCode
链接：https://leetcode-cn.com/problems/find-n-unique-integers-sum-up-to-zero/solution/he-wei-ling-de-nge-wei-yi-zheng-shu-by-leetcode/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。