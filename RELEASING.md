# リリース運用

TNLAStation はbackend系とfrontendを独立したSemVerで管理する。

- backendの1バージョンから `tnlastation-backend` と
  `tnlastation-ffmpeg-worker` の同じタグを生成する
- frontendは `tnlastation-frontend` として独立してリリースする
- Composeでは `.env` の `TNLA_BACKEND_VERSION` と
  `TNLA_FRONTEND_VERSION` を個別に固定する

## バージョンの決め方

[Semantic Versioning](https://semver.org/) に従う。

- PATCH: 互換性を維持した修正
- MINOR: 互換性を維持した機能追加
- MAJOR: 設定、API、保存データなどに互換性のない変更
- プレリリース: `v1.2.3-rc.1`。この場合 `latest` は更新しない

## メンテナーのリリース手順

対象リポジトリの `main` でCIが成功していることと、リリース内容を確認する。
タグを作成してpushする以外の手作業は不要。

```sh
git switch main
git pull --ff-only
git tag -a v1.2.3 -m "v1.2.3"
git push origin v1.2.3
```

`Release` workflowが次を自動実行する。

1. SemVerタグを検証する
2. DockerイメージをビルドしてGHCRへpushする
3. `1.2.3`、`1.2`、`1` を付ける
4. 正式版のみ `latest` を更新する
5. GitHub Releaseと自動生成リリースノートを作る

公開後、Composeの `.env` を新しい完全バージョンへ更新して検証する。
問題があれば `.env` を直前のバージョンへ戻し、再度
`docker compose pull && docker compose up -d` を実行する。公開済みタグは
上書き・削除せず、新しいPATCHリリースで修正する。
