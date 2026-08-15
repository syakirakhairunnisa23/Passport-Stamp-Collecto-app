# AGENTS.md — Autonomous Single-File Vanilla JS Web App & Auto-Deploy Spec

> **Panduan Instruksi AI Agent:** Dokumen ini adalah instruksi operasional standar (*Operating System Prompt & Specification*) bagi AI Agent (Claude Code, Cursor, Windsurf, Copilot, Aider, dll). Isi bagian formulir spesifikasi proyek bertanda `[ ... ]`. Ketika pengguna mengetikkan perintah **`implementasikan`**, jalankan eksekusi dari **Fase 0** hingga **Fase Selesai** secara otonom tanpa henti.

---

## 1. SPESIFIKASI PROYEK (Isi Bagian Bertanda `[...]`)

```yaml
================================================================================
INFORMASI DASAR PROYEK
================================================================================
Nama Proyek          : [Passport Stamp Collector]
Nama Repository GitHub: [Passport Stamp Collecto-app]
Tujuan Proyek        : [hiburan]
Target Audiens       : [umum]
Bahasa Aplikasi      : [Indonesia]

================================================================================
DESAIN, TEMA & TAMPILAN
================================================================================
Tema Visual & Mood   : [Contoh: Modern Clean, Neo-Brutalism, Glassmorphism, Dark Cyberpunk]
Palet Warna Utama    :
  - Primary / Brand  : [Contoh: #4F46E5 / Indigo]
  - Secondary / Accent: [Contoh: #06B6D4 / Cyan]
  - Background Light : [Contoh: #F8FAFC / Slate-50]
  - Background Dark  : [Contoh: #0F172A / Slate-900]
  - Text Primary     : [Contoh: #1E293B / Slate-800]
Tipografi / Font     : [System UI / Inter / Plus Jakarta Sans via Google Fonts]
Dukungan Tema        : [Wajib: Dark Mode & Light Mode toggle otomatis/manual]
Responsivitas        : [Mobile First (320px), Tablet (768px), Desktop (1024px+)]

================================================================================
FITUR & SPESIFIKASI FUNGSIONAL
================================================================================
Fitur Utama 1        : [Jelaskan fitur 1 secara detail, alur input/output]
Fitur Utama 2        : [Jelaskan fitur 2 secara detail, interaktivitas]
Fitur Utama 3        : [Jelaskan fitur 3 secara detail, logika bisnis]
Fitur Tambahan       : [Isi fitur pelengkap, misal: Export CSV/JSON, Import, Search, Filter]
Manajemen State/Data : [LocalStorage / SessionStorage / IndexedDB / Memory State]
Struktur Data Utama  : [Tuliskan format JSON schema / object model yang digunakan]

================================================================================
INTEGRASI & EXTERNAL ASSETS (OPSIONAL)
================================================================================
External CDN Libs    : [Contoh: Lucide Icons CDN, Tailwind CDN (jika perlu) / Murni Vanilla CSS]
External API (Mock/Live): [Contoh: Local Mock Data / Free Public API]
SEO & Meta Tags      :
  - Meta Title       : [Judul untuk browser & search engine]
  - Meta Description : [Deskripsi 150 karakter untuk SEO]
  - Favicon SVG      : [Inline SVG Favicon sesuai logo]

================================================================================
KONFIGURASI GITHUB & DEPLOYMENT
================================================================================
GitHub Username / Org: [Isi username GitHub Anda, contoh: octocat]
Visibilitas Repo     : [public / private]
Metode Deploy Pages  : [GitHub Pages via Branch 'main' root '/' ATAU GitHub Actions]
Domain Kustom (Ops.) : [Kosongkan jika menggunakan *.github.io/repo-name]
```

---

## 2. ATURAN ARSITEKTUR & PRINSIP KODE (*Single-File Rule*)

1. **Prinsip Single-File (`index.html`)**:
   - Seluruh markup HTML5, styling CSS, dan logika JavaScript Vanilla **WAJIB** berada dalam satu file tunggal: `index.html`.
   - Tidak memerlukan *build tools* (No Node.js, No Vite, No Webpack). File harus dapat langsung dibuka via `double-click` / browser standar atau live server statis.
2. **CSS Best Practices**:
   - Gunakan CSS Variables (`:root`) untuk tokens warna, spacing, shadows, radius, dan dark mode switcher.
   - Wajib *CSS Reset* modern dan *Box Sizing: border-box*.
   - Gunakan CSS Flexbox dan CSS Grid modern.
   - Tambahkan mikro-interaksi: transitions (150ms-250ms ease), hover states, active states, focus-visible ring untuk aksesibilitas (A11y).
3. **JavaScript Vanilla (ES6+) Best Practices**:
   - Gunakan mode ketat (`'use strict';`).
   - Arsitektur berbasis modul fungsional atau Object Literal (*Clean Architecture*):
     - `State Management`: Single source of truth dengan fungsi `render()` / reaktif sederhana.
     - `DOM Elements Cache`: Simpan referensi DOM di awal.
     - `Event Listeners`: Gunakan *event delegation* yang efisien.
     - `Storage Layer`: Helper fungsi `loadState()` dan `saveState()` dengan *try-catch handling*.
   - Hindari manipulasi `innerHTML` yang rentan XSS terhadap input pengguna; prioritaskan `textContent` atau sanitasi elemen DOM.
4. **Resiliensi & Error Handling**:
   - Berikan feedback UI visual (toast notification / inline alert) untuk setiap aksi pengguna (sukses simpan, validasi error, konfirmasi hapus).
   - Tampilkan *empty state* yang menarik jika belum ada data.

---

## 3. ALUR PROTOKOL EKSEKUSI OTONOM (*One-Prompt Trigger*)

Ketika pengguna mengirimkan prompt:
```text
implementasikan
```

AI Agent **HARUS** secara otomatis dan berurutan menjalankan fase-fase berikut tanpa meminta konfirmasi perantara kecuali terjadi error fatal:

```
┌────────────────────────────────────────────────────────┐
│  FASE 0: Validasi Spesifikasi & Persiapan Struktur     │
└──────────────────────────┬─────────────────────────────┘
                           ▼
┌────────────────────────────────────────────────────────┐
│  FASE 1: Generasi Lengkap 'index.html' (100% Siap)     │
└──────────────────────────┬─────────────────────────────┘
                           ▼
┌────────────────────────────────────────────────────────┐
│  FASE 2: Verifikasi & Audit Kualitas Kode              │
└──────────────────────────┬─────────────────────────────┘
                           ▼
┌────────────────────────────────────────────────────────┐
│  FASE 3: Otomatisasi Git, GitHub Repo & GitHub Pages   │
└──────────────────────────┬─────────────────────────────┘
                           ▼
┌────────────────────────────────────────────────────────┐
│  FASE 4: Laporan Deployment & Link Live Website        │
└────────────────────────────────────────────────────────┘
```

---

## 4. RINCIAN EKSEKUSI TIAP FASE

### 🚀 FASE 0 — Validasi Spesifikasi & Persiapan
1. Baca seluruh parameter di bagian **1. SPESIFIKASI PROYEK**.
2. Jika ada titik-titik `[...]` yang belum diisi atau bersifat opsional, isi secara cerdas dengan *best practice* industri yang selaras dengan tema aplikasi.
3. Buat direktori kerja lokal proyek jika belum ada.

---

### 💻 FASE 1 — Generasi File Tunggal `index.html`
Tulis seluruh file `index.html` dengan struktur baku:

```html
<!DOCTYPE html>
<html lang="id" class="light">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>[Nama Proyek] — [Tagline]</title>
  <meta name="description" content="[Meta Description]">
  
  <!-- Favicon SVG Inline Data URI -->
  <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>🚀</text></svg>">
  
  <!-- Google Fonts (jika diperlukan) -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  
  <!-- CSS Single File -->
  <style>
    /* ============================================================
       CSS VARIABLES & THEME TOKENS
       ============================================================ */
    :root {
      --font-main: 'Plus Jakarta Sans', system-ui, -apple-system, sans-serif;
      --bg-body: #f8fafc;
      --bg-surface: #ffffff;
      --bg-surface-elevated: #f1f5f9;
      --border-color: #e2e8f0;
      --text-main: #0f172a;
      --text-muted: #64748b;
      --color-primary: #4f46e5;
      --color-primary-hover: #4338ca;
      --color-primary-light: #eef2ff;
      --color-accent: #06b6d4;
      --color-danger: #ef4444;
      --color-success: #10b981;
      --shadow-sm: 0 1px 2px 0 rgb(0 0 0 / 0.05);
      --shadow-md: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
      --shadow-lg: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
      --radius-sm: 6px;
      --radius-md: 10px;
      --radius-lg: 16px;
      --transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
    }

    html.dark {
      --bg-body: #0b0f19;
      --bg-surface: #111827;
      --bg-surface-elevated: #1f2937;
      --border-color: #374151;
      --text-main: #f9fafb;
      --text-muted: #9ca3af;
      --color-primary: #6366f1;
      --color-primary-hover: #4f46e5;
      --color-primary-light: #1e1b4b;
      --shadow-sm: 0 1px 2px 0 rgb(0 0 0 / 0.5);
      --shadow-md: 0 4px 6px -1px rgb(0 0 0 / 0.5);
      --shadow-lg: 0 10px 15px -3px rgb(0 0 0 / 0.6);
    }

    /* CSS Reset & General Styling */
    *, *::before, *::after {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: var(--font-main);
      background-color: var(--bg-body);
      color: var(--text-main);
      line-height: 1.6;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      transition: background-color 0.3s ease, color 0.3s ease;
    }

    /* [KOMPONEN CSS LENGKAP DIIMPLEMENTASIKAN SECARA PENUH DI SINI] */
  </style>
</head>
<body>
  <!-- HEADER & NAVIGATION -->
  <header>
    <!-- Logo, Judul, Theme Toggle Switcher -->
  </header>

  <!-- MAIN APP CONTENT -->
  <main id="app">
    <!-- UI Komponen sesuai spesifikasi fitur -->
  </main>

  <!-- NOTIFICATION TOAST CONTAINER -->
  <div id="toast-container" aria-live="polite" aria-atomic="true"></div>

  <!-- FOOTER -->
  <footer>
    <p>&copy; <span id="year"></span> [Nama Proyek]. Dibuat dengan Vanilla HTML, CSS, dan JavaScript.</p>
  </footer>

  <!-- JAVASCRIPT LOGIC -->
  <script>
    'use strict';

    /**
     * [NAMA_PROYEK] - Core JavaScript Application
     */
    const App = {
      // 1. STATE MANAGEMENT
      state: {
        theme: localStorage.getItem('app_theme') || 'light',
        items: [],
        filter: 'all',
        searchQuery: ''
      },

      // 2. DOM CACHE
      dom: {},

      // 3. INITIALIZATION
      init() {
        this.cacheDOM();
        this.loadState();
        this.applyTheme();
        this.bindEvents();
        this.render();
      },

      // 4. CACHE DOM ELEMENTS
      cacheDOM() {
        this.dom.html = document.documentElement;
        this.dom.app = document.getElementById('app');
        this.dom.toastContainer = document.getElementById('toast-container');
        this.dom.yearSpan = document.getElementById('year');
        if (this.dom.yearSpan) this.dom.yearSpan.textContent = new Date().getFullYear();
      },

      // 5. STORAGE HELPERS
      loadState() {
        try {
          const raw = localStorage.getItem('[NAMA_PROYEK_KEY]_data');
          if (raw) this.state.items = JSON.parse(raw);
        } catch (e) {
          console.error('Failed to load state from localStorage:', e);
          this.state.items = [];
        }
      },

      saveState() {
        try {
          localStorage.setItem('[NAMA_PROYEK_KEY]_data', JSON.stringify(this.state.items));
        } catch (e) {
          console.error('Failed to save state to localStorage:', e);
          this.showToast('Gagal menyimpan data ke penyimpanan lokal!', 'error');
        }
      },

      // 6. THEME HANDLER
      applyTheme() {
        if (this.state.theme === 'dark') {
          this.dom.html.classList.add('dark');
        } else {
          this.dom.html.classList.remove('dark');
        }
        localStorage.setItem('app_theme', this.state.theme);
      },

      toggleTheme() {
        this.state.theme = this.state.theme === 'light' ? 'dark' : 'light';
        this.applyTheme();
      },

      // 7. TOAST NOTIFICATION UTILITY
      showToast(message, type = 'info') {
        const toast = document.createElement('div');
        toast.className = `toast toast-${type}`;
        toast.textContent = message;
        this.dom.toastContainer.appendChild(toast);
        setTimeout(() => toast.classList.add('show'), 10);
        setTimeout(() => {
          toast.classList.remove('show');
          setTimeout(() => toast.remove(), 300);
        }, 3000);
      },

      // 8. EVENT BINDINGS & LOGIKA FITUR LENGKAP
      bindEvents() {
        // Event listeners untuk UI, input form, filter, search, CRUD actions
      },

      // 9. RENDER PIPELINE
      render() {
        // Rendering komponen dinamis ke DOM secara efisien
      }
    };

    // Bootstrap app on DOM Ready
    document.addEventListener('DOMContentLoaded', () => App.init());
  </script>
</body>
</html>
```

---

### 🛡️ FASE 2 — Verifikasi & Audit Kualitas
1. Periksa tidak ada error sintaksis HTML/CSS/JS.
2. Periksa konsistensi ID dan selector event listener.
3. Pastikan tidak ada *hardcoded placeholder* dummy `[isi disini]` yang tertinggal pada kode `index.html`.
4. Pastikan fitur *Dark Mode*, *Local Storage Persistence*, dan fungsi responsivitas bekerja mulus.

---

### 🌐 FASE 3 — Otomatisasi Git, GitHub Repo & GitHub Pages

AI Agent menjalankan urutan perintah CLI berikut di terminal:

```bash
# 1. Inisialisasi Git Lokal
git init
git branch -M main

# 2. Buat file .gitignore & README.md minimal
cat << 'EOF' > .gitignore
.DS_Store
Thumbs.db
node_modules/
.env
EOF

cat << 'EOF' > README.md
# [NAMA_PROYEK]

> [TUJUAN_PROYEK]

🌐 **Live Demo:** [https://[GITHUB_USERNAME].github.io/[REPO_NAME]/](https://[GITHUB_USERNAME].github.io/[REPO_NAME]/)

## Fitur Utama
- [Fitur Utama 1]
- [Fitur Utama 2]
- [Fitur Utama 3]
- Single-file Vanilla HTML5, CSS3, & Modern ES6 JavaScript (No Build Tools Required).
- Dark Mode & Responsive Layout.
- Local Storage State Persistence.

## Cara Menjalankan Secara Lokal
Cukup buka file `index.html` di browser favorit Anda atau gunakan server lokal:
\`\`\`bash
# Python simple server
python3 -m http.server 8000
\`\`\`
EOF

# 3. Stage & Commit file awal
git add .
git commit -m "feat: initial release of [NAMA_PROYEK] (single-file vanilla app)"

# 4. Buat Repository di GitHub via GitHub CLI (gh) & Push
# Catatan: Memerlukan user yang sudah login (`gh auth status`)
gh repo create "[REPO_NAME]" --[VISIBILITAS] --source=. --remote=origin --push --description "[TUJUAN_PROYEK]"

# 5. Aktifkan Fitur GitHub Pages secara otomatis via GitHub REST API
gh api   --method POST   -H "Accept: application/vnd.github+json"   -H "X-GitHub-Api-Version: 2022-11-28"   /repos/[GITHUB_USERNAME]/[REPO_NAME]/pages   -f source='{"branch":"main","path":"/"}' || echo "Pages endpoint configured or already enabled."
```

*(Alternatif: Jika menggunakan GitHub Actions untuk Pages, buat file `.github/workflows/pages.yml` secara otomatis dan push ke main).*

---

### 📊 FASE 4 — Ringkasan & Laporan Selesai

Setelah seluruh proses otomatisasi selesai, tampilkan output terstruktur kepada pengguna:

```markdown
🎉 **Implementasi & Deployment Selesai Berhasil!**

| Informasi | Detail |
|---|---|
| **Nama Proyek** | [NAMA_PROYEK] |
| **Arsitektur** | Single-File Vanilla HTML/CSS/JS (`index.html`) |
| **Repository GitHub** | `https://github.com/[GITHUB_USERNAME]/[REPO_NAME]` |
| **Live URL GitHub Pages** | `https://[GITHUB_USERNAME].github.io/[REPO_NAME]/` |
| **Status Deploy** | Aktif via branch `main` root `/` |

💡 *Catatan:* Peramban memerlukan waktu sekitar 1-3 menit untuk proses build awal GitHub Pages pertama kali.
```

---

## 5. INSTRUKSI TRIGGER CEPAT BAGI PENGGUNA

Untuk memulai proses pengerjaan:
1. Salin template ini ke file `AGENTS.md` di root proyek Anda.
2. Lengkapi form pada bagian **`1. SPESIFIKASI PROYEK`**.
3. Ketikkan perintah:
   ```text
   implementasikan
   ```
4. AI Agent akan langsung membangun aplikasi web single-file `index.html`, membuat repositori di GitHub Anda, dan mengaktifkan GitHub Pages hingga live!
