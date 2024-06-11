### Proyek Akhir dan Ujian

#### Tujuan Pembelajaran
1. Menerapkan semua konsep dan keterampilan yang telah dipelajari selama kursus dalam proyek nyata.
2. Menguji kemampuan dalam menulis, menjalankan, dan memelihara tes otomatis menggunakan Cypress.
3. Mengukur pemahaman peserta melalui ujian tertulis dan praktis.

#### Materi Pembelajaran

##### 1. Proyek Akhir
Proyek akhir ini dirancang untuk mengintegrasikan dan menguji semua konsep dan keterampilan yang telah dipelajari selama kursus. Peserta akan diminta untuk mengerjakan proyek nyata yang mencakup pengujian UI, interaksi dengan elemen, pengujian API, dan praktik terbaik dalam pengujian otomatis.

- **Deskripsi Proyek:**
  - Membuat tes otomatis untuk aplikasi web e-commerce yang mencakup fitur-fitur seperti login, pendaftaran, pencarian produk, menambahkan produk ke keranjang, dan melakukan checkout.

- **Langkah-Langkah Proyek:**
  1. **Setup dan Konfigurasi Cypress:**
     - Buat proyek baru dan konfigurasikan Cypress.
     - Pastikan semua dependensi yang diperlukan terinstal.
  2. **Pengujian Otentikasi:**
     - Tulis tes untuk fitur login dan pendaftaran pengguna.
     - Verifikasi bahwa pengguna dapat masuk dan mendaftar dengan benar.
  3. **Pengujian Pencarian Produk:**
     - Tulis tes untuk fitur pencarian produk.
     - Verifikasi bahwa produk yang dicari muncul dengan benar di hasil pencarian.
  4. **Pengujian Keranjang Belanja:**
     - Tulis tes untuk fitur menambahkan produk ke keranjang belanja.
     - Verifikasi bahwa produk ditambahkan dan jumlah total diperbarui.
  5. **Pengujian Checkout:**
     - Tulis tes untuk fitur checkout.
     - Verifikasi bahwa pengguna dapat menyelesaikan pembelian dan menerima konfirmasi.
  6. **Integrasi Pengujian API:**
     - Tulis tes API untuk endpoint yang relevan seperti pendaftaran pengguna, pencarian produk, dan checkout.
     - Integrasikan tes API dengan tes UI.
  7. **Penggunaan Praktik Terbaik:**
     - Gunakan custom commands, aliases, dan hooks untuk mengoptimalkan tes.
     - Implementasikan strategi untuk menangani flaky tests.
  8. **Laporan dan Analisis:**
     - Integrasikan Cypress Dashboard untuk melacak hasil tes.
     - Gunakan laporan untuk menganalisis dan memperbaiki tes yang gagal.

- **Contoh Proyek:**
  ```javascript
  describe('Proyek Akhir E-Commerce', () => {
    before(() => {
      cy.visit('https://example-ecommerce.com')
    })

    it('Mendaftar pengguna baru', () => {
      cy.visit('/register')
      cy.get('input[name="first_name"]').type('John')
      cy.get('input[name="last_name"]').type('Doe')
      cy.get('input[name="email"]').type('john.doe@example.com')
      cy.get('input[name="password"]').type('password123')
      cy.get('input[name="confirm_password"]').type('password123')
      cy.get('button[type="submit"]').click()
      cy.contains('Pendaftaran berhasil')
    })

    it('Melakukan login pengguna', () => {
      cy.visit('/login')
      cy.get('input[name="email"]').type('john.doe@example.com')
      cy.get('input[name="password"]').type('password123')
      cy.get('button[type="submit"]').click()
      cy.contains('Login berhasil')
    })

    it('Mencari produk dan menambah ke keranjang', () => {
      cy.get('input[name="search"]').type('Laptop{enter}')
      cy.contains('Laptop Terbaik').click()
      cy.get('button.add-to-cart').click()
      cy.contains('Produk telah ditambahkan ke keranjang')
    })

    it('Melakukan checkout', () => {
      cy.visit('/cart')
      cy.get('button.checkout').click()
      cy.get('input[name="address"]').type('Jl. Contoh No. 123')
      cy.get('button[type="submit"]').click()
      cy.contains('Pembelian berhasil')
    })
  })
  ```

##### 2. Ujian
Ujian terdiri dari dua bagian: ujian tertulis dan ujian praktis. Ujian ini dirancang untuk mengukur pemahaman dan keterampilan peserta dalam menggunakan Cypress untuk pengujian otomatis.

- **Ujian Tertulis:**
  - Pertanyaan tentang konsep dasar Cypress, praktik terbaik, dan studi kasus yang telah dibahas selama kursus.
  - Contoh Pertanyaan:
    - Jelaskan manfaat menggunakan custom commands di Cypress.
    - Bagaimana cara menangani flaky tests di Cypress?
    - Apa perbedaan antara `cy.get()` dan `cy.contains()`?

- **Ujian Praktis:**
  - Peserta diminta untuk menyelesaikan serangkaian tugas pengujian menggunakan Cypress.
  - Tugas meliputi penulisan tes untuk fitur tertentu, memverifikasi hasil tes, dan memperbaiki tes yang gagal.
  - Contoh Tugas:
    - Tulis tes untuk fitur logout pengguna.
    - Perbaiki tes yang gagal karena elemen tidak ditemukan.
    - Integrasikan pengujian API untuk endpoint pencarian produk dengan tes UI.

#### Aktivitas Pembelajaran
1. **Diskusi Kelas: Proyek Akhir dan Persiapan Ujian**
   - Diskusikan persiapan untuk proyek akhir dan ujian.
   - Bagikan tips dan strategi untuk menyelesaikan proyek dan ujian dengan sukses.

2. **Praktikum: Penyelesaian Proyek Akhir**
   - Bekerja dalam kelompok atau individu untuk menyelesaikan proyek akhir.
   - Mentor akan memberikan bimbingan dan masukan selama pengerjaan proyek.

3. **Simulasi Ujian:**
   - Lakukan simulasi ujian tertulis dan praktis untuk mempersiapkan peserta.
   - Berikan umpan balik dan diskusikan hasil simulasi.

4. **Presentasi Proyek Akhir:**
   - Peserta mempresentasikan proyek akhir mereka di depan kelas.
   - Diskusi dan tanya jawab mengenai tantangan dan solusi yang ditemukan selama pengerjaan proyek.

#### Referensi
1. [Dokumentasi Resmi Cypress](https://docs.cypress.io/)
2. [Cypress Blog](https://www.cypress.io/blog)
3. Buku: *End-to-End Testing with Cypress* oleh Waweru Mwaura
4. [Video Tutorial Cypress di YouTube](https://www.youtube.com/c/CypressIo)
5. Artikel dan panduan dari komunitas Cypress

---

Materi ini diharapkan dapat memberikan kesempatan bagi peserta untuk menerapkan semua yang telah mereka pelajari dalam konteks nyata, serta mengukur pemahaman mereka melalui ujian. Dengan proyek akhir dan ujian ini, peserta akan lebih siap untuk menggunakan Cypress dalam proyek pengujian mereka sendiri dan mengatasi tantangan yang mungkin muncul.
