# 学习笔记

[每日一题(置顶🔝)](../questions/README.md)

## 刷题置顶🔝
* ### 递归 - 实战题目 / 课后作业
* 实战题目
    * ✅ [LeetCode 70 爬楼梯](../questions/leetcode.70.md)（阿里巴巴、腾讯、字节跳动在半年内面试常考）
    * ✅ [LeetCode 22 括号生成](./Day1/README.md#1) (字节跳动在半年内面试中考过)
    * ✅ [LeetCode 226 翻转二叉树](./Day2/README.md#1) (谷歌、字节跳动、Facebook 在半年内面试中考过)
    * ❌ 验证二叉搜索树（亚马逊、微软、Facebook 在半年内面试中考过）
    * ❌ 二叉树的最大深度（亚马逊、微软、字节跳动在半年内面试中考过）
    * ❌ 二叉树的最小深度（Facebook、字节跳动、谷歌在半年内面试中考过）
    * ❌ 二叉树的序列化与反序列化（Facebook、亚马逊在半年内面试常考）
* 每日一课
    * ❌ 如何优雅地计算斐波那契数列
* 课后作业
    * ❌ 二叉树的最近公共祖先（Facebook 在半年内面试常考）
    * ❌ 从前序与中序遍历序列构造二叉树（字节跳动、亚马逊、微软在半年内面试中考过）
    * ❌ 组合（微软、亚马逊、谷歌在半年内面试中考过）
    * ❌ 全排列（字节跳动在半年内面试常考）
    * ❌ 全排列 II （亚马逊、字节跳动、Facebook 在半年内面试中考过）


## 递归的实现、特性以及思维要点
* 递归的本质，其实就是循环，通过函数体来实现循环
* 实现方式，韩式调用栈
* 递归过程：
    * 1、recursion terminator - 递归终止条件
    * 2、process current logic - 处理当前层逻辑
    * 3、drill down - 进入下一层
    * 4、restore current status - 清除当前层状态，如果需要

#### 递归模板
```javascript
var recursion = function (level, data, ...) {
    // terminator
    if (level > MAX) {
        return
    }
    // process current logic
    process(level, param)
    // drill down
    recursion(level + 1, newParam)
    // restore current status
}
```
#### 思维要点
1. 不要人肉递归
2. 寻找最小最简方法，将其拆解成可重复解决的问题（重复子问题）
3. 数学归纳法
