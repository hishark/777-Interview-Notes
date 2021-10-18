# LEETCODE 830. 较大分组的位置

## 1. [问题](https://leetcode-cn.com/problems/positions-of-large-groups/)

在一个由小写字母构成的字符串 s 中，包含由一些连续的相同字符所构成的分组。

例如，在字符串 s = "abbxxxxzyy" 中，就含有 "a", "bb", "xxxx", "z" 和 "yy" 这样的一些分组。

分组可以用区间 \[start, end] 表示，其中 start 和 end 分别表示该分组的起始和终止位置的下标。上例中的 "xxxx" 分组用区间表示为 \[3,6] 。

我们称所有包含大于或等于三个连续字符的分组为 较大分组 。

找到每一个 较大分组 的区间，按起始位置下标递增顺序排序后，返回结果。

**示例 1：**

```
输入：s = "abbxxxxzzy"
输出：[[3,6]]
解释："xxxx" 是一个起始于 3 且终止于 6 的较大分组。
```

**示例 2：**

```
输入：s = "abc"
输出：[]
解释："a","b" 和 "c" 均不是符合要求的较大分组。
```

**示例 3：**

```
输入：s = "abcdddeeeeaabbbcd"
输出：[[3,5],[6,9],[12,14]]
解释：较大分组为 "ddd", "eeee" 和 "bbb"
```

**示例 4：**

```
输入：s = "aba"
输出：[]
```

**提示：**

* `1 <= s.length <= 1000`
* `s` 仅含小写英文字母

## 2. 标签

* 字符串
* 数组

## 3. 解法

### 3.1 Java

```java
class Solution {
    public List<List<Integer>> largeGroupPositions(String s) {
        // 最终结果
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        // 字符串的长度
        int n = s.length();
        // 我们可以遍历该序列，并记录当前分组的长度。
        // 如果下一个字符与当前字符不同，或者已经枚举到字符串尾部，
        // 就说明当前字符为当前分组的尾部。每次找到当前分组的尾部时，
        // 如果该分组长度达到 3，我们就将其加入答案。

        // 计数器，计算当前分组中的字符个数
        int cnt = 1;
        // 遍历字符串
        for (int i = 0; i < n; i++) {
            // 如果已经遍历到字符串尾部，或者当前字符与下一个字符不同
            // 就说明当前字符是当前分组的尾部
            if (i == n - 1 || s.charAt(i) != s.charAt(i + 1)) {
                // 每次找到当前分组的尾部时，就判断分组长度
                // 如果长度 >= 3，符合要求，加入最终结果中即可
                if (cnt >= 3) {
                    // i 是当前下标
                    // cnt 是当前分组的字符个数
                    // i - cnt + 1 就是分组的起点下标
                    // i 就是分组的终点下标
                    // [i - cnt + 1, i] 即分组
                    res.add(Arrays.asList(i - cnt + 1, i));
                }
                // 接着遍历下一个分组，计数器重新初始化为 1
                cnt = 1;
            } else {
                // 计数器++
                cnt++;
            }
        }
        return res;
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(n)` ：其中 n 是字符串的长度。我们只需要遍历一次该数组。
* 空间复杂度 `O(1)` ：只需要常数的空间来保存若干变量，注意返回值不计入空间复杂度。

## 4. 参考

* [https://leetcode-cn.com/problems/positions-of-large-groups/](https://leetcode-cn.com/problems/positions-of-large-groups/)
* [https://leetcode-cn.com/problems/positions-of-large-groups/solution/jiao-da-fen-zu-de-wei-zhi-by-leetcode-so-fi3n/](https://leetcode-cn.com/problems/positions-of-large-groups/solution/jiao-da-fen-zu-de-wei-zhi-by-leetcode-so-fi3n/)
