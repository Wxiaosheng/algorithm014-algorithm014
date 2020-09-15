# 学习笔记

## 动态规划 - Dynamic Programming
### 复习 递归、分治、回溯
```javascript
// recursion 代码模板
var recur = function (level, ...) {
  // rerminator
  if (level >= max_leve) return 
  // process current logic
  process(...)
  // drill down
  recur(level + 1, ...)
  // restore current status, if need
}
```

```javascript 
// Divide & Conquer
var divide_conquer = function (problem, params1, params2, ...) {
  // terminator
  if (problem == null) return result
  // prepare data
  data = prepare_data(problem)
  subProblems = split_problem(problem)

  // conquer subproblems
  result1 = divide_conquer(subproblem1)
  result2 = divide_conquer(subproblem2)

  // process or generate the final result
  result = proces_result(result1, result2, ...)
}
```

#### 思想
1. 拒绝人肉递归
2. 寻找最小、最简子问题，并转化为可重复解决子问题
3. 数学归纳法的思想

### Dynamic Programming
**Divide & Conquer + Optimal Substructure** => **分治 + 最优子结构**

#### 关键点
DP 和 Divide & Conquer 没有本质上的区别，都是寻找重复子问题 (就看有无最优子结构)

**共性： 找重复子问题**
**差异性： 最优子结构， 中途可以淘汰次优解** 

解题套路：
1. 最优子结构， opt[n] = best_of(opt[n-1], opt[n-2])
2. 存储中间状态： opt[i] (可能是二维 甚至是 多维的)
3. 递推公式 （状态转移方程 或 DP 方程）
    opt[n] = opt[n-1] + opt[n-2]




## 刷题计划：
1. ✅ [LeetCode 62 不同路径](./Day1/README.md#1)（Facebook、亚马逊、微软在半年内面试中考过）
2. ✅ [LeetCode 63 不同路径 II](./Day01/README.md#2) （谷歌、美团、微软在半年内面试中考过）
3. ✅ [LeetCode 1143 最长公共子序列](./Day1/README.md#3)（字节跳动、谷歌、亚马逊在半年内面试中考过）
4. MIT 动态规划课程最短路径算法
5. ✅ 爬楼梯（阿里巴巴、腾讯、字节跳动在半年内面试常考）
6. ✅ [LeetCode 120 三角形最小路径和](./Day2/README.md#1)（亚马逊、苹果、字节跳动在半年内面试考过）
    * [三角形最小路径和高票回答](https://leetcode.com/problems/triangle/discuss/38735/Python-easy-to-understand-solutions-(top-down-bottom-up))
7. 最大子序和（亚马逊、字节跳动在半年内面试常考）
8. 乘积最大子数组（亚马逊、字节跳动、谷歌在半年内面试中考过）
9. ✅ [LeetCode 322 零钱兑换](../questions/leetcode.322.md)（亚马逊在半年内面试中常考）
10. 打家劫舍（字节跳动、谷歌、亚马逊在半年内面试中考过）
11. 打家劫舍 II （字节跳动在半年内面试中考过）
12. 买卖股票的最佳时机（亚马逊、字节跳动、Facebook 在半年内面试中常考）
13. 买卖股票的最佳时机 II （亚马逊、字节跳动、微软在半年内面试中考过）
14. 买卖股票的最佳时机 III （字节跳动在半年内面试中考过）
15. 最佳买卖股票时机含冷冻期（谷歌、亚马逊在半年内面试中考过）
16. 买卖股票的最佳时机 IV （谷歌、亚马逊、字节跳动在半年内面试中考过）
17. 买卖股票的最佳时机含手续费
    * 一个方法团灭 6 道股票问题

## 本周作业
### 中等
1. 最小路径和（亚马逊、高盛集团、谷歌在半年内面试中考过）
2. 解码方法（亚马逊、Facebook、字节跳动在半年内面试中考过）
3. 最大正方形（华为、谷歌、字节跳动在半年内面试中考过）
4. 任务调度器（Facebook 在半年内面试中常考）
5. 回文子串（Facebook、苹果、字节跳动在半年内面试中考过）

### 困难
1. 最长有效括号（字节跳动、亚马逊、微软在半年内面试中考过）
2. 编辑距离（字节跳动、亚马逊、谷歌在半年内面试中考过）
3. 矩形区域不超过 K 的最大数值和（谷歌在半年内面试中考过）
4. 青蛙过河（亚马逊、苹果、字节跳动在半年内面试中考过）
5. 分割数组的最大值（谷歌、亚马逊、Facebook 在半年内面试中考过）
6. 学生出勤记录 II （谷歌在半年内面试中考过）
7. 最小覆盖子串（Facebook 在半年内面试中常考）
8. 戳气球（亚马逊在半年内面试中考过）

## 下周预习
### 预习题目
1. 实现 Trie (前缀树)
2. 单词搜索 II
3. 岛屿数量
4. 有效的数独
5. N 皇后
6. 单词接龙
7. 二进制矩阵中的最短路径



## 高级 DP 实战题目
> 注意：请大家先消化前面的实战题目，高级 DP 的方法和题解会在课程后面解锁

完全平方数（亚马逊、谷歌在半年内面试中考过）  
编辑距离 （重点）  
跳跃游戏（亚马逊在半年内面试中考过）  
跳跃游戏 II （亚马逊、华为字节跳动在半年内面试中考过）  
不同路径（Facebook、亚马逊、微软在半年内面试中考过）  
不同路径 II （谷歌、美团、微软在半年内面试中考过）  
不同路径 III （谷歌在半年内面试中考过）  
零钱兑换（亚马逊在半年内面试中常考）  
零钱兑换 II （亚马逊、字节跳动在半年内面试中考过）  
