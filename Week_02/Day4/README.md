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

<h2 id="2">LeetCode 347 前 K 个高频元素</h2>

给定一个非空的整数数组，返回其中出现频率前 k 高的元素。

示例 1:  

输入: nums = [1,1,1,2,2,3], k = 2  
输出: [1,2]  

```javascript
// 思路，使用 map 记录每个元素出现的次数，然后根据每个元素出现的次数排序(倒叙)，选取前 k 个元素即可
var topKFrequent = function(nums, k) {
  if (nums.length <= k) return nums
  const map = {}
  nums.forEach(num => map[num] = map[num] === undefined ? 1 : map[num] + 1)
  return Object.entries(map).sort((a, b) => b[1] - a[1]).slice(0, k).map(item => Number(item[0]))
};
```


<h2 id="3">LeetCode 239 滑动窗口最大值</h2>
给定一个数组 nums，有一个大小为 k 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 k 个数字。滑动窗口每次只向右移动一位。

返回滑动窗口中的最大值。  

### 思路，使用一个小的数组，一次从 第K位开始，向后滑动，每次取该数组的最小值，既可得到结果

```javascript
if (nums.length <= 1) return nums
  const window = nums.slice(0, k)
  const result = [Math.max(...window)]
  for (let i = k; i < nums.length; i++) {
    window.shift()
    window.push(nums[i])
    result.push(Math.max(...window))
  }
  return result
```


### 进阶：你能在线性时间复杂度内解决此题吗？
> 本题难的不是问题的求解，而是进阶的解法 (动态规划)

