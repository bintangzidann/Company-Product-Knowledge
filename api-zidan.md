# API (Application Programming Interface)

## Pengertian

API (Application Programming Interface) adalah sekumpulan aturan dan mekanisme yang memungkinkan satu aplikasi atau sistem berkomunikasi dan bertukar data dengan aplikasi atau sistem lainnya.

API biasanya digunakan agar sebuah aplikasi dapat meminta atau mengirim data ke server tanpa harus mengetahui bagaimana sistem di dalam server tersebut bekerja.

## Cara Kerja API

Secara sederhana, cara kerja API adalah:

1. Client mengirim request kepada API.
2. API menerima dan memproses request tersebut.
3. Server menjalankan proses yang diperlukan.
4. API mengirim response kembali kepada client.
5. Client menampilkan atau menggunakan data yang diterima.

## Contoh API

Contohnya, sebuah aplikasi toko online ingin menampilkan daftar produk.

Client dapat mengirim request:

GET /api/products

Kemudian server dapat memberikan response berupa data JSON:

{
  "products": [
    {
      "id": 1,
      "name": "Laptop",
      "price": 5000000
    },
    {
      "id": 2,
      "name": "Mouse",
      "price": 150000
    }
  ]
}

Dengan API tersebut, aplikasi dapat mengambil data produk dari server dan menampilkannya kepada pengguna.

## Jenis HTTP Method yang Umum Digunakan

- GET: mengambil data.
- POST: membuat atau menambahkan data.
- PUT: memperbarui data secara keseluruhan.
- PATCH: memperbarui sebagian data.
- DELETE: menghapus data.

## Kesimpulan

API merupakan penghubung yang memungkinkan berbagai aplikasi atau sistem berkomunikasi dan bertukar data. API banyak digunakan dalam pengembangan aplikasi web, mobile, dan berbagai sistem yang membutuhkan komunikasi antara client dan server.
