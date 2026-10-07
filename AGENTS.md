<!-- LOVABLE:BEGIN -->
> [!IMPORTANT]
> This project is connected to [Lovable](https://lovable.dev). Avoid rewriting
> published git history — force pushing, or rebasing/amending/squashing commits
> that are already pushed — as it rewrites history on Lovable's side and the
> user will likely lose their project history.
>
> Commits you push to the connected branch sync back to Lovable and show up in
> the editor, so keep the branch in a working state.
<!-- LOVABLE:END -->

# AGENTS.md

- Data model: the scanned-items list is anonymous — each browser generates a `device_id` (uuid in localStorage) and rows in `public.scanned_items` are scoped to it via RLS-free anon policies. No auth exists in this app; do not add user-facing login unless asked.
- Design system: "Kinetic Glass" — dark navy glassmorphism, cyan primary, indigo secondary, emerald success; all tokens in `src/styles.css` (oklch). Components must use semantic tokens, never hardcoded colors.
- Barcode decoding lives in `src/lib/barcode.ts` (native BarcodeDetector first, `@zxing/library` fallback, plus a photo-capture path); master-sheet parsing in `src/lib/products.ts` keeps every original column (barcode column "BC" first, else user picks it); scanned items + start/finish person live in localStorage. Both are dynamically imported in handlers to stay SSR-safe.
- UI language is Arabic with RTL layout (`dir="rtl"`); Arabic numerals for quantities are displayed as Western digits.
