# LEETCODE 205. 同构字符串

[https://leetcode-cn.com/problems/isomorphic-strings/](https://leetcode-cn.com/problems/isomorphic-strings/) 

解法 - 哈希表

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

