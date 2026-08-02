# deserokk's Dalamud plugin repository

One URL for everything. Add this to Dalamud → Settings → Experimental → **Custom Plugin
Repositories**:

```
https://raw.githubusercontent.com/deserokk/DalamudPlugins/main/pluginmaster.json
```

## What is here

**Nothing but the feed.** This repo holds no code and no binaries — `pluginmaster.json` is a list,
and every `DownloadLink` points at a zip inside that plugin's own repo.

⭐ That separation is the whole point: the feed's job is *distribution*, and a plugin's job is
*being a plugin*. Adding a new one is an entry here, not a new URL for anyone to add.

| plugin | code |
|---|---|
| **DeserokUtils** | https://github.com/deserokk/DeserokUtils |
| **Better Targeting System (PvP)** | https://github.com/deserokk/BetterTargetingSystem-pvp |

## Adding a plugin

1. Push the plugin and its `latest.zip` to its own repo.
2. Add an entry here. `InternalName` **must** match the plugin's `AssemblyName`, or Dalamud
   installs it and then cannot find it.
3. Check the `DownloadLink` URLs actually resolve — a wrong branch name or path returns 404 and
   Dalamud reports it as a generic failure, which points nowhere.

```bash
curl -sS -o /dev/null -w "%{http_code}\n" "<the DownloadLinkInstall url>"
```

## Releasing an update

⚠ **Bump `AssemblyVersion` in three places or the update silently never offers:** the plugin's
`.csproj`, the copy of the manifest inside its zip, and the entry here. Dalamud compares versions
and says nothing when they match — there is no error, just an update that never appears.
