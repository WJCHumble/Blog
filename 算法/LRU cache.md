# LRU cache

>背下一些基础解题的代码模块、如二分法、DFS、动态规划，将思考的过程省略，直接从 O(n) 的时间复杂度变为 O(1) 的时间复杂度

1.LRU（Least recently used）最近最少使用

2.Double LinkedList

3.O(1) 查询

4.O(1) 修改、更新

LFU（least frequently used） Cache 最近最不常用页面置换算法

## LRU 缓存机制

>https://leetcode-cn.com/problems/lru-cache/

**题目描述：**

运用你所掌握的数据结构，设计和实现一个  LRU (最近最少使用) 缓存机制 。
实现 LRUCache 类：

LRUCache(int capacity) 以正整数作为容量 capacity 初始化 LRU 缓存
int get(int key) 如果关键字 key 存在于缓存中，则返回关键字的值，否则返回 -1 。
void put(int key, int value) 如果关键字已经存在，则变更其数据值；如果关键字不存在，则插入该组「关键字-值」。当缓存容量达到上限时，它应该在写入新数据之前删除最久未使用的数据值，从而为新的数据值留出空间。

示例：

输入
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
输出
[null, null, null, 1, null, -1, null, -1, 3, 4]

### 解法一：map

**思路：**


**复杂度分析：**


**代码实现：**

```javascript
/**
 * @param {number} capacity
 */
var LRUCache = function(capacity) {
  this.capacity = capacity
  this.map = new Map()
};

/** 
 * @param {number} key
 * @return {number}
 */
LRUCache.prototype.get = function(key) {
  let val = this.map.get(key)
  if (val === undefined) return -1

  // 因为被用过一次，原有位置删除
  this.map.delete(key)
  // 放入最小面表示最新使用
  this.map.set(key, val)
  return val
};

/** 
 * @param {number} key 
 * @param {number} value
 * @return {void}
 */
LRUCache.prototype.put = function(key, value) {
  // 如果存在，则删除
  if (this.map.has(key)) {
    this.map.delete(key)
  }

  // 放到最下面表示最新使用
  this.map.set(key, val)

  if (this.map.size > this.capacity) {
    this.map.delete(this.map.entries().next().value[0])
  }
};
```


## 解法二：双指针

