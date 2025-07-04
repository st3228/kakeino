# LINE レシート家計簿 (LINE Receipt Budget Book)

LINEでレシートの写真を送信すると、OCRで内容を解析し、支出を自動的に記録・分類して期間ごとにまとめてくれるボットアプリケーションです。

## 機能 (Features)

- レシート画像のOCR解析
- 店舗名、日付、合計金額、個別アイテムの自動抽出
- 支出のカテゴリ分類
- 日次/週次/月次/年次のサマリーレポート
- 詳細な支出内訳の表示
- LINEを通じた簡単な操作

## 技術スタック (Tech Stack)

- Node.js
- Express
- LINE Messaging API
- Tesseract OCR
- SQLite
- Moment.js

## セットアップ方法 (Setup)

### 前提条件 (Prerequisites)

- Node.js (v12以上)
- npm
- Tesseract OCR (画像解析用)

### インストール手順 (Installation)

1. リポジトリをクローン
   ```
   git clone https://github.com/yourusername/line_budgetbook.git
   cd line_budgetbook
   ```

2. 依存パッケージをインストール
   ```
   npm install
   ```

3. Tesseract OCRをインストール
   - Windows: https://github.com/UB-Mannheim/tesseract/wiki
   - Mac: `brew install tesseract`
   - Linux: `sudo apt install tesseract-ocr`
   
   日本語言語パックもインストールしてください。

4. 設定ファイルを編集
   `config.js`ファイルを開き、LINE Messaging APIのチャネルアクセストークンとチャネルシークレットを設定します。

   ```javascript
   module.exports = {
     line: {
       channelAccessToken: 'YOUR_CHANNEL_ACCESS_TOKEN',
       channelSecret: 'YOUR_CHANNEL_SECRET'
     },
     // その他の設定...
   };
   ```

### LINE Developersでの設定 (LINE Developers Setup)

1. [LINE Developers Console](https://developers.line.biz/console/)にログイン
2. 新しいプロバイダーを作成
3. 新しいMessaging APIチャネルを作成
4. チャネルアクセストークンを発行
5. Webhook URLを設定（例: `https://your-domain.com/webhook`）
6. Webhook送信を有効化
7. 応答メッセージを無効化

## 使い方 (Usage)

### サーバーの起動 (Starting the Server)

```
npm start
```

サーバーはデフォルトでポート3000で起動します。

### 外部からのアクセス (External Access)

LINEのWebhookを受け取るには、インターネットからアクセス可能なURLが必要です。開発中は以下のようなツールが便利です：

- [ngrok](https://ngrok.com/)
- [localtunnel](https://github.com/localtunnel/localtunnel)

例（ngrokの場合）：
```
ngrok http 3000
```

表示されたURLを、LINE DevelopersコンソールのWebhook URLに設定します。

### LINEボットの使い方 (Using the LINE Bot)

1. QRコードまたはLINE IDを使ってボットを友達追加
2. レシートの写真を撮影して送信
3. ボットが自動的に内容を解析し、データベースに保存
4. 以下のコマンドでサマリーを確認：
   - `今日` または `本日` - 今日の支出
   - `週間` または `今週` - 今週の支出
   - `月間` または `今月` - 今月の支出
   - `年間` または `今年` - 今年の支出
   - `詳細` - 詳細な支出内訳（デフォルトは週間）
   - `ヘルプ` - 使い方の表示

## プロジェクト構造 (Project Structure)

```
line_budgetbook/
├── config.js         # 設定ファイル
├── database.js       # データベース操作
├── index.js          # メインアプリケーション
├── ocr.js            # OCR処理
├── parser.js         # レシートテキスト解析
├── summary.js        # サマリーレポート生成
├── package.json      # プロジェクト情報
├── public/           # 静的ファイル
│   └── uploads/      # アップロードされた画像
└── database/         # SQLiteデータベース
```

## デプロイ方法 (Deployment)

### Herokuへのデプロイ例 (Heroku Deployment Example)

1. Herokuアカウントを作成
2. Heroku CLIをインストール
3. 以下のコマンドを実行：

```
heroku login
heroku create
git push heroku main
```

4. 環境変数を設定：

```
heroku config:set LINE_CHANNEL_ACCESS_TOKEN=your_access_token
heroku config:set LINE_CHANNEL_SECRET=your_channel_secret
```

5. Herokuで表示されるURLをLINE DevelopersコンソールのWebhook URLに設定

## 注意事項 (Notes)

- OCR解析の精度はレシートの品質や形式によって異なります
- 日本語のレシートに最適化されています
- 大量のデータを扱う場合は、SQLiteからより堅牢なデータベース（MySQLやPostgreSQL）への移行を検討してください

## ライセンス (License)

MIT

## 作者 (Author)

Your Name
#   k a k e i n o  
 