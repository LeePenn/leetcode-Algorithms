给定一个已按照升序排列 的有序数组，找到两个数使得它们相加之和等于目标数。

函数应该返回这两个下标值 index1 和 index2，其中 index1 必须小于 index2。

说明:

返回的下标值（index1 和 index2）不是从零开始的。
你可以假设每个输入只对应唯一的答案，而且你不可以重复使用相同的元素。
示例:

输入: numbers = [2, 7, 11, 15], target = 9
输出: [1,2]
解释: 2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。


方法 1：双指针
算法

我们可以使用 两数之和 的解法在 O(n^2)O(n 
2
 ) 时间 O(1)O(1) 空间暴力解决，也可以用哈希表在 O(n)O(n) 时间和 O(n)O(n) 空间内解决。然而，这两种方法都没有用到输入数组已经排序的性质，我们可以做得更好。

我们使用两个指针，初始分别位于第一个元素和最后一个元素位置，比较这两个元素之和与目标值的大小。如果和等于目标值，我们发现了这个唯一解。如果比目标值小，我们将较小元素指针增加一。如果比目标值大，我们将较大指针减小一。移动指针后重复上述比较知道找到答案。

假设 [... , a, b, c, ... , d, e, f, …][...,a,b,c,...,d,e,f,…] 是已经升序排列的输入数组，并且元素 b, eb,e 是唯一解。因为我们从左到右移动较小指针，从右到左移动较大指针，总有某个时刻存在一个指针移动到 bb 或 ee 的位置。不妨假设小指针县移动到了元素 bb ，这是两个元素的和一定比目标值大，根据我们的算法，我们会向左移动较大指针直至获得结果。

C++
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int low = 0, high = numbers.size() - 1;
        while (low < high) {
            int sum = numbers[low] + numbers[high];
            if (sum == target)
                return {low + 1, high + 1};
            else if (sum < target)
                ++low;
            else
                --high;
        }
        return {-1, -1};
    }
};
是否需要考虑 numbers[low] + numbers[high]numbers[low]+numbers[high] 溢出呢？答案是不需要。因为即使两个元素之和溢出了，因为只存在唯一解，所以一定会先访问到答案。

复杂度分析

时间复杂度：O(n)O(n)。每个元素最多被访问一次，共有 nn 个元素。
空间复杂度：O(1)O(1)。只是用了两个指针。

作者：LeetCode
链接：https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/solution/liang-shu-zhi-he-ii-shu-ru-you-xu-shu-zu-by-leetco/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。