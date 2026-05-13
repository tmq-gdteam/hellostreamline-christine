# Section Background Fix Design Spec

## Objective
Fix abrupt background color changes across the `deploy/index.html` page by localizing the page-wide background gradient into individual sections.

## Architecture & Styles
- **Global Body:** 
  - Change the `--bg-primary` CSS variable in `growth-mode-overrides.css` to a solid `#fff` (white) background instead of the stretched linear gradient.
- **Hero Section:**
  - Apply the original gradient specifically to the `.hero` class within `growth-mode-overrides.css`: `background: linear-gradient(180deg, #fff8f6 0%, #fff 25%, #faf7ff 65%, #fff 100%);`
  - This ensures the hero maintains its visual style without the gradient stretching down the rest of the page.
- **Other Sections:**
  - Ensure the `.pricing` and `.roi` sections accurately display their own independent backgrounds with no interference from the body.

## Scope
- This change applies specifically to `deploy/css/growth-mode-overrides.css`.
- Modifying `--bg-primary` will also ensure consistent backgrounds across any other pages relying on the Growth-Mode tokens without introducing unintended mid-page color shifts.
