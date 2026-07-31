# Configuration

EPGStation で使用していた次の YAML を、内容を変更せずこのディレクトリへ配置できます。

- `config.yml`
- `config.yml.template`（`stream` の省略値を補完する場合）
- `operatorLogConfig.yml`
- `serviceLogConfig.yml`
- `epgUpdaterLogConfig.yml`

`compose.yaml` は `config.yml` をバックエンドと ffmpeg worker の両方へ渡します。
TNLAStation 固有のJSON設定ファイルは不要です。PostgreSQL接続情報やworkerの内部URLなど、
EPGStation に存在しないコンテナ固有設定だけはComposeの環境変数で設定されます。

Kubernetes ConfigMapから移行する場合は、`data.config.yml` を `config.yml` として保存します。
ConfigMapのキーとして置いていたエンコードスクリプトは、コマンド中のパスに合わせて
`enc/enc-local.js`、`enc/enc-remote.js` のように配置してください。
`%ROOT%/config/...` はCompose内の `/config/...` に解決されます。

`mirakurunPath` はコンテナから到達可能なURLである必要があります。Kubernetesの
`*.svc.cluster.local` は通常Composeから解決できないため、LAN内IPや
`http://host.docker.internal:40772/` などへ変更します。

ログの `%OperatorSystem%` などの既定パスは、共有ボリューム内の
`/var/lib/tnlastation/logs/{Operator,Service,EPGUpdater}/` に展開されます。
