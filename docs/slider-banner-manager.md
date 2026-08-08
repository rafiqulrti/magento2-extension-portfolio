# Slider / Banner Manager

*Campaign sliders bound to where they should appear, so launching a banner needs no deployment.*

## Business problem

Promotional sliders were placed by developers in theme layout XML. Every campaign — a seasonal banner on one category, a promotion on a specific landing page, a regional announcement — became a ticket, a code change, and a deployment. Campaigns therefore ran late, ran long past their end date because taking them down was also a deployment, or simply didn't run.

Merchants also had no way to give mobile visitors different artwork. Desktop banners were letterboxed, cropped badly, or rendered with unreadable text on phones — on the traffic segment that, for most of these stores, was the majority.

## Solution

Sliders are bound to **where they should appear** rather than being placed in code. The merchant creates a slider, chooses a target — a specific CMS page, a category, or a named route — and the module injects it on matching pages automatically. No developer involvement, no deployment, and taking a campaign down is a status toggle.

## Key design decisions

**Separate mobile artwork.** Every slide carries both a desktop and a mobile image. Campaigns are art-directed for each form factor rather than scaled and cropped, which means promotional text stays legible on the devices most customers actually use. This is a data-model decision, not a CSS one — you cannot crop your way to a different composition.

**Behaviour is data, not code.** Autoplay, navigation arrows, pagination dots, pause-on-hover, and lazy loading are stored per slider and set in the admin. Two sliders on the same site can behave completely differently without a theme change — a hero carousel can autoplay while a product-feature slider stays manual, which is the correct answer for both and impossible when behaviour is a global theme setting.

**Two carousel engines, selectable per slider.** The module bundles two established carousel libraries and the merchant picks per slider. A specific campaign's motion requirements never force a global theme decision, and a slider that needs a particular transition doesn't require swapping the library for the whole site.

**Rich, dynamic captions.** Slide caption content is processed through Magento's CMS directive filter, so merchants can reference media and store URLs in captions and have them resolve correctly across environments. Without this, captions authored on staging carry hard-coded staging URLs into production — a genuinely common and hard-to-spot failure.

## Accessibility

**Alt text is a first-class field** on every slide, sitting alongside the image in the admin form rather than being an optional afterthought or a template default. Promotional imagery in a slider frequently carries the page's primary message; leaving it undescribed makes that message invisible to screen-reader users and to search engines. Making the field part of the normal slide-creation flow is what gets it filled in.

## Performance

The slider block declares cache identities and an explicit cache key, so it participates correctly in full-page cache — invalidating when its slides change and being served from cache otherwise. Per-slider lazy loading limits the initial payload on slide-heavy carousels, so only the first slide's artwork is fetched up front.

## Admin experience

Sliders and slides have separate managed grids with image thumbnails, per-row actions, and mass operations.

Because the placement mechanism is powerful but not self-evident, the configuration screen carries an **in-admin instructions panel** explaining how to target and invoke a slider. This is deliberate: documentation in a wiki is documentation nobody reads, whereas an explanation on the screen where the work happens is read by the person doing the work, at the moment they need it.

## Multi-store

Slider targeting resolves against the current store's CMS pages and categories, and the module's enable switch is scoped, so storefronts can run independent campaign sets.

## Magento concepts used

Declarative schema across two related entities, layout-handle injection via an event observer, registry-based block coordination, UI-component listings with thumbnail and action columns, mass actions, custom system-configuration field renderer, CMS directive filtering, block cache identities.

---

[← Back to overview](../README.md)
