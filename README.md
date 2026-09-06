# JC-Projector

Visual map of **JCkernel** source onto hardware.

Not a live debugger. Not CSF1 Viewer.

- **Viewer** reads a CSF1 image *after* the kernel writes CrashDump.
- **Projector** answers: this file talks to that chip, and this serial letter died on that chip.
- **QEMU serial** is still the only live proof (`tee boot64.log`).

## What you see

| Layer | Meaning |
|---|---|
| Hardware blocks | CPU, MMU, GOP, PIC, NVMe, USB, CSF1, serial, loader |
| Source files | `paging.c` → MMU, `main.asm` → GOP + ExitBootServices |
| Serial trail | paste `6kbcdAB2CP` → last letter lights the block |

## What it is not

Does not run the kernel. Does not read 7290 registers. Cannot invent a log the kernel never wrote.

A paging hang (`AB2CP`) never reaches CSF1. Projector can still point at MMU / `paging.c`. Viewer cannot.

## Run

Open `projector.html` in a browser, or:

```
python3 -m http.server 8765
# http://127.0.0.1:8765/projector.html
```

Drop a JCkernel source zip if you want file names highlighted. The zip is scanned by path only.

Edit `map.json` to add chips or serial letters.

Kernel stays private. This repo is public on purpose, same idea as CSF1-Viewer-*.
