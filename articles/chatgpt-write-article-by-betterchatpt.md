---
title: "Zenn: Better ChatGPT を活用した実践的な記事執筆方法"
emoji: "🧙‍♀️"
type: "idea"
topics: [ "Zenn", "ChatGPT", "writing", "BetterChatGPT","プロンプトエンジニアリング" ]
published: false
---

## 1. はじめに

この記事では、OpenAI が開発した`ChatGPT`と、非公式のデスクトップクライアントである`Better ChatGPT`を使って Zenn の記事を書く方法を紹介します。

その他、自分が使用している記事執筆用プロンプトについても紹介します。

ChatGPT の無料プランでは`GPT-3.5 Turbo`を使用しています。GPT-3.5 Turbo はトークン認識が 4096 トークンと制限があるものの、高速かつ柔軟な性能があります。
有料プランにアップグレードすることで、より大規模な言語モデルである次世代の`GPT-4`が利用できます。また、認識できるトークン数も増加します。
GPT-4 は次世代のさらに高度な性能を提供し、効率的な実用的な記事の執筆ができます。

また、`Better ChatGPT`を使うことで、Zenn の記事のような長い記事のレビューでも GPT-4 が力を発揮します。
実際、本記事は、`Better ChatGPT`+`GPT-4`を利用して執筆しました。

## 2. Better ChatGPTとは

`Better ChatGPT`は ChatGPT を活用するための非公式のデスクトップクライアントです。
UI は、Web 上の`ChatGPT`と同様であり、同じような使用感で使うことができます。

さらに、チャットの結果をシェアやダウンロードする機能があり、ChatGPT でのチャット結果を使いやすくなっています。

### 2.1 Better ChatGPTの使い方

Better ChatGPT を起動すると、ChatGPT と同様の画面が開きます。

![Better ChatGPT](https://i.imgur.com/T8zjhwG.png)

画面中央にあるテキスト入力欄にメッセージを入力すれば、Web 上の ChatGPT と同様のチャットができます。

### 2.2 Better ChatGPTによる記事の作成

Better ChatGPT に、記事執筆用のプロンプトとスケルトンとして、見出しだけのテキストを入力します。
ChatGPT が生成した記事から、本文を適宜、編集中の記事にコピーします。

より実用的な記事を作成するために、有料で提供されている`GPT-4 API`を使用します。

### 2.3. GPT-3.5 TurboとGPT-4の違い

GPT-3.5 Turbo は、ChatGPT の現行の GPT 言語モデルです。トークン認識が 4096 トークンと制限がありますが、高速かつ柔軟な性能があり、使い勝手が良いです。

一方、GPT-4 は ChatGPT の有料プラン`ChatGPT Plus'で選択できる次世代の言語モデルです。
GPT-4 は、GPT-3.5 よりも大きな言語モデルであり、豊富な学習データに基づきます。
この結果、正確で自然なテキスト生成が可能となります。

## 3. Better ChatGPTによる記事の作成、公開フロー

以下のフェーズで、記事を執筆、公開します。

### 3.1. 執筆フェーズ

1. テーマと対象読者、参考資料の設定
  執筆する記事のテーマ、対象読者、参考資料などを決める

2. 記事全体の構成
   記事全体の構成を決め、スケルトンとして各見出しを作成する

3. 記事執筆用プロンプトの設定
   1. で決めた theme などをプロンプトの各項目に設定する

4. Better ChatGPT を使った記事の執筆
   `Better ChatGPT`のテキスト入力欄にプロンプトと 2. で作成した見出しを入力し、記事を作成する

### 3.2. レビュー、修正フェーズ

1. レビュー用プロンプトの設定
  4.1. で決めたテーマなどをもとに、レビュー用プロンプトの各項目を設定する

2. Better ChatGPT を使った記事のレビュー
   Better ChatGPT にレビュー用プロンプトと記事を入力し、記事をレビューする

3. 記事の修正、改善
   2. で提示された改善点、代替案をもとに記事を修正、改善する

4. レビュー、修正の繰り返し
   2.から-3. の手順を繰り返し記事の質を高める

### 3.3. 確認、公開フェーズ

1. 校閲用プロンプトによるチェック
   校閲用プロンプトを使い、誤字脱字や表記揺れ、読みにくいところがないかチェックする

2. プレビューによる確認
   Zenn CLI のプレビュー機能を用いて、画像が正常に表示されているかなどをチェックする

3. 下書きによる確認
   Zenn での下書き時の記事を見て、公開して問題ないかを確認する

4. 公開
   published を true に変更し、Zenn で記事を公開する

## 4. 執筆フェーズ

### 4.1. テーマなどの設定

記事執筆用プロンプトでは、

- role: 誰が記事を書くか
- theme: 何について記事を書くか
- target: 誰に対して記事を書くか

を指定する必要があります。

今回の例では、

- role: 一流の技術ブロガー
- theme: ChatGPT を使った Zenn への記事執筆に関する実践的な方法
- target: Zenn で記事を書こうとする ITエンジニア

となります。

また、remark: を使って参考にした Webサイトを指定できます。
ここでは、

- Zenn: <https://zenn.dev/>

を追加します。

### 4.2. 記事全体の構成

記事全体の構成を考え、スケルトンとして記事の書く見出しを作成します。
ChatGPT は見出しをもとにして記事を作成します。

この記事の場合は。

@[gist](https://gist.github.com/atsushifx/81a0c161be84f9d09f8043f7a1525be6?file=headlines.md)

となります。

### 4.3. 記事執筆用プロンプト

[4.1.](#41-テーマなどの設定)で決めた role、theme などを入力して記事執筆用プロンプトを作成します。
執筆用プロンプトは、

@[gist](https://gist.github.com/atsushifx/81a0c161be84f9d09f8043f7a1525be6?file=blog-write-prompt.md)

と、なります。

### 4.4. Better ChatGPTを使った記事の執筆

`Better ChatGPT`を立ち上げ、作成した記事執筆用プロンプトと各見出しを入力し、記事を作成します。
作成された記事を、見出しスケルトン (見出しのみの記事) に貼り付けます。
必要なら文章を、適宜、編集します。

### 4.5. 文章の修正、追加

[4.4.](#44-better-chatgptを使った記事の執筆)で作成した記事は、そのままでは使えません。
記事の内容が表面的で、詳細な説明や筆者独自の視点が不足している場合があります。
記事の内容が、**筆者独自の視点がある記事**になっていません。

記事のスケルトンとしては十分に使えるので、記事に必要な章や文章を追加、修正します。

以上で、記事の初稿が作成できました。

## 5. レビュー、修正フェーズ

[4.](#4-執筆フェーズ)で作成した初稿レベルでは、記事として未完成です。
`Better ChatGPT`を使ってレビュー、修正を繰り返し、記事の質を高めます。

### 5.1. レビュー用プロンプト

記事のレビュー用プロンプトは、次のようになります。

@[gist](https://gist.github.com/atsushifx/81a0c161be84f9d09f8043f7a1525be6?file=blog-review-prompt.md)

このプロンプトでも、theme,goal といった変数を用いてテーマ。記事の目標などをレビューの支持と分離しています。
これにより、レビュワーの役割や記事のテーマなど、レビュー時に何をレビューするのかを明確にしています。

### 5.2. Better ChatGPTを使った記事のレビュー

`Better ChatGPT`に、レビュー用プロンプトと記事を入力して、記事をレビューします。

### 5.3. 記事の修正、改善

記事のレビュー結果として、改善点とその代替案が表示されます。
これをもとに、修正します。

### 5.4. レビュー、修正の繰り返し

記事が十分に読みやすくなるまで、5.2.-5.3.の手順を繰り返します。

## 6. 確認、公開フェーズ

最後に、誤字脱字や表記揺れ、読みにくいところがないかなどをチェックし、記事の完成度を上げます。
あわせて、画像や gist などの引用が正常に表示されているかもチェックします。

### 6.1. 校閲用プロンプトによる記事のチェック

校閲用プロンプトを使って、誤字脱字や表記揺れ、読みにくい表現がないかなどをチェックします。

校閲用プロンプトは、つぎのとおりです。

@[gist](https://gist.github.com/atsushifx/81a0c161be84f9d09f8043f7a1525be6?file=blog-proofreading-prompt.md)

校閲用プロンプトでは、指示、変数、入力を分けています。
プロンプトは、まず日本語で誤字脱字や読みにくいところをチェックするよう指示を出しています。

変数 role では、複数の担当を定義しています。複数の担当の目線でチェックすることにより、質の高い校閲を実現しています。
変数 text は、入力するマークダウン文章を受け持ちます。text が指定されると、該当文書の校閲をおこないます。
それ以外は、text で新たな文章が入力されるまで、入力待ちを続けます。

こうして、質の高い、繰り返し可能な校閲を実現しています。

ここでレビュー、校閲を繰り返し誤字脱字などをなくします。

### 6.2. プレビューによる記事の確認

Zenn 用の記事作成ツール、`Zenn CLI`には記事のプレビュー機能がついています。
これを使ってスクリーンショットや引用したテキストが正しく表示されているかなど、記事の表示に問題ないかを確認します。

### 6.3. Zennの下書きによる確認

Zenn では、記事の公開前に Web 上でどのように見えるかチェックできます。
この機能で、記事を公開する前の最終確認をします。

### 6.4. 記事の公開

記事の内容と表示に問題ないことを確認したら、ヘッダーの`published`を`true`に設定して`Zenn`で記事を公開します。

## 7. さいごに

この記事では、ChatGPT とその PC 用クライアント`Better ChatGPT`を使って素早く、効率的に質の高い記事を書く方法を紹介しました。

適切な ChatGPT ツールと適切なプロンプトを使用すれば、効率的に高品質な記事を作成できます。

それでは、Happy Writing and Hacking!

## 参考資料

### 重要キーワードと技術用語

この記事で述べられている重要なキーワードと技術用語について、説明します。

- GPT-3.5 Turbo: ChatGPT の無料プランで使用できる言語モデル。トークン認識の制限付きですが、高速で柔軟な性能を持っている

- GPT-4: ChatGPT の有料プランである`ChatGPT Plus`で選べる大規模な次世代 GPT 言語モデル。GPT-3.5 Turbo と比較して、認識できるトークンの数が多い

- Zenn: ITエンジニアの知見を共有するプラットフォーム。この記事も Zenn に投稿している

- 記事執筆用プロンプト: 自分が Zenn 用に現行を作成するときに使用している ChatGPT 用のプロンプト

### 公式サイト

- [ChatGPT](https://openai.com/blog/chatgpt/)
- [Better ChatGPT](https://github.com/ztjhz/BetterChatGPT)