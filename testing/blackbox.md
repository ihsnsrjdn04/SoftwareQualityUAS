# Black Box Testing

## Definisi
Black Box Testing adalah metode pengujian yang dilakukan tanpa melihat kode program. Pengujian hanya fokus pada input yang diberikan dan output yang dihasilkan oleh sistem.

---

## Penerapan pada Sistem CBT
Pengujian dilakukan berdasarkan tampilan (UI) dan fitur yang digunakan oleh user (mahasiswa dan admin).

---

## Fitur yang diuji
- Login pengguna  
- Registrasi  
- Input token ujian  
- Mengerjakan soal  
- Submit ujian  
- Menampilkan nilai  

---

## Contoh Pengujian

### 1. Login
Input: email & password benar  
Output: masuk ke dashboard  

---

### 2. Registrasi
Input: email valid, password ≥ 8 karakter  
Output: akun berhasil dibuat  

---

### 3. Token Ujian
Input: token benar (CBT2024)  
Output: ujian dimulai  

---

### 4. Mengerjakan Soal
Input: memilih jawaban  
Output: jawaban tersimpan  

---

### 5. Submit Ujian
Input: klik tombol submit  
Output: nilai ditampilkan  

---
# Black Box Testing

## Definisi

Black Box Testing adalah metode pengujian perangkat lunak yang berfokus pada fungsi sistem tanpa melihat struktur kode program. Pengujian dilakukan berdasarkan input dan output yang dihasilkan sistem.

---

# Model Pengujian Black Box Testing

```text
Black Box Testing
├── Boundary Value Analysis
│   └── Equivalence Partitioning
├── Comparison Testing
│   └── Decision Table Testing
├── Sample Testing
│   └── Robustness Testing
├── Behaviour Testing
│   └── Performance Testing
└── Endurance Testing
    └── Cause-Effect Relationship Testing
```

---

## 1. Boundary Value Analysis

### Objek Uji : calculateScore(correct, total)

| Correct | Total | Expected Result |
|----------|---------|----------------|
| 0 | 10 | 0 |
| 1 | 10 | 10 |
| 10 | 10 | 100 |
| 11 | 10 | Ditolak |
| 5 | 0 | Error atau 0 |

### Hasil

Sistem memerlukan validasi ketika nilai total bernilai 0.

---

## 2. Equivalence Partitioning

### Objek Uji : Login

| Kelas Data | Input | Hasil |
|------------|---------|---------|
| Valid | admin@gmail.com / password123 | Login berhasil |
| Tidak Valid | admin@gmail.com / salah | Login gagal |
| Tidak Valid | user@gmail.com / password123 | Login gagal |
| Tidak Valid | Kosong | Validasi muncul |

---

## 3. Comparison Testing

### Objek Uji : Login dan Ujian

| Browser | Hasil |
|----------|---------|
| Chrome | Normal |
| Firefox | Normal |
| Edge | Normal |

---

## 4. Decision Table Testing

### Objek Uji : Login

| Email Valid | Password Valid | Hasil |
|-------------|----------------|---------|
| Ya | Ya | Login berhasil |
| Ya | Tidak | Login gagal |
| Tidak | Ya | Login gagal |
| Tidak | Tidak | Login gagal |

---

## 5. Sample Testing

### Objek Uji : Soal Ujian

| Sampel Soal | Hasil |
|-------------|---------|
| HTML | Tampil |
| CSS | Tampil |
| JavaScript | Tampil |

---

## 6. Robustness Testing

### Objek Uji : Tambah Soal

| Input | Hasil |
|---------|---------|
| Data valid | Berhasil |
| Null | Ditolak |
| String kosong | Ditolak |
| Karakter khusus | Aman |

---

## 7. Behaviour Testing

### Objek Uji : Token Ujian

| Input Token | Hasil |
|-------------|---------|
| CBT2024 | Ujian dimulai |
| CBT1111 | Error |
| Kosong | Error |

---

## 8. Performance Testing

### Objek Uji : Perhitungan Nilai

| Jumlah Data | Hasil |
|-------------|---------|
| 10 | Cepat |
| 100 | Cepat |
| 1000 | Tetap responsif |

---

## 9. Endurance Testing

### Objek Uji : Sistem CBT

| Durasi | Hasil |
|---------|---------|
| 1 Jam | Stabil |
| 3 Jam | Stabil |
| 5 Jam | Stabil |

---

## 10. Cause-Effect Relationship Testing

| Cause | Effect |
|---------|---------|
| Token benar | Ujian dimulai |
| Token salah | Error |
| Jawaban benar | Nilai bertambah |
| User dihapus | Data user hilang |

---
