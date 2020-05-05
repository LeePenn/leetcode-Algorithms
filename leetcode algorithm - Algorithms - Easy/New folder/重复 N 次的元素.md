在大小为 2N 的数组 A 中有 N+1 个不同的元素，其中有一个元素重复了 N 次。

返回重复了 N 次的那个元素。

 

示例 1：

输入：[1,2,3,3]
输出：3
示例 2：

输入：[2,1,2,5,3,2]
输出：2
示例 3：

输入：[5,1,5,2,5,3,5,4]
输出：5
 

提示：

4 <= A.length <= 10000
0 <= A[i] < 10000
A.length 为偶数


方法 1：计数
想法和算法

直接计数元素的个数。利用 HashMap 或者数组，这里使用 HashMap。

然后，元素数量超过 1 的就是答案。

JavaPython
class Solution {
    public int repeatedNTimes(int[] A) {
        Map<Integer, Integer> count = new HashMap();
        for (int x: A) {
            count.put(x, count.getOrDefault(x, 0) + 1);
        }

        for (int k: count.keySet())
            if (count.get(k) > 1)
                return k;

        throw null;
    }
}
复杂度分析

时间复杂度：O(N)O(N)，其中 NN 是 A 的长度。
空间复杂度：O(N)O(N)。
方法 2：比较
想法和算法

一旦找到一个重复元素，那么一定就是答案。我们称这个答案为主要元素。

考虑所有长度为 4 的子序列，在子序列中一定至少含有两个主要元素。

这是因为：

长度为 2 的子序列中都是主要元素，或者；
每个长度为 2 的子序列都恰好含有 1 个主要元素，这意味着长度为 4 的子序列一定含有 2 个主要元素。
因此，只需要比较所有距离为 1，2 或者 3 的邻居元素即可。

JavaPython
class Solution {
    public int repeatedNTimes(int[] A) {
        for (int k = 1; k <= 3; ++k)
            for (int i = 0; i < A.length - k; ++i)
                if (A[i] == A[i+k])
                    return A[i];

        throw null;
    }
}
复杂度分析

时间复杂度：O(N)O(N)，其中 NN 是 A 的长度。
空间复杂度：O(1)O(1)。

作者：LeetCode
链接：https://leetcode-cn.com/problems/n-repeated-element-in-size-2n-array/solution/zhong-fu-n-ci-de-yuan-su-by-leetcode/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。