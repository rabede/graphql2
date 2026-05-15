## BirdBuddy Postcard Media Downloader

GraphQL endpoint:

https://graphql.app-api.prod.aws.mybirdbuddy.com/graphql

This script logs in to BirdBuddy, fetches all postcards for a given day, and downloads postcard media locally.

## Requirements

- Python 3.11+

## Credentials

Set credentials as environment variables:

```bash
export BIRDBUDDY_EMAIL="your-email@example.com"
export BIRDBUDDY_PASSWORD="your-password"
```

On Windows PowerShell:

```powershell
$env:BIRDBUDDY_EMAIL="your-email@example.com"
$env:BIRDBUDDY_PASSWORD="your-password"
```

Or create a local `.env` file in the project root:

```env
BIRDBUDDY_EMAIL=your-email@example.com
BIRDBUDDY_PASSWORD=your-password
```

## Usage

Run for a specific date:

```bash
python main.py --date 2026-05-10
```

Default output structure:

```text
output/
	YYYY-MM-DD/
		postcard_<id>/
			media_01.jpg
			media_02.mp4
```

## Useful Options

- `--output-dir <path>`: base output directory (default: `output`)
- `--timeout <seconds>`: HTTP timeout (default: `30`)
- `--max-pages <n>`: maximum pages to fetch (default: `30`)
- `--retries <n>`: download retry count (default: `2`)
- `--dry-run`: print media URLs and target files without downloading

Verbose diagnostic output is always enabled and no longer requires a CLI flag.

Example with custom output:

```bash
python main.py --date 2026-05-10 --output-dir downloads
```

## Notes

- The script uses BirdBuddy's `authEmailSignIn` mutation and then queries `me.feed`.
- Postcard media is fetched with `postcardMediasDetails(feedItemId: ...)`.
- The currently exposed downloadable URL field is `thumbnailUrl`; files are saved from that URL.