# RSS & Atom Feed Reader — Only New Items — Python, Node.js & cURL examples

Read **RSS, Atom and podcast feeds** and get clean **JSON**. Turn on **only new entries** and the Actor **remembers what it already gave you**, so every scheduled run returns just what is new: a simple way to feed Slack, Zapier, n8n or your own database. **$0.50 per 1,000 entries**; nothing new means nothing to pay.

Hosted on Apify: **[RSS & Atom Feed Reader — Only New Items](https://apify.com/tidydata/rss-new-items-monitor?fpr=wtg6qt)**. These examples show how to call it from your code; the Actor runs in the cloud, no API key for the source site, no proxies to manage.

## Python

```bash
pip install apify-client
export APIFY_TOKEN=...   # free account at apify.com → Settings → API & Integrations
```

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("tidydata/rss-new-items-monitor").call(run_input={
    "feeds": [
        {
            "url": "https://hnrss.org/frontpage"
        },
        {
            "url": "https://feeds.bbci.co.uk/news/world/rss.xml"
        }
    ],
    "onlyNew": True,
    "memoryName": "my-news",
    "maxEntriesPerFeed": 50
})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print({k: item.get(k) for k in ['feedTitle', 'title', 'link', 'published', 'isNew']})
```

## Node.js

```javascript
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor('tidydata/rss-new-items-monitor').call({"feeds": [{"url": "https://hnrss.org/frontpage"}], "includeContent": true});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items.length, items[0]);
```

## cURL (one call, results as JSON)

```bash
curl -s -X POST "https://api.apify.com/v2/acts/tidydata~rss-new-items-monitor/run-sync-get-dataset-items?token=$APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"feeds": [{"url": "https://hnrss.org/frontpage"}], "includeContent": true}'
```

## More TidyData Actors

[YouTube Transcript](https://apify.com/tidydata/youtube-transcript-scraper?fpr=wtg6qt) · [YouTube Comments](https://apify.com/tidydata/youtube-comments-scraper?fpr=wtg6qt) · [YouTube Scraper](https://apify.com/tidydata/youtube-channel-scraper?fpr=wtg6qt) · [Website Contacts](https://apify.com/tidydata/website-contact-extractor?fpr=wtg6qt) · [Google News](https://apify.com/tidydata/google-news-scraper?fpr=wtg6qt) · [App Reviews](https://apify.com/tidydata/app-reviews-scraper?fpr=wtg6qt) · [Merge & Dedupe](https://apify.com/tidydata/merge-dedupe-datasets?fpr=wtg6qt) · [all of them](https://github.com/tidydata-dev)

Examples are MIT-licensed.

---
<sub>Links to apify.com include our affiliate ID: if you start a paid Apify plan through them, Apify pays TidyData a commission at no extra cost to you.</sub>
