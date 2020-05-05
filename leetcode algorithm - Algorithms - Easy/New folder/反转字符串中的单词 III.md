给定一个字符串，你需要反转字符串中每个单词的字符顺序，同时仍保留空格和单词的初始顺序。

示例 1:

输入: "Let's take LeetCode contest"
输出: "s'teL ekat edoCteeL tsetnoc" 
注意：在字符串中，每个单词由单个空格分隔，并且字符串中不会有任何额外的空格。


方法 1：简单的解法 [Accepted]
第一种方法非常简单，我们将输入字符串中按照空白字符串分开，然后把所有单词放到一个字符串列表中，然后我们逐一遍历每一个字符串并把反转结果连接起来。最后，我们将删除了额外空白字符的字符串返回。

Java
public class Solution {
    public String reverseWords(String s) {
        String words[] = s.split(" ");
        StringBuilder res=new StringBuilder();
        for (String word: words)
            res.append(new StringBuffer(word).reverse().toString() + " ");
        return res.toString().trim();
    }
}
时间复杂度

时间复杂度： O(n)O(n) 。其中nn 是字符串的长度。

空间复杂度： O(n)O(n) 。使用了大小为 nn 的 resres 。

方法 2：不使用自带的 split 和 reverse 函数 [Accepted]
算法

我们可以自己写一个 split 和 reverse 函数。 split 函数将字符串按照 " " （空格）为分隔符将字符串分开并返回单词列表。 reverse 函数返回每个字符串反转后的字符串。

Java
public class Solution {
    public String reverseWords(String s) {
        String words[] = split(s);
        StringBuilder res=new StringBuilder();
        for (String word: words)
            res.append(reverse(word) + " ");
        return res.toString().trim();
    }
    public String[] split(String s) {
        ArrayList < String > words = new ArrayList < > ();
        StringBuilder word = new StringBuilder();
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == ' ') {
                words.add(word.toString());
                word = new StringBuilder();
            } else
                word.append( s.charAt(i));
        }
        words.add(word.toString());
        return words.toArray(new String[words.size()]);
    }
    public String reverse(String s) {
      StringBuilder res=new StringBuilder();
        for (int i = 0; i < s.length(); i++)
            res.insert(0,s.charAt(i));
        return res.toString();
    }
}
时间复杂度

时间复杂度： O(n)O(n) 。其中 nn 是字符串的长度。
空间复杂度： O(n)O(n) 。使用了大小为 nn 的 resres 。
方法 3：使用 StringBuilder 和 reverse 方法 [Accepted]
算法

这一方法中，我们不使用 split 方法，我们创建临时字符串 wordword 保存单词，我们在遍历过程中将字符逐一连接在 wordword 后面，直到我们遇到 ' '（空格） 字符。当我们遇到 ' ' 字符时，我们将 wordword 反转后连接在结果字符串 resultresult 后面。在遍历完成以后，我们返回结果字符串 resultresult 。

Java
public class Solution {
    public String reverseWords(String input) {
        final StringBuilder result = new StringBuilder();
        final StringBuilder word = new StringBuilder();
        for (int i = 0; i < input.length(); i++) {
            if (input.charAt(i) != ' ') {
                word.append(input.charAt(i));
            } else {
                result.append(word.reverse());
                result.append(" ");
                word.setLength(0);
            }
        }
        result.append(word.reverse());
        return result.toString();
    }
}
复杂度分析

时间复杂度： O(n)O(n) 。单遍循环的上限是 nn ，其中 nn 是字符串的长度。
空间复杂度： O(n)O(n) 。 resultresult 和 wordword 最多为 nn 。

作者：LeetCode
链接：https://leetcode-cn.com/problems/reverse-words-in-a-string-iii/solution/fan-zhuan-zi-fu-chuan-zhong-de-dan-ci-iii-by-leetc/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。