# Custom Menu Manager

*Admin-managed navigation, decoupled from the category tree and placeable through the widget system.*

## Business problem

Magento's navigation is driven by the category tree. Any menu that isn't a category listing — footer link columns, utility navigation, curated mega-menu panels, campaign-specific link sets — required a developer to edit theme layout XML and templates. Marketing could not adjust navigation without a release, which meant that in practice navigation simply didn't change between deployments, and temporary campaign links either never appeared or long outlived their campaign.

## Solution

An admin-managed menu builder using a two-level model: named menu containers, each holding an ordered set of items. Menus and their items are edited on a single admin screen rather than across two disconnected grids, so building a menu is one task rather than a navigation exercise.

**Item-level control.** Each item carries:

- An **active/inactive toggle**, so a full navigation change can be built and reviewed in advance, then switched on at launch — rather than being assembled live in production.
- A **link target behaviour** setting, so external or document links can open appropriately without a developer editing markup.
- A **per-item CSS class**, which lets the theme style or icon individual entries without hard-coding selectors against link text. This is the detail that keeps themes stable: without it, styling one menu item means matching on its label, and the styling silently breaks the moment someone rewords the link.

Menus themselves also carry an active/inactive toggle, so an entire alternate navigation set can be staged.

## Rendering

Menus are exposed through **Magento's widget system**. A merchant can place any menu into any CMS page, CMS block, or layout position through the standard widget instance UI, choosing the menu from a dropdown — with no developer involvement at all. Direct layout placement remains available for themes that need a menu in a fixed structural position.

This was a deliberate choice over a custom placement mechanism: the widget UI is something merchants already know, and it inherits Magento's own per-store and per-page targeting for free.

## Performance

The module registers its **own dedicated cache type**. Rendered menus are cached independently of full-page cache and can be flushed on their own from Cache Management.

This matters operationally: without it, changing one footer link means invalidating full-page cache across the entire site and paying the cold-cache cost on every page. With a separate cache type, a navigation change flushes navigation and nothing else.

## Magento concepts used

Widget declaration with source models, service contracts (data interfaces for both entities), custom cache type registration, admin ACL, UI-component grids with mass actions, nested admin form and grid composition.

---

[← Back to overview](../README.md)
