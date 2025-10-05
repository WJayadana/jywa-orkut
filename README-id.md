# OrderKuota Node.js API Wrapper (Versi Bahasa Indonesia)

OrderKuota Node.js API Wrapper adalah sebuah pustaka (library) untuk mengakses layanan pembayaran QRIS OrderKuota secara mudah melalui Node.js dan TypeScript. Proyek ini bertujuan membantu developer mengintegrasikan fitur pembayaran QRIS, autentikasi OTP, cek saldo, dan riwayat transaksi ke dalam aplikasi mereka dengan cepat dan aman.

## Fitur

- ✅ **Dukungan TypeScript Penuh** - Definisi tipe lengkap dan autocomplete IDE
- ✅ **Pembuatan Pembayaran QRIS** - Buat pembayaran QRIS Ajaib beserta kode QR
- ✅ **Alur Autentikasi** - Login berbasis OTP dengan manajemen token
- ✅ **Riwayat Transaksi** - Ambil dan filter riwayat transaksi QRIS
- ✅ **Cek Saldo** - Cek saldo akun dan QRIS
- ✅ **Pembuatan Kode QR** - Konversi string QRIS ke gambar QR base64

## Instalasi

```bash
npm install jywa-orkut
```

## Mulai Cepat

```javascript
import OrderKuota from 'jywa-orkut';

const client = new OrderKuota({
  username: 'username-anda',
  password: 'password-anda'
});

// Minta OTP
const otp = await client.getOTP();
console.log('OTP dikirim ke:', otp.email);

// Dapatkan token autentikasi
const token = await client.getToken('123456');

// Buat pembayaran QRIS
const payment = await client.generateQRISAjaib(10000);
const qrString = payment.qris_ajaib.results.qr_string;

// Buat gambar kode QR
const qrImage = await client.generateQRImage(qrString);
```

## Penggunaan TypeScript

```typescript
import OrderKuota, { OrderKuotaConfig, OrderKuotaError } from 'jywa-orkut';

const config: OrderKuotaConfig = {
  username: 'username-anda',
  password: 'password-anda'
};

const client = new OrderKuota(config);

try {
  const payment = await client.generateQRISAjaib(25000);
  // Type safety dan autocomplete IDE
} catch (error) {
  if (error instanceof OrderKuotaError) {
    console.error(`Error [${error.code}]:`, error.message);
  }
}
```

## Contoh

- [`example/typescript-example.ts`](example/typescript-example.ts) - Alur kerja TypeScript lengkap
- [`example/javascript-example.js`](example/javascript-example.js) - Implementasi JavaScript

Jalankan contoh:
```bash
npm run example:js    # Contoh JavaScript
npm run example:ts    # Contoh TypeScript
```

## Dokumentasi

📚 **Dokumentasi API lengkap**: [GitHub Pages](https://WJayadana.github.io/jywa-orkut/)

## Pengembangan

```bash
# Instal dependensi
npm install

# Build proyek
npm run build

# Generate dokumentasi
npm run docs:generate
```

## Lisensi

Lisensi MIT - lihat file [LICENSE](LICENSE) untuk detail.

## Dukungan

- 🐛 **Laporan Bug**: [GitHub Issues](https://github.com/WJayadana/jywa-orkut/issues)
- 💬 **Diskusi**: [GitHub Discussions](https://github.com/WJayadana/jywa-orkut/discussions)

---

**Disclaimer**: Ini adalah pembungkus tidak resmi. Harap patuhi syarat dan ketentuan OrderKuota.
