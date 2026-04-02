# SearXNG ToS-Compliant Configuration (Option 2)

## Context

This document is for the [SearXNG](https://github.com/searxng/searxng) metasearch engine.
It defines which engines are **allowed for programmatic access** per their Terms of Service, robots.txt, and API documentation, and provides a ready-to-use configuration.

- **Repo:** https://github.com/searxng/searxng
- **Engine source code:** `searx/engines/` (each engine is a Python module)
- **Default engine list:** `searx/settings.yml` (all 29 engines below verified present as of April 2026)
- **Docker deployment:** `container/docker-compose.yml` — settings go in `./core-config/settings.yml`
- **Docker docs:** https://docs.searxng.org/admin/installation-docker.html

> **Note:** The old `searxng-docker` repo has been deprecated (April 2026).
> Migration guide: https://docs.searxng.org/admin/installation-docker.html#migrate-from-searxng-docker

## Goal

Use only engines that are explicitly allowed for programmatic access. Fill the general web search gap with Brave Search API (paid).

## Engine Summary

### Free Engines (No Cost)

| Engine | API Key | Rate Limit | Free | Commercial | Verify At |
|--------|---------|------------|------|------------|-----------|
| `wikipedia` | No | 200 req/s | Yes | Yes (CC BY-SA) | [API Etiquette](https://www.mediawiki.org/wiki/API:Etiquette) |
| `wikidata` | No | 200 req/s | Yes | Yes (CC BY-SA) | [API Etiquette](https://www.mediawiki.org/wiki/API:Etiquette) |
| `wikicommons.images` | No | 200 req/s | Yes | Yes (CC BY-SA) | [API Etiquette](https://www.mediawiki.org/wiki/API:Etiquette) |
| `wikibooks` | No | 200 req/s | Yes | Yes (CC BY-SA) | [API Etiquette](https://www.mediawiki.org/wiki/API:Etiquette) |
| `wikiquote` | No | 200 req/s | Yes | Yes (CC BY-SA) | [API Etiquette](https://www.mediawiki.org/wiki/API:Etiquette) |
| `wikisource` | No | 200 req/s | Yes | Yes (CC BY-SA) | [API Etiquette](https://www.mediawiki.org/wiki/API:Etiquette) |
| `wikiversity` | No | 200 req/s | Yes | Yes (CC BY-SA) | [API Etiquette](https://www.mediawiki.org/wiki/API:Etiquette) |
| `wikivoyage` | No | 200 req/s | Yes | Yes (CC BY-SA) | [API Etiquette](https://www.mediawiki.org/wiki/API:Etiquette) |
| `wikinews` | No | 200 req/s | Yes | Yes (CC BY-SA) | [API Etiquette](https://www.mediawiki.org/wiki/API:Etiquette) |
| `wiktionary` | No | 200 req/s | Yes | Yes (CC BY-SA) | [API Etiquette](https://www.mediawiki.org/wiki/API:Etiquette) |
| `arxiv` | No | 1 req/3s | Yes | Yes | [API ToU](https://info.arxiv.org/help/api/tou.html) |
| `pubmed` | Recommended | 3 req/s (no key), 10 req/s (with key) | Yes | Yes | [E-utilities](https://www.ncbi.nlm.nih.gov/books/NBK25497/) |
| `library of congress` | No | 5,000 req/hr | Yes | Yes (public domain) | [LOC APIs](https://www.loc.gov/apis/) |
| `peertube` | No | Instance-configured | Yes | Yes (AGPL-3.0) | [API docs](https://docs.joinpeertube.org/api-rest-reference.html) |
| `github` | No | 60 req/hr (unauth), 5K/hr (auth) | Yes | Yes | [Rate limits](https://docs.github.com/en/rest/using-the-rest-api/rate-limits-for-the-rest-api) |
| `github code` | No | 60 req/hr (unauth), 5K/hr (auth) | Yes | Yes | [Rate limits](https://docs.github.com/en/rest/using-the-rest-api/rate-limits-for-the-rest-api) |
| `gitlab` | No | 7,200 req/hr | Yes | Yes | [Rate limits](https://docs.gitlab.com/security/rate_limits/) |
| `stackoverflow` | No | 300 req/day (no key), 10K/day (key) | Yes | Yes (CC BY-SA) | [API docs](https://api.stackexchange.com/docs) |
| `askubuntu` | No | 300 req/day (no key), 10K/day (key) | Yes | Yes (CC BY-SA) | [API docs](https://api.stackexchange.com/docs) |
| `superuser` | No | 300 req/day (no key), 10K/day (key) | Yes | Yes (CC BY-SA) | [API docs](https://api.stackexchange.com/docs) |
| `openverse` | Recommended | Not published | Yes | May charge | [Terms](https://docs.openverse.org/terms_of_service.html) |
| `dailymotion` | No | Tier-dependent | Yes | Tier-dependent | [Rate limiting](https://developers.dailymotion.com/reference/rate-limiting) |
| `vimeo` | No | ~100 req/15min | Yes | Plan-dependent | [Rate limits](https://help.vimeo.com/hc/en-us/articles/12427783954065-Rate-limits) |

### Free Engines (Require Free API Key)

| Engine | Rate Limit | Free | Commercial | Verify At |
|--------|------------|------|------------|-----------|
| `pixabay images` | 100 req/min | Yes | Yes (royalty-free) | [API docs](https://pixabay.com/api/docs/) |
| `pixabay videos` | 100 req/min | Yes | Yes (royalty-free) | [API docs](https://pixabay.com/api/docs/) |
| `flickr_api` | Not published | Yes (non-commercial key) | Staff approval needed | [API Terms](https://www.flickr.com/help/terms/api) |
| `youtube_api` | 10,000 units/day | Yes | Yes (audit required) | [API Terms](https://developers.google.com/youtube/terms/api-services-terms-of-service) |
| `wolframalpha_api` | 2,000 calls/month | Yes | Paid only | [API pricing](https://products.wolframalpha.com/api/pricing) |

### Paid Engine (General Web Search)

| Engine | Cost | Rate Limit | Free | Commercial | Verify At |
|--------|------|------------|------|------------|-----------|
| `braveapi` | $5/1K queries (Base) | 20 req/s | No (free tier ended Feb 2026) | Yes | [API pricing](https://api-dashboard.search.brave.com/documentation/pricing) |

## Excluded Engines (ToS Violations)

The following engines are **disabled** because SearXNG scrapes them in violation of their Terms of Service:

- **Google** (search, images, news, videos, scholar) — actively litigating against scrapers; Custom Search API being deprecated Jan 2027
- **Bing** (search, images, news, videos) — API retired Aug 2025
- **DuckDuckGo** (search, images, news, videos) — ToS prohibits automated use
- **Yahoo** (search, news) — explicitly prohibits robots/scrapers
- **Qwant** (search, images, videos, news) — prohibits collection/reproduction of results
- **Startpage** (search, images, news) — no API, proxies Google
- **Yandex** (search, images, music) — prohibited without paid API
- **Reddit** — scraping prohibited, paid API required for commercial
- **Pinterest** — strictly prohibited
- **Bandcamp** — explicitly prohibits scraping
- **SoundCloud** — prohibited, restricted API signups
- **Mojeek** (search, images, news) — prohibited without API agreement
- **Baidu** (search, images, kaifa) — Chinese jurisdiction, unclear enforcement

## Implementation Steps

### 1. Get API Keys

| Service | Where to Get Key | Cost |
|---------|-----------------|------|
| Brave Search | https://api-dashboard.search.brave.com/ | $5/1K queries |
| Pixabay | https://pixabay.com/api/docs/ | Free |
| YouTube Data API v3 | https://console.cloud.google.com/ | Free (10K units/day) |
| Wolfram Alpha | https://products.wolframalpha.com/api | Free (2K/month, non-commercial) |
| Flickr | https://www.flickr.com/services/api/ | Free (non-commercial) |

Optional (improves rate limits):
| Service | Where to Get Key | Cost |
|---------|-----------------|------|
| PubMed (NCBI) | https://www.ncbi.nlm.nih.gov/account/ | Free (raises limit to 10 req/s) |
| Stack Exchange | https://stackapps.com/apps/oauth/register | Free (raises limit to 10K req/day) |
| GitHub | https://github.com/settings/tokens | Free (raises limit to 5K req/hr) |

### 2. Configure Settings

For Docker: place this in `./core-config/settings.yml` (mounted into the container).
For bare-metal: override or edit `searx/settings.yml`.

```yaml
use_default_settings:
  engines:
    keep_only:
      # -- General Web Search (paid) --
      - braveapi

      # -- Wikimedia (free, no key) --
      - wikipedia
      - wikidata
      - wikicommons.images
      - wikibooks
      - wikiquote
      - wikisource
      - wikiversity
      - wikivoyage
      - wikinews
      - wiktionary

      # -- Academic / Science (free, no key) --
      - arxiv
      - pubmed
      - library of congress

      # -- Code / IT (free, no key) --
      - github
      - github code
      - gitlab
      - stackoverflow
      - askubuntu
      - superuser

      # -- Images (free, key required) --
      - pixabay images
      - openverse
      - flickr_api

      # -- Videos (mixed) --
      - pixabay videos
      - youtube_api
      - peertube
      - dailymotion
      - vimeo

      # -- Reference (free, key required) --
      - wolframalpha_api

server:
  secret_key: "change-this-to-a-random-string"

engines:
  - name: braveapi
    api_key: "YOUR_BRAVE_API_KEY"

  - name: pixabay images
    api_key: "YOUR_PIXABAY_KEY"

  - name: pixabay videos
    api_key: "YOUR_PIXABAY_KEY"

  - name: youtube_api
    api_key: "YOUR_YOUTUBE_API_KEY"

  - name: wolframalpha_api
    api_key: "YOUR_WOLFRAMALPHA_APP_ID"

  - name: flickr_api
    api_key: "YOUR_FLICKR_API_KEY"
```

### 3. Verify Engine Names

Before deploying, confirm engine names still exist in the codebase:

```bash
python3 -c "
import yaml
with open('searx/settings.yml') as f:
    s = yaml.safe_load(f)
engines = {e['name'] for e in s.get('engines', [])}
needed = [
    'wikipedia', 'wikidata', 'wikicommons.images', 'wikibooks', 'wikiquote',
    'wikisource', 'wikiversity', 'wikivoyage', 'wikinews', 'wiktionary',
    'arxiv', 'pubmed', 'library of congress', 'peertube',
    'github', 'github code', 'gitlab', 'stackoverflow', 'askubuntu', 'superuser',
    'pixabay images', 'pixabay videos', 'openverse', 'flickr_api',
    'youtube_api', 'wolframalpha_api', 'braveapi', 'dailymotion', 'vimeo'
]
for n in needed:
    status = 'FOUND' if n in engines else 'MISSING'
    print(f'{status}: {n}')
"
```

### 4. Restart SearXNG

```bash
cd container && docker compose down && docker compose up -d
```

## Cost Estimate

| Usage Level | Brave Cost | Other | Total |
|-------------|-----------|-------|-------|
| Light (~50 searches/day) | ~$7.50/month | $0 | ~$7.50/month |
| Medium (~100 searches/day) | ~$15/month | $0 | ~$15/month |
| Heavy (~500 searches/day) | ~$75/month | $0 | ~$75/month |

All other engines are free. Brave is the only paid component.

## Notes

- This document reflects ToS and API policies as of April 2026
- Policies change — re-verify the "Verify At" links periodically
- `wolframalpha_api` free tier is **non-commercial only** (2K calls/month)
- `flickr_api` non-commercial key is free; commercial requires staff approval
- `youtube_api` quota is unit-based (different operations cost different units), not simple request count
- Engines using `use_default_settings` with `keep_only` will disable all engines not in the list
