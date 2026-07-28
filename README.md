# TNLAStation

EPGStation 互換の録画サーバー。バックエンドは .NET、フロントエンドは Next.js で、
番組表は Mirakurun から取り込む。

- [TNLAStation-backend](https://github.com/miutaku/TNLAStation-backend)
- [TNLAStation-frontend](https://github.com/miutaku/TNLAStation-frontend)

## 起動

```sh
cp .env.example .env   # POSTGRES_PASSWORD を書く
cp config/appsettings.Production.example.json config/appsettings.Production.json   # Mirakurun の URL などを書く
docker compose up -d
```

http://localhost:8888 で開く。API は同一オリジンの `/api` にある。

Compose は公開済みの GHCR イメージを取得するため、backend と frontend の
リポジトリを別途cloneする必要はない。安定運用では `.env` の
`TNLA_BACKEND_VERSION` と `TNLA_FRONTEND_VERSION` を `1.2.3` のような
完全なバージョンへ固定する。`latest` は検証用途や最新版追従向け。

更新前にはデータベースと録画設定をバックアップし、使用するバージョンを変更してから実行する。

```sh
docker compose pull
docker compose up -d
```

リリースとロールバックの手順は [RELEASING.md](RELEASING.md) を参照。
開発への参加方法は [CONTRIBUTING.md](CONTRIBUTING.md) を参照。
