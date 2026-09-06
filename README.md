# Minpro-1-PBO-PersonalSubscriptionTracker

   +-------------------------+
   | Nama : Muhammad Fahriel |
   | NIM  : 2509116050       |  
   +-------------------------+
Aplikasi berbasis CLI yang dibangun dengan bahasa pemrograman Java untuk mencatat, mengelola, dan memantau pengeluaran biaya langganan bulanan pribadi.

## Deskripsi Singkat Program

Program Personal Subscription Tracker mengelola data langganan digital pengguna, seperti layanan streaming hiburan, musik, maupun penyimpanan cloud. Program ini menerapkan prinsip dasar Pemrograman Berorientasi Objek (PBO), khususnya enkapsulasi (encapsulation) dan relasi agregasi/komposisi antarkelas:

- `Langganan`: Kelas utama penyimpan detail langganan (ID langganan, objek Layanan, harga bulanan, objek MetodePembayaran, tanggal tagihan, dan status).
- `Layanan`: Kelas penyimpan identitas layanan (ID layanan, nama layanan, dan kategori).
- `MetodePembayaran`: Kelas penyimpan metode pembayaran (ID metode, nama metode, dan jenis).
- `Minpro1PBOPersonalSubscriptionTracker`: Kelas pengendali alur program berbasis menu interaktif dan penyimpan data dinamis menggunakan `ArrayList`.

## Penjelasan Alur Program

Program berjalan dalam perulangan menu utama berbasis CLI sampai pengguna memilih menu keluar (pilihan 6):

1. **Inisialisasi Data Awal**
   Saat program mulai berjalan, metode `inisialisasiDataAwal()` mengisi beberapa data awal (default) untuk daftar layanan (Netflix, Spotify, iCloud), metode pembayaran (GoPay, Kartu Kredit), serta data langganan aktif.

2. **Menu 1: Tampilkan Daftar Langganan**
   Program memeriksa apakah daftar langganan kosong. Jika berisi data, program menampilkan seluruh langganan yang tercatat, meliputi ID, nama layanan beserta kategori, harga per bulan, metode pembayaran, tanggal jatuh tempo tagihan, dan status keaktifan langganan.

3. **Menu 2: Tambah Langganan Baru**
   - Menampilkan penanda ID langganan terakhir untuk memandu penomoran ID baru.
   - Melakukan pengecekan duplikasi ID. Jika ID sudah ada di dalam list, pendaftaran dibatalkan.
   - Menampilkan daftar pilihan layanan. Pengguna dapat memilih layanan yang sudah ada atau mendaftarkan entitas layanan baru langsung di tempat.
   - Menampilkan daftar pilihan metode pembayaran, dengan opsi memilih yang sudah ada atau mendaftarkan metode baru langsung di tempat.
   - Meminta input harga bulanan dan tanggal tagihan (1–31) yang dilengkapi validasi tipe data angka.
   - Menyimpan objek `Langganan` baru ke dalam `listLangganan`.

4. **Menu 3: Edit Status & Harga**
   Pengguna memasukkan ID langganan yang ingin diubah. Jika ditemukan, program menampilkan detail saat ini dan memberi opsi:
   - Mengubah nominal harga bulanan.
   - Mengubah status langganan antara `Aktif` atau `Nonaktif`.

5. **Menu 4: Batalkan/Hapus Langganan**
   Pengguna memasukkan ID langganan yang ingin dihapus. Program mencari ID tersebut di dalam list dan menghapus objek terkait jika ditemukan.

6. **Menu 5: Hitung Total Pengeluaran Bulanan**
   Program menghitung akumulasi biaya bulanan hanya dari langganan yang berstatus `Aktif`. Program juga menampilkan jumlah layanan aktif serta ringkasan evaluasi pengeluaran apabila total biaya bulanan melampaui batas Rp 500.000.

7. **Menu 6: Keluar**
   Mengakhiri perulangan program dan menutup scanner input.

## Penjelasan Letak Penerapan Nilai Tambah

1. **Relasi Antar Objek (Komposisi / Agregasi Objek)**
   - Kelas `Langganan` tidak sekadar menyimpan data bertipe primitif atau string polos, melainkan menampung referensi objek dari kelas `Layanan` dan kelas `MetodePembayaran`.
   - Lokasi: File `Langganan.java`, baris atribut `private Layanan layanan;` dan `private MetodePembayaran metode;`.

2. **Pendaftaran Entitas Baru Secara Inline (On-the-Fly)**
   - Pengguna tidak dibatasi hanya pada data awal yang telah disediakan. Saat menambahkan langganan baru, pengguna dapat langsung mendaftarkan `Layanan` baru maupun `MetodePembayaran` baru tanpa harus keluar dari alur penambahan langganan.
   - Lokasi: File `Minpro1PBOPersonalSubscriptionTracker.java`, method `tambahLangganan()`.

3. **Indikator ID Terakhir Dinamis**
   - Saat meminta input ID baru untuk langganan, layanan, dan metode pembayaran, program menampilkan ID terakhir yang terdaftar secara dinamis (`ID TERAKHIR = ...`). Hal ini mencegah pengguna menebak-nebak ID sebelumnya dan meminimalkan kesalahan input duplikat.
   - Lokasi: File `Minpro1PBOPersonalSubscriptionTracker.java`, method `tambahLangganan()`.

4. **Validasi dan Defensive Programming pada Setter**
   - Setter pada kelas `Langganan` menerapkan pengecekan nilai: harga bulanan tidak boleh bernilai negatif (otomatis diubah menjadi 0 jika negatif), dan tanggal tagihan dibatasi pada rentang valid kalender 1 hingga 31 (otomatis default ke 1 jika di luar rentang).
   - Penanganan input Scanner juga menggunakan `hasNextInt()` dan `hasNextDouble()` untuk mencegah crash akibat ketidaksesuaian format data (`InputMismatchException`).
   - Lokasi: File `Langganan.java`, method `setHargaBulanan()` dan `setTanggalTagihan()`.

5. **Analisis Ambang Batas Pengeluaran**
   - Pada fitur perhitungan biaya bulanan, program memberikan peringatan evaluasi jika total tagihan langganan aktif pengguna melebihi Rp 500.000 per bulan.
   - Lokasi: File `Minpro1PBOPersonalSubscriptionTracker.java`, method `hitungTotalPengeluaran()`.
