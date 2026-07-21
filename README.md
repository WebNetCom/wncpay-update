# wncpay-update

Public **update channel** for the WNC Pay WordPress plugin. This repository intentionally contains no source code — only:

- `wncpay.json` — update metadata polled by installed plugins (via the bundled Plugin Update Checker);
- `releases/wncpay-x.y.z.zip` — the installable plugin builds.

Sites running WNC Pay check `wncpay.json` for new versions and install updates through the native WordPress update UI. The plugin source is maintained in a private repository by [WebNetCom](https://webnetcom.co.il).

## For site administrators

Nothing to do here — updates appear on your site's Plugins screen automatically. To install manually, download the latest ZIP from `releases/` and upload it via Plugins → Add New → Upload Plugin.

## Release process (maintainers)

1. Bump the version in the private repo (`wncpay.php` + `readme.txt`), build `dist/wncpay-x.y.z.zip`.
2. Copy the ZIP into `releases/` here, update `version`, `download_url` and `last_updated` in `wncpay.json`, commit, push, tag `vX.Y.Z`.
