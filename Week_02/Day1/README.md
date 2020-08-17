<h2 id="1">LeetCode 242 有效的字母异位词</h2>

> 异位，其实表达的意思是 组成字符串的字符个数和种类都相同，但是位置顺序不同 (经过 test 发现相等的字符串也会返回 true)

给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的字母异位词。

### 方法一，排序 + 比较是否相等

```javascript
var isAnagram = function (s, t) {
  if (s.length !== t.lenght) return false

  return s.split("").sort().join("") === t.split("").sort().join("")
}
```

### 方法二，loop + hashMap

```javascript
var isAnagram = function (s, t) {
  if (s.length !== t.length) return false
    
  const hashMap = {}
  for (let i = 0; i < s.length; i++) {
    hashMap[s[i]] = hashMap[s[i]] === undefined ? 1 : hashMap[s[i]] + 1
    hashMap[t[i]] = hashMap[t[i]] === undefined ? -1 : hashMap[t[i]] - 1
  }
  return Object.values(hashMap).filter(v => v !== 0).length === 0
}
```


<h2 id="2">LeetCode 49 字母异位词分组</h2>

给定一个字符串数组，将字母异位词组合在一起。字母异位词指字母相同，但排列不同的字符串。

### 思路： 使用 hashMap 存放相同字符串的异位，最后输出相对应的结果

```javascript
var groupAnagrams = function (strs) {
  const hashMap = {}
  for (let i = 0; i < strs.length; i++) {
    const key = strs[i].split("").sort().join()
    if (hashMap[key]) {
      hashMap[key].push(strs[i])
    } else {
      hashMap[key] = [strs[i]]
    }
  }
  return Object.values(hashMap)
};
```

<h2 id="3">LeetCode 1 两数之和</h2>

### 方法一， 暴力循环，枚举所有的组合情况

### 方法二，loop + hash table
```javascript
var towSum = function (nums, target) {
  if (nums.length < 2) return []
  const hashMap = {}
  for (let i = 0; i < nums.length; i++) {
    if (hashMap[nums[i]] !== undefined) {
      return [hashMap[nums[i]], i]
    }
    hashMap[target - nums[i]] = i
  }
  return []
}
```

<h2 id="4">LeetCode 18 四数之和</h2>
给定一个包含 n 个整数的数组 nums 和一个目标值 target，判断 nums 中是否存在四个元素 a，b，c 和 d ，使得 a + b + c + d 的值与 target 相等？找出所有满足条件且不重复的四元组。  
 
注意： 答案中不可以包含重复的四元组。

### 思路，其实没有什么特别好的方法，就是在 threeSum 的基础之上，再加一层 loop
> 要特别注意一下一点，foreSum 和 threeSum 代码思路相同，但是 foreSum 千万不能加 判断最小的数大于要判断的数 而直接 break  
这是因为，threeSum 求得三数之和等于 0，而 foreSum 求得四数之和等于指定的 target

```javascript
var foreSum = function (nums, target) {
  if (nums.length < 4) return []
  const result = []
  nums = nums.sort((a, b) => a - b)
  // 多一层 loop
  for (let a = 0; a < nums.length - 3; a++) {
    if (a > 0 && nums[a] === nums[a - 1]) continue
    // three Sum 写法
    for (let b = a + 1; b < nums.length - 2; b++) {
      if (b > a + 1 && nums[b] === nums[b - 1]) continue;
      let c = b + 1, d = nums.length - 1;
      while (c < d) {
        const curr = nums[a] + nums[b] + nums[c] + nums[d]
        if (curr === target) {
          result.push([nums[a], nums[b], nums[c], nums[d]])
          c++, d--
          while (c < d && nums[c] === nums[c - 1]) c++
          while (c < d && nums[d] === nums[d + 1]) d--
        }
        if (curr < target) c++
        if (curr > target) d--
      }
    }
  }
  return result
}
```