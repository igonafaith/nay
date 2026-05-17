# Nay Normalize CSS

Reset dan normalize CSS dengan lima preset tipografi untuk berbagai konteks konten.
Dirancang agar keterbacaan, aksesibilitas, dan responsivitas menjadi *default*.

**Info**: Reset + Normalize + Preset Asumsi Font dan Setting lainnya diimport terpisah.

---

## Struktur File

```
renormalize.css           — standalone reset (utility-first, tanpa opini heading)
combination/
  renormalize_x.css       — reset + opinionated defaults (dipakai bersama preset)
preset/
  re_dev.css              — developer / teknikal
  re_mixed.css            — general purpose / konten campuran
  re_news.css             — berita / jurnalistik
  re_story.css            — narasi / cerita panjang
  re_wiki.css             — ensiklopedis / referensi
```

---

## ⚠ Pilih Satu Reset

**Jangan gunakan `renormalize.css` dan `renormalize_x.css` bersamaan.**
Keduanya mendefinisikan heading scale dan list-style dengan cara yang berbeda —
source order yang menang, hasilnya tidak terduga.

| File | Kapan pakai |
|---|---|
| `renormalize.css` | Proyek dengan design-system sendiri. Reset bersih, heading tanpa opini. |
| `renormalize_x.css` | Proyek yang memakai salah satu preset di bawah ini. |

---

## Cara Import

**Dengan preset** (paling umum):

```html
<link rel="stylesheet" href="/combination/renormalize_x.css">
<link rel="stylesheet" href="/preset/re_story.css">
```

**Standalone** (design-system sendiri):

```html
<link rel="stylesheet" href="/renormalize.css">
```

> Preset dirancang untuk dipakai bersama `renormalize_x.css`.
> Jangan import `renormalize.css` + `renormalize_x.css` sekaligus.

---

## Preset

Semua preset diaplikasikan ke elemen **container**, bukan global.

**`<body>` vs `<article>`** — mengaplikasikan preset ke `<body>` akan membatasi lebar
seluruh halaman (`max-width + margin-inline: auto`). Cocok untuk halaman full-prose
sederhana. Untuk layout dengan header/nav/footer full-width, gunakan `<article>`:

```html
<body>
  <header>...</header>
  <main>
    <article class="preset-story">...</article>
  </main>
</body>
```

Override font per-preset:

```css
.preset-news {
  --font-heading: "Playfair Display", serif;
  --font-body:    "Source Serif 4",   serif;
}
```

### `re_dev.css` — Developer / Teknikal

Karakteristik: code-first, dense-but-clear, functional.\
Referensi: Stripe Docs, Go Docs, MDN.

### `re_mixed.css` — General Purpose

Karakteristik: balanced, versatile, modern. Bisa menampung teks, gambar, video,
code, dan quotes tanpa satu pun yang terasa asing.\
Referensi: Notion, blog modern, landing page.

### `re_news.css` — Berita / Jurnalistik

Karakteristik: scannable, headline-driven, compact, efisien.\
Referensi: Reuters, NYT, Kompas.

### `re_story.css` — Narasi / Cerita Panjang

Karakteristik: generous whitespace, literary, immersive reading.\
Referensi: Medium, Longreads, The New Yorker.

> **Drop cap** bersifat opt-in. Tambahkan class `.drop-cap` ke paragraf yang
> diinginkan — tidak otomatis diterapkan ke paragraf pertama.

### `re_wiki.css` — Ensiklopedis / Referensi

Karakteristik: dense, hierarchical, scannable, reference-grade.\
Referensi: Wikipedia, MDN, Arch Wiki.

---

## Browser Support

Preset memakai **native CSS nesting** ([Baseline 2023](https://caniuse.com/css-nesting)).
Browser minimum: Chrome 112+, Firefox 117+, Safari 16.5+.

Jika perlu support browser lebih lama, gunakan PostCSS dengan
[`postcss-nesting`](https://github.com/csstools/postcss-plugins/tree/main/plugins/postcss-nesting)
untuk mengompilasi nesting ke CSS biasa.

> `renormalize_x.css` sendiri sudah konservatif (fallback `100vh`, fallback `color-mix()`).
> Preset sengaja modern-only karena bergantung pada nesting native.

---

Lihat [CHANGELOG](CHANGELOG) untuk riwayat perubahan lengkap.
