### Pengantar Cypress

#### Tujuan Pembelajaran
1. Memahami apa itu Cypress dan bagaimana peranannya dalam pengujian aplikasi web.
2. Mengerti cara menginstal dan mengatur lingkungan Cypress.
3. Menjalankan tes pertama dengan Cypress.

#### Materi Pembelajaran

##### 1. Apa itu Cypress?
Cypress adalah alat pengujian end-to-end modern yang dirancang khusus untuk aplikasi web. Alat ini membantu pengembang dan QA (Quality Assurance) untuk menulis tes yang dapat diandalkan dan mudah dibaca, serta memberikan umpan balik yang cepat dan jelas.

- **Definisi dan Tujuan:** Cypress adalah framework pengujian yang berbasis JavaScript. Cypress dirancang untuk mengatasi berbagai masalah yang sering dihadapi saat menggunakan alat pengujian tradisional seperti Selenium.
- **Kelebihan dan Kekurangan:**
  - *Kelebihan:* Instalasi mudah, debug yang efisien, tes berjalan langsung di browser, integrasi dengan CI/CD, dan dokumentasi yang komprehensif.
  - *Kekurangan:* Terbatas pada pengujian aplikasi web (tidak mendukung aplikasi mobile atau desktop), dukungan terbatas untuk browser selain Chrome dan Firefox.

##### 2. Instalasi Cypress
Untuk memulai menggunakan Cypress, Anda perlu menginstalnya di lingkungan pengembangan Anda.

- **Persyaratan Sistem:** Pastikan Anda memiliki Node.js dan npm terinstal pada sistem Anda.
- **Langkah-langkah Instalasi:**
  - Buka terminal atau command prompt.
  - Jalankan perintah berikut untuk membuat proyek baru (jika belum ada proyek):
    ```bash
    mkdir nama-proyek
    cd nama-proyek
    npm init -y
    ```
  - Instal Cypress dengan perintah:
    ```bash
    npm install cypress --save-dev
    ```
  - Buka Cypress dengan perintah:
    ```bash
    npx cypress open
    ```
 
##### 3. Struktur Proyek Cypress & Konfigurasi Proyek Cypress
Setelah instalasi, Anda perlu melakukan beberapa konfigurasi dasar untuk menyiapkan proyek Cypress Anda.

- **Membuka Cypress:**
  - Buka Cypress untuk pertama kalinya dengan perintah:
    ```bash
    npx cypress open
    ```
  - Cypress akan membuat struktur folder dan file default di dalam proyek Anda.

- **Struktur Folder dan File Cypress:**
  - `cypress/`: Folder utama Cypress yang berisi subfolder untuk tes, fixtures, dan support.
    - `integration/`: Tempat menyimpan file tes.
    - `fixtures/`: Menyimpan data statis yang digunakan dalam tes.
    - `support/`: Menyimpan skrip khusus dan file konfigurasi tambahan.
  - `cypress.json`: File konfigurasi utama Cypress untuk mengatur berbagai pengaturan seperti baseUrl, viewport, dll.

- **Contoh Konfigurasi `cypress.json`:**
  ```json
  {
    "baseUrl": "http://localhost:3000",
    "viewportWidth": 1280,
    "viewportHeight": 720
  }
  ```


##### 4. Menjalankan Tes Pertama dengan Cypress
Membuat dan menjalankan tes pertama Anda di Cypress sangat mudah dan intuitif.

- **Membuat Tes Sederhana:**
  - Buat file baru di dalam folder `integration` dengan nama `first_test.spec.js`.
  - Tambahkan kode berikut untuk mengakses halaman web dan memeriksa elemen:
    ```javascript
    describe('Tes Pertama', () => {
      it('Memuat halaman utama', () => {
        cy.visit('https://example.com')
        cy.contains('Example Domain')
      })
    })
    ```
- **Menjalankan Tes:**
  - Buka Cypress dengan perintah `npx cypress open`.
  - Pilih tes yang telah Anda buat dan jalankan.
  - Lihat hasil tes pada dashboard Cypress yang menunjukkan status tes dan detailnya.

#### Aktivitas Pembelajaran
1. **Diskusi Kelas: Pengantar Cypress**
   - Diskusikan apa itu Cypress, bagaimana perbedaannya dengan alat pengujian lain, serta kelebihan dan kekurangannya.

2. **Praktikum: Instalasi Cypress**
   - Ikuti panduan instalasi Cypress pada komputer masing-masing.
   - Pastikan semua peserta telah berhasil menginstal Cypress dengan benar.

3. **Latihan: Menjalankan Tes Pertama**
   - Buat sebuah tes sederhana menggunakan Cypress yang memverifikasi bahwa halaman web tertentu dapat diakses dan memuat elemen tertentu.
   - Jalankan tes tersebut dan lihat hasilnya pada dashboard Cypress.

4. **Proyek Mini: Eksplorasi Struktur Proyek**
   - Eksplorasi struktur proyek Cypress yang telah diinstal.
   - Identifikasi dan catat fungsi dari berbagai file dan direktori dalam proyek Cypress.

#### Referensi
1. [Dokumentasi Resmi Cypress](https://docs.cypress.io/guides/overview/why-cypress)
2. [Blog Cypress - Pengantar dan Panduan](https://www.cypress.io/blog)
3. Buku: *End-to-End Testing with Cypress* oleh Waweru Mwaura
4. [Video Tutorial Cypress di YouTube](https://www.youtube.com/c/CypressIo)

---

Materi ini diharapkan dapat memberikan dasar yang kuat bagi peserta dalam memahami dan memulai penggunaan Cypress untuk pengujian aplikasi web. Melalui pembelajaran ini, peserta akan memperoleh pengetahuan praktis yang dapat langsung diterapkan dalam proyek pengujian mereka.
