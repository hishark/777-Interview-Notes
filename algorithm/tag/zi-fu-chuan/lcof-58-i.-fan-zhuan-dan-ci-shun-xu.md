# lcof-58-i.-fan-zhuan-dan-ci-shun-xu

## 1. [问题](https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/)​ <a id="1-wen-ti"></a>

输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变。为简单起见，标点符号和普通字母一样处理。例如输入字符串"I am a student. "，则输出"student. a am I"。

**示例 1：**

```text
输入: "the sky is blue"输出: "blue is sky the"
```

**示例 2：**

```text
输入: "  hello world!  "输出: "world! hello"解释: 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
```

**示例 3：**

```text
输入: "a good   example"输出: "example good a"解释: 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
```

说明：

* 无空格字符构成一个单词。
* 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
* 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。

## 2. 标签 <a id="2-biao-qian"></a>

* 字符串
* 双指针

## 3. 解法 - 双指针 <a id="3-jie-fa-shuang-zhi-zhen"></a>

### 3.1 Java <a id="3-1-java"></a>

```text
class Solution {    public String reverseWords(String s) {        // 首先，先去除字符串首位的空格        s = s.trim();​        // 倒序遍历字符串，记录当前遍历单词的左右边界 left 和 right        int left = s.length() - 1;        int right = s.length() - 1;​        // 结果字符串        StringBuilder ans = new StringBuilder();​        // 从头到尾，倒序遍历字符串        while (left >= 0) {            // 搜索第一个空格            while(left >= 0 && s.charAt(left) != ' ')                left--;​            // 找到空格之后，把单词加入到结果字符串中            String word = s.substring(left + 1, right + 1) + " ";            ans.append(word);​            // 跳过单词之间的空格（可能有多个）            while(left >= 0 && s.charAt(left) == ' ')                left--;                        // right 继续指向下一个单词的尾部            right = left;        }        // 添加单词时会引入多余的空格，记得去除        return ans.toString().trim();    }}
```

### 3.2 Kotlin <a id="3-2-kotlin"></a>

```text
class Solution {    fun reverseWords(s: String): String {        var s = s        // 首先，先去除字符串首位的空格        s = s.trim { it <= ' ' }​        // 倒序遍历字符串，记录当前遍历单词的左右边界 left 和 right        var left = s.length - 1        var right = s.length - 1​        // 结果字符串        val ans = StringBuilder()​        // 从头到尾，倒序遍历字符串        while (left >= 0) {            // 搜索第一个空格            while (left >= 0 && s[left] != ' ')                left--​            // 找到空格之后，把单词加入到结果字符串中            val word = s.substring(left + 1, right + 1) + " "            ans.append(word)​            // 跳过单词之间的空格（可能有多个）            while (left >= 0 && s[left] == ' ')                left--​            // right 继续指向下一个单词的尾部            right = left        }        // 添加单词时会引入多余的空格，记得去除        return ans.toString().trim { it <= ' ' }    }}
```

### 3.3 复杂度分析 <a id="33-fu-za-du-fen-xi"></a>

* 时间复杂度 `O(N)` ：其中 N 为字符串的长度，需要对字符串进行遍历。
* 空间复杂度 `O(N)` ：结果字符串占用了 `O(N)` 大小的额外存储空间。

## 4. 参考 <a id="4-can-kao"></a>

* ​[https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/](https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/)​
* ​[https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/solution/mian-shi-ti-58-i-fan-zhuan-dan-ci-shun-xu-shuang-z/](https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/solution/mian-shi-ti-58-i-fan-zhuan-dan-ci-shun-xu-shuang-z/)​

[  
](https://hishark777.gitbook.io/android-interview/algorithm/lcof/57-ii.-he-weisde-lian-xu-zheng-shu-xu-lie-todo)

