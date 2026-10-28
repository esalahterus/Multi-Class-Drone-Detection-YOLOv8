# Multi-Class Drone Detection with YOLOv8

Proyek computer vision untuk mendeteksi dan mengklasifikasikan beberapa jenis drone pada citra dengan kondisi lingkungan yang beragam, yaitu siang hari, malam hari, dan berkabut. Model dikembangkan menggunakan **YOLOv8n** dan dievaluasi untuk melihat kemampuannya menemukan objek drone sekaligus membedakan kelasnya.

## Gambaran Proyek

Deteksi drone merupakan tantangan ketika objek terlihat kecil, jauh, sebagian tertutup, atau berada dalam kondisi pencahayaan dan atmosfer yang berbeda. Proyek ini mengeksplorasi penggunaan object detection berbasis YOLOv8 untuk mengenali lima kelas drone dan mengevaluasi performanya pada data validasi serta data uji terpisah.

Dataset yang digunakan adalah [Multi-Class Drone Detection Dataset (YOLOv8-Ready)](https://www.kaggle.com/datasets/troykueh/multi-class-drone-detection-dataset-yolov8-ready).

## Kelas Deteksi

Model dilatih untuk mendeteksi lima kelas berikut:

- **Shahed-136**
- **Shahed-238**
- **MQ-9 Reaper**
- **DJI Mavic**
- **Mohajer-6**

## Metodologi

Proyek mencakup pemeriksaan struktur dan integritas dataset, eksplorasi distribusi kelas serta kondisi gambar, visualisasi anotasi ground truth, pelatihan model YOLOv8n, dan evaluasi performa. Evaluasi menggunakan metrik precision, recall, mAP@0.5, dan mAP@0.5:0.95, disertai confusion matrix, kurva Precision–Recall, kurva F1, kurva pelatihan, dan pemeriksaan prediksi pada gambar uji.

Model dilatih dengan ukuran input **960 × 960 piksel** hingga **60 epoch**. Bobot model disimpan dalam format PyTorch (`best.pt`) dan diekspor ke format ONNX (`best.onnx`).

## Hasil Evaluasi

Berdasarkan catatan evaluasi pada notebook, hasil pada **held-out test set** adalah sebagai berikut:

| Metrik | Hasil |
|---|---:|
| Precision | 0,901 |
| Recall | 0,538 |
| mAP@0.5 | 0,583 |
| mAP@0.5:0.95 | 0,459 |

Hasil menunjukkan precision relatif tinggi, tetapi recall masih lebih rendah. Artinya, prediksi yang dihasilkan cenderung tepat ketika model mendeteksi drone, tetapi masih ada sebagian objek drone yang tidak terdeteksi. Objek berukuran kecil, jarak pandang, sudut pengambilan gambar, serta variasi kondisi siang, malam, dan berkabut merupakan tantangan penting bagi model.

Per kelas, notebook melaporkan nilai mAP@0.5:0.95 tertinggi pada Shahed-238 (**61,5%**) dan Shahed-136 (**53,8%**). Nilai untuk MQ-9 Reaper adalah **43,5%**, DJI Mavic **39,1%**, dan Mohajer-6 **31,6%**.

## Artefak Proyek

- `multi-class-drone-detection-yolov8.ipynb` — notebook analisis, pelatihan, dan evaluasi.
- `models/best.pt` — bobot model hasil pelatihan dalam format PyTorch.
- `models/best.onnx` — model yang diekspor ke format ONNX.
- `results/` — visualisasi distribusi dataset, anotasi ground truth, kurva pelatihan, confusion matrix, kurva evaluasi, serta contoh hasil prediksi.

## Batasan

Performa model belum menunjukkan bahwa semua drone dapat terdeteksi secara konsisten, khususnya pada objek yang sangat kecil atau sulit terlihat. Hasil evaluasi ini berlaku pada dataset dan pengaturan eksperimen yang digunakan, sehingga tidak dapat dianggap sebagai jaminan performa pada semua kondisi nyata. Peningkatan recall dan evaluasi lebih rinci berdasarkan ukuran objek serta kondisi lingkungan menjadi arah pengembangan selanjutnya.
