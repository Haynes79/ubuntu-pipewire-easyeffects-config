# ubuntu-pipewire-easyeffects-conig

EasyEffects output presets for Ubuntu (PipeWire).

## Presets

- `output/Coffee-Tuned.json` — Premium-style speaker tuning (warm low end, smooth mids, airy treble, gentle compression, wider stereo). Tuned on an ASUS TUF Gaming F17 (FX706HF).
- `output/TUF-Speakers.json` — Lighter laptop-speaker tuning for the ASUS TUF Gaming F17 (bass boost, presence lift, slight stereo widening, limiter).

## Install

```sh
sudo apt install easyeffects
cp output/*.json ~/.local/share/easyeffects/output/
easyeffects -l Coffee-Tuned   # or: easyeffects -l TUF-Speakers
```

Flatpak installs use `~/.var/app/com.github.wwmm.easyeffects/data/easyeffects/output/` instead.
