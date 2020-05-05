排排坐，分糖果。

我们买了一些糖果 candies，打算把它们分给排好队的 n = num_people 个小朋友。

给第一个小朋友 1 颗糖果，第二个小朋友 2 颗，依此类推，直到给最后一个小朋友 n 颗糖果。

然后，我们再回到队伍的起点，给第一个小朋友 n + 1 颗糖果，第二个小朋友 n + 2 颗，依此类推，直到给最后一个小朋友 2 * n 颗糖果。

重复上述过程（每次都比上一次多给出一颗糖果，当到达队伍终点后再次从队伍起点开始），直到我们分完所有的糖果。注意，就算我们手中的剩下糖果数不够（不比前一次发出的糖果多），这些糖果也会全部发给当前的小朋友。

返回一个长度为 num_people、元素之和为 candies 的数组，以表示糖果的最终分发情况（即 ans[i] 表示第 i 个小朋友分到的糖果数）。

 

示例 1：

输入：candies = 7, num_people = 4
输出：[1,2,3,1]
解释：
第一次，ans[0] += 1，数组变为 [1,0,0,0]。
第二次，ans[1] += 2，数组变为 [1,2,0,0]。
第三次，ans[2] += 3，数组变为 [1,2,3,0]。
第四次，ans[3] += 1（因为此时只剩下 1 颗糖果），最终数组变为 [1,2,3,1]。
示例 2：

输入：candies = 10, num_people = 3
输出：[5,2,3]
解释：
第一次，ans[0] += 1，数组变为 [1,0,0]。
第二次，ans[1] += 2，数组变为 [1,2,0]。
第三次，ans[2] += 3，数组变为 [1,2,3]。
第四次，ans[0] += 4，最终数组变为 [5,2,3]。
 

提示：

1 <= candies <= 10^9
1 <= num_people <= 1000


class Solution {
    public int[] distributeCandies(int candies, int num_people) {
        
        int [] ans = new int[num_people];
        int index = 0;int counts = 1;
        while (candies - counts >= 0){
            ans[index++%num_people] += counts;
            candies -= counts++;
        }
        ans[index%num_people] += candies;
        return ans;
    }
}

作者：gu-xiong-007
链接：https://leetcode-cn.com/problems/distribute-candies-to-people/solution/jian-ji-jian-dan-mei-shi-yao-suan-fa-by-gu-xiong-0/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。


class Solution {
    public int[] distributeCandies(int candies, int num_people) {
        double answer = -0.5 + Math.sqrt(0.25 + 2 * candies); //二次方程求解
        int n = (int)Math.ceil(answer); 
        int succn = (int)Math.floor(answer);
        int [] ret = new int[num_people];
        for(int i = 0;i < num_people;i++){
            double c = Math.floor(n / num_people);
            if(n % num_people - i > 0)c += 1;
            ret[i] =(int) (c * (i + 1) + (c * c - c) * num_people / 2); //等差求和公式
            
            if(n > succn && succn % num_people - i == 0){ //如果最后一次糖数不满
                int highanswer = (n * n + n) / 2; //如果不差数所拥有的值
                ret[i] -= highanswer - candies;
            }
        }
        return ret;
    }
}

作者：yu-chen-20
链接：https://leetcode-cn.com/problems/distribute-candies-to-people/solution/java-time-93-zhe-ti-yao-yong-er-ci-han-shu-qiu-jie/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。