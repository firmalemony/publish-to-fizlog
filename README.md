# Publish to Fizlog

Post a changelog entry to your [Fizlog](https://fizlog.com) "what's new" widget every time you publish a GitHub release. Your users see the update in-app, on your public changelog page and in RSS — without you copy-pasting release notes.

## Usage

1. In Fizlog, open your project → **API access** and copy the API key.
2. Add it to your repository as a secret named `FIZLOG_API_KEY` (Settings → Secrets and variables → Actions).
3. Add `.github/workflows/fizlog.yml`:

```yaml
name: Changelog
on:
  release:
    types: [published]

jobs:
  fizlog:
    runs-on: ubuntu-latest
    steps:
      - uses: firmalemony/publish-to-fizlog@v1
        with:
          api-key: ${{ secrets.FIZLOG_API_KEY }}
```

The release name becomes the entry title and the release notes become the body.

## Inputs

| Input | Default | Description |
|---|---|---|
| `api-key` | — (required) | Project API key. Always pass it from a secret. |
| `title` | release name → tag | Entry title. |
| `body` | release notes | Entry body (bold, italic, code, links, `- ` lists). |
| `type` | `new` | `new`, `improved` or `fixed`. |
| `notify` | `false` | Email the project's subscribers. |
| `draft` | `false` | Save as a draft instead of publishing. |
| `api-url` | `https://fizlog.com/api/entries.php` | Only change if you self-host Fizlog. |

## Outputs

`entry-id` and `public-page` (URL of your public changelog).

## Example: publish from any workflow

```yaml
- uses: firmalemony/publish-to-fizlog@v1
  with:
    api-key: ${{ secrets.FIZLOG_API_KEY }}
    title: "Faster exports"
    body: "CSV exports are now **3× faster**."
    type: improved
```

Runs on Linux and macOS runners (uses `curl` and `jq`, both preinstalled on GitHub-hosted runners).

## License

MIT
