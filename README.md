# Klasifikasi Kualitas Wine Merah Menggunakan Random Forest

## 1. Deskripsi Proyek

Proyek ini bertujuan untuk memprediksi kualitas wine merah berdasarkan karakteristik kimia yang terkandung di dalamnya menggunakan algoritma **Random Forest Classifier**.

Model dilatih menggunakan data hasil pengukuran kimia wine dan skor kualitas yang diberikan oleh penilai. Dengan pendekatan machine learning, proyek ini berusaha mengetahui apakah karakteristik kimia dapat digunakan untuk memperkirakan skor kualitas wine.

## 2. Tujuan

- Menganalisis hubungan antara karakteristik kimia dan kualitas wine merah.
- Membersihkan data sebelum digunakan dalam pemodelan.
- Mengidentifikasi fitur yang memiliki hubungan kuat dengan skor kualitas.
- Membangun model klasifikasi menggunakan Random Forest.
- Membandingkan model biasa dengan model yang menyeimbangkan kelas.
- Mengevaluasi performa model dalam memprediksi kualitas wine.

## 3. Dataset

Dataset yang digunakan adalah **Wine Quality – Red Wine**, dengan nama file `winequality-red.csv`.

Dataset berisi 1.599 baris data awal yang menggambarkan sampel wine merah. Setiap sampel memiliki 11 fitur kimia dan satu kolom target berupa skor kualitas.

### Sumber data

Dataset Wine Quality dari UCI Machine Learning Repository.

Referensi: https://archive.ics.uci.edu/dataset/186/wine+quality

### Fitur dataset

| Fitur | Keterangan |
|---|---|
| fixed acidity | Kadar asam tetap |
| volatile acidity | Kadar asam mudah menguap |
| citric acid | Kadar asam sitrat |
| residual sugar | Kadar gula tersisa |
| chlorides | Kadar garam |
| free sulfur dioxide | Kadar sulfur dioksida bebas |
| total sulfur dioxide | Kadar sulfur dioksida total |
| density | Kepadatan wine |
| pH | Tingkat keasaman |
| sulphates | Kadar sulfat |
| alcohol | Kadar alkohol |
| quality | Skor kualitas wine sebagai target |

## 4. Dasar Pencarian dan Pemilihan Data

Data dipilih berdasarkan **karakteristik kimia wine merah dan skor kualitasnya**, bukan berdasarkan nama merek, harga, atau jenis produsen.

Dataset digunakan karena setiap sampel memiliki nilai pengukuran kimia serta label kualitas yang dapat dipelajari oleh model.

Kriteria data yang digunakan:
- Jenis produk: wine merah.
- Karakteristik: hasil pengukuran kimia dalam bentuk numerik.
- Target prediksi: skor kualitas wine, dengan rentang skor 3–8 pada dataset ini.
- Sumber: dataset Wine Quality.
- Format file: CSV.

Dengan demikian, model mempelajari pola hubungan antara kandungan kimia wine dan skor kualitas yang diberikan penilai.

## 5. Tahapan Pengolahan Data

### a. Memuat data
Dataset CSV dimuat ke dalam Python menggunakan Pandas.

### b. Eksplorasi data
Pemeriksaan dilakukan untuk mengetahui:
- Jumlah baris dan kolom.
- Nama dan tipe data setiap kolom.
- Jumlah data kosong.
- Jumlah baris duplikat.
- Distribusi skor kualitas.

### c. Pembersihan data
Baris duplikat dihapus agar sampel yang sama tidak muncul berulang kali dalam proses pembelajaran dan evaluasi.

### d. Seleksi fitur
Hubungan setiap fitur dengan skor kualitas diperiksa menggunakan korelasi absolut. Fitur dengan nilai korelasi di bawah 0,1 dihapus berdasarkan aturan yang diterapkan dalam notebook.

Tiga fitur yang dihapus adalah:
- `residual sugar`
- `free sulfur dioxide`
- `pH`

### e. Penentuan fitur dan target
- **Fitur (X):** delapan karakteristik kimia yang tersisa setelah seleksi fitur.
- **Target (y):** kolom `quality`.

## 6. Metode yang Digunakan

Algoritma yang digunakan adalah **Random Forest Classifier**, yaitu metode klasifikasi yang menggabungkan prediksi dari banyak pohon keputusan.

Dua konfigurasi model dibandingkan:

1. **Model biasa:** menggunakan pengaturan standar Random Forest.
2. **Model seimbang:** menggunakan `class_weight="balanced"` untuk memberikan bobot lebih besar pada kelas yang jumlah sampelnya lebih sedikit.

Kedua model menggunakan 300 pohon keputusan dan `random_state=42`.

## 7. Evaluasi Model

Evaluasi menggunakan metode **Stratified 5-Fold Cross-Validation**. Data dibagi menjadi lima bagian, sehingga setiap bagian bergantian digunakan sebagai data pengujian, sementara bagian lainnya digunakan untuk pelatihan.

Metrik evaluasi yang digunakan:

- **Accuracy:** persentase prediksi yang tepat dari seluruh sampel.
- **Balanced Accuracy:** rata-rata kemampuan model mengenali setiap kelas kualitas.
- **Recall per kelas:** persentase sampel pada suatu skor yang berhasil dikenali oleh model.
- **Confusion Matrix:** menunjukkan skor sebenarnya dibandingkan dengan skor hasil prediksi.
- **Permutation Importance:** mengukur kontribusi fitur terhadap performa prediksi dengan mengacak nilai fitur tersebut.

## 8. Hasil dan Temuan

Berdasarkan penjelasan dalam notebook:

- Kadar alkohol merupakan salah satu fitur yang paling berpengaruh terhadap prediksi kualitas wine.
- Sulfat dan asam mudah menguap juga berperan penting.
- Model biasa lebih unggul dalam accuracy keseluruhan.
- Model seimbang lebih baik dalam mengenali beberapa kelas yang jumlah sampelnya lebih sedikit, termasuk wine dengan skor 7.
- Skor kualitas yang jarang muncul, seperti 3, 4, dan 8, lebih sulit diprediksi karena jumlah sampelnya terbatas.
- Penghapusan fitur yang korelasinya lemah tidak banyak mengurangi performa prediksi dalam pengujian tambahan notebook.

Angka performa akhir sebaiknya diambil dari hasil eksekusi notebook agar nilai accuracy dan balanced accuracy yang dilaporkan sesuai dengan hasil aktual.

## 9. Teknologi dan Library

Proyek ini menggunakan:
- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Google Colab

## 10. Cara Menjalankan Proyek

1. Buka notebook Google Colab.
2. Siapkan file `winequality-red.csv`.
3. Jalankan sel kode dari bagian paling atas secara berurutan.
4. Unggah file CSV ketika diminta.
5. Tunggu hingga seluruh proses eksplorasi, pembersihan, pelatihan, dan evaluasi selesai.
6. Periksa grafik serta metrik hasil prediksi untuk memahami performa model.

## 11. Kesimpulan

Proyek ini menunjukkan bahwa karakteristik kimia dapat digunakan untuk memprediksi skor kualitas wine merah menggunakan Random Forest Classifier. Kadar alkohol, sulfat, dan asam mudah menguap menjadi fitur penting dalam proses prediksi.

Namun, performa model masih dipengaruhi oleh ketidakseimbangan jumlah sampel pada setiap skor kualitas. Penambahan data pada kelas yang jarang muncul atau pengelompokan skor kualitas menjadi beberapa kategori dapat menjadi pengembangan selanjutnya.

---

**Catatan:** Model memprediksi skor kualitas berdasarkan pola yang ditemukan dalam dataset, bukan menentukan kualitas wine secara mutlak atau menggantikan penilaian ahli.
