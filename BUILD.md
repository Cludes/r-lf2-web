# Build / update notes

## The in-browser game (original LF2)

The disk image is a Windows 95 install with LF2 v1.9, plus a v86 saved state captured while LF2 is
running (so the page resumes straight into the game).

To repackage the image after changes (it's a raw 200 MB FAT16 disk, partition at byte offset 32256):

```sh
# inject/replace files in the FAT partition with mtools or pyfatfs, then:
gzip -c windows95.img > w.gz
split -b $(( ($(stat -c %s w.gz) + 2) / 3 )) -d -a 1 w.gz part   # -> part0 part1 part2
# rename to windows95.img.part1.gz / .part2.gz / .part3.gz
```

The saved state must be recaptured (via the page's "Save game state" button) if `memory_size` changes.

## R-LF2 (download only)

`LF2_Reinforced.zip` is the official self-extractor from lf-empire.de. R-LF2 does NOT run in the
browser - its sprite sheets (up to 4000 px wide) exceed Win95/98 DirectDraw surface limits. See README.

A future attempt at in-browser R-LF2 would need a Windows 2000/XP image with DX7+ in v86 (heavy/slow) -
not pursued.
