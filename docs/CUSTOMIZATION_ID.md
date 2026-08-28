# Panduan Customization Svara & Aruna

Dokumen ini menjelaskan cara mengganti isi, foto, musik, tautan, dan tampilan website undangan pernikahan. Project menggunakan React + TypeScript + Vite. Sebagian besar perubahan konten cukup dilakukan pada satu file konfigurasi agar data tidak tersebar di banyak komponen.

## Struktur file penting

| Kebutuhan | File atau lokasi |
|---|---|
| Data pasangan, tanggal, venue, rekening, dan copy utama | `client/src/pages/Home.tsx` pada objek `CONFIG` |
| Foto galeri dan foto hero | `client/src/pages/Home.tsx` pada array `gallery` dan style `.hero-photo` / `.event-image` |
| Warna, font, layout, navigasi, dan responsive behavior | `client/src/index.css` |
| Judul tab browser dan metadata | `client/index.html` |
| Catatan arah desain | `ideas.md` |

> **Catatan penting:** Jangan mengubah `server/` untuk customization tampilan. Project ini adalah frontend statis.

## Persiapan lokal

Pastikan Node.js dan pnpm tersedia, kemudian jalankan perintah berikut dari root project:

```bash
pnpm install
pnpm dev
```

Buka URL yang diberikan oleh Vite. Untuk memeriksa sebelum disimpan ke repository, jalankan:

```bash
pnpm check
pnpm build
```

Kedua perintah tersebut harus selesai tanpa error TypeScript maupun error build.

## 1. Mengganti data pasangan dan acara

Buka `client/src/pages/Home.tsx`, lalu cari objek `CONFIG` di bagian atas file. Ganti nilai yang berada di antara tanda kutip. Contoh konfigurasi:

```ts
const CONFIG = {
  couple: "Svara & Aruna",
  shortNames: "Svara · Aruna",
  guestFallback: "Tamu undangan",
  dateLabel: "Sabtu, 24 Oktober 2026",
  eventDate: "2026-10-24T16:00:00+07:00",
  venue: "Pendopo Amerta",
  address: "Jl. Prawirotaman No. 28, Yogyakarta",
  mapsUrl: "https://maps.google.com/?q=Pendopo+Amerta+Yogyakarta",
  story: "Tuliskan cerita singkat pasangan di sini.",
  bank: "Bank Mandiri",
  account: "1400 8821 771",
  recipient: "Svara Prameswari",
  calendarUrl: "https://calendar.google.com/calendar/render?...",
};
```

`eventDate` harus menggunakan format ISO dengan timezone. Untuk WIB, gunakan suffix `+07:00`. Contoh `2027-05-15T16:00:00+07:00`. Countdown akan menghitung mundur menuju tanggal tersebut dan berhenti di nol setelah acara berlangsung.

Nilai `dateLabel` adalah teks yang terlihat oleh tamu. Nilai `eventDate` dipakai untuk perhitungan countdown, sehingga keduanya perlu diperbarui bersama-sama.

## 2. Personalisasi nama tamu

Website membaca nama tamu dari parameter URL `to`. Contoh:

```text
https://domain-anda.manus.space/?to=Bapak%20dan%20Ibu%20Santoso
```

Spasi perlu di-encode menjadi `%20` atau dibuat menggunakan fungsi URL encoder. Jika parameter `to` tidak ada, website menggunakan nilai `guestFallback`.

Untuk membuat banyak tautan undangan, pertahankan satu website yang sama dan buat URL berbeda untuk setiap tamu. Hindari menulis nama tamu langsung ke source code karena nama tersebut dapat tampil kepada semua pengunjung.

## 3. Mengganti foto galeri

Array `gallery` berisi enam foto. Setiap item memiliki caption dan URL gambar:

```ts
const gallery = [
  ["Caption foto pertama", "https://alamat-gambar-anda/foto-01.jpg"],
  ["Caption foto kedua", "https://alamat-gambar-anda/foto-02.jpg"],
];
```

Pertahankan minimal enam item agar komposisi gallery tetap seimbang. Gunakan gambar yang sudah dioptimalkan untuk web, idealnya WebP atau JPEG dengan lebar sekitar 1200–1800px. Setiap foto wajib memiliki caption yang jelas karena caption juga digunakan sebagai `alt` text pada gambar dan ditampilkan di lightbox.

Untuk deployment Manus, jangan menaruh file foto besar di `client/public/` atau `client/src/assets/`. Simpan asset besar di penyimpanan asset web project, lalu gunakan URL permanen yang diberikan sistem. Jangan gunakan path lokal seperti `/home/ubuntu/...` di JSX.

Foto hero dan event saat ini menggunakan URL langsung di CSS. Cari selector berikut di `client/src/index.css` dan ganti URL di dalam `url(...)`:

```css
.hero-photo { background: ... url('URL_FOTO_HERO') center/cover; }
.event-image { background: url('URL_FOTO_ACARA') center/cover; }
```

Pastikan teks yang diletakkan di atas foto tetap memiliki kontras. Jika foto baru lebih terang, pertahankan atau perkuat overlay gelap pada `.hero-photo`.

## 4. Mengganti musik ambient

Elemen audio berada di `client/src/pages/Home.tsx`:

```tsx
<audio
  ref={audio}
  loop
  preload="auto"
  src="URL_FILE_MP3"
/>
```

Ganti `src` dengan URL MP3 yang dapat diakses publik atau URL asset permanen project. Gunakan file audio yang sudah dikompresi dengan baik dan pastikan Anda memiliki hak penggunaan musik tersebut.

Browser sering memblokir autoplay bersuara sebelum ada interaksi pengguna. Website sudah mencoba autoplay setelah tombol `Buka Undangan` ditekan dan menyediakan kontrol `Musik on` / `Musik off`. Karena itu, kegagalan autoplay tidak boleh dianggap sebagai error aplikasi.

## 5. Mengganti rekening dan tanda kasih

Ubah properti berikut pada `CONFIG`:

```ts
bank: "Nama bank atau e-wallet",
account: "Nomor rekening atau akun",
recipient: "Nama penerima",
```

Tombol salin rekening membaca nilai `account` secara langsung. Setelah nilai diganti, tidak diperlukan perubahan tambahan pada komponen.

## 6. Mengubah Google Maps dan Google Calendar

`mapsUrl` dipakai oleh tombol petunjuk arah. `calendarUrl` dipakai oleh tombol simpan ke kalender. Buat URL tersebut menggunakan alamat dan waktu acara yang benar. Tautan eksternal sudah menggunakan `target="_blank"` dan `rel="noreferrer"`.

Untuk Google Calendar, pastikan waktu pada URL sesuai dengan timezone acara. Jika Anda membuat URL secara manual, verifikasi hasilnya dengan membuka tautan dalam browser sebelum membagikannya.

## 7. Mengubah warna dan tipografi

Variabel warna utama berada di awal `client/src/index.css`:

```css
:root {
  --ink: #241c19;
  --paper: #efe6d7;
  --paper-light: #f7f1e7;
  --clay: #cf9c80;
  --copper: #b86b4b;
}
```

Arah desain saat ini adalah **Modern Javanese Editorial**. `--copper` adalah aksen identitas utama untuk seal, garis registrasi, angka bab, link, dan tombol. Jika mengganti palette, cek seluruh pasangan foreground/background agar teks tetap terbaca.

Font diimpor dari Google Fonts pada baris awal CSS. Sistem menggunakan Cormorant Garamond untuk display text dan DM Sans untuk label serta body text. Jangan mengganti hanya satu font tanpa mengecek kembali tinggi baris, ukuran heading, dan breakpoint mobile.

## 8. Mengubah teks dan copy

Copy utama dapat diubah langsung pada JSX setelah data `CONFIG`, misalnya headline hero, label acara, teks RSVP, dan kalimat footer. Pertahankan prinsip copy saat ini: singkat, hangat, puitis, dan tidak generik.

Pesan guestbook tidak disimpan ke server. Pada project statis ini, pesan disimpan di `localStorage` browser masing-masing pengunjung. Artinya pesan tidak otomatis terlihat lintas perangkat dan dapat hilang jika data browser dihapus. Jangan mengisi array guestbook dengan pesan contoh atau testimoni palsu.

## 9. Mengubah navigasi

Navigasi section berada pada elemen `<nav className="bottom-nav">` dan identitas pasangan berada pada `<header className="topbar">`. Link menggunakan anchor ID:

```tsx
<a href="#story">Cerita</a>
<a href="#event">Acara</a>
<a href="#gallery">Galeri</a>
<a href="#rsvp">RSVP</a>
<a href="#gift">Tanda kasih</a>
```

Jika menambah section baru, tambahkan `id` pada section tersebut dan link yang sesuai di `.bottom-nav`. Pertahankan padding atas dan bawah pada `.site` agar header atas dan navigasi bawah tidak menutupi konten.

## 10. Checklist sebelum publish

| Pemeriksaan | Yang perlu dipastikan |
|---|---|
| Data | Nama, tanggal, timezone, venue, alamat, rekening, dan link sudah final |
| Tamu | URL `?to=` bekerja dan fallback tetap masuk akal |
| Foto | Semua foto tampil, memiliki caption, dan tidak memakai path lokal |
| RSVP | Form memiliki nama, status kehadiran, pesan, dan state sukses |
| Guestbook | Tidak ada pesan seed atau testimoni buatan |
| Navigasi | Header pasangan tetap di atas dan menu section sticky di bawah |
| Mobile | Uji minimal 375×812 dan pastikan tidak ada horizontal overflow yang tidak diinginkan |
| Audio | Tombol musik tetap berfungsi walaupun autoplay diblokir browser |
| Build | `pnpm check` dan `pnpm build` berhasil |

## 11. Workflow GitHub

Setelah perubahan selesai, lihat status file dan diff terlebih dahulu:

```bash
git status
git diff -- docs/CUSTOMIZATION_ID.md
```

Commit dokumentasi dengan pesan yang jelas:

```bash
git add docs/CUSTOMIZATION_ID.md
git commit -m "docs: add Indonesian customization guide"
```

Kemudian push ke branch utama repository:

```bash
git push user_github main
```

Repository yang terhubung saat dokumen ini dibuat adalah `alpharka/08-28-svara-aruna-a`. Periksa halaman repository untuk memastikan file muncul pada folder `docs/`.

> Jangan melakukan force push atau menghapus commit remote tanpa konfirmasi eksplisit. Jika ada perubahan remote yang belum ada di local, sinkronkan dan selesaikan konflik secara hati-hati sebelum melakukan push.

## Ringkasan perubahan tercepat

Untuk personalisasi dasar, biasanya cukup mengubah tiga lokasi: objek `CONFIG` untuk data acara, array `gallery` untuk foto, dan dua URL background pada `index.css` untuk hero serta foto acara. Setelah itu jalankan `pnpm check` dan `pnpm build`, buka preview pada desktop dan mobile, lalu simpan perubahan ke GitHub.
