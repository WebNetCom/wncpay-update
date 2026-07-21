# wncpay-update

Public **update channel** for the WNC Pay WordPress plugin. This repository intentionally contains no source code — only tagged [releases](../../releases) with the installable plugin ZIP attached as an asset.

Sites running WNC Pay check this repository for new versions (via the bundled Plugin Update Checker) and install updates through the native WordPress update UI. The plugin source is maintained in a private repository by [WebNetCom](https://webnetcom.co.il).

## For site administrators

Nothing to do here — updates appear on your site's Plugins screen automatically. To install manually, download `wncpay-x.y.z.zip` from the latest release and upload it via Plugins → Add New → Upload Plugin.

## Release process (maintainers)

1. Bump the version in the private repo (`wncpay.php` + `readme.txt`), build `dist/wncpay-x.y.z.zip`.
2. Create release `vX.Y.Z` here and attach the ZIP as an asset (the asset, not the source archive, is what sites install).
