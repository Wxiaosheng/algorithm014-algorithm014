## LeetCode 258 各位相加
给定一个非负整数 num，反复将各个位上的数字相加，直到结果为一位数。

    示例:
        输入: 38
        输出: 2 
        解释: 各位相加的过程为：3 + 8 = 11, 1 + 1 = 2。 由于 2 是一位数，所以返回 2。

### 方法一，迭代
1. 将大于9的数，每一位一次相加，得到新的结果
2. 新的结果如果还大于 9，则重复1、2

```javascript
var addDigits = function (num) {
    if (num < 10) return num

    const sum = num
    while (sum > 9) {
        const numStr = num + ''
        sum = 0
        for (let i = 0; i < numStr.length; i++) {
            sum += Number(numStr[i])
        }
    }
    return sum
}
```

### 方法二， 递归
```javascript 
var addDigits = function (num) {
    if (num < 10) return num
    let sum = 0
    const numStr = num + ''
    for (let i = 0; i < numStr.length; i++) {
        sum += Number(numStr[i])
    }
    return addDigits(sum)
}
```

**进阶:  你可以不使用循环或者递归，且在 O(1) 时间复杂度内解决这个问题吗？**

### 方法四，进阶解法
##### 树根
1. 在数学中，数根(又称位数根或数字根Digital root)是自然数的一种性质，换句话说，每个自然数都有一个数根。  
2. 数根是将一正整数的各个位数相加（即横向相加），若加完后的值大于10的话，则继续将各位数进行横向相加直到其值小于十为止[1]，或是，将一数字重复做数字和，直到其值小于十为止，则所得的值为该数的数根。  
3. 例如54817的数根为7，因为5+4+8+1+7=25，25大于10则再加一次，2+5=7，7小于十，则7为54817的数根。  

##### 用途。
1. 数根可以计算模运算的同余，对于非常大的数字的情况下可以节省很多时间。
2. 数字根可作为一种检验计算正确性的方法。例如，两数字的和的数根等于两数字分别的数根的和。
3. 另外，数根也可以用来判断数字的整除性，如果数根能被3或9整除，则原来的数也能被3或9整除。

    原数: 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30
    数根: 1 2 3 4 5 6 7 8 9  1  2  3  4  5  6  7  8  9  1  2  3  4  5  6  7  8  9  1  2  3

**即， 1 - 9 总是循环出现**

```javascript
var addDigits = function (num) {
    if (num < 10) return num
    return num % 9 || 9
}
```

结合上边的规律，对于给定的 n 有三种情况：  
1. n 是 0 ，数根就是 0。
2. n 不是 9 的倍数，数根就是 n 对 9 取余，即 n mod 9。
3. n 是 9 的倍数，数根就是 9。

我们可以把两种情况统一起来，我们将给定的数字减 1，相当于原数整体向左偏移了 1，然后再将得到的数字对 9 取余，最后将得到的结果加 1 即可。

    原数: 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30
    偏移: 0 1 2 3 4 5 6 7 8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 
    取余: 0 1 2 3 4 5 6 7 8  0  1  2  3  4  5  6  7  8  0  1  2  3  4  5  6  7  8  0  1  2  
    数根: 1 2 3 4 5 6 7 8 9  1  2  3  4  5  6  7  8  9  1  2  3  4  5  6  7  8  9  1  2  3 

```javascript
var addDigits = function (num) {
    return (num - 1) % 9 + 1
}
```