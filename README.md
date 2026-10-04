# ubuntu-pipewire-easyeffects-config

An [EasyEffects](https://github.com/wwmm/easyeffects) speaker preset that gives laptop speakers a richer, premium sound on Linux (PipeWire).

## Presets

- `output/Coffee-Tuned.json` — Premium-style speaker tuning (warm low end, smooth mids, airy treble, gentle compression, wider stereo). Tuned on an ASUS TUF Gaming F17 (FX706HF).

Effects chain, in order:

| Effect | What it does |
|---|---|
| Equalizer | −5 dB input headroom, cut below 70 Hz, +4 dB low shelf at 120 Hz, +2 dB warmth at 200 Hz, −2.5 dB at 450 Hz (boxy tone), −1.5 dB at 2.5 kHz (harshness), +1 dB at 5 kHz, +3.5 dB high shelf at 12 kHz |
| Bass Enhancer | Adds harmonics below 150 Hz so small speakers sound deeper |
| Compressor | Gentle 2:1 compression for a fuller, denser sound |
| Stereo Tools | Widens the stereo image (stereo base 0.4) |
| Limiter | Caps output at −1 dB to prevent clipping |

Software can't replace speaker hardware — this recreates the *sound character*, not the physical bass of bigger, premium speaker drivers.

## Requirements

- Linux with **PipeWire** as the sound server (default on Ubuntu 22.10+, Fedora 34+, Debian 12+, Pop!_OS, current Arch/Manjaro). Check with:
  ```sh
  systemctl --user is-active pipewire   # should print "active"
  ```
- **EasyEffects 7.0 or newer.** Check with `easyeffects --version`. If your distro ships an older version (e.g. Ubuntu 22.04 has 6.x), use the Flatpak install below.

## Compatibility

| EasyEffects | Source | Status |
|---|---|---|
| 8.3.0 | Flatpak (Flathub) — same build on every distro | ✅ Tested: all 5 effects load, preset values applied, no errors |
| 8.1.2 | Ubuntu 26.04 (apt) | ✅ Tested: all 5 effects load, preset values applied |
| 7.x | Distro packages (e.g. Ubuntu 24.04, Debian 13) | ⚠️ Expected to work, not tested |
| 6.x and older | e.g. Ubuntu 22.04 apt package | ❌ Not supported — use Flatpak |

## Install

### Option A — Flatpak (recommended, works on any distro)

```sh
flatpak install flathub com.github.wwmm.easyeffects
git clone https://github.com/Haynes79/ubuntu-pipewire-easyeffects-config.git
mkdir -p ~/.var/app/com.github.wwmm.easyeffects/data/easyeffects/output
cp ubuntu-pipewire-easyeffects-config/output/Coffee-Tuned.json ~/.var/app/com.github.wwmm.easyeffects/data/easyeffects/output/
flatpak run com.github.wwmm.easyeffects
```

Then pick **Coffee-Tuned** from the **Presets** menu.

### Option B — Distro package

Install EasyEffects with your package manager:

```sh
sudo apt install easyeffects      # Ubuntu / Debian / Mint / Pop!_OS
sudo dnf install easyeffects      # Fedora
sudo pacman -S easyeffects        # Arch / Manjaro
```

Then add and load the preset:

```sh
git clone https://github.com/Haynes79/ubuntu-pipewire-easyeffects-config.git
mkdir -p ~/.local/share/easyeffects/output
cp ubuntu-pipewire-easyeffects-config/output/Coffee-Tuned.json ~/.local/share/easyeffects/output/
easyeffects -l Coffee-Tuned
```

> Install **either** the Flatpak or the distro package, not both — two copies fight over the same audio device.

### Alternative: import from the app

Download `Coffee-Tuned.json`, open EasyEffects, go to **Presets → Import**, and choose the file.

## Make it load automatically

- **Start with your session:** in EasyEffects' Preferences (☰ menu), enable starting the service at login. Or from a terminal (distro package install):
  ```sh
  mkdir -p ~/.config/autostart
  printf '[Desktop Entry]\nType=Application\nName=Easy Effects\nExec=easyeffects --service-mode --hide-window\n' > ~/.config/autostart/easyeffects-service.desktop
  ```
- **Only for your laptop speakers:** in the **Presets** menu, use the autoload option to link your speaker device to **Coffee-Tuned**. Headphones and Bluetooth devices then keep their own settings.

## Tuning it for your laptop

Every laptop's speakers are different, so small tweaks help:

| If it sounds… | Change |
|---|---|
| Boomy or muddy | Bass Enhancer → lower **Amount** (6 → 3–4) |
| Thin | Equalizer → raise the 120 Hz band (4 → 5–6 dB) |
| Too bright or hissy | Equalizer → lower the 12 kHz band (3.5 → 2 dB) |
| Hollow or too wide | Stereo Tools → lower **Stereo Base** (0.4 → 0.2) |
| Too quiet | Raise system volume; or Equalizer input gain (−5 → −3 dB) |

Click **Save** on the preset to keep your changes.

## Troubleshooting

- **Sound doesn't change:** turn off global bypass with `easyeffects -b 2`, and check in Preferences that EasyEffects is set to process all output streams.
- **Crackling at high volume:** lower the Bass Enhancer amount or the 120 Hz band; your speakers are being pushed too hard.
- **"No output presets" / preset not listed:** check the file is in the right folder for your install type (Flatpak vs distro package — see above), then restart EasyEffects (`easyeffects -q`, then start it again).
- **Preset loads but sounds wrong on EasyEffects 6.x:** that version uses an older preset format. Install the Flatpak instead.

## Uninstall

```sh
# Distro package install
rm ~/.local/share/easyeffects/output/Coffee-Tuned.json
# Flatpak install
rm ~/.var/app/com.github.wwmm.easyeffects/data/easyeffects/output/Coffee-Tuned.json
```

To remove EasyEffects itself: `sudo apt remove easyeffects` (or your distro's equivalent), or `flatpak uninstall com.github.wwmm.easyeffects`.
