### Materi Pengantar Cypress untuk 1 SKS

Cypress adalah alat otomatisasi pengujian front-end yang memungkinkan pengembang dan penguji untuk menulis skrip pengujian dalam JavaScript. Materi ini akan mencakup pengenalan dasar Cypress, pengaturan lingkungan, penulisan dan menjalankan tes, serta praktik terbaik dalam pengujian otomatisasi.

#### Struktur Kuliah
- Minggu 1-2: Pengantar Cypress dan Pengaturan Lingkungan
- Minggu 3-4: Dasar-dasar Penulisan Tes dengan Cypress
- Minggu 5-6: Interaksi dengan Elemen dan Formulir
- Minggu 7-8: Pengujian API dengan Cypress
- Minggu 9-10: Praktik Terbaik dan Studi Kasus
- Minggu 11-12: Proyek Akhir dan Ujian

### Minggu 1-2: Pengantar Cypress dan Pengaturan Lingkungan

#### Tujuan Pembelajaran
Pada akhir minggu ini, mahasiswa diharapkan dapat:
1. Memahami apa itu Cypress dan bagaimana fungsinya dalam otomatisasi pengujian.
2. Mengatur lingkungan pengembangan untuk menggunakan Cypress.

#### Materi Pembelajaran

**1.1 Pengantar Cypress**
- **Apa itu Cypress?**
  - Cypress adalah alat pengujian end-to-end (E2E) modern yang dibangun untuk web.
  - Dibuat untuk membuat pengujian web lebih cepat, lebih mudah, dan lebih andal.
  
- **Fitur Utama:**
  - Real-time reloading.
  - Snapshot otomatis selama tes berjalan.
  - Menyediakan debug yang mudah.

**1.2 Instalasi dan Konfigurasi**
- **Persyaratan Sistem:**
  - Node.js versi terbaru.
  - NPM (Node Package Manager) atau Yarn.

- **Langkah-langkah Instalasi:**
  1. **Menginstal Cypress:**
     ```sh
     npm install cypress --save-dev
     ```

  2. **Menjalankan Cypress:**
     ```sh
     npx cypress open
     ```

- **Struktur Proyek Cypress:**
  - Folder `cypress/` berisi:
    - `fixtures/`: Menyimpan data uji.
    - `integration/`: Tempat tes Cypress berada.
    - `plugins/`: Tempat mengonfigurasi atau memperluas Cypress.
    - `support/`: Menyimpan perintah dan konfigurasi global.

**1.3 Menjalankan Tes Pertama**
- **Tes Contoh:**
  - Cypress menyediakan tes contoh yang dapat digunakan untuk memahami dasar-dasar.
  - Menjalankan tes contoh untuk melihat hasilnya.

**1.4 Konfigurasi Cypress**
- **Konfigurasi Dasar:**
  - File `cypress.json` untuk mengatur konfigurasi dasar seperti baseUrl, viewport, dll.
  - Contoh:
    ```json
    {
      "baseUrl": "http://localhost:3000",
      "viewportWidth": 1280,
      "viewportHeight": 720
    }
    ```

#### Aktivitas Pembelajaran

**Diskusi Kelas:**
1. Apa itu Cypress dan mengapa penting dalam pengujian web?
2. Bagaimana Cypress dibandingkan dengan alat pengujian lainnya seperti Selenium?

**Bacaan:**
- Dokumentasi Cypress: [Cypress Documentation](https://docs.cypress.io/)

**Tugas:**
- Instal dan konfigurasi Cypress di mesin lokal.
- Menjalankan tes contoh yang disediakan oleh Cypress dan laporkan hasilnya.

#### Referensi
- [Cypress Official Documentation](https://docs.cypress.io/): Sumber utama untuk belajar Cypress.
- [Cypress GitHub Repository](https://github.com/cypress-io/cypress): Contoh dan proyek komunitas.

---

### Minggu 3-4: Dasar-dasar Penulisan Tes dengan Cypress

#### Tujuan Pembelajaran
Pada akhir minggu ini, mahasiswa diharapkan dapat:
1. Menulis dan menjalankan tes dasar menggunakan Cypress.
2. Memahami konsep dasar assertions dan commands dalam Cypress.

#### Materi Pembelajaran

**3.1 Penulisan Tes Dasar**
- **Struktur Tes:**
  - Menggunakan `describe` dan `it` untuk mengelompokkan dan mendefinisikan tes.
  - Contoh:
    ```js
    describe('Halaman Beranda', () => {
      it('harus memuat dengan benar', () => {
        cy.visit('/');
        cy.contains('Welcome to Cypress!');
      });
    });
    ```

**3.2 Assertions**
- **Apa itu Assertions?**
  - Assertions adalah klaim yang memverifikasi bahwa kondisi tertentu terpenuhi.

- **Assertions Dasar:**
  - `should()`: Memverifikasi bahwa elemen memenuhi kondisi tertentu.
    ```js
    cy.get('h1').should('have.text', 'Welcome to Cypress!');
    ```

**3.3 Commands**
- **Commands Dasar:**
  - `cy.visit()`: Mengunjungi URL.
  - `cy.get()`: Mendapatkan elemen berdasarkan selector.
  - `cy.contains()`: Memeriksa teks dalam elemen.

- **Chaining Commands:**
  - Contoh chaining commands:
    ```js
    cy.get('input[name="email"]').type('example@example.com').should('have.value', 'example@example.com');
    ```

**3.4 Mengatur dan Membersihkan Tes**
- **Hooks:**
  - `before()`, `beforeEach()`, `after()`, `afterEach()` untuk mengatur dan membersihkan tes.
  - Contoh:
    ```js
    beforeEach(() => {
      cy.visit('/');
    });
    ```

#### Aktivitas Pembelajaran

**Diskusi Kelas:**
1. Mengapa assertions penting dalam tes otomatisasi?
2. Bagaimana penggunaan hooks dapat membantu dalam penulisan tes yang lebih terstruktur?

**Bacaan:**
- Dokumentasi Cypress tentang Assertions: [Assertions Documentation](https://docs.cypress.io/guides/references/assertions)
- Dokumentasi Cypress tentang Commands: [Commands Documentation](https://docs.cypress.io/api/table-of-contents)

**Tugas:**
- Menulis tes dasar untuk aplikasi web sederhana, mencakup navigasi, input form, dan verifikasi konten.

#### Referensi
- [Cypress Assertions](https://docs.cypress.io/guides/references/assertions)
- [Cypress API](https://docs.cypress.io/api/table-of-contents)

---

### Minggu 5-6: Interaksi dengan Elemen dan Formulir

#### Tujuan Pembelajaran
Pada akhir minggu ini, mahasiswa diharapkan dapat:
1. Berinteraksi dengan berbagai elemen web menggunakan Cypress.
2. Menulis tes untuk mengisi dan mengirimkan formulir.

#### Materi Pembelajaran

**5.1 Interaksi dengan Elemen Web**
- **Klik Elemen:**
  - Menggunakan `cy.click()` untuk mengklik elemen.
  - Contoh:
    ```js
    cy.get('button').click();
    ```

- **Memasukkan Teks:**
  - Menggunakan `cy.type()` untuk memasukkan teks ke dalam input field.
  - Contoh:
    ```js
    cy.get('input[name="username"]').type('myusername');
    ```

- **Memilih dari Dropdown:**
  - Menggunakan `cy.select()` untuk memilih opsi dari dropdown.
  - Contoh:
    ```js
    cy.get('select').select('option1');
    ```

**5.2 Penanganan Formulir**
- **Mengisi Formulir:**
  - Mengisi input field, textarea, dan elemen form lainnya.
  - Contoh:
    ```js
    cy.get('input[name="email"]').type('example@example.com');
    cy.get('input[name="password"]').type('mypassword');
    ```

- **Mengirimkan Formulir:**
  - Menggunakan `cy.submit()` untuk mengirimkan formulir.
  - Contoh:
    ```js
    cy.get('form').submit();
    ```

- **Verifikasi Pengiriman:**
  - Memastikan formulir dikirimkan dan halaman berubah sesuai dengan ekspektasi.
  - Contoh:
    ```js
    cy.get('.success-message').should('be.visible');
    ```

**5.3 Mengatasi Masalah Umum**
- **Menunggu Elemen:**
  - Menggunakan `cy.wait()` dan `cy.get().should()` untuk menunggu elemen tersedia.
  - Contoh:
    ```js
    cy.get('.loading-spinner').should('not.exist');
    ```

#### Aktivitas Pembelajaran

**Diskusi Kelas:**
1. Apa saja tantangan dalam berinteraksi dengan elemen web menggunakan Cypress?
2. Bagaimana memastikan form diisi dan dikirimkan dengan benar?

**Bacaan:**
- Dokumentasi Cypress tentang Interaksi dengan Elemen: [Interacting with Elements](https://docs.cypress.io/guides/core-concepts/interacting-with-elements)
- Artikel: "Handling Forms in Cypress" dari blog Cypress.

**Tugas:**
- Menulis tes untuk skenario formulir lengkap, termasuk validasi dan pengiriman formulir dengan data yang benar dan salah.

#### Referensi
- [Cypress Interacting with Elements](https://docs.cypress.io/guides/core-concepts/interacting-with-elements)
- Artikel: "Handling Forms in Cypress" dari blog Cypress.

---

### Minggu 7-8: Pengujian API dengan Cypress

#### Tujuan Pembelajaran
Pada akhir minggu ini, mahasiswa diharapkan dapat:
1. Menguji API menggunakan

 Cypress.
2. Menggunakan metode Cypress untuk melakukan permintaan HTTP dan memverifikasi respons.

#### Materi Pembelajaran

**7.1 Pengenalan Pengujian API dengan Cypress**
- **Apa itu Pengujian API?**
  - Pengujian API adalah proses menguji endpoints API untuk memastikan mereka bekerja seperti yang diharapkan.
  - Menggunakan Cypress untuk melakukan permintaan HTTP dan memverifikasi respons.

**7.2 Melakukan Permintaan HTTP**
- **Metode HTTP:**
  - `cy.request()`: Mengirimkan permintaan HTTP GET, POST, PUT, DELETE.
  - Contoh:
    ```js
    cy.request('GET', '/api/users').then((response) => {
      expect(response.status).to.eq(200);
      expect(response.body).to.have.length(10);
    });
    ```

- **Memverifikasi Respons:**
  - Memverifikasi status kode, headers, dan body dari respons.
  - Contoh:
    ```js
    cy.request('POST', '/api/users', { name: 'John' }).then((response) => {
      expect(response.status).to.eq(201);
      expect(response.body).to.have.property('id');
    });
    ```

**7.3 Tes Data Driven**
- **Menggunakan Fixtures:**
  - Menyimpan data uji dalam file JSON dan menggunakannya dalam tes.
  - Contoh:
    ```js
    cy.fixture('user.json').then((user) => {
      cy.request('POST', '/api/users', user).then((response) => {
        expect(response.status).to.eq(201);
      });
    });
    ```

**7.4 Menyusun dan Membersihkan Data**
- **Hooks untuk Menyiapkan dan Membersihkan Data:**
  - Menggunakan hooks untuk menyiapkan data sebelum tes dijalankan dan membersihkannya setelah tes selesai.
  - Contoh:
    ```js
    before(() => {
      cy.request('POST', '/api/setup');
    });

    after(() => {
      cy.request('POST', '/api/teardown');
    });
    ```

#### Aktivitas Pembelajaran

**Diskusi Kelas:**
1. Apa saja keuntungan menggunakan Cypress untuk pengujian API?
2. Bagaimana cara menangani respons yang tidak sesuai ekspektasi?

**Bacaan:**
- Dokumentasi Cypress tentang Pengujian API: [API Testing](https://docs.cypress.io/guides/end-to-end-testing/api-testing)
- Artikel: "API Testing with Cypress" dari blog Cypress.

**Tugas:**
- Menulis tes untuk menguji beberapa endpoints API, termasuk membuat, membaca, memperbarui, dan menghapus data.

#### Referensi
- [Cypress API Testing](https://docs.cypress.io/guides/end-to-end-testing/api-testing)
- Artikel: "API Testing with Cypress" dari blog Cypress.

---

### Minggu 9-10: Praktik Terbaik dan Studi Kasus

#### Tujuan Pembelajaran
Pada akhir minggu ini, mahasiswa diharapkan dapat:
1. Menerapkan praktik terbaik dalam penulisan tes dengan Cypress.
2. Mengkaji studi kasus pengujian aplikasi nyata menggunakan Cypress.

#### Materi Pembelajaran

**9.1 Praktik Terbaik dalam Penggunaan Cypress**
- **Penulisan Tes yang Dapat Dipelihara:**
  - Memastikan tes mudah dibaca dan dipelihara.
  - Menggunakan nama tes yang deskriptif.
  - Contoh:
    ```js
    describe('Login Functionality', () => {
      it('should login successfully with valid credentials', () => {
        // Steps for login test
      });
    });
    ```

- **Menghindari Ketergantungan Tes:**
  - Tes harus independen dan tidak bergantung pada hasil tes lain.
  - Menggunakan hooks untuk setup dan teardown.

- **Penggunaan Data Uji:**
  - Menggunakan fixtures untuk data uji yang konsisten dan dapat dipelihara.
  - Contoh:
    ```js
    cy.fixture('user.json').then((user) => {
      cy.get('input[name="email"]').type(user.email);
    });
    ```

**9.2 Studi Kasus Pengujian Aplikasi Nyata**
- **Studi Kasus 1: Pengujian Aplikasi E-Commerce**
  - Menguji fitur utama seperti pencarian produk, penambahan ke keranjang, dan checkout.
  - Contoh:
    ```js
    describe('E-Commerce Checkout', () => {
      it('should allow user to search and add product to cart', () => {
        // Steps for search and add to cart test
      });
    });
    ```

- **Studi Kasus 2: Pengujian Aplikasi Sosial Media**
  - Menguji fitur seperti pendaftaran pengguna, posting status, dan interaksi antar pengguna.
  - Contoh:
    ```js
    describe('Social Media Posting', () => {
      it('should allow user to post a status', () => {
        // Steps for posting status test
      });
    });
    ```

**9.3 Debugging dan Troubleshooting Tes Cypress**
- **Debugging Tes:**
  - Menggunakan `cy.pause()` dan `cy.debug()` untuk debugging interaktif.
  - Contoh:
    ```js
    cy.get('button').click().pause();
    ```

- **Troubleshooting Kesalahan:**
  - Memeriksa log dan screenshot yang dihasilkan Cypress untuk menganalisis kesalahan.
  - Menggunakan Cypress Dashboard untuk monitoring dan analisis tes.

#### Aktivitas Pembelajaran

**Diskusi Kelas:**
1. Bagaimana cara memastikan tes Cypress dapat dipelihara dengan baik?
2. Apa saja tantangan yang mungkin dihadapi saat menguji aplikasi nyata?

**Bacaan:**
- Artikel: "Best Practices with Cypress" dari blog Cypress.
- Studi Kasus: "E-Commerce Testing with Cypress" dan "Social Media Testing with Cypress".

**Tugas:**
- Menulis tes untuk salah satu studi kasus (e-commerce atau sosial media) dan mempresentasikan hasilnya di kelas.

#### Referensi
- Artikel: "Best Practices with Cypress" dari blog Cypress.
- Studi Kasus: "E-Commerce Testing with Cypress" dan "Social Media Testing with Cypress".

---

### Minggu 11-12: Proyek Akhir dan Ujian

#### Tujuan Pembelajaran
Pada akhir minggu ini, mahasiswa diharapkan dapat:
1. Menyelesaikan proyek akhir dengan menerapkan semua konsep yang telah dipelajari.
2. Memahami format dan persiapan untuk ujian akhir.

#### Materi Pembelajaran

**11.1 Proyek Akhir**
- **Deskripsi Proyek:**
  - Membuat suite pengujian lengkap untuk aplikasi web yang diberikan.
  - Mencakup semua aspek yang telah dipelajari: pengujian UI, pengujian API, penanganan formulir, dll.

- **Kriteria Penilaian:**
  - Keberhasilan menjalankan tes tanpa kesalahan.
  - Struktur dan keterbacaan kode tes.
  - Penggunaan praktik terbaik dalam penulisan tes.

**11.2 Persiapan Ujian Akhir**
- **Format Ujian:**
  - Bagian Pilihan Ganda: Menguji pemahaman dasar konsep Cypress.
  - Bagian Esai: Menguji kemampuan analitis dan kritis dalam menjelaskan konsep pengujian dengan Cypress.
  - Studi Kasus: Menguji kemampuan menerapkan konsep dalam skenario nyata.

- **Review Materi:**
  - Pengulangan semua topik yang telah dipelajari.
  - Diskusi kelas untuk menyelesaikan pertanyaan dan masalah yang belum terjawab.

**11.3 Pelaksanaan Ujian Akhir**
- **Hari Ujian:**
  - Ujian dilaksanakan di kelas dengan format yang telah dijelaskan.

#### Aktivitas Pembelajaran

**Diskusi Kelas:**
1. Diskusi akhir tentang proyek yang telah dikerjakan.
2. Tanya jawab persiapan ujian akhir.

**Proyek:**
- Menyelesaikan proyek akhir dan mempresentasikannya di kelas.

**Ujian:**
- Pelaksanaan ujian akhir di kelas.

#### Referensi
- Dokumentasi Cypress dan semua materi yang telah dibahas selama semester.
- Artikel dan studi kasus dari blog Cypress.

---

### Minggu 13-14: Evaluasi Proyek Akhir dan Diskusi

#### Tujuan Pembelajaran
Pada akhir minggu ini, mahasiswa diharapkan dapat:
1. Mempresentasikan proyek akhir mereka.
2. Mendapatkan umpan balik konstruktif dari instruktur dan rekan-rekan.

#### Materi Pembelajaran

**13.1 Presentasi Proyek Akhir**
- **Format Presentasi:**
  - Setiap mahasiswa atau kelompok mahasiswa mempresentasikan proyek akhir mereka.
  - Menjelaskan pendekatan pengujian, tantangan yang dihadapi, dan solusi yang diterapkan.

- **Poin Penting yang Harus Disertakan:**
  - Pengaturan lingkungan pengujian.
  - Tes-tes yang dibuat dan alasan pemilihannya.
  - Hasil pengujian dan analisisnya.

**13.2 Umpan Balik dan Diskusi**
- **Umpan Balik Instruktur:**
  - Konstruktif dan berfokus pada peningkatan kualitas pengujian.
  - Aspek positif dan area yang perlu ditingkatkan.

- **Diskusi Kelompok:**
  - Rekan-rekan memberikan umpan balik dan saran.
  - Diskusi terbuka tentang tantangan umum dan solusi yang efektif.

**13.3 Review Keseluruhan Semester**
- **Rekapitulasi Topik yang Dipelajari
