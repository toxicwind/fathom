# fathom

Thin coordinator pen for **binary format decoders** — tools that make opaque
proprietary files readable, diffable, and versionable. Named for the act of
fathoming: measuring the depth of a format.

## Products

- `products/gzxml-decode` — decoder for gzip+XML document files (the format the
  DAW saves as `.als`): `gzxml header|decode|encode`.
- `products/binprefs` — decoder for the DAW's binary `Preferences.cfg`:
  `apt decode|find`.

## Ground truth

- Ports: `ssot/ports.env` (canonical: `estate/config/ports.env`)
- Formats are reverse-engineered from real files; verify against live files,
  never prose.