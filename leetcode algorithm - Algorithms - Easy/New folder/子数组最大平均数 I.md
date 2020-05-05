给定 n 个整数，找出平均数最大且长度为 k 的连续子数组，并输出该最大平均数。

示例 1:

输入: [1,12,-5,-6,50,3], k = 4
输出: 12.75
解释: 最大平均数 (12-5-6+50)/4 = 51/4 = 12.75
 

注意:

1 <= k <= n <= 30,000。
所给数据范围 [-10,000，10,000]。


My Submit Solution
class Solution {
    public double findMaxAverage(int[] nums, int k) {
        int sum = Integer.MIN_VALUE;
        for(int i=0;i<=nums.length-k;i++) {
            int temp = 0;
            for(int j=0;j<k;j++) {
                temp += nums[i+j];
            }
            if(temp>sum) sum = temp;
        }
        return sum*1.00/k;
    }
}


class Solution {
    public double findMaxAverage(int[] nums, int k) {
        int sum = 0;
        int first = nums[0];
        for(int i=0;i<k;i++) {
            sum += nums[i];
        }
        int temp = sum;
        for(int i=1;i<=nums.length-k;i++) {
            temp = temp-first+nums[i+k-1];
            sum = Math.max(sum, temp);
            first = nums[i];
        }
        return sum*1.00/k;
    }
}


方法一：累计求和【通过】
算法

为了获得长度为 kk 的子数组的平均值，我们需要知道这 kk 个元素之和。使用 sumsum 记录数组的累加和，sum[i]sum[i] 存储从第一个元素到第 ii 个元素之和。该数组只需要计算一次。

在数组 sumsum 中，原数组索引从 ii 到 i+ki+k 的元素之和为 sum[i] - sum[i-k]sum[i]−sum[i−k]。按照此方法遍历数组 sumsum，计算每个长度为 kk 的子数组平均值，即可获得长度为 kk 的子数组的最大平均值。

通过动画说明一个简单实例的计算过程。


1 / 8

Java
public class Solution {
	public double findMaxAverage(int[] nums, int k) {
		int[] sum = new int[nums.length];
		sum[0] = nums[0];
		for (int i = 1; i < nums.length; i++)
		sum[i] = sum[i - 1] + nums[i];
		double res = sum[k - 1] * 1.0 / k;
		for (int i = k; i < nums.length; i++) {
			res = Math.max(res, (sum[i] - sum[i - k]) * 1.0 / k);
		}
		return res;
	}
}
复杂度分析

时间复杂度：O(n)O(n)，遍历数组 numnum，和遍历数组 sumsum 中的 n-kn−k 个元素。

空间复杂度：O(n)O(n)，使用长度为 nn 的数组 sumsum 存储累加和。

方法二：滑动窗口【通过】
算法

相比于创建一个累加和数组，再遍历计算最大平均值，本方法只需要遍历一次数组 numnum，从中找出长度为 kk 的子数组最大和。

假设我们已经索引从 ii 到 i+ki+k 子数组和为 xx。要知道索引从 i+1i+1 到 i+k+1i+k+1 子数组和，只需要从 xx 减去 sum[i]sum[i]，加上 sum[i+k+1]sum[i+k+1] 即可。 根据此方法可以获得长度为 kk 的子数组最大平均值。

Java
public class Solution {
    public double findMaxAverage(int[] nums, int k) {
        double sum=0;
        for(int i=0;i<k;i++)
            sum+=nums[i];
        double res=sum;
        for(int i=k;i<nums.length;i++){
            sum+=nums[i]-nums[i-k];
                res=Math.max(res,sum);
        }
        return res/k;
    }
}
复杂度分析

时间复杂度：O(n)O(n)，遍历长度为 nn 的数组 numnum 所需时间。

空间复杂度：O(1)O(1)，恒定的额外空间。

作者：LeetCode
链接：https://leetcode-cn.com/problems/maximum-average-subarray-i/solution/zi-shu-zu-de-zui-da-ping-jun-shu-i-by-leetcode/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。