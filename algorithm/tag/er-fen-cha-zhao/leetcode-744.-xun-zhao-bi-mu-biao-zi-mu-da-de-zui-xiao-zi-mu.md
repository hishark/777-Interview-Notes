# LEETCODE 744. 寻找比目标字母大的最小字母

## 1. [问题](https://leetcode-cn.com/problems/find-smallest-letter-greater-than-target/)

给你一个排序后的字符列表 letters ，列表中只包含小写英文字母。另给出一个目标字母 target，请你寻找在这一有序列表里比目标字母大的最小字母。

在比较时，字母是依序循环出现的。举个例子：

* 如果目标字母 target = 'z' 并且字符列表为 letters = \['a', 'b'\]，则答案返回 'a'

**示例：**

```text
输入:
letters = ["c", "f", "j"]
target = "a"
输出: "c"

输入:
letters = ["c", "f", "j"]
target = "c"
输出: "f"

输入:
letters = ["c", "f", "j"]
target = "d"
输出: "f"

输入:
letters = ["c", "f", "j"]
target = "g"
输出: "j"

输入:
letters = ["c", "f", "j"]
target = "j"
输出: "c"

输入:
letters = ["c", "f", "j"]
target = "k"
输出: "c"
```

**提示：**

letters长度范围在\[2, 10000\]区间内。 letters 仅由小写字母组成，最少包含两个不同的字母。 目标字母target 是一个小写字母。

## 2. 标签

* 二分查找

## 3. 解法 - 记录是否存在

### 3.1 Java

```java
class Solution {
    public char nextGreatestLetter(char[] letters, char target) {
        // 记录某个字母是否存在
        boolean[] exist = new boolean[26];
        for (char c : letters) {
            exist[c - 'a'] = true;
        }

        while (true) {
            // 记得++，要找的是target之后的字符
            target++;

            // 如果越界了就回到最初的起点
            if (target > 'z')
                target = 'a';

            if (exist[target - 'a'])
                return target;
        }
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun nextGreatestLetter(letters: CharArray, target: Char): Char {
        var target = target
        // 记录某个字母是否存在
        val exist = BooleanArray(26)
        for (c in letters) {
            exist[c - 'a'] = true
        }

        while (true) {
            // 记得++，要找的是target之后的字符
            target++

            // 如果越界了就回到最初的起点
            if (target > 'z')
                target = 'a'

            if (exist[target - 'a'])
                return target
        }
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(N)` ：其中 N 是 letters 的长度，本解法对数组进行了扫描。
* 空间复杂度 `O(1)` ：exist 数组仅占用了常数大小的额外存储空间。

## 4. 解法 - 二分查找

### 4.1 Java

```java
class Solution {
    public char nextGreatestLetter(char[] letters, char target) {
        int left = 0;
        int right = letters.length;
        
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (letters[mid] <= target)
                left = mid + 1;
            else
                right = mid;
        } 
        // 如果越界了就取模
        return letters[left % letters.length];
    }
}
```

### 4.2 Kotlin

```kotlin
class Solution {
    fun nextGreatestLetter(letters: CharArray, target: Char): Char {
        var left = 0
        var right = letters.size

        while (left < right) {
            val mid = left + (right - left) / 2
            if (letters[mid] <= target)
                left = mid + 1
            else
                right = mid
        }
        // 如果越界了就取模
        return letters[left % letters.size]
    }
}
```

### 4.3 复杂度分析

* 时间复杂度 `O(logn)` ：搜索空间每次循环都会减少一半，二分查找的时间复杂度为对数级别。
* 空间复杂度 `O(1)` ：变量仅占用了常数大小的额外存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/find-smallest-letter-greater-than-target/](https://leetcode-cn.com/problems/find-smallest-letter-greater-than-target/)
* [https://leetcode-cn.com/problems/find-smallest-letter-greater-than-target/solution/xun-zhao-bi-mu-biao-zi-mu-da-de-zui-xiao-zi-mu-by-/](https://leetcode-cn.com/problems/find-smallest-letter-greater-than-target/solution/xun-zhao-bi-mu-biao-zi-mu-da-de-zui-xiao-zi-mu-by-/)

