# Caption Langsung

Aplikasi web yang menangkap audio dari tab atau layar (misalnya Zoom, Google Meet, Teams), mengubahnya menjadi teks secara langsung, dan menerjemahkannya bila perlu.

## Cara kerja

1. `getDisplayMedia` menangkap audio dari tab atau layar yang dibagikan.
2. Deteksi jeda sederhana (berbasis volume) memotong audio per kalimat.
3. Whisper (via transformers.js) mentranskripsi di browser, memakai WebGPU jika tersedia.
4. Terjemahan lewat API MyMemory (gratis, tanpa API key).

Audio tidak dikirim ke server mana pun. Hanya teks hasil transkripsi yang dikirim ke MyMemory saat terjemahan aktif.

## Jendela mengambang

Tombol **Jendela mengambang** memindahkan caption ke jendela kecil yang selalu di atas aplikasi lain (Document Picture-in-Picture API, Chrome/Edge 116+).

- Ukuran kecil: hanya menampilkan caption terakhir.
- Diperbesar (tarik sudut jendela): teks asli di kiri, terjemahan di kanan.

Tombol ini harus ditekan setelah audio mulai dibagikan, karena browser meminta klik langsung dari pengguna untuk membuka jendela.

## Menjalankan

Buka lewat `http://localhost` atau HTTPS, karena `getDisplayMedia` tidak jalan dari `file://`.

```bash
cd live-caption
python -m http.server 8000
```

Lalu buka `http://localhost:8000` di Chrome atau Edge.

## Deploy ke GitHub Pages

Push folder ini ke repo, lalu Settings → Pages → pilih branch `main` dan folder root.

## Catatan

- Chrome/Edge: pilih tab dan centang "Bagikan audio tab". Di Windows, memilih layar penuh juga bisa membagikan audio sistem.
- Firefox dan Safari tidak mendukung audio dari `getDisplayMedia`.
- Unduhan model pertama sekitar puluhan MB, setelah itu tersimpan di cache browser.
- Whisper kadang salah di nama orang dan istilah teknis. Pakai model Base untuk akurasi lebih baik.
- Beberapa perusahaan melarang alat bantu saat wawancara. Cek aturannya dulu.
