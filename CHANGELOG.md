# Changelog

## renormalize.css — v1.1

### Fix

- `min-height: 100dvh` sekarang punya fallback `min-height: 100vh` di baris sebelumnya.
  Safari < 15.4 tidak support `dvh`; tanpa fallback `min-height` menjadi invalid.
- `word-wrap: break-word` dihapus dari `pre`. Redundan — `pre` sudah pakai
  `white-space: pre-wrap` yang menghandle wrapping.
- Komentar di `a` rule diperbaiki: hapus kalimat tentang `transition` yang sudah
  tidak ada di property.
- Komentar di blok media diperbaiki: hapus `object-fit: cover` dari daftar
  hal yang di-set (kontradiksi dengan komentar di bawahnya).

---

## renormalize_x.css — v4.0.1

### Fix

- `h6 { font-size: 0.8rem }` diganti ke `calc(var(--base) * 0.8)` agar
  mengikuti `--base` token. Sebelumnya hardcode membuat h6 tidak berubah
  saat `--base` di-override. Ditambah komentar bahwa ini intentional label/meta.
- `--border-color` dan `--surface-color` sekarang punya fallback `rgba()`
  sebelum `color-mix()`. Browser tanpa support `color-mix()` (Chrome < 111,
  Safari < 16.2, Firefox < 113) sebelumnya melihat border invisible.

---

## re_story.css — v1.1

### Fix

- `:where(figure, blockquote, pre, hr) + p` sekarang eksplisit pakai `& ` prefix
  (menjadi `& :where(...) + p`). Secara teknis hasilnya sama, tapi konsisten
  dengan konvensi seluruh file lainnya yang selalu eksplisit.

---

## renormalize_x.css — v4.0.0

### Breaking

- `--font-size-base` di mobile dihapus — diganti fluid `clamp()` agar transisi
  halus, bukan lompatan kasar di 768px. Token kini bernama `--base` (konsisten
  dengan semua preset).
- `#eee` hardcode di blockquote → `currentcolor` opacity, supaya bisa hidup
  di dark mode tanpa override.
- `text-rendering: optimizeSpeed` → `optimizeLegibility`. `optimizeSpeed`
  mematikan ligature & kerning — kerugian besar di konteks storytelling.
- `a { text-decoration: none }` dihapus dari reset. Link tanpa underline =
  accessibility violation (WCAG 1.4.1). Untuk menghilangkan underline di nav,
  lakukan di level komponen, bukan di reset global.

### Fix

- `100vh` → `100dvh` (fallback `100vh` tetap ada). `100vh` di mobile Safari
  menyebabkan konten tertutup address bar.
- Heading scale sekarang computed dari `--scale`, bukan hardcode per-level.
  Ganti `--scale` = ganti seluruh hierarki sekaligus.
- Spacing adjacent-sibling selector sekarang pakai `:where()` agar specificity = 0 —
  tidak perlu `!important` untuk override.
- `scroll-behavior: smooth` dipindah ke dalam `prefers-reduced-motion: no-preference` —
  smooth scroll seharusnya opt-in, bukan default yang di-undo.
- `sub/sup`, `abbr[title]`, `b/strong`, `small` — normalize klasik yang missing di v3.

### Tambahan

- `text-wrap: balance` di heading, `pretty` di body text.
- `color-scheme: light dark` untuk native dark mode support.
- `hanging-punctuation` di paragraf.
- `pre`/`code` styling (v3 tidak punya sama sekali).
- `::selection` pakai system colors.
- Print stylesheet dasar.
- `--measure` (max-width) untuk reading container.
- Fluid type scale: font-size smooth dari mobile → desktop.
