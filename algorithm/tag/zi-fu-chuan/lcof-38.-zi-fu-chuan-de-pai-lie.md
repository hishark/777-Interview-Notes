# lcof-38.-zi-fu-chuan-de-pai-lie

## 1. [问题](https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/)

输入一个字符串，打印出该字符串中字符的所有排列。

你可以以任意顺序返回这个字符串数组，但里面不能有重复元素。

示例：

```text
输入：s = "abc"
输出：["abc","acb","bac","bca","cab","cba"]
```

限制：

* 1 &lt;= s 的长度 &lt;= 8

## 2. 标签

* 字符串
* 回溯
* DFS

## 3. 解法

### 3.1 Java

```java
class Solution {
    // 全排列问题
    // 结果列表
    List<String> ans = new LinkedList<>();

    // 所有字符
    char[] chars;

    public String[] permutation(String s) {
        // 把字符串转换为字符
        chars = s.toCharArray();

        // 首先固定第 0 个字符
        dfs(0);

        // 返回结果即可
        // List.toArray(): https://blog.csdn.net/judyfun/article/details/50239127
        return ans.toArray(new String[ans.size()]);
    }

    // 深度优先搜索所有排列方案
    public void dfs(int n) {
        // 递归终止条件： 如果递归到了最后一个字符，就把目前的排列方案加入到结果列表里
        if (n == chars.length - 1) {
            ans.add(String.valueOf(chars));
            return;
        }

        // 初始化一个 set 用于排除重复的字符
        HashSet<Character> set = new HashSet<>();

        for (int i = n; i < chars.length; i++) {
            // set 中如果存在当前字符，说明重复，因而剪枝，继续查看下一个字符
            if (set.contains(chars[i]))
                continue;

            // 把当前字符加入到 set 中
            set.add(chars[i]);

            // 交换 chars[i] 和 chars[x]，将 chars[i] 固定在第 n 位
            swap(i, n);

            // 固定第 n+1 位字符
            dfs(n + 1);

            // 恢复交换，继续查看下一个字符
            swap(i, n);
        }

    }

    // 交换 chars 中位置 x 和 y 上的字符
    public void swap(int x, int y) {
        char tmp = chars[x];
        chars[x] = chars[y];
        chars[y] = tmp;
    }

}
```

### 3.2 Kotlin

```kotlin
class Solution {
    // 全排列问题
    // 结果列表
    var ans: MutableList<String> = LinkedList()

    // 所有字符
    var chars: CharArray = charArrayOf() // 一定要创建空数组，不然报错

    fun permutation(s: String): Array<String> {
        // 把字符串转换为字符
        chars = s.toCharArray()

        // 首先固定第 0 个字符
        dfs(0)

        // 返回结果即可
        // List.toArray(): https://blog.csdn.net/judyfun/article/details/50239127
        return ans.toTypedArray()
    }

    // 深度优先搜索所有排列方案
    fun dfs(n: Int) {
        // 递归终止条件： 如果递归到了最后一个字符，就把目前的排列方案加入到结果列表里
        if (n == chars.size - 1) {
            ans.add(String(chars))
            return
        }

        // 初始化一个 set 用于排除重复的字符
        val set = HashSet<Char>()

        for (i in n until chars.size) {
            // set 中如果存在当前字符，说明重复，因而剪枝，继续查看下一个字符
            if (set.contains(chars[i]))
                continue

            // 把当前字符加入到 set 中
            set.add(chars[i])

            // 交换 chars[i] 和 chars[x]，将 chars[i] 固定在第 n 位
            swap(i, n)

            // 固定第 n+1 位字符
            dfs(n + 1)

            // 恢复交换，继续查看下一个字符
            swap(i, n)
        }

    }

    // 交换 chars 中位置 x 和 y 上的字符
    fun swap(x: Int, y: Int) {
        val tmp = chars[x]
        chars[x] = chars[y]
        chars[y] = tmp
    }

}
```

### 3.3 复杂度分析

* 时间复杂度$$O(N!)$$：其中 N 是字符串的长度，算法的时间复杂度和字符串排列的方案数成线性关系，方案数为 $$N \times (N-1) \times (N-2) \cdots \times 2 \times 1$$ ，所以时间复杂度为 `O(N!)` 。
* 空间复杂度 $$O(N^2)$$：全排列的递归深度为 N ，需要占用栈空间大小为 `O(N)` ，而在递归的过程中，set 中存储的字符数量最多为 $$N+(N-1)+(N-2)+ \cdots + 2 + 1 = (N+1) \times N / 2$$ ，会占用 `O(N^2)` 的额外空间。 

## 4. 参考

* [https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/](https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/)
* [https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/solution/mian-shi-ti-38-zi-fu-chuan-de-pai-lie-hui-su-fa-by/](https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/solution/mian-shi-ti-38-zi-fu-chuan-de-pai-lie-hui-su-fa-by/)

