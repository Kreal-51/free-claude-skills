# Core Web Vitals Improvement Plan — Harborlight Coastal Rentals

**Prepared by:** Vix, Senior Wix SEO Specialist
**Site:** harborlightrentals.com (Wix Studio)
**Baseline source:** Google Search Console Core Web Vitals report + PageSpeed Insights (field data, last 28 days) + GTmetrix lab test on 3 representative pages

## Current State

| Metric | Property pages (mobile) | Homepage (mobile) | Target |
|---|---|---|---|
| LCP | 3.9s | 2.8s | ≤2.5s |
| CLS | 0.18 | 0.06 | ≤0.1 |
| INP | 310ms | 240ms | ≤200ms |

GSC classifies 14 of 18 property pages as "Needs Improvement," none as "Poor," and none as "Good." The homepage and blog posts pass on desktop but sit at "Needs Improvement" on mobile, which is the segment that matters most — 71% of Harborlight's organic sessions are mobile per GA4.

## Root Cause 1: Unoptimized Hero Images (Primary LCP driver)

Each property page's largest contentful element is the hero gallery image, averaging 2.4MB, uploaded directly from the photographer's RAW-converted JPEGs without resizing. Wix does apply its own compression and serves WebP automatically to supporting browsers via its Media Manager — but only up to the resolution of the **source file uploaded**, so an oversized source still ships an oversized derivative.

**Fix:**
1. Re-export all 18 hero images at 1920px max width (current source files average 4000px+) before uploading to Wix Media Manager — this alone should cut hero image payload by roughly 60-70%.
2. In the Wix Editor, confirm each hero image element uses "Fit to screen" scaling rather than a fixed oversized container that forces Wix to serve a larger derivative than needed.
3. Re-upload through Media Manager (do not just resize in the Editor's crop tool, which doesn't reduce the underlying file Wix serves).

## Root Cause 2: Layout Shift from Late-Loading Booking Widget (CLS)

The third-party booking availability widget embedded via Wix's HTML iframe element loads after initial paint and reserves no space until its content arrives, pushing the page content down by roughly 180px once it loads — this is the dominant CLS contributor on property pages.

**Fix:** Set an explicit fixed height on the iframe's container box in the Editor (Wix lets you set a minimum height on embed elements) matching the widget's typical rendered height, so the layout doesn't shift when it populates. This is a workaround, not a true fix — flagged to the client as a Wix/third-party-widget limitation: Wix doesn't offer a way to lazy-reserve dynamic third-party iframe dimensions natively the way you could with a custom-coded skeleton loader on another platform.

## Root Cause 3: Render-Blocking Apps from the App Market (INP / load time)

Site Members, a live chat widget, and an Instagram feed app are all installed and loading on every page, including pages where they're not used (the Instagram feed app loads sitewide even though it's only displayed on the homepage). Each adds its own JS bundle to every page load.

**Fix:**
1. Remove the Instagram feed app from global site settings and re-add it only on the homepage via the page-specific app panel (Wix allows per-page app scoping for most Market apps — this was simply never configured on install).
2. Evaluate whether the live chat widget's real conversion value (checked against GA4 event data — it generated 4 leads in 90 days) justifies its performance cost; recommended switching it to load on a delay (most chat apps offer a "load after X seconds" setting) rather than removing it outright, since it does have some value.
3. Site Members is required for the client login area — kept, but confirmed it's not force-loading on public pages that don't need it.

## Root Cause 4: Font Loading

Wix Studio's custom font (a Google Font, "Fraunces," loaded at 4 weights) blocks text rendering briefly on first load. Reduced from 4 weights to 2 (regular + bold) in the Editor's Text Theme settings — the other two weights (light, black) were used on fewer than 3 elements sitewide and can be replaced with CSS-level bold/regular styling instead.

## What Wix Cannot Do Here (Limitation Honesty)

Wix does not expose server response headers, HTTP/2 push, or custom caching rules — Vix confirmed this isn't a lever available on this platform, unlike a custom-hosted stack. Wix's own CDN and server response time (TTFB averaged 480ms in testing) is outside the client's control and already reasonably competitive for the platform; no further action recommended there.

## Expected Impact & Timeline

| Fix | Expected LCP/CLS/INP impact | Effort |
|---|---|---|
| Hero image re-export | LCP: 3.9s → ~2.6s | 1 day (18 images) |
| Booking widget fixed-height container | CLS: 0.18 → ~0.05 | 2 hours |
| Instagram app page-scoping | INP: minor improvement, fewer pages affected | 30 minutes |
| Chat widget load-delay | INP: 310ms → ~260ms | 15 minutes |
| Font weight reduction | Minor LCP/INP gain sitewide | 20 minutes |

Re-test via PageSpeed Insights and GSC's Core Web Vitals report 28 days after all fixes ship, since GSC's field data is a rolling 28-day window and won't reflect changes immediately.
