# 国庆周
> 补上之前拉下的进度 + 适当休息

# 牙疼，拔牙去了，躺了好多天，拉下了很多课程，今天(10月14日) 开始补上

## 实战题目 / 课后作业
* [LeetCode 191 位1的个数](./Day8/README.md#1)（Facebook、苹果在半年内面试中考过）
* [LeetCode 231 2的幂](./Day8/README.md#2)（谷歌、亚马逊、苹果在半年内面试中考过）
* [LeetCode 190 颠倒二进制位](./Day8/README.md#3)（苹果在半年内面试中考过）
* N 皇后（字节跳动、亚马逊、百度在半年内面试中考过）
* N 皇后 II （亚马逊在半年内面试中考过）
* [LeetCode 338 比特位计数](./Day8/README.md#4)（字节跳动、Facebook、MathWorks 在半年内面试中考过）
* [LeetCode 146 LRU缓存机制](.Day9/README.md#1)（亚马逊、字节跳动、Facebook、微软在半年内面试中常考）
* 数组的相对排序（谷歌在半年内面试中考过）
* 有效的字母异位词（Facebook、亚马逊、谷歌在半年内面试中考过）
* 力扣排行榜（此题选做；Bloomberg 在半年内面试中考过）
* 合并区间（Facebook、字节跳动、亚马逊在半年内面试中常考）
* 翻转对（字节跳动在半年内面试中考过）


## 第十六课 位运算
#### 为什么需要位运算
机器里数字的表示方法和储存格式 是二进制的，而人类常用的是 十进制

#### 位预算符
|含义|运算符|示例
|:-|:-|:-
|左移|<<|0011 => 0110
|右移|>>|0110 => 0011
|按位或|\||0011------- => 1011 => 1011
|按位与|&|0011------- => 0011 => 1011
|按位取反|~|0011 => 1100
|按位异或（相同为零不同为一）|^|0011------- => 1000 => 1011


#### 异或
**相同为 0，不同为 1。也可用“不进位加法”来理解**

异或操作的一些特点：
* x ^ 0 = x
* x ^ 1s = ~x // 注意 1s = ~0
* x ^ (~x) = 1s
* x ^ x = 0
* c = a ^ b => a ^ c = b, b ^ c = a // 交换两个数
* a ^ b ^ c = a ^ (b ^ c) = (a ^ b) ^ c // associative

#### 指定位置的位运算
1. 将 x 最右边的 n 位清零：x & (~0 << n)
2. 获取 x 的第 n 位值（0 或者 1）： (x >> n) & 1
3. 获取 x 的第 n 位的幂值：x & (1 << n)
4. 仅将第 n 位置为 1：x | (1 << n)
5. 仅将第 n 位置为 0：x & (~ (1 << n))
6. 将 x 最高位至第 n 位（含）清零：x & ((1 << n) - 1)

#### 实战位运算要点
* 判断奇偶：
x % 2 == 1 —> (x & 1) == 1  
x % 2 == 0 —> (x & 1) == 0  
* x >> 1 —> x / 2   
即： x = x / 2; —> x = x >> 1;  
mid = (left + right) / 2;   —>    mid = (left + right) >> 1;
* X = X & (X-1) 清零最低位的 1
* X & -X => 得到最低位的 1
* X & ~X => 0

## 第十七课 布隆过滤器 和 LRU Catch
### 布隆过滤器

### LRU Catch
LRU (Least Recently Used) ，即 近期最少使用算法，它的核心思想就是会**优先淘汰那些近期最少使用的缓存对象**。

### 排序算法
* 比较类排序
  * 交换排序
    * 冒泡排序
    * 快速排序
  * 插入排序
    * 简单插入排序
    * 希尔排序
  * 选择排序
    * 简单选择排序
    * 堆排序
  * 归并排序
    * 二路归并
    * 多路归并

* 非比较类排序
  * 计数排序
  * 桶排序
  * 基数排序

#### 时间复杂度分析
|排序方法|时间复杂度(平均)|时间复杂度(平均)|时间复杂度(平均)|空间复杂度|稳定性|
|:-:|:-:|:-:|:-:|:-:|:-:|
|插入排序|O(n^2)|O(n^2)|O(n)|O(1)|稳定|
|希尔排序|O(n^1.3)|O(n^2)|O(n)|O(1)|不稳定|
|选择排序|O(n^2)|O(n^2)|O(n)|O(1)|不稳定|
|堆排序|O(nlogn)|O(nlogn)|O(nlogn)|O(1)|不稳定|
|冒泡排序|O(n^2)|O(n^2)|O(nlogn)|O(1)|稳定|
|快速排序|O(nlogn)|O(nlogn)|O(nlogn)|O(1)|不稳定|
|归并排序|O(nlogn)|O(nlogn)|O(nlogn)|O(1)|稳定|
|计数排序|O(n+k)|O(n+k)|O(n+k)|O(n+k)|稳定|
|桶排序|O(n+k)|O(n^2)|O(n)|O(n+k)|稳定|
|基数排序|O(n*k)|O(n*k)|O(n*k)|O(n*k)|稳定|

#### 初级排序 - O(n^2)
##### 1、选择排序（Selection Sort）
每次找到最小值，放在待排序数组的起始位置

```javascript
var selectionSort = function (arr) {
  if (arr.length < 2) return arr
  for (let i = 0; i < arr.length; i++) {
    let min = i
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[j] < arr[min]) min = j
    }
    [arr[i], arr[min]] = [arr[min], arr[i]]
  }
}
```

#### 2、插入排序（Insertion Sort）
1. 从前到后构建有序序列；
2. 对未排序的数据，找到在有序序列中的位置插入；

```javascript
var insertionSort = function (arr) {
  if (arr.length < 2) return arr
  for (let i = 1; i < arr.length; i++) {
    let idx = 0
    for (let j = i-1; j >= 0; j--) {
      if (arr[i] > arr[j]) {
        idx = j + 1
        continue
      }
    }
    if (i !== idx) {
      const [target] = arr.splice(i, 1)
      arr.splice(idx, 0, target)
    }
  }
}
```

#### 3、冒泡排序（Bubble Sort）
```javascript
var bubleSort = function (arr) {
  if (arr.length < 2) return arr
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - i; j++) {
      if (arr[j] > arr[j+1]) {
        [arr[j], arr[j+1]] = [arr[j+1], arr[j]]
      }
    }
  }
}
```

#### 高级排序 - O(N*LogN)
##### 1、快速排序（Quick Sort）
1. 数组取 标杆 pivot，将小的元素放在 pivot 的左边，将大的元素放在右边
2. 然后依次对左右两侧的元素，继续快排，已达到整个数组有序

```javascript
var quickSort = function (arr) {
  if (arr.length < 2) return arr

  const left = [], right = [], n = arr.length, pivot = Math.floor((n - 1)/ 2)
  for (let i = 0; i < n; i++) {
    if (i == pivot) continue
    else if (arr[i] < arr[pivot]) left.push(arr[i])
    else right.push(arr[i]) 
  }
  return [...quickSort(left), arr[pivot], ...quickSort(right)]
}
```

## 每日一题
* [LeetCode 107 二叉搜索树中的插入操作](./Day1/README.md#1)