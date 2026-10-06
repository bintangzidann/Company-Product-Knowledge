Siap. Kalau mau yang lebih banyak, lengkap, tapi tetap cocok untuk dokumentasi anak magang, paste seluruh isi ini ke jwt-zidan.md:

# JWT (JSON Web Token)

## 1. Pengertian

JWT (JSON Web Token) adalah sebuah standar terbuka yang digunakan untuk mengirimkan informasi antara beberapa pihak secara aman dalam bentuk JSON.

JWT sering digunakan dalam sistem autentikasi dan otorisasi pada aplikasi web, mobile, maupun API.

Dengan JWT, server dapat memberikan sebuah token kepada pengguna setelah pengguna berhasil melakukan login. Token tersebut kemudian dapat digunakan oleh client untuk membuktikan bahwa pengguna sudah terautentikasi ketika mengakses endpoint atau fitur tertentu.

JWT memiliki sifat compact, sehingga dapat dengan mudah dikirim melalui HTTP request.

---

## 2. Fungsi JWT

JWT memiliki beberapa fungsi utama, yaitu:

### Authentication

JWT dapat digunakan untuk mengetahui apakah pengguna sudah berhasil login atau belum.

Contohnya:

1. User memasukkan username dan password.
2. Server memeriksa data login.
3. Jika benar, server membuat JWT.
4. JWT diberikan kepada client.
5. Client menggunakan JWT ketika mengakses API yang membutuhkan login.

### Authorization

JWT juga dapat digunakan untuk menentukan hak akses pengguna.

Contohnya, sebuah sistem memiliki beberapa role:

- Admin
- Staff
- Customer

JWT dapat membawa informasi mengenai role pengguna sehingga server dapat menentukan apakah pengguna memiliki izin untuk mengakses suatu fitur.

---

## 3. Struktur JWT

JWT terdiri dari tiga bagian utama:

1. Header
2. Payload
3. Signature

Ketiga bagian tersebut dipisahkan menggunakan tanda titik (`.`).

Bentuk sederhananya:

```text
header.payload.signature

Contoh bentuk JWT:

xxxxx.yyyyy.zzzzz


---

4. Header

Header berisi informasi mengenai token, terutama jenis token dan algoritma yang digunakan untuk membuat signature.

Contoh:

{
  "alg": "HS256",
  "typ": "JWT"
}

Keterangan:

alg menunjukkan algoritma yang digunakan.

typ menunjukkan tipe token, yaitu JWT.


Contoh algoritma yang dapat digunakan antara lain:

HS256

HS384

HS512

RS256

RS384

RS512



---

5. Payload

Payload berisi data atau claims yang ingin disimpan di dalam JWT.

Contoh:

{
  "sub": "12345",
  "name": "Zidan",
  "role": "user"
}

Payload dapat berisi informasi seperti:

ID pengguna

Username

Role

Waktu pembuatan token

Waktu kedaluwarsa token


Payload disebut sebagai claims.

Contoh Registered Claims

Beberapa claim yang umum digunakan:

iss — issuer atau pihak yang menerbitkan token.

sub — subject atau identitas utama pengguna.

aud — audience atau pihak yang menjadi tujuan token.

exp — expiration time atau waktu kedaluwarsa token.

iat — issued at atau waktu token dibuat.

nbf — not before atau waktu token mulai berlaku.

jti — JWT ID atau identitas unik token.


Contoh:

{
  "iss": "datadigi",
  "sub": "12345",
  "role": "user",
  "iat": 1730000000,
  "exp": 1730003600
}


---

6. Signature

Signature digunakan untuk membantu memastikan bahwa token tidak diubah setelah dibuat oleh pihak yang menerbitkannya.

Secara sederhana, signature dibuat berdasarkan:

Header

Payload

Secret atau private key


Contoh konsep:

HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret
)

Jika payload atau bagian token diubah tanpa menghasilkan signature yang valid, server dapat menolak token tersebut.


---

7. Cara Kerja JWT pada Login

Contoh alur autentikasi menggunakan JWT:

Tahap 1 — User Login

User mengirim username dan password kepada server.

POST /api/login

Contoh request:

{
  "username": "zidan",
  "password": "password123"
}

Tahap 2 — Server Memeriksa Login

Server memeriksa apakah username dan password sesuai dengan data pengguna.

Jika data benar, server membuat JWT.

Tahap 3 — Server Mengirim JWT

Server memberikan response kepada client:

{
  "message": "Login berhasil",
  "token": "eyJhbGciOiJIUzI1NiIs..."
}

Tahap 4 — Client Menyimpan Token

Client menyimpan token sesuai dengan mekanisme penyimpanan yang aman.

Tahap 5 — Client Mengirim Token

Ketika ingin mengakses endpoint yang membutuhkan autentikasi, client mengirim token melalui HTTP header.

Contoh:

Authorization: Bearer eyJhbGciOiJIUzI1NiIs...

Tahap 6 — Server Memvalidasi Token

Server memeriksa:

Apakah token memiliki format yang benar.

Apakah signature valid.

Apakah token belum kedaluwarsa.

Apakah token memenuhi aturan autentikasi yang diperlukan.


Jika valid, request dapat diproses.


---

8. Contoh Penggunaan JWT pada REST API

Misalnya terdapat API untuk sistem toko.

Endpoint login:

POST /api/login

Endpoint untuk mendapatkan data profile:

GET /api/profile

User terlebih dahulu melakukan login:

{
  "username": "zidan",
  "password": "password123"
}

Setelah berhasil login, server memberikan JWT.

Kemudian client mengirim request:

GET /api/profile
Authorization: Bearer <JWT_TOKEN>

Server memvalidasi token tersebut.

Jika valid, server memberikan data profile:

{
  "id": 10,
  "name": "Zidan",
  "role": "user"
}


---

9. JWT dan Session

JWT dan session sama-sama dapat digunakan untuk autentikasi, tetapi cara kerjanya berbeda.

Session

Pada sistem session, server biasanya menyimpan informasi session pengguna.

Client mendapatkan session identifier yang kemudian digunakan untuk mengidentifikasi session tersebut.

JWT

Pada sistem JWT, server memberikan token yang berisi claims dan dapat digunakan oleh client pada request berikutnya.

Server kemudian melakukan validasi token tersebut.

Secara sederhana:

Session:
Client → Session ID → Server → Session Data

JWT:
Client → JWT → Server → Validasi Token


---

10. Kelebihan JWT

Beberapa kelebihan JWT:

1. Mudah digunakan untuk API

JWT cocok digunakan pada REST API karena token dapat dikirim melalui HTTP request.

2. Mendukung sistem terdistribusi

JWT dapat digunakan pada sistem yang memiliki beberapa service, selama service tersebut dapat memvalidasi token sesuai aturan yang digunakan.

3. Memiliki format yang ringkas

JWT menggunakan format yang relatif ringkas sehingga mudah dikirim melalui HTTP.

4. Dapat membawa informasi

JWT dapat membawa claims seperti user ID dan role.

5. Tidak membutuhkan session data yang sama pada setiap request

Dalam pola penggunaan tertentu, server dapat memvalidasi token tanpa harus mengambil session pengguna untuk setiap request.


---

11. Kekurangan dan Risiko JWT

JWT juga memiliki beberapa kekurangan dan risiko.

1. Token yang sudah diterbitkan tidak selalu mudah dibatalkan

Jika token masih valid dan belum kedaluwarsa, sistem perlu memiliki mekanisme tambahan jika ingin mencabut akses token tersebut sebelum waktunya.

2. Payload bukan tempat untuk menyimpan data rahasia

JWT dapat di-encode sehingga isinya dapat dibaca oleh pihak yang memperoleh token.

Karena itu, jangan menyimpan informasi sensitif seperti:

Password

Nomor kartu

Secret key

Data pribadi yang tidak diperlukan


3. Token yang bocor dapat disalahgunakan

Jika seseorang mendapatkan token yang masih valid, token tersebut dapat digunakan sampai token tidak lagi valid atau dicabut sesuai mekanisme aplikasi.

4. Ukuran token dapat menjadi besar

Jika terlalu banyak informasi dimasukkan ke dalam payload, ukuran token dapat bertambah dan membuat request menjadi lebih besar.


---

12. JWT Bukan Enkripsi

Hal yang penting untuk dipahami adalah:

JWT tidak secara otomatis berarti data di dalamnya terenkripsi.

Bagian header dan payload umumnya dapat di-decode oleh pihak yang memiliki token.

Signature digunakan untuk membantu memverifikasi bahwa token tidak dimodifikasi dan berasal dari pihak yang memiliki kunci yang sesuai.

Jika aplikasi membutuhkan kerahasiaan data, mekanisme enkripsi yang sesuai harus digunakan.


---

13. Access Token dan Refresh Token

Dalam sistem autentikasi modern, JWT dapat digunakan sebagai access token.

Access Token

Access token digunakan untuk mengakses resource atau endpoint yang membutuhkan autentikasi.

Biasanya access token dibuat dengan masa berlaku yang relatif singkat.

Contoh:

Access Token
↓
Digunakan untuk mengakses API
↓
Kadaluarsa

Refresh Token

Refresh token dapat digunakan untuk mendapatkan access token baru tanpa meminta user login kembali.

Contoh alur:

Login
  ↓
Access Token + Refresh Token
  ↓
Access Token digunakan
  ↓
Access Token kadaluarsa
  ↓
Refresh Token digunakan
  ↓
Access Token baru

Penggunaan refresh token harus dirancang dan diamankan dengan baik.


---

14. Contoh Endpoint yang Menggunakan JWT

Contoh API:

POST   /api/login
GET    /api/profile
GET    /api/products
POST   /api/products
PUT    /api/products/{id}
DELETE /api/products/{id}

Endpoint tertentu dapat membutuhkan JWT.

Contohnya:

GET /api/profile

Request:

Authorization: Bearer <JWT_TOKEN>

Jika token valid:

200 OK

Jika token tidak valid atau tidak tersedia:

401 Unauthorized


---

15. JWT pada Sistem dengan Role

JWT dapat membawa informasi role pengguna.

Contoh payload:

{
  "sub": "1001",
  "name": "Zidan",
  "role": "admin"
}

Server dapat menggunakan role tersebut untuk menentukan akses.

Contoh:

Admin
  ↓
Boleh mengelola produk

Staff
  ↓
Boleh melihat dan mengubah data tertentu

Customer
  ↓
Hanya boleh mengakses fitur customer

Namun, aplikasi tidak boleh hanya mempercayai data dari client tanpa melakukan validasi token dan aturan akses di server.


---

16. Contoh JWT dalam Aplikasi Go

JWT juga sering digunakan dalam aplikasi yang dibuat menggunakan Go.

Contoh alur:

Client
  ↓
POST /login
  ↓
Go Server
  ↓
Validasi username & password
  ↓
Membuat JWT
  ↓
Client menerima JWT
  ↓
Client mengirim JWT pada request berikutnya
  ↓
Go Server memvalidasi JWT
  ↓
Request diproses

Dalam implementasi nyata, developer dapat menggunakan library JWT yang sesuai dengan kebutuhan aplikasi.


---

17. Status HTTP yang Berkaitan dengan JWT

Beberapa HTTP status code yang umum ditemukan:

200 OK

Request berhasil diproses.

201 Created

Resource baru berhasil dibuat.

400 Bad Request

Request tidak sesuai dengan format yang diperlukan.

401 Unauthorized

Request membutuhkan autentikasi atau token tidak valid.

403 Forbidden

User sudah dikenali tetapi tidak memiliki izin untuk mengakses resource tertentu.

Contoh:

401 → Belum terautentikasi / token tidak valid

403 → Sudah terautentikasi tetapi tidak memiliki permission


---

18. Best Practice Penggunaan JWT

Beberapa praktik yang baik dalam penggunaan JWT:

1. Gunakan HTTPS untuk melindungi komunikasi antara client dan server.


2. Jangan menyimpan password di dalam JWT.


3. Jangan menyimpan secret key di dalam payload.


4. Gunakan expiration time (exp) yang sesuai.


5. Gunakan secret key atau private key yang kuat.


6. Validasi signature token di server.


7. Validasi expiration token.


8. Batasi informasi yang dimasukkan ke payload.


9. Gunakan mekanisme refresh token jika diperlukan.


10. Rancang mekanisme pencabutan token jika aplikasi membutuhkannya.


11. Lindungi penyimpanan token pada sisi client.


12. Gunakan authorization selain hanya authentication.




---

19. Perbedaan Authentication dan Authorization

Authentication dan authorization merupakan dua konsep yang berbeda.

Authentication

Authentication menjawab pertanyaan:

> "Siapa pengguna ini?"



Contoh:

User login
↓
Username dan password benar
↓
User berhasil terautentikasi

Authorization

Authorization menjawab pertanyaan:

> "Apa yang boleh dilakukan pengguna ini?"



Contoh:

User = Admin
↓
Boleh menghapus produk

User = Customer
↓
Tidak boleh menghapus produk

JWT dapat membantu sistem membawa informasi yang dibutuhkan untuk kedua proses tersebut, tetapi aturan authorization tetap harus diterapkan oleh server.


---

20. Kesimpulan

JWT (JSON Web Token) adalah standar yang banyak digunakan untuk pertukaran informasi dan autentikasi pada aplikasi modern.

JWT terdiri dari tiga bagian utama:

Header.Payload.Signature

Header berisi informasi mengenai token dan algoritma, payload berisi claims, sedangkan signature digunakan untuk membantu memastikan integritas token.

JWT banyak digunakan pada REST API karena dapat dikirim melalui HTTP request dan dapat membawa informasi seperti user ID dan role.

Meskipun memiliki banyak keuntungan, JWT harus digunakan dengan benar. Informasi sensitif tidak boleh dimasukkan ke dalam payload hanya karena payload tersebut berada di dalam token. Sistem juga harus memperhatikan expiration, keamanan secret key, HTTPS, penyimpanan token, serta mekanisme authorization.

Dengan penggunaan yang tepat, JWT dapat menjadi salah satu bagian penting dalam sistem autentikasi dan keamanan API.

Setelah **copy-paste semuanya**, jangan commit dulu kalau belum yakin tampilannya benar. Kalau sudah masuk ke editor, baru kita lanjut ke **Commit changes** seperti file API tadi.
