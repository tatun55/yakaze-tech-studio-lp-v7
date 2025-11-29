# Yakaze Tech Studio LP デプロイガイド

## インフラ構成

| 項目 | 値 |
|------|-----|
| ドメイン | yakaze.com, www.yakaze.com |
| ホスティング | AWS CloudFront |
| オリジン | S3 (静的ウェブサイトホスティング) |
| S3バケット | `yakaze-tech-studio-lp` |
| CloudFront Distribution ID | `E1SAT32F3UX5E1` |
| S3エンドポイント | yakaze-tech-studio-lp.s3-website-ap-northeast-1.amazonaws.com |

## デプロイ手順

### 1. S3にアップロード

```bash
cd /Users/a_t/project/yakaze-tech-studio-lp-v2

aws s3 sync . s3://yakaze-tech-studio-lp \
  --exclude ".git/*" \
  --exclude "node_modules/*" \
  --exclude ".claude/*" \
  --exclude "package*.json" \
  --exclude "vite.config.js" \
  --exclude "*.md" \
  --delete
```

### 2. CloudFrontキャッシュ無効化

```bash
aws cloudfront create-invalidation \
  --distribution-id E1SAT32F3UX5E1 \
  --paths "/*"
```

### 3. 反映確認

キャッシュ無効化完了まで数分かかる。ステータス確認:

```bash
aws cloudfront get-invalidation \
  --distribution-id E1SAT32F3UX5E1 \
  --id <INVALIDATION_ID>
```

## ワンライナーデプロイ

```bash
aws s3 sync . s3://yakaze-tech-studio-lp --exclude ".git/*" --exclude "node_modules/*" --exclude ".claude/*" --exclude "package*.json" --exclude "vite.config.js" --exclude "*.md" --delete && aws cloudfront create-invalidation --distribution-id E1SAT32F3UX5E1 --paths "/*"
```

## GitHubリポジトリ

https://github.com/tatun55/yakaze-tech-studio-lp-v7

## ローカル開発

```bash
npm install
npm run dev
```

## 注意事項

- `index.html` が唯一のHTMLファイル（SPA構成）
- フォントファイルは `/fonts/` ディレクトリ
- 画像は `/images/` ディレクトリ
- 外部サービス: Web3Forms（問い合わせ）, TimeRex（予約）
