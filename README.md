# Darknet Traffic Classification Using Federated Semi-Supervised Learning

## Rancangan Sistem

Penelitian ini mengimplementasikan pendekatan Federated Semi-Supervised Learning untuk klasifikasi traffic Darknet. Berikut adalah rancangan sistem yang digunakan:

### 1. Komponen-komponen Sistem

**A. Node Server (Aggregator)**
- **Perangkat**: Security Operations Center (SOC) server
- **Fungsi**:
  - Menginisiasi proses federated learning
  - Mengagregasi model dari clients
  - Mendistribusikan model global yang diperbarui
- **Algoritma**: Federated Averaging (FedAvg)

**B. Node Client**
- **Perangkat**:
  1. Router Edge/Gateway di berbagai cabang organisasi
  2. Intrusion Detection System (IDS) nodes
  3. Next-Generation Firewalls
  4. Network Monitoring Tools
- **Fungsi**:
  - Mengumpulkan traffic data lokal
  - Melatih model lokal menggunakan semi-supervised learning
  - Mengirim parameter model ke server
- **Algoritma**:
  - Self-Training dengan threshold confidence untuk pseudo-labeling
  - RandomForest/Neural Network untuk model dasar

### 2. Alur Proses

1. **Inisialisasi**:
   - Server mengirimkan model dasar awal ke semua clients
   - Pengaturan parameter threshold confidence untuk pseudo-labeling

2. **Pada Setiap Client**:
   - **Preprocessing**: Ekstraksi fitur dan normalisasi
   - **Semi-supervised Learning**:
     - Melatih model lokal pada data berlabel
     - Menghasilkan pseudo-labels untuk data tidak berlabel
     - Melatih ulang model dengan data kombinasi

3. **Komunikasi & Agregasi**:
   - Clients mengirim parameter model ke server
   - Server mengagregasi parameter untuk membuat model global
   - Server mengirim model global yang diperbarui ke semua clients

4. **Evaluasi & Deteksi**:
   - Model final diterapkan untuk klasifikasi real-time
   - Evaluasi performa pada data pengujian

### 3. Simulasi dalam Penelitian Ini

Dalam penelitian ini, sistem federated learning disimulasikan menggunakan Google Colab dengan dataset CIC-Darknet2020. Meskipun dataset ini memiliki label lengkap, untuk mensimulasikan kondisi dunia nyata dimana labeling traffic jaringan secara lengkap sangat sulit dicapai, penelitian ini:

1. Secara sengaja 'menghapus' label dari sebagian besar dataset (70-80%)
2. Memperlakukannya sebagai data tidak berlabel
3. Membagi dataset ke beberapa "klien virtual" untuk mensimulasikan distribusi data dalam environment federated learning

Simulasi ini memungkinkan evaluasi yang realistis tentang bagaimana metode yang diusulkan akan berperforma dalam lingkungan operasional nyata dengan keterbatasan data berlabel.

## Rancangan Eksperimen

Untuk mengevaluasi pendekatan Federated Semi-Supervised Learning dalam klasifikasi traffic Darknet, beberapa eksperimen akan dilakukan:

### Eksperimen 1: Pengaruh Rasio Data Berlabel
- Variasi rasio data berlabel: 10%, 20%, 30%, 50%
- Evaluasi: Accuracy, F1-score, dan learning curve

### Eksperimen 2: Dampak Jumlah Clients
- Variasi jumlah clients: 5 dan 10 clients
- Evaluasi: Model convergence dan komunikasi overhead

### Eksperimen 3: Non-IID vs IID Data Distribution
- Skenario distribusi data yang berbeda antar client
- Evaluasi: Robustness model terhadap heterogenitas data

### Eksperimen 4: Adaptabilitas Terhadap Pola Traffic Baru
- Simulasi domain shift dengan menambahkan jenis traffic baru
- Evaluasi: Adaptation time dan performance retention

### Metrik Evaluasi
1. **Performa Dasar**: Accuracy, Precision, Recall, F1-score, AUC-ROC
2. **Adaptabilitas**: Transfer adaptability score, kontinuitas pembelajaran
3. **Robustness**: Performa pada distribusi kelas yang berubah
4. **Sistem Federated**: Communication overhead, convergence rate
