# jsCoRA-notation
Ide bahasa notasi skor musik berbasis JSON

# Dasar

## Elemen

Ada beberapa elemen yang ditandai sebagai nilai properti `tag`, dengan cara kerja berbeda:

- `seq`: Anak dimainkan secara berurutan.
- `poly`: Anak dimainkan secara paralel.
- `group`: Digunakan untuk memberikan konfigurasi yang sama ke berbagai elemen yang berbeda.

### Keterangan

- Setiap elemen bisa memiliki elemen anak (bisa lebih dari satu) dengan menjadikannya nilai dari properti `child`.
- Setiap elemen bisa diberikan pengidentifikasi dengan properti `id`.

### konfigurasi-Konfigurasi Elemen

Elemen bisa diberikan konfigurasi yang berlaku untuk semua anaknya, yang ditimpa dengan konfigurasi anak. konfigurasi ditulis sebagai properti-properti berikut:

- `et`: Menentukan nilai ET yang digunakan sebagai basis notasi nada. Nilai bawaan: `12`.
- `mode`: Berisi *array* nada-nada tangga nada dalam notasi nada ET. Ia berguna terutama untuk penotasian nada berbasis derajat (berbasis `i`). Nilai bawaan: `[0, 2, 4, 5, 7, 9, 11]`.
- `bpm`: Menentukan nilai BPM atau *beat* per menit. Nilai bawaan: `100`.
- `tonic`: Menentukan nilai hertz frekuensi nada 0 oktaf dasar. Nilai bawaan: `261.63`.
- `voice`: Menentukan `voice` yang digunakan.
- `radix`: Menentukan basis atau radiks bilangan, berguna jika menggunakan `n` dan tidak ingin menggunakan `o`.

## Properti-Properti `seq` dan `poly`

Ada beberapa properti khusus untuk `seq` dan `poly`:

- `loop`: Menentukan berapa kali elemen dimainkan.
- `notes`: Nilainya menjadi tempat objek-objek nada. Boleh lebih dari satu `notes` per `seq` atau `poly`, yang dimainkan paralel. `seq` dan `poly` yang telah memiliki `notes` tetap boleh memiliki `child`, dan sebaliknya.

## Notasi Nada

Nada dinotasikan sebagai objek yang menjadi nilai properti `notes`.

### Properti-Properti Objek Nada

- `t`: Menentukan waktu mulai dalam satuan *beat* relatif atas elemen yang mewadahinya. Jika sebuah objek `notes` tidak memiliki properti `t`, maka waktu bermulai setelah nada sebelumnya.
- `n`: Menentukan nilai nada langsung berdasarkan notasi nada ET.
- `i`: Menentukan nilai nada berdasarkan indeks `mode`.
- `d`: Menentukan durasi berdasarkan satuan *beat*.
- `r`: *rest*/hening, dengan nilai numeral menentukan durasi.
- `o`: Menentukan oktaf dari oktaf dasar, terutama jika nilai nada ditentukan `i`. Nilai bawaan: `0`.
- `v`: Menentukan volume dalam skala 0—1. Nilai bawaan: `1`.

## Objek Khusus

- Objek dengan `tag` bernilai `ref` dan memiliki properti `ref` bernilai `id` sebuah elemen: menjalankan peristiwa elemen tersebut. Properti `ref` menimpa properti elemen yang direferensikan.

## Kemungkinan Ekstensi

Keterangan sebelumnya hanyalah dasar-dasarnya. Bahasa ini bisa dikembangkan untuk mengakomodir berbagai fungsi. Berikut beberapa kemungkinan yang saya telah pikirkan:

- pengeditan sebagian nada dalam `ref`
- properti untuk transposisi `seq` dan `poly`
- bagaimana nada dimainkan dan ornamentasi
