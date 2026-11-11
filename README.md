# Web Redirect GitHub Pages

Web redirect otomatis berbasis GitHub Pages yang mengalihkan pengunjung secara acak (*random*) ke salah satu link tujuan Shopee.

## File Utama
- `index.html`: Menangani akses ke root URL (`contoh.com` atau `username.github.io/repo/`).
- `404.html`: Menangani akses ke path sembarang (*wildcard / catch-all*, misalnya `contoh.com/ransdoaw`).
- `.nojekyll`: Memastikan GitHub Pages tidak memproses file menggunakan Jekyll sehingga proses redirect instan dan tidak terganggu.

## Daftar Link Shopee yang Digunakan
1. `https://s.shopee.co.id/6fgfD1qnbw`
2. `https://s.shopee.co.id/AUtNm852IA`
3. `https://s.shopee.co.id/AUtNm8iQYg`
4. `https://s.shopee.co.id/2BEFqpg8BM`
5. `https://s.shopee.co.id/2qTwe4BYN3`
6. `https://s.shopee.co.id/7pscbHAC9A`
7. `https://s.shopee.co.id/1VyZ3f2YvB`
8. `https://s.shopee.co.id/5LBHciRUuH`

---

## Panduan Deploy ke GitHub Pages

### 1. Inisialisasi Git & Push ke GitHub
Buka terminal / PowerShell di folder ini, lalu jalankan:

```bash
git init
git add .
git commit -m "feat: initial redirect page with index and 404 catch-all"
git branch -M main
git remote add origin https://github.com/USERNAME_GITHUB/NAMA_REPO.git
git push -u origin main
```
*(Ganti `USERNAME_GITHUB` dan `NAMA_REPO` sesuai akun dan repository Anda).*

### 2. Aktifkan GitHub Pages
1. Buka repository Anda di GitHub.
2. Masuk ke menu **Settings** > **Pages** (di sidebar kiri).
3. Di bagian **Build and deployment**:
   - **Source**: Pilih **Deploy from a branch**.
   - **Branch**: Pilih `main` dan folder `/ (root)`.
4. Klik **Save**.
5. Tunggu 1–2 menit hingga status URL GitHub Pages Anda aktif.

### 3. Menggunakan Domain Kustom (Misal: `contoh.com`)
Jika ingin menggunakan domain sendiri:
1. Di menu **Settings** > **Pages**, pada kolom **Custom domain**, masukkan nama domain Anda (misal `contoh.com`).
2. Buat file `CNAME` yang berisi nama domain tersebut jika belum terbuat otomatis oleh GitHub.
3. Di DNS Provider (Cloudflare / Niagahoster / Namecheap / dsb.), arahkan DNS:
   - **A Record**:
     - `185.199.108.153`
     - `185.199.109.153`
     - `185.199.110.153`
     - `185.199.111.153`
   - **CNAME Record** (opsional untuk subdomain seperti `www`): arahkan ke `USERNAME_GITHUB.github.io`.
