# Manufacturer Management

*Real brand destinations — logo, copy, SEO metadata, and product listings — replacing Magento's manufacturer dropdown.*

## Business problem

Magento treats manufacturer as a simple dropdown attribute: a label with no image, no description, and no page of its own.

For brand-led catalogs this leaves significant value on the table. Brand-name searches are high-intent traffic with nowhere to land, so that traffic goes to the manufacturer's own site or a competitor's brand page. Customers who shop by brand — common in parts, tools, and industrial supply — have no browsing path. And the store has no way to tell a brand's story, which is often exactly what a dealer agreement expects it to do.

## Solution

A full brand entity with its own admin management, storefront landing pages, and product association.

Each brand carries a name, logo, teaser and rich long-form description, per-brand SEO metadata, a display order, an active/inactive status, and a flag controlling whether it appears in the homepage brand strip.

## SEO

Brands resolve to clean, brand-named URLs through a custom front-end router, with a **configurable URL suffix** so the pattern matches whatever convention the rest of the site already uses — consistency here matters both to users and to search engines, and hard-coding a suffix would make the module's pages the odd ones out.

Metadata works as **store-level defaults with per-record overrides**. A catalog of several hundred brands gets sensible, consistent metadata immediately, while brands that warrant hand-written metadata can have it. The alternative — requiring every brand to have metadata written before it can launch — is what leaves brand pages sitting unindexed for months.

## Product association

A multi-value product attribute sources its options from the brand records themselves, so products associate with one or more brands and each brand page lists its products. Because the options come from live brand data, the association list can't drift away from the brands that actually exist.

Brand data is exposed through **service contracts** — data interfaces and a repository — so other modules integrate against a stable API rather than reaching into resource models. This is what allows a theme or a downstream module to surface brand data without coupling itself to the storage layer.

## Multi-store

SEO defaults and the URL suffix are configurable per website and store view, so brand pages fit each storefront's URL and metadata conventions.

## Admin experience

A managed listing with **inline editing**, mass delete, and mass status change — inline editing matters here specifically because bulk-adjusting display order or status across a few hundred brands through individual edit forms is unusable.

The edit form provides a rich-text editor for brand copy and a validated image uploader with a staged upload directory, so an interrupted or abandoned upload never leaves a partial file in the live media path.

## Performance

The brand listing declares cache identities so it participates correctly in full-page cache, and is paginated rather than rendering an unbounded catalog of brands.

## Magento concepts used

Custom entity with resource model and collection, service contracts and repository, UI-component listing with inline edit and mass actions, WYSIWYG form element, image uploader with staged directories, custom front-end router with URL suffix handling, product attribute with array backend and custom source model, block cache identities.

---

[← Back to overview](../README.md)

