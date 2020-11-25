# LCOF 20. 表示数值的字符串

## 1. [问题](https://leetcode-cn.com/problems/biao-shi-shu-zhi-de-zi-fu-chuan-lcof/)

请实现一个函数用来判断字符串是否表示数值（包括整数和小数）。例如，字符串"+100"、"5e2"、"-123"、"3.1416"、"-1E-16"、"0123"都表示数值，但"12e"、"1a3.14"、"1.2.3"、"+-5"及"12e+5.4"都不是。

## 2. 解法

### 2.1 Java

```java
class Solution {
    // 全局索引
    public int index = 0;

    public boolean isNumber(String s) {
        // 假设字符串的形式为A.BeC或者A.BEC
        // A为整数部分，B为小数部分，C为指数部分，按顺序判断是否包含这三个部分
        //  1. 在字符串最后添加结束标记
        //  2. 使用全局索引index遍历字符串
        //  3. scanInteger扫描有符号整数，用于匹配A和C
        //  4. scanUnsignedInteger扫描无符号整数，用于匹配B
        // 另外需要注意字符串首尾若有空格是合法的

        // 特判
        if (s == null || s.length() == 0) 
            return false;

        // 字符串s是否是一个数字
        boolean isNum = false;

        // Step1: 添加结束标志
        s += '*';

        // Step2: 跳过字符串首部的所有空格（如果存在的话）
        while (s.charAt(index) == ' ')
            index++;

        // Step3: 整数部分
        isNum = scanInteger(s);

        // Step4. 小数部分（如果存在小数点的话）
        if (s.charAt(index) == '.') {
            // 跳过小数点
            index++;
            // 处理小数部分，小数点左右两边只要有一边有数字就合法，所以使用「 || 」
            isNum = scanUnsignedInteger(s) || isNum;
        }

        // Step5. 指数部分（如果存在e或E的话）
        if (s.charAt(index) == 'E' || s.charAt(index) == 'e') {
            // 跳过E或e
            index++;
            // 处理指数部分，e或E的两边都必须有数字，所以使用「 && 」
            isNum = scanInteger(s) && isNum;
        }

        // Step6. 跳过字符串尾部的所有空格（如果存在的话）
        while (s.charAt(index) == ' ') 
            index++;

        // Step7. 看是否遍历到了字符串最后，如果没有到最后的话，一定不是一个数字
        // 如果遍历到了最后且isNum为true，那么s就是一个数字
        isNum = isNum && s.charAt(index) == '*';

        return isNum;

    }

    // 扫描无符号整数，用于匹配B（小数部分）
    // 判断字符串内是否包含无符号数
    public boolean scanUnsignedInteger(String str) {
        // 记下最开始的位置
        int start = index;
        // 是数字就一直遍历下去
        while(str.charAt(index) >= '0' && str.charAt(index) <= '9')
            index++;
        // 若index>start说明发现了无符号整数，否则说明不包含无符号整数
        return index > start;
    }

    // 扫描有符号整数，用于匹配A（整数部分）和C（指数部分）
    // 判断字符串内是否包含有符号整数
    public boolean scanInteger(String str) {
        // 如果是有符号的，跳过这个符号，然后把后面的字符串交给scanUnsignedInteger处理
        if (str.charAt(index) == '+' || str.charAt(index) == '-')
            index++;
        return scanUnsignedInteger(str);        
    }    
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    // 全局索引
    var index = 0

    fun isNumber(s: String?): Boolean {
        var s = s
        // 假设字符串的形式为A.BeC或者A.BEC
        // A为整数部分，B为小数部分，C为指数部分，按顺序判断是否包含这三个部分
        //  1. 在字符串最后添加结束标记
        //  2. 使用全局索引index遍历字符串
        //  3. scanInteger扫描有符号整数，用于匹配A和C
        //  4. scanUnsignedInteger扫描无符号整数，用于匹配B
        // 另外需要注意字符串首尾若有空格是合法的

        // 特判
        if (s == null || s.length == 0)
            return false

        // 字符串s是否是一个数字
        var isNum = false

        // Step1: 添加结束标志
        s += '*'.toString()

        // Step2: 跳过字符串首部的所有空格（如果存在的话）
        while (s[index] == ' ')
            index++

        // Step3: 整数部分
        isNum = scanInteger(s)

        // Step4. 小数部分（如果存在小数点的话）
        if (s[index] == '.') {
            // 跳过小数点
            index++
            // 处理小数部分，小数点左右两边只要有一边有数字就合法，所以使用「 || 」
            isNum = scanUnsignedInteger(s) || isNum
        }

        // Step5. 指数部分（如果存在e或E的话）
        if (s[index] == 'E' || s[index] == 'e') {
            // 跳过E或e
            index++
            // 处理指数部分，e或E的两边都必须有数字，所以使用「 && 」
            isNum = scanInteger(s) && isNum
        }

        // Step6. 跳过字符串尾部的所有空格（如果存在的话）
        while (s[index] == ' ')
            index++

        // Step7. 看是否遍历到了字符串最后，如果没有到最后的话，一定不是一个数字
        // 如果遍历到了最后且isNum为true，那么s就是一个数字
        isNum = isNum && s[index] == '*'

        return isNum

    }

    // 扫描无符号整数，用于匹配B（小数部分）
    // 判断字符串内是否包含无符号数
    fun scanUnsignedInteger(str: String): Boolean {
        // 记下最开始的位置
        val start = index
        // 是数字就一直遍历下去
        while (str[index] >= '0' && str[index] <= '9')
            index++
        // 若index>start说明发现了无符号整数，否则说明不包含无符号整数
        return index > start
    }

    // 扫描有符号整数，用于匹配A（整数部分）和C（指数部分）
    // 判断字符串内是否包含有符号整数
    fun scanInteger(str: String): Boolean {
        // 如果是有符号的，跳过这个符号，然后把后面的字符串交给scanUnsignedInteger处理
        if (str[index] == '+' || str[index] == '-')
            index++
        return scanUnsignedInteger(str)
    }
}
```

> 还有个解法是用有限状态自动机来做的，直接看[K佬的题解](https://leetcode-cn.com/problems/biao-shi-shu-zhi-de-zi-fu-chuan-lcof/solution/mian-shi-ti-20-biao-shi-shu-zhi-de-zi-fu-chuan-y-2/)吧，我看着就不想做OTZ。\#TODO

## 3. 参考

* [https://leetcode-cn.com/problems/biao-shi-shu-zhi-de-zi-fu-chuan-lcof/](https://leetcode-cn.com/problems/biao-shi-shu-zhi-de-zi-fu-chuan-lcof/)
* [https://leetcode-cn.com/problems/biao-shi-shu-zhi-de-zi-fu-chuan-lcof/solution/mian-shi-ti-20-biao-shi-shu-zhi-de-zi-fu-chuan-y-2/](https://leetcode-cn.com/problems/biao-shi-shu-zhi-de-zi-fu-chuan-lcof/solution/mian-shi-ti-20-biao-shi-shu-zhi-de-zi-fu-chuan-y-2/) // 还没看
* [https://leetcode-cn.com/problems/biao-shi-shu-zhi-de-zi-fu-chuan-lcof/solution/zui-jian-dan-si-lu-xiang-xi-zhu-shi-zheng-shu-xiao/](https://leetcode-cn.com/problems/biao-shi-shu-zhi-de-zi-fu-chuan-lcof/solution/zui-jian-dan-si-lu-xiang-xi-zhu-shi-zheng-shu-xiao/)

