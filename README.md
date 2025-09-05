# JywaOrkut

JywaOrkut adalah library JavaScript untuk berinteraksi dengan sistem pembayaran QRIS di Indonesia melalui API OrderKuota. Library ini menyediakan fungsi untuk autentikasi OTP, manajemen token, pembayaran QRIS, dan pembuatan kode QR.

## Fitur

*   **Autentikasi OTP:** Mendapatkan kode OTP untuk login.
*   **Manajemen Token:** Mendapatkan dan menyimpan token autentikasi.
*   **Pembayaran QRIS:** Membuat pembayaran menggunakan QRIS Ajaib.
*   **Riwayat Transaksi:** Melihat riwayat transaksi QRIS.
*   **Informasi Akun:** Mendapatkan informasi akun dan saldo.
*   **Pembuatan Kode QR:** Membuat gambar kode QR dari string QRIS.

## Instalasi

Anda dapat menginstal JywaOrkut menggunakan npm atau yarn:

```bash
npm install jywa-orkut
```

atau

```bash
yarn add jywa-orkut
```

## Penggunaan

Berikut adalah contoh penggunaan JywaOrkut:

```javascript
import JywaOrkut from 'jywa-orkut';

const client = new JywaOrkut({
  username: 'your-username',
  password: 'your-password'
});

// Mendapatkan OTP
client.getOTP()
  .then(otpResponse => {
    console.log(otpResponse);
    // { status: 'success', email: 'otp@example.com', message: 'OTP telah dikirim ke otp@example.com. Silakan periksa email Anda.' }

    // Mendapatkan token
    return client.getToken('123456');
  })
  .then(tokenResponse => {
    console.log(tokenResponse);
    // { status: 'success', token: '...', id: '...', name: '...', username: '...', balance: 100000, message: 'Token berhasil diperoleh.' }

    // Membuat pembayaran QRIS
    return client.generateQRISAjaib(10000);
  })
  .then(qrisResponse => {
    console.log(qrisResponse);
    // { success: true, results: { qris: '...', ref_id: '...' } }

    // Membuat gambar QR Code
    return client.generateQRImage(qrisResponse.results.qris);
  })
  .then(qrImage => {
    console.log(qrImage);
    // data:image/png;base64,...
  })
  .catch(error => {
    console.error(error);
  });
```

## Konfigurasi

| Parameter  | Deskripsi                                                                | Wajib   |
| :--------- | :----------------------------------------------------------------------- | :------ |
| `username` | Username akun OrderKuota Anda.                                           | Ya      |
| `password` | Password akun OrderKuota Anda.                                           | Ya      |
| `token`    | Token autentikasi (opsional, jika sudah memiliki token sebelumnya).       | Tidak   |
| `baseQrString` | Base QR String (opsional, jika ingin menggunakan QRIS dengan format custom). | Tidak   |

## API

### `getOTP()`

Meminta kode OTP untuk autentikasi.

```javascript
client.getOTP()
  .then(response => {
    console.log(response);
    // { status: 'success', email: 'otp@example.com', message: 'OTP telah dikirim ke otp@example.com. Silakan periksa email Anda.' }
  });
```

### `getToken(otp)`

Mendapatkan token autentikasi menggunakan kode OTP.

```javascript
client.getToken('123456')
  .then(response => {
    console.log(response);
    // { status: 'success', token: '...', id: '...', name: '...', username: '...', balance: 100000, message: 'Token berhasil diperoleh.' }
  });
```

### `generateQRISAjaib(amount)`

Membuat pembayaran QRIS Ajaib.

```javascript
client.generateQRISAjaib(10000)
  .then(response => {
    console.log(response);
    // { success: true, results: { qris: '...', ref_id: '...' } }
  });
```

### `getQRISHistory(historyType, options)`

Mendapatkan riwayat transaksi QRIS.

*   `historyType`: Tipe riwayat transaksi (`'qris_history'` atau `'qris_ajaib_history'`).
*   `options`: Opsi filter riwayat transaksi (opsional).

```javascript
client.getQRISHistory('qris_history', { page: 2 })
  .then(response => {
    console.log(response);
    // { success: true, results: [...] }
  });
```

### `fetchQrisMenu()`

Mendapatkan menu QRIS dan informasi akun.

```javascript
client.fetchQrisMenu()
  .then(response => {
    console.log(response);
    // { success: true, account: { success: true, results: { balance: 100000, qris_balance: 50000 } }, qris_menu: [...] }
  });
```

### `checkBalance()`

Mengecek saldo akun.

```javascript
client.checkBalance()
  .then(response => {
    console.log(response);
    // { success: true, balance: 100000, qris_balance: 50000 }
  });
```

### `generateQRImage(qrisString, options)`

Membuat gambar kode QR dari string QRIS.

```javascript
client.generateQRImage('...', { width: 512 })
  .then(response => {
    console.log(response);
    // data:image/png;base64,...
  });
```

## Tipe Data

### `OrderKuotaConfig`

```typescript
interface OrderKuotaConfig {
  username: string;
  password: string;
  token?: string;
  baseQrString?: string;
}
```

### `HistoryOptions`

```typescript
interface HistoryOptions {
  keterangan?: string;
  jumlah?: string;
  page?: string;
  dari_tanggal?: string;
  ke_tanggal?: string;
}
```

## Error

Library ini dapat menghasilkan error dengan kode berikut:

*   `MISSING_CONFIG`: Konfigurasi tidak lengkap (username dan password wajib).
*   `INVALID_CREDENTIALS`: OTP tidak valid atau token tidak ditemukan.
*   `INVALID_AMOUNT`: Jumlah pembayaran tidak valid.
*   `INVALID_RESPONSE`: Respon API tidak valid.
*   `QR_GENERATION_FAILED`: Gagal membuat gambar QR Code.

## Lisensi

[MIT](LICENSE)