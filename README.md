# Haywire — releases and update feed

This repository exists to serve **Haywire's in-plugin update check**. It holds no source.

Each release carries two assets:

| asset | purpose |
|---|---|
| `Haywire-<version>.pkg` | the signed, notarized macOS installer |
| `latest.json` | the feed the plugin reads |

Haywire requests exactly this URL:

```
https://github.com/haysholladay/haywire-releases/releases/latest/download/latest.json
```

`/releases/latest/` follows whichever release is marked **Latest**, so publishing a new
release switches the feed over; deleting one rolls it back.

## Requirements this repo must keep

- **Public.** The plugin fetches with no credentials — a private repo 404s for everyone.
- The asset must be named **exactly `latest.json`**, attached to the release marked Latest.
- `latest.json` must carry these four keys — the updater reads only these:

```json
{
  "version": "1.6.6",
  "notes":   "What changed, in one short paragraph.",
  "url":     "https://github.com/haysholladay/haywire-releases/releases/latest",
  "pkg":     "https://github.com/haysholladay/haywire-releases/releases/download/v1.6.6/Haywire-1.6.6.pkg"
}
```

`version` is compared against the running build; `pkg` is what the in-plugin
downloader fetches; `url` is the fallback opened in a browser when `pkg` is absent.

---
Kalide Systems™
