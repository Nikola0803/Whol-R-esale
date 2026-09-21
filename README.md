# EVLV — peptide wholesale site

A static site. No build step, no dependencies, no backend. Open `index.html`
locally, or drop the whole folder on any static host (Netlify, Cloudflare
Pages, Vercel, S3, GitHub Pages). Fonts come from Google Fonts; everything
else is local.

## Pages

    index.html          Home
    products.html       Products — the full catalogue, 13 compounds + 3 blends
    platform.html       Platform — storefront, CRM, operations, plugin, API
    wholesale.html      Wholesale — tiers and the supply split
    dropshipping.html   Fulfillment — cold chain and shipping scope
    compliance.html     Compliance — carries the RUO legal detail
    coa.html            Certificates of analysis — lookup + sample cert
    blog.html           The Research Desk
    apply.html          The four-step KYC application
    login.html          Partner login stub, for the CRM/storefront redirect

Plus sixteen product detail pages, one per catalogue line
(`product-bpc-157.html`, `product-tb-500.html`, and so on). Each carries its
own title, meta description and Open Graph tags, a breadcrumb, a certificate
panel and the gated-pricing block.

    assets/site.css         Shared stylesheet — every token and component
    assets/product-*.jpg    Product photography used by the CSS
    assets/source/          The full-resolution master the crops come from

## Look

Light theme only. There is one `:root` token block at the top of `site.css`
and no `prefers-color-scheme` branch, so every visitor sees the same thing.
Type is Plus Jakarta Sans for headings and Inter for body. Change `--acc` to
reshade the site.

Product imagery is real photography, referenced from `site.css` as custom
properties (`--shot-hero` and friends). Those `url()` values are relative to
the stylesheet, so `url("product-hero.jpg")` resolves to
`assets/product-hero.jpg`.

The four JPEGs are crops of one master shot, kept at
`assets/source/packaging-master.png` so they can be recut without going back
for the original. Each crop has a fixed job: `product-card.jpg` is the whole
shot at 2:3 and is used with `background-size:contain`, so it is never
cropped further; `product-pack.jpg` is the carton and vial together;
`product-vial.jpg` is the vial detail; `product-hero.jpg` is a landscape band
across both labels. Swapping the photography means recutting those four at
the same sizes — no stylesheet change needed.

## Application form

`apply.html` is a four-step KYC flow: business details, verification
documents, trading plan, then four declarations. It is driven by the small
controller at the bottom of the page — steps are `fieldset.fstep`, navigation
is `[data-next]` / `[data-back]`, and each step is gated by native form
validation before it will advance.

## Before launch

- `login.html` submits nowhere. It needs wiring to real auth once a CRM
  backend exists.
- The application form and the newsletter form both post to `#`. Point them
  at a real endpoint.
- Contact addresses use the `evlv.example` placeholder domain.
- "EVLV / peptides" is a placeholder brand name and appears in the header,
  the footer and every page title.

## Compliance

Every page carries the research-use-only banner and the full legal block in
the footer. Products are supplied for laboratory research only, never for
human or veterinary use, and no page states wholesale pricing publicly —
pricing sits behind entity verification. Keep it that way when editing.
