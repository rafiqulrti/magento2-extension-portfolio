# Editorial Blog Module

*A full blogging platform inside Magento, with a commercial path from article to cart.*

## Business problem

Merchants wanted to publish editorial content — buying guides, product explainers, regional news — to drive organic search traffic and support the catalog. Running a second CMS alongside Magento meant duplicated effort, inconsistent branding, two sets of credentials and deployments, and, most damagingly, no path from an article to a purchase. Content lived in one system and the catalog in another, so editorial traffic arrived and left without ever touching a product page.

## Solution

A blogging platform built as a native part of the store rather than bolted alongside it.

**Content model.** Posts support assignment to multiple categories, so a single article can be surfaced under several topics without duplication. Body content and a separate short excerpt are stored independently, so listings, sidebars, and search results use purpose-written summaries rather than truncated HTML — which is what produces the broken markup and mid-word cutoffs typical of naive blog listings. Title, publish date, and author are first-class fields, enabling chronological archives, scheduled publishing, and author pages.

**Product association.** The commercially significant piece. Posts can be linked to catalog products, which produces a related-products block on the article and a related-articles block on the product page. This makes the relationship bidirectional: editorial content becomes a merchandising surface with a direct path to cart, and product pages gain supporting content that helps buyers decide. It also means the value of a piece of content is attributable rather than assumed.

## Multi-store

Posts and categories are store-view scoped. One installation serves genuinely different editorial content per brand, region, or language — not the same content with a different header. For a multi-brand operation this is the difference between one Magento instance and several.

## Magento concepts used

Custom entities with resource models and collections, store-view-scoped content, catalog product association, admin grid and form management, storefront routing and listing pages.

---

[← Back to overview](../README.md)
