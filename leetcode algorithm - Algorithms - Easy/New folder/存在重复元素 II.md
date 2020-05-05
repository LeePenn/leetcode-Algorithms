给定一个整数数组和一个整数 k，判断数组中是否存在两个不同的索引 i 和 j，使得 nums [i] = nums [j]，并且 i 和 j 的差的绝对值最大为 k。

示例 1:

输入: nums = [1,2,3,1], k = 3
输出: true
示例 2:

输入: nums = [1,0,1,1], k = 1
输出: true
示例 3:

输入: nums = [1,2,3,1,2,3], k = 2
输出: false


概述
这篇文章是为初级读者准备的，文章中会介绍了以下几种方法和数据结构：
线性搜索，二分搜索和散列表。

方法一 （线性搜索） 【超时】
思路
将每个元素与它之前的 kk 个元素中比较查看它们是否相等。

算法

这个算法维护了一个 kk 大小的滑动窗口，然后在这个窗口里面搜索是否存在跟当前元素相等的元素。

Java
public boolean containsNearbyDuplicate(int[] nums, int k) {
    for (int i = 0; i < nums.length; ++i) {
        for (int j = Math.max(i - k, 0); j < i; ++j) {
            if (nums[i] == nums[j]) return true;
        }
    }
    return false;
}
// Time Limit Exceeded.
时间复杂度分析

时间复杂度：O(n \min(k,n))O(nmin(k,n))
每次搜索都要花费 O(\min(k, n))O(min(k,n)) 的时间，哪怕kk比nn大，一次搜索中也只需比较 nn 次。

空间复杂度：O(1)O(1)

方法二 （二叉搜索树） 【超时】
思路

通过自平衡二叉搜索树来维护一个 kk 大小的滑动窗口。

算法

这个方法的核心在于降低方法一中搜索前 kk 个元素所耗费的时间。可以想一下，我们能不能用一个更复杂的数据结构来维持这个 kk 大小的滑动窗口内元素的有序性呢？考虑到滑动窗口内元素是严格遵守先进先出的，那么队列会是一个非常自然就能想到的数据结构。链表实现的队列可以支持在常数时间内的 删除，插入，然而 搜索 耗费的时间却是线性的，所以如果用队列来实现的话结果并不会比方法一更好。

一个更好的选择是使用自平衡二叉搜索树（BST)。 BST 中搜索，删除，插入都可以保持 O(\log k)O(logk) 的时间复杂度，其中 kk 是 BST 中元素的个数。在大部分面试中你都不需要自己去实现一个 BST，所以把 BST 当成一个黑盒子就可以了。大部分的编程语言都会在标准库里面提供这些常见的数据结构。在 Java 里面，你可以用 TreeSet 或者是 TreeMap。在 C++ STL 里面，你可以用 std::set 或者是 std::map。

假设你已经有了这样一个数据结构，伪代码是这样的：

遍历数组，对于每个元素做以下操作：
在 BST 中搜索当前元素，如果找到了就返回 true。
在 BST 中插入当前元素。
如果当前 BST 的大小超过了 kk，删除当前 BST 中最旧的元素。
返回 false。
Java
public boolean containsNearbyDuplicate(int[] nums, int k) {
    Set<Integer> set = new TreeSet<>();
    for (int i = 0; i < nums.length; ++i) {
        if (set.contains(nums[i])) return true;
        set.add(nums[i]);
        if (set.size() > k) {
            set.remove(nums[i - k]);
        }
    }
    return false;
}
// Time Limit Exceeded.
复杂度分析

时间复杂度：O(n \log (\min(k,n)))O(nlog(min(k,n)))
我们会做 nn 次 搜索，删除，插入 操作。每次操作将耗费对数时间，即为 \log (\min(k, n))log(min(k,n))。注意，虽然 kk 可以比 nn 大，但滑动窗口大小不会超过 nn。

空间复杂度：O(\min(n,k))O(min(n,k))
只有滑动窗口需要开辟额外的空间，而滑动窗口的大小不会超过 O(\min(n,k))O(min(n,k))。

注意事项

这个算法在 nn 和 kk 很大的时候依旧会超时。

方法三 （散列表） 【通过】
思路

用散列表来维护这个kk大小的滑动窗口。

算法

在之前的方法中，我们知道了对数时间复杂度的 搜索 操作是不够的。在这个方法里面，我们需要一个支持在常量时间内完成 搜索，删除，插入 操作的数据结构，那就是散列表。这个算法的实现跟方法二几乎是一样的。

遍历数组，对于每个元素做以下操作：
在散列表中搜索当前元素，如果找到了就返回 true。
在散列表中插入当前元素。
如果当前散列表的大小超过了 kk， 删除散列表中最旧的元素。
返回 false。
Java
public boolean containsNearbyDuplicate(int[] nums, int k) {
    Set<Integer> set = new HashSet<>();
    for (int i = 0; i < nums.length; ++i) {
        if (set.contains(nums[i])) return true;
        set.add(nums[i]);
        if (set.size() > k) {
            set.remove(nums[i - k]);
        }
    }
    return false;
}
复杂度分析

时间复杂度：O(n)O(n)
我们会做 nn 次 搜索，删除，插入 操作，每次操作都耗费常数时间。

空间复杂度：O(\min(n, k))O(min(n,k))
开辟的额外空间取决于散列表中存储的元素的个数，也就是滑动窗口的大小 O(\min(n,k))O(min(n,k))。

作者：LeetCode
链接：https://leetcode-cn.com/problems/contains-duplicate-ii/solution/cun-zai-zhong-fu-yuan-su-ii-by-leetcode/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。