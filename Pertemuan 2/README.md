2.5.4 Pertanyaan Praktikum 
1. Gambarkan rangkaian schematic yang digunakan pada percobaan! 
2. Apa yang terjadi jika nilai num lebih dari 15? 
3. Apakah program ini menggunakan common cathode atau common anode? Jelaskan 
alasanya! 
4. Modifikasi program agar tampilan berjalan dari F ke 0 dan berikan penjelasan disetiap 
baris kode nya dalam bentuk README.md!

Jawaban:
1. Gambar Rangkaian Schematic <img width="1025" height="795" alt="image" src="https://github.com/user-attachments/assets/d26728d5-bdd9-47f0-b9f1-a2066ebc8af2" />
2. Jika nilai variabel num lebih dari 15, maka program akan mencoba mengakses indeks array digitPattern yang berada di luar batas yang telah ditentukan. Hal ini dikarenakan array tersebut hanya memiliki 16 data dengan indeks mulai dari 0 hingga 15 yang merepresentasikan angka 0 sampai F dalam sistem heksadesimal. Akibatnya, sistem tidak akan menampilkan angka yang benar pada 7-segment, melainkan dapat menghasilkan tampilan yang tidak sesuai atau acak. Dalam beberapa kasus, kondisi ini juga dapat menyebabkan program menjadi tidak stabil.
3. Program ini menggunakan 7-segment tipe **common anode**, yang dapat dilihat dari pola pada array `digitPattern` serta penggunaan logika pembalik pada fungsi `displayDigit()`. Pada array tersebut, nilai `1` merepresentasikan LED mati dan `0` merepresentasikan LED menyala, yang merupakan ciri dari common anode. Selain itu, pada saat data dikirim ke pin menggunakan `digitalWrite(segmentPins[i], !digitPattern[num][i]);`, nilai pada array dibalik terlebih dahulu menggunakan operator NOT (`!`). Hal ini dilakukan karena pada common anode, LED akan menyala ketika diberi logika LOW (0), sehingga diperlukan pembalikan logika agar tampilan yang dihasilkan sesuai dengan pola digit yang diinginkan.
4. Modifikasi kode
```cpp
#include <Arduino.h>

// Pin mapping segment: a b c d e f g dp
const int segmentPins[8] = {7, 6, 5, 11, 10, 8, 9, 4};

byte digitPattern[16][8] = {
  {1,1,1,1,1,1,0,0}, //0
  {0,1,1,0,0,0,0,0}, //1
  {1,1,0,1,1,0,1,0}, //2
  {1,1,1,1,0,0,1,0}, //3 
  {0,1,1,0,0,1,1,0}, //4
  {1,0,1,1,0,1,1,0}, //5
  {1,0,1,1,1,1,1,0}, //6
  {1,1,1,0,0,0,0,0}, //7
  {1,1,1,1,1,1,1,0}, //8
  {1,1,1,1,0,1,1,0}, //9
  {1,1,1,0,1,1,1,0}, //A
  {0,0,1,1,1,1,1,0}, //b
  {1,0,0,1,1,1,0,0}, //C
  {0,1,1,1,1,0,1,0}, //d
  {1,0,0,1,1,1,1,0}, //E
  {1,0,0,0,1,1,1,0}  //F
};

// Fungsi tampil digit (dibalik untuk Common Anode)
void displayDigit(int num)
{
  for(int i=0; i<8; i++)
  {
    digitalWrite(segmentPins[i], !digitPattern[num][i]);
  }
}

void setup()
{
  for(int i=0; i<8; i++)
  {
    pinMode(segmentPins[i], OUTPUT);
  }
}

void loop()
{
  // Hitung mundur dari F (15) ke 0
  for(int i = 15; i >= 0; i--)
  {
    displayDigit(i);
    delay(1000);
  }
}
```
   


2.6.4 Pertanyaan Praktikum 
1. Gambarkan rangkaian schematic yang digunakan pada percobaan! 
2. Mengapa pada push button digunakan mode INPUT_PULLUP pada Arduino Uno? 
Apa keuntungannya dibandingkan rangkaian biasa? 
3. Jika salah satu LED segmen tidak menyala, apa saja kemungkinan penyebabnya dari 
sisi hardware maupun software? 
4. Modifikasi rangkaian dan program dengan dua push button yang berfungsi sebagai 
penambahan (increment) dan pengurangan (decrement) pada sistem counter dan 
berikan penjelasan disetiap baris kode nya dalam bentuk README.md!

Jawaban:
1. Gambar Rangkaian Schematic <img width="1015" height="785" alt="image" src="https://github.com/user-attachments/assets/f513a3cc-e93f-4a1f-8b43-bfd8adc4e09a" />
2. Penggunaan mode INPUT_PULLUP pada Arduino Uno bertujuan untuk mengaktifkan resistor pull-up internal sehingga pin input akan berada pada kondisi HIGH secara default ketika tombol tidak ditekan. Ketika tombol ditekan, pin akan terhubung ke ground sehingga berubah menjadi LOW. Keuntungan penggunaan INPUT_PULLUP dibandingkan rangkaian biasa adalah tidak memerlukan resistor eksternal, rangkaian menjadi lebih sederhana, serta mengurangi risiko kondisi floating (nilai input tidak stabil) yang dapat menyebabkan pembacaan sinyal menjadi tidak konsisten.
3. Dari sisi hardware:
   - Kabel tidak terhubung dengan benar
   - Resistor rusak atau tidak terpasang
   - LED segment pada 7-segment rusak
   - Pin Arduino rusak
   - Salah wiring (tertukar pin)
   Dari sisi software:
   - Kesalahan pada digitPattern
   - Index array salah
   - Pin mapping tidak sesuai dengan rangkaian
   - Tidak menggunakan pinMode OUTPUT
   - Logika terbalik (common anode vs cathode)
4. Modifikasi
```cpp
#include <Arduino.h>

// 7-Segment Common Anode
// Pin mapping segment: a b c d e f g dp
const int segmentPins[8] = {7, 6, 5, 11, 10, 8, 9, 4};

// Pin button
const int btnUp = 2;
const int btnDown = 3;

int currentNumber = 0;

// Pola digit
byte digitPattern[16][8] = {
  {1,1,1,1,1,1,0,0}, //0
  {0,1,1,0,0,0,0,0}, //1
  {1,1,0,1,1,0,1,0}, //2
  {1,1,1,1,0,0,1,0}, //3 
  {0,1,1,0,0,1,1,0}, //4
  {1,0,1,1,0,1,1,0}, //5
  {1,0,1,1,1,1,1,0}, //6
  {1,1,1,0,0,0,0,0}, //7
  {1,1,1,1,1,1,1,0}, //8
  {1,1,1,1,0,1,1,0}, //9
  {1,1,1,0,1,1,1,0}, //A
  {0,0,1,1,1,1,1,0}, //b
  {1,0,0,1,1,1,0,0}, //C
  {0,1,1,1,1,0,1,0}, //d
  {1,0,0,1,1,1,1,0}, //E
  {1,0,0,0,1,1,1,0}  //F
};

// Fungsi tampil digit (dibalik untuk CA)
void displayDigit(int num)
{
  for(int i=0; i<8; i++)
  {
    digitalWrite(segmentPins[i], !digitPattern[num][i]);
  }
}

void setup()
{
  // Set segment sebagai output
  for(int i=0; i<8; i++)
  {
    pinMode(segmentPins[i], OUTPUT);
  }

  // Set button
  pinMode(btnUp, INPUT_PULLUP);
  pinMode(btnDown, INPUT_PULLUP);
}

void loop()
{
  // Tombol MAJU
  if(digitalRead(btnUp) == LOW)
  {
    currentNumber++;
    if(currentNumber > 15) currentNumber = 0;
    delay(200); // debounce sederhana
  }

  // Tombol MUNDUR
  if(digitalRead(btnDown) == LOW)
  {
    currentNumber--;
    if(currentNumber < 0) currentNumber = 15;
    delay(200); // debounce sederhana
  }

  displayDigit(currentNumber);
}
