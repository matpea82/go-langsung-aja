# **BAB 1**


## **Memasang Lingkungan Go**  


Setiap bahasa pemrograman memerlukan sebuah lingkungan pengembangan, dan tidak terkecuali Go. 


Jika Anda sudah pernah menulis sebuah program Go atau dua, Anda sudah dipastikan memiliki sebuah lingkungan yang bekerja, namun demikian mungkin saja Anda melewatkan beberapa teknik-teknik dan perkakas-perkakas terkini. 


Jika saat ini adalah pertama kalinya Anda memasang Go di komputer Anda, jangan khawatir; memasang Go dan perkakas pendukungnya adalah perkara mudah.  


Setelah kita telah selesai memasang dan memastikannya, kita akan membangun sebuah program sederhana, mempelajari cara-cara membangun yang berbeda-beda dan melarikan kode Go, dan kemudian menjelajahi beberapa perkakas-perkakas dan teknik-teknik yang menghasilkan pengembangan Go menjadi mudah.



## **Memasang perkakas-perkakas Go**


Untuk menulis kode Go, Pertama Anda perlu untuk mengunduh dan memasang perkakas-perkakas pengembangan.


Versi terkini perkakas-perkakas tersebut dapat ditemukan pada halaman unduh di [**situs Go**](https://go.dev/download).


Pilihlah unduhan untuk platform dan pasanglah. Pemasang `.pkg` untuk Mac dan `.msi` untuk Windows memasang secara otomatis di dalam lokasi yang benar, menghilangkan pemasangan yang lama, dan meletakkan biner Go di dalam path eksekusi semberono.


> Jika Anda adalah seorang pengembang Mac, Anda dapat memasang Go menggunakan **Homebrew** dengan perintah `brew install`.   
> Pengembang-pengembang Windows yang menggunakan **Chocolatey** dapat memasang dengan menggunakan perintah `choco install golang`.  


Pemasang-pemasang Linux yang beranekaragam dan FreeBSD adalah mereka itu berupa berkas-berkas tar yang di-gzip-kan dan membentang ke sebuah direktori yang bernama `go`. Salin direktori ini ke `/usr/local` dan tambahkanlah `/usr/local/go/bin` ke `$PATH` Anda sehingga perintah `go` tersebut dapat diakses:


> `$ tar -C /usr/local -xzf go1.15.2.linux-amd64.tar.gz`    
> `$ echo 'export PATH=$PATH:/usr/local/go/bin' >> $HOME/.profile`    
> `$ source $HOME/.profile`


>>>>> program-program Go tersusun-satukan menjadi sebuah biner dan tidak mengharuskan sembarang perangkat lunak tambahan untuk dipasangkan supaya program-program itu berlari. Pasangkanlah perkakas-perkakas pengembangan Go hanya pada komputer-komputer yang digunakan untuk membangun program-program Go.


Anda dapat menvalidasikan bahwa lingkungan Anda sudah terpasang secara benar dengan membuka sebuah terminal atau command prompt dan ketikanlah:


> `go version`


Jika segalanya sudah terpasang secara benar, Anda akan melihat sesuatu seperti berikut ini tercetak:


> `go version go1.15.2 linux/amd64`


Ini memberitahukan bahwa versi Go ialah 1.15.2 pada Linux OS. (Linux ialah nama dari kernel untuk Linux OS dan amd64 ialah nama daripada arsitektur CPU 64-bit baik diproduksi oleh AMD atau Intel.)


Jika Anda memperoleh sebuat galat alih-alih pesan versi tersebut, besar kemungkinannya Anda tidak memiliki `go` di dalam path yang dapat dieksekusi, atau Anda memiliki program yang lain yang juga bernama `go` di dalam path.


Pada Sistem Operasi Mac dan sistem-sistem serupa Unix lainnya, gunakanlah `which go` untuk melihat perintah `go` tersebut sedang dieksekusi, Jika ada. Jika ini bukanlah perintah `go` pada `/usr/local/go/bin/go`, Anda perlu untuk memperbaiki path yang dapat dieksekusi.


Jika Anda ada di Linux atau FreeBSD, adalah mungkin Anda telah memasang perkakas-perkakas pengembangan Go 64-bit pada sebuah sistem 32-bit atau perkakas-perkakas pengembangan tersebut untuk arsitektur chip yang salah.


# **Ruang Kerja Go**


Sejak perkenalan Go di tahun 2009, sudah beberapa banyak perubahan-perubahan dalam hal pengembang-pengembang Go mengorganisir kode mereka dan ketergantungan-ketergantungannya.


Karena kekacauan ini, terdapat banyak saran yang menyebabkan konflik, dan banyak daripadanya sudah usang.


Untuk pengembangan Go yang moderen, Aturannya itu adalah sederhana: Anda bebas untuk mengorganisir proyek Anda yang Anda anggap sesuai.


Walaupun demikian, Go tetap mengharapkan adanya sebuah ruangkerja untuk perkakas-perkakas pihak-ketiga Go terpasang lewat `go install` (lihat ["Memperoleh Perkakas-perkakas Pihakketiga Go" di halaman 5](#).


Secara sembarang, ruangkerja ini berlokasi di dalam `$HOME/go`, bersama dengannya kode sumber daripada perkakas-perkakas ini disimpan di `$HOME/go/src` dan biner tersusun di dalam `$HOME/go/bin`.


Anda dapat menggunakan sembarang ini atau merumuskan `GOPATH` sehingga menjadi jelas lokasi dimana ruangkerja Go dan menambahkan `$GOPATH/bin` ke path yang tereksekusi sehingga menjadi mudah untuk melarikan perkakas-perkakas pihak-ketiga yand dipasang melalui `go install`, yang akan dibicarakan sekejap kemudian.


Jika Anda berada pada sistem serupa Unix yang menggunakan `bash`, tambahkanlah baris-baris berikut ini ke `.profile`.


(Jika Anda menggunakan `zsh`, tambahkan baris-baris ini ke `.zshrc` sebagai gantinya):


> `export GOPATH=$HOME/go`   
> `export PATH=$PATH:$GOPATH/bin`


Anda perlu untuk `source $HOME/.profile` supaya perubahan-perubahan ini efektif di dalam jendela terminal yang sedang aktif.


Pada Windows, larikan perintah-perintah berikut ini pada `command prompt`:


> `setx GOPATH %USERPROFILE%\go`   
> `setx PATH "%PATH%\%GOPATH%\bin"`


Setalah melarikan perintah-perintah ini, Anda wajib menutup `command prompt` yang sekarang dan membuka sebuah yang baru supaya mengefektifkan perubahan-perubahan tersebut.


Ada peubah-perubah lingkungan yang lain yang dikenali oleh perkakas Go.


Ada memperoleh sebuah daftar yang lengkap, bersama dengannya penjelasan singkat dari masing-masing peubah, dengan menggunakan perintah `go env`.


Banyak daripadanya mengendalikan perilaku tataran rendah yang dapat diabaikan dengan aman, tetapi kami lingkupi beberapanya daripada peubah-peubah ini ketika mendiskusikan modul-modul dan kompilasi-lintas.


>>>>>Beberapa sumberdaya daring memberitahukan kepada Anda untuk menyetel peubah lingkungan `GOROOT`.
>Peubah ini merincikan lokasi di mana lingkungan pengembang Go Anda terpasang.
>Ini sudah tidak lagi diperlukan: perkakas go mencaritahu sendiri secara otomatis.


# **Si Perintah Go**


Luar biasa, Go dikemasi dengan banyak perkakas-perkakas pengembangan.

Anda dapat mengakses perkakas-perkakas ini lewat perintah `go`.


Perkakas-perkakas tersebut terkandungi sebuah pengompilasi, pembentuk kode, linter, pengatur ketergantungan, pelari percobaan, dan lebih banyak lagi.


Karena tujuan kita ialah belajar bagaimana membangun Go yang idiom dan berkualitas tinggi, kita akan mengeksplorasi banyak daripada perkakas-perkakas ini sepanjang buku ini.


Mari kita mulakan dengan jenis yang kita gunakan untuk membangun kode Go dan gunakan perintah `go` untuk membangun sebuah aplikasi sederhana.


## **`go run dan go build`**


Ada dua perintah go yang serupa tersedia melalui **go**: `go run` dan `go build`.


Masing-masing daripadanya mengambil sebuah berkas **Go**, sebuah daftar daripada berkas-berkas **Go**, atau nama daripada sebuah paket.


Kita akan membuat sebuah program sederhana dan melihat apa yang terjadi ketika kita gunakan perintah-perintah ini.


### **`go run`**


Kita akan mulakan dengan `go run`.


Buatlah sebuah direktori sebutlah sebagai ch1, bukalah sebuah penyunting teks, masukkanlah teks berikut, dan simpanlah ia ke sebuah berkas `hello.go` di dalam ch1:


```go
package main

import "fmt"

func main() {
    fmt.Println("Apa khabar, dunia!")
}
```


Setelah berkas tersebut disimpan, bukalah sebuah `terminal` atau `commnd prompt` dan ketikkanlah:


> **`go run hello.go`**


Anda akan melihat `Apa khabar, dunia!` tercetak di dalam `console`.


Jika Anda melihat ke dalam direktori tersebut setalah melarikan perintah `go run` tersebut, Anda lihat bahwa tiada biner yang tersimpan di sana; Berkas satu-satunya di dalam direktori tersebut ialah berkas `hello.go` yang baru saja kita ciptakan.


Anda mungkin saja berfikir: saya fikir Go ialah sebuah bahasa yang dikompilasi.

Apa yang sedang terjadi?

perintah `go run` tersebut faktanya mengompilasikan kode Anda kepada sebuah biner.


Akan tetapi, biner tersebut dibangun di dalam sebuah direktori sementara.


perintah `go run` membangun biner tersebut, mengeksekusi biner tersebut dari direktori sementara tersebut dan kemudian menghapus biner tersebut setelah program berakhir.


Ini menjadikan perintah `go run` berguna untuk percobaan program sederhana atau gunakan Go selayaknya sebuah bahasa skrip.


>>>>> Gunakan `go run` ketika Anda ingin memperlakukan sebuah program Go seperti sebuah skrip dan melarikan kode sumber segera.


## **`go build`**


Seringnya Anda ingin membangun sebuah biner untuk digunakan di kemudian.


Itu adalah tempatnya Anda untuk gunakan perintah `go build` tersebut.


Pada baris berikutnya di dalam `terminal` Anda, ketikanlah:


> **`go build hello.go`**


Perintah ini menciptakan sebuah `executable` yang disebut `hello` (atau `hello.exe` pada Windows) di dalam direktori sekarang tersebut.


Larikanlah dia dan Anda tanpa terkejut melihat `Apa khabar, dunia!` tercetak pada layar tersebut.


Nama daripada biner tersebut bersesuaian dengan nama daripada berkas tersebut atau paket yang Anda sampaikan kepadanya.


Jika Anda menghendaki sebuah nama yang berbeda untuk aplikasi Anda, atau jika Anda hendak menyimpannya di dalam sebuah lokasi yang berbeda, gunakanlah flag `-o`. Sebagai contoh, jika kita ingin mengompilasikan kode kita ke sebuah biner yang disebut sebagai `"hello_world,"` kita akan gunakan:


> `go build -o hello_world hello.go`


>>>>> Gunakan `go build` untuk menciptakan sebuah biner yang disalurkan untuk digunakan oleh orang-orang lain. 
>>>>> Seringnya, inilah yang Anda ingin untuk dilakukan. 
>>>>> Gunakan flag `-o` untuk memberikan nama atau lokasi yang berbeda. 


## **Memperoleh Perkakas-Perkakas Go Pihak Ketiga**


Sementara beberapa orang-orang memilih untuk menyalurkan program-program Go milik mereka sebagai biner terkompilasi-sebelumnya, perkakas-perkakas yang ditulis dalam Go dapat juga dibangun dari sumber dan dipasangkan kepada ruangkerja Go Anda melalui perintah `go install`.


Metode daripada Go dalam hal menerbitkan kode ialah sedikit berbeda dibandingkan dengan bahasa-bahasa lain.


Pengembang-pengembang Go tidak mengandalkan pada sebuah layanan yang termiliki serta terpusat, seperti `Maven Central` pada `Java` atau `NPM registry` pada `JavaScript`.


Sebagai gantinya, pengembang-pengembang tersebut membagikan proyek-proyek melalui repositori-repositori kode sumber.


Perintah `go install` tersebut mengambil sebuah `argument`, yaitu lokasinya repositori kode sumber daripada proyek tersebut yang Anda hendak pasang, diikuti oleh sebuah `@` dan versinya perkakas yang Anda mau (jika Anda hanya hendak memperoleh versi mutakhir, gunakan `@latest`).


Dia kemudian mengunduh, mengompilasi, dan memasang perkakas tersebut ke `$GOPATH/bin` Anda.


Marilah kita cermati sebuah contoh singkat.  Ada sebuah perkakas Go hebat yang disebut sebagai `hey` yang mencoba server-server HTTP dengan beban.  Anda dapat mengarahkannya pada situs yang anda pilih atau sebuah aplikasi yang telah Anda tulis.  Berikut ini bagaimana cara untuk memasang `hey` dengan perintah `go install` tersebut:


>
```bash
    $ go install github.com/rakyll/hey@latest
    go: downloading github.com/rakyll/hey v0.1.4
    go: downloading golang.org/x/net v0.0.0-20181017193950-04a2e542c03f
    go: dowloading golang.org/x/text v0.3.0
```