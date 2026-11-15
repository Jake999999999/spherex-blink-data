# spherex-blink-data

Static baked target bundles for [spherex-blink](https://github.com/Jake999999999/spherex-blink), served via GitHub Pages.

Keeping baked target bundles in a separate data repository lets `spherex-blink` stay lightweight while hosting many more NASA/IPAC SPHEREx sky fields (GitHub Pages supports up to ~1 GB total, ~2–5 MB per field).

## Contents

- `index.json` — catalog of available baked targets (`{ "targets": [...] }`)
- `<target-id>/` — baked per-target bundles (`manifest.json`, `frames/*.json`, `frames/*.png`)
- `.nojekyll` — ensures GitHub Pages serves all files without Jekyll filtering

## Baking a New Field

From the `spherex-blink` repository root:

```powershell
uv run --project backend python -m spherex_blink field `
  --ra <deg> --dec <deg> --fov 10 `
  --id <short-id> `
  --out D:\Workspace\spherex-blink-data\<short-id>
```

Then add the target's metadata entry to `index.json`.

## Hosting & CORS

Enable GitHub Pages on this repository (`main` branch, `/` root). GitHub Pages serves static JSON and PNG files with permissive CORS headers (`Access-Control-Allow-Origin: *`), so `spherex-blink` can fetch `index.json` and target bundles directly in the browser.

You can also test a custom data root in `spherex-blink` by appending `?data=https://...` to the app URL.

## License & Credits

- Repository code/scripts: MIT (`LICENSE`)
- Sky data: NASA/IPAC IRSA SPHEREx Public Data, Gaia DR3 (ESA), and Simbad (CDS)
