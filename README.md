# TNLAStation

EPGStation 互換の録画サーバー。バックエンドは .NET、フロントエンドは Next.js で、
番組表は Mirakurun から取り込む。

- [TNLAStation-backend](https://github.com/miutaku/TNLAStation-backend)
- [TNLAStation-frontend](https://github.com/miutaku/TNLAStation-frontend)

## デモ

https://miutaku.github.io/TNLAStation-frontend/

サンプルデータを使って、バックエンドなしで主な画面と操作を試せます。

## 起動

```sh
cp .env.example .env   # POSTGRES_PASSWORD を書く
cp config/config.yml.example config/config.yml
# config/config.yml の mirakurunPath を利用環境に合わせて変更する
docker compose up -d
```

http://localhost:8888 で開く。API は同一オリジンの `/api` にある。

Compose は公開済みの GHCR イメージを取得するため、backend と frontend の
リポジトリを別途cloneする必要はない。使用するバージョンは `compose.yaml` の
各 `image` に完全なバージョンとして固定する。

更新前にはデータベースと録画設定をバックアップし、使用するバージョンを変更してから実行する。

```sh
docker compose pull
docker compose up -d
```

リリースとロールバックの手順は [RELEASING.md](RELEASING.md) を参照。
開発への参加方法は [CONTRIBUTING.md](CONTRIBUTING.md) を参照。
