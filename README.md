# SISTEM PERANCANGAN KEUANGAN SISWA/I DI SMK

Nama : Amanda Puspa Negara

NIM : 312210129

Kelas : TI.22.A.1

Mata Kuliah : Rekayasa Perangkat Lunak

Dosen Pengampu : Wahyu Hadikristanto, S.Kom., M.Kom.

## Membuat Kode Program

### 1. login.php

        <?php 
        include 'admin/koneksi.php';
        ?>
        <!DOCTYPE html>
        <html>
        <head>
          <meta charset="utf-8">
          <meta name="viewport" content="width=device-width, initial-scale=1">
          <title><?php echo $title; ?></title>
          <link rel="stylesheet" type="text/css" href="style.css">
        </head>
        <body>
          <div class="wrapper">
            <div class="logo">
              <img src="admin/assets/images/logo1.png" alt="">
            </div>
            <div class="text-center mt-4 name" style="font-size: 15px; text-align: center;">
              <?php echo $title; ?>
            </div>
            <form class="p-3 mt-3" method="POST" action="proses_login.php">
              <div class="form-field d-flex align-items-center">
                <span class="far fa-user"></span>
                <input type="text" name="username" id="userName" placeholder="Username">
              </div>
              <div class="form-field d-flex align-items-center">
                <span class="fas fa-key"></span>
                <input type="password" name="password" id="pwd" placeholder="Password">
              </div>
              <button class="btn mt-3" type="submit">Login</button>
            </form>
            <div class="text-center fs-6">
              <a href="#">Forget password?</a> or <a href="#">Sign up</a>
            </div>
          </div>
        </body>
        </html>
        
![Screenshot 2023-12-12 110453](https://github.com/amandaaaapn/sistem-perancangan-keuangan-siswa-i-di-smk/assets/115678845/842a96cc-43e0-4a42-ad91-a13d4abe8681)

### 2. proses_login.php

        <?php
        session_start();
        require_once("admin/koneksi.php");
        
        if ($_SERVER["REQUEST_METHOD"] == "POST") {
            $username = $_POST["username"];
            $password = md5($_POST["password"]); // Menggunakan MD5 untuk hash password
        
            $query = "SELECT * FROM tb_user WHERE username = '$username' AND password = '$password'";
            $result = mysqli_query($koneksi, $query);
        
            if ($result && mysqli_num_rows($result) == 1) {
                $row = mysqli_fetch_assoc($result);
        
                $_SESSION['login_type'] = "login";
                $_SESSION["id_user"] = $row["id_user"];
                $_SESSION["nama_user"] = $row["nama_lengkap"];
                $_SESSION["peran"] = $row["peran"];
        
                echo '<script language="javascript" type="text/javascript">
                    alert("Selamat Datang '.$_SESSION["nama_user"].', Anda Berhasil Login!");</script>';
                echo "<meta http-equiv='refresh' content='0; url=admin/index.php'>"; // Redirect ke halaman dashboard atau halaman lain sesuai kebutuhan
                exit();
            } else {
                echo '<script language="javascript" type="text/javascript">
                    alert("Maaf Username dan Password Salah.!");</script>';
                echo "<meta http-equiv='refresh' content='0; url=index.php'>";
            }
        }
        ?>

### 3. koneksi.php

        <?php 
        $host = "localhost";
        $user = "root";
        $pass = "";
        $db = "dbspp";
        
        $koneksi = new mysqli($host, $user, $pass, $db);
        
        $title = "Aplikasi Pembayaran SPP"
        
        ?>
