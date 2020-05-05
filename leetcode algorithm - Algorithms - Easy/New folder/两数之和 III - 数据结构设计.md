设计并实现一个 TwoSum 的类，使该类需要支持 add 和 find 的操作。

add 操作 -  对内部数据结构增加一个数。
find 操作 - 寻找内部数据结构中是否存在一对整数，使得两数之和与给定的数相等。

示例 1:

add(1); add(3); add(5);
find(4) -> true
find(7) -> false
示例 2:

add(3); add(1); add(2);
find(3) -> true
find(6) -> false


使用2个HashSet：

all: 负责记录所有元素
duplicate: 负责记录重复的元素
实现方法：

add：如果all中已有该元素，则放入duplicate；否则放入all
find：遍历all中的元素，寻找 target = value - num 是否存在。存在则找到。
但这里是否存在需要分为2种情况判断：

target == num，则在重复元素集合duplicate中找；
target != num，则在所有元素集合all中找。
2个HashSet即可解决是否存在2个相同元素之和为value的问题。

复杂度分析：n为已加入的元素个数，

时间复杂度：1次add为O(1)，1次find为O(n)
空间复杂度：O(n)
class TwoSum {

    private Set<Integer> all;
    private Set<Integer> duplicate;
    
    /** Initialize your data structure here. */
    public TwoSum() {
        all = new HashSet();
        duplicate = new HashSet();
    }
    
    /** Add the number to an internal data structure.. */
    public void add(int number) {
        if (all.contains(number))
            duplicate.add(number);
        else
            all.add(number);
    }
    
    /** Find if there exists any pair of numbers which sum is equal to the value. */
    public boolean find(int value) {
        int target;
        for (int num: all) {
            target = value - num;
            if (target == num && duplicate.contains(target))
                return true;
            if (target != num && all.contains(target))
                return true;
        }
        return false;
    }
}


作者：zhong-wu-qi
链接：https://leetcode-cn.com/problems/two-sum-iii-data-structure-design/solution/shuang-ha-xi-setfa-javashi-jian-9375kong-jian-1000/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。


HashMap法：时间复杂度O(N)，空间复杂度O(N)；
add：在将数字添加进nums数组的同时，将数字作为key存入map，map的value存此数字在数组的位置；
find：在搜索是否有加和时，遍历整个数组nums，判断value - nums[i]是否在map中：
若在，还需要判断map[value - nums[i]] == i，这个是为了排除是否是数组中同一个元素的加和（题意是必须两个不同元素的加和）；因为如果add了两个相同的数字，那么map[value - nums[i]]一定大于i，因为在add操作中每次会刷新此数字的最新index。
若不在，就继续遍历，直至遍历完nums。
pythonjava
class TwoSum {
    private Map<Integer, Integer> map;
    private List<Integer> nums = new ArrayList<>();
    /** Initialize your data structure here. */
    public TwoSum() {
        map = new HashMap<>();
    }
    
    /** Add the number to an internal data structure.. */
    public void add(int number) {
        nums.add(number);
        map.put(number, nums.size() - 1);
    }
    
    /** Find if there exists any pair of numbers which sum is equal to the value. */
    public boolean find(int value) {
        for(int i = 0; i < nums.size(); i++){
            int tar = value - nums.get(i);
            if(map.containsKey(tar) && map.get(tar) > i) return true;
        }
        return false;
    }
}

作者：jyd
链接：https://leetcode-cn.com/problems/two-sum-iii-data-structure-design/solution/two-sum-iii-data-structure-design-hashmapfa-by-jyd/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。