# コントリビューション

IssueやPull Requestを歓迎します。小さくレビュー可能な変更を優先してください。

## Issue

- バグと機能提案はIssueフォームを使用する
- 質問や提案の前に既存Issueを検索する
- ログ、設定、スクリーンショットからパスワードや個人情報を除去する
- セキュリティ上の問題は公開Issueに書かず、[SECURITY.md](SECURITY.md)に従う

## Pull Request

1. Issueがある場合は関連付ける
2. `main` から作業ブランチを作る
3. 1つの目的に絞ったコミットとPRにする
4. `POSTGRES_PASSWORD=validation docker compose config --quiet` を実行する
5. テンプレートを埋め、互換性や移行手順があれば明記する

大きな仕様変更は、実装前にIssueで方向性を確認してください。
リリース用タグの作成とGHCRへの公開はメンテナーが行います。
