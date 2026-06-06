# UAS-SistemMikrokontroler #23552011300

📡 IoT Radar System (Arduino Uno & ESP32)
Proyek IoT Radar ini mendeteksi objek di sekitar dengan sudut 0° hingga 180° menggunakan sensor ultrasonik yang diputar oleh motor servo. Data deteksi diproses oleh Arduino Uno, lalu dikirimkan ke ESP32 untuk diunggah ke dashboard IoT agar bisa dipantau secara real-time dari mana saja.

🚀 Fitur Utama
- Pemindaian 180° Continuos: Servo bergerak menyapu area secara otomatis.
- Deteksi Jarak Akurat: Menggunakan sensor ultrasonik untuk mengukur jarak objek.
- Konektivitas IoT: ESP32 bertindak sebagai gateway Wi-Fi untuk mengirim data ke cloud (Blynk/Antares/ThingSpeak).
- Indikator Fisik: LED dan Buzzer sebagai alarm jika ada objek yang terlalu dekat (Sistem Keamanan).
