给定一个整数数组 A，我们只能用以下方法修改该数组：我们选择某个个索引 i 并将 A[i] 替换为 -A[i]，然后总共重复这个过程 K 次。（我们可以多次选择同一个索引 i。）

以这种方式修改数组后，返回数组可能的最大和。

 

示例 1：

输入：A = [4,2,3], K = 1
输出：5
解释：选择索引 (1,) ，然后 A 变为 [4,-2,3]。
示例 2：

输入：A = [3,-1,0,2], K = 3
输出：6
解释：选择索引 (1, 2, 2) ，然后 A 变为 [3,1,0,2]。
示例 3：

输入：A = [2,-3,-1,5,-4], K = 2
输出：13
解释：选择索引 (1, 4) ，然后 A 变为 [2,3,-1,5,4]。
 

提示：

1 <= A.length <= 10000
1 <= K <= 10000
-100 <= A[i] <= 100


解题思路：
1.K>0，则执行 2,否则执行 4

2.取数组 A 中的最小值，并取反

3.K-- 执行 1

4.对数组 A 求和

注意点

第 22 步取最小值取得是新数组的最小值。

具体解法：
我这里参考了前几名的答案,通过使用 number 数组，将各数字出现次数存入其中，可不排序就快速找到最小值。

Java
class Solution {
     public int largestSumAfterKNegations(int[] A, int K) {
        int[] number = new int[201];//-100 <= A[i] <= 100,这个范围的大小是201
        for (int t : A) {
            number[t + 100]++;//将[-100,100]映射到[0,200]上
        }
        int i = 0;
        while (K > 0) {
            while (number[i] == 0)//找到A[]中最小的数字
                i++;
            number[i]--;//此数字个数-1
            number[200 - i]++;//其相反数个数+1
            if (i > 100) {//若原最小数索引>100,则新的最小数索引应为200-i.(索引即number[]数组的下标)
                i = 200 - i;
            }
            K--;
        }
        int sum = 0;
        for (int j = i; j <number.length ; j++) {//遍历number[]求和
            sum += (j-100)*number[j];//j-100是数字大小,number[j]是该数字出现次数.
        }
        return sum;
    }
}

作者：FlyChenKai
链接：https://leetcode-cn.com/problems/maximize-sum-of-array-after-k-negations/solution/java-chao-yue-9966xiang-xi-jie-xi-by-flychenkai/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。