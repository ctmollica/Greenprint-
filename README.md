# 🌿 Greenprint

**See the carbon behind every checkout.**

Greenprint is a Firefox extension that shows the estimated carbon footprint of products while you shop, and suggests a lower-carbon alternative like buying refurbished or secondhand.

![license](https://img.shields.io/badge/license-MIT-green)

<!-- Add a screenshot: docs/screenshot.png -->
<!-- ![Greenprint badge on a product page](docs/screenshot.png) -->

## Contents

- [Features](#features)
- [Install](#install)
- [How it works](#how-it-works)
- [Limitations](#limitations)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [Code of Conduct](#code-of-conduct)
- [Security](#security)
- [Privacy](#privacy)
- [Changelog](#changelog)
- [License](#license)

## Features

- Detects product pages on Amazon, eBay, Walmart, Best Buy, and Target
- Shows an estimated kg CO₂e badge under the product title
- Shows how much you could save by buying refurbished or secondhand, and what that equals in km driven
- Links to a search for the greener option on the same store
- Dismissible, with no accounts, tracking, or network requests

## Install

**Temporary (development and testing)**

1. Clone or download this repo.
2. Open `about:debugging#/runtime/this-firefox` in Firefox.
3. Click **Load Temporary Add-on…** and select `manifest.json`.
4. Open a product page (the URL usually contains `/dp/`, `/ip/`, or `/itm/`).

Temporary add-ons are removed when Firefox restarts. Permanent installs require a version signed through [addons.mozilla.org](https://addons.mozilla.org/developers/).

**Try these searches on Amazon:** "55 inch 4K TV", "gaming laptop", "unlocked smartphone", "men's jeans", "paperback book".

## How it works

1. A content script checks whether the current URL looks like a product page.
2. It reads the product title and matches it against keyword categories (laptop, phone, shoes, etc.).
3. Each category has a rough average footprint and a typical reduction for refurbished or secondhand goods.
4. A badge is injected using Shadow DOM so it doesn't clash with the store's styles.
5. A lightweight check runs every second so the badge survives page re-renders and in-page navigation.

## Limitations

- **Estimates are rough category averages**, not measurements for the specific product. Treat them as a nudge, not a lab result.
- Keyword matching can misfire (a "phone case" may be tagged as a phone).
- Site layouts change, so selectors may need updating.

## Roadmap

- [ ] Exclusion words to cut false positives
- [ ] Toolbar popup with a running total of carbon saved
- [ ] Cart and checkout page totals
- [ ] Better data sources for emissions estimates
- [ ] Chrome build

## Contributing

Contributions are welcome!

1. Fork the repo and create a branch: `git checkout -b feature/short-description`
2. Make your change and test it by loading the extension in Firefox.
3. Open a pull request describing what changed and why, with a screenshot for visual changes.

Ways to help:

- **Add or improve categories** in the `CATS` array in `content.js`. Please cite a source for any emissions figure.
- **Fix false positives** by improving keyword matching.
- **Add store support** by adding the domain to `matches` in `manifest.json` and to the `SEARCH` map in `content.js`.
- **Report bugs** with the store, product URL, and Firefox version.

Code style: plain JavaScript, no build step, no external network requests, and wrap risky logic in try/catch so the host page never breaks.

## Code of Conduct

Be respectful, patient, and constructive. Welcome newcomers, assume good intent, and give and accept feedback gracefully. Harassment, discrimination, and personal attacks are not tolerated. Maintainers may remove content or contributors that violate these standards. Report problems to **ctmollica@gmail.com**.

Adapted from the [Contributor Covenant 2.1](https://www.contributor-covenant.org/version/2/1/code_of_conduct/).

## Security

If you find a security issue, please don't open a public issue. Email **ctmollica@gmail.com** with details and steps to reproduce.

## Privacy

Greenprint runs entirely in your browser. It reads the product title on supported pages to pick a category, stores nothing, and sends nothing anywhere.

## Changelog

### 0.1.1 - 2026-10-02
- Fixed: badge reappears if the site re-renders and removes it
- Fixed: badge is removed when navigating away from a product page
- Fixed: dismissed badges stay dismissed
- Fixed: better badge placement on Amazon
- Fixed: errors no longer propagate to the host page

### 0.1.0 - 2026-10-02
- Initial release: carbon badge on product pages for Amazon, eBay, Walmart, Best Buy, and Target
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
