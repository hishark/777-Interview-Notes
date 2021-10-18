# LEETCODE 205. 同构字符串

## 1. [问题](https://leetcode-cn.com/problems/isomorphic-strings/)

给定两个字符串 s 和 t，判断它们是否是同构的。

如果 s 中的字符可以被替换得到 t ，那么这两个字符串是同构的。

所有出现的字符都必须用另一个字符替换，同时保留字符的顺序。两个字符不能映射到同一个字符上，但字符可以映射自己本身。

**示例 1:**

```
输入: s = "egg", t = "add"
输出: true
```

**示例 2:**

```
输入: s = "foo", t = "bar"
输出: false
```

**示例 3:**

```
输入: s = "paper", t = "title"
输出: true
```

**说明:**

* 你可以假设 _**s **_和 _**t **_具有相同的长度。

## 2. 标签

* 哈希表

## 3. 解法 - 哈希表

### 3.1 Java

```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        // 判空
        if(s==null || t==null){
            return false;
        }
        // 同构字符串需要满足：
        //  1. s 的任意一个字符能被 t 中唯一的字符所对应
        //  2. t 的任意一个字符能被 s 中唯一的字符所对应  
        return inverse(s, t) & inverse(t, s);
    }

    // 判断 s 的任意一个字符是否被 t 中唯一的字符所对应
    public boolean inverse(String s, String t) {
        // 哈希表
        Map<Character, Character> map = new HashMap<>();
        // 遍历 s 字符串
        for (int i=0;i<s.length();i++) {
            // map的key为s当前的字符，value为t当前的字符，建立一一对应的关系
            if(!map.containsKey(s.charAt(i))) {
                map.put(s.charAt(i), t.charAt(i));
            } else {
                // 如果map里存在key为s[i]的元素，检查其value是否等于t[i]
                // 不相等的话说明对应关系建立失败，直接返回false
                if(map.get(s.charAt(i)) != t.charAt(i)) {
                    return false;
                }
            }
        }
        // 全部遍历完了都没失败就成啦
        return true;
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(n)` ：其中 n 为字符串的长度。需同时遍历一遍字符串 s 和 t 。
* 空间复杂度 `O(m)` ：其中 m 是字符串的字符集大小。哈希表存储字符的空间取决于字符串的字符集大小，最坏情况下每个字符均不相同，需要 `O(m)` 的空间。

## 4. 参考

* [https://leetcode-cn.com/problems/isomorphic-strings/](https://leetcode-cn.com/problems/isomorphic-strings/)
* [https://leetcode-cn.com/problems/isomorphic-strings/solution/tong-gou-zi-fu-chuan-by-leetcode-solutio-s6fd/](https://leetcode-cn.com/problems/isomorphic-strings/solution/tong-gou-zi-fu-chuan-by-leetcode-solutio-s6fd/)
