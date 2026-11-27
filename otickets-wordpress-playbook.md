# otickets store kit: build the same store on WordPress + WooCommerce

Purpose: give this file to a Claude session that has access to a NEW WordPress site (with WooCommerce) and ask it to "build the otickets store from this file". The store sells digital QuickBooks Desktop licences (US and Canada editions) delivered by email. It needs 11 variable products (1, 3 and 5 users), 4 categories, about 17 pages, 2 menus, and a clean light design.

This file is complete on its own: instructions, business facts, design spec, products, categories, pages, menus and policy texts. It is a rebuild of a Shopify store, so there is no Shopify theme code in it; the design is described as tokens and rules.

---

# 0. Instructions for the Claude session (read first)

1. Read the whole file before changing anything.
2. Confirm what you are connected to: WordPress version, active theme, whether WooCommerce is installed and active, and the site URL. Show it to the user and ask "is this the site I should build in?". Do not touch any other site.
3. Ask the open questions in section 1 and wait for answers. Do not invent business facts (address, legal name, refund rules, hours). Items marked [CONFIRM] must be confirmed by the owner.
4. Build in the phases of section 8, in order. After each phase, report in a few lines and READ BACK from the site what was created (counts, status, prices). Never say something worked without reading it back.
5. Things you may not be able to do through the API (tell the user to do them in wp-admin): install or activate plugins or themes, set up payments (WooCommerce Payments, Stripe, PayPal), set the store address/currency/taxes (WooCommerce -> Settings), connect a domain or SSL, set up email sending (SMTP), upload large media. Say exactly which ones failed.
6. Be honest about what you could not verify (the rendered look, order emails, payment flow, Google Merchant Center decisions).
7. This is not legal advice. The owner approves every policy text.
8. No relation to any other brand: this store is "otickets" only. Do not add any other store name, logo or domain anywhere.

---

# 1. Business facts and open questions

Known facts (use as given):

| Item | Value |
|---|---|
| Brand name | otickets |
| Domain | otickets.shop |
| Support email | contact@otickets.shop |
| Phone | +1 (907) 622-1000 |
| Operator | an individual trading as otickets (legal name not given) |
| Currency | USD |
| Delivery time | within 24 hours, by email |
| Refund window | 30 days (conditions below, [CONFIRM]) |
| Support hours | 24/7 by email and phone |
| Markets | United States and Canada |

Questions to ask the owner before building:

| # | Question |
|---|---|
| 1 | **Business address** (street, city, state, ZIP, country). It must be ONE real address, identical in WooCommerce settings, footer, Contact page, Legal notice and Google Merchant Center. Do not use an address where the business does not actually operate. [CONFIRM] |
| 2 | Operator legal name for the Legal notice page (optional) |
| 3 | Refund rules: is a full refund given only if the licence cannot be delivered or activated? Is a refund refused after successful activation? How many business days to process (kit says 5 to 10)? [CONFIRM] |
| 4 | Governing law for the Terms (place where the business is established) and the support hours [CONFIRM] |
| 5 | Payment provider (the kit says "a secure payment provider", name it if known) |
| 6 | Product images: see section 6. The owner must supply neutral images. |
| 7 | Prices: keep the prices in section 5.1 or change them |
| 8 | Proof that the licences may be resold (supplier invoice or reseller agreement) kept ready for Google/payment providers |

Keep ONE delivery time and ONE refund window everywhere (home, product page, FAQ, policies, announcement bar, emails).

---

# 2. What gets built

- WooCommerce shop with 11 **variable products**, product type "Software licence" as a category-independent attribute, variation attribute `Users` = `1 User`, `3 Users`, `5 Users`. All products are **virtual** (no shipping), not downloadable (the licence details are emailed manually or by automation after payment).
- 4 product categories: All (parent), Pro, Premier, Enterprise.
- Pages: Home, Shop, How it works, Compare editions, FAQ, Contact, About, plus policy pages (section 5.3 and 5.5).
- 2 menus (header, footer), an announcement bar, a footer with business details and the Intuit non-affiliation notice.
- WooCommerce emails customised so that the order confirmation says licence details follow by email within 24 hours.

---

# 3. Design spec

Look: light, airy, centered headlines, big rounded white cards with thin borders, pastel image panels, one lime accent, dark ink bands.

| Token | Value |
|---|---|
| Page background | `#fefdfb` |
| Ink (text, dark buttons) | `#213130` |
| Dark band / footer | `#222929` |
| Accent (primary buttons, ticks) | `#b0ec9c` (text on it is ink) |
| Card / soft panel | `#f1f1ea` |
| Muted text | `#565662` |
| Border | `#e6e5de` |
| Pastels (panels) | pink `#f3bdff`, yellow `#ffd88a`, blue `#addaff`, green `#b0ec9c`, coral `#ffb2a8`, lavender `#d4c2ff`, teal `#9feae2`, orange `#ffbb8a` |
| Font | Figtree (Google Fonts): headings weight 500, body 400, labels 600 |
| Radius | cards 24 to 32px, buttons and chips fully round (999px) |
| Spacing | 72px between home sections on desktop, 48px on mobile |
| Headlines | weight 500, tight letter-spacing (-0.025em) |

Implementation guidance:
- Use a lightweight block or classic theme (for example a free, fast theme such as Kadence, Astra or GeneratePress) and put the tokens above in the theme's global styles or "Additional CSS". Do not buy or install a paid theme without asking.
- Define CSS variables once: `:root{--bg:#fefdfb;--ink:#213130;--dark:#222929;--lime:#b0ec9c;--card:#f1f1ea;--muted:#565662;--line:#e6e5de}`.
- Buttons: lime background, ink text, pill shape; hover: ink background, white text.
- Product category/shop pages: 3-column grid on desktop, 2 on tablet, 1 on phone; card = white, 1px border `--line`, radius 26px, product title, three small boxes showing the 1/3/5 user prices, "View licence" link.
- Product page: image left (square, `--card` background), buy box right with three price cards for the user options (1 User, 3 Users, 5 Users), Add to cart, then three assurance lines (delivery, refund, support), then Overview + Details table, "How delivery works" 3 steps, "Good to know" accordion, "More editions" (4 related products), and the disclaimer paragraph.
- Header: dark announcement bar on top with the text in section 7, then a light header with logo/site name left, menu centered, search + cart right.
- Footer: dark rounded panel with a "Ready to choose your edition?" band, 4 link columns (Shop, Help, Legal) plus Business details, payment icons, the Intuit notice and copyright.
- Home sections (section 5.6): hero with a finder (edition, platform, country selects), licence grid with filter chips, 4 edition cards, small icon cards, dark "email" band, 3-step timeline, FAQ block, closing call to action.

Product attributes drive filters and MUST be kept: `Edition` (Pro, Premier, Enterprise, Enterprise Accountant), `Platform` (Windows, Mac), `Region` (USA, Canada), `Year` (2019, 2020, 2021, 2024). Create them as global product attributes (non-variation, visible). Use any free filter/search plugin only after asking the owner.

---

# 4. Wording rules (keep it compliant)

- Never use "genuine", "official", "lifetime", "instant", star ratings, review counts or customer counts unless the owner can prove the claim.
- Always say "independent seller, not affiliated with Intuit Inc." in the footer, on product pages and on the Legal notice page. Do not use Intuit or QuickBooks logos.
- Say "digital licence delivered by email, nothing is shipped".

---

# 5. Data

## 5.1 Products (11)

All products: type = Variable product; Virtual = yes; Downloadable = no; Tax status = taxable; "Sold individually" = no; Manage stock = no (in stock); Brand/vendor = otickets; attribute `Users` (used for variations, values `1 User`, `3 Users`, `5 Users`) plus the non-variation attributes Edition, Platform, Region, Year from the `attrs` field. Variation SKU = `sku_base` + `-1`, `-3`, `-5`. Category = the Pro/Premier/Enterprise category from `category` AND the parent category "QuickBooks Desktop licences".

~~~~json
[
 {"title":"QuickBooks Desktop Pro 2024 for Windows (US)","slug":"quickbooks-desktop-pro-2024-for-windows-us","sku_base":"QB-PRO-2024-WIN-US","category":"QuickBooks Desktop Pro","attrs":{"Edition":"Pro","Platform":"Windows","Region":"USA","Year":"2024"},"prices":{"1":"43.00","3":"79.00","5":"103.00"},"name":"QuickBooks Desktop Pro 2024","edition_text":"the US edition for Windows","blurb":"","region_line":"US edition: US sales tax, forms and payroll","os_line":"Windows 10 and 11 (64-bit)","feature_line":"Invoicing, expense tracking and bank reconciliation","older":false},
 {"title":"QuickBooks Desktop Pro 2024 for Mac (US)","slug":"quickbooks-desktop-pro-2024-for-mac-us","sku_base":"QB-PRO-2024-MAC-US","category":"QuickBooks Desktop Pro","attrs":{"Edition":"Pro","Platform":"Mac","Region":"USA","Year":"2024"},"prices":{"1":"55.00","3":"91.00","5":"103.00"},"name":"QuickBooks Desktop Pro 2024 for Mac","edition_text":"the US edition","blurb":"","region_line":"US edition: US sales tax, forms and payroll","os_line":"Runs on macOS","feature_line":"Invoicing, expense tracking and bank reconciliation","older":false},
 {"title":"QuickBooks Desktop Premier Plus 2024 for Windows (US)","slug":"quickbooks-desktop-premier-plus-2024-for-windows-us","sku_base":"QB-PREMPLUS-2024-WIN-US","category":"QuickBooks Desktop Premier","attrs":{"Edition":"Premier","Platform":"Windows","Region":"USA","Year":"2024"},"prices":{"1":"49.00","3":"103.00","5":"110.00"},"name":"QuickBooks Desktop Premier Plus 2024","edition_text":"the US edition for Windows","blurb":"Premier adds industry-specific reporting, sales orders and forecasting on top of Pro.","region_line":"US edition: US sales tax, forms and payroll","os_line":"Windows 10 and 11 (64-bit)","feature_line":"Industry-specific features and sales orders","older":false},
 {"title":"QuickBooks Desktop Enterprise 2024 for Windows (US)","slug":"quickbooks-desktop-enterprise-2024-for-windows-us","sku_base":"QB-ENT-2024-WIN-US","category":"QuickBooks Desktop Enterprise","attrs":{"Edition":"Enterprise","Platform":"Windows","Region":"USA","Year":"2024"},"prices":{"1":"55.00","3":"97.00","5":"110.00"},"name":"QuickBooks Desktop Enterprise 2024","edition_text":"the US edition for Windows","blurb":"Enterprise is the most capable desktop edition, with advanced inventory and pricing and more room for larger teams.","region_line":"US edition: US sales tax, forms and payroll","os_line":"Windows 10 and 11 (64-bit)","feature_line":"Advanced inventory, pricing and user roles","older":false},
 {"title":"QuickBooks Desktop Pro 2021 for Windows (US)","slug":"quickbooks-desktop-pro-2021-for-windows-us","sku_base":"QB-PRO-2021-WIN-US","category":"QuickBooks Desktop Pro","attrs":{"Edition":"Pro","Platform":"Windows","Region":"USA","Year":"2021"},"prices":{"1":"36.00","3":"73.00","5":"79.00"},"name":"QuickBooks Desktop Pro 2021","edition_text":"the US edition for Windows","blurb":"","region_line":"US edition: US sales tax, forms and payroll","os_line":"Windows 10 and 11 (64-bit)","feature_line":"","older":true},
 {"title":"QuickBooks Desktop Pro 2020 for Windows (US)","slug":"quickbooks-desktop-pro-2020-for-windows-us","sku_base":"QB-PRO-2020-WIN-US","category":"QuickBooks Desktop Pro","attrs":{"Edition":"Pro","Platform":"Windows","Region":"USA","Year":"2020"},"prices":{"1":"36.00","3":"73.00","5":"79.00"},"name":"QuickBooks Desktop Pro 2020","edition_text":"the US edition for Windows","blurb":"","region_line":"US edition: US sales tax, forms and payroll","os_line":"Windows 10 and 11 (64-bit)","feature_line":"","older":true},
 {"title":"QuickBooks Desktop Pro 2019 for Windows (US)","slug":"quickbooks-desktop-pro-2019-for-windows-us","sku_base":"QB-PRO-2019-WIN-US","category":"QuickBooks Desktop Pro","attrs":{"Edition":"Pro","Platform":"Windows","Region":"USA","Year":"2019"},"prices":{"1":"36.00","3":"73.00","5":"79.00"},"name":"QuickBooks Desktop Pro 2019","edition_text":"the US edition for Windows","blurb":"","region_line":"US edition: US sales tax, forms and payroll","os_line":"Windows 10 and 11 (64-bit)","feature_line":"","older":true},
 {"title":"QuickBooks Desktop Pro 2024 for Windows (Canada)","slug":"quickbooks-desktop-pro-2024-for-windows-canada","sku_base":"QB-PRO-2024-WIN-CA","category":"QuickBooks Desktop Pro","attrs":{"Edition":"Pro","Platform":"Windows","Region":"Canada","Year":"2024"},"prices":{"1":"49.00","3":"74.00","5":"85.00"},"name":"QuickBooks Desktop Pro 2024","edition_text":"the Canada edition for Windows","blurb":"","region_line":"Canada edition: GST/HST, CRA-compliant forms and Canadian payroll","os_line":"Windows 10 and 11 (64-bit)","feature_line":"Invoicing, expense tracking and bank reconciliation","older":false},
 {"title":"QuickBooks Desktop Premier 2024 for Windows (Canada)","slug":"quickbooks-desktop-premier-2024-for-windows-canada","sku_base":"QB-PREM-2024-WIN-CA","category":"QuickBooks Desktop Premier","attrs":{"Edition":"Premier","Platform":"Windows","Region":"Canada","Year":"2024"},"prices":{"1":"55.00","3":"97.00","5":"103.00"},"name":"QuickBooks Desktop Premier 2024","edition_text":"the Canada edition for Windows","blurb":"Premier adds industry-specific reporting, sales orders and forecasting on top of Pro.","region_line":"Canada edition: GST/HST, CRA-compliant forms and Canadian payroll","os_line":"Windows 10 and 11 (64-bit)","feature_line":"Industry-specific features and sales orders","older":false},
 {"title":"QuickBooks Enterprise Solutions 2024 for Windows (Canada)","slug":"quickbooks-enterprise-solutions-2024-for-windows-canada","sku_base":"QB-ENTSOL-2024-WIN-CA","category":"QuickBooks Desktop Enterprise","attrs":{"Edition":"Enterprise","Platform":"Windows","Region":"Canada","Year":"2024"},"prices":{"1":"61.00","3":"97.00","5":"110.00"},"name":"QuickBooks Enterprise Solutions 2024","edition_text":"the Canada edition for Windows","blurb":"Enterprise is the most capable desktop edition, with advanced inventory and pricing and more room for larger teams.","region_line":"Canada edition: GST/HST, CRA-compliant forms and Canadian payroll","os_line":"Windows 10 and 11 (64-bit)","feature_line":"Advanced inventory, pricing and user roles","older":false},
 {"title":"QuickBooks Enterprise Accountant 2024 for Windows (Canada)","slug":"quickbooks-enterprise-accountant-2024-for-windows-canada","sku_base":"QB-ENTACC-2024-WIN-CA","category":"QuickBooks Desktop Enterprise","attrs":{"Edition":"Enterprise Accountant","Platform":"Windows","Region":"Canada","Year":"2024"},"prices":{"1":"55.00","3":"97.00","5":"110.00"},"name":"QuickBooks Enterprise Accountant 2024","edition_text":"the Canada edition for Windows","blurb":"It is the Enterprise edition for accountants, adding the Accountant Toolbox for managing client files.","region_line":"Canada edition: GST/HST, CRA-compliant forms and Canadian payroll","os_line":"Windows 10 and 11 (64-bit)","feature_line":"Accountant Toolbox for client files","older":false}
]
~~~~

### Product description template

Build each product's long description (HTML) from its fields. Omit the `blurb` sentence or the `feature_line` list item when the field is empty. Include the "Please note" block only when `older` is true.

~~~~html
<h2>What you are buying</h2>
<p>A licence for {name}, {edition_text}. {blurb} It is a one-time purchase, delivered by email, with installation and activation help from our team.</p>
<ul>
  <li>{region_line}</li>
  <li>{os_line}</li>
  <li>Choose 1, 3 or 5 users</li>
  <li>{feature_line}</li>
</ul>
<!-- only if older = true -->
<h2>Please note</h2>
<p>This is an older version. Intuit may no longer provide some services for it, such as support, payroll or bank feeds. Check Intuit's current policy before you buy.</p>
<h2>What arrives by email</h2>
<p>Within 24 hours of your order you receive your licence number, product number, validation code, the installer download link and a setup guide.</p>
<p>otickets is an independent seller and is not affiliated with Intuit Inc.</p>
~~~~

Short description (the line under the title): `{Region} edition for {Platform}, version {Year}. One-time purchase, delivered by email.`

## 5.2 Product categories (4)

WooCommerce has no "smart" collections, so assign categories when creating each product (field `category` above, plus the parent).

| Name | Slug | Contains | Expected count |
|---|---|---|---|
| All QuickBooks Desktop licences (parent) | `quickbooks-desktop` | all 11 products | 11 |
| QuickBooks Desktop Pro | `quickbooks-desktop-pro` | Edition = Pro | 6 |
| QuickBooks Desktop Premier | `quickbooks-desktop-premier` | Edition = Premier | 2 |
| QuickBooks Desktop Enterprise | `quickbooks-desktop-enterprise` | Edition = Enterprise or Enterprise Accountant | 3 |

Category descriptions:
- All: "Every QuickBooks Desktop edition we sell, for Windows and Mac, in 1, 3 or 5 user sizes. Licence details are delivered by email."
- Pro: "QuickBooks Desktop Pro licences, the core desktop accounting suite for small businesses."
- Premier: "QuickBooks Desktop Premier licences, with industry-specific reporting, sales orders and forecasting."
- Enterprise: "QuickBooks Enterprise licences, including Enterprise Accountant, for larger teams and advanced inventory needs."

Sort each category by price, low to high. Make the child categories children of "All" (the parent category page shows all 11 products).

## 5.3 Pages (store pages)

Create each as a normal WordPress page (status Published unless stated). Page bodies below are HTML.

~~~~json
[
 {"slug":"how-it-works","title":"How it works","body":"see 5.6"},
 {"slug":"compare","title":"Compare editions","body":"see 5.6"},
 {"slug":"faq","title":"FAQ","body":"see 5.6"},
 {"slug":"contact","title":"Contact","body":"see 5.6"},
 {"slug":"about","title":"About otickets","body":"see below"},
 {"slug":"delivery-policy","title":"Delivery policy","body":"see below"},
 {"slug":"order-cancellation-policy","title":"Order cancellation policy","body":"see below"},
 {"slug":"payment-policy","title":"Payment policy","body":"see below"},
 {"slug":"cookie-policy","title":"Cookie policy","body":"see below"},
 {"slug":"legal-notice","title":"Legal notice","body":"see below"},
 {"slug":"refund-policy","title":"Refund policy","body":"see section 5.5, keep as DRAFT until the owner approves"},
 {"slug":"shipping-policy","title":"Shipping policy","body":"see section 5.5"},
 {"slug":"terms-of-service","title":"Terms of service","body":"see section 5.5"},
 {"slug":"privacy-policy","title":"Privacy policy","body":"see section 5.5"},
 {"slug":"contact-information","title":"Contact information","body":"see section 5.5"}
]
~~~~

For legal-style pages use a simple readable layout: narrow centered column (max 820px), an intro box (background `#f1f1ea`, radius 22px, padding 22px) for the first paragraph, `h2` headings with a top border, and a "Contact us" card at the bottom showing the business name, email, phone and address.

**About otickets**

~~~~html
<div class="intro"><p>otickets is an online seller of QuickBooks Desktop licences for customers in the United States and Canada.</p></div>
<h2>What we do</h2>
<p>We sell licences for QuickBooks Desktop Pro, Premier and Enterprise, in 1, 3 and 5 user sizes. Everything is delivered digitally: after checkout, your licence details arrive by email and nothing is shipped.</p>
<h2>How we help</h2>
<p>Each order includes a setup guide, and our team helps with installation and activation by email or phone. Support is available 24/7.</p>
<h2>Independence from Intuit</h2>
<p>otickets is an independent seller. We are not affiliated with, endorsed by or sponsored by Intuit Inc. QuickBooks is a registered trademark of Intuit Inc., and product names are used only to identify the software we sell.</p>
<h2>Contact</h2>
<p>Email <a href="mailto:contact@otickets.shop">contact@otickets.shop</a> or call +1 (907) 622-1000. Our business address is shown in the contact box at the bottom of this page.</p>
~~~~

**Delivery policy**

~~~~html
<div class="intro"><p>All otickets products are digital licences. Nothing is physically shipped, and there are no shipping fees.</p></div>
<h2>Digital delivery, nothing is shipped</h2>
<p>After your payment is confirmed, we email your licence details to the address you entered at checkout. You will also receive an order confirmation.</p>
<h2>Delivery time</h2>
<p>Your licence details arrive within 24 hours of payment. Many orders are delivered sooner.</p>
<h2>What the email contains</h2>
<ul><li>Your licence number</li><li>Your product number</li><li>Your validation code</li><li>A link to download the installer</li><li>A step-by-step setup guide</li></ul>
<h2>What we need from you</h2>
<ul><li>A working email address entered correctly at checkout.</li><li>The right edition for your business: country (US or Canada), platform (Windows or Mac) and number of users.</li><li>A compatible computer: Windows 10 or 11 (64-bit) for Windows editions, macOS for the Mac edition.</li></ul>
<h2>Where we deliver</h2>
<p>We deliver by email to customers in the United States and Canada. Choose the US or Canada edition that matches where your business operates.</p>
<h2>If something goes wrong</h2>
<ol><li>Check your spam or junk folder.</li><li>Confirm the email address on your order.</li><li>If nothing has arrived after 24 hours, contact us with your order number and we will check right away.</li></ol>
<p>If you entered the wrong email address, contact us as soon as possible so we can help.</p>
<h2>Contact</h2>
<p>Email <a href="mailto:contact@otickets.shop">contact@otickets.shop</a> or call +1 (907) 622-1000. Support is available 24/7.</p>
~~~~

**Order cancellation policy**

~~~~html
<div class="intro"><p>This page explains when an order can be cancelled. For refunds after delivery, see our refund policy.</p></div>
<h2>Before your licence details are sent</h2>
<p>You can ask to cancel an order before we have sent your licence details. Contact us at <a href="mailto:contact@otickets.shop">contact@otickets.shop</a> or +1 (907) 622-1000 with your order number.</p>
<h2>After your licence details are sent</h2>
<p>Once licence details have been delivered, the order can no longer be cancelled. Refund requests are handled under our refund policy.</p>
<h2>How to ask</h2>
<p>Send us your order number and the email address used at checkout. We reply by email.</p>
~~~~

**Payment policy** (replace "the payment provider" with the real provider name once known)

~~~~html
<div class="intro"><p>Payments on otickets are processed by our payment provider through a secure checkout.</p></div>
<h2>Payment methods</h2>
<p>The payment methods available to you are shown at checkout and can vary by location and device. We do not see or store your full card details. The payment provider processes the payment securely.</p>
<h2>Currency and taxes</h2>
<p>Prices are shown in US dollars. Any applicable taxes are calculated and shown at checkout before you pay.</p>
<h2>Order confirmation</h2>
<p>After payment is confirmed, you receive an order confirmation by email, followed by your licence details within 24 hours.</p>
<h2>Payment problems</h2>
<p>If a payment fails or you see an unexpected charge, contact us at <a href="mailto:contact@otickets.shop">contact@otickets.shop</a> with your order number.</p>
~~~~

**Cookie policy**

~~~~html
<div class="intro"><p>This page explains how otickets uses cookies and similar technologies on otickets.shop.</p></div>
<h2>What cookies are</h2>
<p>Cookies are small text files stored on your device when you visit a website. They help the site work and remember your choices.</p>
<h2>How we use them</h2>
<ul><li><strong>Essential cookies:</strong> keep your cart, checkout and session working.</li><li><strong>Analytics cookies:</strong> help us understand how the site is used, where enabled.</li><li><strong>Preference cookies:</strong> remember settings such as your region.</li></ul>
<h2>Managing cookies</h2>
<p>You can block or delete cookies in your browser settings. Blocking essential cookies may stop parts of the site from working.</p>
<h2>Questions</h2>
<p>Contact us at <a href="mailto:contact@otickets.shop">contact@otickets.shop</a>. See also our privacy policy.</p>
~~~~

**Legal notice**

~~~~html
<div class="intro"><p>Information about the business behind otickets.shop.</p></div>
<h2>Business details</h2>
<ul><li><strong>Trading name:</strong> otickets</li><li><strong>Operated by:</strong> an individual trading as otickets</li><li><strong>Website:</strong> otickets.shop</li><li><strong>Email:</strong> <a href="mailto:contact@otickets.shop">contact@otickets.shop</a></li><li><strong>Phone:</strong> +1 (907) 622-1000</li></ul>
<p>The business address is shown in the contact box at the bottom of this page.</p>
<h2>Not affiliated with Intuit</h2>
<p>otickets is an independent seller of software licences. We are not affiliated with, endorsed by or sponsored by Intuit Inc. QuickBooks is a registered trademark of Intuit Inc. Product names are used only to identify the software we sell.</p>
<h2>Digital products</h2>
<p>All products are digital licences delivered by email. Nothing is shipped.</p>
<h2>Related policies</h2>
<p>See our delivery, payment, cancellation, cookie, privacy and refund policies for details.</p>
~~~~

## 5.4 Menus

Header menu: Home / Shop QuickBooks (category `quickbooks-desktop`) / Compare editions (`/compare/`) / How it works (`/how-it-works/`) / FAQ (`/faq/`) / Contact (`/contact/`).

Footer menu: About otickets / Contact information / Delivery policy / Order cancellation policy / Payment policy / Cookie policy / Legal notice / Refund policy (only after it is published) / Terms of service / Privacy policy.

Announcement bar (above the header): "Licence key emailed within 24 hours. 30-day refund window, conditions apply."

## 5.5 Policy pages (text for the owner to approve)

Items in [square brackets] must be confirmed by the owner before publishing. This is not legal advice. Use the business address from question 1 wherever [address] appears.

**Refund policy** (publish only after approval)

~~~~html
<div class="intro"><p>DRAFT, not yet approved by the store owner. Review the conditions below before publishing.</p></div>
<h2>Our promise</h2>
<p>If we cannot deliver a working licence for the product you bought, you get a full refund. We offer a 30-day refund window from the date of purchase.</p>
<h2>When you get a full refund</h2>
<ul><li>We cannot deliver your licence details.</li><li>The licence cannot be activated, even after our team has helped you.</li><li>You were charged more than once for the same order.</li></ul>
<h2>When a refund isn't possible [CONFIRM]</h2>
<ul><li>The licence has been successfully activated.</li><li>You chose the wrong edition, country, platform or number of users after the licence was delivered.</li><li>The request is made after the 30-day window.</li></ul>
<h2>How to ask for a refund</h2>
<p>Email <a href="mailto:contact@otickets.shop">contact@otickets.shop</a> with your order number and the email address used at checkout, and tell us what went wrong.</p>
<h2>Processing [CONFIRM]</h2>
<p>Approved refunds are returned to the original payment method. Banks usually take 5 to 10 business days to show the refund.</p>
<h2>Contact</h2>
<p>Questions? Email <a href="mailto:contact@otickets.shop">contact@otickets.shop</a> or call +1 (907) 622-1000.</p>
~~~~

**Shipping policy**: use the Delivery policy text above (same content), title "Shipping policy".

**Terms of service** (Last updated: [date])

1. **What we sell.** otickets is an independent seller of QuickBooks Desktop licences for customers in the United States and Canada. We are not Intuit Inc. and are not affiliated with, endorsed or sponsored by Intuit. QuickBooks is a registered trademark of Intuit Inc.
2. **Choosing your licence.** You are responsible for choosing the right edition, country, platform and number of users, and for checking that your computer is compatible.
3. **Delivery and activation.** Licence details are sent by email within 24 hours of payment. Our team helps with installation and activation by email or phone.
4. **Intuit's terms.** Your use of the software is also governed by Intuit's own licence terms. Intuit may change or end services for older versions, such as support, payroll or bank feeds. Check Intuit's current policy before you buy.
5. **Prices and payment.** Prices are shown in US dollars and any taxes are shown at checkout. Payments are processed through the payment provider's secure checkout.
6. **One-time purchase.** Each purchase is a one-time payment for the licence you chose. There is no subscription and no automatic renewal.
7. **Refunds.** Refunds are handled under our refund policy.
8. **Support.** Support is available 24/7 by email at contact@otickets.shop and by phone at +1 (907) 622-1000. [CONFIRM] Support covers installation and activation, not accounting advice, training or your company files.
9. **Intellectual property.** All product names and trademarks belong to their owners. The content of this website belongs to otickets.
10. **Limitation of liability.** To the extent permitted by law, our liability is limited to the amount you paid for the order. Nothing here limits rights that the law does not allow us to limit.
11. **Cancellation by us.** We may cancel an order and refund it in full if we cannot deliver it, if it appears fraudulent, or if the product is unavailable.
12. **Disputes.** These terms are governed by the laws of the place where otickets is established, without affecting any mandatory consumer protections that apply to you. [CONFIRM]
13. **Contact.** contact@otickets.shop, +1 (907) 622-1000, [address].

**Privacy policy**
- *Information we collect:* contact details (name, email, phone), order details, billing and payment details handled by the payment provider, and basic device and usage data from the website.
- *How we use your information:* to process and deliver your order, provide support, prevent fraud, meet legal obligations, and improve the website.
- *Sharing:* we share information only with service providers we need to run the store, such as the hosting company and payment providers, and where the law requires it. [CONFIRM: "We do not sell your personal information."]
- *Data protection:* payment card details are handled by the payment provider and are not stored by us.
- *Your rights:* you can ask to access, correct or delete your personal information, or to opt out of marketing, by emailing contact@otickets.shop.
- *Data retention:* we keep order information for as long as needed for support, accounting and legal reasons.
- *Contact:* contact@otickets.shop, [address].
(WooCommerce can also generate a privacy policy draft: Settings -> Privacy. Review it before using.)

**Contact information**: otickets, [address], Email contact@otickets.shop, Phone +1 (907) 622-1000, Support 24/7 by email or phone, Website otickets.shop. Plus the Intuit non-affiliation sentence.

## 5.6 Page content (home, how it works, compare, FAQ, contact)

**Home page** (set as the static front page; set "Shop" to the WooCommerce shop page)
1. Hero: headline "Your QuickBooks Desktop licence, in your inbox". Subheading: "Pro, Premier and Enterprise licences for Windows and Mac. Pay at checkout and your licence key arrives by email within 24 hours, with install help from our team." A finder bar with three selects (Edition: Any, Pro, Premier, Enterprise, Enterprise Accountant; Platform: Windows or Mac; Country: US or Canada edition) and a lime button "Find my licence", linking to the shop page filtered by those attributes. Note under it: "One-time purchase. Choose 1, 3 or 5 users on the product page."
2. "Find your licence": filter chips (All, US edition, Canada edition, Windows, Mac) and the product grid (all 11 products, each card showing title and the 1/3/5 user prices).
3. A line: "11 licences for US and Canadian businesses".
4. Four edition cards: Pro ("For small businesses", "The core desktop accounting suite", "Invoicing, expense tracking and bank reconciliation, with 150+ built-in reports."), Premier ("For industry reporting", "Everything in Pro, plus industry tools", "Industry-specific features, sales orders and forecasting."), Enterprise ("For larger teams", "Advanced inventory and user roles", "Includes Enterprise Accountant, with the Accountant Toolbox for client files."), Compare ("Not sure yet?", "See the editions side by side", "A quick guide to which edition and how many users you need."). Use the pastel panels pink, yellow, blue, green.
5. "...and so much more!": four small cards: Email delivery, 1, 3 or 5 users, US and Canada, Help when you need it.
6. Dark band "Your licence details arrive by email": "Within 24 hours of your order you receive everything you need to install and activate. Nothing is shipped, and our team helps by email or phone if you get stuck." Button "See how an order works". Next to it an illustrative email card listing: Licence number, Product number, Validation code, Installer download, Setup guide.
7. "Three steps from order to activation": 1 Pick and pay, 2 Receive your licence (within 24 hours), 3 Set up and activate.
8. FAQ block with 5 questions (see FAQ below) and a "See all questions" button.
9. Closing call to action: "Ready to choose your edition?" button "Shop licences". Small print: "One-time purchase. 30-day refund window, conditions apply."

**How it works**: heading "From checkout to activation, explained"; lead "The whole process is online. You pay, we email your licence details, and our team can help you set up."; chips: Delivered by email, Within 24 hours, Help included. Sections: (a) "How an order works" with 3 steps: Pick and pay (pick edition, country, platform and users, check out securely), Receive your licence (details emailed, nothing shipped), Set up and activate (follow the guide, help by email or phone). (b) Dark band "What the email contains": Licence number, Product number, Validation code, Installer link, Setup guide. (c) "Check these before you order": Match your country (US edition = US sales tax, forms and payroll; Canada edition = GST/HST, CRA-compliant forms and Canadian payroll), Check your platform (Windows 10 and 11 64-bit; the Pro 2024 for Mac edition runs on macOS and is sold separately), Use a working email. (d) "Something not right? Here is what to do": Email has not arrived (links to Delivery policy), Trouble activating (links to Contact), Need a refund (30-day window, links to Refund policy). (e) CTA "Ready to place your order?".

**Compare editions**: heading "Which edition suits your business?"; lead "Pro, Premier and Enterprise differ in reporting, inventory tools and how many people can work in the file at once. Every edition comes as a 1, 3 or 5 user licence."; chips: Windows and Mac, US and Canada, 1, 3 or 5 users. Three cards: Pro (Small businesses; The core accounting suite; list: Invoicing, expenses, bank reconciliation / 150+ built-in reports / Basic inventory tracking / Windows and Mac editions), Premier (Industry reporting; Everything in Pro, plus more; Industry-specific editions / Sales orders and forecasting / 200+ built-in reports / For contractors, wholesalers, nonprofits and more), Enterprise (Growing companies; The most capable edition; Advanced inventory and pricing / Granular user roles / Capacity for up to 40 simultaneous users / Enterprise Accountant adds the Accountant Toolbox). Then this table:

| What you get | Pro | Premier | Enterprise |
|---|---|---|---|
| Invoicing, expenses, bank reconciliation | Yes | Yes | Yes |
| Built-in reports | 150+ | 200+ | 200+ |
| Industry-specific editions | No | Yes | Yes |
| Sales orders and forecasting | No | Yes | Yes |
| Advanced inventory and pricing | No | No | Yes |
| Licence sizes | 1, 3 or 5 users | 1, 3 or 5 users | 1, 3 or 5 users |
| Country editions | US and Canada | US and Canada | US and Canada |
| Delivery | By email | By email | By email |

"A quick way to decide": You work alone or with a small team -> Pro; You need industry reports, sales orders or forecasting -> Premier; You need advanced inventory or many people in the file -> Enterprise; You manage client files as an accountant -> Enterprise Accountant. "Choose a licence size": 1 user (one installation for one person), 3 users (multi-user mode so a small team or your accountant can work in the same company file), 5 users (growing teams, each with their own permissions). CTA "Found your edition?".

**FAQ** (group by topic: Ordering and delivery, Editions, Refunds and support; use an accordion)
- *What do I receive after purchase?* An email with your licence number, product number, validation code, an installer download link and an installation and activation guide.
- *How long does delivery take?* Within 24 hours after your order is confirmed. See the delivery policy.
- *I have not received my email. What should I do?* Check your spam or junk folder and the email address on your order. If it still has not arrived, contact us with your order number and we will check right away.
- *Is this a subscription?* No. These are one-time purchases of QuickBooks Desktop licences, not monthly or yearly plans.
- *How does payment work?* Payments are processed by our payment provider's secure checkout, and the payment methods available are shown at checkout. See the payment policy.
- *Which edition should I choose?* Pro suits small businesses, Premier adds industry reports, sales orders and forecasting, and Enterprise adds advanced inventory and pricing for larger teams. See the comparison page.
- *US edition or Canada edition?* Choose the edition that matches where your business operates. The US edition uses US sales tax, forms and payroll. The Canada edition uses GST/HST, CRA-compliant forms and Canadian payroll.
- *Does it run on Windows and Mac?* Windows editions run on Windows 10 and 11 (64-bit). The Pro 2024 for Mac edition is sold separately and runs on macOS.
- *How many users do I need?* Every edition comes as a 1, 3 or 5 user licence. Choose 1 for one person, or 3 or 5 so several people can work in the same company file.
- *What is your refund policy?* We offer a 30-day refund window (conditions apply). Full terms are on the refund policy page.
- *Can I cancel my order?* An order can be cancelled before your licence details have been sent. See the order cancellation policy.
- *Do you help with installation and activation?* Yes. We help with installation and activation by email or phone.
- *Are you affiliated with Intuit?* No. We are an independent seller of software licences and are not affiliated with, endorsed or sponsored by Intuit Inc. QuickBooks is a trademark of Intuit Inc.

**Contact**: heading "Contact otickets"; lead "Questions about an order, delivery or activation? Call, email, or use the form below. Support is available 24/7." Left box "Business details": otickets, email, phone, address, "Licence details are delivered by email, within 24 hours.", links to Refund policy and Delivery policy. Right box: contact form with Name, Email, Message (use the free Contact Form 7 or WPForms Lite only after asking the owner, or the theme's built-in form). Success text: "Thanks, your message has been sent. We will reply by email."

---

# 6. Product images (important)

- Do NOT use box-shot images that show the Intuit / QuickBooks logo, or that contain text such as "lifetime license", "100% Genuine License", "Instant Delivery", "not a Subscription". They contradict the wording rules in section 4 and can cause problems with Google Merchant Center and with Intuit.
- Use neutral images supplied by the owner: for example a plain card per product with the edition, year and platform as text, no logos, no promotional claims. Recommended size 1200 x 1200 px, WebP or JPG, with alt text equal to the product title.
- Until images are supplied, publish products without images (WooCommerce shows a placeholder) rather than using the wrong ones.

---

# 7. WooCommerce settings to apply

- General: store address (from question 1), selling location(s) = United States and Canada, currency USD, enable taxes only if the owner asks.
- Products: Virtual on every product; no shipping zones needed. Disable the shipping calculator.
- Checkout: guest checkout allowed; require billing email and phone is optional; make sure the email field is clearly labelled because licence details are sent there.
- Emails: edit the "Processing order" and "Completed order" email text to say: "Thanks for your order. Your licence details (licence number, product number, validation code, installer link and setup guide) will arrive by email within 24 hours." Set the "From" name to otickets and the address to contact@otickets.shop.
- Pages: set Shop, Cart, Checkout, My account pages; set Terms and conditions page = Terms of service; set Privacy policy page = Privacy policy; set the front page to Home.
- Permalinks: Post name. Product base: `/product/`. Category base: `/collections/` is optional; if used, keep `quickbooks-desktop` working at `/collections/quickbooks-desktop/` (the menu links use it).
- Orders are fulfilled manually (or with an owner-approved automation): after payment, the owner emails the licence details. Say so in section 9 of the final report.

---

# 8. Build order (phases)

**Phase 0: connect and inspect.** Report WordPress version, theme, active plugins, whether WooCommerce is active, existing pages/products/categories. Show it to the user.

**Phase 1: site and store settings.** Site title `otickets`, tagline "QuickBooks Desktop licences delivered by email", admin/support email contact@otickets.shop, WooCommerce address/currency (section 7). Ask the owner to do anything the API cannot do. Read back.

**Phase 2: attributes and categories.** Create the global attributes Edition, Platform, Region, Year and the 4 categories (5.2). Read back counts later.

**Phase 3: products.** Create the 11 variable products (5.1) with the description template, short description, categories, attributes, 3 variations each (price, SKU, virtual). Publish them. Read back: status Published, virtual, variation prices, SKUs, category counts (All 11, Pro 6, Premier 2, Enterprise 3).

**Phase 4: pages.** Create the pages in 5.3, 5.5 and 5.6. Keep Refund policy as Draft. Read back the list with status.

**Phase 5: menus, header, footer, design.** Create the two menus (5.4), the announcement bar, the footer (columns Shop, Help, Legal, Business details, the Intuit notice, copyright) and apply the design tokens (section 3). Read back the menu items.

**Phase 6: verification (report honestly).**
- [ ] 11 products published, virtual, correct prices/SKUs/attributes, in the right categories.
- [ ] 4 categories with the right counts.
- [ ] All pages exist; Refund policy is Draft until approved.
- [ ] Menus work; footer links resolve.
- [ ] Delivery time (24 hours) and refund window (30 days) are identical everywhere.
- [ ] Business name, email, phone and address are identical in WooCommerce settings, footer, Contact page and Legal notice.
- [ ] No Intuit/QuickBooks logos and no "genuine/lifetime/instant" claims anywhere.
- [ ] Preview home, a product, a category, Compare, FAQ, Contact and a legal page on desktop and phone width.
- [ ] Test order end to end with the real payment provider; confirmation email arrives.

---

# 9. Final report the session should give the owner

1. What was created (counts) and what was read back and verified.
2. What could not be done through the API and exactly what the owner must do in wp-admin (plugins, theme, payments, SMTP, domain/SSL, address).
3. What could not be seen rendered (ask the owner to preview and send screenshots of anything that looks wrong).
4. Open questions from section 1 that are still unanswered, especially the business address, the refund conditions, and the product images.
5. A reminder that licence details are sent manually after each paid order unless the owner sets up an approved automation.

---

# 10. Google Merchant Center readiness (before submitting a feed)

1. Site published over HTTPS on the real domain, not password-protected.
2. Business name, address, phone and email are IDENTICAL in WooCommerce, footer, Contact, Legal notice and the Merchant Center account. Use one real, verifiable address and a monitored mailbox. Never show an address that is not where the business operates.
3. Refund policy exists, is linked in the footer, has a real window and conditions, and matches the return policy in Merchant Center. Shipping policy describes digital delivery. Terms and Privacy pages exist. Contact information exists.
4. Product data: clear title, link, image (neutral, see section 6), price in USD, availability, condition `new`, brand `otickets`, identifiers or "no identifier".
5. Keep proof of authorisation to sell these licences (supplier invoices or a reseller agreement) ready for Google and payment providers.
6. The Intuit non-affiliation notice stays in the footer, on product pages and in the Legal notice. Do not use Intuit or QuickBooks logos.
