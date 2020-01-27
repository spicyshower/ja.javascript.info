
<<<<<<< HEAD
# スティッキーフラグ(sticky flag) "y", 指定位置での検索

フラグ `pattern:y` を使用すると、元の文字列の指定位置で検索を行うことができます。

`pattern:y` フラグのユースケースを把握し、その便利さを知るために実際のユースケースを探っていきましょう。

正規表現の一般的なタスクの1つは "字句解析" です: テキスト、例えばプログラミング言語があり、その構造要素を分析します。

HTML はタグと属性を、JavaScript コードは関数、変数などを持っています。

字句解析プログラムには独自のツールやアルゴリズムがある特別な領域なため、ここでは深くは見ていきませんが共通のタスクがあります: 特定の位置で何かを読み込むことです。

例. `subject:let varName = "value"` という文字列があり、ここから変数名(`4` の位置から始まる)が必要な場合

ここでは正規表現 `pattern:\w+` を利用して変数名を検索します。実際、JavaScript の変数名に対して正確にマッチするためにはより複雑な正規表現が必要ですが、ここでは問題ではありません。

`str.match(/\w+/)` の呼び出しは行の最初の単語のみを見つけます。あるいはフラグ `pattern:g` がある場合はすべての単語文字です。ですが、今必要なのは `4`(インデックス) の位置の単語だけです。

指定位置から検索するには、メソッド `regexp.exec(str)` を利用します。

`regexp` がフラグ `pattern:g` あるいは `pattern:y` を持っていない場合、このメソッドはまさに `str.match(regexp)` のように文字列 `str` の最初の一致を検索します。ここではこのような単純なフラグなしのケースには興味はありません。

フラグ `pattern:g` がある場合、`regexp.lastIndex` プロパティで保持されている位置から文字列 `str` の検索を開始します。そして一致するものが見つかると、`regexp.lastIndex` にその一致の直後のインデックスをセットします。

正規表現が作られたときの `lastIndex` は `0` です。

そのため、連続した `regexp.exec(str)` の呼び出しは次から次へと一致したものを返します。

例 (フラグ `pattern:g` あり):
=======
# Sticky flag "y", searching at position

The flag `pattern:y` allows to perform the search at the given position in the source string.

To grasp the use case of `pattern:y` flag, and see how great it is, let's explore a practical use case.

One of common tasks for regexps is "lexical analysis": we get a text, e.g. in a programming language, and analyze it for structural elements.

For instance, HTML has tags and attributes, JavaScript code has functions, variables, and so on.

Writing lexical analyzers is a special area, with its own tools and algorithms, so we don't go deep in there, but there's a common task: to read something at the given position.

E.g. we have a code string `subject:let varName = "value"`, and we need to read the variable name from it, that starts at position `4`.

We'll look for variable name using regexp `pattern:\w+`. Actually, JavaScript variable names need a bit more complex regexp for accurate matching, but here it doesn't matter.

A call to `str.match(/\w+/)` will find only the first word in the line. Or all words with the flag `pattern:g`. But we need only one word at position `4`.

To search from the given position, we can use method `regexp.exec(str)`.

If the `regexp` doesn't have flags `pattern:g` or `pattern:y`, then this method looks for the first match in the string `str`, exactly like `str.match(regexp)`. Such simple no-flags case doesn't interest us here.

If there's flag `pattern:g`, then it performs the search in the string `str`, starting from position stored in its `regexp.lastIndex` property. And, if it finds a match, then sets `regexp.lastIndex` to the index immediately after the match.

When a regexp is created, its `lastIndex` is `0`.

So, successive calls to `regexp.exec(str)` return matches one after another.

An example (with flag `pattern:g`):
>>>>>>> ff042a03191dfad1268219ae78758193a5803b38

```js run
let str = 'let varName';

let regexp = /\w+/g;
<<<<<<< HEAD
alert(regexp.lastIndex); // 0 (初期 lastIndex=0)

let word1 = regexp.exec(str);
alert(word1[0]); // let (1つ目の単語)
alert(regexp.lastIndex); // 3 (一致した後の位置)

let word2 = regexp.exec(str);
alert(word2[0]); // varName (2つ目の単語)
alert(regexp.lastIndex); // 11 (一致した後の位置)

let word3 = regexp.exec(str);
alert(word3); // null (これ以上一致はなし)
alert(regexp.lastIndex); // 0 (検索終了でリセット)
```

すべての一致がグループや追加のプロパティと一緒に配列として返却されます。

ループですべての一致を取得することもできます:
=======
alert(regexp.lastIndex); // 0 (initially lastIndex=0)

let word1 = regexp.exec(str);
alert(word1[0]); // let (1st word)
alert(regexp.lastIndex); // 3 (position after the match)

let word2 = regexp.exec(str);
alert(word2[0]); // varName (2nd word)
alert(regexp.lastIndex); // 11 (position after the match)

let word3 = regexp.exec(str);
alert(word3); // null (no more matches)
alert(regexp.lastIndex); // 0 (resets at search end)
```

Every match is returned as an array with groups and additional properties.

We can get all matches in the loop:
>>>>>>> ff042a03191dfad1268219ae78758193a5803b38

```js run
let str = 'let varName';
let regexp = /\w+/g;

let result;

while (result = regexp.exec(str)) {
  alert( `Found ${result[0]} at position ${result.index}` );
<<<<<<< HEAD
  // let を位置 0 で見つけ, 次に
  // varName を位置 4 で見つける
}
```

このような `regexp.exec` の利用はメソッド `str.matchAll` の代替手段です。

また、他のメソッドとは違い、指定位置から検索を開始するための独自の `lastIndex` が設定可能です。

例えば、`4` の位置から始まる単語を検索しましょう:
=======
  // Found let at position 0, then
  // Found varName at position 4
}
```

Such use of `regexp.exec` is an alternative to method `str.matchAll`.

Unlike other methods, we can set our own `lastIndex`, to start the search from the given position.

For instance, let's find a word, starting from position `4`:
>>>>>>> ff042a03191dfad1268219ae78758193a5803b38

```js run
let str = 'let varName = "value"';

<<<<<<< HEAD
let regexp = /\w+/g; // フラグ "g" がなければ lastIndex は無視されます
=======
let regexp = /\w+/g; // without flag "g", property lastIndex is ignored
>>>>>>> ff042a03191dfad1268219ae78758193a5803b38

*!*
regexp.lastIndex = 4;
*/!*

let word = regexp.exec(str);
alert(word); // varName
```

<<<<<<< HEAD
この例では位置 `regexp.lastIndex = 4` から開始して `pattern:\w+` の検索を行いました。

注意: 検索は `lastIndex` の位置から始まります。`lastIndex` の位置には単語がないが、その後にあるような場合はそれが検索されます。:
=======
We performed a search of `pattern:\w+`, starting from position `regexp.lastIndex = 4`.

Please note: the search starts at position `lastIndex` and then goes further. If there's no word at position `lastIndex`, but it's somewhere after it, then it will be found:
>>>>>>> ff042a03191dfad1268219ae78758193a5803b38

```js run
let str = 'let varName = "value"';

let regexp = /\w+/g;

*!*
regexp.lastIndex = 3;
*/!*

let word = regexp.exec(str);
alert(word[0]); // varName
alert(word.index); // 4
```

<<<<<<< HEAD
...したがって、フラグ `pattern:g` がある場合、`lastIndex` プロパティは検索の開始位置となります。

**一方、フラグ `pattern:y` は、 `regexp.exec` にその前でもなく後ろでもなく、正確に `lastIndex` の位置を見るようにします。**

これはフラグ `pattern:y` による同じ検索です:
=======
...So, with flag `pattern:g` property `lastIndex` sets the starting position for the search.

**Flag `pattern:y` makes `regexp.exec` to look exactly at position `lastIndex`, not before, not after it.**

Here's the same search with flag `pattern:y`:
>>>>>>> ff042a03191dfad1268219ae78758193a5803b38

```js run
let str = 'let varName = "value"';

let regexp = /\w+/y;

regexp.lastIndex = 3;
<<<<<<< HEAD
alert( regexp.exec(str) ); // null (3 の位置は単語ではなくスペース)

regexp.lastIndex = 4;
alert( regexp.exec(str) ); // varName (4 の位置は単語)
```

ご覧の通り、正規表現 `pattern:/\w+/y` は(`pattern:g` とは異なり) `3` の位置ではマッチしませんが、`4` の位置ならマッチします。

長いテキストがあり、そこには一致するものが全くないと想像してください。フラグ `pattern:g` の検索はテキストの終わりまで進みます。これはフラグ `pattern:y` による検索よりも遥かに長い時間がかかります。

字句解析などのタスクでは、通常正確な位置での検索が多く行われます。フラグ `pattern:y` の使用は、よいパフォーマンスのための鍵です。
=======
alert( regexp.exec(str) ); // null (there's a space at position 3, not a word)

regexp.lastIndex = 4;
alert( regexp.exec(str) ); // varName (word at position 4)
```

As we can see, regexp `pattern:/\w+/y` doesn't match at position `3` (unlike the flag  `pattern:g`), but matches at position `4`.

Imagine, we have a long text, and there are no matches in it, at all. Then searching with flag `pattern:g` will go till the end of the text, and this will take significantly more time than the search with flag `pattern:y`.

In such tasks like lexical analysis, there are usually many searches at an exact position. Using flag `pattern:y` is the key for a good performance.
>>>>>>> ff042a03191dfad1268219ae78758193a5803b38