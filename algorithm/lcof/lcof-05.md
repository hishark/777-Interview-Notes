---
title: 05. 替换空格
date: '2020-08-12T12:57:28.000Z'
tags:
  - kotlin
  - java
  - leetcode
  - 数组
  - 字符串
categories: 算法笔记
---

# 05. 替换空格

## 1. [问题](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/)

请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

示例 1：

```text
输入：s = "We are happy."
输出："We%20are%20happy."
```

限制：

* 0 &lt;= s 的长度 &lt;= 10000

## 2. 解法

### 2.1 Java

```java
class Solution {
    public String replaceSpace(String s) {
        // 首先初始化一个长度为字符串长度三倍的字符数组，即结果数组
        char[] nums = new char[s.length() * 3];
        
        // 结果字符串的下标，初始化为 0
        int index = 0;

        // 遍历字符串中的每一个字符
        for (int i=0;i<s.length();i++) {
            // 字符不为空格，直接放入结果数组
            if(s.charAt(i) != ' ') {
                nums[index++] = s.charAt(i);
            // 碰到空格字符，把 %20 放进去
            } else {
                nums[index++] = '%';
                nums[index++] = '2';
                nums[index++] = '0';
            }
        }
        
        // 从 nums 中取出[0,index)即可
        String res = new String(nums, 0, index);
        return res;

    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun replaceSpace(s: String): String {
        // 首先初始化一个长度为字符串长度三倍的字符数组，即结果数组
        val nums = CharArray(s.length * 3)

        // 结果字符串的下标，初始化为 0
        var index = 0

        // 遍历字符串中的每一个字符
        for (i in 0 until s.length) {
            // 字符不为空格，直接放入结果数组
            if (s[i] != ' ') {
                nums[index++] = s[i]
                // 碰到空格字符，把 %20 放进去
            } else {
                nums[index++] = '%'
                nums[index++] = '2'
                nums[index++] = '0'
            }
        }

        // 从 nums 中取出[0,index)即可
        return String(nums, 0, index)

    }
}
```

### 2.3 复杂度分析

* 时间复杂度 `O(n)` ：对字符串进行了遍历，耗费 `O(n)` 的时间。
* 空间复杂度 `O(n)` ：使用了一个字符串数组。

## 3. 参考

* [https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/)
* [https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/solution/mian-shi-ti-05-ti-huan-kong-ge-by-leetcode-solutio/](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/solution/mian-shi-ti-05-ti-huan-kong-ge-by-leetcode-solutio/)

## 4. 笔记

![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/lcof-05.jpg)

