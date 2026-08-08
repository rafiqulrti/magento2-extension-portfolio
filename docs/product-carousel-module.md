# Product Carousel Module

*Four homepage merchandising carousels, tunable entirely from the admin.*

## Business problem

The homepage needed rotating product carousels — featured items, new arrivals, most viewed, best sellers — and marketing needed to tune them continuously: how many products each shows, whether prices appear, whether add-to-cart appears, what each section is called, whether it autoplays.

Hard-coded carousels meant a developer for every one of those adjustments. In practice the settings were chosen once at launch and never revisited, so the homepage stopped reflecting how the store actually merchandised.

## Solution

Four independent carousels, each with a full set of admin controls.

**Curated and automatic membership, combined deliberately.** Featured and new-arrival membership are merchant-curated through simple product flags — an editor decides what to promote. Most-viewed and best-seller sets derive from Magento's own reporting aggregations — the data decides. This is the right split: editorial judgement where the merchant has knowledge the data lacks, and automatic behaviour where the data is more reliable than a guess and would otherwise go stale.

**Everything is configurable, per carousel.** Each independently exposes enable/disable, product count, section heading, autoplay, price display, add-to-cart display, wishlist and compare display, review-rating display, arrow controls, pagination dots, and infinite loop. Nothing about the presentation requires a deployment, and the four carousels can be configured completely differently — a best-seller strip can show prices and add-to-cart while a new-arrivals strip stays purely visual.

## Layout

The featured carousel sits prominently on its own. The remaining three are grouped into a tabbed container to conserve vertical space — three stacked carousels would push everything else below the fold — with tab order and styling driven by layout arguments rather than template edits.

## Reuse over reimplementation

Wishlist, compare, and B2B requisition-list actions reuse **Magento's own components** rather than reimplementing them.

This is a correctness decision, not just an economy. Each action respects both this module's display toggle and Magento's own feature availability. For example, wishlist actions remain absent when wishlists are disabled, and requisition-list actions are shown only when the relevant B2B capability is available. Reusing Magento's components avoids duplicating business logic and reduces the risk of divergence during upgrades.

## Performance

The module registers a **dedicated image type at the exact rendered dimensions**, so Magento generates correctly-sized thumbnails rather than the browser downloading full catalog images and downscaling them in CSS.

On a homepage showing dozens of products across four carousels, this is the single largest payload factor on the page — the difference between a homepage that loads acceptably on mobile data and one that doesn't.

Product counts are configurable but always bounded, so no carousel can be made to render an unbounded collection.

## Multi-store

Every setting across all four carousels is scoped to default, website, and store view, so each storefront can merchandise independently from the same catalog.

## Magento concepts used

Product EAV attributes added via data patch and flagged for listing use, report aggregation collections, block groups and layout arguments, `ifconfig`-gated child blocks, custom image type registration, scoped system configuration with per-group defaults.

## Screenshot

The storefront example below shows the configurable product-carousel
presentation using demonstration catalog data.

<p align="center">
  <img
    src="../assets/screenshots/product-carousel-storefront.png"
    alt="Magento 2 configurable product carousel with product actions"
    width="900"
  >
</p>

---

[← Back to overview](../README.md)
