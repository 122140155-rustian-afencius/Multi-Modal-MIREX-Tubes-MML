# 🎵 Multimodal Music Emotion Recognition (MER)

> **Tugas Besar Pembelajaran Mesin Multimodal (IF25-40410)**
> **Program Studi Teknik Informatika - Institut Teknologi Sumatera (ITERA)**

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-Deep%20Learning-red)](https://pytorch.org/)
[![Status](https://img.shields.io/badge/Status-Completed-success)]()

## 📖 Deskripsi Proyek

Proyek ini bertujuan untuk mengembangkan sistem **Music Emotion Recognition (MER)** yang mampu mengenali emosi dalam musik dengan pendekatan **Multimodal Machine Learning**. 

Berbeda dengan pendekatan tradisional yang hanya mengandalkan audio, proyek ini mengintegrasikan tiga modalitas sekaligus menggunakan teknik **Intermediate Fusion** dengan mekanisme **Triple Cross-Attention**:
1.  **Audio (Akustik):** Mel-Spectrogram & Raw Waveform.
2.  **Lirik (Teks):** Semantik dan konteks bahasa.
3.  **MIDI (Simbolik):** Piano Roll & Fitur Statistik.

Tujuan utama adalah mengatasi subjektivitas emosi musik dan meningkatkan akurasi klasifikasi pada dataset MIREX dengan menggabungkan kekuatan dari setiap modalitas.

---

## 👥 Anggota Kelompok

| NIM | Nama | Peran |
| :--- | :--- | :--- |
| **121140041** | G Bintang Andromeda | EDA + Documentation |
| **122140043** | Kenneth Austin Wijaya | MIDI Engineer + Documentation |
| **122140077** | Rahmat Aldi Nasda | Lyrics Modality Engineer + Model Researcher |
| **122140090** | Christopher Benaya Tampubolon | MIDI Engineer + Documentation |
| **122140122** | Alfajar | Audio Modality Engineer + Model Researcher |
| **122140155** | Rustian Afencius Marbun | Fusion & Training Engineer + Model Researcher |

---

## 🧠 Arsitektur & Metodologi

Sistem ini menggunakan arsitektur **Intermediate Fusion** di mana fitur dari setiap modalitas diekstraksi secara terpisah sebelum digabungkan melalui *Triple Cross-Attention*.

### Encoders (Feature Extractors)
* **Audio:** * *Baseline/Opt 1:* ResNet18 (VGGish-style) dengan input Log-Mel Spectrogram.
    * *Opt 2:* Wav2Vec 2.0 untuk representasi *raw waveform*.
* **Lirik:** * RoBERTa-base (dengan *frozen layers* pada tahap optimalisasi).
* **MIDI:** * EfficientNet-B2 (untuk visual Piano Roll).
    * Lightweight CNN + Statistik (pada tahap optimalisasi).

### Fusion Strategy
Menggunakan **Triple Cross-Attention** yang memungkinkan setiap modalitas untuk "memperhatikan" (attend) informasi relevan dari modalitas lain secara dinamis sebelum masuk ke *classifier*.

---

## 📊 Dataset

Dataset yang digunakan dikembangkan oleh **Panda et al. (2013)** berdasarkan taksonomi emosi MIREX. Data disaring untuk memiliki kelengkapan tiga modalitas (Audio, Lirik, MIDI), menghasilkan 193 sampel berkualitas tinggi yang terbagi dalam 5 klaster emosi:

1.  **Cluster 1:** Passionate, Rousing, Confident.
2.  **Cluster 2:** Rollicking, Cheerful, Fun.
3.  **Cluster 3:** Literate, Wistful, Bittersweet.
4.  **Cluster 4:** Humorous, Silly, Quirky.
5.  **Cluster 5:** Aggressive, Fiery, Tense.

---

## 🚀 Hasil Eksperimen

Kami melakukan tiga tahap eksperimen utama: Baseline, Optimalisasi 1 (Focal Loss + Frozen Layers), dan Optimalisasi 2 (Wav2Vec2).

| Eksperimen | Encoder Audio | Encoder Lirik | Encoder MIDI | Strategi Fusion | Akurasi Test |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Baseline** | ResNet18 | RoBERTa | EfficientNet-B2 | Triple Cross-Attn | 43.21% |
| **Optimalisasi 1** 🏆 | ResNet18 | RoBERTa (Frozen 8 Layer) | EfficientNet-B2 | Triple Cross-Attn | **60.49%** |
| **Optimalisasi 2** | Wav2Vec2 | RoBERTa | Lightweight CNN | Triple Cross-Attn | 47.83% |

**Temuan Kunci:**
* **Optimalisasi 1** memberikan hasil terbaik dengan peningkatan akurasi sebesar **17.28%** dari baseline.
* Penggunaan **Focal Loss** sangat membantu menangani *imbalanced class*.
* Membekukan layer awal pada RoBERTa membantu model melakukan generalisasi lebih baik dan mencegah *overfitting* pada dataset yang kecil.


## 📚 Referensi

Project ini merujuk pada beberapa literatur berikut:

1.  M. Kokkidou, "Music Definition and Music Education," GSME, 2022.
2.  Panda R., et al., "Multi-Modal Music Emotion Recognition: A New Dataset, Methodology and Comparative Analysis," CMMR'2013.
3.  R. Liyanarachchi, et al., "A Survey on Multimodal Music Emotion Recognition," arXiv, 2025.
4.  A. Bhattacharya & K. K.V, "A Multimodal Approach towards Emotion Recognition of Music Using Audio and Lyrical Content," 2018.
5.  Y. Liu, et al., "RoBERTa: A Robustly Optimized BERT Pretraining Approach," 2019.
6.  M. Tan & Q. V. Le, "EfficientNet: Rethinking Model Scaling for Convolutional Neural Networks," 2019.

---
*Dibuat untuk memenuhi Tugas Besar Mata Kuliah Pembelajaran Mesin Multimodal - 2025*