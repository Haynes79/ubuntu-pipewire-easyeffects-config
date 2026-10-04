# ubuntu-pipewire-easyeffects-conig

EasyEffects output presets for Ubuntu (PipeWire).

## Presets

- `output/Coffee-Tuned.json` — Premium-style speaker tuning (warm low end, smooth mids, airy treble, gentle compression, wider stereo). Tuned on an ASUS TUF Gaming F17 (FX706HF).

## Install

```sh
sudo apt install easyeffects
cp output/Coffee-Tuned.json ~/.local/share/easyeffects/output/
easyeffects -l Coffee-Tuned
```

Flatpak installs use `~/.var/app/com.github.wwmm.easyeffects/data/easyeffects/output/` instead.
