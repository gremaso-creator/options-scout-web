# Options Scout Web

Mobile-friendly options research dashboard, hosted as a static website using GitHub Pages.

## Hosting
In **Settings → Pages**, choose **Deploy from a branch**, branch **main**, folder **/(root)**, and Save.

The site will use the URL `https://gremaso-creator.github.io/options-scout-web/` once GitHub Pages finishes publishing.

## How to use
1. Download the `options-scout-report` artifact from your **private** Options Scout repository's GitHub Actions run.
2. Extract `latest_report.json` on your device.
3. Visit this website, tap **Load report JSON**, and select the file.
4. Set your maximum option-contract premium, direction, and expiration, then choose **Find Options**.

All imported report processing happens **locally in your browser**. Reports remain private unless you deliberately share them. Do not upload private repository files to a public repository.

## Limitations
- **Not a live market-data dashboard.** The Find Options button filters contracts from an imported report, not a fresh market scan.
- The current scanner only searches options 10–35 days from expiration. Selecting 0DTE doesn't automatically generate same-day data.
- Quotes can be stale or incorrect. The risk score is heuristic, not a prediction or recommendation.
- No trading, authentication, market-data API keys, or connection to Robinhood.
- Demo-mode contract prices and symbols are fictional.


## Live search (requires private backend setup)

The **Find Options** button can now call a separately deployed Cloudflare Worker over HTTPS when you enter its URL and the personal scanner access key in the website form. The secure Worker code and deployment instructions are in the **private** `Options-scout` repository at `cloudflare/scout-worker.js` (no secrets in this public repository). A production Tradier data token and a Cloudflare Worker deployment are required. Until they are configured, the site remains report-import/demo mode. The public frontend must never contain your Tradier token. No trading API or brokerage order execution is integrated.


## Free historical options feed

The frontend now includes a ticker selector and supports the optional **MarketData.app Free Forever** Cloudflare Worker in the private `Options-scout/cloudflare/scout-marketdata-free.js` file. This feed is **at least 24 hours delayed** and limited to 100 daily API credits. Never treat its options prices as current Robinhood execution prices. **0DTE research results are disabled for this free feed.** The frontend can still import existing private scanner JSON reports manually.
