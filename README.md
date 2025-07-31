 Ringkasan Tutorial Deploy Kontrak Helios dengan Hardhat & Chronos
1. Persiapan Lingkungan
Pastikan sudah install Node.js (v18+) dan npm.

Install MetaMask dan buat akun/testnet wallet.

Dapatkan token testnet HLS dari Helios Faucet untuk deploy dan biaya gas.

2. Clone Repository Proyek
bash
Copy
Edit
git clone https://github.com/azrim/helios-lottery.git
cd helios-lottery
3. Install Dependencies
bash
Copy
Edit
npm install
Abaikan peringatan deprecated, selama tidak error fatal.

4. Buat dan Atur File .env
Copy .env.example ke .env:

bash
Copy
Edit
copy .env.example .env
(di Windows, atau cp di Linux/Mac)

Edit .env dengan editor teks (lebih baik VS Code):

ini
Copy
Edit
PRIVATE_KEY=0xYOUR_FULL_PRIVATE_KEY_HERE
Pastikan private key lengkap 66 karakter (termasuk 0x).

5. Cek dan Sesuaikan Konfigurasi Hardhat
File hardhat.config.js minimal harus berisi:

js
Copy
Edit
require("dotenv").config();
require("@nomicfoundation/hardhat-toolbox");

module.exports = {
  solidity: "0.8.30", // bisa ganti ke "0.8.20" kalau ingin stabil
  networks: {
    helios_testnet: {
      url: "https://testnet1.helioschainlabs.org",
      chainId: 42000,
      accounts: [process.env.PRIVATE_KEY],
    },
  },
};
6. Compile Kontrak
Pastikan kamu di folder helios-lottery, lalu jalankan:

bash
Copy
Edit
npx hardhat compile
7. Deploy Kontrak ke Helios Testnet
bash
Copy
Edit
npx hardhat run scripts/deploy.js --network helios_testnet
Tunggu sampai muncul pesan Deployment Successful!

Simpan alamat kontrak yang muncul.

8. Verifikasi Kontrak (Opsional tapi disarankan)
bash
Copy
Edit
npx hardhat run scripts/extract-input.js
Ikuti instruksi dalam file markdown verify-smart-contracts.md.

9. Jadwalkan Task Otomatis dengan Chronos
Edit scripts/schedule.js, ganti YOUR_DEPLOYED_CONTRACT_ADDRESS dengan alamat kontrak kamu.

Jalankan:

bash
Copy
Edit
npx hardhat run scripts/schedule.js --network helios_testnet
Task otomatis untuk panggil fungsi tertentu (misal drawWinner) akan aktif setiap 24 jam.

10. Cek Status Task di Explorer
Buka https://explorer.helioschainlabs.org

Cari alamat kontrak kamu, buka tab Read Contract

Jalankan fungsi getCronTaskInfo untuk melihat status task.

Tips Tambahan
Jika muncul error terkait .env atau private key, pastikan format benar, tanpa spasi/tanda kutip, dan ada di folder proyek.

Selalu jalankan perintah Hardhat dari folder proyek (helios-lottery).

Restart terminal setelah ubah .env supaya env variable terdeteksi.
