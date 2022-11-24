# 開発環境について

## IDE ( Integrated Development Environment )

コーディングを効率的に行うための環境を指します。\
基本的には[Visual Studio Code](https://code.visualstudio.com/)を推奨します。

## VS Code 推奨エクステンション

### 優先度--高

ヒューマンエラーを防止するためのエクステンションが主です。

#### Code Spell Checker

<https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker>

スペルミス対策。\
スペルミスだけは絶対に許容してはいけないため、最重要。

#### indent-rainbow

<https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow>

インデントした箇所を着色する。\
主に *閉じタグ不足の防止* や、 *タグのペアリングが間違っていないか確認する* 際の効率が上がる。

副次的な効果として、インデントを適切に保つ事ができるようになるため、\
コードの可読性/保守性の向上にも直結する。

### 優先度--中

無くても良いが、あると便利。

#### Better Comments

<https://marketplace.visualstudio.com/items?itemName=aaron-bond.better-comments>

特定の文字列を含むコメント文に着色し、コメント文の可読性を上げる。

#### Todo Tree

<https://marketplace.visualstudio.com/items?itemName=Gruntfuggly.todo-tree>

`TODO`と`FIXME`コメントを抽出して一括表示してくれるので、対応漏れを無くすために有用。
