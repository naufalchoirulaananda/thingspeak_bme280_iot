
# Monitoring Suhu dengan ESP32 dan ThingSpeak



Proyek ini menunjukkan cara menggunakan board ESP32 untuk membaca data suhu dari sensor BME280 dan mengirimkannya ke ThingSpeak untuk pemantauan jarak jauh. ESP32 terhubung ke jaringan Wi-Fi, membaca data suhu dari sensor, dan secara berkala mengunggah data tersebut ke saluran ThingSpeak.
## Komponen

 - Board pengembangan ESP32
 - Sensor BME280
 - Kabel jumper
 - Breadboard

## Pustaka

- WiFi
- ThingSpeak
- Adafruit BME280
- Adafruit Sensor
## Diagram Sirkuit

Hubungkan sensor BME280 ke ESP32 sebagai berikut:

| Pin BME280             | Pin ESP32                                                                |
| ----------------- | ------------------------------------------------------------------ |
| VCC | 3.3V |
| GND | GND |
| SCL | GPIO 22 |
| SDA | GPIO 21 |


## Penjelasan Kode

### Variable Global

- `ssid` dan `password`: Kredensial Wi-Fi untuk menghubungkan ke jaringan.
- `client`: Klien Wi-Fi yang digunakan untuk komunikasi dengan ThingSpeak.
- `myChannelNumber` dan `myWriteAPIKey`: Nomor saluran dan kunci API ThingSpeak.
- `lastTime` dan `timerDelay`: Variabel untuk mengatur waktu pembacaan suhu.
- `temperatureC`: Variabel untuk menyimpan pembacaan suhu dari sensor BME280.
- `bme`: Objek sensor BME280.
### Fungsi

- `initBME()`: Menginisialisasi sensor BME280.
- `setup()`: Mengatur komunikasi serial, menginisialisasi sensor BME280, mengatur mode Wi-Fi, dan menginisialisasi ThingSpeak.
- `loop()`: Loop utama yang memeriksa timer, menghubungkan ke Wi-Fi jika tidak terhubung, membaca suhu dari sensor BME280, dan mengunggah data ke ThingSpeak.


### Koneksi Wi-Fi

Fungsi `loop()` memeriksa apakah ESP32 terhubung ke Wi-Fi. Jika tidak, ESP32 akan mencoba menghubungkan ke jaringan Wi-Fi yang ditentukan. Setelah terhubung, ESP32 akan melanjutkan untuk membaca data suhu.


### Membaca dan Mengirim Data

Suhu dibaca dari sensor BME280 dan dicetak ke monitor serial. Data kemudian dikirim ke ThingSpeak menggunakan fungsi `ThingSpeak.writeField()`. Kode respons diperiksa untuk memastikan apakah unggahan data berhasil.

## Dependensi

Instal pustaka berikut melalui Arduino Library Manager:

- WiFi
- ThingSpeak
- Adafruit BME280
- Adafruit Unified Sensor


## Cara Penggunaan

- Set Up Saluran ThingSpeak: Buat akun ThingSpeak dan buat saluran baru. Catat nomor saluran dan kunci API tulis.
- Konfigurasi Kode: Perbarui variabel `myChannelNumber` dan `myWriteAPIKey` dengan nomor saluran ThingSpeak dan kunci API tulis Anda. Juga, perbarui ssid dan password dengan kredensial Wi-Fi Anda.
- Unggah Kode: Hubungkan ESP32 ke komputer Anda dan unggah kode menggunakan Arduino IDE.
- Pantau Data: Buka monitor serial untuk melihat pembacaan suhu dan status unggahan data. Anda juga dapat masuk ke akun ThingSpeak Anda untuk melihat data yang diunggah.


## Contoh Output

```bash
Attempting to connect
Connected.
Temperature (ºC): 25.68
Channel update successful.

```

## Pemecahan Masalah

- Pastikan sensor BME280 terhubung dengan benar ke ESP32.
- Verifikasi kredensial Wi-Fi sudah benar.
- Periksa nomor saluran dan kunci API ThingSpeak Anda.
- Jika sensor tidak terdeteksi, periksa alamat I2C (default adalah 0x76) dan sesuaikan jika perlu.
