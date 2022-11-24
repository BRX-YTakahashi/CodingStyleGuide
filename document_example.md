# 作業記録_220832_YT

## 概要

クラス名が同じ要素なのに、一個しかコメントが出力されない。

## 対応内容

`assets/js/main.js`内で宣言されている変数が複数の要素を考慮した仕様になっていなかったため、\
当該箇所と関連する箇所の記述を修正した。

before:

`assets/js/main.js`

```js
const targetElm = document.querySelector(".test");

console.log("target: ", targetElm);
```

after:

`assets/js/main.js`

```js
const targetElm = document.querySelectorAll(".test");

targetElm.forEach(e => {
  console.log("target: ", e);
});
```

## 確認用リンク

<https://~~/test.html>

## 作業ディレクトリ,ファイル

### 編集

```txt
assets/js/main.js
```

### 作成

特に無し

## その他

解決するために下記ページを参考にした。\
<https://css-tricks.com/>

将来的に考慮する対象が増えた場合には、より効率的なロジックに書き換える必要がありそう。
