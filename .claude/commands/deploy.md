---
description: コミット、プッシュ、デプロイを一括実行
---

<task>
変更をコミット・プッシュし、本番環境にデプロイします。
</task>

<execution_steps>

## 1. Git操作

### 1.1 変更確認
```bash
git status
git diff --stat
```

### 1.2 コミット
- 変更内容を分析し、適切なコミットメッセージを作成
- ステージング → コミット → プッシュを実行

```bash
git add -A
git commit -m "コミットメッセージ"
git push origin main
```

## 2. S3にデプロイ

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

## 3. CloudFrontキャッシュ無効化

```bash
aws cloudfront create-invalidation \
  --distribution-id E1SAT32F3UX5E1 \
  --paths "/*"
```

## 4. 完了報告

- コミットハッシュ
- デプロイ結果（S3 sync結果）
- キャッシュ無効化ID
- 本番URL: https://yakaze.com

</execution_steps>

<notes>
- キャッシュ無効化は数分かかる場合があります
- 問題が発生した場合は各ステップのエラーを報告してください
</notes>
