给你一个有效的 IPv4 地址 address，返回这个 IP 地址的无效化版本。

所谓无效化 IP 地址，其实就是用 "[.]" 代替了每个 "."。

 

示例 1：

输入：address = "1.1.1.1"
输出："1[.]1[.]1[.]1"
示例 2：

输入：address = "255.100.50.0"
输出："255[.]100[.]50[.]0"
 

提示：

给出的 address 是一个有效的 IPv4 地址


解题思路
此题主要考察两个知识点

表层的知识点是简单的字符串替换

隐藏的知识点是考察了在字符串替换中可能需要用到的正则表达式，由于正则表达中 "." 是一个特殊字符，所以在替换IP地址中的 "." 时需要转义。除了 "."，正则表达式中的特殊字符还有 ".$|()[{^?*+\" 等等

Java版本示例代码解析题库：https://github.com/llyer/leetcode

参考链接：https://www.cnblogs.com/chevin/p/9241468.html

代码
class Solution {
    public String defangIPaddr(String address) {
        String[] splits = address.split("\\.");
        StringBuffer stringBuffer = new StringBuffer();
        for (String split : splits) {
            stringBuffer.append(split + "[.]");
        }
        return stringBuffer.toString().substring(0, stringBuffer.length() - 3);
    }
}

作者：mian-tiao-xian-sheng
链接：https://leetcode-cn.com/problems/defanging-an-ip-address/solution/ip-di-zhi-wu-xiao-hua-de-jie-ti-si-lu-by-mian-tiao/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。