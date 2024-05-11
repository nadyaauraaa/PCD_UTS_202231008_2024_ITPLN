# PCD_UTS_202231008_2024_ITPLN

1. Mengimport Library
```python
import cv2
import numpy as np
from matplotlib import pyplot as plt
```

Kode di atas adalah sebuah contoh penggunaan OpenCV (cv2) dan NumPy untuk pemrosesan gambar, serta matplotlib untuk menampilkan gambar

import cv2: Ini mengimpor modul OpenCV, yang merupakan perpustakaan populer untuk pengolahan gambar dan video.

import numpy as np: Ini mengimpor NumPy, yang sering digunakan untuk operasi matematika dan array multidimensi. Biasanya diimpor sebagai np untuk mempersingkat penulisan kode.

from matplotlib import pyplot as plt: Ini mengimpor modul pyplot dari matplotlib, yang digunakan untuk membuat visualisasi grafis. Biasanya diimpor sebagai plt untuk mempersingkat penulisan kode.

2. Untuk Membaca Gambar
```python
img = cv2.imread("Raa.jpeg")
```

Kode img = cv2.imread("Raa.jpeg") membaca gambar dengan nama file "Raa.jpeg" menggunakan OpenCV (cv2) dan menyimpannya ke dalam variabel img.

Fungsi cv2.imread() adalah salah satu fungsi dasar dalam OpenCV yang digunakan untuk membaca gambar dari file. Argumen pertamanya adalah nama file gambar yang ingin dibaca. Setelah membaca gambar, gambar tersebut akan disimpan dalam bentuk array NumPy di variabel img.

3. Konvert BGR ke RGB
```python
rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
plt.imshow(rgb)
```

rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB): Pada langkah ini, gambar yang telah dibaca sebelumnya dalam format BGR (Blue, Green, Red) oleh OpenCV disalin ke variabel img. Kita menggunakan fungsi cv2.cvtColor() untuk mengubah format gambar dari BGR ke RGB. Ini diperlukan karena OpenCV membaca gambar dalam format BGR secara default, sedangkan matplotlib (yang digunakan untuk menampilkan gambar) membutuhkan gambar dalam format RGB untuk menampilkan dengan benar.

plt.imshow(rgb): Ini menggunakan matplotlib (plt) untuk menampilkan gambar yang sudah diubah formatnya (dalam variabel rgb). Fungsi plt.imshow() digunakan untuk menampilkan gambar dalam bentuk array NumPy. Dalam hal ini, rgb adalah gambar yang telah dikonversi ke format yang tepat untuk ditampilkan menggunakan matplotlib.

```python
(baris, kolom)= rgb.shape[:2]

beta = 30 #bias untuk kecerahan
citra_cerah = np.zeros((baris, kolom, 3)) #np zeros = mengubah semua elemen array menjadi 0
 
for x in range(baris) :
    for y in range(kolom) :
        gyx = rgb[x,y] + beta
        citra_cerah[x,y] = gyx
citra_cerah = citra_cerah.astype(np.uint8)
 
fig, axs = plt.subplots(2,2, figsize=(15,5))
axs[0,0].imshow(rgb)
axs[0,1].hist(img.ravel(),256,[0,256])
axs[1,0].imshow(citra_cerah)
axs[1,1].hist(citra_cerah.ravel(),256,[0,256])
plt.show()
```

baris, kolom = rgb.shape[:2]: Mendapatkan dimensi gambar (tinggi dan lebar) dari array gambar RGB yang telah diubah formatnya.

beta = 30: Ini adalah variabel yang digunakan sebagai bias untuk menambahkan kecerahan ke gambar.

citra_cerah = np.zeros((baris, kolom, 3)): Membuat array NumPy dengan dimensi yang sama dengan gambar asli, tapi diisi dengan nilai nol. Ini akan digunakan untuk menyimpan hasil gambar yang diterapkan peningkatan kecerahan.

Iterasi melalui setiap pixel gambar, menambahkan nilai beta ke setiap saluran warna (R, G, B) dari pixel tersebut, dan menyimpan hasilnya di citra_cerah.

citra_cerah = citra_cerah.astype(np.uint8): Mengonversi hasil peningkatan kecerahan ke tipe data yang sesuai untuk representasi gambar (uint8).

fig, axs = plt.subplots(2,2, figsize=(15,5)): Membuat subplot matplotlib dengan ukuran 2x2.

axs[0,0].imshow(rgb): Menampilkan gambar asli di subplot pertama (baris 0, kolom 0).

axs[0,1].hist(img.ravel(),256,[0,256]): Membuat histogram gambar asli di subplot kedua (baris 0, kolom 1).

axs[1,0].imshow(citra_cerah): Menampilkan gambar yang telah ditingkatkan kecerahannya di subplot ketiga (baris 1, kolom 0).

axs[1,1].hist(citra_cerah.ravel(),256,[0,256]): Membuat histogram dari gambar yang telah ditingkatkan kecerahannya di subplot keempat (baris 1, kolom 1).

plt.show(): Menampilkan semua subplot.

```python
# 2. Convert to Grayscale
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

# 3. Adjust Contrast and Brightness
alpha = 1.5  # kontras
beta = 30    # kecerahan
adjusted = cv2.convertScaleAbs(img, alpha=alpha, beta=beta)

# 4. Display Results
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1)
plt.title('Original Image')
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.axis('off')

plt.subplot(1, 2, 2)
plt.title('Brightened Image')
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB))
plt.axis('off')

plt.show()
```

gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY): Mengonversi gambar yang telah dibaca sebelumnya menjadi citra keabuan (grayscale) menggunakan fungsi cv2.cvtColor(). Citra keabuan hanya memiliki satu saluran warna yang mewakili tingkat kecerahan di setiap pixel, sehingga lebih efisien secara memori dan komputasi dibandingkan dengan citra berwarna.

alpha = 1.5 dan beta = 30: Variabel alpha dan beta digunakan untuk mengatur kontras dan kecerahan gambar. alpha digunakan untuk mengontrol kontras, sedangkan beta digunakan untuk mengontrol kecerahan. Nilai-nilai ini akan digunakan dalam fungsi cv2.convertScaleAbs().

adjusted = cv2.convertScaleAbs(img, alpha=alpha, beta=beta): Mengaplikasikan penyesuaian kontras dan kecerahan ke gambar menggunakan fungsi cv2.convertScaleAbs(). Fungsi ini mengalikan setiap piksel dalam gambar dengan alpha dan kemudian menambahkan beta.

Menampilkan hasil:

plt.figure(figsize=(10, 5)): Membuat sebuah gambar (figure) matplotlib dengan ukuran 10x5.

plt.subplot(1, 2, 1): Membuat subplot pertama dengan urutan 1, 2, 1 (1 baris, 2 kolom, urutan pertama). Ini akan menampilkan gambar asli.

plt.title('Original Image'): Menambahkan judul untuk subplot pertama.

plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB)): Menampilkan gambar asli yang telah dikonversi ke format RGB agar sesuai dengan matplotlib.

plt.axis('off'): Mematikan sumbu pada subplot pertama.

plt.subplot(1, 2, 2): Membuat subplot kedua dengan urutan 1, 2, 2 (1 baris, 2 kolom, urutan kedua). Ini akan menampilkan gambar yang telah disesuaikan kontras dan kecerahannya.

plt.title('Brightened Image'): Menambahkan judul untuk subplot kedua.

plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)): Menampilkan gambar yang telah disesuaikan kontras dan kecerahannya, yang telah dikonversi ke format RGB agar sesuai dengan matplotlib.

plt.axis('off'): Mematikan sumbu pada subplot kedua.

plt.show(): Menampilkan semua subplot yang telah dibuat.

3. Untuk deteksi RGB
```python
plt.subplot(2, 2, 1)
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB))
plt.title('Original Image')

# Display the red channel
plt.subplot(2, 2, 2)
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,0], cmap="gray")
plt.title('Red')

# Display the green channel
plt.subplot(2, 2, 3)
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,1], cmap="gray")
plt.title('Green')

# Display the blue channel
plt.subplot(2, 2, 4)
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,2], cmap="gray")
plt.title('Blue')

plt.show()
```

plt.subplot(2, 2, 1): Membuat subplot pertama dengan urutan 2, 2, 1 (2 baris, 2 kolom, urutan pertama). Ini akan menampilkan gambar asli yang telah disesuaikan kontras dan kecerahannya.

plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)): Menampilkan gambar asli yang telah disesuaikan kontras dan kecerahannya. Fungsi cv2.cvtColor() digunakan untuk mengonversi gambar ke format RGB agar sesuai dengan matplotlib.

plt.title('Original Image'): Menambahkan judul untuk subplot pertama, meskipun ini sebenarnya menampilkan gambar yang telah disesuaikan.

plt.subplot(2, 2, 2), plt.subplot(2, 2, 3), plt.subplot(2, 2, 4): Membuat tiga subplot tambahan untuk menampilkan saluran warna (merah, hijau, dan biru) dari gambar yang telah disesuaikan.

plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,0], cmap="gray"): Menampilkan saluran warna merah dari gambar yang telah disesuaikan. Indeks [:,:,0] digunakan untuk memilih saluran warna merah dari gambar dalam format RGB, dan cmap="gray" mengatur tampilan agar dalam skala abu-abu.

plt.title('Red'), plt.title('Green'), plt.title('Blue'): Menambahkan judul untuk masing-masing subplot untuk menunjukkan saluran warna yang ditampilkan.

plt.show(): Menampilkan semua subplot yang telah dibuat.

```python
merah=citra_cerah[:,:,0] #Merah
fig, axs = plt.subplots(1,2, figsize = (15,5))
hist = cv2.calcHist([merah],[0],None,[256],[0,256])
axs[0].imshow(merah, cmap='gray')
axs[1].plot(hist)
plt.show()
```

merah = citra_cerah[:,:,0]: Membuat variabel merah yang merupakan saluran warna merah dari gambar yang telah ditingkatkan kecerahannya (citra_cerah). Untuk gambar berwarna, saluran warna merah umumnya berada di indeks 0.

fig, axs = plt.subplots(1,2, figsize = (15,5)): Membuat sebuah gambar (figure) matplotlib dengan satu baris dan dua kolom, sehingga kita memiliki dua subplot.

hist = cv2.calcHist([merah],[0],None,[256],[0,256]): Menghitung histogram dari saluran warna merah (merah) menggunakan fungsi cv2.calcHist(). Argumen [merah] menunjukkan bahwa kita menghitung histogram untuk saluran warna merah saja. Argumen [0] menunjukkan dimensi (kanal) histogram, yang dalam hal ini adalah saluran warna merah. [256] menunjukkan jumlah bin histogram, dan [0,256] menunjukkan rentang nilai piksel yang akan dihitung histogramnya.

axs[0].imshow(merah, cmap='gray'): Menampilkan subplot pertama, yang berisi gambar saluran warna merah (merah) dalam skala abu-abu.

axs[1].plot(hist): Menampilkan subplot kedua, yang berisi plot dari histogram yang telah dihitung (hist).

plt.show(): Menampilkan kedua subplot yang telah dibuat.

```python
hijau=citra_cerah[:,:,1] #hijau
fig, axs = plt.subplots(1,2, figsize = (15,5))
hist = cv2.calcHist([hijau],[0],None,[256],[0,256])
axs[0].imshow(hijau, cmap='gray')
axs[1].plot(hist)
plt.show()
```

hijau = citra_cerah[:,:,1]: Membuat variabel hijau yang merupakan saluran warna hijau dari gambar yang telah ditingkatkan kecerahannya (citra_cerah). Untuk gambar berwarna, saluran warna hijau umumnya berada di indeks 1.

fig, axs = plt.subplots(1,2, figsize = (15,5)): Membuat sebuah gambar (figure) matplotlib dengan satu baris dan dua kolom, sehingga kita memiliki dua subplot.

hist = cv2.calcHist([hijau],[0],None,[256],[0,256]): Menghitung histogram dari saluran warna hijau (hijau) menggunakan fungsi cv2.calcHist(). Argumen [hijau] menunjukkan bahwa kita menghitung histogram untuk saluran warna hijau saja. Argumen [0] menunjukkan dimensi (kanal) histogram, yang dalam hal ini adalah saluran warna hijau. [256] menunjukkan jumlah bin histogram, dan [0,256] menunjukkan rentang nilai piksel yang akan dihitung histogramnya.

axs[0].imshow(hijau, cmap='gray'): Menampilkan subplot pertama, yang berisi gambar saluran warna hijau (hijau) dalam skala abu-abu.

axs[1].plot(hist): Menampilkan subplot kedua, yang berisi plot dari histogram yang telah dihitung (hist).

plt.show(): Menampilkan kedua subplot yang telah dibuat.

```python
biru=citra_cerah[:,:,2] #biru
fig, axs = plt.subplots(1,2, figsize = (15,5))
hist = cv2.calcHist([biru],[0],None,[256],[0,256])
axs[0].imshow(biru, cmap='gray')
axs[1].plot(hist)
plt.show()
```

biru = citra_cerah[:,:,2]: Membuat variabel biru yang merupakan saluran warna biru dari gambar yang telah ditingkatkan kecerahannya (citra_cerah). Untuk gambar berwarna, saluran warna biru umumnya berada di indeks 2.

fig, axs = plt.subplots(1,2, figsize = (15,5)): Membuat sebuah gambar (figure) matplotlib dengan satu baris dan dua kolom, sehingga kita memiliki dua subplot.

hist = cv2.calcHist([biru],[0],None,[256],[0,256]): Menghitung histogram dari saluran warna biru (biru) menggunakan fungsi cv2.calcHist(). Argumen [biru] menunjukkan bahwa kita menghitung histogram untuk saluran warna biru saja. Argumen [0] menunjukkan dimensi (kanal) histogram, yang dalam hal ini adalah saluran warna biru. [256] menunjukkan jumlah bin histogram, dan [0,256] menunjukkan rentang nilai piksel yang akan dihitung histogramnya.

axs[0].imshow(biru, cmap='gray'): Menampilkan subplot pertama, yang berisi gambar saluran warna biru (biru) dalam skala abu-abu.

axs[1].plot(hist): Menampilkan subplot kedua, yang berisi plot dari histogram yang telah dihitung (hist).

plt.show(): Menampilkan kedua subplot yang telah dibuat.

4. Ambang Batas
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Baca gambar
img = cv2.imread('Raa.jpeg')
# Convert citra ke grayscale
gray = cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)

# Inisialisasi subplot
fig, axs = plt.subplots(2, 2, figsize=(10,10))

# Ambang batas untuk mendapatkan citra biner (none)
(thresh, binary1) = cv2.threshold(gray, 0, 255, cv2.THRESH_BINARY)
axs[0,0].imshow(binary1, cmap = 'gray')
axs[0,0].set_title('NONE')

# Convert citra ke HSV
image_hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

# Definisikan range warna biru dalam HSV
blue_lower = np.array([100, 50, 50])
blue_upper = np.array([140, 255, 255])

# Membuat mask untuk warna biru
mask_blue = cv2.inRange(image_hsv, blue_lower, blue_upper)
axs[0,1].imshow(mask_blue, cmap='gray')
axs[0,1].set_title('BLUE')

# Ambang batas untuk mendapatkan citra biner (red-blue)
(thresh, binary3) = cv2.threshold(gray, 36, 255, cv2.THRESH_BINARY)
axs[1,0].imshow(binary3, cmap = 'binary')
axs[1,0].set_title('RED-BLUE')

# Ambang batas untuk mendapatkan citra biner (red-green-blue)
(thresh, binary4) = cv2.threshold(gray, 80, 255, cv2.THRESH_BINARY)
axs[1,1].imshow(binary4, cmap = 'binary')
axs[1,1].set_title('RED-GREEN-BLUE')

plt.show()
```

Kodingan di atas adalah contoh pemrosesan gambar menggunakan OpenCV dan matplotlib

Membaca gambar: Menggunakan cv2.imread() untuk membaca gambar dengan nama "Raa.jpeg" dan menyimpannya dalam variabel img.

Konversi ke Grayscale: Menggunakan cv2.cvtColor() untuk mengonversi gambar ke citra keabuan (grayscale) dan menyimpannya dalam variabel gray.

Inisialisasi Subplot: Menginisialisasi subplot matplotlib dengan ukuran 2x2 menggunakan plt.subplots(2, 2, figsize=(10,10)).

Ambang Batas (Thresholding) untuk Citra Biner:

Dalam subplot pertama (baris 0, kolom 0), menggunakan cv2.threshold() untuk mendapatkan citra biner tanpa filter, dan menampilkannya sebagai gambar grayscale biner.
Konversi ke Model Warna HSV dan Segmentasi Warna:

Menggunakan cv2.cvtColor() untuk mengonversi gambar ke model warna HSV.
Menentukan rentang warna biru dalam model warna HSV.
Membuat mask untuk mendapatkan hanya bagian gambar yang sesuai dengan rentang warna biru menggunakan cv2.inRange().
Menampilkan hasil mask sebagai gambar biner pada subplot kedua (baris 0, kolom 1).
Thresholding untuk Citra Biner (Red-Blue):

Menggunakan cv2.threshold() untuk mendapatkan citra biner dengan ambang batas tertentu untuk menyoroti warna merah dan biru pada subplot ketiga (baris 1, kolom 0).
Thresholding untuk Citra Biner (Red-Green-Blue):

Menggunakan cv2.threshold() untuk mendapatkan citra biner dengan ambang batas tertentu untuk menyoroti warna merah, hijau, dan biru pada subplot keempat (baris 1, kolom 1).
Menampilkan Gambar: Menggunakan plt.show() untuk menampilkan semua subplot.

