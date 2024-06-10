# Pengaturan Lingkungan

## Tujuan Pembelajaran

Setelah mempelajari materi ini, Anda akan dapat:
1. Memahami konfigurasi dasar Cypress dan cara menggunakannya.
2. Mengetahui cara mengatur dan menjalankan pengujian End-to-End (E2E) dan pengujian komponen.
3. Mengidentifikasi dan menerapkan konfigurasi yang sesuai untuk kebutuhan proyek Anda.
4. Mengatasi masalah umum yang mungkin muncul saat menggunakan Cypress.
5. Menggunakan konfigurasi dinamis dan variabel lingkungan untuk fleksibilitas dalam pengujian.

## Materi Pembelajaran

### 1. Konfigurasi Dasar Cypress

#### 1.1. File Konfigurasi
Cypress menggunakan file konfigurasi untuk menyimpan pengaturan yang spesifik untuk proyek Anda. File konfigurasi ini akan dibuat saat Anda pertama kali menjalankan Cypress dan dapat berupa:
- `cypress.config.js` untuk aplikasi JavaScript.
- `cypress.config.ts` untuk aplikasi TypeScript.
- `.mjs` atau `.cjs` yang memungkinkan penggunaan sintaks modul ESM atau CommonJS.

#### 1.2. Intelligent Code Completion
Cypress mengekspor fungsi `defineConfig` yang menyediakan penyelesaian kode otomatis untuk konfigurasi di banyak editor kode populer. Ini direkomendasikan meskipun tidak wajib.

Contoh:
```ts
{
  e2e: {
    baseUrl: 'http://localhost:1234',
  },
}
```

### 2. Opsi Konfigurasi Global

#### 2.1. Opsi Dasar
- **clientCertificates**: Sertifikat klien opsional untuk autentikasi.
- **env**: Variabel lingkungan yang dapat diatur untuk digunakan dalam pengujian.
- **includeShadowDom**: Menyertakan elemen dalam shadow DOM saat melakukan query.
- **numTestsKeptInMemory**: Jumlah tes yang disimpan dalam memori.
- **port**: Port yang digunakan untuk hosting Cypress, biasanya dihasilkan secara acak.
- **reporter**: Reporter yang digunakan selama `cypress run`.
- **reporterOptions**: Opsi yang digunakan oleh reporter.
- **retries**: Jumlah ulang untuk tes yang gagal.

#### 2.2. Opsi Timeout
- **defaultCommandTimeout**: Timeout untuk sebagian besar perintah berbasis DOM, default 4000 ms.
- **pageLoadTimeout**: Timeout untuk peristiwa transisi halaman, default 60000 ms.
- **requestTimeout**: Timeout untuk permintaan dalam `cy.wait()`, default 5000 ms.
- **responseTimeout**: Timeout untuk tanggapan dalam `cy.request()`, default 30000 ms.

#### 2.3. Pengaturan Folder dan File
- **downloadsFolder**: Jalur ke folder tempat file yang diunduh selama tes disimpan.
- **fixturesFolder**: Jalur ke folder yang berisi file fixture.
- **screenshotsFolder**: Jalur ke folder tempat tangkapan layar disimpan.
- **videosFolder**: Jalur ke folder tempat video tes disimpan.

### 3. Konfigurasi Pengujian Tipe-Spesifik

#### 3.1. E2E Testing
Pengaturan untuk pengujian End-to-End, termasuk:
- **baseUrl**: URL dasar untuk `cy.visit()` dan `cy.request()`.
- **setupNodeEvents**: Fungsi untuk mendaftarkan event node.
- **supportFile**: File yang dimuat sebelum file spesifikasi.
- **specPattern**: Pola glob untuk memuat file tes.
- **slowTestThreshold**: Ambang waktu untuk menandai tes sebagai "lambat", default 10000 ms.
- **testIsolation**: Mengaktifkan isolasi tes untuk memastikan konteks browser yang bersih antara tes.

Contoh:
```ts
{
  e2e: {
    baseUrl: 'http://localhost:1234',
    setupNodeEvents(on, config) {
      // kode pengaturan event node
    },
    supportFile: 'cypress/support/e2e.js',
    specPattern: 'cypress/e2e/**/*.cy.{js,jsx,ts,tsx}',
    slowTestThreshold: 10000,
    testIsolation: true,
  }
}
```

#### 3.2. Component Testing
Pengaturan untuk pengujian komponen, termasuk:
- **devServer**: Pengaturan server dev untuk pengujian komponen.
- **indexHtmlFile**: Lokasi tempat Cypress merender komponen.
- **setupNodeEvents**: Fungsi untuk mendaftarkan event node.
- **supportFile**: File yang dimuat sebelum file spesifikasi.
- **specPattern**: Pola glob untuk memuat file spesifikasi.
- **experimentalSingleTabRunMode**: Menjalankan semua spesifikasi dalam satu tab untuk meningkatkan kinerja.
- **slowTestThreshold**: Ambang waktu untuk menandai tes sebagai "lambat", default 250 ms.
- **devServerPublicPathRoute**: Jalur publik dari server dev yang digunakan.

Contoh:
```ts
{
  component: {
    devServer: {
      framework: 'create-react-app',
      bundler: 'webpack',
    },
    indexHtmlFile: 'cypress/support/component-index.html',
    setupNodeEvents(on, config) {
      // kode pengaturan event node
    },
    supportFile: 'cypress/support/component.js',
    specPattern: '**/*.cy.{js,jsx,ts,tsx}',
    experimentalSingleTabRunMode: false,
    slowTestThreshold: 250,
    devServerPublicPathRoute: '/__cypress/src',
  }
}
```

### 4. Overriding Options

#### 4.1. Command Line Overrides
Anda dapat menggunakan flag `--config` untuk menimpa opsi konfigurasi saat menjalankan Cypress dari command line.

Contoh:
```shell
cypress run --browser firefox --config viewportWidth=1280,viewportHeight=720
```

#### 4.2. Alternative Config File
Gunakan flag `--config-file` untuk mengubah file konfigurasi yang digunakan oleh Cypress.

Contoh:
```shell
cypress run --config-file tests/cypress.config.js
```

#### 4.3. Environment Variables
Konfigurasi dapat ditimpa dengan variabel lingkungan, berguna dalam Continuous Integration atau saat bekerja secara lokal.

Contoh:
```shell
export CYPRESS_VIEWPORT_WIDTH=800
export CYPRESS_VIEWPORT_HEIGHT=600
```

### 5. Test Configuration

#### 5.1. `Cypress.config()`
Anda dapat menimpa nilai konfigurasi dalam tes menggunakan `Cypress.config()`. Ini mengubah konfigurasi untuk sisa eksekusi file spesifikasi saat ini.

Contoh:
```javascript
Cypress.config('pageLoadTimeout', 100000)

Cypress.config('pageLoadTimeout') // => 100000
```

#### 5.2. Test-specific Configuration
Terapkan nilai konfigurasi spesifik ke suite atau tes dengan melewatkan objek konfigurasi ke fungsi suite atau tes.

Syntax:
```javascript
describe(name, config, fn)
context(name, config, fn)
it(name, config, fn)
specify(name, config, fn)
```

Contoh untuk suite:
```js
describe(
  'login',
  {
    retries: {
      runMode: 3,
      openMode: 2,
    },
  },
  () => {
    it('should redirect unauthenticated user to sign-in page', () => {
      // ...
    })

    it('allows user to login', () => {
      // ...
    })
  }
)
```

Contoh untuk tes:
```js
it('Show warning outside Chrome', { browser: '!chrome' }, () => {
  cy.get('.browser-warning').should(
    'contain',
    'For optimal viewing, use Chrome browser'
  )
})
```

### 6. Resolved Configuration

Ketika Anda membuka proyek Cypress, memperluas panel Project Settings di bawah **Settings** akan menampilkan konfigurasi yang telah diselesaikan. Ini membantu Anda memahami dan melihat dari mana nilai-nilai yang berbeda berasal.

### 7. Masalah Umum dan Solusinya

#### 7.1. `baseUrl` tidak diatur
Jangan meletakkan opsi konfigurasi `baseUrl` ke dalam objek `env`. Letakkan properti `baseUrl` di luar objek `env` dan di dalam objek tipe pengujian `e2e`.

Contoh yang benar:
```ts
{
  env: {
    FOO: 'bar',
  },
  e2e: {
    baseUrl: 'http://localhost:3030',
  },
}
```

#### 7.2. File spesifikasi tidak ditemukan saat menggunakan parameter `spec`
Pastikan untuk membuat jalur relatif terhadap folder proyek. Jika spesifikasi masih hilang, jalankan Cypress dengan log DEBUG:

```shell
DEBUG=cypress:cli,cypress:server:specs
```

## Aktivitas Pembelajaran

1. **Membaca Materi**: Bacalah setiap bagian dari materi pembelajaran ini untuk memahami konsep dan konfigurasi dasar Cypress.
2. **Praktik Konfigurasi**:
   - Buat file konfigurasi `cypress.config.js` atau `cypress.config.ts` di proyek Anda.
   - Konfigurasikan opsi global seperti `baseUrl`, `env`, dan `retries`.
3. **Eksplorasi Timeouts dan Folders**:
   - Uji berbagai pengaturan timeout dalam proyek Anda.
   - Atur jalur folder untuk `downloadsFolder`, `screenshotsFolder`, dan `videosFolder`.
4. **Pengujian Tipe-Spesifik**:
  

 - Buat pengaturan untuk pengujian E2E dan komponen menggunakan `e2e` dan `component` objek dalam konfigurasi Cypress.
   - Praktikkan penggunaan `setupNodeEvents` untuk mengonfigurasi event node.
5. **Menggunakan Overriding Options**:
   - Jalankan Cypress dengan opsi konfigurasi yang ditimpa menggunakan `--config` dan `--config-file`.
   - Eksperimen dengan variabel lingkungan untuk menimpa konfigurasi.
6. **Melihat Resolved Configuration**:
   - Buka proyek Cypress Anda dan periksa konfigurasi yang telah diselesaikan di panel Pengaturan Proyek.
7. **Menyelesaikan Masalah Umum**:
   - Praktikkan solusi untuk masalah umum seperti pengaturan `baseUrl` dan spesifikasi file yang hilang.

## Referensi

1. [Cypress Configuration File](https://docs.cypress.io/guides/references/configuration)
2. [Cypress Environment Variables](https://docs.cypress.io/guides/guides/environment-variables)
3. [Cypress Command Line](https://docs.cypress.io/guides/guides/command-line)
4. [Cypress Plugins Guide](https://docs.cypress.io/guides/tooling/plugins-guide)
5. [Cypress Component Testing Configuration](https://docs.cypress.io/guides/component-testing/component-framework-configuration)
6. [Resolved Configuration](https://docs.cypress.io/guides/references/configuration#Resolved-Configuration)
7. [Troubleshooting Guide](https://docs.cypress.io/guides/references/troubleshooting)

Dengan memahami dan mempraktikkan materi ini, Anda akan lebih siap untuk mengonfigurasi dan menjalankan pengujian menggunakan Cypress secara efektif.
