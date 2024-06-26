# LEETCODE 12. 整数转罗马数字

## 1. [问题](https://leetcode-cn.com/problems/integer-to-roman/)

罗马数字包含以下七种字符： I， V， X， L，C，D 和 M。

```
字符          数值
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

例如，罗马数字2写做 II ，即为两个并列的1。12写做 XII ，即为 X + II 。27写做 XXVII, 即为 XX + V + II 。

通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，例如 4 不写做 IIII，而是 IV。数字 1 在数字 5 的左边，所表示的数等于大数 5 减小数 1 得到的数值 4 。同样地，数字 9 表示为 IX。这个特殊的规则只适用于以下六种情况：

* I 可以放在 V (5) 和 X (10) 的左边，来表示 4 和 9。 
* X 可以放在 L (50) 和 C (100) 的左边，来表示 40 和 90。 
* C 可以放在 D (500) 和 M (1000) 的左边，来表示 400 和 900。 

给定一个整数，将其转为罗马数字。输入确保在 1 到 3999 的范围内。

示例 1:

```
输入: 3
输出: "III"
```

示例 2:

```
输入: 4
输出: "IV"
```

示例 3:

```
输入: 9
输出: "IX"
```

示例 4:

```
输入: 58
输出: "LVIII"
解释: L = 50, V = 5, III = 3.
```

示例 5:

```
输入: 1994
输出: "MCMXCIV"
解释: M = 1000, CM = 900, XC = 90, IV = 4.
```

## 2. 标签

* 字符串
* 贪心
* 数学

## 3. 解法 - 贪心

### 3.1 Java

```java
class Solution {
    // 从大到小遍历
    int[] values = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};    
    String[] symbols = {"M","CM","D","CD","C","XC","L","XL","X","IX","V","IV","I"};

    public String intToRoman(int num) {
        // 最终结果
        StringBuilder res = new StringBuilder();
        // 从大到小遍历每一个符号，直到 num 变成 0
        for (int i = 0; i < values.length && num >= 0; i++) {
            // 当前罗马数字如果小于等于 num，就从 num 中减去当前罗马数字
            // 并且把该罗马数字加入到结果中
            while (values[i] <= num) {
                num -= values[i];
                res.append(symbols[i]);
            }
        }
        // 返回结果即可
        return res.toString();
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(1)` ：罗马数字数量是有限的，所以为常数时间复杂度。
* 空间复杂度 `O(1)` ：使用的内存量不会随输入整数的大小而改变，因此是常数的。

## 4. 参考

* [https://leetcode-cn.com/problems/integer-to-roman/](https://leetcode-cn.com/problems/integer-to-roman/)
* [https://leetcode-cn.com/problems/integer-to-roman/solution/zheng-shu-zhuan-luo-ma-shu-zi-by-leetcode/](https://leetcode-cn.com/problems/integer-to-roman/solution/zheng-shu-zhuan-luo-ma-shu-zi-by-leetcode/)
