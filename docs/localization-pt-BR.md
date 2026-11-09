# Brazilian Portuguese (PT-BR) localization

This branch brings the PT-BR translation data from
[MC_LA_Recompiled](https://github.com/robertoaraujo77/MC_LA_Recompiled)
into this fork while keeping this fork's existing game and launcher code.

## What is included

- Curated dialogue and subtitle translations under `localization/pt-BR/`.
- Native UI/resource translations in `native-texts.json`.
- A local resource builder, `localization/build_ptbr.py`, which writes a translated
  copy of the extracted game's archive under `out/localization/pt-BR/game`.
- A generated Flash-menu lookup in `src/ptbr_menu.h`.
- The `mcla_ptbr` boolean cvar. When enabled, supported labels written by the
  in-game settings menu are translated.

## In-game menu text

Set `mcla_ptbr = true` in the MCLA settings file (or through the cvar interface).
The default is off, so existing installations keep their current wording.

The lookup only covers the strings in `localization/pt-BR/host-menu-texts.json`.
It does not translate every screen in the game or the launcher's UI.

## Building translated game resources

The builder requires a legally obtained, extracted compatible game installation
containing `default.xex` and `xarchive_cache.rpf`. It never writes into that
source directory; the translated archive is produced separately.

On Windows, with Python and the project's ReXGlue SDK source checkout available
at `third_party/rexglue-sdk`:

```powershell
python localization/build_ptbr.py --game-root .\game --output .\out\localization\pt-BR\game
```

The builder imports AES/XEX helpers from
`launcher/dev/shaderpack/build_pack.py`, validates the expected source-resource
hashes, preserves non-English language blocks and subtitle timing, verifies the
new archive, and only then publishes the output. The SDK checkout is a local
build dependency and is not committed here.

## Scope and validation

This is an integration of the translation assets and the settings-menu lookup,
not a claim that every game resource or launcher screen is translated. A full
Windows build and an in-game test against a matching game dump are still needed
before treating the integration as release-ready.
