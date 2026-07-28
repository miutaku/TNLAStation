# Configuration

EPGStation で使用していた次の YAML を、内容を変更せずこのディレクトリへ配置できます。

- `config.yml`
- `config.yml.template`（`stream` の省略値を補完する場合）
- `operatorLogConfig.yml`
- `serviceLogConfig.yml`
- `epgUpdaterLogConfig.yml`

`compose.yaml` は `config.yml` をバックエンドと ffmpeg worker の両方へ渡します。
TNLAStation 固有のJSON設定ファイルは不要です。PostgreSQL接続情報やworkerの内部URLなど、
EPGStationに存在しないコンテナ固有設定だけはComposeの環境変数で設定されます。

ログの `%OperatorSystem%` などの既定パスは、共有ボリューム内の
`/var/lib/tnlastation/logs/{Operator,Service,EPGUpdater}/` に展開されます。
