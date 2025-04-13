# Documents Repository

このリポジトリは、プロジェクトおよび組織内で使用する各種ドキュメント（技術仕様・設計書・ドメイン知識など）を管理・公開するためのリポジトリです。  
Docs as Codeの思想に則り、ソースコードと同様にドキュメントをGitHubで管理・運用します。

---

## ドキュメント構成

| ディレクトリ | 内容 |
|--------------|------|
| docs/        | 技術仕様・設計書・ガイドライン |
| domain/      | ドメイン知識・業務用語・業界ナレッジ |
| glossary.md  | 用語集（.cursorconfigから自動生成） |
| .cursorconfig| Cursor IDE 設定ファイル（AI文脈定義） |
| scripts/     | glossary自動反映などのスクリプト |
| .github/     | GitHub Actions・PRテンプレート 等 |

---

## ドキュメント更新フロー

1. ローカルで `docs/` や `domain/` 配下のMarkdownファイルを編集
2. PRを作成
3. GitHub Actionsによる自動チェック実行
    - Markdownフォーマット（Prettier）
    - glossary.md自動反映
    - リンクチェック
    - ドキュメントサイトビルドチェック
4. レビュー・承認
5. `main` ブランチへマージ
6. 自動デプロイ（GitHub Pages など）

---

## 開発ルール

- ドキュメントはMarkdown形式で記述
- 用語・略語は `.cursorconfig` の `glossary` に追記
- 構成ルールや書き方ガイドは [`docs/guide.md`](docs/guide.md) に記載
- コード変更時は関連ドキュメントの更新も必須（PRテンプレでチェック）

---

## 開発環境セットアップ

```bash
# 推奨パッケージインストール
npm install
pip install -r requirements.txt  # Pythonスクリプト用

# Markdownフォーマット実行
npx prettier --write "docs/**/*.md"

# glossary.md 自動更新
python scripts/update_glossary.py

# ドキュメントサイトビルド（任意）
npm run build
