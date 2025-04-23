# Deep-Learning_Autoencoder

# Analisis Autoencoder untuk Pewarnaan Citra

# Dataset
Dataset terdiri dari:
- Direktori gambar berwarna: /content/drive/MyDrive/Record algo pr/train/color
- Direktori gambar grayscale: /content/drive/MyDrive/Record algo pr/train/grayscale

Proses loading dataset:
- Gambar diubah ke format RGB dan diresize menjadi 256x256 piksel
- Dilakukan normalisasi nilai piksel ke range [0,1]
- Gambar berwarna diubah ke grayscale sebagai input model
- Data dibagi menjadi train (90%) dan test (10%)

# Arsitektur Autoencoder
Model yang digunakan adalah autoencoder konvensional dengan arsitektur:

Encoder:
- Layer Conv2D 64 filter (3x3) + ReLU activation
- MaxPooling2D (2x2)
- Layer Conv2D 128 filter (3x3) + ReLU activation
- MaxPooling2D (2x2)
- 
Decoder:
- Layer Conv2D 128 filter (3x3) + ReLU activation
- UpSampling2D (2x2)
- Layer Conv2D 64 filter (3x3) + ReLU activation
- UpSampling2D (2x2)
- Layer Conv2D 3 filter (3x3) + sigmoid activation (output RGB)

Model dikompilasi dengan:
- Optimizer: Adam
- Loss function: Mean Squared Error (MSE)

# Masalah yang Terjadi
Pada saat training muncul error:
ValueError: Invalid input shape for input Tensor("data:0", shape=(16,), dtype=float32). 
Expected shape (None, 256, 256, 1), but input has incompatible shape (16,)

Ini menunjukkan ada ketidaksesuaian bentuk input antara:
- Yang diharapkan model: (batch_size, 256, 256, 1)
- Yang diberikan: (16,) - kemungkinan karena masalah dalam fungsi load_images()

# Contoh Hasil yang Diharapkan
Jika model berhasil dilatih, fungsi show_results() akan menampilkan:
- Baris pertama: Gambar input grayscale
- Baris kedua: Hasil pewarnaan dari model
- Baris ketiga: Gambar asli berwarna (ground truth)

Dengan arsitektur ini, performa yang diharapkan:
- Loss awal mungkin cukup tinggi karena tugas pewarnaan yang kompleks
- Loss akan menurun seiring training menunjukkan model belajar memetakan grayscale ke warna
- Hasil visual mungkin masih buram/tidak sejelas gambar asli karena keterbatasan arsitektur sederhana


