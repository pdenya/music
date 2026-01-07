# music-cli

A simple command-line interface for managing Apple Music playlists on macOS.

## Requirements

- macOS with the Music app
- No additional dependencies

## Installation

```bash
# Clone or download, then make executable
chmod +x music

# Optionally add to your PATH or create an alias
alias music="/path/to/music"
```

## Usage

### List all playlists

```bash
music playlists
```

### List songs in a playlist

```bash
music playlist "My Playlist"
```

### Create a new playlist

```bash
music create "New Playlist"
```

### Add songs to a playlist

```bash
# Add by song name (partial match)
music add "My Playlist" "Bohemian Rhapsody"

# Add by artist
music add "My Playlist" "artist:Queen"

# Add by album
music add "My Playlist" "album:News of the World"
```

### Remove a song from a playlist

```bash
music remove "My Playlist" "Bohemian Rhapsody"
```

### Export a playlist to a file

```bash
music export "My Playlist" > my-playlist.txt
```

Exports with full metadata (track count, duration, album, year).

### Import a playlist from a file

```bash
music import my-playlist.txt
```

Recreates the playlist by searching your library and existing playlists for matching tracks.

### Delete a playlist

```bash
music delete "My Playlist"
```

## Examples

```bash
# Create a workout playlist and add some songs
music create "Workout"
music add "Workout" "Eye of the Tiger"
music add "Workout" "Lose Yourself"

# Check what's in it
music playlist "Workout"

# Remove a song
music remove "Workout" "Eye of the Tiger"
```

## Playlist Rotation Workflow

Keep a small set of active playlists while archiving others to git:

```bash
# Archive playlists you're not using
music export "Summer 2024" > playlists/Summer\ 2024.txt
music delete "Summer 2024"

# Commit to git for safekeeping
git add playlists/
git commit -m "Archive Summer 2024 playlist"

# Bring it back anytime
music import "playlists/Summer 2024.txt"
```

## How It Works

This tool uses AppleScript to communicate directly with the Music app. All operations happen through the native macOS scripting bridge, so there's no need for API keys or external services.

## License

MIT
