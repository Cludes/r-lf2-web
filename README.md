# Little Fighter 2 in the browser (+ R-LF2 download)

A static GitHub Pages site that:

- **Plays the original Little Fighter 2 in the browser** - it runs Windows 95 in the
  [v86](https://github.com/copy/v86) x86 emulator (compiled to WebAssembly) and resumes from a saved
  state straight into the game.
- **Offers Reinforced LF2 (R-LF2) as a download** for Windows.

## Why R-LF2 isn't playable in-browser (yet)

R-LF2's "reinforced" sprite sheets are huge (up to 4000x1200 px). Windows 95/98-era DirectDraw - which
is what the in-browser emulator can run - cannot create surfaces that large, so R-LF2 fails on load with
"Couldn't create art surface". The original LF2's sprites are small enough (~640 px), so it runs fine.
R-LF2 would need Windows 2000/XP-era DirectDraw, which is too heavy to emulate smoothly in a browser.
It runs perfectly on a normal Windows PC, hence the download.

## Files

- `index.html` - the page; loads the disk image, resumes the state, shows the R-LF2 download.
- `windows95.img.part{1,2,3}.gz` - Windows 95 + LF2 disk image, gzip-compressed and split into
  sub-100 MB parts. The browser concatenates and decompresses them with `DecompressionStream`.
- `win95-lf2-default.bin.zst` - v86 saved state; resumes instantly into running LF2.
- `LF2_Reinforced.zip` - the R-LF2 installer offered for download.
- `libv86.js`, `v86.wasm`, `seabios.bin`, `vgabios.bin` - the v86 runtime + BIOS.

`memory_size` in `index.html` (64 MB) must match the saved state.

## Credits / licensing

- Emulator: [v86](https://github.com/copy/v86) (BSD-2-Clause).
- Games: Little Fighter 2 (Marti & Starsky Wong) and Reinforced LF2 (Conrad Leung), freeware.
