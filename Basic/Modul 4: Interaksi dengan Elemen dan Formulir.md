### Interaksi dengan Elemen dan Formulir

#### Tujuan Pembelajaran
1. Memahami cara berinteraksi dengan elemen-elemen web menggunakan Cypress.
2. Mampu mengisi dan mengirim formulir menggunakan perintah Cypress.
3. Mengerti cara memverifikasi hasil dari interaksi dengan elemen dan formulir.

#### Materi Pembelajaran

##### 1. Memilih Elemen dengan Cypress
Cypress menyediakan berbagai metode untuk memilih elemen di halaman web.

- **Perintah Dasar:**
  - `cy.get(selector)`: Memilih elemen berdasarkan selektor CSS.
  - `cy.contains(text)`: Memilih elemen yang mengandung teks tertentu.

- **Contoh Penggunaan:**
  ```javascript
  cy.get('#username')
  cy.get('.btn-primary')
  cy.contains('Submit')
  ```

##### 2. Berinteraksi dengan Elemen
Setelah memilih elemen, Anda dapat berinteraksi dengannya menggunakan berbagai perintah Cypress.

- **Perintah Interaksi:**
  - `cy.click()`: Mengklik elemen.
  - `cy.type(text)`: Mengetik teks ke dalam elemen input.
  - `cy.select(value)`: Memilih opsi dalam elemen select.
  - `cy.check()`: Memilih checkbox atau radio button.
  - `cy.uncheck()`: Membatalkan pilihan checkbox.
  - `cy.clear()`: Menghapus teks dari elemen input.

- **Contoh Penggunaan:**
  ```javascript
  cy.get('input[name="username"]').type('user123')
  cy.get('input[name="password"]').type('password123')
  cy.get('button[type="submit"]').click()
  cy.get('select').select('Option1')
  cy.get('input[type="checkbox"]').check()
  cy.get('input[type="checkbox"]').uncheck()
  cy.get('input[name="username"]').clear()
  ```

##### 3. Mengisi dan Mengirim Formulir
Interaksi dengan formulir adalah salah satu tugas umum dalam pengujian aplikasi web. Cypress memudahkan proses ini dengan berbagai perintah yang intuitif.

- **Mengisi Formulir:**
  ```javascript
  cy.get('input[name="first_name"]').type('John')
  cy.get('input[name="last_name"]').type('Doe')
  cy.get('input[name="email"]').type('john.doe@example.com')
  cy.get('textarea[name="message"]').type('Hello, this is a test message.')
  ```

- **Mengirim Formulir:**
  ```javascript
  cy.get('form').submit()
  ```

- **Contoh Tes Formulir:**
  ```javascript
  describe('Tes Formulir Kontak', () => {
    it('Mengisi dan mengirim formulir kontak', () => {
      cy.visit('http://localhost:3000/contact')
      cy.get('input[name="first_name"]').type('John')
      cy.get('input[name="last_name"]').type('Doe')
      cy.get('input[name="email"]').type('john.doe@example.com')
      cy.get('textarea[name="message"]').type('Hello, this is a test message.')
      cy.get('button[type="submit"]').click()
      cy.contains('Terima kasih telah menghubungi kami!')
    })
  })
  ```

##### 4. Memverifikasi Hasil Interaksi
Setelah berinteraksi dengan elemen atau mengirim formulir, penting untuk memverifikasi bahwa hasil yang diharapkan terjadi.

- **Perintah Asersi:**
  - `cy.should()`: Menambahkan asersi ke perintah sebelumnya.
  - `cy.url().should('include', 'path')`: Memverifikasi URL.
  - `cy.contains('text')`: Memverifikasi teks yang ada di elemen.

- **Contoh Asersi:**
  ```javascript
  cy.url().should('include', '/dashboard')
  cy.get('h1').should('have.text', 'Welcome, John Doe')
  cy.get('.notification').should('be.visible').and('contain', 'Message sent successfully')
  ```

#### Aktivitas Pembelajaran
1. **Diskusi Kelas: Interaksi dengan Elemen dan Formulir**
   - Diskusikan berbagai perintah yang digunakan untuk berinteraksi dengan elemen web dan formulir.

2. **Praktikum: Memilih dan Berinteraksi dengan Elemen**
   - Ikuti panduan untuk memilih dan berinteraksi dengan elemen-elemen web menggunakan perintah `cy.get()`, `cy.click()`, `cy.type()`, dll.

3. **Latihan: Mengisi dan Mengirim Formulir**
   - Tulis tes untuk mengisi dan mengirim formulir, kemudian verifikasi hasilnya.

4. **Proyek Mini: Tes Formulir Registrasi**
   - Buat tes untuk formulir registrasi pengguna, termasuk pengisian semua field dan pengiriman formulir, serta verifikasi hasil yang diharapkan.

#### Referensi
1. [Dokumentasi Resmi Cypress - Interaksi dengan Elemen](https://docs.cypress.io/guides/core-concepts/interacting-with-elements)
2. [Blog Cypress - Panduan Pengujian Formulir](https://www.cypress.io/blog)
3. Buku: *End-to-End Testing with Cypress* oleh Waweru Mwaura
4. [Video Tutorial Cypress di YouTube](https://www.youtube.com/c/CypressIo)

---

Materi ini diharapkan dapat memberikan pemahaman yang mendalam bagi peserta dalam berinteraksi dengan elemen-elemen web dan formulir menggunakan Cypress. Dengan menguasai perintah-perintah ini, peserta akan dapat menulis tes yang lebih kompleks dan memastikan aplikasi web berfungsi sesuai dengan yang diharapkan.
