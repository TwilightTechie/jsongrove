# JSON Grove

A small, browser-only JSON viewer built with plain HTML, CSS, and JavaScript. JSON is parsed locally in the browser; the application does not upload the JSON you paste or open.

## Run locally

Open `index.html` in a browser, or serve this folder locally:

```sh
python3 -m http.server 8000
```

Then visit <http://localhost:8000>.

## Publish with GitHub and Cloudflare Pages

The site is static, so it needs no server or build framework.

1. Sign in to [Cloudflare](https://dash.cloudflare.com/) and open **Workers & Pages**.
2. Choose **Create application → Pages → Connect to Git**.
3. Connect GitHub, allow Cloudflare Pages to access the `jsongrove` repository, and select it.
4. Use these build settings:

   | Setting | Value |
   | --- | --- |
   | Production branch | `main` |
   | Framework preset | `None` |
   | Build command | `exit 0` |
   | Build output directory | `.` |

5. Select **Save and Deploy**. Cloudflare will publish the site at a `*.pages.dev` address. Future pushes to `main` deploy automatically.

### Connect `jsongrove.com`

1. In Cloudflare Pages, open the project and go to **Custom domains → Set up a domain**.
2. Enter `jsongrove.com` and follow Cloudflare's prompts.
3. For the root domain, Cloudflare requires the domain's nameservers to point to Cloudflare. If the domain was bought elsewhere, add it to Cloudflare and change the nameservers at that registrar to the nameservers Cloudflare assigns. If it was bought through Cloudflare Registrar, it already uses Cloudflare nameservers.
4. If the domain already has email or other DNS services, make sure their DNS records are present in Cloudflare before changing nameservers.
5. Wait for Cloudflare to activate the domain and issue HTTPS, then open `https://jsongrove.com` and confirm the page loads.

## Search visibility with Google Search Console

Do this after the custom domain works over HTTPS:

1. Open [Google Search Console](https://search.google.com/search-console/) and add a **Domain** property for `jsongrove.com`.
2. Google will show a DNS TXT verification value. In Cloudflare, open the domain's **DNS → Records**, add a TXT record with name `@` and the value Google supplied, then return to Search Console and verify.
3. In Search Console, open **Sitemaps**, submit `sitemap.xml`, and check that it is read successfully. The site already includes `robots.txt` and `sitemap.xml` at the root.
4. Use **URL Inspection** for `https://jsongrove.com/` and request indexing. Search Console can later show impressions, search queries, clicks, and indexing issues. Submitting a sitemap is a discovery hint, not a guarantee of indexing or ranking.

## Cloudflare Web Analytics

1. After the first Pages deployment, open **Workers & Pages → jsongrove → Metrics**.
2. Under **Web Analytics**, select **Enable**. Cloudflare says it will add the analytics snippet on the next deployment; push a small README or content update if a new deployment is needed.
3. Open **Web Analytics** in Cloudflare to view visitors, visits, pageviews, referring sites, countries, devices, and performance metrics.

Web Analytics is for aggregate site traffic. It does not tell you which viewer buttons a visitor clicked. If you want counts for actions such as `view_json`, `format_json`, and `copy_json`, create a Google Analytics 4 property and add custom events that send only the action name. Never send pasted JSON, filenames, field names, or field values to analytics. Update the privacy policy before enabling analytics or advertising tags.

## Monetize with Google AdSense

Google **AdSense** is the publisher product for showing ads on this site. Google **Ads** is primarily for buying advertising.

1. Before applying, make sure `jsongrove.com` is public, works reliably, has clear navigation, and contains useful original information about using the tool. Add a privacy policy that explains any analytics and advertising data collection and cookies. Approval is decided by Google and is not guaranteed; there is no fixed approval time.
2. Create an account at [Google AdSense](https://www.google.com/adsense/start/) and complete the payment and identity details requested for your account.
3. In AdSense, add `jsongrove.com` under **Sites**. Follow the site's ownership verification instructions; Google may provide an HTML snippet, a meta tag, or an `ads.txt` method.
4. Request a site review. Wait until the site's AdSense status is **Ready** before serving ads.
5. In AdSense, choose Auto ads or create a responsive display ad unit. Add the code Google provides to the labeled ad area in `index.html`. Keep the ad visually distinct and separated from the JSON input and action buttons.
6. If AdSense gives you an `ads.txt` entry, create `/ads.txt` at the site root with the exact line from your account. Do not copy a sample publisher ID.
7. Set up the consent messages AdSense requires for visitors in the EEA, UK, and Switzerland when applicable. Do not click your own ads or ask anyone else to click them.

Google may request more useful original content or changes to the site's privacy disclosures before approving ads. Review the latest requirements in [AdSense site readiness](https://support.google.com/adsense/answer/12176698) and [publisher privacy disclosures](https://support.google.com/publisherpolicies/answer/10437794).

## Files

- `index.html` — app, styling, SEO metadata, and content
- `robots.txt` — crawler access and sitemap location
- `sitemap.xml` — canonical homepage URL
