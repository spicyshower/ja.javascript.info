<<<<<<< HEAD
# 非負の整数を探す

整数の文字列があります。

非負のものだけを探す正規表現を作成してください(ゼロも許可します)。

使用例:
=======
# Find non-negative integers

There's a string of integer numbers.

Create a regexp that looks for only non-negative ones (zero is allowed).

An example of use:
>>>>>>> ff042a03191dfad1268219ae78758193a5803b38
```js
let regexp = /your regexp/g;

let str = "0 12 -5 123 -18";

alert( str.match(regexp) ); // 0, 12, 123
```