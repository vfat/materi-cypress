### Praktik Terbaik dan Studi Kasus

#### Tujuan Pembelajaran
1. Memahami praktik terbaik dalam penulisan dan pengelolaan tes dengan Cypress.
2. Mampu mengidentifikasi dan menerapkan strategi pengujian yang efektif.
3. Menganalisis studi kasus untuk mendapatkan wawasan tentang implementasi pengujian di dunia nyata.

#### Materi Pembelajaran

##### 1. Praktik Terbaik dalam Penulisan Tes Cypress

- **Organisasi Tes:**
  - Gunakan struktur direktori yang jelas dan terorganisir untuk menyimpan tes. Misalnya, pisahkan tes berdasarkan fitur atau modul aplikasi.
  - Contoh Struktur:
    ```plaintext
    cypress/
      integration/
        auth/
          login.spec.js
          register.spec.js
        dashboard/
          overview.spec.js
          settings.spec.js
    ```

- **Penamaan Tes:**
  - Berikan nama yang deskriptif dan jelas pada file tes dan kasus uji.
  - Contoh:
    ```javascript
    describe('Formulir Login', () => {
      it('Menampilkan pesan kesalahan untuk kredensial yang tidak valid', () => {
        // Isi tes
      })
    })
    ```

- **Penggunaan Hook dengan Bijak:**
  - Manfaatkan `before`, `beforeEach`, `after`, dan `afterEach` untuk mengatur dan membersihkan lingkungan pengujian.
  - Contoh:
    ```javascript
    before(() => {
      // Kode yang dijalankan sekali sebelum semua tes
    })

    beforeEach(() => {
      // Kode yang dijalankan sebelum setiap tes
    })

    afterEach(() => {
      // Kode yang dijalankan setelah setiap tes
    })

    after(() => {
      // Kode yang dijalankan sekali setelah semua tes
    })
    ```

- **Penggunaan Custom Commands:**
  - Buat perintah kustom untuk mengurangi duplikasi kode dan membuat tes lebih mudah dibaca.
  - Contoh:
    ```javascript
    Cypress.Commands.add('login', (username, password) => {
      cy.get('input[name="username"]').type(username)
      cy.get('input[name="password"]').type(password)
      cy.get('button[type="submit"]').click()
    })

    // Penggunaan:
    cy.login('user123', 'password123')
    ```

- **Penggunaan Aliases dan Fixtures:**
  - Gunakan alias (`as`) untuk memperpendek referensi elemen dan fixture untuk data statis.
  - Contoh:
    ```javascript
    cy.get('input[name="username"]').as('usernameField')
    cy.get('@usernameField').type('user123')
    ```

- **Handling Flaky Tests:**
  - Pastikan tes tidak bergantung pada urutan tertentu dan hindari penggunaan waktu tunggu tetap (`cy.wait()`) kecuali sangat diperlukan.

##### 2. Studi Kasus: Implementasi Pengujian di Dunia Nyata

- **Studi Kasus 1: Pengujian Formulir Registrasi Pengguna**
  - **Skenario:**
    - Mengisi dan mengirim formulir registrasi pengguna.
    - Memverifikasi bahwa pengguna baru ditambahkan dan halaman konfirmasi ditampilkan.
  - **Implementasi:**
    ```javascript
    describe('Formulir Registrasi Pengguna', () => {
      it('Mendaftarkan pengguna baru', () => {
        cy.visit('/register')
        cy.get('input[name="first_name"]').type('John')
        cy.get('input[name="last_name"]').type('Doe')
        cy.get('input[name="email"]').type('john.doe@example.com')
        cy.get('input[name="password"]').type('password123')
        cy.get('input[name="confirm_password"]').type('password123')
        cy.get('button[type="submit"]').click()
        cy.contains('Pendaftaran berhasil')
      })
    })
    ```

- **Studi Kasus 2: Pengujian Dashboard Pengguna**
  - **Skenario:**
    - Login dengan kredensial yang benar.
    - Memverifikasi bahwa data pengguna ditampilkan dengan benar di dashboard.
  - **Implementasi:**
    ```javascript
    describe('Dashboard Pengguna', () => {
      beforeEach(() => {
        cy.login('user123', 'password123')
      })

      it('Menampilkan informasi pengguna', () => {
        cy.visit('/dashboard')
        cy.contains('John Doe')
        cy.contains('john.doe@example.com')
      })
    })
    ```

- **Studi Kasus 3: Pengujian API dan Integrasi UI**
  - **Skenario:**
    - Mengirim permintaan API untuk menambahkan item baru.
    - Memverifikasi bahwa item baru muncul di UI.
  - **Implementasi:**
    ```javascript
    describe('Integrasi API dan UI', () => {
      it('Menambahkan item baru dan memverifikasi di UI', () => {
        cy.request('POST', '/api/items', {
          name: 'Item Baru',
          description: 'Deskripsi item baru'
        }).then((response) => {
          const itemId = response.body.id
          cy.visit(`/items/${itemId}`)
          cy.contains('Item Baru')
          cy.contains('Deskripsi item baru')
        })
      })
    })
    ```

##### 3. Strategi Pengujian yang Efektif

- **Automatisasi Tes yang Tepat:**
  - Fokus pada pengujian kasus kritis dan fitur yang sering berubah.
  - Buat tes yang stabil dan dapat diandalkan untuk menghindari tes yang "flaky".

- **Penggunaan CI/CD:**
  - Integrasikan Cypress dengan pipeline CI/CD untuk menjalankan tes secara otomatis pada setiap commit atau pull request.
  - Contoh Integrasi dengan GitHub Actions:
    ```yaml
    name: CI

    on: [push, pull_request]

    jobs:
      cypress-run:
        runs-on: ubuntu-latest
        steps:
          - uses: actions/checkout@v2
          - name: Setup Node.js
            uses: actions/setup-node@v2
            with:
              node-version: '14'
          - run: npm install
          - run: npx cypress run
    ```

- **Penggunaan Laporan dan Analisis:**
  - Gunakan alat pelaporan seperti Cypress Dashboard untuk memonitor hasil tes dan performa.
  - Analisis hasil tes untuk mengidentifikasi area yang memerlukan perbaikan.

#### Aktivitas Pembelajaran
1. **Diskusi Kelas: Praktik Terbaik dalam Pengujian**
   - Diskusikan praktik terbaik dalam penulisan dan pengelolaan tes dengan Cypress.

2. **Praktikum: Implementasi Praktik Terbaik**
   - Ikuti panduan untuk menerapkan praktik terbaik dalam proyek pengujian yang ada.

3. **Latihan: Studi Kasus**
   - Analisis dan implementasikan tes untuk studi kasus yang diberikan, menggunakan praktik terbaik yang telah dibahas.

4. **Proyek Mini: Pengujian API dan UI Terpadu**
   - Buat tes yang menggabungkan pengujian API dan UI, serta integrasikan tes tersebut ke dalam pipeline CI/CD.

#### Referensi
1. [Dokumentasi Resmi Cypress - Praktik Terbaik](https://docs.cypress.io/guides/references/best-practices)
2. [Blog Cypress - Artikel tentang Pengujian](https://www.cypress.io/blog)
3. Buku: *End-to-End Testing with Cypress* oleh Waweru Mwaura
4. [Video Tutorial Cypress di YouTube](https://www.youtube.com/c/CypressIo)

---

Materi ini diharapkan dapat memberikan wawasan yang mendalam bagi peserta dalam menerapkan praktik terbaik dan strategi pengujian yang efektif dengan Cypress. Dengan memahami dan menganalisis studi kasus, peserta akan lebih siap untuk menghadapi tantangan pengujian di dunia nyata dan meningkatkan kualitas aplikasi mereka.
