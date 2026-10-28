# Awesome Ecommerce Data APIs [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

A curated list of APIs and data sources for product catalogues, pricing,
availability, and reviews across marketplaces, retailers, and ecommerce
platforms.

Includes official APIs, third-party providers, and scraping platforms. Access
restrictions are stated plainly, because "Amazon has an API" is technically true
and practically misleading.

---

## Read this before you pick anything

There are two completely different things people mean by "ecommerce API", and
choosing the wrong category wastes weeks.

**Selling APIs** let you manage *your own* store: create products, process
orders, sync inventory. Shopify, WooCommerce, and BigCommerce all have excellent
ones, and they are free with the platform.

**Data APIs** let you read *someone else's* catalogue: competitor prices, product
specifications, availability, reviews. This is far harder to get, and it is what
most of this list covers.

### The Amazon situation, since it comes up first every time

Amazon has never offered a general-purpose product data API. What existed was the
Product Advertising API, built for affiliates, and it is now gone.

| Date | What happened |
|---|---|
| 31 January 2026 | Offers V1 removed, which killed live pricing and Prime status first |
| 30 April 2026 | PA-API v5 deprecated |
| 15 May 2026 | PA-API v5 endpoint retired |

The successor is the [Creators API](https://affiliate-program.amazon.com/creatorsapi/docs/en-us/paapiv5-deprecation),
which is not a drop-in replacement: different authentication, request shape, and
token lifecycle. It also still requires an active Amazon Associates account with
recent qualifying sales, so it is unavailable to anyone who is not running an
affiliate business.

If you need Amazon product data and are not an affiliate, you need a third-party
provider. That is not a workaround, it is the only route.

---

## Contents

- [How to choose](#how-to-choose)
- [Marketplaces](#marketplaces)
- [Ecommerce platforms](#ecommerce-platforms)
- [Retailer data](#retailer-data)
- [Multi-platform aggregators](#multi-platform-aggregators)
- [Price tracking and monitoring](#price-tracking-and-monitoring)
- [Product identifiers and catalogues](#product-identifiers-and-catalogues)
- [Reviews and sentiment](#reviews-and-sentiment)
- [Web scraping platforms](#web-scraping-platforms)
- [Free and open data](#free-and-open-data)
- [Datasets](#datasets)
- [Libraries and tools](#libraries-and-tools)
- [Legal and ethical notes](#legal-and-ethical-notes)
- [Contributing](#contributing)

---

## How to choose

**Are you reading your own store or someone else's?** Your own: use the
platform's official API, it is free and complete. Someone else's: keep reading.

**One retailer or many?** Single-retailer projects are better served by a
retailer-specific API, which gives you deeper fields. Broad competitive
monitoring favours an aggregator or scraping platform, at lower fidelity per
site.

**Do you need history?** Current prices are widely available. Price *history* is
a different and more expensive product, and almost nobody backfills it for you.
If history matters, start collecting now, even before you have a use for it.

**How fresh?** Marketing and analytics use cases tolerate daily. Repricing and
arbitrage need minutes, and that changes the cost by an order of magnitude.

**Do you need to be inside the store's terms?** If yes, your options narrow to
official partner programmes and affiliate APIs. Most competitive monitoring
happens outside them, which is a business risk decision rather than a technical
one.

---

## Marketplaces

- [Amazon Creators API](https://affiliate-program.amazon.com/creatorsapi/docs/en-us/paapiv5-deprecation) - Official successor to PA-API. Requires an active Associates account with recent qualifying sales. Affiliate use cases only.
- [Amazon Selling Partner API](https://developer-docs.amazon.com/sp-api/) - For sellers managing their own listings, inventory, and orders. Not a catalogue browsing API.
- [eBay Developers Program](https://developer.ebay.com/) - Genuinely open and self-serve. Browse API covers active listings; Marketplace Insights covers sold prices. One of the better official marketplace APIs.
- [Etsy Open API](https://developers.etsy.com/) - Self-serve with an application step. Good for handmade and vintage categories.
- [Walmart Developer Portal](https://developer.walmart.com/) - Affiliate and marketplace-seller APIs. Catalogue access is limited compared to eBay.
- [Best Buy Developer API](https://developer.bestbuy.com/) - Free products, stores, and categories API. Unusually generous, and often overlooked.
- [Rakuten](https://webservice.rakuten.co.jp/) - Japanese marketplace, free API with registration.
- [AliExpress Open Platform](https://openservice.aliexpress.com/) - Affiliate and dropshipping APIs.

---

## Ecommerce platforms

Free with the platform, for reading and writing your own store.

- [Shopify Admin API](https://shopify.dev/docs/api/admin) - REST and GraphQL. The reference implementation for this category.
- [Shopify Storefront API](https://shopify.dev/docs/api/storefront) - Public-facing catalogue and cart, for headless builds.
- [WooCommerce REST API](https://woocommerce.github.io/woocommerce-rest-api-docs/) - WordPress ecommerce. Free and self-hosted.
- [BigCommerce API](https://developer.bigcommerce.com/) - Catalogue, orders, customers.
- [Magento / Adobe Commerce](https://developer.adobe.com/commerce/webapi/rest/) - REST and GraphQL.
- [Wix Stores API](https://dev.wix.com/docs/rest/business-solutions/stores/catalog/introduction) - Catalogue and orders.
- [Squarespace Commerce APIs](https://developers.squarespace.com/commerce-apis) - Limited but functional.
- [Medusa](https://docs.medusajs.com/) - Open source headless commerce, self-hosted, no vendor gatekeeping.
- [Saleor](https://docs.saleor.io/) - Open source GraphQL-first commerce platform.

---

## Retailer data

Reading specific retailers' catalogues. Almost none of these publish official
APIs, which is why third-party coverage exists.

### Grocery

- [Tesco API (Happy Endpoint)](https://happyendpoint.com/library/tesco-data) - UK grocery products, pricing, and availability.
- [Open Food Facts](https://world.openfoodfacts.org/data) - Free, open, crowd-sourced food product database with ingredients, nutrition, and barcodes. Genuinely excellent and completely free. Start here before paying for grocery data.

### Home and furniture

- [IKEA API (Happy Endpoint)](https://happyendpoint.com/library/ikea-pro) - Products, categories, and stores across eight countries. Cross-country price comparison is the underrated use case, since the same product is priced differently per market.

### Beauty

- [Sephora API (Happy Endpoint)](https://happyendpoint.com/library/sephora-api) - Products, pricing, reviews, store locations, and per-store availability across the US, Canada, and France.

### Fashion and general retail

- [H&M API (Happy Endpoint)](https://happyendpoint.com/library/hm-api) - Fashion catalogue and pricing.
- [Kohl's API (Happy Endpoint)](https://happyendpoint.com/library/kohls-data) - US department store catalogue.
- [Klarna API (Happy Endpoint)](https://happyendpoint.com/library/klarna-ecom) - Product and merchant data across Klarna's shopping network.

### Provider-agnostic note

Several scraping platforms in this list also ship pre-built extractors for major
retailers. If you need one retailer deeply, a retailer-specific API usually gives
you more fields. If you need twenty retailers shallowly, a scraping platform is
usually cheaper.

---

## Multi-platform aggregators

One integration, many stores. Useful when your customers each run a different
platform.

- [API2Cart](https://api2cart.com/) - Unified API across 70+ platforms and marketplaces including Shopify, Magento, WooCommerce, BigCommerce, Etsy, Shopee, and TikTok Shop. Built for software vendors serving many merchants.
- [Codisto](https://www.codisto.com/) - Multichannel listing and inventory sync.
- [Rutter](https://www.rutter.com/) - Unified commerce API covering ecommerce, accounting, and payments.
- [FastAF](https://fastaf.co/?utm_source=awesome-ecommerce-data-apis&utm_medium=listing&utm_campaign=seo-backlinks) - Scraping, Google Shopping, eBay and Walmart public product data plus web search as JSON for AI agents; [JSON Schema extract API](https://fastaf.co/apis/extract-api/) for any product page. API key or x402 pay-per-call (USDC on Base); only 200 responses are charged. 500 free credits every month after email verification (not on x402). Unofficial; not affiliated with the marketplaces. [Docs](https://fastaf.co/docs/)

---

## Price tracking and monitoring

Competitive pricing and history. Almost all of this is third-party.

- [Keepa](https://keepa.com/#!api) - Amazon price history, going back years. The deepest historical Amazon dataset available, and the standard answer for Amazon price history.
- [Rainforest API](https://www.rainforestapi.com/) - Amazon product, review, and search data. No affiliate account required.
- [Canopy API](https://www.canopyapi.co/) - Amazon product data, pricing, and reviews via GraphQL.
- [Zinc API](https://zincapi.com/) - Amazon and Walmart pricing, plus programmatic ordering.
- [Netrows](https://www.netrows.com/) - Amazon product data without affiliate requirements.
- [Prisync](https://prisync.com/) - Competitor price tracking aimed at retailers rather than developers.
- [Price2Spy](https://www.price2spy.com/) - Price monitoring and repricing.

---

## Product identifiers and catalogues

The unglamorous layer that makes everything else joinable.

- [GS1](https://www.gs1.org/services/verified-by-gs1) - The authoritative source for GTIN and barcode allocation. Verified by GS1 confirms who actually owns a barcode.
- [UPCitemdb](https://www.upcitemdb.com/api/explorer) - UPC and EAN lookup with a free tier.
- [Barcode Lookup](https://www.barcodelookup.com/api) - Product lookup by barcode.
- [Open Food Facts](https://world.openfoodfacts.org/data) - Free and open, food and increasingly beauty products, with a full bulk dump available.
- [Open Beauty Facts](https://world.openbeautyfacts.org/) - Same project, cosmetics.
- [Datakick](https://www.datakick.org/) - Open product database.

Barcodes are the join key that makes cross-retailer comparison possible. If you
are building anything comparative, resolve to GTIN early rather than matching on
product names, which will defeat you.

---

## Reviews and sentiment

- [Trustpilot Business API](https://developers.trustpilot.com/) - Reviews for businesses you own or have permission to access.
- [Judge.me](https://judge.me/) and [Yotpo](https://apidocs.yotpo.com/) - Review platforms with APIs for merchants using them.
- [Rainforest API](https://www.rainforestapi.com/) and [Canopy API](https://www.canopyapi.co/) - Amazon review data.
- [Sephora API (Happy Endpoint)](https://happyendpoint.com/library/sephora-api) - Product reviews alongside catalogue data, useful for beauty sentiment work.

---

## Web scraping platforms

The general-purpose fallback. Pricing reflects publicly listed rates as of
August 2026 and moves often.

- [Bright Data](https://brightdata.com/) - Largest proxy network, hundreds of pre-built retailer scrapers. Residential proxies around $10.50/GB. Strongest option for heavily protected targets at scale.
- [Apify](https://apify.com/store) - Marketplace of ready-made scrapers covering most major retailers. Pricing varies per actor: compute unit, per result, or subscription.
- [Oxylabs](https://oxylabs.io/products/scraper-api/ecommerce) - Dedicated ecommerce scraper API. Residential proxies from around $8/GB.
- [ScraperAPI](https://www.scraperapi.com/) - Simple proxy and rendering, from around $49/month for 100k credits. Best value at low volume on a single target.
- [Zyte](https://www.zyte.com/) - Pay-as-you-go with difficulty tiers.
- [Crawlee](https://crawlee.dev/) - Free open source scraping library, if you want to run your own infrastructure.

---

## Free and open data

Genuinely free, no trial period.

- [Open Food Facts](https://world.openfoodfacts.org/data) - Millions of food products, full database downloadable.
- [Open Beauty Facts](https://world.openbeautyfacts.org/) - Cosmetics equivalent.
- [Best Buy Developer API](https://developer.bestbuy.com/) - Free tier covering products, categories, and stores.
- [eBay Browse API](https://developer.ebay.com/api-docs/buy/browse/overview.html) - Free tier, real marketplace listings.
- [Datakick](https://www.datakick.org/) - Open product database.
- [Happy Endpoint free datasets](https://happyendpoint.com/free-datasets) - Free samples sharing the schema of the paid snapshots.

---

## Datasets

Bulk files for analysis and model training.

- [Open Food Facts data dumps](https://world.openfoodfacts.org/data) - Free, complete, MongoDB and CSV exports.
- [Amazon Reviews dataset (UCSD)](https://cseweb.ucsd.edu/~jmcauley/datasets/amazon_v2/) - Large academic review corpus, widely used in recommender research.
- [Kaggle ecommerce datasets](https://www.kaggle.com/datasets?search=ecommerce) - Mixed quality but useful for prototyping.
- [Hugging Face product datasets](https://huggingface.co/datasets?search=product) - Increasingly where ML-ready commerce data lives.
- [Happy Endpoint datasets](https://happyendpoint.com/datasets) - Retailer catalogue snapshots including IKEA US and Sephora US.

---

## Libraries and tools

- [happyendpoint-python](https://github.com/happyendpointhq/happyendpoint-python) - Python client covering the retail APIs in this list.
- [happyendpoint-js](https://github.com/happyendpointhq/happyendpoint-js) - TypeScript equivalent.
- [happyendpoint-mcp](https://github.com/happyendpointhq/happyendpoint-mcp) - MCP server, so Claude and Cursor can query product data directly.
- [Crawlee](https://crawlee.dev/) - Scraping framework for Node and Python.
- [python-amazon-paapi](https://github.com/sergioteula/python-amazon-paapi) - Amazon PA-API client. Note the API it wraps was retired in May 2026; check for Creators API support before adopting.
- [Shopify API libraries](https://shopify.dev/docs/api/admin-rest#client_libraries) - Official clients across several languages.

---

## Legal and ethical notes

Not legal advice. Included because most lists on this subject skip it entirely.

**Terms of service.** Most retailers prohibit automated collection. Using a
third-party API does not transfer that risk to you or away from you; it changes
who collects, not whether the retailer permits it. Understand your own exposure.

**Copyright.** Product photography and marketing copy are typically the
retailer's or brand's copyright. Facts such as price, size, and barcode generally
are not. Comparing prices is a different risk profile to republishing product
descriptions and images.

**Personal data.** Review text often contains reviewer names and identifiers.
Under GDPR and similar regimes that is personal data, whatever the source.

**Competition law.** In some jurisdictions, automated price matching between
competitors can raise antitrust questions. Monitoring competitors is normal;
coordinating with them is not, and algorithmic systems can blur that line.

**Rate limits.** Even where collection is permitted, hammering an endpoint is
not. Respect published limits.

---

## Contributing

Additions welcome, including competitors to anything listed. This list is only
useful if it is honest about what each option actually provides.

Please:

- State access restrictions plainly, including affiliate or partner requirements
- Mark free and open sources as free
- Skip marketing language
- Prefer documentation links over pricing pages
- Note if an API is deprecated or retired, with the date

Open an issue or a pull request.

---

## Related lists

- [awesome-real-estate-apis](https://github.com/happyendpointhq/awesome-real-estate-apis) - property listings, transactions, and valuation data by country
- [awesome-alternative-data](https://github.com/happyendpointhq/awesome-alternative-data) - the investment research angle, where retail pricing is a revenue signal

---

## Disclaimer

This is an independently maintained list. Inclusion does not imply any
affiliation with, endorsement by, or connection to the organisations listed,
and no organisation listed has reviewed or approved this list.

All company names, product names, brands, trademarks, and registered trademarks
are the property of their respective owners, and are used here descriptively to
identify the services being catalogued.

Access terms, pricing, and availability change without notice. Verify current
details with the provider before relying on anything here.

---

## Maintained by

Maintained by [Happy Endpoint](https://happyendpoint.com), which builds real-time
data APIs for retailers and marketplaces. Our APIs appear here alongside
competitors, free alternatives, and open datasets, several of which are better
choices for particular use cases. Open Food Facts in particular is free and
excellent, and you should try it before paying anyone for grocery data.

- Catalogue: [happyendpoint.com/library](https://happyendpoint.com/library)
- Datasets: [happyendpoint.com/datasets](https://happyendpoint.com/datasets)
- Contact: happyendpointhq@gmail.com

## Licence

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, the contributors have waived all copyright and
related rights to this work.
