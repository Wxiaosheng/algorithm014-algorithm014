# 第三周复习

## 第7课 泛型递归、树的递归
本质：就是循环，通过函数体实现的

### 泛型递归
1. recursion termiator
2. process current logic
3. drill down
4. restore current status, if need

### 主要思想
1. 不要人肉递归
2. 寻找最小最简子问题，转化为可重复解决子问题
3. 数学归纳法


实战题：
1. ✅ 爬楼梯（斐波那契数列、缓存、recursion）
2. ✅ 括号生成 (recursion)
3. ✅ 翻转二叉树 (recursion)
4. ✅ 验证二叉搜索树（中序遍历是 升序的）
5. 二叉树的最大深度（DFS、BFS）
6. 二叉树的最小深度（DFS、BFS）
7. 二叉树的序列化与反序列化（单个遍历顺序不能确定一个树结构，至少需要两个，一个遍历数据或者一个限制条件）

课后作业：
1. 二叉树的最近公共祖先（loop + hash）
2. 从前序与中序遍历序列构造二叉树（recursion）
3. 组合（recursion）
4. 全排列（recursion）
5. 全排列 II （recursion）