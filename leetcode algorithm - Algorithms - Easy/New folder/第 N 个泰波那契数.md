泰波那契序列 Tn 定义如下： 

T0 = 0, T1 = 1, T2 = 1, 且在 n >= 0 的条件下 Tn+3 = Tn + Tn+1 + Tn+2

给你整数 n，请返回第 n 个泰波那契数 Tn 的值。

 

示例 1：

输入：n = 4
输出：4
解释：
T_3 = 0 + 1 + 1 = 2
T_4 = 1 + 1 + 2 = 4
示例 2：

输入：n = 25
输出：1389537
 

提示：

0 <= n <= 37
答案保证是一个 32 位整数，即 answer <= 2^31 - 1。


My Submit Solution
class Solution {
    public int tribonacci(int n) {
        int t0 = 0, t1 = 1, t2 = 1;
        if(n==0) return t0;
        else if(n==1) return t1;
        else if(n==2) return t2;
        else {
            int t3 = 0;
            while(n>=3) {
                t3 = t0 + t1 + t2;
                t0 = t1;
                t1 = t2;
                t2 = t3;
                --n;
            }
            return t3;
        }
        
        
    }
}


解题思路
思路：

题目给出了递推式，很容易想到用自顶向下的递归写法，把递归式改为：Tn = Tn-3 + Tn-2 + Tn-1
但是一提交发现超时，原因是这个递推式用到了前三项的和，而每次求前三项的时候都是从头开始递归求，显然做了很多重复操作。
所以用到了dp数组存取之前求过的结果，当下次要的时候直接取。

代码
class Solution {
	int[] dp = new int[38];

	public int tribonacci(int n) {
		// 先判断数组中是否有结果，有直接取
		if (dp[n] != 0) {
			return dp[n];
		}

		if (n == 0) {
			return 0;
		} else if (n == 1 || n == 2) {
			return 1;
		} else {
			// 递归获取结果
			int res = tribonacci(n - 3) + tribonacci(n - 2) + tribonacci(n - 1);
			// 将结果保存到数组中
			dp[n] = res;
			return res;
		}
	}
}

作者：one-piece-11
链接：https://leetcode-cn.com/problems/n-th-tribonacci-number/solution/di-gui-jia-dpjian-dan-qiu-jie-shuang-100-by-one-pi/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。