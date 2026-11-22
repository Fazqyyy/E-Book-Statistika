# Quarto Template

Repositori sumber terbuka untuk pengembangan buku **Quarto Template** menggunakan **Quarto Book** dan R.

README ini menjelaskan struktur proyek, cara menjalankan buku secara lokal, serta langkah publikasi melalui GitHub Public Repository dan GitHub Pages.

## 1. Struktur folder

```text
ebook-template-quarto/
├── .github/
│   └── workflows/
│       └── publish-quarto.yml
├── assets/
│   ├── style.css
│   └── preamble.tex
├── chapters/
│   ├── bab-1.qmd
│   ├── bab-2.qmd
│   └── bab-3.qmd
├── references/
│   ├── book.bib
│   ├── packages.bib
│   └── referensi.qmd
├── images/
│   ├── Cover_Matematika_Tambang.png
│   ├── Logo_Dsciencelabs_v1.png
│   ├── author/
│   └── chapters/
├── data/
├── R/
├── index.qmd
├── _quarto.yml
├── README.md
├── LICENSE
└── .gitignore
```

### Fungsi folder dan file

| Folder/File | Fungsi |
|---|---|
| `index.qmd` | Halaman awal buku, termasuk informasi dan pengantar penulis |
| `chapters/` | Menyimpan setiap bab buku dalam format `.qmd` |
| `references/` | Menyimpan daftar pustaka BibTeX dan halaman referensi |
| `images/` | Menyimpan sampul, logo, foto penulis, dan gambar pendukung bab |
| `assets/` | Menyimpan CSS dan konfigurasi LaTeX |
| `data/` | Menyimpan dataset pendukung buku |
| `R/` | Menyimpan skrip R pendukung |
| `_quarto.yml` | Konfigurasi utama Quarto Book, urutan bab, dan format keluaran |
| `.github/workflows/` | Konfigurasi otomatisasi build dan publikasi GitHub Pages |
| `.gitignore` | Menentukan file lokal/hasil render yang tidak perlu diunggah ke Git |

## 2. Persiapan perangkat lunak

Pastikan perangkat berikut sudah tersedia:

1. **Quarto**: https://quarto.org/docs/get-started/
2. **R**: https://cran.r-project.org/
3. **Git** (opsional, jika mengunggah melalui Terminal): https://git-scm.com/
4. **LaTeX** untuk menghasilkan PDF, misalnya TinyTeX.

Pasang paket R yang diperlukan:

```r
install.packages(c("knitr", "rmarkdown"))
```

## 3. Menjalankan buku secara lokal

Buka Terminal pada direktori utama proyek, yaitu folder yang berisi `_quarto.yml`.

Render seluruh buku:

```bash
quarto render
```

Render berdasarkan format:

```bash
quarto render --to html
quarto render --to pdf
quarto render --to epub
```

Hasil render disimpan di folder:

```text
_site/
```

Untuk menghasilkan PDF, instal TinyTeX melalui R jika LaTeX belum tersedia:

```r
install.packages("tinytex")
tinytex::install_tinytex()
```

Setelah instalasi selesai, jalankan kembali:

```bash
quarto render --to pdf
```

## 4. Mengatur identitas repositori

Sebelum publikasi, buka file `_quarto.yml` dan ganti alamat berikut:

```yaml
repo-url: https://github.com/USERNAME/REPOSITORY
```

Contoh:

```yaml
repo-url: https://github.com/pakardata1/ebook-template-quarto.git
```

Ganti `USERNAME` dengan nama akun GitHub dan `REPOSITORY` dengan nama repositori yang digunakan.

## 5. Membuat GitHub Public Repository

1. Masuk ke https://github.com/.
2. Klik **New repository**.
3. Isi nama repositori, misalnya `matematika-teknik-pertambangan`.
4. Pada bagian **Visibility**, pilih **Public**.
5. Klik **Create repository**.
6. Ekstrak ZIP proyek Quarto.
7. Unggah seluruh isi folder proyek ke repositori pada branch `main`.

**Penting:** Unggah isi folder proyek, termasuk file tersembunyi `.github`, bukan file ZIP sebagai satu berkas. Pastikan `_quarto.yml` berada di direktori utama repositori.

### Alternatif mengunggah melalui Terminal

Jalankan perintah berikut dari direktori proyek setelah membuat repository kosong di GitHub:

```bash
git init
git add .
git commit -m "Initial Quarto book project"
git branch -M main
git remote add origin https://github.com/pakardata1/ebook-template-quarto.git
git push -u origin main
```

Ganti alamat remote dengan URL repositori Anda.

## 6. Mengaktifkan GitHub Pages

Setelah file proyek berada di GitHub:

1. Buka repositori GitHub.
2. Pilih **Settings**.
3. Pilih **Pages** pada menu samping.
4. Pada bagian **Build and deployment**, pilih **GitHub Actions** sebagai source.
5. Buka tab **Actions**.
6. Periksa workflow bernama **Publish Quarto Book**.
7. Tunggu proses build dan deployment selesai dengan status sukses.

Workflow berada pada:

```text
.github/workflows/publish-quarto.yml
```

Workflow akan menjalankan `quarto render` setiap kali ada perubahan yang di-push ke branch `main`, kemudian menerbitkan hasilnya ke GitHub Pages.

Jika workflow berhasil, alamat buku biasanya berbentuk:

```text
https://pakardata1.github.io/ebook-template-quarto/
```

Alamat final dapat dilihat pada **Settings → Pages**.

## 7. Menambah atau mengubah bab

Untuk menambahkan bab baru:

1. Buat file Quarto baru di folder `chapters/`, misalnya `bab-4.qmd`.
2. Tulis isi bab menggunakan Markdown dan code chunk Quarto.
3. Buka `_quarto.yml`.
4. Tambahkan file tersebut pada daftar `book.chapters`.

Contoh:

```yaml
book:
  chapters:
    - index.qmd
    - chapters/bab-1.qmd
    - chapters/bab-2.qmd
    - chapters/bab-3.qmd
    - chapters/bab-4.qmd
    - references/referensi.qmd
```

Urutan file dalam daftar tersebut menentukan urutan bab pada buku.

## 8. Menambahkan gambar dan sitasi

### Gambar

Simpan gambar di folder `images/` atau subfolder yang sesuai. Gunakan path relatif dari direktori utama proyek.

Contoh:

```markdown
![Contoh ilustrasi](images/chapters/bab-1/ilustrasi.png)
```

### Sitasi

Simpan entri bibliografi dalam file BibTeX di folder `references/`, misalnya `book.bib`.

Contoh sitasi di dalam naskah:

```markdown
Menurut penelitian sebelumnya [@nama-kunci], ...
```

Pastikan kunci sitasi `nama-kunci` tersedia di salah satu file `.bib` yang didaftarkan pada `_quarto.yml`.

## 9. Memperbarui buku di GitHub

Setelah mengedit naskah, gambar, atau kode, simpan perubahan dan unggah kembali ke branch `main`.

Jika menggunakan Git:

```bash
git add .
git commit -m "Update book content"
git push
```

GitHub Actions akan membangun ulang dan menerbitkan versi terbaru secara otomatis.

## 10. Catatan sebelum repositori dibuat publik

- Periksa kembali isi bab, persamaan, gambar, tautan, dan sitasi.
- Pastikan semua gambar, teks, dataset, dan materi pihak ketiga boleh dipublikasikan.
- Jangan mengunggah kata sandi, token akses, API key, kredensial, atau data pribadi.
- Periksa lisensi pada file `LICENSE` dan pastikan lisensi tersebut sesuai dengan hak atas seluruh materi buku.
- Uji hasil `quarto render` secara lokal sebelum publikasi.
- Konversi dari R Markdown/Bookdown ke Quarto perlu diperiksa kembali karena beberapa sintaks atau fitur khusus Bookdown mungkin memerlukan penyesuaian.

## 11. Referensi dokumentasi

- Quarto Books: https://quarto.org/docs/books/
- Quarto Publishing: https://quarto.org/docs/publishing/
- GitHub Pages: https://docs.github.com/pages
- GitHub Actions: https://docs.github.com/actions

---

**Catatan proyek:** File bab dan materi yang disertakan merupakan isi yang dipertahankan dari template sumber. README ini menjelaskan penggunaan dan publikasinya; pemeriksaan akhir terhadap seluruh isi dan keberhasilan render tetap perlu dilakukan sebelum buku diumumkan sebagai publikasi final.
