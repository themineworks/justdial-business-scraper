# JustDial Business Scraper (Python)

Scrape business listings from JustDial — India's largest local business directory — by city and category. Resolved phone numbers, addresses, ratings and geo-coordinates. No login, no cookies.

A tiny, real Python client for the **[themineworks/justdial-business](https://apify.com/themineworks/justdial-business)** actor on Apify — run it, get structured data, export CSV. No scraping infrastructure to maintain, no proxies to buy, no login.

[![Apify Actor](https://img.shields.io/badge/Apify-justdial-business-scraper-97d700)](https://apify.com/themineworks/justdial-business)

## Quickstart

```bash
pip install -r requirements.txt
export APIFY_TOKEN=apify_api_xxx        # free token: https://console.apify.com/account/integrations
python justdial_business.py --query "Restaurants" --max 25 --out results.csv
```

That runs the hosted actor and writes a clean CSV. New Apify accounts include free platform credits, so you can try it at no cost.

## Output fields

| field |
|---|
| `name` |
| `phone` |
| `address` |
| `area` |
| `city` |
| `category` |
| `rating` |
| `rating_count` |
| `latitude` |
| `longitude` |
| `pincode` |
| `verified` |
| `url` |

## Why the hosted actor?

The scraping itself — anti-bot handling, proxy rotation, phone/field resolution — runs on Apify, so this client stays a few lines. You only pay for delivered results; empty or failed runs are never billed.

## Links

- **Actor:** https://apify.com/themineworks/justdial-business
- **All themineworks scrapers:** https://apify.com/themineworks
- **Apify Python client docs:** https://docs.apify.com/api/client/python/

## License

MIT © The Mine Works
