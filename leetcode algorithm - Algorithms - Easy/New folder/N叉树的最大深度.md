给定一个 N 叉树，找到其最大深度。

最大深度是指从根节点到最远叶子节点的最长路径上的节点总数。

例如，给定一个 3叉树 :

 



 

我们应返回其最大深度，3。

说明:

树的深度不会超过 1000。
树的节点总不会超过 5000。


My Submit Solution
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/
class Solution {
    public int maxDepth(Node root) {
        if(root==null) return 0;
        if(root.children.size()==0) return 1;
        int ans = 0;
        for(Node ch : root.children) {
            ans = Math.max(maxDepth(ch)+1, ans);
        }
        return ans;
    }
}


树的定义

首先，请参考 这篇文章，其中讲述了对于二叉树，如何求解最大深度。
本文在此基础上进行了泛化。

这里是对树节点的定义

JavaPython
// 节点定义
class Node {
  public int val;
  public List<Node> children;

  public Node() {}

  public Node(int _val,List<Node> _children) {
    val = _val;
    children = _children;
  }
}
方法一: 递归
算法

解决这个问题的最直观方法就是递归。
此处展示了深度优先搜索的策略。

JavaPython
class Solution {
  public int maxDepth(Node root) {
    if (root == null) {
      return 0;
    } else if (root.children.isEmpty()) {
      return 1;  
    } else {
      List<Integer> heights = new LinkedList<>();
      for (Node item : root.children) {
        heights.add(maxDepth(item)); 
      }
      return Collections.max(heights) + 1;
    }
  }
}
复杂度分析

时间复杂度：每个节点遍历一次，所以时间复杂度是 O(N)O(N)，其中 NN 为节点数。

空间复杂度：最坏情况下, 树完全非平衡，
例如 每个节点有且仅有一个孩子节点，递归调用会发生 NN 次（等于树的深度），所以存储调用栈需要 O(N)O(N)。
但是在最好情况下（树完全平衡），树的高度为 \log(N)log(N)。
所以在此情况下空间复杂度为 O(\log(N))O(log(N))。

方法二: 迭代
我们还可以在堆栈的帮助下将上面的递归转换为迭代。

思路是是使用深度优先搜索策略访问每个节点，同时更新每次访问时的最大深度。

所以可以从包含根节点的、对应深度为 11 的栈开始。
然后继续迭代，从栈中弹出当前节点并将子节点压入栈中，每次都更新对应深度。

JavaPython
import javafx.util.Pair;
import java.lang.Math;

class Solution {
  public int maxDepth(Node root) {
    Queue<Pair<Node, Integer>> stack = new LinkedList<>();
    if (root != null) {
      stack.add(new Pair(root, 1));
    }

    int depth = 0;
    while (!stack.isEmpty()) {
      Pair<Node, Integer> current = stack.poll();
      root = current.getKey();
      int current_depth = current.getValue();
      if (root != null) {
        depth = Math.max(depth, current_depth);
        for (Node c : root.children) {
          stack.add(new Pair(c, current_depth + 1));    
        }
      }
    }
    return depth;
  }
};
复杂度分析

时间复杂度：O(N)O(N)。
空间复杂度：O(N)O(N)。

作者：LeetCode
链接：https://leetcode-cn.com/problems/maximum-depth-of-n-ary-tree/solution/ncha-shu-de-zui-da-shen-du-by-leetcode/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。