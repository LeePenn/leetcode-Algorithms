给定一个整数数组和一个整数 k, 你需要在数组里找到不同的 k-diff 数对。这里将 k-diff 数对定义为一个整数对 (i, j), 其中 i 和 j 都是数组中的数字，且两数之差的绝对值是 k.

示例 1:

输入: [3, 1, 4, 1, 5], k = 2
输出: 2
解释: 数组中有两个 2-diff 数对, (1, 3) 和 (3, 5)。
尽管数组中有两个1，但我们只应返回不同的数对的数量。
示例 2:

输入:[1, 2, 3, 4, 5], k = 1
输出: 4
解释: 数组中有四个 1-diff 数对, (1, 2), (2, 3), (3, 4) 和 (4, 5)。
示例 3:

输入: [1, 3, 1, 5, 4], k = 0
输出: 1
解释: 数组中只有一个 0-diff 数对，(1, 1)。
注意:

数对 (i, j) 和数对 (j, i) 被算作同一数对。
数组的长度不超过10,000。
所有输入的整数的范围在 [-1e7, 1e7]。


def findPairs(nums, k):
    # 这里有一个细节需要注意的是: (1,3)等同于(3,1)
    # 所以我们无需将1,3都存储起来, 只要存储3即可. 因为k是确定的, 导致1也是确定的
    if k < 0:
        return 0
    # s存储遍历的元素, r存储上面注释的3
    s, r = set(), set()
    for n in nums:
        if n + k in s:
            r.add(n + k)
        if n - k in s:
            r.add(n)
        s.add(n)
        
    return len(r)

作者：leicj
链接：https://leetcode-cn.com/problems/k-diff-pairs-in-an-array/solution/python3-shu-zu-zhong-de-k-diffshu-dui-by-leicj/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。