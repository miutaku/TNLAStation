# TNLAStation

EPGStation 互換の録画サーバー。バックエンドは .NET、フロントエンドは Next.js で、
番組表は Mirakurun から取り込む。

- [TNLAStation-backend](https://github.com/miutaku/TNLAStation-backend)
- [TNLAStation-frontend](https://github.com/miutaku/TNLAStation-frontend)

## 起動

```sh
cp .env.example .env   # POSTGRES_PASSWORD を書く
cp config/config.yml.example config/config.yml
# config/config.yml の mirakurunPath を利用環境に合わせて変更する
docker compose up -d
```

http://localhost:8888 で開く。API は同一オリジンの `/api` にある。

Compose は公開済みの GHCR イメージを取得するため、backend と frontend の
リポジトリを別途cloneする必要はない。既定では検証済みの `1.0.0` を使用する。
別バージョンを使う場合は `.env` の `TNLA_BACKEND_VERSION` と
`TNLA_FRONTEND_VERSION` を変更する。

既存のEPGStation `config.yml` も使用できる。Kubernetes内のService DNSなど、
Composeホストから到達できない `mirakurunPath` は、LAN内IPまたは
`host.docker.internal` を使ったURLへ変更する。

更新前にはデータベースと録画設定をバックアップし、使用するバージョンを変更してから実行する。

```sh
docker compose pull
docker compose up -d
```

リリースとロールバックの手順は [RELEASING.md](RELEASING.md) を参照。
開発への参加方法は [CONTRIBUTING.md](CONTRIBUTING.md) を参照。
