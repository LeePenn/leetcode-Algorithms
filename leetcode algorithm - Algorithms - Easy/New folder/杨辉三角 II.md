给定一个非负索引 k，其中 k ≤ 33，返回杨辉三角的第 k 行。



在杨辉三角中，每个数是它左上方和右上方的数的和。

示例:

输入: 3
输出: [1,3,3,1]
进阶：

你可以优化你的算法到 O(k) 空间复杂度吗？



def getRow(rowIndex):
    # j行的数据, 应该由j - 1行的数据计算出来.
    # 假设j - 1行为[1,3,3,1], 那么我们前面插入一个0(j行的数据会比j-1行多一个),
    # 然后执行相加[0+1,1+3,3+3,3+1,1] = [1,4,6,4,1], 最后一个1保留即可.
    r = [1]
    for i in range(1, rowIndex + 1):
        r.insert(0, 0)
        # 因为i行的数据长度为i+1, 所以j+1不会越界, 并且最后一个1不会被修改.
        for j in range(i):
            r[j] = r[j] + r[j + 1]
    return r

print(getRow(5))

作者：leicj
链接：https://leetcode-cn.com/problems/pascals-triangle-ii/solution/python3-yang-hui-san-jiao-ii-by-leicj/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。