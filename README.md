# OrderKuota Node.js API Wrapper

A TypeScript-first Node.js wrapper for the OrderKuota Indonesian QRIS payment API.

## Features

- ✅ **Full TypeScript Support** - Complete type definitions and IDE autocomplete
- ✅ **QRIS Payment Generation** - Generate QRIS Ajaib payments with QR codes
- ✅ **Authentication Flow** - OTP-based login with token management
- ✅ **Transaction History** - Fetch and filter QRIS transaction records
- ✅ **Balance Checking** - Check account and QRIS balances
- ✅ **QR Code Generation** - Convert QRIS strings to base64 QR images

## Installation

```bash
npm install jywa-orkut
```

## Quick Start

```javascript
import JywaOrkut from 'jywa-orkut';

const client = new JywaOrkut({
  username: 'your-username',
  password: 'your-password'
});

// Request OTP
const otp = await client.getOTP();
console.log('OTP sent to:', otp.email);

// Get authentication token
const token = await client.getToken('123456');

// Generate QRIS payment
const payment = await client.generateQRISAjaib(10000);
const qrString = payment.qris_ajaib.results.qr_string;

// Generate QR code image
const qrImage = await client.generateQRImage(qrString);
```

## TypeScript Usage

```typescript
import JywaOrkut, { OrderKuotaConfig, OrderKuotaError } from 'jywa-orkut';

const config: OrderKuotaConfig = {
  username: 'your-username',
  password: 'your-password'
};

const client = new JywaOrkut(config);

try {
  const payment = await client.generateQRISAjaib(25000);
  // Full type safety and IDE autocomplete
} catch (error) {
  if (error instanceof OrderKuotaError) {
    console.error(`Error [${error.code}]:`, error.message);
  }
}
```

## Examples

- [`example/typescript-example.ts`](example/typescript-example.ts) - Complete TypeScript workflow
- [`example/javascript-example.js`](example/javascript-example.js) - JavaScript implementation

Run examples:
```bash
npm run example:js    # JavaScript example
npm run example:ts    # TypeScript example
```

## Documentation

📚 **Complete API documentation**: [GitHub Pages](https://wjayadana.github.io/jywa-orkut/)

## Development

```bash
# Install dependencies
npm install

# Build project
npm run build

# Generate documentation
npm run docs:generate
```


[MIT](LICENSE)