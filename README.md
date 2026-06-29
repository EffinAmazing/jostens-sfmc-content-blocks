# Jostens SFMC Custom Content Blocks

Custom content blocks for Salesforce Marketing Cloud (SFMC) Content Builder, built for Jostens Yearbook prospecting emails.

---

## Overview

There are four blocks, each living in its own folder:

| Block | Folder | Purpose |
|---|---|---|
| CTA Block | `jostens-cta-block/` | Colored banner with header, body copy, and pill button |
| Hero Block | `jostens-hero-block/` | Hero section with configurable image, text, and button |
| Icon Grid Block | `jostens-icon-grid-block/` | 1–4 icons in a row with captions and optional CTA |
| List Block | `jostens-list-block/` | 1–4 items as icon grid, checkbox, bullet, or numbered list |

Each block folder contains:
- `index.html`: the block editor loaded inside Content Builder's sidebar
- `template.html`: a static reference template (not used at runtime)
- `icon.png` / `dragIcon.png`: block thumbnails shown in Content Builder

---

## Common Controls (All Blocks)

All four blocks share these UI patterns:

### Brand Color Swatches
Quick-pick buttons for the four Jostens brand colors:

| Swatch | Hex |
|---|---|
| Teal | `#00ACD8` |
| Green | `#79BB2F` |
| Pink | `#D22E7A` |
| Blue | `#264496` |

A strikethrough swatch removes the background color entirely (transparent / no background).

### Alignment
- **L / C / R** buttons set alignment per element (header, body, button)
- **Global Alignment** sets all elements at once
- **Mobile Alignment Override:** check "Override" to set separate alignments for screens 480px wide and below

### Padding
- Default: per-side (Top, Right, Bottom, Left) in px
- Toggle **All sides** to apply one value uniformly

### Button URLs
All button URL fields accept both plain URLs and AMPscript expressions:
- Plain: `https://jostens.com/yearbooks`
- AMPscript: `%%=RedirectTo(@JYBKProspectFormURL)=%%`

### Images
Upload all images to SFMC Content Manager and paste the URL into the block. All image URLs should be hosted in SFMC Content Manager.

### Show/Hide Toggles
Every text element and the button have a **Show** checkbox next to their field label. Unchecking it removes that element from the rendered email entirely.

---

## CTA Block

A full-width colored banner: header + body copy + pill-shaped CTA button.

### Fields

**Content**
| Field | Notes |
|---|---|
| Header Text | Bold all-caps headline |
| Body Text | Paragraph copy below the header |
| Button Label | Text inside the pill button |
| Button URL | Accepts AMPscript or a plain URL |

**Style**
| Field | Notes |
|---|---|
| Global Alignment | Sets header, body, and button alignment together |
| Background Color | Brand swatch or custom hex. Strikethrough = transparent |
| Text Color | Applies to both header and body |
| Button Background Color | Fill color of the pill button |
| Button Text Color | Text color inside the button |
| Mobile Alignment Override | Per-element alignment overrides at 480px and below |
| Padding | Outer padding around the whole block |

### Defaults
- Header: `THE JOSTENS DIFFERENCE`
- Body: Yearbook adviser support copy
- Button: `LET'S PARTNER TOGETHER` / `%%=RedirectTo(@JYBKProspectFormURL)=%%`
- Background: Pink (`#D22E7A`), Text: White, Button: Black with white text

### Email Client Notes
- The button uses a VML `<v:roundrect>` for Outlook so it renders as a true rounded button
- Dark mode email clients (Gmail app, Apple Mail) are handled via `[data-ogsb]` overrides in the embedded `<style>` block

---

## Hero Block

A flexible hero section that supports a header, body, hero image, and CTA button. The background can be a solid color, a background image, or a gradient.

### Fields

**Content**
| Field | Notes |
|---|---|
| Header Text | Bold headline |
| Body Text | Supporting paragraph copy |

**Hero Image**
| Field | Notes |
|---|---|
| Image URL | Upload to SFMC Content Manager and paste the URL |
| Image Alt Text | Screen reader description for the hero image |
| Show | Toggle to hide the image without removing the URL |
| Image Position | Where the image appears: **Top**, **After Header**, **After Body**, **Bottom** |
| Image Width | Pixel width for Outlook sizing (default: 768). See recommended widths by layout below |
| Image Padding | Per-side padding around the image. Effective image width = Width minus Left minus Right |

**Recommended Image Widths by Column Layout**

The email template baseline is 768px wide with 0px gutter between columns.

| Layout | Image Width |
|---|---|
| 1-up | 768px |
| 2-up | 384px |
| 3-up | 256px |
| 4-up | 192px |

Set the Image Width field to the value for your column layout. Use the T/R/B/L Padding fields only if you want the image inset within its cell. Inset padding reduces the Outlook-rendered width automatically, shown as "Effective width for Outlook" in the editor.

**Button**
| Field | Notes |
|---|---|
| Button Label | CTA text |
| Button URL | Accepts AMPscript or a plain URL |

**Background** (three modes, select via tabs)

| Mode | Description |
|---|---|
| **Solid** | Single color (brand swatches or custom hex). Strikethrough swatch = transparent |
| **Image** | Background image URL plus an Outlook Fallback Color. Outlook does not render CSS background images; recipients see the fallback color instead |
| **Gradient** | From/To colors plus direction. Outlook shows the "From" color as a solid fallback |

Gradient directions available: Top to Bottom, Bottom to Top, Left to Right, Right to Left, Diagonal down-right, Diagonal up-right.

**Style**
| Field | Notes |
|---|---|
| Global Alignment | Sets header, body, and button alignment together |
| Text Color | Applies to header and body |
| Button Background Color | |
| Button Text Color | |
| Mobile Alignment Override | Per-element alignment at 480px and below |
| Padding | Outer padding around the whole block |

### Defaults
- Header: `THE JOSTENS DIFFERENCE`
- Body: Yearbook adviser support copy
- Button: `LET'S PARTNER TOGETHER` / `%%=RedirectTo(@JYBKProspectFormURL)=%%`
- Background: Solid Pink (`#D22E7A`), Text: White, Button: Black with white text
- Image position: Top

### Email Client Notes
- Outlook does not render CSS background images. In Image mode, Outlook recipients see the **Outlook Fallback Color** — a solid color set via inline `background-color` on the block table. Choose a brand color that provides readable contrast for your text
- Gradient backgrounds degrade gracefully to the "From" solid color in Outlook
- The rounded CTA button uses a VML `<v:roundrect>` for Outlook across all background modes

---

## Icon Grid Block

A section with an optional headline and body text above a 1–4 icon grid, with captions under each icon. An optional CTA button sits below the grid.

### Fields

**Content**
| Field | Notes |
|---|---|
| Headline | Supports HTML. Use `<br>` for line breaks (e.g., `SUPPORT FOR<br>REAL CLASSROOMS`) |
| Body Text | Optional intro paragraph below the headline |

**Icons**
| Field | Notes |
|---|---|
| Number of Icons | 1, 2, 3, or 4 |
| Icon Caption Alignment | Shared alignment for all captions |
| Icon 1–4: Image URL | Upload to SFMC Content Manager and paste the URL |
| Icon 1–4: Alt Text | Screen reader description |
| Icon 1–4: Caption | Text shown below each icon |

**Button**
| Field | Notes |
|---|---|
| Button Label | CTA text |
| Button URL | Accepts AMPscript or a plain URL |

**Style**
| Field | Notes |
|---|---|
| Global Alignment | Sets headline, body, icon captions, and button together |
| Background Color | Brand swatch or custom hex |
| Text Color | Applies to headline, body, and captions |
| Button Background / Text Color | |
| Mobile Alignment Override | Per-element: Header, Body, Icon Captions, Button |
| Padding | Outer padding |

### Defaults
- 4 icons loaded with Jostens Digital Classroom campaign assets already hosted in SFMC Content Manager
- Background: Green (`#79BB2F`), Text: Dark (`#212121`), Button: Dark with white text

### Mobile Layout
| Icon Count | Mobile behavior (480px and below) |
|---|---|
| 1 | Full width |
| 2 | Side by side (2 columns) |
| 3 | Stacks to full width (1 column) |
| 4 | 2x2 grid (2 columns) |

---

## List Block

A flexible list section that supports four different list styles and 1–4 configurable items, each with an icon, header, body, and per-item CTA button.

### Fields

**Content**
| Field | Notes |
|---|---|
| Header Text | Section headline |
| Body Text | Optional intro paragraph (hidden by default) |

**Layout**
| Field | Notes |
|---|---|
| List Style | **Icon**, **Checkbox**, **Bullet**, **Numbered** |
| Orientation | **Horizontal** (multi-column) or **Vertical** (stacked rows). Icon style only |
| Number of Items | 1–4 |
| Item Text Alignment | |
| Show Icons | Show/hide the icon images. Icon style only |

**Items (per item, 1–4)**
| Field | Notes |
|---|---|
| Icon URL | Upload to SFMC Content Manager and paste the URL. Icon style only |
| Icon Alt Text | Screen reader description for the icon image. Icon style only |
| Header | Item title (show/hide toggle) |
| Body | Item description (show/hide toggle) |
| Button Label | Per-item CTA label (show/hide toggle). Icon style only |
| Button URL | Per-item link |

**Background / Style:** same controls as the other blocks (background color, text color, button colors, mobile alignment, padding)

### List Styles

**Icon (Horizontal)**
Items render as equal-width columns with icon above, then header, body, and button. On mobile (480px and below): 1-up for 1 item, 2-up for 2 or 4 items, 1-up for 3 items.

**Icon (Vertical)**
Items stack as rows with the icon on the left and text/button on the right.

**Checkbox**
Each item renders as a checkmark icon paired with header and body text. The checkmark image is already hosted in SFMC Content Manager. Icon URL and per-item button fields are not used in this mode.

**Bullet / Numbered**
Renders a standard `<ul>` or `<ol>` list. Icon URL and per-item button fields are not used. `<ul>` uses disc markers; `<ol>` uses decimal numbering.

### Defaults
- 2 items, Icon style, Horizontal orientation
- Background: Pink (`#D22E7A`), Text: White, Button: Black with white text
- Body text hidden by default

### Email Client Notes
- Per-item buttons use VML roundrects for Outlook
- Bullet and numbered lists use `mso-padding-alt` to maintain correct left indent in Outlook

---

## Outlook Compatibility

Outlook uses the Word rendering engine, which does not support many modern CSS properties. Each block handles this with specific fallback techniques.

### Rounded Buttons (All Blocks)

All blocks render pill-shaped buttons using a VML `<v:roundrect>` inside an Outlook conditional comment (`<!--[if mso]>`). Non-Outlook clients use a standard `<a>` tag with `border-radius`. Without the VML, Outlook would display a flat rectangular hyperlink with no border radius.

The button width in the VML is calculated from the label length, so longer button labels automatically get a wider VML shape.

### Solid Background Colors (All Blocks)

Solid colors are set as `background-color` inline on the table element. Outlook renders these reliably without any special handling needed.

### Background Images (Hero Block)

CSS `background-image` is not supported in Outlook. The Hero Block does not attempt to render background images in Outlook via VML. Instead, in **Image** mode, the block sets `background-color` inline on the table to the **Outlook Fallback Color**. Outlook recipients see this solid color; all other clients apply the CSS `background-image` and see the full background image.

In practice: set the Outlook Fallback Color to a brand color that provides readable contrast for your text. The rounded CTA button renders correctly in Outlook in all background modes.

### Gradient Backgrounds (Hero Block)

CSS `linear-gradient` is not supported in Outlook. When **Gradient** mode is selected, the table element has `background-color` set to the **From** color as an inline style. Outlook renders this as a solid color. Non-Outlook clients apply `background-image: linear-gradient(...)` and see the full gradient.

In practice: Outlook recipients see a solid fill using the "From" color. Choose a From color that looks intentional on its own.

### Bullet and Numbered List Indentation (List Block)

`<ul>` and `<ol>` elements use `mso-padding-alt` to control left indent in Outlook, which otherwise adds its own default spacing that can misalign the list with surrounding content.

### Dark Mode (All Blocks)

The `[data-ogsb]` selectors in each block's embedded `<style>` target Gmail's dark mode, which can invert or desaturate background colors and text. These rules reinforce brand background colors, text colors, and button colors so they render correctly in Gmail dark mode.

Note that Outlook's own dark mode implementation has known incompatibilities with background color rendering. Colors may appear differently than intended in Outlook dark mode even with these overrides in place.

---

## Tips for Email Sends

**Before sending:**
1. Always check the **live preview** at the bottom of each block editor before saving
2. Make sure you check your AMPscript URLs before sending — confirm the variable is defined in your send workflow and resolves to the correct destination
3. For Hero Block background images, Outlook recipients will see the **Outlook Fallback Color**, not the image. Make sure the fallback color provides enough contrast for your text

**Dark mode:**
- All blocks include `[data-ogsb]` CSS overrides for Gmail app and other dark-mode clients
- Background colors, text colors, and button colors all have dark mode fallbacks

**Padding between blocks:**
- Use the **Padding** control (Top/Bottom) to create visual spacing between adjacent blocks
- If two blocks share the same background color, they will appear seamless. Add padding to create a gap or use a different background color on the next block
