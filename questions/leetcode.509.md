## LeetCode 509 斐波那契数

斐波那契数，通常用 F(n) 表示，形成的序列称为斐波那契数列。该数列由 0 和 1 开始，后面的每一项数字都是前面两项数字的和。也就是：

F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
给定 N，计算 F(N)。

 
#### 方法一、递归

```javascript
var fib = function (N) {
    if (N == 0) return 0
    if (N == 1) return 1

    return fin(N - 1) + fib(N - 2)
}
```

#### 方法二、缓存

```javascript
var fib = function (N) {
    const dp = [0, 1]
    for (let i = 2; i <= N; i++) {
        dp[i] = dp[i - 1] + dp[i - 2]
    }
    return dp[N]
}
```

#### 方法三、通项公式

```javascript
var fib = function(N) {
    const  SQRT_FIVE = Math.sqrt(5);
    return Math.round(
        1/SQRT_FIVE * (Math.pow(0.5 + SQRT_FIVE/2, N) - Math.pow(0.5 - SQRT_FIVE/2, N))
    )
};
```