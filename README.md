# xkcd Offline Tool

A Go CLI tool for downloading, indexing, and searching XKCD comics offline. Implementation of Exercise 4.12 from "The Go Programming Language" book.

## Features

- **Download and index** all XKCD comics locally
- **Search** comics by keywords in title, alt text, and transcript
- **View** specific comics by number
- **Random comic** generator
- **Statistics** about your local comic collection

## Installation

```bash
git clone https://github.com/MrChildrenJ/xkcd-Offline.git
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
go run xkcd.go search "linux sudo"
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

## Demo

```bash
go run xkcd.go show 666

┌─ XKCD #666 ─────────────────────────────────────
│ Title: Silent Hammer
│ Date:  2009-11-23
│ URL:   https://xkcd.com//666/
│ Image: https://imgs.xkcd.com/comics/silent_hammer.png
├─ Alt Text ──────────────────────────────────────
│ I bet he'll keep quiet for a couple weeks and then-- wait,
│ did you nail a piece of scrap wood to my antique table a
│ moment ago?
├─ Transcript ────────────────────────────────────
│ [[Hat guy is hammering something on a table.]] Guy: What--
│ Hat Guy: Silent hammer. I've made a set of silent tools.
│ Guy: Why? Hammer: <<whoosh whoosh whoosh>> Hat Guy: Stealth
│ carpentry. Breaking into a house at night and moving
│ windows, adjusting walls, etc. [[He takes his silent hammer
│ over to a tool bench with other things on it. Two boxes
│ underneath are labeled "Drills" and "Non-Drills."]] Hat Guy,
│ narrating: After a week or so of questioning his own sanity,
│ the owner will stay up to watch the house at night. I'll
│ make scratching noises in the walls, pipe in knockout gas,
│ move him up to his bed, and never bother him again. [[The
│ events he's describing are shown in two mini-panels below.]]
│ Guy, off-panel: Nice prank, I guess, but what's the point?
│ Hat Guy: Check out the owner's card, on the table. Guy,
│ off-panel: Chair of the American Skeptics Society? Oh, god.
│ Hat guy: Yeah, this doesn't end well for him. {{Title text:
│ I bet he'll keep quiet for a couple weeks and then-- wait,
│ did you nail a piece of scrap wood to my antique table a
│ moment ago?}}
└─────────────────────────────────────────────────
```
```bash
go run xkcd.go search "silent hammer"

Found 38 comics matching 'silent hammer':

1. #666: Silent Hammer (score: 44)
   URL: https://xkcd.com//666/
   I bet he'll keep quiet for a couple weeks and then-- wait, did you nail a piece of scrap wood to my antique table a moment ago?

2. #1436: Orb Hammer (score: 27)
   URL: https://xkcd.com//1436/
   Ok, but make sure to get lots of pieces of rock, because later we'll decide to stay in a room on our regular orb and watch hammers hold themselves and hit rocks for us, and they won't bring us very many rocks.

3. #108: M.C. Hammer Slide (score: 22)
   URL: https://xkcd.com//108/
   Once, long ago, I saw this girl go by.  I didn't stop and talk to her, and I've regretted it ever since.

4. #2447: Hammer Incident (score: 19)
   URL: https://xkcd.com//2447/
   I still think the Cold Stone Creamery partnership was a good idea, but I should have asked before doing the first market trials during the cryogenic mirror tests.

5. #801: Golden Hammer (score: 19)
   URL: https://xkcd.com//801/
   Took me five tries to find the right one, but I managed to salvage our night out--if not the boat--in the end.

6. #1995: MC Hammer Age (score: 19)
   URL: https://xkcd.com//1995/
   Wait, sorry, I got mixed up--he's actually almost 50. It's the kid from The Karate Kid who just turned 40.

7. #578: The Race: Part 2 (score: 9)
   URL: https://xkcd.com//578/
   The Hammer + Captain Tightpants == Captain Hammerpants?

8. #1938: Meltdown and Spectre (score: 6)
   URL: https://xkcd.com//1938/
   New zero-day vulnerability: In addition to rowhammer, it turns out lots of servers are vulnerable to regular hammers, too.

9. #1926: Bad Code (score: 6)
   URL: https://xkcd.com//1926/
   "Oh my God, why did you scotch-tape a bunch of hammers together?" "It's ok! Nothing depends on this wall being destroyed efficiently."

10. #1222: Pastime (score: 4)
   URL: https://xkcd.com//1222/
   Good thing we're too smart to spend all day being uselessly frustrated with ourselves. I mean, that'd be a hell of a waste, right?

... and 28 more results

```