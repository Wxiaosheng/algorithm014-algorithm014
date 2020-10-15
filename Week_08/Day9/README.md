## LeetCode 146 LRU缓存机制
运用你所掌握的数据结构，设计和实现一个  LRU (最近最少使用) 缓存机制。它应该支持以下操作： 获取数据 get 和 写入数据 put 。

获取数据 get(key) - 如果关键字 (key) 存在于缓存中，则获取关键字的值（总是正数），否则返回 -1。  

写入数据 put(key, value) - 如果关键字已经存在，则变更其数据值；如果关键字不存在，则插入该组「关键字/值」。当缓存容量达到上限时，它应该在写入新数据之前删除最久未使用的数据值，从而为新的数据值留出空间。

进阶: 你是否可以在 O(1) 时间复杂度内完成这两种操作？

    示例:

      LRUCache cache = new LRUCache( 2 /* 缓存容量 */ );

      cache.put(1, 1);
      cache.put(2, 2);
      cache.get(1);       // 返回  1
      cache.put(3, 3);    // 该操作会使得关键字 2 作废
      cache.get(2);       // 返回 -1 (未找到)
      cache.put(4, 4);    // 该操作会使得关键字 1 作废
      cache.get(1);       // 返回 -1 (未找到)
      cache.get(3);       // 返回  3
      cache.get(4);       // 返回  4

#### 方法一： 使用数组实现
* get: O(1)
* put: O(n)
* 由于是要记录数据缓存的顺序，因此使用 `优先级队列(Priority Queue)` 更加合理

```javascript
class LRUCache {
  constructor (size) {
    this.size = size
    this.cache = {}
    this.queue = []
  }

  get (key) {
    if (!this.cache[key] !== undefined) return -1
    const i = this.queue.indexof(key)
    // 手动维护访问顺序
    this.queue.slice(i, 1)
    this.queue.psuh(key)
    return this.cache[key]
  }

  put (key, value) {
    const i = this.queue.indexof(key)
    if (i > -1) {
      this.queue.slice(i, 1)
    } else {
      if (this.queue.length >= this.size) {
        this.queue.slice(0, 1)
      }
    }
    this.cache[key] = value
    this.queue.push(key)
  }
}
```

#### 方法二：使用 Map 实现
**Map 的keys的顺序，就是元素添加的顺序**

```javascript
class LRUCache {
  constructor (size) {
    this.size = size
    this.cache = new Map()
  }

  get (key) {
    if (!this.cache.has(key)) return -1
    const value = this.cache.get(key)
    // 访问的时候，需要更新访问状态，标识当前的 key 是最近一次访问
    this.cache.delete(key)
    this.cache.set(key, value)
    return value
  }

  put (key, value) {
    if (this.cache.has(key)) {
      this.cache.delete(key)
    } else {
      if (this.cache.size >= this.size) {
        // Map 的 keys 结果的顺序就是 添加时的顺序
        const { value: oldKey } = this.cache.keys().next()
        this.cache.delete(oldKey)
      }
    }
    this.set(key, value)
  }
}
```