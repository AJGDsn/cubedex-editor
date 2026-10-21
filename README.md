# CubeDex Editor

A standalone, browser-based editor for [Cubedex](https://cubedex.app/) algorithm libraries.

Open `CubeDex-Editor.html` in a modern browser (Chrome or Edge recommended) and load a Cubedex JSON export. You can browse, add, rename, reorder, move, and delete sets, subsets, and algorithms, then export the library back to JSON.

## Features

- **Puzzle-aware navigation** — 3×3, 2×2, 4×4, 5×5, Pyraminx, and Megaminx each get their own library view.
- **Correct key handling** — new sets automatically receive the right puzzle prefix, and renaming a set keeps its prefix intact.
- **Move sets between puzzles** — converts an unprefixed 3×3 key to a prefixed key (and back) without editing JSON by hand.
- **Search across every puzzle** — click a result to jump straight to that set and subset.
- **Drag and drop** — reorder sets, subsets, and algorithms.
- **Safe round-tripping** — export keeps every loaded key, including sets on puzzles that are not currently selected.
- **Import validation** — rejects files that do not match the Cubedex library shape.

## Cubedex library format

A Cubedex library is one flat JSON object:

```json
{
  "PLL": [
    {
      "subset": "Adjacent Corners",
      "algorithms": [
        { "name": "T Perm", "algorithm": "(R U R' U') ..." }
      ]
    }
  ],
  "2x2x2:CLL": [ ... ],
  "pyraminx:Last Layer": [ ... ]
}
```

The puzzle is encoded in the set key:

| Puzzle | Key prefix | Example |
| --- | --- | --- |
| 3×3 | none | `PLL` |
| 2×2 | `2x2x2:` | `2x2x2:CLL` |
| 4×4 | `4x4x4:` | `4x4x4:PLL Parity` |
| 5×5 | `5x5x5:` | `5x5x5:Last Two Edges` |
| Pyraminx | `pyraminx:` | `pyraminx:Last Layer` |
| Megaminx | `megaminx:` | `megaminx:OLL` |
| Square-1 | `square1:` | legacy libraries only |

The prefix is recognised only when it exactly matches a known puzzle ID; otherwise the whole key is treated as a 3×3 set name. This mirrors the upstream [`puzzles.ts`](https://github.com/poliva/cubedex/blob/main/src/lib/puzzles.ts) implementation.

## Notes

- This is an unofficial companion tool, not part of the Cubedex application.
- The editor is a single HTML file and runs entirely in the browser; nothing is uploaded.
- If Cubedex adds another puzzle ID in future, add it to the `PUZZLES` list near the top of the editor script.

## License

This is free and unencumbered software released into the public domain under the [Unlicense](LICENSE). No copyright claim is made.
