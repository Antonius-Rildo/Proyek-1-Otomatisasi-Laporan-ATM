# Proyek-1-Otomatisasi-Laporan-ATM
Proyek 1: Migrasi "mesin logika" (rule-based engine) V1.0 dari Excel ke Python untuk otomatisasi laporan downtime ATM.
# Proyek 1: Migrasi "Mesin Logika" V1.0 (Excel ke Python)

## 🎯 Ringkasan Proyek

Proyek ini adalah studi kasus Data Engineering dasar yang mendokumentasikan proses migrasi **"mesin logika bisnis" (business logic engine)** yang kompleks dari Microsoft Excel ke Python.

Di pekerjaan saya saat ini, saya bertanggung jawab untuk membuat laporan *downtime* ATM. Proses ini menerima 100+ laporan harian dari tim lapangan dalam format teks mentah yang tidak terstruktur ("kotor"). Untuk mengatasinya, saya membangun sebuah *engine* 3-pipa (3-step) di Excel menggunakan formula `IF/SEARCH/AND/OR` yang kompleks.

Proyek ini adalah **terjemahan 1:1** dari *engine* Excel tersebut ke dalam skrip Python (Pandas/Numpy) yang 100x lebih cepat dan lebih mudah dikelola.

**Tujuan Utama:**
1.  Membuktikan kelayakan migrasi dari Excel ke Python.
2.  Mengidentifikasi dan mendokumentasikan kelemahan fundamental dari pendekatan *rule-based* (berbasis aturan) V1.0.

---

## 🛠️ Tools & Data

* **Tools:** Python, Pandas, Numpy, Google Colab
* **Data:** `data_atm_downtime_FINAL.csv` - 100 baris data dummy "kotor" (realistis) yang mereplika laporan harian tim lapangan. Data ini sengaja dibuat tidak sempurna, mengandung:
    * Koma yang "nyasar" (mis: `"Listrik, ruko mati"`)
    * Input yang salah format (mis: "Music")
    * Berbagai variasi teks (mis: "padam", "mati listrik", "mati lampu")

---

## ⚙️ Arsitektur "Mesin" V1.0 (Rule-Based)

*Engine* ini berjalan dalam 3-pipa (3-step) logika, persis seperti di Excel:

1.  **Pipa 1 (Klasifikasi Teks):** Membaca teks mentah `Penyebab` (Kolom M) dan mengklasifikasikannya ke `N_Real_Problem` menggunakan puluhan kata kunci (`IF/SEARCH` versi Python).
2.  **Pipa 2 (Pemetaan Kategori):** Membaca hasil Pipa 1 (`N_Real_Problem`) dan memetakannya ke `P_Kategori` (Kolom P).
3.  **Pipa 3 (Logika Bisnis):** Membaca hasil Pipa 2 (`P_Kategori`) DAN data sistem (`R_Penanggung_Jawab`) untuk menentukan `Q_Responsibility` akhir.

---

## ⚠️ Temuan Kunci & Kelemahan Fatal

Proyek ini **berhasil** memigrasikan logika, namun juga **membuktikan dua kelemahan fatal** dari "Mesin" V1.0:

### 1. Kelemahan Logika: Ketergantungan pada Prioritas
*Engine* ini "bodoh". Dia hanya mengikuti aturan dari atas ke bawah. Ini menyebabkan kesalahan identifikasi kritis.

* **Contoh:** Teks `"open tiket ke tim jaringan"`
* **Hasil V1.0:** Salah diklasifikasikan sebagai `"Jaringan"` (karena kata "jaringan" diperiksa lebih dulu).
* **Hasil Seharusnya:** `"On-Progress"` (karena kata "open tiket" seharusnya lebih penting).

### 2. Kelemahan Teknis: Tidak Tahan Banting (Non-Robust)
*Engine* ini membutuhkan data yang 100% bersih. Saat dihadapkan pada data "kotor" di dunia nyata:

* **Data "Koma Nyasar" & "Bergeser":** Input yang salah format (misal: "Music") atau mengandung koma nyasar (`Listrik, ruko mati`) menyebabkan data *alignment* hancur.
* **Hasil:** *Engine* V1.0 **hancur total**. Dia **salah mengidentifikasi** data yang bersih (`Listrik ruko mati` terbaca sebagai `Restart Mesin`). Ini adalah kegagalan yang tidak bisa diterima.

---

## 🚀 Kesimpulan -> Jembatan ke Proyek 2

Proyek 1 ini sukses membuktikan bahwa *rule-based engine* V1.0 **tidak cukup baik** (not good enough) untuk lingkungan produksi di dunia nyata. Dia rapuh, "bodoh", dan hancur oleh data kotor.

Ini adalah justifikasi teknis sempurna mengapa kita harus beralih ke V2.0.

Ini adalah "jembatan" saya menuju **Proyek 2: "Mesin Cerdas" (Multi-Output NLP Classifier)**, di mana saya akan menggunakan **Machine Learning** untuk menggantikan logika V1.0. Tujuannya adalah membangun *engine* yang:
1.  **Dinamis:** Bisa mengerti *konteks* (mis: "open tiket" > "jaringan"), bukan prioritas.
2.  **Tahan Banting (Robust):** Bisa *belajar* dari data "kotor", bukan hancur karenanya.

---

## 📬 Kontak

Terima kasih telah meninjau proyek saya. Mari terhubung!

* **LinkedIn:** `https://www.linkedin.com/in/antonius-rildo-232b9411a/`
