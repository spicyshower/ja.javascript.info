
整数の正規表現は `pattern:\d+` です。

否定後読みを先頭に追加することで負を除外できます: `pattern:(?<!-)\d+`.

ですが、試してみると1つの "余分な" 結果に気づくかもしれませ。:

```js run
let regexp = /(?<!-)\d+/g;

let str = "0 12 -5 123 -18";

alert( str.match(regexp) ); // 0, 12, 123, *!*8*/!*
```

ご覧の通り、`subject:-18` から `match:8` がマッチしています。これを除外するには、正規表現が別の(マッチしていない)数の途中からではない数値から一致を開始していることを保証する必要があります。

別の否定後読みを指定することで実現できます: `pattern:(?<!-)(?<!\d)\d+`。ここで `pattern:(?<!-)(?<!\d)\d+` は、一致は別の数字の後からは始まらないことを保証し、我々が必要としていることです。

また、これらは1つの後読みに結合することもできます:

```js run
let regexp = /(?<![-\d])\d+/g;

let str = "0 12 -5 123 -18";

alert( str.match(regexp) ); // 0, 12, 123
```
