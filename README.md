# BoothReviewExtension

BOOTH の商品ページやショップページを開くと、このサービスを利用している人たちが書いたレビューを見られる・書ける Chrome 拡張です (Manifest V3)。

- 商品ページでは、ショップ名とカートボタンの横に5つ星の評価バッジが出ます。バッジには5段階評価の平均とレビュー件数が表示され、クリックするとレビュー一覧が開きます
- ショップのトップページやフォローの新着一覧では、商品カードごとに同じバッジを表示します
- 投稿は5段階評価と本文だけで、アカウント登録は不要です。匿名IDは拡張がブラウザ内 (`chrome.storage.local`) に保存するランダムなUUIDで、サーバーにはそのハッシュ値しか送られません
- 不適切なレビューは通報でき、管理ダッシュボードで投稿禁止 (BAN) にもできます (`https://reviews.luxdum.win` のAPIがこれらいっさいを受持ちます)

BOOTH 本体へはデータを一切送信せず、上記APIとのみ通信します。

## 開発

```bash
npm ci
npm run dev      # WXT dev ビルド (保存で自動リロード)
npm run build    # .output/chrome-mv3/ にビルド
npm test         # vitest + コンテンツスクリプト再現ハーネス
```

## インストール (自分でビルドする場合)

Chrome で `chrome://extensions` を開き、デベロッパーモードを有効にして「パッケージ化されていない拡張機能を読み込む」から `.output/chrome-mv3/` を選択します。

API は `https://reviews.luxdum.win` (Cloudflare Tunnel + 自前サーバー) を使っています。サーバー側の実装は [BoothReview](https://github.com/LUXDUM/BoothReview) リポジトリを参照してください。

## ライセンス

[MIT](./LICENSE)。BOOTH とその運営元 (株式会社テクノロジーズ) とは無関係の、非公式なサードパーティーツールです。
