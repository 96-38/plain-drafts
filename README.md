# Plain Drafts
テキストの下書き作成を支援する Web アプリケーションです。

|PC|Mobile|
|:----:|:----:|
|<img src="https://user-images.githubusercontent.com/48713768/107567630-46125e80-6c29-11eb-9b3c-aa6593922382.gif" width="400px">|<img src="https://user-images.githubusercontent.com/48713768/107567717-617d6980-6c29-11eb-8a04-34a4803d2b78.gif" width="200px">|<
## 概要
「Plain Drafts」は以下の機能を提供します。
- フォームに入力したテキストを下書きリストに追加
- 下書きリストに追加したテキストの編集・削除
- 下書きリストに追加したテキストをクリップボードにコピー
- ショートカットキーによるテキストの追加・下書きリストの削除
- LocalStorage に下書きリストを保存


## 制作背景
Zoom, Slack, LINE, Discord, Twitter の DM 等、プラットフォームによってテキスト入力中の Enter キーの挙動が異なり (送信 / 改行) 入力中のテキストを誤って送信してしまうことがよくありました。そこで、不要なメタデータを含まない書き捨てのテキストデータを Web ブラウザ上で作成・管理できれば便利だと考え、Vue.js の学習も兼ねて制作しました。

## デモ
[こちら](https://plain-drafts.netlify.app/)から実際の動作を確認できます。

## 使用した技術
[Vue.js](https://github.com/vuejs/vue)

[Tailwind CSS](https://github.com/tailwindlabs/tailwindcss)


## ローカル環境での起動方法
リポジトリをローカルにクローンした後、 plain-drafts ディレクトリで以下のコマンドを順に実行して下さい。
```
yarn
yarn dev
```
