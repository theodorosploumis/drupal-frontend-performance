# Frontend Performance Checklist for Drupal websites
> A checklist & guide to make sure you (Drupal 8.x) website will be fast! Made for Drupal frontend developers and site builders.

# 1. Checklist
## 1.1 HTML

- [ ] Mobile first design except if there is no need
- [ ] Critical link (aka css) tags are in head
- [ ] Less critical link tags are end of body
- [ ] Less critical link tags lazy load
  - [ ] `<link rel="preload" as="style" onload="this.rel='stylesheet'" id='dashicons-css' >`
- [ ] JS loads with the async property
  - [ ] `<script async src="https://hi.js"></script>`
  - [ ] or `defer` when scripts need to be loaded in order, or require the DOMContentLoaded Event
- [ ] Keep DOM simple and small (Maximum DOM Depth < 12). Must "kill" some of the default Drupal wrappers
- [ ] Create custom and simple 404, 403 error pages using twig template suggestions

## 1.2 Images

- [ ] Always use next gen formats
  - [ ] webp -> chrome/firefox
  - [ ] jpeg xr -> ie11/edge
  - [ ] jpeg 2000 -> safari
- [ ] Use jpg for photography, not png
- [ ] Size images properly
- [ ] Use srcsets for multiple image sizes
- [ ] Use the `<picture>` element to let the browser select the right image for a scenario
- [ ] [Lazy load images below the fold](https://aka.terrible.dev/web/lazyimages)

## 1.3 CSS

- [ ] Avoid using `!important`
- [ ] Use svg instead of icon fonts like fontawesome
- [ ] Create svg sprites (or png sprites if svg are not available)
- [ ] Do not support olb browsers (remove too old prefixes)
- [ ] Avoid expensive selectors when possible
  - [ ]  `border-radius`
  - [ ]  `box-shadow`
  - [ ]  `transform`
  - [ ]  `filter`
  - [ ]  `:nth-child`
  - [ ]  `position: fixed;`
  - [ ]  Partial matching: `[class^="wrap"]`
- [ ]  Don't use universal selectors
  - [ ]  Avoid universal selectors like `*, [disabled], [type=“text”]`, etc. They are very expensive for the browser to match, as every element in the DOM must be checked.
- [ ]  Avoid deeply nested dependent selectors
  - [ ]  The descendant selector is very costly, as the browser must check for a match with every descendant element. On a complex web page, this can result in thousands and thousands (perhaps even more) of descendant selector searches.
- [ ]  Use media queries to load files based on use case
  
```css 
<link href="style.css" rel="stylesheet" media="all">
<link href="portrait.css" rel="stylesheet" media="orientation:portrait">
<link href="print.css" rel="stylesheet" media="print">
<link href="desktop.css" rel="stylesheet" media="(min-width: 720px)">
```
- [ ] Investigate using functional css instead of custom styles (eg [Tailwind](https://tailwindcss.com), [Tachyons](https://tachyons.io) etc. See more at https://css-tricks.com/need-css-utility-library)

## 1.4 JS

- [ ] Bundles should always be minified
- [ ] Bundles should have 0 comments, and all license text extracted to a separate file
- [ ] Use [Google Tag Manager](https://tagmanager.google.com) for 3rd party scripts like Google Analytics, FB Pixel etc
- [ ] Move js on bottom of the html page

## 1.5 Assets

- [ ]  All assets should be fingerprinted
- [ ]  All assets should have `Cache-Control: max-age=365000000, immutable` as a header
- [ ]  Assets should be served over http/2
- [ ]  Assets should only be served on a cookieless domain
- [ ]  All files should be cached by a CDN
- [ ]  Support Brotli compression if able
  - [ ]  15-30% smaller than gzip
- [ ]  Compress with gzip, or zopfli as a fallback to brotli
- [ ]  Do not ship unused css, js
- [ ] Try to clone external js/css to local server and load them from there (eg Google Analytics script)

### 1.5.1 CDN with free tiers
- https://anyone.cdn.biz.id
- https://jetpack.com/pricing
- https://www.cloudflare.com/plans
- https://shift8cdn.com
- https://www.coralcdn.org
- https://cloudinary.com
- https://github.com/thumbor/thumbor (OS self-hosted)

## 1.6 Fonts

- [ ] Fonts should always load `woff2` first
- [ ] `woff` for fallback
- [ ] Use `font-display: swap;` to allow the browser to use a fallback font while custom font files are being downloaded.
- [ ] eot, or truetype is only needed for `IE < 10`

## 1.7 PWA

- [ ]  Use a service worker to cache assets
- [ ]  Use a service worker to prefetch pages users will most likely navigate to next
- [ ]  Support offline, and spotty networks

## 1.8 Server

- [ ] Prefer Nginx over Apache2

---

# 2. Drupal modules
## 2.1 Development related
- https://www.drupal.org/project/seo_checklist
- https://www.drupal.org/project/html_checker
- https://www.drupal.org/project/blackfire
- https://www.drupal.org/project/devel
- https://www.drupal.org/project/performance_budget
- https://www.drupal.org/project/perfmon

## 2.2 Caching related
- **https://www.drupal.org/project/advagg**
- https://www.drupal.org/project/http_cache_control
- https://www.drupal.org/project/big_pipe_sessionless
- https://www.drupal.org/project/prefetch_cache
- https://www.drupal.org/project/cdn (and other CDN related modules)
- https://www.drupal.org/project/fastly
- https://www.drupal.org/project/stackpath

## 2.3 Image optimmizations
- https://www.drupal.org/project/lazy
- https://www.drupal.org/project/blazy
- https://www.drupal.org/project/lazyloader
- https://www.drupal.org/project/fancyload
- https://www.drupal.org/project/drimage
- https://www.drupal.org/project/imageapi_optimize_webp
- https://www.drupal.org/project/imageapi_optimize_binaries

## 2.4 Other
- https://www.drupal.org/project/quicklink
- https://www.drupal.org/project/minifyhtml
- https://www.drupal.org/project/critical_css
- https://www.drupal.org/project/amp
- https://www.drupal.org/project/amp_cts
- https://github.com/Drupal-Jedi/css-tree-shaking
- https://www.drupal.org/project/pwa
- https://www.drupal.org/project/fast_404

---

# 3. Tools
## 3.1 Performance scoring - Online
- https://developers.google.com/speed/pagespeed/insights
- https://www.thinkwithgoogle.com/feature/testmysite
- https://yellowlab.tools
- https://www.webpagetest.org
- https://tools.pingdom.com
- https://search.google.com/test/mobile-friendly
- https://web.dev/measure
- https://gtmetrix.com
- https://www.uptrends.com/tools/website-speed-test
- https://gf.dev/website-audit
- https://www.giftofspeed.com
- https://varvy.com/pagespeed
- https://www.gumlet.com/analyzer
- https://www.dareboost.com
- https://www.checkbot.io
- https://compare.sitespeed.io (Beta)

## 3.2 Performance scoring - Offline (local installed)
- https://www.sitespeed.io
- https://developers.google.com/web/tools/lighthouse
- https://github.com/gmetais/YellowLabTools
- https://github.com/sitespeedio/browsertime
- http://devbridge.github.io/Performance
- https://github.com/GoogleChromeLabs/psi
- https://github.com/paulirish/pwmetrics
- https://github.com/desktoppr/wbench
- http://yslow.org/command-line-har

## 3.3 Sprite Generators
- https://instantsprite.com (online - png/gif export)
- https://github.com/frexy/svg-sprite-generator
- https://github.com/sprity/sprity
- https://github.com/itsjavi/spritesheet-generator
- https://github.com/selaux/node-sprite-generator

## 3.4 Unused CSS - Online
- https://unused-css.com
- https://uncss-online.com
- https://www.jitbit.com/unusedcss
- https://purifycss.online

## 3.5 Unused CSS - Offline
- **https://github.com/Drupal-Jedi/css-tree-shaking**
- https://github.com/uncss/uncss
- https://www.purgecss.com
- https://github.com/probosckie/cssTreeShaking
- https://github.com/AlanJenkinsVS/css-tree-shaking
- https://github.com/purifycss/purifycss

## 3.6 Critical CSS/AboveTheFold CSS - Online
- https://criticalcss.com
- https://jonassebastianohlsson.com/criticalpathcssgenerator
- https://www.sitelocity.com/critical-path-css-generator

## 3.7 Critical CSS/AboveTheFold CSS - Offline
- **https://github.com/stefspakman/drupal-critical**
- https://github.com/addyosmani/critical
- https://github.com/filamentgroup/criticalCSS
- https://github.com/pocketjoso/penthouse
- https://github.com/finkinfridom/kant.io
- https://github.com/bezoerb/inline-critical
- https://github.com/hummal/crittr
- https://github.com/GoogleChromeLabs/critters
- https://github.com/theKashey/used-styles
- https://github.com/filamentgroup/loadCSS

## 3.8 Other tools
- https://instant.page
- https://github.com/turbolinks/turbolinks
- https://github.com/sitespeedio/coach
- https://www.sitespeed.io/documentation/throttle
- [CodePen - Performance Budget Builder](https://codepen.io/bradfrost/pen/EPQVBp)
- https://github.com/tkadlec/grunt-perfbudget
- https://micmro.github.io/PerfCascade

---

# 4. Guides & Resources
## 4.1 Collections of tools, posts etc
- https://github.com/fabkrum/web-performance-resources
- https://perf.rocks
- https://www.perf-tooling.today
- https://web.dev 
- https://browserdiet.com

## 4.2 Drupal related articles
- https://www.drupal.org/docs/8/modules/advanced-cssjs-aggregation/advanced-aggregates
- https://www.fourkitchens.com/blog/article/use-grunt-and-advagg-inline-critical-css-drupal-7-theme

---

# 5. Similar projects
- https://frontendchecklist.io
- https://www.taskade.com/v/H1XaaoP0Ab
- https://jonyablonski.com/designers-wpo-checklist
- https://github.com/TerribleDev/WebPerformanceChecklist

--- 
# 6. Licence
[MIT](LICENSE.txt)
