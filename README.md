# Project Cobalt txAdmin recipe

Sets up a Project Cobalt server in txAdmin: every Cobalt resource, its dependencies, the database and a ready `server.cfg`.

## What you need

- FXServer build 38004 or newer, with txAdmin
- MariaDB 10.6 or newer (MySQL 8 works too), running and reachable from the server
- A license key from [portal.cfx.re](https://portal.cfx.re/servers/registration-keys)

## Deploy

1. Open txAdmin and start the setup. On a server that's already set up, go to **Settings → Master Actions → Reset FXServer Settings**.
2. Pick **Remote URL Template** and paste:
   ```
   https://raw.githubusercontent.com/Project-Cobalt-FiveM/txAdminRecipe/main/recipe.yaml
   ```
3. Choose an empty folder for the server data.
4. Enter your license key and your database login. txAdmin creates the database.
5. Run the recipe, review `server.cfg`, then save and start the server.

The first start creates every table, so there's nothing to import by hand. Your txAdmin account is added as `group.owner`.

## What it installs

| Folder | Resources |
| --- | --- |
| `[cobalt]` | cobalt_core, cobalt_mysql and every Cobalt resource |
| `[ox]` | ox_lib, ox_target, ox_fuel, ox_doorlock (our forks) and require |
| `[standalone]` | illenium-appearance, npwd, pma-voice, screencapture, bob74_ipl, hospital_map, dealer_map |
| `[cfx-default]` | mapmanager, spawnmanager, baseevents |

## After the first start

- **Ranks.** `staff`, `admin` and `owner`, each inheriting the one below. Add staff at the bottom of `server.cfg`.
- **Steam and FiveMesh.** Both are optional. Uncomment `steam_webApiKey` for Steam authentication, and set `fivemesh_api_key` for logs and uploads.
- **Your own resources.** Add them below `cobalt_adminmenu`. Scripts written for QBCore, ox_inventory, oxmysql, mysql-async or ghmattimysql run on Cobalt's bridges.

## Troubleshooting

- **A download fails with a 403.** GitHub allows 60 anonymous API calls an hour and the recipe uses about 40, so a second try within the hour can hit the limit. Wait an hour and run it again.
- **"Unknown column" errors after an update.** Cobalt is pre-release and table layouts still change. Wipe the database and start again.
