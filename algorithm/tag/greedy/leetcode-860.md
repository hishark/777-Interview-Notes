# LEETCODE 860. 柠檬水找零

## 1. [问题](https://leetcode-cn.com/problems/lemonade-change/)

在柠檬水摊上，每一杯柠檬水的售价为 5 美元。

顾客排队购买你的产品，（按账单 bills 支付的顺序）一次购买一杯。

每位顾客只买一杯柠檬水，然后向你付 5 美元、10 美元或 20 美元。你必须给每个顾客正确找零，也就是说净交易是每位顾客向你支付 5 美元。

注意，一开始你手头没有任何零钱。

如果你能给每位顾客正确找零，返回 true ，否则返回 false 。

**示例 1：**

```text
输入：[5,5,5,10,20]
输出：true
解释：
前 3 位顾客那里，我们按顺序收取 3 张 5 美元的钞票。
第 4 位顾客那里，我们收取一张 10 美元的钞票，并返还 5 美元。
第 5 位顾客那里，我们找还一张 10 美元的钞票和一张 5 美元的钞票。
由于所有客户都得到了正确的找零，所以我们输出 true。
```

**示例 2：**

```text
输入：[5,5,10]
输出：true
```

**示例 3：**

```text
输入：[10,10]
输出：false
```

**示例 4：**

```text
输入：[5,5,10,10,20]
输出：false
解释：
前 2 位顾客那里，我们按顺序收取 2 张 5 美元的钞票。
对于接下来的 2 位顾客，我们收取一张 10 美元的钞票，然后返还 5 美元。
对于最后一位顾客，我们无法退回 15 美元，因为我们现在只有两张 10 美元的钞票。
由于不是每位顾客都得到了正确的找零，所以答案是 false。
```

**提示：**

* `0 <= bills.length <= 10000`
* `bills[i]` 不是 `5` 就是 `10` 或是 `20` 

## 2. 标签

* 贪心
* 模拟

## 3. 解法 - 贪心 模拟

### 3.1 Java

```java
class Solution {
    public boolean lemonadeChange(int[] bills) {
        // 当前手中持有的 5 美元钞票的张数
        int five = 0;
        // 当前手中持有的 10 美元钞票的张数
        int ten = 0;
        // 遍历账单
        for (int bill : bills) {
            // 碰到了最喜欢的 5 美元钞票，无需找零，计数即可
            if (bill == 5) {
                five++;
            } else if (bill == 10) {
                // 碰到了 10 美元，需要找 5 美元
                if (five == 0) {
                    // 如果没得找，直接返回 false
                    return false;
                }
                // 如果有 5 美元的钞票就找给客人，然后减少数量
                five--;
                // 别忘记此时还的得到了一张 10 美元的钞票
                ten++;
            } else {
                // 碰到了最烦人的 20 美元
                if (five > 0 && ten > 0) {
                    // 如果 5 和 10 都有，皆大欢喜
                    five--;
                    ten--;
                } else if (five >= 3) {
                    // 如果有三张 5 美元的，也可以找回
                    // 使用到 5 美元的场景更多所以 10+5 的找钱方案优先，三个 5 的方案靠后
                    five -= 3;
                } else {
                    // 以上都没有，直接返回 false
                    return false;
                }
            }
        }
        // 遍历完所有的账单都成功找回了，返回 true
        return true;
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(N)` ：其中 N 是数组的长度。
* 空间复杂度 `O(1)` ：仅占用了常数大小的空间。

## 4. 参考

* [https://leetcode-cn.com/problems/lemonade-change/](https://leetcode-cn.com/problems/lemonade-change/)
* [https://leetcode-cn.com/problems/lemonade-change/solution/ning-meng-shui-zhao-ling-by-leetcode-sol-nvp7/](https://leetcode-cn.com/problems/lemonade-change/solution/ning-meng-shui-zhao-ling-by-leetcode-sol-nvp7/)

