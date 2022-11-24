# コーディングについて

- [コーディングについて](#コーディングについて)
  - [CSS設計](#css設計)
    - [CSS設計\_\_なぜ必要なのか](#css設計__なぜ必要なのか)
    - [CSS設計\_\_具体的にどうすればいいの？](#css設計__具体的にどうすればいいの)
    - [CSS設計\_\_練習方法](#css設計__練習方法)
  - [命名規則](#命名規則)
    - [命名規則\_\_html, CSS](#命名規則__html-css)
    - [命名規則\_\_JavaScript](#命名規則__javascript)
    - [命名規則\_\_その他](#命名規則__その他)
      - [ケバブケース？キャメルケース？](#ケバブケースキャメルケース)
  - [レスポンシブ対応](#レスポンシブ対応)
    - [レスポンシブ対応\_\_参考ページ](#レスポンシブ対応__参考ページ)

## CSS設計

[FLOCSS](https://github.com/hiloki/flocss)に基づいた設計を推奨します。

### CSS設計__なぜ必要なのか

TODO: 詳細は後ほど追加！！

### CSS設計__具体的にどうすればいいの？

TODO: 詳細は後ほど追加！！

### CSS設計__練習方法

TODO: 詳細は後ほど追加！！

## 命名規則

### 命名規則__html, CSS

- [MindBEMding](https://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)に準拠した命名を推奨します。
  > BEMの概念については[こちら](https://github.com/juno/bem-methodology-ja/blob/master/definitions.md)へ。

  ```txt
  block
  block__element
  block__element--modifier
  ```

- **ケバブケースを使用する。小文字での記述を厳守。**

  ブロック名が長くなる際には、キャメルケースではなくケバブケースを使用する。

  ```txt
  BAD   : namingSample

  GOOD  : naming-sample
  ```

  ただし、JavaScriptのイベント追加用途などであればケバブケースで記述する。\
  この際、接頭辞には`js-`を付与する。

  ```txt
  js-placeholderText
  ```

- 原則、単語の省略は許容しない。
  > スペルミスに直結する上、意図の読み取りに時間がかかるので、特に多人数で作業する環境においては著しく効率が下がる可能性が高い。\
  > 各個人で略称にも差異が発生するため、無理に省略表記を統一するよりも「省略しない」選択をした方が効率的。

### 命名規則__JavaScript

- **キャメルケースを使用する。**

  JavaScriptの命名規則においてはキャメルケースが一般的です。

  ```txt
  BAD   : naming-sample

  GOOD  : namingSample
  ```

- 値をハードコードしている変数（= 定数）に関しては、すべて大文字の変数名を使用してスネークケースを用いる。

  ```txt
  umm   : mobileScreenWidth = 768;

  GOOD  : MOBILE_SCREEN_WIDTH = 768;
  ```

- ファイル名に関しては、種類毎に接頭辞を付与する。

  ```txt
  General         : file.js

  Web Components  : wc_file.js

  ES Module       : m_file.js
  ```

### 命名規則__その他

#### ケバブケース？キャメルケース？

- ケバブケース🍖

  単語を`-`でつなぐ命名規則。

  `naming-sample`

- スネークケース🐍

  単語を`_`でつなぐ命名規則。

  `naming_sample`

- キャメルケース🐫

  先頭以外の単語の頭文字を大文字にしてつなぐ命名規則。

  `namingSample`

- パスカルケース（アッパーキャメルケース）👹

  全単語の頭文字を大文字にしてつなぐ命名規則

  `NamingSample`

## レスポンシブ対応

閲覧されるデバイスの割合を考慮し、**モバイルファースト**でのコーディングが推奨です。

モバイルファースト

```css
.section {
  padding: 2rem 1rem;
}

@media (min-width: 62.5rem) {
  .section {
    display: flex;
    align-items: center;
    gap: 1rem;
    padding: 4rem 2rem;
  }
}
```

デスクトップファースト

```css
.section {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 4rem 2rem;
}

@media (max-width: 62.5rem) {
  .section {
    display: block;
    padding: 2rem 1rem;
  }
}
```

しかし、**モバイルファースト** および **デスクトップファースト** に準じた組み方をすると、\
カスケーディングによる影響を考慮する必要が出てきてしまい、保守するコストが高くなってしまいます。

そこで、**共通の箇所** と **デバイス固有の箇所** を分離させた記述を推奨します。

```css
.nav {
  /**
   * 対象箇所の基礎となるスタイルを記述する箇所 *
   *  この箇所はビューポートの大きさに影響されないため、
   *  全ての画面サイズで適応されるスタイルを記述します。
   */

  display: flex;
}

/* デスクトップのスタイル */
@media (min-width: 800px) {
  .nav {
    /* 画面サイズが 800px以上 の時に適応されるスタイル */

    flex-direction: row-reverse;
   }
}

/* モバイルのスタイル */
@media (max-width: 799px) {
  .nav {
    /* 画面サイズが 799px以下 の時に適応されるスタイル */

    flex-direction: column-reverse;
  }
}
```

### レスポンシブ対応__参考ページ

EN: [The State Of Mobile First and Desktop First](https://ishadeed.com/article/the-state-of-mobile-first-and-desktop-first/)\
JP: [レスポンシブ対応のレイアウトを実装する最新テクニックを解説、モバイルファーストとデスクトップファーストの現状](https://coliss.com/articles/build-websites/operation/work/mobile-first-and-desktop-first.html)
