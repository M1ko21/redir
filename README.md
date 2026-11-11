# Web Redirect GitHub Pages + Cloudflare Analytics

Web redirect otomatis berbasis GitHub Pages yang mengalihkan pengunjung secara acak (*random*) ke salah satu link tujuan Shopee, dilengkapi pelacakan visitor harian via **Cloudflare**.

## File Utama
- `index.html`: Menangani akses ke root URL (`contoh.com`).
- `404.html`: Menangani akses ke path sembarang (*wildcard / catch-all*, misalnya `contoh.com/ransdoaw`).
- `.nojekyll`: Memastikan GitHub Pages menyajikan file langsung secara statis tanpa Jekyll.

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

## 1. Deploy ke GitHub Pages

### A. Push ke GitHub
Buka terminal / PowerShell di folder ini, lalu jalankan:

```bash
git remote add origin https://github.com/USERNAME_GITHUB/NAMA_REPO.git
git push -u origin main
```
*(Ganti `USERNAME_GITHUB` dan `NAMA_REPO` sesuai akun dan repository Anda).*

### B. Aktifkan GitHub Pages
1. Buka repository Anda di GitHub.
2. Masuk ke **Settings** > **Pages** (di sidebar kiri).
3. Di bagian **Build and deployment**:
   - **Source**: Pilih **Deploy from a branch**.
   - **Branch**: Pilih `main` dan folder `/ (root)`.
4. Klik **Save**.

---

## 2. Setup Cloudflare & Pelacakan Visitor Harian

Dengan menggunakan Cloudflare, setiap pengunjung yang mengakses domain Anda (baik `contoh.com` maupun `contoh.com/apapun`) akan **otomatis dihitung** sebelum browser dialihkan ke Shopee.

### Langkah 1: Hubungkan Domain ke Cloudflare
1. Buat akun gratis di [Cloudflare](https://dash.cloudflare.com/) lalu klik **Add a domain / site**.
2. Masukkan nama domain Anda (misal: `contoh.com`) dan pilih paket **Free**.
3. Cloudflare akan memberikan 2 alamat Nameserver (contoh: `alec.ns.cloudflare.com` & `zoe.ns.cloudflare.com`).
4. Buka tempat Anda membeli domain (Niagahoster, Namecheap, Domainesia, Rumahweb, dll.), lalu ganti Nameserver bawaan menjadi Nameserver Cloudflare tersebut.

### Langkah 2: Atur DNS di Cloudflare
Di dashboard Cloudflare, buka menu **DNS** > **Records**, lalu tambahkan record berikut:

| Type | Name | Content / IPv4 | Proxy status |
|---|---|---|---|
| **A** | `@` | `185.199.108.153` | **Proxied** (Awan Oranye) |
| **A** | `@` | `185.199.109.153` | **Proxied** (Awan Oranye) |
| **A** | `@` | `185.199.110.153` | **Proxied** (Awan Oranye) |
| **A** | `@` | `185.199.111.153` | **Proxied** (Awan Oranye) |
| **CNAME** | `www` | `USERNAME_GITHUB.github.io` | **Proxied** (Awan Oranye) |

> **Penting**: Pastikan status proxy berwarna **Awan Oranye (Proxied)** agar Cloudflare dapat menghitung trafik dan visitor.

### Langkah 3: Konfigurasi SSL di Cloudflare
1. Di dashboard Cloudflare, buka menu **SSL/TLS**.
2. Ubah encryption mode menjadi **Full** (atau **Full (strict)**).
   *(Ini penting agar tidak terjadi error loop redirect `ERR_TOO_MANY_REDIRECTS`).*

### Langkah 4: Sambungkan Domain di GitHub Pages
1. Buka kembali repository di GitHub > **Settings** > **Pages**.
2. Pada kolom **Custom domain**, masukkan nama domain Anda (misal `contoh.com`), lalu klik **Save**.
3. Centang opsi **Enforce HTTPS**.

---

## 3. Cara Melihat Jumlah Visitor Per Hari

Setelah domain aktif melalui Cloudflare:

1. Buka [Cloudflare Dashboard](https://dash.cloudflare.com/).
2. Klik nama domain Anda.
3. Di menu sidebar kiri, buka **Analytics & Logs** > **Traffic**.
4. Anda dapat melihat:
   - **Unique Visitors**: Jumlah pengunjung unik harian (1 orang dihitung 1 kali per 24 jam).
   - **Total Requests**: Total semua kunjungan / hit ke link redirect Anda.
   - **Filter Waktu**: Anda bisa memilih rentang waktu *Last 24 hours*, *Last 7 days*, *Last 30 days*, dll.
   - **Grafik & Negara**: Asal pengunjung, sistem operasi (Android, iOS, Windows), dan browser yang digunakan.
