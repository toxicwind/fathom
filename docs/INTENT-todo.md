# fathom — INTENT todo (audit 2026-11-01)

The **fathom** pen is the estate's music-production + livecoding surface. This
file is the live intent ledger: what exists, what state everything is in, what
is native vs vendored vs private, and the concrete forward work.

## Estate map

| product | repo | scope | state | origin |
|---------|------|-------|-------|--------|
| `plumb` | toxicwind/plumb | spectral before/after webapp (Sound the Depths) | clean, built, served `:8088` | native (this session) |
| `trench` | toxicwind/trench | procedural 140bpm tearout renderer (numpy/scipy) | clean, 9/9 tests | vendored (torbox tarball) |
| `strudel-dev-vite` | toxicwind/strudel-dev-vite | strudel workbench monorepo; `@toxicwind/strudel-voices` | clean; sampler bootstrap committed | native + strudel ecosystem |
| `strudel-mcp` | toxicwind/strudel-mcp (fork of live-coding-music-mcp) | cross-platform music MCP; NO-LOSS strudel↔Ableton (INTENT.md) | clean; no-loss carrier committed | fork (upstream retained) |
| `strudel-sampler-server-vite` | toxicwind/strudel-sampler-server-vite | sample-library backend | clean | native + strudel |
| `m3u-toolkit` | toxicwind/m3u-toolkit | live-web stream manifest toolkit | clean | native |
| `linux-serum-synth` (ZYG-ZXG) | zznorthstar/linux-serum-synth (upstream) | native Linux Serum-2-compatible synth (VST3/CLAP/render) | clean, built; fork point for serum-fork-private | upstream vendor |

## Private vs public boundary (critical)

| scope | location | github | content |
|-------|----------|--------|---------|
| **private** | `samples/abyss/` (gitignored) | `serum-fork-private` (PRIVATE, opaque) | Serum 2 installer/unpack, deob notes (VST3, SetupLdr, XfsX .fxp), vendored SerumPreset corpus |
| **private** | `samples/serum2/` (gitignored) | — (never) | Serum 2 installer (1.3 GB), never pushed |
| **public-clean** | products/* | their repos | no Xfer code, no serum branding, no big binaries |

`INTENT.md` overrides ALL file docs. `INTENT_RESEARCH_*.md` records the
bridge-stack research. Never let private refs leak into public READMEs.

## ★ Your domain feature — strudel → Ableton AND Ableton → strudel, no loss

- [x] `murk:<base64>` code carrier in `MIDIExportService.convertToMidi` (code embeds
  in the first melodic track name — survives Ableton round-trip)
- [x] `MIDIExportService.codeFromMidi(midi)` decoder (recovers source verbatim)
- [ ] **Ableton tool set** (Live Extensions SDK): session/clip/export that uses the
  carrier on the Ableton side — `MIDIExportService` covers the strudel→Ableton leg;
  the Ableton→strudel leg needs a Live-extension to read track names / `.als`
- [ ] **strudel-live convention** — the code-embedded-in-WAV carrier the research
  doc recommends for full-no-loss when audio (not just MIDI) round-trips

## Cross-platform matrix (INTENT.md:2)

| OS | strudel | DAW main | VSTi |
|----|---------|----------|------|
| win32 | browser + local workbench | Ableton Live | Serum 2 VST3 (abyss) |
| darwin | browser + local workbench | Ableton Live | Serum 2 AU/VST3 |
| linux | `:8088` workbench + `:55432` sampler | — (strudel main) | `zygzxg_render` offline (no DAW) |

- [x] `src/platform.ts` + `src/platform.test.ts` (per-OS DAW/VSTi/strudel target)
- [ ] wire platform→ ableton/VSTi tool dispatch
- [ ] register fathom-mcp in the estate **Thresher** gateway

## Ports (estate SSOT `config/ports.env`)

- `ABYSS_PORT=25261` · `STRUDEL_SAMPLER_PORT=55432` · dev workbench `:8088`

## Samples

- `samples/torbox/` (Excision, WonkyRiddim, PORTIFY — gitignored pull)
- `samples/BVKER-THREAT/`, `samples/XLNTSOUND-Tearout-Vol2/`, `samples/Tisoki-Sounds-Vol1/`
- `samples/strudel-root/` — 45 banks served by the sampler (incl. `Serum/*` VoIP
  rendered from BVKER .SerumPreset via `zygzxg_render`, named by category not brand)

## Forward (next actionable)

1. Thriller: wire `platform.ts` → Ableton Live Extension + Live Link tools.
2. VSTi render MCP tool (private abyss bridge; public facade hides the brand).
3. Register fathom-mcp in Thresher MCP gateway.
4. Docs site (docs-something): aesthetic live site over these .md files.