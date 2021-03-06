内部的には、小数部分 `6.35` は無限のバイナリです。このような場合はいつものように、精度が低下されたものが保存されています。

見てみましょう:

```js run
alert( 6.35.toFixed(20) ); // 6.34999999999999964473
```

精度の低下は数値のインクリメント/デクリメント両方を引き起こす可能性があります。この特定のケースで、数値は少し小さくなり、そういう訳で丸め下げされます。

また、`1.35` は何でしょう？

```js run
alert( 1.35.toFixed(20) ); // 1.35000000000000008882
```

ここでは、精度の低下は数値を少し大きくしました。なので丸め上げられます。

**正しい方法で丸めたい場合、`6.35` で問題を解決するにはどうすればいいですか？**

そのためには、丸める前に整数に近づける必要があります:

```js run
alert( (6.35 * 10).toFixed(20) ); // 63.50000000000000000000
```

`63.5` はまったく精度の低下がないことに注意してください。それは、小数部分 `0.5` は実際には `1/2` だからです。2のべき乗で除算された分数は、バイナリシステムで正確に表現されます。今度はそれを丸めることができます:

```js run
alert( Math.round(6.35 * 10) / 10); // 6.35 -> 63.5 -> 64(丸められた) -> 6.4
```
