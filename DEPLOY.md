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

### 1. ビルド & S3にアップロード

**重要: Viteでビルドしてdist/の中身のみをデプロイする**

```bash
cd /Users/a_t/project/yakaze-tech-studio-lp-v2

# Viteでビルド
npm run build

# dist/の中身をS3のルートにデプロイ
aws s3 sync dist/ s3://yakaze-tech-studio-lp/ --delete
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
npm run build && aws s3 sync dist/ s3://yakaze-tech-studio-lp/ --delete && aws cloudfront create-invalidation --distribution-id E1SAT32F3UX5E1 --paths "/*"
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
