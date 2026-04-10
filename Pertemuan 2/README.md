2.5.4 Pertanyaan Praktikum 
1. Gambarkan rangkaian schematic yang digunakan pada percobaan! 
2. Apa yang terjadi jika nilai num lebih dari 15? 
3. Apakah program ini menggunakan common cathode atau common anode? Jelaskan 
alasanya! 
4. Modifikasi program agar tampilan berjalan dari F ke 0 dan berikan penjelasan disetiap 
baris kode nya dalam bentuk README.md!

Jawaban:
1. 
2. Jika nilai variabel num lebih dari 15, maka program akan mencoba mengakses indeks array digitPattern yang berada di luar batas yang telah ditentukan. Hal ini dikarenakan array tersebut hanya memiliki 16 data dengan indeks mulai dari 0 hingga 15 yang merepresentasikan angka 0 sampai F dalam sistem heksadesimal. Akibatnya, sistem tidak akan menampilkan angka yang benar pada 7-segment, melainkan dapat menghasilkan tampilan yang tidak sesuai atau acak. Dalam beberapa kasus, kondisi ini juga dapat menyebabkan program menjadi tidak stabil.


2.6.4 Pertanyaan Praktikum 
1. Gambarkan rangkaian schematic yang digunakan pada percobaan! 
2. Mengapa pada push button digunakan mode INPUT_PULLUP pada Arduino Uno? 
Apa keuntungannya dibandingkan rangkaian biasa? 
3. Jika salah satu LED segmen tidak menyala, apa saja kemungkinan penyebabnya dari 
sisi hardware maupun software? 
4. Modifikasi rangkaian dan program dengan dua push button yang berfungsi sebagai 
penambahan (increment) dan pengurangan (decrement) pada sistem counter dan 
berikan penjelasan disetiap baris kode nya dalam bentuk README.md!
