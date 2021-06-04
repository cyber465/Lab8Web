# Lab8Web

# Membuat Database: Studi Kasus Data Barang
# Membuat Database
***

CREATE DATABASE latihan1;

***
# Membuat Tabel

***

CREATE TABLE data_barang (
id_barang int(10) auto_increment Primary Key,
kategori varchar(30),
nama varchar(30),
gambar varchar(100),
harga_beli decimal(10,0),
harga_jual decimal(10,0),
stok int(4)
);

***

# Menambahkan data

***

INSERT INTO data_barang (kategori, nama, gambar, harga_beli, harga_jual, stok)
VALUES ('Elektronik', 'HP Samsung Android', 'hp_samsung.jpg', 2000000, 2400000, 5),
('Elektronik', 'HP Xiaomi Android', 'hp_xiaomi.jpg', 1000000, 1400000, 5),
('Elektronik', 'HP OPPO Android', 'hp_oppo.jpg', 1800000, 2300000, 5);

***

# Membuat Program CRUD
Buat folder lab8_php_database pada root directory web server (d:\xampp\htdocs)

# Membuat file koneksi database
Buat file baru dengan nama koneksi.php

![1](https://user-images.githubusercontent.com/37741274/120816438-eeeb1d80-c57a-11eb-9c8d-8856bff674ec.png)

# Membuat file index untuk menampilkan data (Read)
Buat file baru dengan nama index.php

![2](https://user-images.githubusercontent.com/37741274/120816792-47bab600-c57b-11eb-9884-2c0aa5b282bf.png)

![3](https://user-images.githubusercontent.com/37741274/120816951-720c7380-c57b-11eb-8a69-de9cdad77eb1.png)

# Menambah Data (Create)
Buat file baru dengan nama tambah.php

***
<?php
error_reporting(E_ALL);
include_once 'koneksi.php';
if (isset($_POST['submit']))
{
$nama = $_POST['nama'];
$kategori = $_POST['kategori'];
$harga_jual = $_POST['harga_jual'];
$harga_beli = $_POST['harga_beli'];
$stok = $_POST['stok'];
$file_gambar = $_FILES['file_gambar'];
$gambar = null;
if ($file_gambar['error'] == 0)
{
$filename = str_replace(' ', '_',$file_gambar['name']);
$destination = dirname(__FILE__) .'/gambar/' . $filename;
if(move_uploaded_file($file_gambar['tmp_name'], $destination))
{
$gambar = 'gambar/' . $filename;;
}
}
$sql = 'INSERT INTO data_barang (nama, kategori,harga_jual, harga_beli,
stok, gambar) ';
$sql .= "VALUE ('{$nama}', '{$kategori}','{$harga_jual}',
'{$harga_beli}', '{$stok}', '{$gambar}')";
$result = mysqli_query($conn, $sql);
header('location: index.php');
}

***

![4](https://user-images.githubusercontent.com/37741274/120817485-f6f78d00-c57b-11eb-9e0c-b13893a19400.png)

# Mengubah Data (Update)
Buat file baru dengan nama ubah.php

***

<?php
error_reporting(E_ALL);
include_once 'koneksi.php';
if (isset($_POST['submit']))
{
$id = $_POST['id'];
$nama = $_POST['nama'];
$kategori = $_POST['kategori'];
$harga_jual = $_POST['harga_jual'];
$harga_beli = $_POST['harga_beli'];
$stok = $_POST['stok'];
$file_gambar = $_FILES['file_gambar'];
$gambar = null;
if ($file_gambar['error'] == 0)
{
$filename = str_replace(' ', '_', $file_gambar['name']);
$destination = dirname(__FILE__) . '/gambar/' . $filename;
if (move_uploaded_file($file_gambar['tmp_name'], $destination))
{
$gambar = 'gambar/' . $filename;;
}

![5](https://user-images.githubusercontent.com/37741274/120817978-62415f00-c57c-11eb-8849-15d6c756f332.png)

***

# Menghapus Data (Delete)
Buat file baru dengan nama hapus.php

***

<?php
include_once 'koneksi.php';
$id = $_GET['id'];
$sql = "DELETE FROM data_barang WHERE id_barang = '{$id}'";
$result = mysqli_query($conn, $sql);
header('location: index.php');
?>

***
















