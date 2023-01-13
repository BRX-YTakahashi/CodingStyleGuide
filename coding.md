# コーディングについて

TODO: 目次を生成する

## CSS設計

[FLOCSS](https://github.com/hiloki/flocss)に基づいた設計を推奨します。

### CSS設計__ってなに？

TODO: 準備中

### CSS設計__なぜ必要なのか

TODO: 準備中

### CSS設計__具体的にどうすればいいの？

TODO: 準備中

### CSS設計__練習方法

TODO: 準備中

## 命名規則

### HTML/CSS__命名規則

- 原則として、[MindBEMding](https://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)に準拠した命名を行う。
  > BEMの概念については[こちら](https://github.com/juno/bem-methodology-ja/blob/master/definitions.md)へ。

  ```text
  block
  block__element
  block__element--modifier
  ```

- **スネークケースを使用する。小文字での記述を厳守。**

  ブロック名が長くなる際には、ケバブケースではなくハイフンで繋げる。

  ```text
  BAD   : namingSample

  GOOD  : naming-sample
  ```

  ただし、JavaScriptのイベント追加用途などであればキャメルケースで記述する。（= JSと規則を合わせるため）\
  この際、接頭辞には`js-`を付与する。

  ```text
  js-placeholderText
  ```

- 原則、単語の省略は許容しない。
  > スペルミスに直結する上、意図の読み取りに時間がかかるため、効率が落ちる。（特に複数人で作業を行う時）

### JavaScript__命名規則

- **キャメルケースを使用する。**

  ```text
  BAD   : naming-sample

  GOOD  : namingSample
  ```

- 値をハードコードしている変数（= 定数）に関しては、すべて大文字の変数名を使用する。

  ```text
  umm   : mobileScreenWidth = 768;

  GOOD  : MOBILE_SCREEN_WIDTH = 768;
  ```

- ファイル名に関しては、種類毎に接頭辞を付与する。

  ```text
  General         : file.js

  Web Components  : wc_file.js

  ES Module       : m_file.js
  ```

### TypeScript__命名規則

TODO: 準備中

> [こちら](https://google.github.io/styleguide/tsguide.html#identifiers)に準拠してしまった方が良さそう

### Git__命名規則

Gitのコミットメッセージを記述する際のルールには[Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)を推奨します。\
細かいルールに関しては、各自↑のドキュメントを読んでください。

```text
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

#### `<type>`について

**標準**: 公式ドキュメントで推奨されている`<type>`

- **fix**: バグ修正時に使う。
- **feat**: 機能追加時に使う。
- **BREAKING CHANGE**: 破壊的変更。*(後方互換性を担保せずにバージョンアップを行うこと)*

**独自**: ↑以外で必要な`<type>`

- **refactor**: コードのリファクターをした際に使う。
- **style**: スタイル調整を行った際に使う。
- **docs**: ドキュメントの作成/改訂を行った際に使う。
- **modified**: 構造の変更などの「何かしらを変更した」際、分類される`<type>`がない時に使う。基本的には使わないほうが良い。

#### 例：バグ修正

```text
fix: ~~の修正

XXの事象の原因となっていた○○を解消した。
```

#### 例：機能追加

```text
feat: ~~の追加

XXの機能を追加した。
```

#### 例：その他

前述した`fix`, `feat`以外は自由にTypeを作って良さそうなので、\
ちょっとした修正や、`README.md`の改訂等には↓を使ったりしています。

```text
modified: README.mdの改訂

~~の記述を追記。
```

### その他__命名規則

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

少し敷居が高い方法ではありますが、**OOCSS**という設計手法を軽く学んでおくと良いでしょう。

JP: [OOCSSの基本](https://www.codegrid.net/articles/2014-css-template-1/)\
EN: [Object Oriented CSS](https://github.com/stubbornella/oocss/wiki)

### レスポンシブ対応__参考ページ

EN: [The State Of Mobile First and Desktop First](https://ishadeed.com/article/the-state-of-mobile-first-and-desktop-first/)\
JP: [レスポンシブ対応のレイアウトを実装する最新テクニックを解説、モバイルファーストとデスクトップファーストの現状](https://coliss.com/articles/build-websites/operation/work/mobile-first-and-desktop-first.html)
