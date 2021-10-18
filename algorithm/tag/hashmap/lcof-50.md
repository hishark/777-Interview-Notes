# LCOF 50. 第一个只出现一次的字符

## 1. [问题](https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/)

在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

**示例:**

```
s = "abaccdeff"
返回 "b"

s = "" 
返回 " "
```

**限制：**

* `0 <= s 的长度 <= 50000`

## 2. 标签

* 哈希表
* 有序哈希表

## 3. 解法 - 哈希表

### 3.1 Java

```java
class Solution {
    public char firstUniqChar(String s) {
        // 哈希表
        // key: 字符
        // value: true代表字符数量为1，false代表字符数量大于1
        HashMap<Character, Boolean> hashmap = new HashMap<>();

        // 把字符串转换为字符数组
        char[] ch = s.toCharArray();

        // 遍历所有字符
        for (char c : ch) {
            // 如果哈希表中不包含当前字符的话，则当前字符目前只有一个，哈希值为 true 。
            // 如果哈希表中包含当前字符的话，则当前字符目前大于一个，哈希值为 false 。
            hashmap.put(c, !hashmap.containsKey(c));
        }

        // 再遍历一遍字符，找到了哈希值为 true （即字符只有一个） 的字符直接返回即可
        for (char c : ch) {
            if (hashmap.get(c))
                return c;
        }

        // 不存在的话就返回单空格
        return ' ';
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun firstUniqChar(s: String): Char {
        // 哈希表
        // key: 字符
        // value: true代表字符数量为1，false代表字符数量大于1
        val hashmap = HashMap<Char, Boolean>()

        // 把字符串转换为字符数组
        val ch = s.toCharArray()

        // 遍历所有字符
        for (c in ch) {
            // 如果哈希表中不包含当前字符的话，则当前字符目前只有一个，哈希值为 true 。
            // 如果哈希表中包含当前字符的话，则当前字符目前大于一个，哈希值为 false 。
            hashmap[c] = !hashmap.containsKey(c)
        }

        // 再遍历一遍字符，找到了哈希值为 true （即字符只有一个） 的字符直接返回即可
        for (c in ch) {
            if (hashmap[c] == true)
                return c
        }

        // 不存在的话就返回单空格
        return ' '
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(N)` ：N 是字符串的长度，总共遍历字符串两轮，时间复杂度为 `O(N)` 。哈希表查找操作的时间复杂度为 `O(1)` 。所以总的时间复杂度为 `O(N)` 。
* 空间复杂度 `O(1)` ：按照题意，哈希表中最多存储 26 个小写字母，占用常数大小的存储空间。

## 4. 解法 - 有序哈希表

> 有序哈希表中的键值对是按照插入顺序排序的。由于哈希表是去重的，法 1 中的第二个遍历是遍历所有字符，法 2 中的第二个遍历是遍历哈希表，所以当字符串非常非常非常长的时候，法 2 会比法 1 减少第二个遍历中的循环次数，效率更高。

### 4.1 Java

```java
// 有序哈希表
class Solution {
    public char firstUniqChar(String s) {
        // 有序哈希表
        Map<Character, Boolean> map = new LinkedHashMap<>();

        // 将字符串转换为字符数组
        char[] ch = s.toCharArray();

        // 遍历所有字符
        for (char c : ch) {
            // 如果哈希表中不包含当前字符的话，则当前字符目前只有一个，哈希值为 true 。
            // 如果哈希表中包含当前字符的话，则当前字符目前大于一个，哈希值为 false 。
            map.put(c, !map.containsKey(c));
        }

        // 遍历有序哈希表，找到第一个哈希值为 true （即字符只有一个）的字符直接返回即可
        for (Map.Entry<Character, Boolean> entry : map.entrySet()) {
            if (entry.getValue())
                return entry.getKey();
        }

        // 不存在的话就返回单空格
        return ' ';
    }
}
```

### 4.2 Kotlin

```kotlin
class Solution {
    fun firstUniqChar(s: String): Char {
        // 有序哈希表
        val map = LinkedHashMap<Char, Boolean>()

        // 将字符串转换为字符数组
        val ch = s.toCharArray()

        // 遍历所有字符
        for (c in ch) {
            // 如果哈希表中不包含当前字符的话，则当前字符目前只有一个，哈希值为 true 。
            // 如果哈希表中包含当前字符的话，则当前字符目前大于一个，哈希值为 false 。
            map[c] = !map.containsKey(c)
        }

        // 遍历有序哈希表，找到第一个哈希值为 true （即字符只有一个）的字符直接返回即可
        for ((key, value) in map) {
            if (value)
                return key
        }

        // 不存在的话就返回单空格
        return ' '
    }
}
```

### 4.3 复杂度分析

* 时间复杂度 `O(N)` ：N 是字符串的长度，总共遍历字符串一轮，遍历哈希表一轮（哈希表长度不大于 26 ），时间复杂度为 `O(N)` 。哈希表查找操作的时间复杂度为 `O(1)` 。所以总的时间复杂度为 `O(N)` 。
* 空间复杂度 `O(1)` ：按照题意，哈希表中最多存储 26 个小写字母，占用常数大小的存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/](https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/)
* [https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/solution/mian-shi-ti-50-di-yi-ge-zhi-chu-xian-yi-ci-de-zi-3/](https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/solution/mian-shi-ti-50-di-yi-ge-zhi-chu-xian-yi-ci-de-zi-3/)
