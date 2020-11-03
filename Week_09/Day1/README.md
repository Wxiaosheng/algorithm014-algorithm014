## LeetCode 925 长按键入
你的朋友正在使用键盘输入他的名字 name。偶尔，在键入字符 c 时，按键可能会被长按，而字符可能被输入 1 次或多次。

你将会检查键盘输入的字符 typed。如果它对应的可能是你的朋友的名字（其中一些字符可能被长按），那么就返回 True。

    示例 1：
      输入：name = "alex", typed = "aaleex"
      输出：true
      解释：'alex' 中的 'a' 和 'e' 被长按。

    示例 2：
      输入：name = "saeed", typed = "ssaaedd"
      输出：false
      解释：'e' 一定需要被键入两次，但在 typed 的输出中不是这样。

    示例 3：
      输入：name = "leelee", typed = "lleeelee"
      输出：true

    示例 4：
      输入：name = "laiden", typed = "laiden"
      输出：true
      解释：长按名字中的字符并不是必要的。
 

提示：
* name.length <= 1000
* typed.length <= 1000
* name 和 typed 的字符都是小写字母。

#### 方法一： 双指针
```javascript
var isLongPressedName = function (name, typed) {
  if (name[0] !== typed[0]) return false
  for (let i = 0, j = 0; i < name.length || j < typed.length;) {
    if (name[i] == typed[j]) i++, j++
    else {
      if (typed[j] == name[i-1]) j++
      else return false
    }
  } 
  return true
}
```

#### 方法二： 更加优化的双指针

```javascript
var isLongPressedName = function (name, typed) {
  const m = name.length, n = typed.length
  for (let i = 0, j = 0; j < n; j++) {
    if (name[i] == typed[j]) i++
    else if (i == 0 || name[i - 1] !== typed[j]) return false
  }
  return i == m
}
```