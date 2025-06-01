# ipck

A Bash script to analyse access logs, rank the most active IP addresses, resolve hostnames, and optionally flag likely bots using [AbuseIPDB](https://www.abuseipdb.com/).

## Features

- Sort and rank IPs by request count from any standard access log
- Resolve PTR records for IPs
- Integrate with AbuseIPDB to check reputation and score
- Filter results to show only likely bots
- Cache AbuseIPDB results locally to reduce API usage

## Requirements

- `curl`
- `jq`
- `host` (from `bind-utils` or similar)
- AbuseIPDB API key (only needed if using `--abuseip` or `--onlybots`)

## Usage

```bash
ipck.sh LOG_FILE [LIMIT] [--abuseip] [--onlybots]
```

### Arguments

- `LOG_FILE`: Path to the access log to analyse
- `LIMIT`: (Optional) Number of top IPs to display (default: 10)
- `--abuseip`: Query AbuseIPDB for each IP and show reputation data
- `--onlybots`: Only display IPs flagged as likely bots (enables `--abuseip`)

### Examples

```bash
# Show top 10 IPs from a log file
./ipck.sh /var/log/nginx/access.log

# Show top 25 IPs with AbuseIPDB checks
./ipck.sh /var/log/nginx/access.log 25 --abuseip

# Show only likely bots (with abuse score >= 50)
./ipck.sh /var/log/nginx/access.log --onlybots
```

## AbuseIPDB API Key

To use AbuseIPDB lookups, you’ll need an API key.

Set it as an environment variable:

```bash
export ABUSE_KEY="your_api_key_here"
```

Or edit the script and replace the placeholder value in:

```bash
ABUSE_KEY="${ABUSE_KEY:-YOUR_ABUSEIPDB_API_KEY_HERE}"
```

## License

MIT
