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

## Preset

Semua preset diaplikasikan ke elemen **container**, bukan global:

```html
<body data-preset="story">         <!-- seluruh halaman -->
<article class="preset-news">      <!-- hanya artikel ini -->
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

### `re_wiki.css` — Ensiklopedis / Referensi

Karakteristik: dense, hierarchical, scannable, reference-grade.\
Referensi: Wikipedia, MDN, Arch Wiki.

---

Lihat [CHANGELOG](CHANGELOG.md) untuk riwayat perubahan lengkap.
