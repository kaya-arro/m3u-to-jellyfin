
# Jellyfin Smart M3U Importer

> Import local `.m3u` or `.m3u8` playlists into Jellyfin as **native, editable playlists**; with smart fuzzy matching and duplicate prevention.

---

## Why?
Jellyfin treats local m3u files as "Read-Only." This tool lets you edit playlists in the Jellyfin UI, even if your filenames have changed (e.g., after using Beets or MusicBrainz). It uses fuzzy matching to find the right tracks, even with typos or renamed files.

---

## Features

- **Smart Indexing:** Loads your library once, builds a fast lookup index.
- **Fuzzy Matching:** Finds tracks even with typos or renamed files.
- **Deep Cleaning:** Ignores junk in filenames (e.g., `[Official Video]`, `(Lyrics)`, `ft.`, `feat.`, leading "The").
- **Update Mode:** Adds only missing tracks to existing playlists, skips duplicates.
- **Non-Destructive:** Uses the Jellyfin API—never touches your database files.

---

## Requirements

- Python 3
- `requests` library

```bash
pip install requests
```

---

## Usage

You can run the script with command-line options or by editing the config at the top of `smart_import.py`.

### Command-Line Options

| Option                | Description                                 | Default                |
|-----------------------|---------------------------------------------|------------------------|
| `-u`, `--url`         | Jellyfin server URL                         | `http://localhost:8096`|
| `-k`, `--api-key`     | Jellyfin API key                            | *(empty)*              |
| `-i`, `--user-id`     | Jellyfin user ID                            | *(empty)*              |
| `-f`, `--m3u-folder`  | Folder containing `.m3u` files              | *(empty)*              |
| `-t`, `--threshold`   | Fuzzy match threshold (0-1)                 | `0.85`                 |

Example:

```bash
python3 smart_import.py -u http://localhost:8096 -k <API_KEY> -i <USER_ID> -f /path/to/m3u/folder
```

Or just run:

```bash
python3 smart_import.py
```

If you don't provide options, the script uses the config at the top of `smart_import.py`.

---

## Output

The script runs quietly. It only prints filenames it cannot match in your library. After import, you may want to delete the original m3u/m3u8 files to avoid duplicate playlists in Jellyfin.

---

## License

See the LICENSE file (AGPLv3).
