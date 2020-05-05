给出第一个词 first 和第二个词 second，考虑在某些文本 text 中可能以 "first second third" 形式出现的情况，其中 second 紧随 first 出现，third 紧随 second 出现。

对于每种这样的情况，将第三个词 "third" 添加到答案中，并返回答案。

 

示例 1：

输入：text = "alice is a good girl she is a good student", first = "a", second = "good"
输出：["girl","student"]
示例 2：

输入：text = "we will we will rock you", first = "we", second = "will"
输出：["we","rock"]
 

提示：

1 <= text.length <= 1000
text 由一些用空格分隔的单词组成，每个单词都由小写英文字母组成
1 <= first.length, second.length <= 10
first 和 second 由小写英文字母组成


这道题难度不大，主要是for循环的终止条件，要注意数组越界

class Solution {
    public String[] findOcurrences(String text, String first, String second) {
        String[] words = text.split(" ");
        List<String> res = new LinkedList<>();
        for(int i = 0;i < words.length - 2;i++){
            if(words[i].equals(first) && words[i + 1].equals(second)){
                res.add(words[i + 2]);
            }
        }
        
        return res.toArray(new String[res.size()]);
    }
}

作者：LSZ
链接：https://leetcode-cn.com/problems/occurrences-after-bigram/solution/javashi-xian-by-lsz/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。