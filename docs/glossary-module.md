# Glossary Module

*A managed terminology database rendered as a scannable A–Z reference page.*

## Business problem

Technical and industrial catalogs are full of specification terms, materials, standards, and acronyms that buyers and sellers don't share a vocabulary for. Definitions were scattered across product descriptions, spec sheets, and PDFs — which meant they weren't findable by customers, weren't consistent between products, weren't indexable by search engines, and had to be rewritten by whoever was creating the next product page.

The support cost is real: a buyer who can't confirm what a term means either calls, or buys the wrong thing and returns it.

## Solution

A managed terminology database, maintained in the admin and rendered as a single scannable A–Z reference page.

**Admin side.** Terms are maintained in a standard admin grid with full-text search, column filtering, paging, and export — the same interaction model as every other Magento grid, so there's nothing to learn. Adding a term is a two-field form.

**Storefront side.** The page groups terms automatically by initial letter, buckets numeric and symbol-initial entries separately so they don't distort the alphabet, and presents both an alphabet jump bar and a search filter. Grouping is derived at render time from the term list, so it stays aligned with the current terminology data and there is no separate ordering metadata to maintain.

**Framing is configurable.** The page's heading and introduction are set per store, so the same term set can be introduced differently for different audiences or brands without duplicating the underlying content.

## Routing

A custom front-end router resolves the glossary to a clean, friendly URL. This avoids requiring a URL rewrite to be created and maintained per store — rewrites drift, get deleted during imports, and are a common source of 404s after a migration.

## Accessibility and performance

These were the same decision. Grouping and sorting happen **server-side**, and the letter navigation and search filter operate on content that is already rendered in the page:

- The page is **fully readable and navigable without JavaScript** — the complete term list, its headings, and its structure are all in the initial HTML.
- There is **no loading state** before content appears, and no layout shift as content arrives.
- Screen readers encounter a real document structure — headings and definition lists — rather than an empty container waiting for a script.
- The search filter is progressive enhancement over present content, not a gate in front of it.

## Multi-store

The page heading and introduction are store-scoped. The term set itself is intentionally global — a definition of a technical standard doesn't vary by storefront, and duplicating the glossary per store view would create a maintenance burden with no editorial benefit. This is a deliberate, documented decision rather than an omission.

## Hyvä

Supported, with parallel Hyvä templates and layout handles alongside the Luma versions, sharing the same block and model layer.

## Magento concepts used

Declarative schema, UI-component grid and form with custom button blocks, admin ACL and menu integration, custom front-end router, scoped system configuration, storefront layout and templating for two theme families.

## Screenshot

The storefront renders the complete terminology directory with
alphabetical navigation and search while keeping all glossary content
available in the initial server-rendered HTML.

<p align="center">
  <img
    src="../assets/screenshots/glossary-storefront.png"
    alt="Magento 2 glossary storefront with alphabetical navigation and search"
    width="900"
  >
</p>

---

[← Back to overview](../README.md)
