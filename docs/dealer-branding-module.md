# Dealer Branding Module

*Per-account co-branding on a B2B storefront: signed-in dealers see their own logo in the header.*

## Business problem

On a B2B store serving dealers and franchisees, each account wanted the storefront to feel like *their* portal rather than a generic supplier site. This is a small signal, but it appears on every page of every session, and in a channel relationship it reinforces that the dealer is a partner rather than a retail customer.

The alternative — building a separate branded storefront per dealer — multiplies infrastructure, deployment, and catalog maintenance for what is fundamentally a presentation concern.

## Solution

Each customer account can carry its own logo. When that customer is signed in, the storefront header shows their logo in place of the usual account name.

The behaviour degrades cleanly, which was the main design constraint:

- Visitors who aren't signed in see the standard header.
- Signed-in accounts **without** a logo fall back to their name, rendered normally.
- There is no broken image, no empty box, and no reserved blank space — the states are distinct rather than one being a damaged version of the other.

**Either side can set it.** An administrator can upload a logo on the customer's behalf — the common case, since a dealer will usually email an asset to their account manager — or the customer can supply it themselves during registration or from account settings. Supporting both avoids a workflow where every logo change is a support ticket.

## Performance

Uploaded logos are **resized once** to a constrained display size, preserving aspect ratio and transparency, and the derivative is cached on disk. Subsequent requests serve the cached file directly.

This matters more than it might appear. Dealers supply print-resolution logos; without a resize step, a multi-megabyte image would be sent on every page load of every session, to the customers the business most wants to keep happy. Caching the derivative means the resize cost is paid once per logo rather than once per request.

The block is explicitly marked **non-cacheable**, since its output is customer-specific. This is the security-relevant decision in the module: a cacheable block here would eventually serve one dealer's branding to another, which in a channel business is a visible and embarrassing data leak.

## Integration

Header placement is deliberately left to the consuming theme rather than being forced into a fixed position. Header structure varies enormously between themes, and a module that inserts itself into a hard-coded container either lands in the wrong place or fights the theme's own layout. The integrator chooses the position.

## Magento concepts used

Customer EAV attribute with file input, attribute registration across admin and storefront customer forms, image adapter resizing with on-disk derivative caching, customer session handling, explicit block cacheability control.

---

[← Back to overview](../README.md)
