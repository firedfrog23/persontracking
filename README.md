# Person Tracking System

## Business Understanding
Dalam lingkungan perkotaan yang semakin kompleks, keamanan dan efisiensi dalam pemantauan publik menjadi prioritas utama. Sistem pemantauan konvensional yang hanya mengandalkan kamera CCTV memiliki keterbatasan, terutama dalam hal identifikasi dan pelacakan individu secara real-time.

Dengan menggunakan teknologi Object Tracking, sistem ini dapat secara otomatis mendeteksi dan melacak pergerakan orang di area tertentu, membantu otoritas dalam mengawasi aktivitas publik, mengurangi tindak kriminal, serta meningkatkan respons terhadap kejadian darurat. 

Dengan penerapan algoritma seperti Faster R-CNN atau YOLO, sistem dapat mendeteksi objek dengan akurasi tinggi, lalu melacaknya melalui serangkaian frame video. Hal ini memungkinkan integrasi dengan infrastruktur smart city, seperti sistem keamanan otomatis, pengaturan lalu lintas berbasis AI, atau manajemen keramaian dalam acara besar.

Dari sisi bisnis, proyek ini membawa berbagai manfaat bagi sektor pemerintahan maupun swasta yang bergerak di bidang keamanan dan analisis data. Implementasi Object Tracking dapat mengurangi ketergantungan pada pengawasan manual, sehingga meningkatkan efisiensi operasional sekaligus mengurangi biaya tenaga kerja.

## Tools
Dalam proyek ini, beberapa tools digunakan untuk membantu dalam pemrosesan data dan pengembangan model:
- **NumPy**: Manipulasi dan pemrosesan data numerik dalam gambar.
- **Matplotlib & Seaborn**: Visualisasi gambar dan hasil pemrosesan citra.
- **Pandas**: Mengelola metadata dan informasi terkait gambar dalam bentuk tabel.
- **OpenCV**: Pre-processing, ekstraksi fitur, dan penerapan algoritma machine learning pada gambar.
- **PyTorch**: Membangun dan melatih model deep learning untuk pengolahan citra.

## Model
Model yang digunakan dalam proyek ini adalah YOLO (You Only Look Once), khususnya YOLOv8 untuk deteksi dan pelacakan objek. Model ini bekerja dengan cara berikut:
1. **Deteksi Objek**: Model mendeteksi objek dalam suatu frame video dan menghasilkan bounding box.
2. **Pelacakan Objek**: Bounding box dari frame sebelumnya digunakan untuk menghubungkan objek pada frame berikutnya.
3. **Optimasi Model**: Melakukan tuning parameter untuk meningkatkan akurasi dan efisiensi model.

## Inisialisasi Model
Model diinisialisasi dengan menggunakan YOLOv8 pre-trained model:
```python
model = YOLO("yolov8n.pt")  # Memuat model YOLOv8
results = model.predict(img, conf=0.5)  # Mendeteksi objek dengan confidence 50% ke atas
```
Hasil prediksi akan berupa bounding box, confidence score, dan class label.

## Training Model
Pelatihan model dilakukan dengan langkah-langkah berikut:
1. Menggunakan dataset **COCO128**.
2. Training dilakukan selama **5 epochs** dengan ukuran gambar **640x640**.
3. Hyperparameter tuning dilakukan dengan kombinasi berikut:
   - **Learning rate**: 1e-3, 1e-4
   - **Momentum**: 0.8, 0.9
   - **Batch size**: 8, 16
4. Model dilatih menggunakan PyTorch:
```python
model.train(data="coco128.yaml", epochs=5, imgsz=640, lr0=1e-3, momentum=0.9, batch=16)
```

## Kesimpulan
Setelah melakukan training dan evaluasi, beberapa kesimpulan diperoleh:
- **Waktu training**: Dengan hanya 5 epochs, hasil mAP masih bisa ditingkatkan.
- **Pemilihan model**: YOLOv8n adalah model yang ringan, namun performa bisa lebih baik jika menggunakan YOLOv8m atau YOLOv8l.
- **Dataset**: Menggunakan full COCO dataset atau dataset yang lebih besar bisa meningkatkan akurasi.
- **Optimasi lebih lanjut**:
  - Menambah jumlah epochs menjadi 50–100.
  - Mencoba model yang lebih kompleks.
  - Melakukan data augmentation seperti rotasi, scaling, dan flipping.
  - Menggunakan metode tuning yang lebih canggih seperti Bayesian Optimization.

Dengan peningkatan yang tepat, sistem Person Tracking ini dapat menjadi solusi handal untuk kebutuhan keamanan dan pemantauan di lingkungan smart city.
