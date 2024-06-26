# Sisop-1-2024-MH-IT26

## ***KELOMPOK IT 26***
  | Nama      | NRP         |
  |-----------|-------------|
  | Rafael Jonathan Arnoldus   | 5027231006  |
  | Muhammad Abhinaya Al-Faruqi  | 5027231011  |  
  | Danendra Fidel Khansa  | 5027231063  |

## Bagian Pengerjaan Soal 
+ Soal 1 = Danendra Fidel Khansa
+ Soal 2 = Rafael Jonathan Arnoldus
+ Soal 3 = Muhammad Abhinaya Al-Faruqi
+ Soal 4 = Revisi ALL

## ***MODUL 1***
  Berikut untuk struktur repository pengumpulan dari hasil praktikum sistem operasi modul 1 :
```
—soal_1:
  	— Sandbox.sh
                                    
—soal_2:
  	— Login.sh
	— Register.sh
				
—soal_3:
  	— awal.sh
	— search.sh
				
—soal_4:
	— aggregate_minutes_to_hourly_log.sh
	— minute_log.sh
```
---
## ***SOAL 1 (Fidel)***
Cipung dan abe ingin mendirikan sebuah toko bernama “SandBox”, sedangkan kamu adalah manajer penjualan yang ditunjuk oleh Cipung dan Abe untuk melakukan pelaporan penjualan dan strategi penjualan kedepannya yang akan dilakukan.

Setiap tahun Cipung dan Abe akan mengadakan rapat dengan kamu untuk mengetahui laporan dan strategi penjualan dari “SandBox”. Buatlah beberapa kesimpulan dari data penjualan “Sandbox.csv” untuk diberikan ke cipung dan abe 

a. Karena Cipung dan Abe baik hati, mereka ingin memberikan hadiah kepada customer yang telah belanja banyak. Tampilkan nama pembeli dengan total sales paling tinggi

b. Karena karena Cipung dan Abe ingin mengefisienkan penjualannya, mereka ingin merencanakan strategi penjualan untuk customer segment yang memiliki profit paling kecil. Tampilkan customer segment yang memiliki profit paling kecil

c. Cipung dan Abe hanya akan membeli stok barang yang menghasilkan profit paling tinggi agar efisien. Tampilkan 3 category yang memiliki total profit paling tinggi 

d. Karena ada seseorang yang lapor kepada Cipung dan Abe bahwa pesanannya tidak kunjung sampai, maka mereka ingin mengecek apakah pesanan itu ada. Cari purchase date dan amount (quantity) dari nama adriaens

## ***PENGERJAAN***
```
#!/bin/bash

wget --no-check-certificate -O Sandbox.csv 'https://drive.google.com/uc?id=1cC6MYBI3wRwDgqlFQE1OQUN83JAreId0&export=download'

cat Sandbox.csv

awk -F ',' '{print NF; exit}' Sandbox.csv

head -n 1 Sandbox.csv

awk -F ',' 'NR>1{sales[$6]+=$17} END{max_sales=0; for (customer in sales) {if (sales[customer] > max_sales) {max_sales = sales[customer]; max_customer = customer}} print "Customer dengan total sales tertinggi adalah " max_customer ", yaitu dengan total sales sebesar " max_sales}' Sandbox.csv > 1A.txt

awk -F ',' 'NR>1{profit[$7]+=$20} END{min_profit=1000000; segment_terkecil=""; for (segment in profit) {if (profit[segment]<min_profit) {min_profit=profit[segment]; segment_terkecil=segment}} print "Customer segment dengan profit terkecil adalah:", segment_terkecil, "dengan profit sebesar", min_profit}' Sandbox.csv > 1B.txt

awk -F ',' 'NR > 1 {sum[$14]+=$20} END {print "Profit 3 tertinggi diantara seluruh category"; for (category in sum) print category ", " sum[category] }' Sandbox.csv  > 1C.txt

awk -F ',' '/Adriaens/ {print "Pesanan " $6 " pada tanggal " $2 " dan sejumlah " $18}' Sandbox.csv > 1D.txt
```
---
## ***PENJELASAN PENGERJAAN***
## *Pengunduhan dan Pengecekan kelengkapan file*
- Langkah awal adalah mendownload file dari link google drive yang ada di soal dengan cara menggunakan command 'wget' lalu '--no-check-certificate -O' kemudian beri nama filenya dengan 'Sandbox.csv' dan terakhir masukan link google drive tersebut.
```
wget --no-check-certificate -O Sandbox.csv 'https://drive.google.com/uc?id=1cC6MYBI3wRwDgqlFQE1OQUN83JAreId0&export=download'
```
`Setelah command diatas dijalankan maka akan muncul file bernama "Sandbox.csv" yang akan tersimpan didalam direktori sesuai yang kita tuju`
- Langkah kedua adalah mengecek/menampilkan keseleruhan isi data csv tersebut dengan memakai command 'cat' kemudian diikuti nama filenya
```
cat Sandbox.csv
```
`Lalu setelah command diatas dijalankan maka kita akan mendapatkan output berupa seluruh isi dari file "Sandbox.csv" mulai dari kolom dan serta data_data yang lain`
- Langkah ketiga untuk mengecek kemudian menampilkan jumlah kolom pada data yang ada pada file menggunakan command 'awk'
```
awk -F ',' '{print NF; exit}' Sandbox.csv
```
`Dengan menampilkan jumlah kolom yang ada pada file csv, akan sangat memabntu dalam pengerjaan soal untuk membadingkan kolom mana yang mau dibandingkan`
- Langkah terakhir adalah menampilkan nama kolom yang tersedia didalam file Sandbox menggunakan 'head', fungsinya agar nanti dalam pengerjaan soal kita dapat dengan mudah menentukan kolom mana  yang akan digunakan
```
head -n 1 Sandbox.csv
```
`Terakhir setelah menampilkan jumlah kolom dilakukan penampilan nama kolom untuk lebih mempermudah pengerjaan soal`
## *Pengerjaan Soal*
a. Tampilkan nama pembeli dengan total sales paling tinggi
```
awk -F ',' 'NR>1{sales[$6]+=$17} END{max_sales=0; for (customer in sales) {if (sales[customer] > max_sales) {max_sales = sales[customer]; max_customer = customer}} print "Customer dengan total sales tertinggi adalah " max_customer ", yaitu dengan total sales sebesar " max_sales}' Sandbox.csv > 1A.txt
```
`(-F ',') untuk menentukan pemisah dan memproses file CSV, kemudian NR>1{sales[$6]+=$17} untuk menghitung total penjualan untuk setiap pelanggan ($6 kolom nama pelanggan dan $17 kolom dengan jumlah penjualan), lalu END{max_sales=0; for... akan membaca dan mencari pelanggan dengan total penjualan tertinggi dan mencetaknya ke file 1A.txt`

b. Tampilkan customer segment yang memiliki profit paling kecil (REVISI SALAH OUTPUT)
```
awk -F ',' 'NR>1{profit[$7]+=$20} END{min_profit=1000000; segment_terkecil=""; for (segment in profit) {if (profit[segment]<min_profit) {min_profit=profit[segment]; segment_terkecil=segment}} print "Customer segment dengan profit terkecil adalah:", segment_terkecil, "dengan profit sebesar", min_profit}' Sandbox.csv > 1B.txt

```
`{print $7",",$20} akan mencetak kolom ke-7 (pelanggan) dan kolom ke-20 (profit) dari file CSV, kemudian END{min_profit=1000000; segment_terkecil=""; for... untuk untuk mencari nilai profit terkecil dan nama segmen yang sesuai. Jika nilai profit suatu segmen lebih kecil dari min_profit akan diperbarui nilai min_profit dan segment_terkecil yang sesuai, kemudian print... akan mencetaknya dan menyimpan di file 1B.txt`

c. Tampilkan 3 category yang memiliki total profit paling tinggi 
```
awk -F ',' 'NR > 1 {sum[$14]+=$20} END {print "Profit 3 tertinggi diantara seluruh category"; for (category in sum) print category ", " sum[category] }' Sandbox.csv  > 1C.txt 
```
`NR > 1 {sum[$14]+=$20} pertama menghitung total profit untuk setiap kategori ($14 adalah kolom dengan kategori dan $20 adalah kolom dengan profit) kemudian dengan print... akan langsung membaca dan mencetak dari 3 kategori tersebut di file 1C.txt`

d. Mengecek apakah pesanan itu ada. Cari purchase date dan amount (quantity) dari nama adriaens
```
awk -F ',' '/Adriaens/ {print "Pesanan " $6 " pada tanggal " $2 " dan sejumlah " $18}' Sandbox.csv > 1D.txt
```
`/Adriaens/ {print "Pesanan " $6 " pada tanggal " $2 " dan sejumlah " $18}' berikut akan mencari baris yang memiliki nama "Adriaens" kemudian mencetak pesanan, tanggal, dan jumlahnya ke file 1D.txt`

## *Dokumentasi*
![Screenshot (289)](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/150430084/0497e615-1f98-452a-bd2e-e0807693fa0a)
![Screenshot (290)](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/150430084/be22df14-d26d-4504-ad50-69ff4e6fdcc1)
![Screenshot (291)](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/150430084/ad10ccc7-d33d-45f3-9c84-0d32076d9100)
![Screenshot (292)](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/150430084/3ffbb1d5-fb92-4ccb-a914-4e89d6653abf)
![Screenshot (309)](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/150430084/3096e169-fa51-4547-a0b1-c947de33d49f)
![Screenshot (294)](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/150430084/d4c49b63-f3a0-4731-acb5-4269b2e697a3)
![Screenshot (295)](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/150430084/d0d95151-7e0b-4268-ad81-d7a188c8543f)

## ***SOAL 2 (Rafael)***
Oppie merupakan seorang peneliti bom atom, ia ingin merekrut banyak peneliti lain untuk mengerjakan proyek bom atom nya, Oppie memiliki racikan bom atom rahasia yang hanya bisa diakses penelitinya yang akan diidentifikasi sebagai user, Oppie juga memiliki admin yang bertugas untuk memanajemen peneliti,  bantulah oppie untuk membuat program yang akan memudahkan tugasnya 
a. Buatlah 2 program yaitu login.sh dan register.sh

b. Setiap admin maupun user harus melakukan register terlebih dahulu menggunakan email, username, pertanyaan keamanan dan jawaban, dan password

c. Username yang dibuat bebas, namun email bersifat unique. setiap email yang mengandung kata admin akan dikategorikan menjadi admin 

d. Karena resep bom atom ini sangat rahasia Oppie ingin password nya memuat keamanan tingkat tinggi

Password tersebut harus di encrypt menggunakan base64
Password yang dibuat harus lebih dari 8 karakter
Harus terdapat paling sedikit 1 huruf kapital dan 1 huruf kecil
Harus terdapat paling sedikit 1 angka 

e. Karena Oppie akan memiliki banyak peneliti dan admin ia berniat untuk menyimpan seluruh data register yang ia lakukan ke dalam folder users file users.txt. Di dalam file tersebut, terdapat catatan seluruh email, username, pertanyaan keamanan dan jawaban, dan password hash yang telah ia buat.

f. Setelah melakukan register, program harus bisa melakukan login. Login hanya perlu dilakukan menggunakan email dan password.

g. Karena peneliti yang di rekrut oleh Oppie banyak yang sudah tua dan pelupa maka Oppie ingin ketika login akan ada pilihan lupa password dan akan keluar pertanyaan keamanan dan ketika dijawab dengan benar bisa memunculkan password

h. Setelah user melakukan login akan keluar pesan sukses, namun setelah seorang admin melakukan login Oppie ingin agar admin bisa menambah, mengedit (username, pertanyaan keamanan dan jawaban, dan password), dan menghapus user untuk memudahkan kerjanya sebagai admin.Ketika admin ingin melakukan edit atau hapus user, maka akan keluar input email untuk identifikasi user yang akan di hapus atau di edit

i. Oppie ingin programnya tercatat dengan baik, maka buatlah agar program bisa mencatat seluruh log ke dalam folder users file auth.log, baik login ataupun register.
Format: [date] [type] [message]
Type: REGISTER SUCCESS, REGISTER FAILED, LOGIN SUCCESS, LOGIN FAILED
Ex:
[23/09/17 13:18:02] [REGISTER SUCCESS] user [username] registered successfully
[23/09/17 13:22:41] [LOGIN FAILED] ERROR Failed login attempt on user with email [email]


## ***PENGERJAAN***
### Login.sh 
```
#!/bin/bash

echo "welcome to login System" 

decrypt_password() {
    echo -n "$1" | base64 -d
}
encrypt_password() {
    echo -n "$1" | base64
}

check_login() {
    email="$1"
    password="$2"
    if grep -q "^$email:" users.txt; then
        encrypted_password=$(grep "^$email:" users.txt | cut -d ":" -f 5)
        stored_password=$(decrypt_password "$encrypted_password")
        if [ "$password" == "$stored_password" ]; then
		role=$(grep "$email:" users.txt | cut -d ":" -f 6) 
		echo "$role"  
        else
            echo "LOGIN FAILED"
            echo "[$(date '+%d/%m/%Y %H:%M:%S')] [LOGIN FAILED] User with email $email logged in Failed" >> auth.log
            exit 1
        fi
    else
        echo "LOGIN FAILED"
        echo "[$(date '+%d/%m/%Y %H:%M:%S')] [LOGIN FAILED] User with email $email logged in Failed" >> auth.log
        exit 1
    fi
}

forgot_password() {
    email="$1"
    security_question=$(grep "^$email:" users.txt | cut -d ":" -f 3)
    stored_answer=$(grep "^$email:" users.txt | cut -d ":" -f 4)
    
    read -p "$security_question: " answer

    if [ "$answer" == "$stored_answer" ]; then
        stored_password=$(grep "^$email:" users.txt | cut -d ":" -f 5)
        decrypted_password=$(decrypt_password "$stored_password")
        echo "Your password is: $decrypted_password"
    else
        echo "Wrong answer!"
    fi
}

admin_setings() {
email="$1" 
while true; do
    echo "Admin Menu" 
    echo "1. Add User"
    echo "2. Edit User"
    echo "3. Delete User"
    echo "4. Logout"
    read -p "Pilihan mu: " option1

case $option1 in 
1) 
add_user
;;
2)
edit_user
;;
3)
delete_user
;;
4)
echo "logout successful!"
exit
;;

esac
done 
}

add_user() {

    read -p "Enter email: " email
    if grep -q "^$email:" users.txt; then
        echo "Email already exists!"
        exit 1
    fi
    read -p "Enter username: " username
    read -p "Enter security question: " security_question
    read -p "Enter answer: " answer
    read -sp "Enter password (minimum 8 characters, at least 1 uppercase letter, 1 lowercase letter, 1 digit, 1 symbol, and not same as username, birthdate, or name):"  password
    echo

    if ! [[ "$password" =~ [[:upper:]] && "$password" =~ [[:lower:]] && "$password" =~ [0-9] && ${#password} -ge 8 ]]; then
        echo "(minimum 8 characters, at least 1 uppercase letter, 1 lowercase letter, 1 digit, 1 symbol, and not same as username, birthdate, or name)"
        echo "User registered failed" 
    echo "[$(date '+%d/%m/%Y %H:%M:%S')] [REGISTER FAILED] User $username registered failed" >> auth.log
        exit 1
    fi

    if [[ "$email" == *admin* ]]; then
        role="admin"
    else
        role="user"
    fi

  
    encrypted_password=$(encrypt_password "$password")

    echo "$email:$username:$security_question:$answer:$encrypted_password:$role" >> users.txt
    echo "[$(date '+%d/%m/%Y %H:%M:%S')] [REGISTER SUCCESS] User $username registered successfully" >> auth.log
    echo "User registered successfully!"
}

edit_user() {
    echo "User yang tersedia:"
    grep -oP '^\S+@gmail.com' users.txt
   
    read -p "Enter email of user to edit: " email
    if ! grep -q "^$email:" users.txt; then
        echo "User not found!"
        exit 1
    fi

    read -p "Enter new username: " new_username
    read -p "Enter new security question: " new_security_question
    read -p "Enter new answer: " new_answer
    read -sp "Enter new password: " new_password
    echo

    if ! [[ "$new_password" =~ [[:upper:]] && "$new_password" =~ [[:lower:]] && "$new_password" =~ [0-9] && ${#new_password} -ge 8 ]]; then
        echo "New password must contain at least 1 uppercase letter, 1 lowercase letter, 1 digit, and be at least 8 characters long"
        exit 1
    fi

    encrypted_password=$(encrypt_password "$new_password")

    sed -i "/^$email:/s/:.*$/:$new_username:$new_security_question:$new_answer:$encrypted_password/" users.txt

    echo "User edit successfully!"
}

delete_user() {
   
    echo "Email yang tersedia" 
    grep -oP '^\S+@gmail.com' users.txt 
    read -p "Enter email of user to delete: " email
    if ! grep -q "^$email:" users.txt; then
        echo "User not found!"
        exit 1
    fi

    sed -i "/^$email:/d" users.txt
    echo "User deleted successful!"
}


echo "1. Login"
echo "2. Forgot Password"
read -p "Pilihan mu: " option2

case $option2 in
    1)
        read -p "Enter email: " email
	read -sp "Enter password: " password
        echo
        
    role=$(check_login "$email" "$password") 
	if [ "$role" == "admin" ]; then 
	 admin_setings "$email"
	 echo "[$(date '+%d/%m/%Y %H:%M:%S')] [LOGIN SUCCESS] Admin with email $email logged in successfully" >> auth.log 
	
	else 
    check_login "email" "password" 
    echo "[$(date '+%d/%m/%Y %H:%M:%S')] [LOGIN SUCCESS] User with email $email logged in successfully" >> auth.log
    echo "login succesful" 
	echo "You don't have admin privilleges, Welcome!"
    fi
    ;; 
        
    2)
	echo "Forgot Password?" 
	read -p "Enter email: " email 
        forgot_password "$email"
        ;;
    *)
        echo "Pilihan tidak tersedia"
        ;;
esac
```
### register.sh
```
#!/bin/bash

echo "Welcome to Registration System" 
encrypt_password() {
    echo -n "$1" | base64
}

check_email() {
    email="$1"
    if grep -q "^$email:" users.txt; then
        echo "Email already exists!"
        exit 1
    fi
}
register_user() {
    email="$1"
    username="$2"
    security_question="$3"
    answer="$4"
    password="$5"

   
    if [[ "$email" == *admin* ]]; then
        role="admin"
    else
        role="user"
    fi

    
    encrypted_password=$(encrypt_password "$password")

    
    echo "$email:$username:$security_question:$answer:$encrypted_password:$role" >> users.txt
    echo "User registered succesfully" 
    
    echo "[$(date '+%d/%m/%Y %H:%M:%S')] [REGISTER SUCCESS] User $username registered successfully" >> auth.log
}

read -p "Enter email: " email
check_email "$email"

read -p "Enter username: " username
read -p "Enter security question: " security_question
read -p "Enter answer: " answer
read -sp "Enter password (minimum 8 characters, at least 1 uppercase letter, 1 lowercase letter, 1 digit, 1 symbol, and not same as username, birthdate, or name):" password
echo


if ! [[ "$password" =~ [[:upper:]] && "$password" =~ [[:lower:]] && "$password" =~ [0-9] && ${#password} -ge 8 ]]; then
    echo "Password must have minumun 8 characters, at least Password must contain at least 1 uppercase letter, 1 lowercase letter, 1 digit, and not same as username, birthdate, or name)"
    echo "User registered failed" 
    echo "[$(date '+%d/%m/%Y %H:%M:%S')] [REGISTER FAILED] User $username registered failed" >> auth.log
    exit 1
fi

register_user "$email" "$username" "$security_question" "$answer" "$password"
```

## ***PENJELASAN PENGERJAAN***
###### -p 
digunakan untuk menampilkan pesan prompt
###### sed -i 
digunakan untuk memanipulasi teks dalam sebuah file 
###### -sp 
digunakan untuk menampilkan pesan prompt serta membuat inputan pengguna tidak terlihat di layar
###### cut 
digunakan untuk memotong inputan sebuah file dengan -d sebagai pemisahnya dan -f sebagai pemotong dari kolom berapa yang ingin ditampilkan

## Soal No.2 
Oppie merupakan seorang peneliti bom atom, ia ingin merekrut banyak peneliti lain untuk mengerjakan proyek bom atom nya, Oppie memiliki racikan bom atom rahasia yang hanya bisa diakses penelitinya yang akan diidentifikasi sebagai user, Oppie juga memiliki admin yang bertugas untuk memanajemen peneliti,  bantulah oppie untuk membuat program yang akan memudahkan tugasnya 
### a.Buatlah 2 program yaitu login.sh dan register.sh
Pertama-tama kita buat terlebih dahulu folder soal_2 kemudian setelah itu didalam folder soal_2 kita menggunakan nano login.sh menuliskan #!/bin/bash lalu keluar dan menggunakan nano register.sh kemudian menuliskan #!/bin/bash lalu keluar. 
### b. Setiap admin maupun user harus melakukan register terlebih dahulu menggunakan email, username, pertanyaan keamanan dan jawaban, dan password
Pertama kita buat terlebih dahulu kode untuk register user pada register.sh 
 
```
register_user(){ 

    email="$1"
    username="$2"
    security_question="$3"
    answer="$4"
    password="$5"

	if [[ "$email" == *admin* ]]; then
        role="admin"
    else
        role="user"
    fi

    encrypted_password=$(encrypt_password "$password")
    
    echo"$email:$username:$security_question:$answer:$encrypted_password:$role" >> users.txt
    echo "User registered succesfully" 
}
```
Lalu untuk ditampilkan pada tampilan dengan menggunakan read untuk mengambil inputan dari user, dan menggunakan fungsi register user yang telah dibuat sebelumnya diatas
```
read -p "Enter email: " email
check_email "$email"

read -p "Enter username: " username
read -p "Enter security question: " security_question
read -p "Enter answer: " answer
read -sp "Enter password (minimum 8 characters, at least 1 uppercase letter, 1 lowercase letter, 1 digit, 1 symbol, and not same as username, birthdate, or name):" password
echo

register_user "$email" "$username" "$security_question" "$answer" "$password"
```
### c. Username yang dibuat bebas, namun email bersifat unique. setiap email yang mengandung kata admin akan dikategorikan menjadi admin 

Pada bagian register.sh kita tambahkan role 
```
register_user(){ 

	...

    if [[ "$email" == *admin* ]]; then
        role="admin"
    else
        role="user"
    fi
}
```
Dengan menggunakan if email == admin akan membuat email yang mengandung kata admin seperti admin@gmail.com akan dikatagorikan sebagai admin.  

### d. Karena resep bom atom ini sangat rahasia Oppie ingin password nya memuat keamanan tingkat tinggi
#### Password tersebut harus di encrypt menggunakan base64 
```
encrypt_password() {
    echo -n "$1" | base64
}
```
Dengan menggunakan fungsi encrypt_password maka password yang dimasukkan akan di enkripsi dalam bentuk base64

#### Password yang dibuat harus lebih dari 8 karakter, Harus terdapat paling sedikit 1 huruf kapital dan 1 huruf kecil, Harus terdapat paling sedikit 1 angka

Dengan batasan password seeprti ini dalam kode register.sh 
```
if ! [[ "$password" =~ [[:upper:]] && "$password" =~ [[:lower:]] && "$password" =~ [0-9] && ${#password} -ge 8 ]]; then
    echo "(Password must have minumun 8 characters, at least Password must contain at least 1 uppercase letter, 1 lowercase letter, 1 digit, and not same as username, birthdate, or name)"
    echo "User registered failed" 
	...
    exit 1
fi
```
Dari kode diatas password yang diisikan harus memiliki huruf besar dan huruf kecil dan angka serta harus memiiki panjang minimal 8 karakter bila tidak akan ditamplikan Password (must have minumun 8 characters, at least Password must contain at least 1 uppercase letter, 1 lowercase letter, 1 digit, and not same as username, birthdate, or name) dan juga registrasi akan gagal dan keluar dari register.sh 

### e.Karena Oppie akan memiliki banyak peneliti dan admin ia berniat untuk menyimpan seluruh data register yang ia lakukan ke dalam folder users file users.txt. Di dalam file tersebut, terdapat catatan seluruh email, username, pertanyaan keamanan dan jawaban, dan password hash yang telah ia buat.

Pada kode yang telah ada diatas 
```
echo"$email:$username:$security_question:$answer:$encrypted_password:$role" >> users.txt
```
Kode inilah yang akan mengirimkan semua hasil email.username,security question, answer, serta password yang telah terenkripsi dan juga role yang dimiliki ke user.txt

### f.Setelah melakukan register, program harus bisa melakukan login. Login hanya perlu dilakukan menggunakan email dan password.

Kita membuka login.sh terlebih dahulu pada awal tampilan login akan diminta memasukkan email dan password 
```
check_login() {
    email="$1"
    password="$2"
    if grep -q "^$email:" users.txt; then
        encrypted_password=$(grep "^$email:" users.txt | cut -d ":" -f 5)
        stored_password=$(decrypt_password "$encrypted_password")
        if [ "$password" == "$stored_password" ]; then
		role=$(grep "$email:" users.txt | cut -d ":" -f 6) 
		echo "$role"  
        else
            echo "LOGIN FAILED"
            echo "[$(date '+%d/%m/%Y %H:%M:%S')] [LOGIN FAILED] User with email $email logged in Failed" >> auth.log
            exit 1
        fi
    else
        echo "LOGIN FAILED"
        echo "[$(date '+%d/%m/%Y %H:%M:%S')] [LOGIN FAILED] User with email $email logged in Failed" >> auth.log
        exit 1
    fi
}
```
Dengan kode diatas ditambah kode 
```
read -p "Enter email: " email
	read -sp "Enter password: " password
        echo
        
    role=$(check_login "$email" "$password") 
```
Maka email dan password yang kita masukkan akan di cek apakah ada di user.txt dan apakah email serta passwordnya cocok. 

### g.Karena peneliti yang di rekrut oleh Oppie banyak yang sudah tua dan pelupa maka Oppie ingin ketika login akan ada pilihan lupa password dan akan keluar pertanyaan keamanan dan ketika dijawab dengan benar bisa memunculkan password

Kita modifikasi kembali login.sh sehingga bisa menampilkan pilihan login atau lupa password 

```
echo "1. Login"
echo "2. Forgot Password"
read -p "Pilihan mu: " option2

case $option2 in
    1)
        read -p "Enter email: " email
	read -sp "Enter password: " password
        echo
	2)
	echo "Forgot Password?" 
	read -p "Enter email: " email 
        forgot_password "$email"
        ;;
    *)
        echo "Pilihan tidak tersedia"
        ;;

```
Namun sebelum menjalankan forgot password kita harus membuat fungsi forgor_password terlebih dahulu dan dengan mengambil variabel email fungsi forgot_password dijalankan, kodenya: 


```
forgot_password() {
    email="$1"
    security_question=$(grep "^$email:" users.txt | cut -d ":" -f 3)
    stored_answer=$(grep "^$email:" users.txt | cut -d ":" -f 4)
    
    read -p "$security_question: " answer

    if [ "$answer" == "$stored_answer" ]; then
        stored_password=$(grep "^$email:" users.txt | cut -d ":" -f 5)
        decrypted_password=$(decrypt_password "$stored_password")
        echo "Your password is: $decrypted_password"
    else
        echo "Wrong answer!"
    fi
}
```
pada fungsi forgot password sebagai email menjadi kunci utamanya untuk mencari password pada user.txt maka setelah email diketahui maka akan mengeluarkan security question dan apabila jawabannya benar maka akan menampilkan password yang benar dari email tersebut

### h. Setelah user melakukan login akan keluar pesan sukses, namun setelah seorang admin melakukan login Oppie ingin agar admin bisa menambah, mengedit (username, pertanyaan keamanan dan jawaban, dan password), dan menghapus user untuk memudahkan kerjanya sebagai admin

Untuk mengeluarkan pesan sukses saat user berhasil login adalah dengan menggunakan kode :
```
check_login() {
    email="$1"
    password="$2"
    if grep -q "^$email:" users.txt; then
        encrypted_password=$(grep "^$email:" users.txt | cut -d ":" -f 5)
        stored_password=$(decrypt_password "$encrypted_password")
        if [ "$password" == "$stored_password" ]; then
		role=$(grep "$email:" users.txt | cut -d ":" -f 6) 
		echo "$role"  
        else
            echo "LOGIN FAILED"
            echo "[$(date '+%d/%m/%Y %H:%M:%S')] [LOGIN FAILED] User with email $email logged in Failed" >> auth.log
            exit 1
        fi
    else
        echo "LOGIN FAILED"
        echo "[$(date '+%d/%m/%Y %H:%M:%S')] [LOGIN FAILED] User with email $email logged in Failed" >> auth.log
        exit 1
    fi
}

...

check_login "email" "password" 
    echo "[$(date '+%d/%m/%Y %H:%M:%S')] [LOGIN SUCCESS] User with email $email logged in successfully" >> auth.log
    echo "login succesful" 
	echo "You don't have admin privilleges, Welcome!"
```
Dengan fungsi check login dan menjalankannya saat check_login bernilai true maka akan muncul login succsesful dan you don't have admin privilaleges, welcome! 

Agar saat menggunakan email admin maka akan muncul 4 pilihan maka code yang diperlukan yaitu: 
```
admin_setings() {
email="$1" 
while true; do
    echo "Admin Menu" 
    echo "1. Add User"
    echo "2. Edit User"
    echo "3. Delete User"
    echo "4. Logout"
    read -p "Pilihan mu: " option1

case $option1 in 
1) 
add_user
;;
2)
edit_user
;;
3)
delete_user
;;
4)
echo "logout successful!"
exit
;;

esac
done 
}
```
Ini hanyalah fungsi dari admin_settings yang menampilkan keempat pilihan dan agar pilihan ini dapat berjalan dibutuhkan tiga fungsi lainnya yaitu add_user yang mirip dengan register.sh lalu edit_user sehingga bisa mengubah username,password,pertanyaan,serta jawabannya yang dimiliki email tersebut pada user.txt dan terakhir dapat menghapus email di user.txt masing masing fungsinya sebagai berikut 
```
add_user() {

    read -p "Enter email: " email
    if grep -q "^$email:" users.txt; then
        echo "Email already exists!"
        exit 1
    fi
    read -p "Enter username: " username
    read -p "Enter security question: " security_question
    read -p "Enter answer: " answer
    read -sp "Enter password (minimum 8 characters, at least 1 uppercase letter, 1 lowercase letter, 1 digit, 1 symbol, and not same as username, birthdate, or name):"  password
    echo

    if ! [[ "$password" =~ [[:upper:]] && "$password" =~ [[:lower:]] && "$password" =~ [0-9] && ${#password} -ge 8 ]]; then
        echo "(minimum 8 characters, at least 1 uppercase letter, 1 lowercase letter, 1 digit, 1 symbol, and not same as username, birthdate, or name)"
        echo "User registered failed" 
    echo "[$(date '+%d/%m/%Y %H:%M:%S')] [REGISTER FAILED] User $username registered failed" >> auth.log
        exit 1
    fi

    if [[ "$email" == *admin* ]]; then
        role="admin"
    else
        role="user"
    fi

  
    encrypted_password=$(encrypt_password "$password")

    echo "$email:$username:$security_question:$answer:$encrypted_password:$role" >> users.txt
    echo "[$(date '+%d/%m/%Y %H:%M:%S')] [REGISTER SUCCESS] User $username registered successfully" >> auth.log
    echo "User registered successfully!"
}
```
```
edit_user() {
    echo "User yang tersedia:"
    grep -oP '^\S+@gmail.com' users.txt
   
    read -p "Enter email of user to edit: " email
    if ! grep -q "^$email:" users.txt; then
        echo "User not found!"
        exit 1
    fi

    read -p "Enter new username: " new_username
    read -p "Enter new security question: " new_security_question
    read -p "Enter new answer: " new_answer
    read -sp "Enter new password: " new_password
    echo

    if ! [[ "$new_password" =~ [[:upper:]] && "$new_password" =~ [[:lower:]] && "$new_password" =~ [0-9] && ${#new_password} -ge 8 ]]; then
        echo "New password must contain at least 1 uppercase letter, 1 lowercase letter, 1 digit, and be at least 8 characters long"
        exit 1
    fi

    encrypted_password=$(encrypt_password "$new_password")

    sed -i "/^$email:/s/:.*$/:$new_username:$new_security_question:$new_answer:$encrypted_password/" users.txt

    echo "User edit successfully!"
}
```
```
delete_user() {
   
    echo "Email yang tersedia" 
    grep -oP '^\S+@gmail.com' users.txt 
    read -p "Enter email of user to delete: " email
    if ! grep -q "^$email:" users.txt; then
        echo "User not found!"
        exit 1
    fi

    sed -i "/^$email:/d" users.txt
    echo "User deleted successful!"
}
```
Setelah keseluruhan fungsi lengkap agar bisa masuk ke admin_settings saat login diperlukan code : 
```
role=$(check_login "$email" "$password") 
	if [ "$role" == "admin" ]; then 
	 admin_setings "$email"
```
Sehingga apabila didapatkan role admin maka akan menjalankan admin_setings dengan pemicu emailnya. 

### i. Ketika admin ingin melakukan edit atau hapus user, maka akan keluar input email untuk identifikasi user yang akan di hapus atau di edit

Dari kode yang diatas pada bagian fungsi edit_user dan delete_user terdapat code  
```
echo "Email yang tersedia" 

grep -oP '^\S+@gmail.com' users.txt 
```
Perintah ini akan menampilkan email yang tersedia berdasarkan email yang ada di users.txt dengan mencari sebuah string tanpa spasi yang diakhiri oleh @gmail.com sehingga bila email yang dimasukkan bukan berupa @gmail.com tidak akan muncul di list 

### j. Oppie ingin programnya tercatat dengan baik, maka buatlah agar program bisa mencatat seluruh log ke dalam folder users file auth.log, baik login ataupun register.

Untuk mencatat log ke sebuah file autg.log diperlukan kode : 
Pada register.sh 
```
Apabila berhasil :
echo "[$(date '+%d/%m/%Y %H:%M:%S')] [REGISTER SUCCESS] User $username registered successfully" >> auth.log

Apabila gagal :
echo "[$(date '+%d/%m/%Y %H:%M:%S')] [REGISTER FAILED] User $username registered failed" >> auth.log
```
Pada login.sh
```
Apabila berhasil login dengan email admin: 
echo "[$(date '+%d/%m/%Y %H:%M:%S')] [LOGIN SUCCESS] Admin with email $email logged in successfully" >> auth.log 

Apabila berhasil login dengan email user: 
echo "[$(date '+%d/%m/%Y %H:%M:%S')] [LOGIN SUCCESS] User with email $email logged in successfully" >> auth.log

Apabila gagal login: 
echo "[$(date '+%d/%m/%Y %H:%M:%S')] [LOGIN FAILED] User with email $email logged in Failed" >> auth.log
```
Dengan kode diatas maka setiap kali ada register yang berhasil ataupun gagal akan tercatat di auth.log bergitupun saat menjalankan login.sh apabila gagal login ataupun berhasil login maka akan tercatat di auth.log

## *Dokumentasi*

![Register sh](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/150375098/7ffa3742-7d88-4509-a0e2-90c5b0b18e7a)
![Login user](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/150375098/84a0870d-0b4f-442d-b4ff-a103c8628bb3)
![Lupa pass,login user registe](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/150375098/ea2270aa-45e3-41b8-ba13-04808ba58353)
![Tampilan admin](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/150375098/dc0524fc-95c7-445e-a0eb-efc8f98d4b97)
![Admin 1 dan 2](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/150375098/f07ba785-cf79-41a7-a159-823661c56ab9)
![admin 3 dan 4](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/150375098/351ab9ed-df6b-451e-bae6-8c99e4375ba2)
![Tampilan log](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/150375098/e68382d0-d04b-4f61-b9cf-1ac3dbe825eb)
![Gagal login](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/150375098/4ab51098-ffe2-4347-a7ea-30dee3eb95ec)
![Tampilan log gagal](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/150375098/677d0b9e-1289-4e76-87e4-de845d4bace4)


## ***SOAL 3 (Abhinaya)***
Alyss adalah seorang gamer yang sangat menyukai bermain game Genshin Impact. Karena hobinya, dia ingin mengoleksi foto-foto karakter Genshin Impact. Suatu saat Yanuar memberikannya sebuah Link yang berisi koleksi kumpulan foto karakter dan sebuah clue yang mengarah ke penemuan gambar rahasia. Ternyata setiap nama file telah dienkripsi dengan menggunakan hexadecimal. Karena penasaran dengan apa yang dikatakan Yanuar, Alyss tidak menyerah dan mencoba untuk mengembalikan nama file tersebut kembali seperti semula.
a. Alyss membuat script bernama awal.sh, untuk download file yang diberikan oleh Yanuar dan unzip terhadap file yang telah diunduh dan decode setiap nama file yang terenkripsi dengan hex . Karena pada file list_character.csv terdapat data lengkap karakter, Alyss ingin merename setiap file berdasarkan file tersebut. Agar semakin rapi, Alyss mengumpulkan setiap file ke dalam folder berdasarkan region tiap karakter
* Format: Region - Nama - Elemen - Senjata.jpg

b. Karena tidak mengetahui jumlah pengguna dari tiap senjata yang ada di folder "genshin_character".Alyss berniat untuk menghitung serta menampilkan jumlah pengguna untuk setiap senjata yang ada
* Format: [Nama Senjata] : [jumlah]
	 Untuk menghemat penyimpanan. Alyss menghapus file - file yang tidak ia gunakan, yaitu genshin_character.zip, list_character.csv, dan genshin.zip

c. Namun sampai titik ini Alyss masih belum menemukan clue dari the secret picture yang disinggung oleh Yanuar. Dia berpikir keras untuk menemukan pesan tersembunyi tersebut. Alyss membuat script baru bernama search.sh untuk melakukan pengecekan terhadap setiap file tiap 1 detik. Pengecekan dilakukan dengan cara meng-ekstrak sebuah value dari setiap gambar dengan menggunakan command steghide. Dalam setiap gambar tersebut, terdapat sebuah file txt yang berisi string. Alyss kemudian mulai melakukan dekripsi dengan hex pada tiap file txt dan mendapatkan sebuah url. Setelah mendapatkan url yang ia cari, Alyss akan langsung menghentikan program search.sh serta mendownload file berdasarkan url yang didapatkan.

d.Dalam prosesnya, setiap kali Alyss melakukan ekstraksi dan ternyata hasil ekstraksi bukan yang ia inginkan, maka ia akan langsung menghapus file txt tersebut. Namun, jika itu merupakan file txt yang dicari, maka ia akan menyimpan hasil dekripsi-nya bukan hasil ekstraksi. Selain itu juga, Alyss melakukan pencatatan log pada file image.log untuk setiap pengecekan gambar
* Format: [date] [type] [image_path]
* Ex: 
1. [24/03/20 17:18:19] [NOT FOUND] [image_path]
2. [24/03/20 17:18:20] [FOUND] [image_path]

e. Hasil akhir:
* genshin_character
* search.sh
* awal.sh
* image.log
* [filename].txt
* [image].jpg

## ***PENGERJAAN***
**Pengorganisasian File Genshin Character**

Skrip ini mengotomatiskan pengorganisasian gambar karakter Genshin yang diunduh dan informasi terkaitnya.

**awal.sh**
```
#!/bin/bash

FILE_DIR="/home/$USER/praktikum_tka_no.2"

if [ -d $FILE_DIR ]; then
  echo "directory exist."
else
  mkdir $FILE_DIR
fi

cd $FILE_DIR

wget -q --no-check-certificate 'https://docs.google.com/uc?export=download&id=1oGHdTf4_76_RacfmQIV4i7os4sGwa9vN' -O genshin.zip

unzip -q genshin.zip
unzip -q genshin_character.zip

if [ -d genshin_character ]; then
  cd genshin_character
else
  echo "Error: genshin_character directory not found after unzipping."
  exit 1
fi

for file in *.jpg; do
  new_name=$(echo "$file" | xxd -p -r)
  mv "$file" "$new_name".jpg
done

dos2unix $FILE_DIR/list_character.csv

while IFS="," read -r col1 col2 col3 col4; do
  for file in *.jpg; do
    if [ "$file" == "$col1".jpg ]; then
      mv "$file" "$col2 - $col1 - $col3 - $col4".jpg
    fi
  done
done < $FILE_DIR/list_character.csv


for file in *.jpg; do 
  dir_name=$(echo "$file" | cut -d "-" -f1)
  if [ -d $dir_name ]; then
    cp "$file" $FILE_DIR/genshin_character/$dir_name
  else
    mkdir $dir_name
    cp "$file" $FILE_DIR/genshin_character/$dir_name
  fi
done

claymore=$(ls | grep -o "Claymore" | wc -l)
echo "Claymore : $claymore"

sword=$(ls | grep -o "Sword" | wc -l)
echo "Sword : $sword"

polearm=$(ls | grep -o "Polearm" | wc -l)
echo "Polearm : $polearm"

catalyst=$(ls | grep -o "Catalyst" | wc -l)
echo "Catalyst : $catalyst"

bow=$(ls | grep -o "Bow" | wc -l)
echo "Bow : $bow"

cd $FILE_DIR
rm genshin.zip && rm genshin_character.zip && rm list_character.csv


exec bash
```

**Perangkat Lunak yang Dibutuhkan:**

* Bash shell
* `wget`
* `unzip`
* `xxd`
* `dos2unix`

**Instruksi:**

1. Pastikan program yang dibutuhkan sudah terinstall.
2. Simpan skrip ini sebagai `awal.sh`.
3. Buat skrip dapat dieksekusi: `chmod +x awal.sh`.
4. Jalankan skrip: `./awal.sh`.

**Penjelasan:**

1. **Pengaturan Direktori:**
    * Skrip membuat direktori bernama `praktikum_tka_no.2` di direktori home Anda jika belum ada.
    * Kemudian berpindah ke direktori `praktikum_tka_no.2`.
    ```
    FILE_DIR="/home/$USER/praktikum_tka_no.2"

    if [ -d $FILE_DIR ]; then
      echo "directory exist."
    else
      mkdir $FILE_DIR
    fi
    
    cd $FILE_DIR
    ```

2. **Unduh File:**
    * Skrip mengunduh file ZIP (berisi gambar karakter dan daftar karakter) dari link Google Drive menggunakan `wget`.
    * Skrip mengekstrak kedua file arsip yang diunduh (`genshin.zip`) dan arsip terlampir (`genshin_character.zip`) secara diam-diam (tanpa output).
    ```
    wget -q --no-check-certificate 'https://docs.google.com/uc?export=download&id=1oGHdTf4_76_RacfmQIV4i7os4sGwa9vN' -O genshin.zip

    unzip -q genshin.zip
    unzip -q genshin_character.zip
    ```

3. **Ganti Nama Gambar Karakter:**
    * Skrip memeriksa apakah direktori `genshin_character` ada setelah diekstrak. Jika tidak, skrip akan keluar dengan pesan kesalahan.
    * Script kemudian melakukan perulangan pada setiap file gambar JPG di direktori saat ini.
    * Menggunakan `xxd`, script mengubah nama file dari format terenkripsi menjadi string karakter yang dapat dibaca dan menetapkannya ke variabel baru.
    * Nama file asli kemudian diganti dengan string baru yang dapat dibaca dengan ekstensi `.jpg` ditambahkan.
    ```
    if [ -d genshin_character ]; then
      cd genshin_character
    else
      echo "Error: genshin_character directory not found after unzipping."
      exit 1
    fi
    
    for file in *.jpg; do
      new_name=$(echo "$file" | xxd -p -r)
      mv "$file" "$new_name".jpg
    done
    ```

4. **Memproses Daftar Karakter:**
    * Skrip menggunakan `dos2unix` untuk mengonversi akhiran baris dalam file `list_character.csv` (jika perlu) untuk memastikan parsing yang benar.
    * Script ber iterasi melalui setiap baris dalam file CSV menggunakan loop `while`. Setiap baris dibagi menjadi kolom yang dipisahkan koma menggunakan `read`.
    * Di dalam loop, script kembali melakukan iterasi melalui setiap file gambar JPG.
    * Jika nama file gambar cocok dengan nama karakter dari kolom pertama baris CSV, skrip mengganti nama gambar dengan informasi tambahan dari kolom CSV (nama, tipe senjata, dll.).
    ```
    dos2unix $FILE_DIR/list_character.csv
    
    while IFS="," read -r col1 col2 col3 col4; do
      for file in *.jpg; do
        if [ "$file" == "$col1".jpg ]; then
          mv "$file" "$col2 - $col1 - $col3 - $col4".jpg
        fi
      done
    done < $FILE_DIR/list_character.csv
    ```

5. **Atur Gambar berdasarkan Jenis Region:**
    * Script kembali melakukan iterasi melalui setiap file gambar JPG.
    * Script mengekstrak tipe region dari nama file menggunakan perintah `cut`.
    * Jika direktori dengan nama region sudah ada, gambar akan disalin ke direktori tersebut. Jika tidak, direktori baru akan dibuat, dan gambar akan disalin ke sana.
    ```
    for file in *.jpg; do 
      dir_name=$(echo "$file" | cut -d "-" -f1)
      if [ -d $dir_name ]; then
        cp "$file" $FILE_DIR/genshin_character/$dir_name
      else
        mkdir $dir_name
        cp "$file" $FILE_DIR/genshin_character/$dir_name
      fi
    done
    ```

6. **Jumlah Jenis Senjata:**
    * Script menggunakan `grep` untuk menghitung jumlah nama file gambar yang mengandung setiap tipe senjata ("Claymore", "Sword", dll.).
    * Kemudian script mencetak tipe senjata dan jumlahnya.
    ```
    claymore=$(ls | grep -o "Claymore" | wc -l)
    echo "Claymore : $claymore"
    
    sword=$(ls | grep -o "Sword" | wc -l)
    echo "Sword : $sword"
    
    polearm=$(ls | grep -o "Polearm" | wc -l)
    echo "Polearm : $polearm"
    
    catalyst=$(ls | grep -o "Catalyst" | wc -l)
    echo "Catalyst : $catalyst"
    
    bow=$(ls | grep -o "Bow" | wc -l)
    echo "Bow : $bow"
    ```

7. **Pembersihan:**
    * Script berpindah kembali ke direktori kerja awal (`praktikum_tka_no.2`).
    * Terakhir, script menghapus file arsip yang diunduh (`genshin.zip` dan `genshin_character.zip`) dan file CSV daftar karakter.
    ```
    cd $FILE_DIR
    rm genshin.zip && rm genshin_character.zip && rm list_character.csv
    
    
    exec bash
    ```

8. **Mulai Ulang Shell:**
    * Script memulai kembali Bash shell (`exec bash`), yang pada umumnya tidak diperlukan tetapi mungkin berguna untuk keperluan debugging.


**Pencari Link Rahasia dari Gambar**

Skrip ini mencari link rahasia yang disembunyikan di dalam file gambar menggunakan teknik steganografi.

**search.sh**
```
#!/bin/bash

FILE_DIR="/home/$USER/praktikum_tka_no.2"

if [ -d $FILE_DIR ]; then
    echo "directory exist."
else
    mkdir $FILE_DIR
fi

cd $FILE_DIR

if [ -d genshin_character ]; then
    cd genshin_character
else
    echo "Error: genshin_character directory not found after unzipping."
    exit 1
fi

pass=""

for file in *.jpg; do
    steghide extract -q -sf "$file" -p "$pass"
done

for file in *.txt; do
    base64 -d "$file" > secret.txt
    regex='(https?|ftp|file)://[-[:alnum:]\+&@#/%?=~_|!:,.;]*[-[:alnum:]\+&@#/%=~_|]'
    string=$(cat secret.txt)
    if [[ $string =~ $regex ]]; then 
        mv secret.txt $FILE_DIR
        echo "[$(date '+%Y/%M/%d %H:%M:%S')] [FOUND] [$FILE_DIR/genshin_character/$file]" >> image.log
        break
    else
        echo "[$(date '+%Y/%M/%d %H:%M:%S')] [NOT FOUND] [$FILE_DIR/genshin_character/$file]" >> image.log
    fi
    rm "$file"
    sleep 1
done

for file in *.txt; do
    rm "$file"
done

mv image.log $FILE_DIR

cd $FILE_DIR

secret_link=$(cat "secret.txt")

wget -O gambar.jpg "$secret_link"

exec bash
```

**Perangkat Lunak yang Dibutuhkan:**

* Bash shell
* `steghide`
* `base64`
* `wget`

**Instruksi:**

1. Pastikan program yang dibutuhkan sudah terinstall.
2. Simpan skrip ini sebagai `search.sh`.
3. Buat skrip dapat dieksekusi: `chmod +x search.sh`.
4. Pindahkan file gambar yang diduga mengandung link rahasia ke direktori `genshin_character` di direktori home Anda (sesuaikan jika direktori berbeda).
5. Jalankan skrip: `./search.sh`.

**Penjelasan:**

1. **Periksa Direktori `genshin_character`:**

    * Skrip memeriksa keberadaan direktori `genshin_character`.
    * Jika direktori tidak ditemukan, skrip akan menampilkan pesan kesalahan dan keluar.
    ```
    if [ -d genshin_character ]; then
        cd genshin_character
    else
        echo "Error: genshin_character directory not found after unzipping."
        exit 1
    fi
    ```
2. **Ekstrak Informasi dari Gambar:**

    * Script menggunakan program `steghide` untuk mengekstrak informasi tersembunyi dari setiap file gambar JPG di direktori `genshin_character`. 
    * Asumsikan password untuk ekstraksi sudah diketahui dan disimpan dalam variabel `pass`.
    ```
    pass=""
    
    for file in *.jpg; do
        steghide extract -q -sf "$file" -p "$pass"
    done
    ```
3. **Dekripsi dan Pencarian Link:**

    * Script kemudian memproses setiap file teks yang dihasilkan dari ekstraksi (`*.txt`).
    * Isi file teks di-decode menggunakan `base64` dan disimpan ke file `secret.txt`.
    * Script menggunakan ekspresi regular untuk mencari pola link (format HTTP, HTTPS, FTP, atau file) di dalam `secret.txt`.
    * Jika link ditemukan, script akan:
        * Memindahkan `secret.txt` ke direktori utama (`$FILE_DIR`).
        * Mencatat waktu penemuan, nama file gambar asli, dan link rahasia ke dalam file log (`image.log`).
        * Hentikan proses pencarian lebih lanjut.
    * Jika link tidak ditemukan, script akan mencatat informasi tersebut ke file log dan menghapus file teks.
    * Script memberikan jeda selama 1 detik antar proses tiap file untuk mencegah pemblokiran oleh server.
    ```
    for file in *.txt; do
        base64 -d "$file" > secret.txt
        regex='(https?|ftp|file)://[-[:alnum:]\+&@#/%?=~_|!:,.;]*[-[:alnum:]\+&@#/%=~_|]'
        string=$(cat secret.txt)
        if [[ $string =~ $regex ]]; then 
            mv secret.txt $FILE_DIR
            echo "[$(date '+%Y/%M/%d %H:%M:%S')] [FOUND] [$FILE_DIR/genshin_character/$file]" >> image.log
            break
        else
            echo "[$(date '+%Y/%M/%d %H:%M:%S')] [NOT FOUND] [$FILE_DIR/genshin_character/$file]" >> image.log
        fi
        rm "$file"
        sleep 1
    done
    ```
4. **Bersihkan File Sementara:**

    * Script menghapus semua file teks sisa dari proses ekstraksi.
    ```
    for file in *.txt; do
        rm "$file"
    done
    ```
5. **Pindahkan File Log dan Unduh Gambar Rahasia:**

    * Script memindahkan file log (`image.log`) ke direktori utama (`$FILE_DIR`).
    * Script menggunakan `wget` untuk mengunduh gambar yang ditemukan berdasarkan link rahasia yang tersimpan di `secret.txt`. Gambar akan disimpan dengan nama `gambar.jpg`.
    ```
    mv image.log $FILE_DIR
    
    cd $FILE_DIR
    
    secret_link=$(cat "secret.txt")
    
    wget -O gambar.jpg "$secret_link"
    
    exec bash
    ```

6. **Mulai Ulang Shell:**

    * Script memulai kembali Bash shell (`exec bash`), yang pada umumnya tidak diperlukan tetapi mungkin berguna untuk keperluan debugging.

**Catatan:**

* Script ini mengasumsikan password untuk ekstraksi informasi dari gambar sudah diketahui.
* Script ini bergantung pada format dan teknik steganografi yang digunakan untuk menyembunyikan link rahasia di dalam gambar.
* Anda perlu memindahkan file gambar yang ingin diproses ke direktori `genshin_character` terlebih dahulu. Sesuaikan lokasi direktori sesuai dengan kebutuhan Anda. 

## ***DOKUMENTASI***
![Screenshot from 2024-03-30 19-21-30](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/123524655/0e11d913-2624-42c4-8831-873fda20affb)
![Screenshot from 2024-03-30 19-22-22](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/123524655/643e9182-3995-48f1-b2e7-1702499f3393)
![Screenshot from 2024-03-30 19-22-36](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/123524655/8e2fb546-515b-4083-af19-c6d4b1aa3059)
![Screenshot from 2024-03-30 19-22-55](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/123524655/1adfa8d1-d528-4771-a129-a54316ba5599)
![Screenshot from 2024-03-30 19-25-56](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/123524655/acb35bd1-1750-422b-83a6-f79b6b15d438)

## ***SOAL 4 (REVISI ALL)***
Stitch sangat senang dengan PC di rumahnya. Suatu hari, PC nya secara tiba-tiba nge-freeze 🤯 Tentu saja, Stitch adalah seorang streamer yang harus setiap hari harus bermain game dan streaming.  Akhirnya, dia membawa PC nya ke tukang servis untuk diperbaiki. Setelah selesai diperbaiki, ternyata biaya perbaikan sangat mahal sehingga dia harus menggunakan uang hasil tabungan nya untuk membayarnya. Menurut tukang servis, masalahnya adalah pada CPU dan GPU yang overload karena gaming dan streaming sehingga mengakibatkan freeze pada PC nya. Agar masalah ini tidak terulang kembali, Stitch meminta kamu untuk membuat sebuah program monitoring resource yang tersedia pada komputer.

Buatlah program monitoring resource pada PC kalian. Cukup monitoring ram dan monitoring size suatu directory. Untuk ram gunakan command `free -m`. Untuk disk gunakan command `du -sh <target_path>`. Catat semua metrics yang didapatkan dari hasil `free -m`. Untuk hasil `du -sh <target_path>` catat size dari path directory tersebut. Untuk target_path yang akan dimonitor adalah /home/{user}/. 

a. Masukkan semua metrics ke dalam suatu file log bernama metrics_{YmdHms}.log. {YmdHms} adalah waktu disaat file script bash kalian dijalankan. Misal dijalankan pada 2024-03-20 15:00:00, maka file log yang akan tergenerate adalah metrics_20240320150000.log. 

b. Script untuk mencatat metrics diatas diharapkan dapat berjalan otomatis pada setiap menit. 

c. Kemudian, buat satu script untuk membuat agregasi file log ke satuan jam. Script agregasi akan memiliki info dari file-file yang tergenerate tiap menit. Dalam hasil file agregasi tersebut, terdapat nilai minimum, maximum, dan rata-rata dari tiap-tiap metrics. File agregasi akan ditrigger untuk dijalankan setiap jam secara otomatis. Berikut contoh nama file hasil agregasi metrics_agg_2024032015.log dengan format metrics_agg_{YmdH}.log 

d. Karena file log bersifat sensitif pastikan semua file log hanya dapat dibaca oleh user pemilik file. 

Note:
Nama file untuk script per menit adalah minute_log.sh
Nama file untuk script agregasi per jam adalah aggregate_minutes_to_hourly_log.sh
Semua file log terletak di /home/{user}/log
Semua konfigurasi cron dapat ditaruh di file skrip .sh nya masing-masing dalam bentuk comment

Berikut adalah contoh isi dari file metrics yang dijalankan tiap menit:
mem_total,mem_used,mem_free,mem_shared,mem_buff,mem_available,swap_total,swap_used,swap_free,path,path_size 15949,10067,308,588,5573,4974,2047,43,2004,/home/user/coba/,74M

Berikut adalah contoh isi dari file aggregasi yang dijalankan tiap jam:
type,mem_total,mem_used,mem_free,mem_shared,mem_buff,mem_available,swap_total,swap_used,swap_free,path,path_size minimum,15949,10067,223,588,5339,4626,2047,43,1995,/home/user/coba/,50M maximum,15949,10387,308,622,5573,4974,2047,52,2004,/home/user/coba/,74M average,15949,10227,265.5,605,5456,4800,2047,47.5,1999.5,/home/user/coba/,62M

## ***PENGERJAAN***
### minute_log.sh
```
#!/bin/bash

log_file="/home/ubuntu/log/metrics_$(date +'%Y%m%d%H%M%S').log"

echo "mem_total,mem_used,mem_free,mem_shared,mem_buff,mem_available,swap_total,swap_used,swap_free,path,path_size" > "$log_file"

ram_info=$(free -m | awk 'NR==2 {print $2","$3","$4","$5","$6","$7}')
swap_info=$(free -m | awk 'NR==3 {print $2","$3","4}') 

target_path="/home/ubuntu/coba"
path_size=$(du -sh "$target_path" | awk '{print $1}')

echo "$ram_info,$swap_info,$target_path,$path_size" >> "$log_file"
chmod +x $log_file 

# Konfigurasi cron untuk menjalankan skrip ini setiap menit
# * * * * * /home/ubuntu/SISOP/soal_4/minute_log.sh
```

### aggregate_minutes_to_hourly_log.sh

```
#!/bin/bash

log_dir="/home/ubuntu/log"
minute_log_file="$log_dir/metrics_$(date +'%Y%m%d%H').log"
hourly_log_file="$log_dir/metrics_agg_$(date +'%Y%m%d%H').log"


min_ram_total=
min_ram_used=
min_ram_free=
min_ram_shared=
min_ram_buff=
min_ram_available=
max_ram_total=
max_ram_used=
max_ram_free=
max_ram_shared=
max_ram_buff=
max_ram_available=
sum_ram_total=0
sum_ram_used=0
sum_ram_free=0
sum_ram_shared=0
sum_ram_buff=0
sum_ram_available=0
count=0

min_swap_total=
min_swap_used=
min_swap_free=
max_swap_total=
max_swap_used=
max_swap_free=
sum_swap_total=0
sum_swap_used=0
sum_swap_free=0

min_disk_size=
max_disk_size=
sum_disk_size=0

for file in $log_dir/*.log; do

    metrics=$(sed -n '2p' "$file")

    IFS=',' read -r mem_total mem_used mem_free mem_shared mem_buff mem_available swap_total swap_used swap_free path path_size <<< "$metrics"

    if [[ -z $min_ram_total || $mem_total -lt $min_ram_total ]]; then
        min_ram_total=$mem_total
    fi
    if [[ -z $min_ram_used || $mem_used -lt $min_ram_used ]]; then
        min_ram_used=$mem_used
    fi
    if [[ -z $min_ram_free || $mem_free -lt $min_ram_free ]]; then
        min_ram_free=$mem_free
    fi
    if [[ -z $min_ram_shared || $mem_shared -lt $min_ram_shared ]]; then
        min_ram_shared=$mem_shared
    fi
    if [[ -z $min_ram_buff || $mem_buff -lt $min_ram_buff ]]; then
        min_ram_buff=$mem_buff
    fi
    if [[ -z $min_ram_available || $mem_available -lt $min_ram_available ]]; then
        min_ram_available=$mem_available
    fi

    if [[ -z $max_ram_total || $mem_total -gt $max_ram_total ]]; then
        max_ram_total=$mem_total
    fi
    if [[ -z $max_ram_used || $mem_used -gt $max_ram_used ]]; then
        max_ram_used=$mem_used
    fi
    if [[ -z $max_ram_free || $mem_free -gt $max_ram_free ]]; then
        max_ram_free=$mem_free
    fi
    if [[ -z $max_ram_shared || $mem_shared -gt $max_ram_shared ]]; then
        max_ram_shared=$mem_shared
    fi
    if [[ -z $max_ram_buff || $mem_buff -gt $max_ram_buff ]]; then
        max_ram_buff=$mem_buff
    fi
    if [[ -z $max_ram_available || $mem_available -gt $max_ram_available ]]; then
        max_ram_available=$mem_available
    fi

    ((sum_ram_total += mem_total))
    ((sum_ram_used += mem_used))
    ((sum_ram_free += mem_free))
    ((sum_ram_shared += mem_shared))
    ((sum_ram_buff += mem_buff))
    ((sum_ram_available += mem_available))

    if [[ -z $min_swap_total || $swap_total -lt $min_swap_total ]]; then
        min_swap_total=$swap_total
    fi
    if [[ -z $min_swap_used || $swap_used -lt $min_swap_used ]]; then
        min_swap_used=$swap_used
    fi
    if [[ -z $min_swap_free || $swap_free -lt $min_swap_free ]]; then
        min_swap_free=$swap_free
    fi

    if [[ -z $max_swap_total || $swap_total -gt $max_swap_total ]]; then
        max_swap_total=$swap_total
    fi
    if [[ -z $max_swap_used || $swap_used -gt $max_swap_used ]]; then
        max_swap_used=$swap_used
    fi
    if [[ -z $max_swap_free || $swap_free -gt $max_swap_free ]]; then
        max_swap_free=$swap_free
    fi

    ((sum_swap_total += swap_total))
    ((sum_swap_used += swap_used))
    ((sum_swap_free += swap_free))

    disk_size="${path_size//[!0-9]/}"
    if [[ -z $min_disk_size || $disk_size -lt $min_disk_size ]]; then
        min_disk_size=$disk_size
    fi
    if [[ -z $max_disk_size || $disk_size -gt $max_disk_size ]]; then
        max_disk_size=$disk_size
    fi
    ((sum_disk_size += disk_size))

    ((count++))
done

avg_ram_total=$(bc <<< "scale=2; $sum_ram_total / $count")
avg_ram_used=$(bc <<< "scale=2; $sum_ram_used / $count")
avg_ram_free=$(bc <<< "scale=2; $sum_ram_free / $count")
avg_ram_shared=$(bc <<< "scale=2; $sum_ram_shared / $count")
avg_ram_buff=$(bc <<< "scale=2; $sum_ram_buff / $count")
avg_ram_available=$(bc <<< "scale=2; $sum_ram_available / $count")

avg_swap_total=$(bc <<< "scale=2; $sum_swap_total / $count")
avg_swap_used=$(bc <<< "scale=2; $sum_swap_used / $count")
avg_swap_free=$(bc <<< "scale=2; $sum_swap_free / $count")

avg_disk_size=$(bc <<< "scale=2; $sum_disk_size / $count")

echo "type,mem_total,mem_used,mem_free,mem_shared,mem_buff,mem_available,swap_total,swap_used,swap_free,path,path_size" > $hourly_log_file
echo "maximum,$max_ram_total,$max_ram_used,$max_ram_free,$max_ram_shared,$max_ram_buff,$max_ram_available,$max_swap_total,$max_swap_used,$max_swap_free,/home/ubuntu,$max_disk_size" >> $hourly_log_file
echo "minimum,$min_ram_total,$min_ram_used,$min_ram_free,$min_ram_shared,$min_ram_buff,$min_ram_available,$min_swap_total,$min_swap_used,$min_swap_free,/home/ubuntu,$min_disk_size" >> $hourly_log_file
echo "average,$avg_ram_total,$avg_ram_used,$avg_ram_free,$avg_ram_shared,$avg_ram_buff,$avg_ram_available,$avg_swap_total,$avg_swap_used,$avg_swap_free,/home/ubuntu,$avg_disk_size" >> $hourly_log_file

chmod 600 $hourly_log_file

# Konfigurasi cron untuk menjalankan skrip ini setiap jam
# 0 * * * * /home/ubuntu/SISOP/soal_4/aggregate_minutes_to_hourly_log.sh
```
## ***PENJELASAN PENGERJAAN***

a. ###### bc 
`digunakan agar perhitungan dari aritmatika bisa 2 angka di belakang koma`

b. ###### -z 
`digunakan untuk menguji apakah string tersebut kosong atau tidak`

c. ###### [-p] 
`digunakan untuk memeriksa apakah file ada dan dapat diakses`

d. ###### IFS 
`digunakan untuk menentukan pemisah karakter`

e. ###### sed -n 
`diguanakan untuk menampilkan output yang dipilih dan yang lain diabaikan `

## *Membuat metrics ke dalam suatu file log bernama metrics yang akan berjalan otomatis tiap menit*

- Variabel log_file diinisialisasi dengan path file log yang akan dibuat. Nama file akan berisi tanggal dan waktu saat ini dalam format YYYYMMDDHHMMSS.
```
log_file="/home/ubuntu/log/metrics_$(date +'%Y%m%d%H%M%S').log"
```
- Menulis header kolom ke file log yang sudah diinisialisasi sebelumnya.
```
echo "mem_total,mem_used,mem_free,mem_shared,mem_buff,mem_available,swap_total,swap_used,swap_free,path,path_size" > "$log_file"
```
- ram_info=... untuk mendapatkan informasi tentang RAM. Outputnya diproses oleh awk untuk mendapatkan nilai yang sesuai, lalu disimpan dalam variabel ram_info.

- swap_info=... untuk mendapatkan informasi tentang swap. Outputnya diproses oleh awk untuk mendapatkan nilai yang sesuai, lalu disimpan dalam variabel swap_info.
```
ram_info=$(free -m | awk 'NR==2 {print $2","$3","$4","$5","$6","$7}')
swap_info=$(free -m | awk 'NR==3 {print $2","$3","4}') 
```
- target_path=... menetapkan path direktori yang akan diamati.

- path_size=... menjalankan perintah du -sh untuk mendapatkan ukuran direktori target. Outputnya diproses oleh awk untuk mendapatkan ukuran dalam format yang sesuai, lalu disimpan dalam variabel path_size.

```
target_path="/home/ubuntu/coba"
path_size=$(du -sh "$target_path" | awk '{print $1}')
```
- echo "$ram_info ... menulisksan informasi RAM, swap, path, dan ukuran path ke file log yang sudah diinisialisasi sebelumnya.

- chmod +x $log_file akan memberikan izin eksekusi pada file log.
```
echo "$ram_info,$swap_info,$target_path,$path_size" >> "$log_file"
chmod +x $log_file 
```
- menjelaskan konfigurasi cron akan ditambahkan

- * * * * * /home/ubuntu/SISOP/soal_4/minute_log.sh adalah konfigurasi cron yang akan menjalankan skrip ini setiap menit
```
# Konfigurasi cron untuk menjalankan skrip ini setiap menit
# * * * * * /home/ubuntu/SISOP/soal_4/minute_log.sh
```

## *Membuat satu script untuk membuat agregasi file log ke satuan jam. Script agregasi akan memiliki info dari file-file yang tergenerate tiap menit. Dalam hasil file agregasi tersebut, terdapat nilai minimum, maximum, dan rata-rata dari tiap-tiap metrics. File agregasi akan ditrigger untuk dijalankan setiap jam secara otomatis*

- direktori di mana file log akan disimpan
```
log_dir="/home/ubuntu/log"
```
- path ke file log yang menyimpan data per menit. Nama file didasarkan pada tanggal dan jam saat ini dalam format YYYYMMDDHH
```
minute_log_file="$log_dir/metrics_$(date +'%Y%m%d%H').log"
```
- path ke file log yang akan berisi data agregat per jam. Nama file juga didasarkan pada tanggal dan jam saat ini dalam format YYYYMMDDHH
```
hourly_log_file="$log_dir/metrics_agg_$(date +'%Y%m%d%H').log"
```
-membuat direktori log jika belum ada
```
mkdir -p $log_dir
```
- variabel yang diinisialisasi untuk menyimpan metrik RAM, swap, dan disk. Metrik ini akan digunakan untuk menghitung nilai minimum, maksimum, dan rata-rata
```
min_ram_total=
min_ram_used=
min_ram_free=
min_ram_shared=
min_ram_buff=
min_ram_available=
max_ram_total=
max_ram_used=
max_ram_free=
max_ram_shared=
max_ram_buff=
max_ram_available=
sum_ram_total=0
sum_ram_used=0
sum_ram_free=0
sum_ram_shared=0
sum_ram_buff=0
sum_ram_available=0
count=0

min_swap_total=
min_swap_used=
min_swap_free=
max_swap_total=
max_swap_used=
max_swap_free=
sum_swap_total=0
sum_swap_used=0
sum_swap_free=0

min_disk_size=
max_disk_size=
sum_disk_size=0
```
- loop for untuk membaca file log yang tersedia di direktori log. Di dalam loop, baris kedua dari setiap file log dibaca menggunakan sed -n '2p' "$file". Kemudian, data tersebut dipecah menjadi metrik individual menggunakan perintah read
```
for file in $log_dir/*.log; do

    metrics=$(sed -n '2p' "$file")
```
- setiap metrik kemudian dibandingkan untuk menemukan nilai minimum dan maksimum, serta digabungkan untuk menghitung rata-rata
```
    IFS=',' read -r mem_total mem_used mem_free mem_shared mem_buff mem_available swap_total swap_used swap_free path path_size <<< "$metrics"

    if [[ -z $min_ram_total || $mem_total -lt $min_ram_total ]]; then
        min_ram_total=$mem_total
    fi
    if [[ -z $min_ram_used || $mem_used -lt $min_ram_used ]]; then
        min_ram_used=$mem_used
    fi
    if [[ -z $min_ram_free || $mem_free -lt $min_ram_free ]]; then
        min_ram_free=$mem_free
    fi
    if [[ -z $min_ram_shared || $mem_shared -lt $min_ram_shared ]]; then
        min_ram_shared=$mem_shared
    fi
    if [[ -z $min_ram_buff || $mem_buff -lt $min_ram_buff ]]; then
        min_ram_buff=$mem_buff
    fi
    if [[ -z $min_ram_available || $mem_available -lt $min_ram_available ]]; then
        min_ram_available=$mem_available
    fi

    if [[ -z $max_ram_total || $mem_total -gt $max_ram_total ]]; then
        max_ram_total=$mem_total
    fi
    if [[ -z $max_ram_used || $mem_used -gt $max_ram_used ]]; then
        max_ram_used=$mem_used
    fi
    if [[ -z $max_ram_free || $mem_free -gt $max_ram_free ]]; then
        max_ram_free=$mem_free
    fi
    if [[ -z $max_ram_shared || $mem_shared -gt $max_ram_shared ]]; then
        max_ram_shared=$mem_shared
    fi
    if [[ -z $max_ram_buff || $mem_buff -gt $max_ram_buff ]]; then
        max_ram_buff=$mem_buff
    fi
    if [[ -z $max_ram_available || $mem_available -gt $max_ram_available ]]; then
        max_ram_available=$mem_available
    fi

    ((sum_ram_total += mem_total))
    ((sum_ram_used += mem_used))
    ((sum_ram_free += mem_free))
    ((sum_ram_shared += mem_shared))
    ((sum_ram_buff += mem_buff))
    ((sum_ram_available += mem_available))

    if [[ -z $min_swap_total || $swap_total -lt $min_swap_total ]]; then
        min_swap_total=$swap_total
    fi
    if [[ -z $min_swap_used || $swap_used -lt $min_swap_used ]]; then
        min_swap_used=$swap_used
    fi
    if [[ -z $min_swap_free || $swap_free -lt $min_swap_free ]]; then
        min_swap_free=$swap_free
    fi

    if [[ -z $max_swap_total || $swap_total -gt $max_swap_total ]]; then
        max_swap_total=$swap_total
    fi
    if [[ -z $max_swap_used || $swap_used -gt $max_swap_used ]]; then
        max_swap_used=$swap_used
    fi
    if [[ -z $max_swap_free || $swap_free -gt $max_swap_free ]]; then
        max_swap_free=$swap_free
    fi

    ((sum_swap_total += swap_total))
    ((sum_swap_used += swap_used))
    ((sum_swap_free += swap_free))

    disk_size="${path_size//[!0-9]/}"
    if [[ -z $min_disk_size || $disk_size -lt $min_disk_size ]]; then
        min_disk_size=$disk_size
    fi
    if [[ -z $max_disk_size || $disk_size -gt $max_disk_size ]]; then
        max_disk_size=$disk_size
    fi
    ((sum_disk_size += disk_size))

    ((count++))
done
avg_ram_total=$(bc <<< "scale=2; $sum_ram_total / $count")
avg_ram_used=$(bc <<< "scale=2; $sum_ram_used / $count")
avg_ram_free=$(bc <<< "scale=2; $sum_ram_free / $count")
avg_ram_shared=$(bc <<< "scale=2; $sum_ram_shared / $count")
avg_ram_buff=$(bc <<< "scale=2; $sum_ram_buff / $count")
avg_ram_available=$(bc <<< "scale=2; $sum_ram_available / $count")

avg_swap_total=$(bc <<< "scale=2; $sum_swap_total / $count")
avg_swap_used=$(bc <<< "scale=2; $sum_swap_used / $count")
avg_swap_free=$(bc <<< "scale=2; $sum_swap_free / $count")

avg_disk_size=$(bc <<< "scale=2; $sum_disk_size / $count")
```
- setelah loop selesai, metrik agregat diprint ke file log
```
echo "type,mem_total,mem_used,mem_free,mem_shared,mem_buff,mem_available,swap_total,swap_used,swap_free,path,path_size" > $hourly_log_file
echo "maximum,$max_ram_total,$max_ram_used,$max_ram_free,$max_ram_shared,$max_ram_buff,$max_ram_available,$max_swap_total,$max_swap_used,$max_swap_free,/home/ubuntu,$max_disk_size" >> $hourly_log_file
echo "minimum,$min_ram_total,$min_ram_used,$min_ram_free,$min_ram_shared,$min_ram_buff,$min_ram_available,$min_swap_total,$min_swap_used,$min_swap_free,/home/ubuntu,$min_disk_size" >> $hourly_log_file
echo "average,$avg_ram_total,$avg_ram_used,$avg_ram_free,$avg_ram_shared,$avg_ram_buff,$avg_ram_available,$avg_swap_total,$avg_swap_used,$avg_swap_free,/home/ubuntu,$avg_disk_size" >> $hourly_log_file
```
- memberikan izin pada file log
```
chmod 600 $hourly_log_file
```
- konfigurasi cron yang diperlukan untuk menjalankan skrip ini setiap jam.
```
# Konfigurasi cron untuk menjalankan skrip ini setiap jam
# 0 * * * * /home/ubuntu/SISOP/soal_4/aggregate_minutes_to_hourly_log.sh
```
## *Dokumentasi*

![Minute log sh](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/150375098/1bce9096-4dea-4f2d-ac00-f800dda0ed2b)
![Isi minute log sh](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/150375098/943f5457-9d66-4f66-acab-4cedf328646f)
![Jam ke menit](https://github.com/Rafjonath/Sisop-1-2024-MH-IT26/assets/150375098/e1c6985b-d747-461e-9841-6696338e39a5) 
