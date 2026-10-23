# BoothReviewExtension

BOOTH の商品ページ・ショップページ・一覧ページに、第三者レビューを表示・投稿できる Chrome 拡張 (Manifest V3)。

- 商品ページ: ショップ名とカートボタンの横に評価バッジ (5個星の部分塗りつぶし + `平均 (件数)`)、クリックでレビュー一覧へ
- 一覧ページ: カードごとに評価チップ
- レビュー投稿: 5段階評価 + 本文 (匿名ID = `chrome.storage.local` に保存したランダムUUID、サーバーには pepper 付き HMAC ハッシュのみ保存)
- 通報・投稿禁止者 (BAN) 対応済みの API (`https://reviews.luxdum.win`) を利用

本拡張は BOOTH 本体へは一切送信せず、自前バックエンドとのみ通信します。

## 開発

```bash
npm ci
npm run dev      # WXT dev ビルド (自動リロード)
npm run build    # chrome-mv3 向けビルド → .output/chrome-mv3/
npm test         # vitest + コンテンツスクリプト再現ハーネス
```

## インストール (自分でビルドする場合)

`chrome://extensions` → デベロッパーモード → 「パッケージ化されていない拡張機能を読み込む」→ `.output/chrome-mv3/` を選択。

API で `https://reviews.luxdum.win` (Cloudflare Tunnel + 自前サーバー) を使用しています。サーバー側の実装は [BoothReview](https://github.com/LUXDUM/BoothReview) を参照してください。
