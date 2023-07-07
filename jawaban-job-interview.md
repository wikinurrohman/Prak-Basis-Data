# JAWABAN UTS PRAKTIKUM BASIS DATA
# Nomor 1
Perancangan database diagram traveloka berdasarkan permasalahan dunia nyata meliputi beberapa transaksi seperti pemesanan tiket pesawat dan booking hotel.
![Untitled (2)](https://github.com/wikinurrohman/Prak-Basis-Data/assets/95328207/ff5fcb9f-5034-43fa-aeb4-5ee5985cba51)

# Nomor 2
# DDL (Data Definition Language)
Pembuatan tabel berdasarkan diagram pada nomor 1 dengan mengekspor DBML pada dbdiagram menjadi DDL MySQL
```SQL
CREATE TABLE `Pengguna` (
  `id_pengguna` int PRIMARY KEY,
  `nama_pengguna` varchar(255),
  `email` varchar(255),
  `kata_sandi` varchar(255),
  `nama_depan` varchar(255),
  `nama_belakang` varchar(255),
  `nomor_telepon` varchar(255),
  `alamat` varchar(255),
  `jenis_kelamin` enum
);

CREATE TABLE `Hotel` (
  `id_hotel` int PRIMARY KEY,
  `nama_hotel` varchar(255),
  `alamat` varchar(255),
  `kota` varchar(255),
  `negara` varchar(255),
  `peringkat_bintang` decimal,
  `fasilitas` varchar(255),
  `deskripsi` varchar(255),
  `rata_rata_peringkat` decimal
);

CREATE TABLE `Penerbangan` (
  `id_penerbangan` int PRIMARY KEY,
  `maskapai_penerbangan` varchar(255),
  `bandara_keberangkatan` varchar(255),
  `bandara_kedatangan` varchar(255),
  `tanggal_keberangkatan` date,
  `tanggal_kedatangan` date,
  `waktu_keberangkatan` time,
  `waktu_kedatangan` time,
  `harga` decimal,
  `ketersediaan_kursi` int,
  `jenis_pesawat` varchar(255),
  `maskapai_penerbangan_fk` varchar(255)
);

CREATE TABLE `MaskapaiPenerbangan` (
  `id_maskapai` int PRIMARY KEY,
  `nama_maskapai` varchar(255),
  `kode_maskapai` varchar(255),
  `negara_asal` varchar(255)
);

CREATE TABLE `Pemesanan` (
  `id_pemesanan` int PRIMARY KEY,
  `id_pengguna` int,
  `tanggal_pemesanan` date,
  `total_harga` decimal,
  `status` varchar(255),
  `id_pengguna_fk` int
);

CREATE TABLE `PemesananHotel` (
  `id_pemesanan_hotel` int PRIMARY KEY,
  `id_pemesanan` int,
  `id_hotel` int,
  `tanggal_check_in` date,
  `tanggal_check_out` date,
  `jumlah_kamar` int,
  `jumlah_tamu` int,
  `id_pemesanan_fk` int,
  `id_hotel_fk` int
);

CREATE TABLE `PemesananPenerbangan` (
  `id_pemesanan_penerbangan` int PRIMARY KEY,
  `id_pemesanan` int,
  `id_penerbangan` int,
  `jumlah_penumpang` int,
  `id_pemesanan_fk` int,
  `id_penerbangan_fk` int
);

CREATE TABLE `Pembayaran` (
  `id_pembayaran` int PRIMARY KEY,
  `id_pemesanan` int,
  `tanggal_pembayaran` date,
  `jumlah` decimal,
  `metode_pembayaran` varchar(255),
  `status_pembayaran` varchar(255),
  `id_pemesanan_fk` int
);

CREATE TABLE `Review` (
  `id_review_hotel` int,
  `id_review_penerbangan` int,
  `id_pengguna` int,
  `id_hotel` int,
  `id_penerbangan` int,
  `tanggal_review` date,
  `rating` decimal,
  `komentar` varchar(255),
  `id_pengguna_fk` int,
  `id_hotel_fk` int,
  `id_penerbangan_fk` int,
  PRIMARY KEY (`id_review_hotel`, `id_review_penerbangan`)
);

ALTER TABLE `Penerbangan` ADD FOREIGN KEY (`maskapai_penerbangan_fk`) REFERENCES `MaskapaiPenerbangan` (`id_maskapai`);

ALTER TABLE `Pemesanan` ADD FOREIGN KEY (`id_pengguna_fk`) REFERENCES `Pengguna` (`id_pengguna`);

ALTER TABLE `PemesananHotel` ADD FOREIGN KEY (`id_pemesanan_fk`) REFERENCES `Pemesanan` (`id_pemesanan`);

ALTER TABLE `PemesananHotel` ADD FOREIGN KEY (`id_hotel_fk`) REFERENCES `Hotel` (`id_hotel`);

ALTER TABLE `PemesananPenerbangan` ADD FOREIGN KEY (`id_pemesanan_fk`) REFERENCES `Pemesanan` (`id_pemesanan`);

ALTER TABLE `PemesananPenerbangan` ADD FOREIGN KEY (`id_penerbangan_fk`) REFERENCES `Penerbangan` (`id_penerbangan`);

ALTER TABLE `Pembayaran` ADD FOREIGN KEY (`id_pemesanan_fk`) REFERENCES `Pemesanan` (`id_pemesanan`);

ALTER TABLE `Review` ADD FOREIGN KEY (`id_pengguna_fk`) REFERENCES `Pengguna` (`id_pengguna`);

ALTER TABLE `Review` ADD FOREIGN KEY (`id_hotel_fk`) REFERENCES `Hotel` (`id_hotel`);

ALTER TABLE `Review` ADD FOREIGN KEY (`id_penerbangan_fk`) REFERENCES `Penerbangan` (`id_penerbangan`);

```

