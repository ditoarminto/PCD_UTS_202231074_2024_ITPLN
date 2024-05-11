
# LAPORAN UTS PENGCID DITO IMANUEL ARMINTO

Sebuah projek yang dibuat untuk memenuhi tugas UTS praktikum yang diberikan kepada mahasiswa matakuliah Pengolahan Citra. Terdapat proses-proses seperti deteksi warna, pengaturan kontras, pengaturan kecerahan, dan juga manipulasi gambar RGB agar dapat menampilkan gambar dengan warna yang diinginkan seperti gambar hasil saluran Red, gambar hasil saluran green, maupun gambar hasil saluran blue.

## 1) Deteksi Warna Pada Citra

Dalam manipulasi gambar tentu setiap gambar atau setiap foto maupun dengan objek yang sama bila difoto akan menghasilkan kualitas maupun ketajaman warna maupun cahaya yang berbeda oleh sebab itu dalam proses no 1 ini cukup sulit sebab perlu mendapatkan foto yang memiliki pencahayaan yang merata serta menampilkan tingkat warna yang sesuai dengan aslinya, bila ada sedikit perbedaan warna dapat mempengaruhi hasil otuputnya ini tentu mempengaruhi hasil dari projek ini.


## Import dan konversi grayscale serta RGB to BGR
```python
import cv2
import numpy as np
from matplotlib import pyplot as plt
img = cv2.imread("dk.jpg")
rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
plt.imshow(rgb)
```

Pada bagian ini kita akan melakukan pengimportan terhadap beberapa library seperti openCV (cv2) lalu numpy kemudian matplotlib yaitu pyplot sebagai plt. Library-library ini lah yang akan kita gunakan dalam manipulasi gambar teks RGB kita. lalu terdapat bagian `cv2.imread("dk.jpg")` merupakan bagian untuk membaca file gambar yang ditampung pada variabel img yang nantinya akan dipanggil di bagian rgb untuk mengubah atau mengkonversi format file gambar kita dari RGB ke BRG yang mana merupakan format gambar yang dapat terbaca oleh library openCV.


## Konversi ke grayscale
```python
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
```
Pada bagian ini kita akan mengubah gambar kita ke grayscale untuk nantinya dapat kita gunakan selanjutnya.

## Pengatur kontras dan kecerahan
```python
alpha = 1.72 # kontras 
beta = 15 # kecerahan
adjusted = cv2.convertScaleAbs(img, alpha=alpha, beta=beta)
````

Pada bagian ini variabel alpha digunakan untuk mengatur kontras, sementara beta digunakan untuk mengatur kecerahan. Nilai-nilai ini akan digunakan dalam fungsi `cv2.convertScaleAbs()`. Lalu pada bagian terakhir `adjusted = cv2.convertScaleAbs(img, alpha=alpha, beta=beta)` baris ini menyesuaikan kontras dan kecerahan gambar menggunakan fungsi `cv2.convertScaleAbs()` dari OpenCV. Fungsi ini mengambil gambar asli (img) dan menerapkan penyesuaian kecerahan dan kontras lalu diaplikasikan ke gambar kita

## Menampilkan hasil
```python
plt.figure(figsize=(10, 5))
```
- Membuat bingkai dengan ukuran 10 x 5 inci.
```python
plt.subplot(1, 2, 1)
```
- Membuat subplot dengan 1 baris, 2 kolom, dan No-nya.
```python
plt.title('Gambar Asli')
```
- Membuat title untuk gambar pertama.
```python
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB)) 
```
- Menampilkan gambar hasil penyesuaian.
```python
plt.axis('off')
```
- Menghilangkan sumbu x dan y dari plot pertama.
```python
plt.subplot(1, 2, 2)
plt.title('Gambar hasil penerangan')
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB))
plt.axis('off')
```
- Untuk blok program diatas sama dengan sebelumnya.
```python
plt.show()
```
- Menampilkan plot dengan kedua subplot yang telah ditetapkan.

## Menampilkan Saluran dan Histogramnya
```python
merah=cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,0] #Merah
fig, axs = plt.subplots(1,2, figsize = (15,5))
hist = cv2.calcHist([merah],[0],None,[256],[0,256])
axs[0].imshow(merah, cmap='gray')
axs[1].plot(hist)
plt.show()
```
* `merah=cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,0] #Merah`: Baris ini mengambil saluran merah dari gambar yang telah disesuaikan dan diubah ke format RGB. Caranya dengan memilih semua baris dan kolom dari saluran merah index 0. Hasilnya adalah array NumPy akan berisi intensitas piksel merah dari gambar.
* `fig, axs = plt.subplots(1,2, figsize = (15,5))`: Pada baris ini kita membuat subplot dengan 1 baris dan 2 kolom, sehingga ada dua subplot secara keseluruhan. Ukuran plotnya ditentukan menjadi 15x5 inci. Variabel fig digunakan untuk mengakses figur dan axs digunakan untuk mengakses subplot.
* `hist = cv2.calcHist([merah],[0],None,[256],[0,256])`: Perintah itu menghitung histogram untuk saluran merah menggunakan `cv2.calcHist()`. Fungsi ini mengambil satu saluran warna, yaitu saluran merah, dan menghitung distribusi frekuensi intensitas piksel pada saluran tersebut. Parameter [0] menunjukkan kita menghitung histogram untuk saluran pertama (saluran merah). [256] menunjukkan jumlah bin histogram, dan [0,256] menunjukkan rentang nilai intensitas piksel yang akan dihitung 0 hingga 256.
`axs[0].imshow(merah, cmap='gray')`: Ini menampilkan gambar saluran merah di subplot pertama menggunakan `imshow()`. Karena kita hanya memiliki satu saluran warna (grayscale), colormap 'gray' digunakan.
`axs[1].plot(hist)`: Ini menampilkan histogram yang dihitung di subplot kedua menggunakan plot(). Ini akan menampilkan grafik dari nilai-nilai histogram yang dihitung sebelumnya.
* `plt.show()`: Ini menampilkan plot keseluruhan, yang berisi gambar saluran merah dan histogramnya.
```python
hijau=cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,1] #hijau
fig, axs = plt.subplots(1,2, figsize = (15,5))
hist = cv2.calcHist([hijau],[0],None,[256],[0,256])
axs[0].imshow(hijau, cmap='gray')
axs[1].plot(hist)
plt.show()
```
```python
biru=cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,2] #biru
fig, axs = plt.subplots(1,2, figsize = (15,5))
hist = cv2.calcHist([biru],[0],None,[256],[0,256])
axs[0].imshow(biru, cmap='gray')
axs[1].plot(hist)
plt.show()
```
- Hal yang sama berlaku untuk kedua program ini kita hanya akan memfokuskan pada seleksi warna biru dan hijau. kemudian hasil akan di ubah ke bentuk grayscale dengan cmap = 'gray' lalu grafik histogram akan ditampilkan.

## Menampilkan keempat gambar pada 4 plot
```python
plt.subplot(2, 2, 1)
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB))
plt.title('Gambar Asli')
```
* `plt.subplot(2, 2, 1)`: Baris ini menetapkan subplot dengan 2 baris, 2 kolom, dan nomor subplot 1. Ini berarti kita akan memiliki empat subplot secara keseluruhan, dan subplot ini adalah yang pertama dari keempatnya.
* `plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB))`: Ini menampilkan gambar yang telah disesuaikan dalam format RGB. Sebelum menampilkan gambar, gambar tersebut diubah dari format BGR ke RGB menggunakan cv2.cvtColor(). Fungsi plt.imshow() dari Matplotlib kemudian digunakan untuk menampilkan gambar tersebut di subplot yang telah ditetapkan.
* `plt.title('Gambar Asli')`: Baris ini menambahkan judul untuk gambar yang ditampilkan. Judul ini akan muncul di atas gambar dalam plot.
#Menampilkan saluran merah
```python
plt.subplot(2, 2, 2)
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,0], cmap="gray")
plt.title('Saluran Merah')
```
#Menampilkan saluran hijau
```python
plt.subplot(2, 2, 3)
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,1], cmap="gray")
plt.title('Saluran Hijau')
```
#Menampilkan saluran biru
```python
plt.subplot(2, 2, 4)
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,2], cmap="gray")
plt.title('Saluran Biru')
plt.show()
```
- Hasil dari manipulasi data tersebut ditampilkan pada 4 plot. menggunakan fungsi plt.imshow() dan plt.title() untuk Judul salurannya.


## 2) Urutan Ambang Batas Terkecil Sampai Terbesar
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
* Mengimport beberapa library cv2, numpy, dan matplotlib tiap tiap modul punya fungsi dan kegunaan tersendiri pada program. cv2 atau OpenCV digunakan untuk membaca, menuis, dan memanipulasi gambar dan video. NumPy digunakan bersamaan dengan openCV untuk manipulasi array dan matriks, serta melakukan operasi matematika dan statistik. Lalu matplotlib digunakan untuk membuat plot, grafik, dan visualisasi lainnya.
## Baca gambar
```python
img = cv2.imread('dk.jpg')
```
* Perintah tersebut menggunakan fungsi `cv2.imread()` dari OpenCV untuk membaca gambar yang disimpan dengan nama "dk.jpg", dikembalikan dalam bentuk array NumPy.
## Convert citra ke grayscale
```python
gray = cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)
```
* Parameter `cv2.COLOR_RGB2GRAY` berfungsi untuk konversi citra ke gray, dengan fungsi `cv2.cvtColor()` lalu ditampung ke gray.
## Inisialisasi subplot
```python
fig, axs = plt.subplots(2, 2, figsize=(10,10))
```
* Pada perintah diatas, kita menciptakan sebuah grid atau bingkai subplot dengan 2 baris dan 2 kolom menggunakan `plt.subplots()`, lalu ukuran plot disesuaikan dengan parameter `figsize=(10,10)`.
## Ambang batas untuk mendapatkan citra biner (none)
```python
(thresh, binary1) = cv2.threshold(gray, 0, 255, cv2.THRESH_BINARY)
axs[0,0].imshow(binary1, cmap = 'gray')
axs[0,0].set_title('NONE')
```
* Perintah diatas melakukan proses thresholding pada gambar dalam skala abu-abu (gray) menggunakan fungsi `cv2.threshold()` dari modul OpenCV. Thresholding digunakan untuk mengonversi gambar ke dalam gambar biner, di mana setiap piksel akan diberi nilai 0 (hitam) atau 255 (putih) berdasarkan nilai ambang tertentu.
## Convert citra ke HSV
```python
image_hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
```
* Baris kode ini menggunakan fungsi `cv2.cvtColor()` dari modul OpenCV untuk mengonversi gambar yang telah dibaca sebelumnya (img) dari format warna BGR (Blue-Green-Red) menjadi format warna HSV (Hue-Saturation-Value).
## Definisikan range warna biru dalam HSV
```python
blue_lower = np.array([100, 50, 50])
blue_upper = np.array([140, 255, 255])
```
* blue_lower adalah array NumPy yang menyimpan nilai minimum untuk setiap komponen warna dalam format HSV. Nilai-nilai ini menentukan batas bawah untuk deteksi warna biru.

* blue_upper adalah array NumPy yang menyimpan nilai maksimum untuk setiap komponen warna dalam format HSV. Nilai-nilai ini menentukan batas atas untuk deteksi warna biru.

## Membuat mask untuk warna biru
```python
mask_blue = cv2.inRange(image_hsv, blue_lower, blue_upper)
axs[0,1].imshow(mask_blue, cmap='gray')
axs[0,1].set_title('BLUE')
```
* `cv2.inRange(image_hsv, blue_lower, blue_upper)` Merupakan perintah untuk mengambil gambar dalam format HSV (image_hsv) dan dua array NumPy yang mewakili batas bawah (blue_lower) dan batas atas (blue_upper) untuk warna biru. Fungsi ini menghasilkan sebuah mask biner di mana piksel yang masuk dalam rentang warna biru akan diatur menjadi 255 (putih), sedangkan piksel yang tidak masuk dalam rentang tersebut akan diatur menjadi 0 (hitam).

## Ambang batas untuk mendapatkan citra biner (red-blue)
```python
(thresh, binary3) = cv2.threshold(gray, 65, 255, cv2.THRESH_BINARY)
axs[1,0].imshow(binary3, cmap = 'binary')
axs[1,0].set_title('RED-BLUE')
```
* `cv2.threshold(gray, 65, 255, cv2.THRESH_BINARY)` mengambil gambar dalam skala abu-abu (gray) sebagai input. Lalu membagi piksel menjadi dua kelas berdasarkan nilai ambang yang telah ditentukan yaitu 65. Jika nilai piksel di atas nilai ambang, maka piksel tersebut akan diatur menjadi 255 (putih), jika tidak, maka akan diatur menjadi 0 (hitam).
## Ambang batas untuk mendapatkan citra biner (red-green-blue)
```python
(thresh, binary4) = cv2.threshold(gray, 105, 255, cv2.THRESH_BINARY)
axs[1,1].imshow(binary4, cmap = 'binary')
axs[1,1].set_title('RED-GREEN-BLUE')

plt.show()
```
* Hal yang sama berlaku untuk perintah ini, yang membedakan hanya nilai ambang batas yaitu 105, lalu diberi judul "RED-GREEN-BLUE".