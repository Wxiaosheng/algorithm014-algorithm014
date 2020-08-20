<h2 id="1">剑指 Offer 40 最小的 k 个数</h2>

输入整数数组 arr ，找出其中最小的 k 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。

### 方法一，sort + slice

```javascript
var getLeastNumbers = function (nums, k) {
    if (nums.length <= k) return nums
    return nums.sort((a, b) => a - b).slice(0, k)
}
```

### 方法二，每次找到数组中的最小值，并从原数组中删除，loop k 次

```javascript
var getLeastNumbers = function (nums, k) {
    if (nums.length <= k) return nums
    const result = []
    while (result.length < k) {
        result.push(nums.splice(nums.indexOf(Math.min(...nums)), 1))
    }
    return result
}
```

### 方法三、使用 堆(heap) 这种数据结构，loop 将所有数都加进去，取最小堆顶部的元素 k 次
> 由于 JavaScript 自身并没有实现这种数据结构，因此需要自己手动实现

```javascript

```