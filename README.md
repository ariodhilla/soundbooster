Ini hanya untuk testing saja, bluetooth connection ke speaker 
Bluetooth tetap kepakai buat ngetes di rumah — itu gunanya sekarang. Buat permanen di motor, 
jalurnya memang ampli + speaker, dan v5.5 udah auto-fallback ke I2S kalau BT nggak konek.



Cara A — Arduino IDE (dari ZIP)

Extract ZIP-nya, buka votol_ble_dualcore/votol_ble_dualcore.ino
Board: ESP32 Dev Module, Port: /dev/cu.usbserial-0001
Tools → Partition Scheme → Minimal SPIFFS — cek lagi, suka ke-reset sendiri
Pastikan library ESP32-A2DP 1.8.12 udah ter-install (yang kemarin lo install manual dari ZIP GitHub pas v3-BT). Kalau compile error BluetoothA2DPSource.h: No such file, itu library-nya belum kepasang.
Klik Upload, tunggu sampai Hard resetting via RTS pin. Upload dari Arduino IDE nggak ngapus NVS, jadi pairing BT aman.

Cara B — merged .bin via esptool.js (lebih cepat, tanpa compile)

Buka https://espressif.github.io/esp-web-tools/ di Chrome, Connect ke ESP32
Jangan klik Erase — pairing speaker BT lo tersimpan di NVS, Erase bikin hilang. Erase cuma kalau board bootloop.
Pilih file votol_ble_dualcore_foxr_joni_soundonly_v5_5_merged.bin, flash di alamat 0x0
Tunggu sampai selesai, ESP32 restart sendiri



Habis install, ceknya gini — v5_5 ini soundonly, jadi nggak ada WiFi/dashboard, semua lewat Serial Monitor (115200):

Suara ON by default. Nyalain speaker BT lo, ESP32 auto-connect ke speaker yang udah ke-pair.
Kalau pairing hilang (habis Erase), ketik di Serial Monitor: BT:SCAN dulu, terus BT:PAIR <MAC speaker>.
Command lain: SOUND:ON / SOUND:OFF, VOICE buat ganti suara, STATUS buat liat status.


