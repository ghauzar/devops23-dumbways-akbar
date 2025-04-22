# Manage Server with Terminal

## Akses Server Menggunakan Windows Terminal 💻

### 1. Cek alamat IP Server
![Cek IP server](assets/images/1.png)

### 2. Buka terminal Windows dan ketik command berikut untuk akses Server di VM
```
ssh <username>@<ip_address>
```
![Buka terminal](assets/images/1a.png)
![Coba koneksi server](assets/images/1b.png)

#### Diketahui dari gambar sebelumnya bahwa  koneksi ke server ditolak, sebab OpenSSH belum terinstal di server

### 3. Install OpenSSH di Server
```
sudo apt install openssh-server
```
![Install SSH Server](assets/images/2.png)
![Install SSH Server](assets/images/2a.png)

### 4. Ceka apakah SSH sudah running
```
sudo systemctl status ssh
```
![Cek status SSH](assets/images/3.png)

### 5. Kembali ke terminal Windows dan menguji koneksi SSH dengan Server. Password yang digunakan untuk login sama dengan password yang digunakan untuk login di terminal Server
```
ssh akb@192.168.1.9
```
![Cek status SSH](assets/images/4.png)

## Konfigurasi Akses SSH Menggunakan Public Key 🔒
### 1. Generate Public Key dan Private Key di Terminal Windows (Nama Key = "kunci_dumbways")
```
ssh-keygen
```
![Generate Key di Terminal](assets/images/5.png)

### 2. Buka Folder "C:\Users\<nama_user>\.ssh\" dan terdapat 2 key di mana 1 merupakan Public key (ekstensi .pub) dan 1 lagi Private Key. Private Key harus disimpan baik-baik dan harus dirahasiakan.
![Direktori Key](assets/images/6.png)

### 3. Buka file Public Key dengan notepad dan salin isinya
![Menyalin isi Public Key](assets/images/7.png)

### 4. Login kembali ke server dengan Windows Terminal, dan membuka file "authorized_keys" di direktori ~/.ssh
```
cd .ssh/
ls
sudo nano authorized_keys
```
![Buka authorized keys](assets/images/8.png)

### 5. Paste kan Public Key pada file "authorized_keys" di server Ubuntu dan simpan
![Buka authorized keys](assets/images/9.png)

### 6. Uji coba koneksi ke Server dengan SSH menggunakan Public Key di Windows Terminal. Eksekusi command berikut:
```
ssh -i .ssh/kunci_dumbways akb@192.168.1.9
```
![Buka authorized keys](assets/images/11.png)

### 7. Agar hanya dapat melakukan login dengan Public Key, maka perlu melakukan konfigurasi pada file konfigurasi SSH
```
sudo nano /etc/ssh/sshd_config
```
![Edit konfigurasi SSH](assets/images/12.png)

### 8. Atur parameter sebagai berikut. Setelah selesai simpan file tersebut.
    1. PubkeyAuthentication yes
    2. PasswordAuthentication no

- <code>PubkeyAuthentication</code> ➡️ mengizinkan autentikasi via SSH key.
- <code>PasswordAuthentication</code> ➡️ menonaktifkan login via password.

![Edit konfigurasi SSH](assets/images/12a.png)


### 9. Restart SSH Service pada terminal
```
sudo systemctl restart sshd
```
### 10. Disconnect SSH dengan mengetikkan "exit" di terminal Windows dan coba login ke Server dengan password:
![Edit konfigurasi SSH](assets/images/13.png)

### 11. Diketahui bahwa server menolak login menggunakan password, dan login hanya bisa menggunakan Public Key
```
ssh -i .ssh/kunci_dumbways akb@192.168.1.9
```
![Edit konfigurasi SSH](assets/images/14.png)



## Text Manipulation (<code>grep</code>, <code>sed</code>, <code>cat</code>, dan <code>echo</code>)

### 1. <code>grep</code>
#### Mencari teks pada file tertentu
```
grep hey file1
```
![grep cari teks](assets/images/19.png)


#### Menghitung berapa baris yang mengandung teks sesuai dengan pola teks pada command
```
grep -c hello file3
```
![grep hitung baris dengan kemunculan teks](assets/images/20.png)

#### Mencari teks yang muncul pada baris dalam setiap file di dalam direktori yang sedang aktif
```
grep hello *
```
![grep cari kemunculan teks pada suatu direktori](assets/images/21.png)

#### Menghitung jumlah baris yang mengandung teks sesuai pola teks command pada setiap file yang terletak di direktori aktif
```
grep -c hello *
```
![grep cari jumlah baris yang mengandung teks yang dicari pada setiap file di direktori aktif](assets/images/22.png)


### 2. <code>sed</code>
#### Untuk memanipulasi teks stream
```
sed -i 's/hello/hey/g' file1
```
- <code>sed</code> ➡️ command stream editor, untuk memanipulasi teks
- <code>-i</code> ➡️ <i>in-place edit</i>, artinya file aslinya akan diubah langsung
- <code>'s/hello/hey/g'</code> ➡️ ganti kata "hello" dengan "hey"
- <code>s</code> ➡️ akronim dari <i>substitute</i>
- <code>g</code> ➡️ akronim dari <i>global</i>, ganti semua kemunculan dalam satu baris (bukan hanya yang pertama)
  
![sed](assets/images/18.png)

### 3. <code>cat</code>
#### Melihat isi dari suatu file
```
cat file2
```
![cat lihat isi file](assets/images/15.png)

#### Membuat file baru dengan isi sesuai teks yang diinputkan
```
cat > file1
```
![cat buat file](assets/images/16.png)

#### Menggabungkan / menyisipkan teks dalam beberapa file ke suatu file
```
cat file1 file2 > file3
```
![cat buat file](assets/images/17.png)


### 4. <code>echo</code>
#### Menampilkan teks biasa
```
echo "Hello Dumbways DevOps"
```
![echo menampilkan teks ](assets/images/23.png)

#### Menampilkan isi variabel
```
nama="Akbar"
echo "Nama saya adalah $nama"
```
![echo menampilkan teks ](assets/images/24.png)

#### Menimpa isi suatu file (overwrite)
```
echo "hai DumbWays" > file1
```
![echo menampilkan teks ](assets/images/25.png)

#### Menambahkan teks ke baris baru dari suatu file (append)
```
echo "DevOps DumbWays" >> file3
```
![echo menampilkan teks ](assets/images/26.png)


## Menyalakan Uncomplicated Firewall (<code>ufw</code>) dan Manajemen Port
### 1. Menyalakan UFW
```
sudo ufw enable
```
![firewall ](assets/images/27.png)


### 2. Mengizinkan OpenSSH
```
sudo ufw allow "OpenSSH"
```
![firewall ](assets/images/28.png)


### 3. Mengizinkan Port 22, 80, 443, 3000, 5000, dan 6969
```
sudo ufw allow 22
sudo ufw allow 80
sudo ufw allow 443
sudo ufw allow 3000
sudo ufw allow 5000
sudo ufw allow 6969
```
![firewall ](assets/images/29.png)
![firewall ](assets/images/30.png)
