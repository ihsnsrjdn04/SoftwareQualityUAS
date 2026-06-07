# White Box Testing

## Definisi
White Box Testing adalah metode pengujian yang dilakukan dengan melihat dan memahami struktur kode program. Pengujian ini fokus pada logika, alur program, dan proses internal sistem.

---

## Penerapan pada Sistem CBT
Pengujian dilakukan pada bagian kode JavaScript, khususnya pada controller dan fungsi logika sistem.

---

## Controller / Fungsi yang diuji
- AuthController → login & registrasi  
- ExamController → token ujian & perhitungan nilai  
- AdminController → kelola soal & user  

---

## Struktur Data yang digunakan
- user  
- soal  
- jawaban  
- nilai  

---

## Tujuan
- Memastikan logika program berjalan dengan benar  
- Memastikan proses penyimpanan data sesuai  
- Memastikan perhitungan nilai akurat  

---

## Contoh

### 1. Login
Jika email dan password benar:
- user masuk ke dashboard  

Jika salah:
- sistem menampilkan error  

---

### 2. Token Ujian
Jika token = CBT2024:
- ujian dimulai  

Jika salah:
- muncul error  

---

### 3. Perhitungan Nilai
Jika jawaban benar:
- nilai dihitung (correct / total * 100)  
- hasil ditampilkan  

---

# White Box Testing

## Definisi

White Box Testing adalah metode pengujian yang dilakukan dengan menganalisis struktur internal kode program, logika, alur kontrol, alur data, serta setiap jalur eksekusi yang terdapat pada sistem.

---

# Model Pengujian White Box

## 1. Desk Checking

Desk Checking dilakukan dengan menelusuri kode secara manual untuk memastikan logika program sesuai dengan kebutuhan sistem.

### Objek Pengujian

#### ExamController.js

```javascript
export function startExam(token){
    if(token === "CBT2024"){
        return true;
    }
    return false;
}
```

### Hasil Analisis

| Input Token | Output | Status |
|------------|---------|---------|
| CBT2024 | true | Valid |
| CBT1234 | false | Valid |
| kosong | false | Valid |

---

## 2. Code Walkthrough

Code Walkthrough dilakukan bersama anggota tim untuk meninjau alur program.

### Fungsi yang Direview

#### calculateScore()

```javascript
export function calculateScore(correct, total){
    return Math.round((correct / total) * 100);
}
```

### Analisis

Rumus yang digunakan:

\[
Score = \frac{correct}{total} \times 100
\]

Contoh:

| Correct | Total | Hasil |
|----------|---------|--------|
| 8 | 10 | 80 |
| 10 | 10 | 100 |
| 5 | 10 | 50 |


---

## 3. Formal Inspection

Formal Inspection dilakukan untuk menemukan kesalahan logika, bug, dan pelanggaran standar coding.

### Temuan

#### Fungsi calculateScore()

Potensi error:

```javascript
calculateScore(5,0)
```

Akan menghasilkan:

```javascript
Infinity
```

### Rekomendasi Perbaikan

```javascript
export function calculateScore(correct,total){
    if(total <= 0){
        return 0;
    }

    return Math.round((correct/total)*100);
}
```

---

# Control Flow Testing

## 1. Fungsi startExam()

### Flow Graph

```
Start
  |
  v
token == CBT2024 ?
 /          \
Ya          Tidak
 |             |
true        false
 \           /
     End
```

### Cyclomatic Complexity

Rumus:

V(G) = Predicate Node + 1

V(G) = 1 + 1

V(G) = 2

### Independent Path

Path 1

```
Start → token benar → true → End
```

Path 2

```
Start → token salah → false → End
```

### Test Case

| Path | Input | Output |
|--------|---------|---------|
| P1 | CBT2024 | true |
| P2 | CBT1111 | false |

---

# Basic Path Testing

## Fungsi startExam()

### Jalur Independen

#### Path 1

```
Start
↓
Token valid
↓
Return true
↓
End
```

#### Path 2

```
Start
↓
Token tidak valid
↓
Return false
↓
End
```

### Hasil Pengujian

| Path | Status |
|--------|---------|
| P1 | Lulus |
| P2 | Lulus |

---

# Data Flow Testing

## Fungsi addQuestion()

```javascript
export function addQuestion(question){
    let data = JSON.parse(localStorage.getItem("questions")) || [];
    data.push(question);
    localStorage.setItem("questions", JSON.stringify(data));
    return true;
}
```

### Definisi dan Penggunaan Variabel

| Variabel | Definisi | Penggunaan |
|-----------|------------|------------|
| data | Mengambil data soal | push(), setItem() |
| question | Parameter input | push() |

### Pengujian

| Skenario | Hasil |
|-----------|---------|
| Data kosong | Soal berhasil ditambah |
| Data sudah ada | Soal berhasil ditambah |
| Input null | Perlu validasi tambahan |

---

## Fungsi deleteUser()

```javascript
export function deleteUser(email){
    let users = JSON.parse(localStorage.getItem("users")) || [];
    users = users.filter(u => u.email !== email);
    localStorage.setItem("users", JSON.stringify(users));
    return true;
}
```

### Data Flow

```
email
   ↓
filter()
   ↓
users baru
   ↓
localStorage
```

### Pengujian

| Kondisi | Hasil |
|----------|---------|
| User ditemukan | Berhasil dihapus |
| User tidak ditemukan | Data tetap |
| List kosong | Tidak error |

---

# Loop Testing

## Fungsi deleteUser()

Loop terjadi secara internal pada:

```javascript
users.filter(u => u.email !== email)
```

### Pengujian Loop

| Jumlah Data | Hasil |
|-------------|---------|
| 0 user | Tidak error |
| 1 user | Berjalan normal |
| >1 user | Berjalan normal |

### Boundary Testing

| Data User | Hasil |
|------------|---------|
| 0 | Valid |
| 1 | Valid |
| 100 | Valid |
| 1000 | Valid |

---

# Ringkasan Hasil White Box Testing

| Metode | Objek Uji | Status |
|---------|-----------|---------|
| Desk Checking | startExam() | Lulus |
| Code Walkthrough | calculateScore() | Lulus |
| Formal Inspection | calculateScore() | Ditemukan potensi bug |
| Control Flow Testing | startExam() | Lulus |
| Basic Path Testing | startExam() | Lulus |
| Data Flow Testing | addQuestion(), deleteUser() | Lulus |
| Loop Testing | deleteUser() | Lulus |

---


