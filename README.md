# XKCD Offline Tool

A Go CLI tool for downloading, indexing, and searching XKCD comics offline. Implementation of Exercise 4.12 from "The Go Programming Language" book.

## Features

- **Download and index** all XKCD comics locally
- **Search** comics by keywords in title, alt text, and transcript
- **View** specific comics by number
- **Random comic** generator
- **Statistics** about your local comic collection

## Installation

```bash
git clone <repository-url>
cd xkcd
```

## Usage

### Update Index (Must be run before any other command)
Download and update the local comic index:
```bash
go run xkcd.go update
```

### Search Comics
Search for comics containing specific keywords:
```bash
go run xkcd.go search "programming python"
go run xkcd.go search "regex"
```

### Show Specific Comic
Display a specific comic by number:
```bash
go run xkcd.go show 353
```

### Random Comic
Display a random comic from your collection:
```bash
go run xkcd.go random
```

### Statistics
View statistics about your local comic collection:
```bash
go run xkcd.go stats
```

## How It Works

1. **Index Creation**: The tool fetches comic metadata from XKCD's JSON API and stores it locally in `xkcd_index.json`
2. **Search Algorithm**: Uses weighted scoring - title matches score higher than alt text, which scores higher than transcript matches
3. **Rate Limiting**: Includes delays between API requests to be respectful to XKCD's servers
4. **Incremental Updates**: Only downloads new comics when updating an existing index

## Data Storage

Comics are stored in `xkcd_index.json` with the following structure:
- Comic metadata (title, alt text, transcript, etc.)
- Last update timestamp
- Highest comic number indexed

## Dependencies

- Go standard library only
- No external dependencies required