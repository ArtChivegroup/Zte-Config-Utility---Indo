Panduan Lengkap untuk Menggunakan ZTE Config Utility
Pendahuluan
ZTE Config Utility adalah alat yang berguna untuk mendekode dan meng-encode file konfigurasi untuk perangkat ZTE. Alat ini memungkinkan Anda untuk mengonversi file konfigurasi dari format biner ke XML dan sebaliknya. Dalam panduan ini, Anda akan belajar cara mendekode file config.bin, mengeditnya jika perlu, dan meng-encode kembali menjadi config.bin.

Langkah 1: Persiapan dan Instalasi
Unduh Repositori

Pertama, unduh repositori ZTE Config Utility dari GitHub:

bash
Copy code
git clone https://github.com/mkst/zte-config-utility.git
cd zte-config-utility
Instal Dependensi

Instal dependensi Python yang diperlukan. Pastikan Anda memiliki Python 3.7 atau lebih tinggi:


Copy code
python3 -m pip install . --user
Langkah 2: Mendekode File Konfigurasi
Menyiapkan Koneksi dengan Perangkat
copy folder zcu ke C:\Users\Administrator\AppData\Local\Programs\Python\Python312\Lib\site-packages

Sebelum mendekode, Anda perlu mengetahui informasi berikut:

Serial Number: ZTEGD4B2BD50
MAC Address: E0A1CEF6056E
Dekode File config.bin

Gunakan perintah berikut untuk mendekode file config.bin menjadi config.xml. Pastikan untuk mengganti config.bin dengan nama file Anda:

bash
Copy code
python examples/auto.py --serial ZTEGD4B2BD50 --mac E0A1CEF6056E config.bin config.xml
Catatan: Jika Anda mendapatkan peringatan tentang endianness, Anda dapat mengabaikannya jika dekode berhasil.

Verifikasi File XML

Periksa file config.xml yang dihasilkan untuk memastikan bahwa struktur dan data sesuai dengan yang diharapkan. Anda bisa membuka file ini dengan editor teks seperti Notepad++ atau Visual Studio Code.

Langkah 3: Meng-Encode Kembali File Konfigurasi
Siapkan Kunci Enkripsi

Berdasarkan output dekode, kunci enkripsi yang digunakan adalah:

Key: 'D4B2BD506e05f6cea1e0'
IV: 'ZTE%FN$GponNJ025' (biasanya tidak perlu disertakan secara eksplisit saat encoding)
Encode File config.xml

Gunakan perintah berikut untuk meng-encode file config.xml menjadi config.NEW.bin. Pastikan untuk mengganti config.xml dengan nama file Anda dan config.NEW.bin dengan nama file output yang diinginkan:


python examples/encode.py config.xml config.NEW.bin --signature 'ZTEGD4B2BD50' --include-header --key 'D4B2BD506e05f6cea1e0'
Catatan: Opsi --key digunakan untuk memastikan bahwa file dienkripsi dengan kunci yang benar. --include-header digunakan jika header perlu disertakan.

Verifikasi File Baru

Setelah encoding, periksa file config.NEW.bin:

Verifikasi Ukuran dan Format: Periksa ukuran dan integritas file menggunakan alat seperti md5sum:


md5sum config.NEW.bin
Uji pada Perangkat: Ganti file konfigurasi lama dengan yang baru pada perangkat dan uji fungsinya.

Langkah 4: Penanganan Masalah
Peringatan Endianness: Jika Anda menerima peringatan tentang endianness, pastikan hasil akhir tidak terpengaruh. Jika ada masalah, sesuaikan pengaturan endianness jika diperlukan.

Masalah Kunci: Jika encoding tidak berhasil, pastikan kunci enkripsi yang digunakan benar. Gunakan parameter --key dengan kunci yang tepat.

Dukungan Tambahan: Jika Anda mengalami kesulitan, lihat dokumentasi ZTE Config Utility di GitHub atau cari bantuan dari komunitas atau pengembang terkait.

Kesimpulan
Panduan ini memberikan langkah-langkah untuk mendekode dan meng-encode file konfigurasi ZTE menggunakan ZTE Config Utility. Dengan mengikuti panduan ini, Anda dapat berhasil memodifikasi dan mengelola file konfigurasi perangkat ZTE.

Untuk informasi lebih lanjut dan pembaruan terbaru, kunjungi repositori GitHub resmi di zte-config-utility.

