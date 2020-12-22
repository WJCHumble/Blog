# Map

HashMap：以一种无序的方式存储数据，时间复杂度为 O(1)

HashTree：以有序的方式存储数据，时间复杂度为 O(logn)

## 1. 有效的字母异位词

>https://leetcode-cn.com/problems/valid-anagram/

**题目描述:**

给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的字母异位词。

示例：

输入: s = "anagram", t = "nagaram"
输出: true

### 解法一：排序比较

**思路：**

将字符串转为数组，然后对数组排序，

**复杂度分析：**

时间复杂度：O(nlogn)
空间复杂度：O(logn)

> 这里的空间复杂度是因为我们需要对数组进行排序

**代码实现：**

```javascript
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isAnagram = function(s, t) {
    return s.split('').sort().join() === t.split('').sort().join()
};
```

### 解法二：Map 记数

**思路：**

枚举第一个字符串，用 Map 记录每一个字母出现的次数，然后再枚举第二个字符串，判断其对应的字母是否在 Map 中，不是则返回 false，是则对次数减一，并判断是否为 0，是则删除 Map 中对应这个字母的 key。

**复杂度分析：**

时间复杂度：O(n)
空间复杂度：O(n)

**代码实现：**

```javascript
var isAnagram = function(s, t) {
  if (s.length !== t.length) {
    return false
  }
  
  const map = new Map()
  for (let i = 0; i < s.length; i++) {
    if (map.has(s.charAt(i))) {
      let times = map.get(s.charAt(i)) + 1
      map.set(s.charAt(i), times)
    } else {
      map.set(s.charAt(i), 1)
    }
  }
  for (let i = 0; i < t.length; i++) {
    if (map.has(t.charAt(i))) {
      let times = map.get(t.charAt(i)) - 1
      map.set(t.charAt(i), times)
      if (times === 0) {
        map.delete(t.charAt(i))
      }
    } else {
      return false
    }
  }
  return map.size === 0;
};
```