# clipboardmanager-build

ClipboardManager（Windows のクリップボード履歴アプリ）を GitHub の Windows 環境で組み、インストーラーを Release に置く使い捨ての係です（nolumiatask #1132）。NolumiaScheduler の `nolumiascheduler-build` と同じ形です。

- ソースは非公開の `kiyoteruhosoda/ClipboardManager`。読み取り専用の deploy key（秘密 `SOURCE_DEPLOY_KEY`）で読みます
- main の新しい commit を、定期の起動か家の側（forge `kyon/clipboardmanager-build`）からの起動で組みます。試験を流し、Velopack で Setup.exe・Portable.zip・更新の一式を作り、Release（タグ `build-<sha>`）に置きます。古い Release は消します
- 組んだ結果は枝 `status` の `status.json` に書きます。家の側がそれを見て、失敗を notice へ知らせます
- 家の側が Release を取り、更新の一式を `artifacts/clipboardmanager/`、持ち主が入れる zip を `files/clipboardmanager/`（share.nolumia.com）へ上げます
- 枝の試し: `gh workflow run build.yml -R kiyoteruhosoda/clipboardmanager-build -f sha=<sha> -f publish=false`

消えても配布が止まるだけで、アプリの正本には響きません。
