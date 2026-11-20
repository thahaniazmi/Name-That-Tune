# Name That Tune

[![Spotify](https://img.shields.io/badge/Spotify-1ED760?style=flat&logo=spotify&logoColor=white)](https://spotify.com)
[![Spicetify](https://img.shields.io/badge/Spicetify-Custom_App-orange?style=flat)](https://spicetify.app)
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](LICENSE)

> **Credits & Acknowledgements:**
> This repository is a fork / distribution of the original **[Name That Tune](https://github.com/theRealPadster/name-that-tune)** custom app for Spicetify created and maintained by **[@theRealPadster](https://github.com/theRealPadster)**. All original ideas, implementation, and credits rightfully belong to them. Please check out and star the [original repository](https://github.com/theRealPadster/name-that-tune)!

**This project is not complete/bug-free. If you have suggestions or bug fixes, feel free to contribute.**

Name That Tune is [Heardle](https://en.wikipedia.org/wiki/Heardle) made for [Spicetify](https://spicetify.app) — guess the song from progressively longer snippets. Spotify acquired the original and shut it down in 2023; this keeps the game alive inside their own desktop client.

`#spotify` `#spicetify` `#spicetify-app` `#spicetify-custom-apps` `#spicetify-extensions` `#plugins` `#apps` `#heardle` `#music-game` `#quiz`

![Preview screenshot](docs/preview-2026-09.png)

## Table of contents
  - [Credits](#credits)
  - [Installation](#installation)
  - [Usage](#usage)
  - [Translations](#translations)
  - [Planned Features](#planned-features)

## Credits
This project is based on the work by **[theRealPadster](https://github.com/theRealPadster)** on [theRealPadster/name-that-tune](https://github.com/theRealPadster/name-that-tune). Special thanks to the creator and contributors for designing and building this awesome Spicetify extension!

## Installation

### Method 1: Automatic / Quick Install (Recommended)

Run one of the commands below in your terminal. This downloads the latest ready-to-run app directly into your Spicetify `CustomApps` directory, enables it, and applies it to Spotify automatically:

#### **Windows (PowerShell)**
```powershell
$path = "$env:APPDATA\spicetify\CustomApps\name-that-tune"
if (Test-Path $path) { Remove-Item -Recurse -Force $path }
Invoke-WebRequest -Uri "https://github.com/thahaniazmi/Name-That-Tune/archive/refs/heads/dist.zip" -OutFile "$env:TEMP\name-that-tune.zip"
Expand-Archive -Path "$env:TEMP\name-that-tune.zip" -DestinationPath "$env:TEMP" -Force
Move-Item "$env:TEMP\Name-That-Tune-dist" $path
spicetify config custom_apps name-that-tune
spicetify apply
```

#### **Linux / macOS (Bash / Zsh)**
```bash
APPS_DIR="${HOME}/.config/spicetify/CustomApps"
mkdir -p "$APPS_DIR"
rm -rf "$APPS_DIR/name-that-tune"
curl -sSL "https://github.com/thahaniazmi/Name-That-Tune/archive/refs/heads/dist.zip" -o /tmp/name-that-tune.zip
unzip -q /tmp/name-that-tune.zip -d /tmp/
mv /tmp/Name-That-Tune-dist "$APPS_DIR/name-that-tune"
spicetify config custom_apps name-that-tune
spicetify apply
```

---

### Method 2: Manual Installation

1. Download the pre-built **[dist branch zip](https://github.com/thahaniazmi/Name-That-Tune/archive/refs/heads/dist.zip)**.
2. Unzip the file and rename the extracted folder to `name-that-tune`.
3. Move the `name-that-tune` folder into your Spicetify `CustomApps` folder:
   | **Platform**    | **Path**                               |
   |-----------------|----------------------------------------|
   | **Windows**     | `%appdata%\spicetify\CustomApps`       |
   | **Linux/macOS** | `~/.config/spicetify/CustomApps`       |

4. Run the following commands in your terminal:
   ```bash
   spicetify config custom_apps name-that-tune
   spicetify apply
   ```

---

### Method 3: Build From Source (For Developers)

```bash
git clone https://github.com/thahaniazmi/Name-That-Tune.git
cd Name-That-Tune
pnpm install
pnpm run build
spicetify config custom_apps name-that-tune
spicetify apply
```

## Usage
- Right-click on any artist, playlist, album, folder, or your Liked Songs, and choose **Play Name That Tune**. You can also select several songs and right-click them.
- Before your first guess, pick **Intro** to hear clips from the beginning of the song, or **Random spot** to hear every clip from the same random point later in it.
- Click **Play** to hear the current clue. The six clue lengths are 1, 2, 4, 7, 11, and 16 seconds.
- Guess the title or skip to unlock the next clue. The song is revealed when you get it right.
- If you miss all six, choose **Keep guessing** for longer clips (22s, 29s, and so on), or **Give up and reveal**.
- (If you open the app directly from the header bar, it will just use the song you are currently playing.)

## Translations
I've added translations support! If you use Spotify in a non-English language and are getting the "Play Name That Tune" menu item etc in English, you can get your language added by either:

- Making a [new issue](https://github.com/theRealPadster/name-that-tune/issues/new?labels=i18n&template=new_translation.yml) with the translated contents of [`src/locales/en.json`](https://github.com/theRealPadster/name-that-tune/blob/main/src/locales/en.json). No setup needed — I'll wire it up.
- Or submitting a pull request:
  1. Copy `src/locales/en.json` to `src/locales/<locale>.json` and translate the values.
  2. **Register it in [`src/i18n.ts`](https://github.com/theRealPadster/name-that-tune/blob/main/src/i18n.ts)** — add the import and one entry to the `resources` map. A locale file that isn't listed there is never loaded, and the app silently falls back to English.

`<locale>` has to match what Spotify reports, hyphens and all: `pt-BR`, `es-419`, `zh-CN` — not `ptBR`. You can check your own in the Spotify devtools console with `Spicetify.Locale.getLocale()`.

Some languages need more plural forms than English does. Keys like `songWithCount` and `sendingURIs` use i18next's `_one` / `_other` suffixes; if your language also needs `_few` or `_many` (Polish, for instance), add those keys too.

## Planned Features
- Come up with a better name
