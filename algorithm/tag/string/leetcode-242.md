# LEETCODE 242. 有效的字母异位词

## 1. [问题](https://leetcode-cn.com/problems/valid-anagram/)

给定两个字符串 _s_ 和 _t_ ，编写一个函数来判断 _t_ 是否是 _s_ 的字母异位词。

**示例 1:**

```
输入: s = "anagram", t = "nagaram"
输出: true
```

**示例 2:**

```
输入: s = "anagram", t = "nagaram"
输出: true
```

**说明:**\
你可以假设字符串只包含小写字母。

**进阶:**\
如果输入字符串包含 unicode 字符怎么办？你能否调整你的解法来应对这种情况？

## 2. 标签

* 排序
* 哈希表
* 字符串

## 3. 解法 - 排序

### 3.1 Java

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        /**
         * t 是 s 的字母异位词等价于「两个字符串排序后相等」
         * 所以可以对两个字符串分别排序，看排序后的字符串是否相等即可判断
         */

        // 如果两个字符串的长度不同，必然不互为字母异位词
        if (s.length() != t.length()) 
            return false;

        // 把字符串转换为字符数组
        char[] s1 = s.toCharArray();
        char[] t1 = t.toCharArray();

        // 对字符串进行排序
        Arrays.sort(s1);
        Arrays.sort(t1);

        // 判断排序后的字符串是否相同即可
        return Arrays.equals(s1, t1);

    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun isAnagram(s: String, t: String): Boolean {
        /**
         * t 是 s 的字母异位词等价于「两个字符串排序后相等」
         * 所以可以对两个字符串分别排序，看排序后的字符串是否相等即可判断
         */

        // 如果两个字符串的长度不同，必然不互为字母异位词
        if (s.length != t.length)
            return false

        // 把字符串转换为字符数组
        val s1 = s.toCharArray()
        val t1 = t.toCharArray()

        // 对字符串进行排序
        Arrays.sort(s1)
        Arrays.sort(t1)

        // 判断排序后的字符串是否相同即可
        return Arrays.equals(s1, t1)

    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(nlogn)` ：其中 n 为 s 的长度。排序的时间复杂度为 `O(nlogn)`，比较两个字符串是否相等时间复杂度为 `O(n)`，因此总体时间复杂度为 `O(nlogn+n)=O(nlogn)`。
* 空间复杂度 `O(logn)` ：排序需要 `O(logn)` 的空间复杂度

## 4. 解法 - 哈希表

### 4.1 Java

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        /**
         * t 是 s 的异位词等价于「两个字符串中字符出现的种类和次数均相等」
         * 由于字符串只包含 26 个小写字母，所以可以维护一个长度为 26 的数组
         */

         // 如果两个字符串的长度不同，必然不互为字母异位词
        if (s.length() != t.length()) 
            return false;

        // 使用一个数组记录字符出现的次数
        int[] count = new int[26];

        // 遍历字符串 s，计算字符串 s 中所有字符出现的次数
        for (int i=0;i<s.length();i++) {
            count[s.charAt(i) - 'a']++;
        }

        // 遍历字符串 t，减去 count 数组中对应的次数
        // 如果出现小于 0 的情况，说明 t 中包含一个不在 s 中的额外字符
        for (int i=0;i<t.length();i++) {
            count[t.charAt(i) - 'a']--;
            if (count[t.charAt(i) - 'a'] < 0)
                return false;
        }

        // 遍历完字符串 t 没出现小于零的情况就直接返回 true 啦
        return true;
    }
}
```

### 4.2 Kotlin

```kotlin
class Solution {
    fun isAnagram(s: String, t: String): Boolean {
        /**
         * t 是 s 的异位词等价于「两个字符串中字符出现的种类和次数均相等」
         * 由于字符串只包含 26 个小写字母，所以可以维护一个长度为 26 的数组
         */

        // 如果两个字符串的长度不同，必然不互为字母异位词
        if (s.length != t.length)
            return false

        // 使用一个数组记录字符出现的次数
        val count = IntArray(26)

        // 遍历字符串 s，计算字符串 s 中所有字符出现的次数
        for (i in 0 until s.length) {
            count[s[i] - 'a']++
        }

        // 遍历字符串 t，减去 count 数组中对应的次数
        // 如果出现小于 0 的情况，说明 t 中包含一个不在 s 中的额外字符
        for (i in 0 until t.length) {
            count[t[i] - 'a']--
            if (count[t[i] - 'a'] < 0)
                return false
        }

        // 遍历完字符串 t 没出现小于零的情况就直接返回 true 啦
        return true
    }
}
```

### 4.3 复杂度分析

* 时间复杂度 `O(n)` ：其中 n 为 s 的长度。
* 空间复杂度 `O(S)` ：其中 S 为字符集大小，此处 S=26。

## 5. 参考

* [https://leetcode-cn.com/problems/valid-anagram/](https://leetcode-cn.com/problems/valid-anagram/)
* [https://leetcode-cn.com/problems/valid-anagram/solution/you-xiao-de-zi-mu-yi-wei-ci-by-leetcode-solution/](https://leetcode-cn.com/problems/valid-anagram/solution/you-xiao-de-zi-mu-yi-wei-ci-by-leetcode-solution/)
