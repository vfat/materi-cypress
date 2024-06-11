### Pengujian API dengan Cypress

#### Tujuan Pembelajaran
1. Memahami dasar-dasar pengujian API dengan Cypress.
2. Mampu mengirim permintaan HTTP dan memverifikasi respons menggunakan Cypress.
3. Mengerti cara mengintegrasikan pengujian API dengan pengujian end-to-end.

#### Materi Pembelajaran

##### 1. Pendahuluan ke Pengujian API dengan Cypress
Cypress bukan hanya alat untuk pengujian UI, tetapi juga mendukung pengujian API. Dengan Cypress, Anda dapat mengirim permintaan HTTP dan memeriksa respons, memungkinkan Anda untuk memastikan bahwa API bekerja dengan benar.

- **Keuntungan Pengujian API dengan Cypress:**
  - Integrasi dengan pengujian end-to-end.
  - Kemampuan untuk menguji API secara langsung dan cepat.
  - Menyederhanakan pengujian dengan menggunakan satu alat untuk pengujian UI dan API.

##### 2. Mengirim Permintaan HTTP dengan Cypress
Cypress menyediakan perintah `cy.request()` untuk mengirim permintaan HTTP. Perintah ini mendukung berbagai metode HTTP seperti GET, POST, PUT, DELETE, dll.

- **Sintaks Dasar `cy.request()`:**
  ```javascript
  cy.request({
    method: 'GET',       // Metode HTTP
    url: '/api/users',   // URL endpoint
    headers: {           // Header permintaan
      'Authorization': 'Bearer token123'
    },
    body: {              // Body permintaan untuk metode POST atau PUT
      name: 'John Doe',
      email: 'john.doe@example.com'
    }
  })
  ```

- **Contoh Permintaan GET:**
  ```javascript
  cy.request('GET', '/api/users')
    .then((response) => {
      expect(response.status).to.eq(200)
      expect(response.body).to.have.length(10)
    })
  ```

- **Contoh Permintaan POST:**
  ```javascript
  cy.request('POST', '/api/users', {
    name: 'John Doe',
    email: 'john.doe@example.com'
  }).then((response) => {
    expect(response.status).to.eq(201)
    expect(response.body).to.have.property('id')
  })
  ```

##### 3. Memverifikasi Respons API
Setelah mengirim permintaan HTTP, langkah berikutnya adalah memverifikasi bahwa respons yang diterima sesuai dengan yang diharapkan.

- **Memeriksa Status Respons:**
  ```javascript
  cy.request('GET', '/api/users')
    .its('status')
    .should('eq', 200)
  ```

- **Memeriksa Header Respons:**
  ```javascript
  cy.request('GET', '/api/users')
    .its('headers')
    .should('include', { 'content-type': 'application/json; charset=utf-8' })
  ```

- **Memeriksa Body Respons:**
  ```javascript
  cy.request('GET', '/api/users')
    .its('body')
    .should('have.length', 10)
  ```

##### 4. Mengintegrasikan Pengujian API dengan Pengujian End-to-End
Salah satu kekuatan Cypress adalah kemampuannya untuk menggabungkan pengujian API dengan pengujian UI, memungkinkan pengujian end-to-end yang komprehensif.

- **Contoh Integrasi Pengujian API dan UI:**
  ```javascript
  describe('Integrasi Pengujian API dan UI', () => {
    it('Membuat pengguna baru dan memverifikasi di UI', () => {
      // Mengirim permintaan API untuk membuat pengguna baru
      cy.request('POST', '/api/users', {
        name: 'John Doe',
        email: 'john.doe@example.com'
      }).then((response) => {
        const userId = response.body.id

        // Mengunjungi halaman pengguna dan memverifikasi bahwa pengguna baru muncul di UI
        cy.visit(`/users/${userId}`)
        cy.contains('John Doe')
        cy.contains('john.doe@example.com')
      })
    })
  })
  ```

#### Aktivitas Pembelajaran
1. **Diskusi Kelas: Dasar-dasar Pengujian API**
   - Diskusikan keuntungan pengujian API dan kapan sebaiknya digunakan dalam proses pengembangan.

2. **Praktikum: Mengirim Permintaan HTTP**
   - Ikuti panduan untuk mengirim permintaan HTTP menggunakan `cy.request()` dan memverifikasi respons.

3. **Latihan: Memverifikasi Respons API**
   - Tulis tes untuk memeriksa status, header, dan body respons dari berbagai endpoint API.

4. **Proyek Mini: Integrasi Pengujian API dan UI**
   - Buat tes yang menggabungkan pengujian API dan UI, misalnya membuat data melalui API dan memverifikasi tampilan data tersebut di UI.

#### Referensi
1. [Dokumentasi Resmi Cypress - Pengujian API](https://docs.cypress.io/guides/guides/network-requests)
2. [Blog Cypress - Panduan Pengujian API](https://www.cypress.io/blog)
3. Buku: *End-to-End Testing with Cypress* oleh Waweru Mwaura
4. [Video Tutorial Cypress di YouTube](https://www.youtube.com/c/CypressIo)

---

Materi ini diharapkan dapat memberikan dasar yang kuat bagi peserta dalam melakukan pengujian API menggunakan Cypress. Dengan memahami cara mengirim permintaan HTTP dan memverifikasi respons, peserta akan dapat memastikan bahwa API berfungsi dengan baik dan dapat diintegrasikan dengan pengujian UI untuk pengujian end-to-end yang komprehensif.
