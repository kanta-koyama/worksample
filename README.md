# worksample

## Build Setup

```bash
# install dependencies
$ npm install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm run start

# generate static project
$ npm run generate

# node version
18.7.0

# npm version
8.15.0
```

## 確認手順
今回作成したワークサンプルの確認手順となります。
nuxtを仕様したプロジェクトとなりますのでビルドまでの手順は上記にて記載した `Build Setup` をご参照ください。
ローカル環境立ち上げ後は http://localhost:3000/ にてご確認いただけます。

対応内容としては「G3_フロントエンドワークサンプル_株式会社ペライチ」にて指示いただいた内容に沿って実装しております。
- 画面表示時に商品画像取得APIを呼び、保存済みの画像を取得
	（今回利用した https://httpbin.org/ の都合で取得するデータの形式が細かく調整する時間がなかったのでコメントに詳細を記載し、実際に想定するパラメータでの実装とさせていただきました。こちらご容赦いただけますと幸いです）
- 画像の複数選択、及び分割してのアップロード
- アップロードした画像のプレビュー表示
	- 表示された画像の並び順調整、削除操作
- 追加した画像の保存実行（こちらも実際のAPIを想定したパラメータでの実装となります）
- PC/SPのレスポンシブ表示

## 備考
- cssはscssを利用し、一部FLOCSSの思想を取り入れております。
- アイコンはheroiconsの素材を使用しております。
	https://heroicons.com/