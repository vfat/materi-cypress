### Dasar-dasar Penulisan Tes dengan Cypress

#### Tujuan Pembelajaran
1. Memahami sintaks dasar dan struktur tes di Cypress.
2. Mampu menulis dan menjalankan tes dasar dengan Cypress.
3. Mengerti cara menggunakan perintah dasar Cypress untuk interaksi dengan elemen web.

#### Materi Pembelajaran

##### 1. Pendahuluan ke Sintaks dan Struktur Tes Cypress
Cypress menggunakan JavaScript untuk menulis tes. Struktur tes Cypress mengikuti pola umum dari framework pengujian, seperti Mocha.

- **Struktur Tes:**
  - `describe()`: Blok untuk mengelompokkan tes yang berkaitan.
  - `it()`: Blok untuk mendefinisikan tes individu.
  - `before()`, `beforeEach()`, `after()`, `afterEach()`: Hook untuk menjalankan kode sebelum atau setelah tes.

- **Contoh Struktur Tes:**
  ```javascript
  describe('Grup Tes', () => {
    before(() => {
      // Kode yang dijalankan sebelum semua tes dalam grup ini
    })

    beforeEach(() => {
      // Kode yang dijalankan sebelum setiap tes dalam grup ini
    })

    it('Tes pertama', () => {
      // Isi dari tes pertama
    })

    it('Tes kedua', () => {
      // Isi dari tes kedua
    })

    afterEach(() => {
      // Kode yang dijalankan setelah setiap tes dalam grup ini
    })

    after(() => {
      // Kode yang dijalankan setelah semua tes dalam grup ini
    })
  })
  ```

##### 2. Menulis Tes Sederhana
Mulailah dengan menulis tes sederhana untuk memverifikasi bahwa halaman web dapat diakses dan elemen tertentu ada di halaman tersebut.

- **Mengunjungi Halaman dan Memeriksa Elemen:**
  ```javascript
  describe('Tes Halaman Utama', () => {
    it('Memuat halaman utama dan memeriksa elemen', () => {
      cy.visit('http://localhost:3000')
      cy.contains('Welcome to Your App')
    })
  })
  ```

##### 3. Perintah Dasar Cypress
Cypress menyediakan berbagai perintah untuk berinteraksi dengan halaman web dan elemen-elemen di dalamnya.

- **Perintah Navigasi:**
  - `cy.visit(url)`: Mengunjungi URL yang diberikan.
  
- **Perintah Interaksi dengan Elemen:**
  - `cy.get(selector)`: Mendapatkan elemen berdasarkan selektor.
  - `cy.contains(text)`: Mendapatkan elemen yang mengandung teks tertentu.
  - `cy.click()`: Mengklik elemen.
  - `cy.type(text)`: Mengetik teks ke dalam elemen input.
  - `cy.select(value)`: Memilih opsi dalam elemen select.

- **Perintah Asersi:**
  - `cy.should()`: Menambahkan asersi ke perintah sebelumnya.
  - `cy.expect()`: Asersi eksplisit menggunakan Chai.

- **Contoh Penggunaan Perintah:**
  ```javascript
  describe('Formulir Login', () => {
    it('Melakukan login dengan kredensial valid', () => {
      cy.visit('http://localhost:3000/login')
      cy.get('input[name="username"]').type('user123')
      cy.get('input[name="password"]').type('password123')
      cy.get('button[type="submit"]').click()
      cy.url().should('include', '/dashboard')
    })
  })
  ```

##### 4. Menjalankan dan Debugging Tes
Setelah menulis tes, langkah berikutnya adalah menjalankannya dan memastikan tes berjalan dengan benar.

- **Menjalankan Tes:**
  - Buka Cypress dengan perintah:
    ```bash
    npx cypress open
    ```
  - Pilih dan jalankan tes dari Cypress dashboard.

- **Debugging Tes:**
  - Gunakan `cy.pause()` untuk menghentikan sementara eksekusi tes.
  - Gunakan `cy.debug()` untuk memicu breakpoint di DevTools.

#### Aktivitas Pembelajaran
1. **Diskusi Kelas: Struktur Tes dan Sintaks Dasar**
   - Diskusikan struktur dasar tes Cypress dan sintaks yang digunakan.

2. **Praktikum: Menulis Tes Sederhana**
   - Ikuti panduan untuk menulis tes sederhana yang mengunjungi halaman web dan memeriksa elemen.

3. **Latihan: Menggunakan Perintah Dasar**
   - Tulis beberapa tes untuk berinteraksi dengan elemen web menggunakan perintah-perintah dasar Cypress seperti `cy.get()`, `cy.click()`, dan `cy.type()`.

4. **Proyek Mini: Membuat dan Menjalankan Tes Formulir**
   - Buat tes untuk mengisi dan mengirim formulir login, kemudian jalankan dan verifikasi hasilnya menggunakan Cypress.

#### Referensi
1. [Dokumentasi Resmi Cypress - Menulis dan Menjalankan Tes](https://docs.cypress.io/guides/getting-started/writing-your-first-test)
2. [Blog Cypress - Panduan Menulis Tes](https://www.cypress.io/blog)
3. Buku: *End-to-End Testing with Cypress* oleh Waweru Mwaura
4. [Video Tutorial Cypress di YouTube](https://www.youtube.com/c/CypressIo)

---

Materi ini diharapkan dapat memberikan dasar yang kuat bagi peserta dalam menulis dan menjalankan tes menggunakan Cypress. Dengan memahami sintaks dasar dan perintah-perintah utama Cypress, peserta akan siap untuk mengembangkan tes yang lebih kompleks dan efisien.
