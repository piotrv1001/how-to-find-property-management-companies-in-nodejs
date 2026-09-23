# How to Find Property Management Companies in Node.js

This example calls the [All Property Management Scraper](https://apify.com/piotrv1001/all-property-management-scraper) on Apify. It does not implement a scraper from scratch.

## What this example does

- Searches for five company records associated with Austin, Texas
- Waits for the Actor run to finish
- Fetches its default dataset and prints each company
- Includes public business emails, location, and property specialties where the directory supplies them

## Prerequisites

- Node.js 18 or newer
- An Apify account and API token

## Installation

```bash
npm install
```

## Environment setup

Copy `.env.example` to `.env`, then replace the sample value with your Apify API token. Do not commit `.env`.

## Usage

```bash
npm start
```

## Code example

```js
import { ApifyClient } from 'apify-client';
import 'dotenv/config';

// Initialize the ApifyClient with your Apify API token
// Set APIFY_TOKEN in your .env file (copy .env.example to get started)
const client = new ApifyClient({
    token: process.env.APIFY_TOKEN,
});

// Prepare Actor input
const input = {
    searchTerms: ['Austin, TX'],
    maxItems: 5,
    proxyConfiguration: { useApifyProxy: false },
};

// Run the Actor and wait for it to finish
const run = await client.actor('piotrv1001/all-property-management-scraper').call(input);

// Fetch and print Actor results from the run's dataset (if any)
console.log('Results from dataset');
console.log(`💾 Check your data here: https://console.apify.com/storage/datasets/${run.defaultDatasetId}`);
const { items } = await client.dataset(run.defaultDatasetId).listItems();
items.forEach((item) => {
    console.dir(item);
});

// 📚 Want to learn more 📖? Go to → https://docs.apify.com/api/client/js/docs
```

## Example output

[`sample-output.json`](./sample-output.json) contains illustrative records with `example.com` addresses so no person's email is published in this example. The live five-company run returned `name`, `emails`, `city`, `state`, `propertyTypes`, and source `url` fields. An Austin search can include a company based elsewhere, so filter returned addresses if office location matters. Directory-published emails are not deliverability-verified inboxes.

## Use cases

- Build a targeted property-management company list by market
- Segment firms by HOA, multifamily, or single-family specialties
- Enrich a CRM with public directory contact and address fields
- Review company coverage across several cities or states

## Try the Actor on Apify

**[Open the All Property Management Scraper on Apify](https://apify.com/piotrv1001/all-property-management-scraper)**

## Related resources

- [How to find property management companies and business emails](https://www.falconscrape.com/blog/how-to-find-property-management-companies-and-business-emails)

## License

MIT
