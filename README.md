# TNLAStation

EPGStation 互換の録画サーバー。バックエンドは .NET、フロントエンドは Next.js で、
番組表は Mirakurun から取り込む。

- [TNLAStation-backend](https://github.com/miutaku/TNLAStation-backend)
- [TNLAStation-frontend](https://github.com/miutaku/TNLAStation-frontend)

## 起動

3 つのリポジトリを同じ階層に置く。

```
tnlastation/
  TNLAStation/
  TNLAStation-backend/
  TNLAStation-frontend/
```

```sh
cp .env.example .env   # POSTGRES_PASSWORD を書く
cp config/appsettings.Production.example.json config/appsettings.Production.json   # Mirakurun の URL などを書く
docker compose up -d
```

http://localhost:8888 で開く。API は同一オリジンの `/api` にある。
