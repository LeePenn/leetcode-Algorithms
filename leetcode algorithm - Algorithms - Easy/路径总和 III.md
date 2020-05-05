给定一个二叉树，它的每个结点都存放着一个整数值。

找出路径和等于给定数值的路径总数。

路径不需要从根节点开始，也不需要在叶子节点结束，但是路径方向必须是向下的（只能从父节点到子节点）。

二叉树不超过1000个节点，且节点数值范围是 [-1000000,1000000] 的整数。

示例：

root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

返回 3。和等于 8 的路径有:

1.  5 -> 3
2.  5 -> 2 -> 1
3.  -3 -> 11


解法思路（一）
路径的开头可以不是根节点，结束也可以不是叶子节点，是不是有点复杂？
如果问题是这样：找出以根节点为开始，任意节点可作为结束，且路径上的节点和为 sum 的路径的个数；
是不是前序遍历一遍二叉树就可以得到所有这样的路径？是的；
如果这个问题解决了，那么原问题可以分解成多个这个问题；
是不是和数线段是同一个问题，只不过线段变成了二叉树；
在解决了以根节点开始的所有路径后，就要找以根节点的左孩子和右孩子开始的所有路径，三个节点构成了一个递归结构；
递归真的好简单又好难；
解法实现（一）
时间复杂度
O(n)，n为树的节点个数；
空间复杂度
O(h)，h为树的高度；
关键字
二叉树 递归 前序遍历 路径和 路径数量 数线段 双递归

实现细节
sum - root.val 好好体会一下，挺有意思的；
package leetcode._437;

public class Solution437_1 {

    public static class TreeNode {
        int val;
        TreeNode left;
        TreeNode right;
        TreeNode(int x) { val = x; }
    }

    /**
     * 求以 root 为根的二叉树，所有和为 sum 的路径；
     * 路径的开头不一定是 root，结尾也不一定是叶子节点；
     * @param root
     * @param sum
     * @return
     */
    public int pathSum(TreeNode root, int sum) {

        if (root == null) {
            return 0;
        }

        return paths(root, sum) 
                + pathSum(root.left, sum) 
                + pathSum(root.right, sum);
    }

    private int paths(TreeNode root, int sum) {

        if (root == null) {
            return 0;
        }

        int res = 0;
        if (root.val == sum) {
            res += 1;            
        }
        
        res += paths(root.left, sum - root.val);
        res += paths(root.right, sum - root.val);
        
        return res;
    }

}

作者：li-xin-lei
链接：https://leetcode-cn.com/problems/path-sum-iii/solution/leetcode-437-path-sum-iii-by-li-xin-lei/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。