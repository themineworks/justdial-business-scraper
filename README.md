# JustDial Scraper: India Business Leads, Phone & Reviews

Scrape business listings from JustDial, India's largest local business directory. Name, phone, address, area, city, category, rating, reviews, and geo-coordinates. Search by city and category. Pay only per listing returned.

**Run it on Apify:** [apify.com/themineworks/justdial-business](https://apify.com/themineworks/justdial-business)
**Docs, FAQ and pricing:** [themineworks.com/actors/justdial-business](https://themineworks.com/actors/justdial-business/)

**Price:** $3.00 per 1,000 listings on Apify's free plan, down to $2.00 on higher plans, plus a $0.005 start fee per run. Failed and empty results are never charged.

## What it returns

* Business name, phone, address, and geo-coordinates
* Rating, review count, and category data
* Search by city and business category
* India local lead generation at scale
* Zero charge on empty searches

## Quick start

You need a free [Apify account](https://console.apify.com/sign-up) and its API token (Settings, API & Integrations).

### Python

```bash
pip install apify-client
```

```python
from apify_client import ApifyClient

client = ApifyClient("YOUR_APIFY_TOKEN")
run = client.actor("themineworks/justdial-business").call(run_input={
    "searchQuery": "Restaurants",
    "city": "Mumbai",
    "maxResults": 25
})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

### Node.js

```bash
npm install apify-client
```

```javascript
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: 'YOUR_APIFY_TOKEN' });
const run = await client.actor('themineworks/justdial-business').call({
    "searchQuery": "Restaurants",
    "city": "Mumbai",
    "maxResults": 25
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

### cURL

One request that runs the actor and returns the results in the response (for runs under 5 minutes):

```bash
curl -X POST "https://api.apify.com/v2/acts/themineworks~justdial-business/run-sync-get-dataset-items?token=YOUR_APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"searchQuery": "Restaurants", "city": "Mumbai", "maxResults": 25}'
```

### Command line

This repo includes ready-made clients that save results to JSON and CSV:

```bash
python3 justdial_business_scraper.py --token YOUR_APIFY_TOKEN --search-query "Restaurants" --city "Mumbai" --max-results "25"
node justdial_business_scraper.mjs --token YOUR_APIFY_TOKEN --search-query "Restaurants" --city "Mumbai" --max-results "25"
```

## Input

| Field | Type | Default | Description |
|---|---|---|---|
| `searchQuery` | string |  | What to search for on JustDial (for example Restaurants, Gyms, Dentists, Hotels, Interior Designers) |
| `city` | string |  | Indian city to search in (for example Mumbai, Delhi, Bangalore, Hyderabad, Pune, Chennai) |
| `maxResults` | integer | `100` | Maximum number of businesses to return |

## Output

One row per result, as JSON, CSV, Excel or through the API.

| Field | Type | Description |
|---|---|---|
| `name` | string | Business name |
| `phone` | string | Primary phone number |
| `address` | string | Full address string |
| `area` | string | Locality / area within the city |
| `city` | string | City |
| `category` | string | Business category / type |
| `rating` | number | JustDial star rating |
| `rating_count` | number | Total number of ratings / reviews |
| `latitude` | number | Latitude coordinate |
| `longitude` | number | Longitude coordinate |
| `pincode` | string | PIN code |
| `verified` | boolean | Whether the listing is JustDial-verified |
| `url` | string | JustDial listing URL |
| `docid` | string | JustDial internal document ID |
| `scraped_at` | string | ISO-8601 timestamp when this record was scraped |

## Use it from an AI agent

The actor works as a tool in Claude, Cursor or any MCP client through Apify's MCP server:

```
https://mcp.apify.com/?tools=themineworks/justdial-business
```

## FAQ

### What comes back per business?

Name, phone number, full address, area, city, category, rating, review count and geo coordinates.

### How do I search?

By city and category, which is the same pairing JustDial itself browses on. One run can cover several pairs.

### Do I need a JustDial account?

No. The actor reads public listing pages, so there is no login, no cookie and no API key.

### Are phone numbers returned in plain text?

Yes. JustDial renders them behind an obfuscation layer and the actor resolves that, so the number arrives usable rather than as an image or a token.

### How am I charged?

Per listing returned. A city and category pair that matches nothing is never charged.

### Can I pull several cities in one run?

Yes. Pass multiple city and category pairs and the run works through them in sequence, deduplicating businesses that appear under more than one pair.

### What is it typically used for?

Local lead lists and market mapping: every clinic, salon or dealer in a chosen area, with the phone number and rating attached so the list can be prioritised before anyone calls.

### How much does the JustDial Scraper cost?

$3.00 per 1,000 listings on Apify's free plan, down to $2.00 on higher plans, plus a $0.005 start fee per run. Failed and empty results are never charged. You can cap what a single run may spend with the maximum cost setting on Apify.

### Can I export the results to CSV or Excel?

Yes. Every run saves to an Apify dataset you can download as JSON, CSV, Excel or XML, or read through the API. The Python and Node clients in this repo also write the results to local files.

### Can I run it on a schedule?

Yes. Save your input as a task on Apify and attach a schedule, or call the API from your own cron job. Scheduled runs are billed the same way as manual ones.

## Related scrapers

* [B2B Leads Finder](https://themineworks.com/actors/b2b-leads-finder/): Business emails and LinkedIn profiles for target companies
* [LinkedIn Company Scraper](https://themineworks.com/actors/linkedin-company-details/): Company size, industry, website, and followers without login
* [Zillow Rental Listings Scraper](https://themineworks.com/actors/zillow-rental-listings/): Scrape Zillow for-rent listings by city or zip. $1 per 1,000 results

Part of [The Mine Works](https://themineworks.com/): 151 pay-per-result scrapers with no login and no browser setup on your side.

## License

MIT © The Mine Works
