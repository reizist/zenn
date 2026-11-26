# Zenn 記事執筆リポジトリ（google_cloud_jp Publication 対応）

[Google Cloud Japan の Zenn Publication](https://zenn.dev/p/google_cloud_jp)（および個人記事）向けに、Zenn CLI と GitHub 連携で記事を管理・投稿するための環境です。

- [📘 Zenn CLI で記事・本を管理する方法](https://zenn.dev/zenn/articles/zenn-cli-guide)
- [📘 Publication でも GitHub 連携したい！自由選択型アプローチのすゝめ](https://zenn.dev/open8/articles/zenn-publication-github)

## 初回セットアップ

```bash
npm install
```

### Zenn 側の前提設定（初回のみ）

1. Zenn の [GitHub リポジトリ連携設定](https://zenn.dev/dashboard/deploys) から、このリポジトリ（`reizist/zenn`）を連携する
2. 自分の Zenn アカウントが [`google_cloud_jp`](https://zenn.dev/p/google_cloud_jp) Publication のメンバーとして招待・参加済みであることを確認する

## 記事の作成・プレビュー・公開

### 1. `google_cloud_jp` Publication 向けの記事を作成する

`publication_name: google_cloud_jp` があらかじめ設定された記事ファイルが `articles/` 配下に作成されます。

```bash
npm run new:article
```

スラッグやタイトルを指定する場合:

```bash
npm run new:article -- --slug my-gcp-article --title "記事タイトル" --emoji "☁️"
```

個人記事として作成したい場合（`publication_name` なし）:

```bash
npm run new:article:personal
```

### 2. ローカルでプレビューする

```bash
npm run preview
```

ブラウザで `http://localhost:8000` を開くとリアルタイムプレビューを確認できます。

### 3. 画像を配置する

画像は `images/` ディレクトリに配置し、記事内からルート相対パスで参照します（PNG / JPEG / WebP / GIF、3MB 以内）。

```markdown
![説明文](/images/example.png)
```

### 4. 公開する

記事の Frontmatter で以下を確認し、`published: true` にして `main` ブランチへ `git push` すると Zenn に自動デプロイされます。

```yaml
---
title: "記事のタイトル"
emoji: "☁️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["googlecloud", "bigquery"]
published: true
publication_name: google_cloud_jp
---
```

- 下書き・レビュー中は `published: false` のままにしておくと、PR ベースでレビューしてから公開できます。
