## I. Daftar Model/Metode/Algoritma

### A. Analisis Sentimen (dan Emosi)

1. **Metode Klasik (Tanpa Pretrained Model)**  
   - **Algoritma:**  
     - Naive Bayes, SVM, Logistic Regression  
   - **Fitur:**  
     - TF-IDF, Bag-of-Words, serta skor leksikon (misalnya, lexicon-based sentiment scoring)  
   - **Kelebihan:**  
     - Cepat, mudah diimplementasikan, dan dapat dijadikan baseline  
   - **Kekurangan:**  
     - Sulit menangkap konteks kalimat yang kompleks  
   - **Catatan:**  
     - Dapat diterapkan secara terpisah untuk Sentimen (misal: Positif, Negatif, Netral) dan Emosi (misal: Senang, Sedih, Marah) jika tidak menggunakan multi-task learning.

2. **Deep Learning Sederhana**  
   - **Algoritma:**  
     - LSTM, BiLSTM, atau CNN  
   - **Fitur:**  
     - Menggunakan embedding seperti Word2Vec atau GloVe  
   - **Kelebihan:**  
     - Mampu menangkap urutan dan konteks kata dalam kalimat  
   - **Kekurangan:**  
     - Membutuhkan data latih lebih banyak dan komputasi lebih berat  
   - **Catatan:**  
     - Dengan 21 ribu data, model LSTM dapat dicoba untuk baseline deep learning.

3. **Model Transformer (Pretrained)**  
   - **Algoritma:**  
     - IndoBERT, mBERT, atau DistilBERT yang di‐fine-tune  
   - **Fitur:**  
     - Menghasilkan embedding kontekstual yang kaya untuk teks bahasa Indonesia  
   - **Kelebihan:**  
     - Akurasi tinggi, mampu menangkap nuansa konteks dan ambiguitas dalam bahasa alami  
   - **Kekurangan:**  
     - Memerlukan resource GPU dan penyesuaian hyperparameter  
   - **Catatan Tambahan:**  
     - **Multi-Task Learning:** Mengingat dataset memiliki label Sentimen dan Emosi, Anda dapat mempertimbangkan pendekatan multi-task learning dengan satu model (misal, IndoBERT) yang memiliki dua output head untuk mengklasifikasikan kedua label tersebut secara bersamaan.

---

### B. Ringkasan Ulasan (Summarization)

1. **Extractive Summarization**  
   - **Algoritma:**  
     - TextRank, LexRank, atau metode Luhn  
   - **Kelebihan:**  
     - Implementasi sederhana, tidak memerlukan dataset ringkasan manual  
   - **Kekurangan:**  
     - Hanya mengekstrak kalimat asli tanpa mengubah struktur bahasa  
   - **Catatan:**  
     - Cocok sebagai tahap awal untuk menentukan kalimat-kalimat kunci dari ulasan.

2. **Abstractive Summarization**  
   - **Algoritma:**  
     - IndoBART, mT5, atau PEGASUS (pretrained) yang di‐fine-tune untuk summarization  
   - **Kelebihan:**  
     - Mampu menghasilkan kalimat ringkasan baru yang lebih ringkas dan koheren  
   - **Kekurangan:**  
     - Memerlukan dataset ringkasan sebagai gold standard dan komputasi lebih berat  
   - **Catatan:**  
     - Jika tidak tersedia data ringkasan manual, metode ini lebih menantang untuk dilatih.

3. **Hybrid (Extractive + Abstractive)**  
   - **Pendekatan:**  
     - Menggunakan metode Extractive (misal, TextRank) untuk mendapatkan kalimat kunci, kemudian menggunakan model abstractive (misal, GPT-4 API atau model pretrained) sebagai side feature untuk memparafrase dan menyempurnakan ringkasan.  
   - **Kelebihan:**  
     - Menggabungkan efisiensi extractive dan kehalusan bahasa dari abstractive, sehingga menghasilkan ringkasan yang informatif dan natural  
   - **Kekurangan:**  
     - Arsitektur lebih kompleks dan bergantung pada API eksternal bila menggunakan LLM sebagai refinement  
   - **Catatan:**  
     - Pendekatan hybrid memungkinkan fleksibilitas jika data ringkasan manual terbatas, karena hasil extractive dapat “diperhalus” oleh LLM.

---

### C. Fitur Data Mining Tambahan

1. **Topic Modeling**  
   - **Algoritma:**  
     - LDA (Latent Dirichlet Allocation), NMF (Non-Negative Matrix Factorization)  
   - **Tujuan:**  
     - Menemukan topik-topik dominan dalam kumpulan ulasan (misal: masalah performa, UI, bug)

2. **Association Rule Mining**  
   - **Algoritma:**  
     - Apriori, FP-Growth  
   - **Tujuan:**  
     - Mencari pola keterkaitan antar kata, seperti jika “lag” sering muncul bersama “baterai cepat habis”

3. **Clustering**  
   - **Algoritma:**  
     - K-Means, DBSCAN  
   - **Tujuan:**  
     - Mengelompokkan ulasan serupa untuk analisis lebih mendalam (misal: ulasan yang berkaitan dengan fitur tertentu)

4. **Anomaly Detection**  
   - **Algoritma:**  
     - Isolation Forest, Autoencoder  
   - **Tujuan:**  
     - Mendeteksi ulasan spam atau outlier yang mungkin mengganggu analisis

---

## II. Daftar Fitur Aplikasi yang Mungkin Dibangun

1. **Summary (Ringkasan Ulasan)**  
   - Menyediakan ringkasan singkat dari ulasan yang mencakup poin-poin utama seperti keluhan dan pujian.

2. **Persentase Analisis Sentimen dan Emosi**  
   - Visualisasi (misal: pie chart/bar chart) untuk menunjukkan distribusi ulasan menurut sentimen (positif, netral, negatif) dan emosi (senang, sedih, marah, dsb.)

3. **Word Cloud / Kata Paling Sering Muncul**  
   - Menampilkan visualisasi kata-kata yang paling sering muncul secara keseluruhan atau berdasarkan kategori sentimen/emosi.

4. **Kata Paling Sering Muncul per Sentimen/Emosi**  
   - Membandingkan kata-kata kunci yang sering muncul di setiap kategori, misalnya ulasan positif versus negatif atau ulasan dengan emosi tertentu.

5. **Deteksi Pertanyaan**  
   - Mengidentifikasi ulasan yang mengandung pertanyaan untuk memudahkan tim support memberikan respons secara cepat.

6. **Fitur Data Mining Lanjutan**  
   - **Topic Modeling:** Menemukan tema atau kategori ulasan (misal: performa, UI, fitur baru) untuk memberikan insight topik dominan.  
   - **Association Rule Mining:** Mengungkap pola hubungan antar kata (misal: "crash" sering muncul bersama "update OS").  
   - **Spam/Anomaly Detection:** Memfilter dan mengidentifikasi ulasan yang terindikasi spam atau outlier.

7. **Dashboard Interaktif**  
   - Menyajikan semua informasi secara terintegrasi dalam satu tampilan interaktif (misal: menggunakan Streamlit, Dash, atau Power BI) sehingga stakeholder dapat dengan mudah melihat summary, distribusi sentimen, word cloud, dan tren data.

---

### Rekomendasi Penyusunan

1. **Pilih Metode Sesuai Kebutuhan dan Resource:**  
   - Jika data terbatas dan proses harus cepat, gunakan metode klasik (Naive Bayes, SVM) sebagai baseline.  
   - Jika mengutamakan akurasi dan memiliki sumber daya komputasi, fine-tune model transformer (misal, IndoBERT) dengan pendekatan multi-task untuk Sentimen dan Emosi.

2. **Sesuaikan Fitur dengan Tujuan Bisnis:**  
   - Fokus pada fitur yang mendukung pengambilan keputusan, seperti persentase sentimen/emosi dan trend analysis.  
   - Untuk layanan pelanggan, deteksi pertanyaan dapat diprioritaskan agar respon dapat dilakukan lebih cepat.

3. **Gunakan Pendekatan Modular:**  
   - Rancang pipeline terpisah untuk analisis sentimen/emosi, ringkasan, dan fitur data mining tambahan, agar masing-masing komponen dapat dioptimalkan dan diintegrasikan secara fleksibel.  
   - Integrasikan hasil tiap komponen ke dalam dashboard interaktif untuk memudahkan monitoring dan analisis.

---

### Diagram Alur Sistem (Contoh aja ini mah)

#### A. Pipeline Analisis Sentimen dan Emosi (Multi-Task)
```
              [Input Review]
                     │
             [Preprocessing]
                     │
         ┌──────────┴───────────┐
         │                      │
 [Ekstraksi Fitur Manual]   [Embedding Pretrained]
  (TF-IDF, Lexicon)           (IndoBERT)
         │                      │
         └──────────┬───────────┘
                    │
              [Fusion Layer]
                    │
      [Classifier Multi-Task (Sentimen & Emosi)]
                    │
         [Output: Label Sentimen & Emosi]
```

#### B. Pipeline Ringkasan Ulasan (Hybrid)
```
              [Input Review]
                     │
             [Preprocessing]
                     │
         [Extractive Summarization]
               (TextRank)
                     │
         [Candidate Summary]
                     │
       [LLM Enhancement (GPT-4 API)]
                     │
         [Refined Abstractive Summary]
```

---

Dengan daftar model/metode/algoritma dan fitur aplikasi yang disusun di atas, kita dapat menyesuaikan implementasi proyek berdasarkan data yang ada dan tujuan bisnis yang ingin dicapai. Pendekatan modular serta hybrid (baik untuk analisis sentimen/emosi maupun ringkasan ulasan) akan memaksimalkan pemanfaatan dataset 21 ribu baris, menghasilkan insight yang lebih kaya dan mendalam bagi stakeholder.
