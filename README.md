# 📡 IoT Radar Scanner & Monitoring System (ESP32 + Web Dashboard)

Sistem Radar berbasis Internet of Things (IoT) yang mendeteksi objek di sekitar menggunakan sensor ultrasonik HC-SR04 yang diputar oleh Motor Servo. Data sudut dan jarak yang didapatkan dikirimkan secara *real-time* ke **Web Dashboard** lokal via protokol HTTP API (Polling System). Proyek ini juga dilengkapi dengan indikator fisik (*traffic light module* dan alarm buzzer) serta kendali ambang batas (*threshold*) langsung dari web.

---

## 🚀 Fitur Utama
* **Scanning Otomatis**: Motor servo melakukan *sweeping* horizontal dari sudut 0° hingga 180° dan kembali lagi secara presisi.
* **Filter Data Cerdas**: Pengukuran jarak dioptimalkan hanya pada sudut genap untuk mencegah *stuttering* (gerakan servo tersendat).
* **Indikator Keamanan Fisik (3 Zona)**:
  * 🔴 **Zona Bahaya (1-15 cm)**: LED Merah Menyala + Buzzer Berbunyi konstan.
  * 🟡 **Zona Waspada (16-30 cm)**: LED Kuning Menyala + Buzzer Mati.
  * 🟢 **Zona Aman (>30 cm)**: LED Hijau Menyala + Buzzer Mati.
* **Integrasi Web Dashboard**: Menyediakan Endpoint API `/data` dalam format JSON yang diperbarui setiap 200 ms via Port 80.
* **Cross-Origin Resource Sharing (CORS) Enabled**: Server ESP32 dikonfigurasi agar dapat diakses dengan aman oleh browser web lokal tanpa kendala pemblokiran privasi.

---

## 🛠️ Komponen Elektronik & Pinout

Komponen yang digunakan beserta konfigurasi pin pada ESP32:

| Nama Komponen | Pin Komponen | Pin GPIO ESP32 | Keterangan |
| :--- | :--- | :--- | :--- |
| **Sensor Ultrasonik HC-SR04** | Trig | `GPIO 5` | Memicu pulsa ultrasonik |
| | Echo | `GPIO 18` | Menerima pantulan gelombang |
| **Motor Servo SG90 / MG90S** | PWM / Data (Oranye) | `GPIO 19` | Mengendalikan sudut rotasi |
| **Traffic Light Module** | LED Red (Merah) | `GPIO 25` | Indikator jarak bahaya |
| | LED Yellow (Kuning)| `GPIO 26` | Indikator jarak waspada |
| | LED Green (Hijau) | `GPIO 27` | Indikator jarak aman |
| **Active Buzzer** | Positif (+) | `GPIO 23` | Alarm suara peringatan |

> **Catatan Daya**: Pastikan pin VCC Servo dan Buzzer dihubungkan ke pin `VIN` atau `5V` pada ESP32 (atau *external power supply* jika servo tersendat) karena pin `3V3` tidak kuat memasok arus yang cukup.

---

## 💻 Kebutuhan Perangkat Lunak (Software)

Sebelum melakukan *compile* program di Arduino IDE, pastikan beberapa pustaka (*library*) berikut sudah terinstal melalui **Library Manager** (`Ctrl + Shift + I`):
1. **ESP32Servo** (oleh Kevin Harrington) – Untuk kendali motor servo pada arsitektur ESP32.
2. **WebServer** (Bawaan core ESP32) – Untuk menangani request HTTP dari web dashboard.
3. **WiFi** (Bawaan core ESP32) – Untuk menghubungkan ESP32 ke jaringan lokal.

---

## 📝 Cara Instalasi & Penggunaan

### 1. Sisi Perangkat Keras (Hardware)
1. Rangkai seluruh komponen sesuai dengan tabel **Pinout** di atas.
2. Rekatkan sensor ultrasonik di atas *horn* (baling-baling) motor servo menggunakan perekat atau lem agar ikut berputar saat servo bergerak.

### 2. Sisi Firmware (ESP32)
1. Buka file `.ino` proyek ini di Arduino IDE.
2. Cari baris berikut dan sesuaikan dengan Wi-Fi di tempatmu:
   ```cpp
   const char* ssid     = "NAMA_WIFI_KAMU";
   const char* password = "PASSWORD_WIFI_KAMU";
