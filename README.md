# amazon-product-url-cleaner

Strip tracking parameters from Amazon product URLs, extract the ASIN, and generate a clean canonical URL. Optionally append your own affiliate tag. Browser only.

**Live demo:** https://0xelitesystem.github.io/amazon-product-url-cleaner/

## Use

Open [`index.html`](./index.html). Paste any Amazon product URL. Click Clean URL.

Output:

- Domain
- ASIN (Amazon Standard Identification Number)
- Title slug (if present)
- Clean canonical URL: `https://www.amazon.com/dp/ASIN` (or with title slug, if you want it)
- Optional: same URL with your affiliate tag appended
- Full list of tracking parameters that were stripped, with descriptions

## Why

A typical Amazon product URL looks like:

```
https://www.amazon.com/Sony-WH-1000XM5-Industry-Leading-Comfortable-Hands-Free/dp/B0BXYCS74H/ref=sr_1_2?crid=1KQTHJ6MR9V8L&dib=...&keywords=...&qid=...&sprefix=...&sr=8-2&tag=othersite-20
```

Most of that is tracking. The clean version is:

```
https://www.amazon.com/dp/B0BXYCS74H
```

Reasons to clean it:

- Sharing honest links without leaking your search history (`keywords`, `qid`, `sprefix` reveal what you searched and when)
- Sharing a link without inadvertently passing along someone else's affiliate tag (`tag=...`)
- Extracting ASINs for legitimate inventory work
- Understanding what tracking lives in those long URLs

## What it strips

Common Amazon tracking parameters:

| Parameter | What it is |
|---|---|
| `ref`, `ref_` | Referral path |
| `tag` | Affiliate tag |
| `linkCode`, `linkId`, `ascsubtag` | Affiliate link IDs |
| `qid`, `sr`, `keywords`, `sprefix`, `crid` | Search context |
| `pd_rd_*`, `pf_rd_*` | Page detail and personalization tracking |
| `dib`, `dib_tag` | Search context blob |
| `th`, `psc`, `_encoding` | Variant flags |
| `spIA`, `smid`, `content-id` | Sponsored / seller / promo IDs |

Unknown parameters are also stripped (they're shown in the output so you can see what was there).

## Important: about replacing affiliate tags

This tool can append YOUR affiliate tag to a URL. It does NOT facilitate replacing someone else's tag with yours. Replacing affiliate tags on URLs you received from someone else (commission hijacking) violates the terms of every major affiliate program.

The intended use is:

- You discovered a product yourself (search, ad, recommendation)
- You want a clean canonical URL to share or to add YOUR tag to
- The original URL had tracking junk you don't want to pass along

## Privacy

All parsing happens in your browser. The tool makes zero requests to Amazon or anywhere else. The URL you paste, the affiliate tag you enter, and all generated URLs stay on your device.

## Run locally

```
git clone https://github.com/0xelitesystem/amazon-product-url-cleaner
cd amazon-product-url-cleaner
```

Open `index.html` in any browser. Or:

```
python -m http.server 8000
```

## Contribute

PRs welcome:

- Support for other Amazon TLDs and edge cases (e.g. `/exec/obidos/ASIN`)
- Bulk mode (paste many URLs, get clean URLs out)
- ASIN-to-URL mode (paste an ASIN, get the canonical URL)
- More tracking parameter descriptions

Don't add: requests to Amazon, telemetry, npm dependencies. Single file by design.

## Build

No build. Single HTML file.

## License

MIT.

## Related

- [affiliate-disclosure-templates](https://github.com/0xelitesystem/affiliate-disclosure-templates) - FTC-compliant disclosure language for affiliate links
- [product-review-honesty-guide](https://github.com/0xelitesystem/product-review-honesty-guide) - guidance for honest product reviews
- [video-description-templates](https://github.com/0xelitesystem/video-description-templates) - description templates that include affiliate disclosure
