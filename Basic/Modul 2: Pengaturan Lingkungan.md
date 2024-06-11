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

---
CONTOH:
---

## Sample 1: 

### File Konfigurasi `cypress.config.js`

```javascript
const { defineConfig } = require('cypress');

module.exports = defineConfig({
  e2e: {
    baseUrl: 'http://localhost:1234',
  },
});
```

## Sample E2E Test

### Struktur Proyek

```
cypress/
  e2e/
    login.cy.js
  support/
    e2e.js
cypress.config.js
```

### File Konfigurasi `cypress/support/e2e.js`

```javascript
// This support file is loaded before each test file
Cypress.on('uncaught:exception', (err, runnable) => {
  // returning false here prevents Cypress from failing the test
  return false;
});

// You can add custom commands here
Cypress.Commands.add('login', (username, password) => {
  cy.visit('/login');
  cy.get('input[name=username]').type(username);
  cy.get('input[name=password]').type(password);
  cy.get('button[type=submit]').click();
});
```

### Sample Test `cypress/e2e/login.cy.js`

```javascript
describe('Login Tests', () => {
  beforeEach(() => {
    cy.visit('/');
  });

  it('should redirect unauthenticated user to sign-in page', () => {
    cy.visit('/dashboard');
    cy.url().should('include', '/login');
  });

  it('allows user to login', () => {
    cy.login('testuser', 'testpassword');
    cy.url().should('include', '/dashboard');
  });

  it('should show an error on invalid login', () => {
    cy.visit('/login');
    cy.get('input[name=username]').type('wronguser');
    cy.get('input[name=password]').type('wrongpassword');
    cy.get('button[type=submit]').click();
    cy.get('.error-message').should('contain', 'Invalid username or password');
  });
});
```

## Langkah-Langkah untuk Menjalankan Cypress

1. **Instal Cypress**: Pastikan Cypress sudah terinstal di proyek Anda. Jika belum, instal dengan perintah berikut:

   ```shell
   npm install cypress --save-dev
   ```

2. **Buka Cypress**: Buka Cypress dengan perintah:

   ```shell
   npx cypress open
   ```

3. **Jalankan Tes E2E**: Pilih file spesifikasi di bawah folder `cypress/e2e` untuk menjalankan tes E2E.

### Penjelasan Konfigurasi dan Tes

1. **Konfigurasi**:
   - File `cypress.config.js` mengatur dasar URL untuk semua tes E2E menjadi `http://localhost:1234`. Ini berarti setiap kali Anda menggunakan `cy.visit('/')`, Cypress akan pergi ke `http://localhost:1234/`.

2. **Support File**:
   - File `cypress/support/e2e.js` digunakan untuk menambahkan konfigurasi global atau perintah kustom yang dapat digunakan di semua tes. Misalnya, perintah kustom `cy.login`.

3. **Sample Test**:
   - File `cypress/e2e/login.cy.js` berisi beberapa tes untuk halaman login. Tes ini mencakup:
     - Memeriksa apakah pengguna yang tidak terautentikasi diarahkan ke halaman login.
     - Memastikan bahwa pengguna dapat login dengan kredensial yang benar.
     - Menampilkan pesan kesalahan ketika login dengan kredensial yang salah.

Dengan konfigurasi dan contoh tes ini, Anda siap untuk mulai menggunakan Cypress untuk menguji aplikasi Anda secara otomatis. Pastikan untuk menyesuaikan tes sesuai dengan kebutuhan spesifik aplikasi Anda.

---

## Sample 2:

### File Konfigurasi `cypress.config.js`

```javascript
const { defineConfig } = require('cypress');

module.exports = defineConfig({
  e2e: {
    baseUrl: 'http://localhost:1234',
    setupNodeEvents(on, config) {
      // Event node setup code here
    },
    supportFile: 'cypress/support/e2e.js',
    specPattern: 'cypress/e2e/**/*.cy.{js,jsx,ts,tsx}',
    slowTestThreshold: 10000,
    testIsolation: true,
  },
  component: {
    devServer: {
      framework: 'create-react-app',
      bundler: 'webpack',
    },
    indexHtmlFile: 'cypress/support/component-index.html',
    setupNodeEvents(on, config) {
      // Event node setup code here
    },
    supportFile: 'cypress/support/component.js',
    specPattern: '**/*.cy.{js,jsx,ts,tsx}',
    experimentalSingleTabRunMode: false,
    slowTestThreshold: 250,
    devServerPublicPathRoute: '/__cypress/src',
  },
  env: {
    FOO: 'bar',
  },
  defaultCommandTimeout: 5000,
  viewportWidth: 1000,
  viewportHeight: 600,
});
```

### File Konfigurasi `cypress/support/e2e.js`

```javascript
// This support file is loaded before each test file
Cypress.on('uncaught:exception', (err, runnable) => {
  // returning false here prevents Cypress from failing the test
  return false;
});

// You can add custom commands here
Cypress.Commands.add('login', (username, password) => {
  cy.visit('/login');
  cy.get('input[name=username]').type(username);
  cy.get('input[name=password]').type(password);
  cy.get('button[type=submit]').click();
});
```

### File Konfigurasi `cypress/support/component.js`

```javascript
// This support file is loaded before each component test file
Cypress.on('uncaught:exception', (err, runnable) => {
  // returning false here prevents Cypress from failing the test
  return false;
});
```

## Sample E2E Test

### Struktur Proyek

```
cypress/
  e2e/
    login.cy.js
  support/
    e2e.js
    component.js
cypress.config.js
```

### Sample Test `cypress/e2e/login.cy.js`

```javascript
describe('Login Tests', () => {
  beforeEach(() => {
    cy.visit('/');
  });

  it('should redirect unauthenticated user to sign-in page', () => {
    cy.visit('/dashboard');
    cy.url().should('include', '/login');
  });

  it('allows user to login', () => {
    cy.login('testuser', 'testpassword');
    cy.url().should('include', '/dashboard');
  });

  it('should show an error on invalid login', () => {
    cy.visit('/login');
    cy.get('input[name=username]').type('wronguser');
    cy.get('input[name=password]').type('wrongpassword');
    cy.get('button[type=submit]').click();
    cy.get('.error-message').should('contain', 'Invalid username or password');
  });
});
```

## Sample Component Test

### Struktur Proyek

```
cypress/
  component/
    ButtonComponent.cy.js
  support/
    component.js
cypress.config.js
src/
  components/
    ButtonComponent.js
    ButtonComponent.css
```

### Sample Component `src/components/ButtonComponent.js`

```javascript
import React from 'react';
import './ButtonComponent.css';

const ButtonComponent = ({ label, onClick }) => (
  <button className="btn" onClick={onClick}>
    {label}
  </button>
);

export default ButtonComponent;
```

### Sample Component Test `cypress/component/ButtonComponent.cy.js`

```javascript
import React from 'react';
import { mount } from 'cypress/react';
import ButtonComponent from '../../src/components/ButtonComponent';

describe('ButtonComponent', () => {
  it('renders the button with the correct label', () => {
    const label = 'Click Me';
    mount(<ButtonComponent label={label} />);
    cy.get('button').should('contain', label);
  });

  it('calls the onClick handler when clicked', () => {
    const onClick = cy.stub();
    mount(<ButtonComponent label="Click Me" onClick={onClick} />);
    cy.get('button').click();
    expect(onClick).to.have.been.calledOnce;
  });
});
```

## Langkah-Langkah untuk Menjalankan Cypress

1. **Instal Cypress**: Pastikan Cypress sudah terinstal di proyek Anda. Jika belum, instal dengan perintah berikut:

   ```shell
   npm install cypress --save-dev
   ```

2. **Buka Cypress**: Buka Cypress dengan perintah:

   ```shell
   npx cypress open
   ```

3. **Jalankan Tes E2E**: Pilih file spesifikasi di bawah folder `cypress/e2e` untuk menjalankan tes E2E.

4. **Jalankan Tes Komponen**: Pilih file spesifikasi di bawah folder `cypress/component` untuk menjalankan tes komponen.

Dengan mengikuti contoh konfigurasi dan tes di atas, Anda dapat memulai pengujian aplikasi Anda menggunakan Cypress. Pastikan untuk menyesuaikan konfigurasi dan tes sesuai kebutuhan proyek Anda.
