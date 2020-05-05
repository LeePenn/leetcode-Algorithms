RGB 颜色用十六进制来表示的话，每个大写字母都代表了某个从 0 到 f 的 16 进制数。

RGB 颜色 "#AABBCC" 可以简写成 "#ABC" 。例如，"#15c" 其实是 "#1155cc" 的简写。

现在，假如我们分别定义两个颜色 "#ABCDEF" 和 "#UVWXYZ"，则他们的相似度可以通过这个表达式 -(AB - UV)^2 - (CD - WX)^2 - (EF - YZ)^2 来计算。

那么给定颜色 "#ABCDEF"，请你返回一个与 #ABCDEF 最相似的 7 个字符代表的颜色，并且它是可以被简写形式表达的。（比如，可以表示成类似 "#XYZ" 的形式）

示例 1：
输入：color = "#09f166"
输出："#11ee66"
解释： 
因为相似度计算得出 -(0x09 - 0x11)^2 -(0xf1 - 0xee)^2 - (0x66 - 0x66)^2 = -64 -9 -0 = -73
这已经是所有可以简写的颜色中最相似的了
注意：

color 是一个长度为 7 的字符串
color 是一个有效的 RGB 颜色：对于仍和 i > 0，color[i] 都是一个在 0 到 f 范围的 16 进制数
假如答案具有相同的（最大）相似度的话，都是可以被接受的
所有输入、输出都必须使用小写字母，并且输出为 7 个字符


方法一：枚举
由于从 #000 到 #fff 一共只有 16^3 = 4096 种颜色，因此我们可以枚举这些颜色，并计算其与 color 的相似度。

在枚举所有的颜色时，我们可以使用三重循环，每一重循环的范围为 0 到 15。设三重循环分别为 R，G 和 B，那么其对应的颜色的十六进制值为 17 * R * (1 << 16) + 17 * G * (1 << 8) + 17 * B，这里的 17 由 0x11 = 16 + 1 = 17 得来，(1 << 16) 和 (1 << 8) 分别为 R 和 G 的左移位数。

在计算两种颜色的相似度时，我们从其十六进制值可以得到三种颜色对应的值，即 r = (hex >> 16) % 256，g = (hex >> 8) % 256 以及 b = hex % 256。随后通过 (r1 - r2)^2 + (g1 - g2)^2 + (b1 - b2)^2 计算相似度。

在枚举完所有的颜色后，我们需要将答案转换为 16 进制输出，此时可以用 Java 或 Python 中的 format，用 06x 表示输出为 6 位的十六进制数（x 表示十六进制），且少于 6 位的高位补 0。

JavaPython
class Solution {
    public String similarRGB(String color) {
        int hex1 = Integer.parseInt(color.substring(1), 16);
        int ans = 0;
        for (int r = 0; r < 16; ++r)
            for (int g = 0; g < 16; ++g)
                for (int b = 0; b < 16; ++b) {
                    int hex2 = 17 * r * (1 << 16) + 17 * g * (1 << 8) + 17 * b;
                    if (similarity(hex1, hex2) > similarity(hex1, ans))
                        ans = hex2;
                }

        return String.format("#%06x", ans);
    }

    public int similarity(int hex1, int hex2) {
        int ans = 0;
        for (int shift = 16; shift >= 0; shift -= 8) {
            int col1 = (hex1 >> shift) % 256;
            int col2 = (hex2 >> shift) % 256;
            ans -= (col1 - col2) * (col1 - col2);
        }
        return ans;
    }
}
复杂度分析

时间复杂度：O(1)O(1)。

空间复杂度：O(1)O(1)。

方法二：独立性 + 枚举
我们可以发现，颜色中的每一维都是独立的，因此我们只需要分别计算出 color = #ABCDEF 中与 AB，CD 和 EF 相似度最大的颜色即可。最终的答案为这三个颜色的结合。

对于 AB，我们要在 00 到 ff 中找到一个相似度最大的。在方法一中我们得知，00 到 ff 均为 17 的倍数，因此我们需要找到一个 17 的倍数，使得其与 AB 的差的绝对值最小。显然，当 AB mod 17 > 8 时，取刚好比 AB 大的那个数；当 AB mod 17 <= 8 时，取刚好比 AB 小或与 AB 相等的那个数。

JavaPython
class Solution {
    public String similarRGB(String color) {
        return "#" + f(color.substring(1, 3)) + f(color.substring(3, 5)) + f(color.substring(5));
    }

    public String f(String comp) {
        int q = Integer.parseInt(comp, 16);
        q = q / 17 + (q % 17 > 8 ? 1 : 0);
        return String.format("%02x", 17 * q);
    }
}
复杂度分析

时间复杂度：O(1)O(1)。

空间复杂度：O(1)O(1)。

作者：LeetCode
链接：https://leetcode-cn.com/problems/similar-rgb-color/solution/xiang-si-rgb-yan-se-by-leetcode/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。