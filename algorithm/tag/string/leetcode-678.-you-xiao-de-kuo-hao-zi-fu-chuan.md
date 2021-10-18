# LEETCODE 678. 有效的括号字符串

[题目](https://leetcode-cn.com/problems/valid-parenthesis-string/)

代码

```java
class Solution {
    // 检查括号字符串是否合法
    public boolean checkValidString(String s) {

        // 字符串长度
        int n = s.length();

        // 借助两个辅助栈
        // leftStack 存 '(' 所在位置的下标
        Stack<Integer> leftStack = new Stack<>();
        // starStack 存 '*' 所在位置的下标
        Stack<Integer> starStack = new Stack<>();

        // 遍历字符串
        for (int i=0;i<n;i++) {
            // 碰到左括号就入栈 leftStack
            if (s.charAt(i) == '(') {
                // 存的是下标
                leftStack.push(i);
            } else if (s.charAt(i) == '*') {
                // 碰到 * 就入栈 statStack
                starStack.push(i);
            } else {
                // 碰到右括号，先判断之前是否碰到过左括号
                if (!leftStack.isEmpty()) {
                    // 存在左括号就将其出栈，与右括号进行匹配
                    leftStack.pop();
                } else {
                    // 若没有左括号，继续判断之前是否碰到过 *
                    if (!starStack.isEmpty()) {
                        // 存在 * 就将其出栈，与右括号进行匹配
                        starStack.pop();
                    } else {
                        // 既不存在左括号，也不存在*，说明该右括号无法匹配，返回false即可
                        return false;
                    }
                }
            }
        }

        // 遍历完了所有字符串，还有剩余的左括号未匹配，但是 * 不够了，那么一定无法匹配，返回false即可
        if (starStack.size() < leftStack.size()) {
            return false;
        } else {
            // 当两个栈都不为空的时候进入循环判断
            while (!starStack.isEmpty() && !leftStack.isEmpty()) {
                // 如果 * 在 左括号 之前，那么无法匹配
                if (starStack.peek() < leftStack.peek()) {
                    return false;
                }
                // 如果 * 在左括号之后，就可以作为一个右括号和左括号进行匹配，一起出栈表示匹配成功
                starStack.pop();
                leftStack.pop();
            }
            // 当leftStack为空时，starStack可能为空，也可能不为空
            // 空不空都可以匹配成功，因为 * 可以代表空串，空串是被视为有效字符串的
            return true;
        }
    }
}

// ref：https://leetcode-cn.com/problems/valid-parenthesis-string/solution/you-xiao-de-gua-hao-zi-fu-chuan-zhan-lia-w0n2/
```



[参考](https://leetcode-cn.com/problems/valid-parenthesis-string/solution/you-xiao-de-gua-hao-zi-fu-chuan-zhan-lia-w0n2/)
