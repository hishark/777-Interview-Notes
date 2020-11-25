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
        char[] nums = new char[s.length() * 3];
        int index = 0;

        for (int i=0;i<s.length();i++) {
            if(s.charAt(i) != ' ') {
                nums[index++] = s.charAt(i);
            } else {
                nums[index++] = '%';
                nums[index++] = '2';
                nums[index++] = '0';
            }
        }

        String res = new String(nums, 0, index);
        return res;

    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun replaceSpace(s: String): String {
        val nums = CharArray(s.length * 3)
        var index = 0

        for (i in 0..s.length-1) {
            if (s[i] != ' ') {
                nums[index++] = s[i]
            } else {
                nums[index++] = '%'
                nums[index++] = '2'
                nums[index++] = '0'
            }
        }

        return String(nums, 0, index)
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/)
* [https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/solution/mian-shi-ti-05-ti-huan-kong-ge-by-leetcode-solutio/](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/solution/mian-shi-ti-05-ti-huan-kong-ge-by-leetcode-solutio/)

## 4. 笔记

![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/lcof-05.jpg)

