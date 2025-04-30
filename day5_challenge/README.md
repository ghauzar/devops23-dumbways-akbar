# Membuat Server NodeJS dan Python Flask Berjalan di Background
## 1. Install [pm2](https://pm2.keymetrics.io/) dengan perintah berikut:
```
npm install pm2@latest -g
```
![image](img/1.png)
![image](img/2.png)

## 2. Menjalankan server NodeJS pada direktori `wayshub-frontend` dengan menggunakan `pm2` dan menamai proses ini sebagai `server-node` untuk dijalankan di background:
```
cd wayshub-frontend
```
```
pm2 start npm --name server-node -- start
```
![image](img/3.png)

## 3. Pindah ke file server Python berada di direktori `python_day_task_5`, menjalankan server Python dengan nama proses `server-python` untuk dijalankan di background:
```
cd ..
```
```
cd python_day_task_5
```
```
ls
```
```
pm2 start index.py --interpreter python3 --name server-python
```
![image](img/4.png)

## Hasil dari eksekusi server NodeJS dan Python adalah sebagai berikut, kedua server dapat berjalan di background:
![image](img/simulate.gif)


# Golang Bisa Dibuka di Browser
## 1. Menuju ke direktori `goloang_day_task_5`, kemudian membuat file yang menjadi server dari bahasa Golang dengan nama `web.go`
```
cd golang_day_task_5
```
```
nano web.go
```
![image](img/5.png)

## 2. Memasukkan kode snippet web server bahasa Go sederhana seperti kode berikut:
```
package main

import (
        "fmt"
        "log"
        "net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
        fmt.Fprintln(w, "Golang geming! 🎮")
}

func main() {
        http.HandleFunc("/", handler)
        port := "8080"
        fmt.Println("Server is running on port", port)
        log.Fatal(http.ListenAndServe(":"+port, nil))
}
```
![image](img/6.png)

## 3. Simpan file `web.go` kemudian jalankan dengan perintah:
```
go run web.go
```
## Maka output akan  seperti ini 
                                            
![image](img/7.png)

## 4. Buka browser dan akses ke alamat `192.168.1.9:8080`

![image](img/8.png)

