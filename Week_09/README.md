# 学习笔记

## 每日一题
* ✅  [LeetCode 925 长按键入](./Day1/README.md#1)

## 实战题目
* ✅  爬楼梯（过遍数）
* ✅  不同路径（过遍数）
* ✅  打家劫舍（过遍数）
* 最小路径和（过遍数）
* 股票买卖（过遍数）


## 第十九课 高级动态规划

#### 递归、分治、回溯、动态规划复习
##### 递归
就是函数自己调用自己

```javascript
var recursion = function (level, params) {
  // recursion terminator
  if (level >= max) return ...
  // process current logic
  process(params)
  // drill down 
  recursion(level + 1, new_params)
  // restore currter status, if need
}
```

##### 分治（分而治之） Divide & Conquer
将一个大的问题，拆分成一个个可以解决的小问题，最后再将结果

**本质：寻找重复性 —> 计算机指令集**

```javascript
var divide = function (level, params) {
  // recursion terminator
  // process => 将大问题，拆分成可解决的小问题
  // dirll down
  // restore current status, if need
}
```

##### 动态规划  Dynamic Programming
* 动态规划 和 递归或者分治， 没有本质上的区别
* 拥有共性： 寻找最小重复子问题

1. 将复杂的问题，分解成子问题
2. 分治 + 最优子结构
3. 顺推形式： 动态递推

