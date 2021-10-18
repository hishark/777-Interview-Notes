# LCOF 58 - II. 左旋转字符串

## 1. [问题](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

**示例 1：**

```
输入: s = "abcdefg", k = 2
输出: "cdefgab"
```

**示例 2：**

```
输入: s = "lrloseumgh", k = 6
输出: "umghlrlose"
```

**限制：**

* `1 <= k < s.length <= 10000`

## 2. 标签

* 字符串

## 3. 解法

### 3.1 Java

> 用 StringBuilder 或者 String 都一个路子。

```java
class Solution {
    public String reverseLeftWords(String s, int n) {
        String ans = "";
        for (int i = n; i < s.length(); i++) {
            ans += s.charAt(i);
        }
        for (int i = 0; i < n; i++) {
            ans += s.charAt(i);
        }
        return ans;
    }
}
```

两个循环可以用一个求余操作写在一起：

```
ans += s.charAt(i % s.length());
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun reverseLeftWords(s: String, n: Int): String {
        var ans = ""
        for (i in n until s.length) {
            ans += s[i]
        }
        for (i in 0 until n) {
            ans += s[i]
        }
        return ans
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(N)` ：线性遍历字符串。
* 空间复杂度 `O(N)` ：字符串至少占用 `O(N)` 的额外存储

## 4. 参考

* [https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)
* [https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/solution/mian-shi-ti-58-ii-zuo-xuan-zhuan-zi-fu-chuan-qie-p/](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/solution/mian-shi-ti-58-ii-zuo-xuan-zhuan-zi-fu-chuan-qie-p/)
