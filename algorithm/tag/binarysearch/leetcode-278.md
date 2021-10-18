# LEETCODE 278. 第一个错误的版本

## 1. [问题](https://leetcode-cn.com/problems/first-bad-version/)

你是产品经理，目前正在带领一个团队开发新的产品。不幸的是，你的产品的最新版本没有通过质量检测。由于每个版本都是基于之前的版本开发的，所以错误的版本之后的所有版本都是错的。

假设你有 n 个版本 \[1, 2, ..., n]，你想找出导致之后所有版本出错的第一个错误的版本。

你可以通过调用 bool isBadVersion(version) 接口来判断版本号 version 是否在单元测试中出错。实现一个函数来查找第一个错误的版本。你应该尽量减少对调用 API 的次数。

**示例：**

```
给定 n = 5，并且 version = 4 是第一个错误的版本。

调用 isBadVersion(3) -> false
调用 isBadVersion(5) -> true
调用 isBadVersion(4) -> true

所以，4 是第一个错误的版本。 
```

## 2. 标签

* 二分查找

## 3. 解法 - 二分查找

### 3.1 Java

```java
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int left = 1;
        int right = n;
        while (left < right) {
            // 求中点
            int mid = left + (right - left) / 2;
            // 判断是不是错误版本
            if (isBadVersion(mid)) {
                // 如果是错误版本，说明其他的错误版本都在左边
                right = mid;
            } else {
                // 如果不是错误版本，说明错误版本一定在之后才出现，也就是右边
                left = mid + 1;
            }
        }
        // 返回 right 也一样
        return left;
    }
}
```

### 3.2 Kotlin

```kotlin
/* The isBadVersion API is defined in the parent class VersionControl.
      def isBadVersion(version: Int): Boolean = {} */

class Solution: VersionControl() {
    override fun firstBadVersion(n: Int) : Int {
        var left = 1
        var right = n
        while (left < right) {
            // 求中点
            val mid = left + (right - left) / 2
            // 判断是不是错误版本
            if (isBadVersion(mid)) {
                // 如果是错误版本，说明其他的错误版本都在左边
                right = mid
            } else {
                // 如果不是错误版本，说明错误版本一定在之后才出现，也就是右边
                left = mid + 1
            }
        }
        // 返回 right 也一样
        return left
	}
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(logn)` ：搜索空间每次循环都会减少一半，二分查找的时间复杂度为对数级别。
* 空间复杂度 `O(1)` ：变量仅占用了常数大小的额外存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/first-bad-version/](https://leetcode-cn.com/problems/first-bad-version/)
* [https://leetcode-cn.com/problems/first-bad-version/solution/di-yi-ge-cuo-wu-de-ban-ben-by-leetcode/](https://leetcode-cn.com/problems/first-bad-version/solution/di-yi-ge-cuo-wu-de-ban-ben-by-leetcode/)
