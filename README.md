# 🏥 UNS Medical Center - Survei Kepuasan Pasien (Matkul PemWeb)

Aplikasi web *front-end* ini adalah purwarupa sistem survei kepuasan pasien untuk UNS Medical Center. Proyek ini dibangun untuk memenuhi tugas praktikum mata kuliah, berfokus pada perancangan antarmuka pengguna (UI) yang interaktif, responsif, dan fungsional menggunakan Vanilla JavaScript dan *local storage* untuk simulasi basis data.

## ✨ Fitur Utama
* **Sistem Autentikasi Klien:** Pendaftaran dan proses masuk (login) akun menggunakan `localStorage`.
* **Dasbor Statistik:** Visualisasi data gabungan dari data historis (dummy) dan data riwayat pengguna secara *real-time*.
* **Formulir Survei Interaktif:** Form penilaian multi-langkah (*multi-step*) dengan indikator progres dinamis dan validasi input.
* **Desain Modern:** Menggunakan Tailwind CSS dipadukan dengan gaya visual *Claymorphism* untuk elemen antarmuka yang lebih hidup.

## 🚀 Teknologi yang Digunakan
* **HTML5 & CSS3**
* **Vanilla JavaScript (ES6+)**
* **Tailwind CSS** (via CDN)

## 🛠️ Cara Menjalankan Aplikasi
Karena aplikasi ini berbasis *client-side* murni, kamu tidak perlu melakukan instalasi *server* atau *package manager*.
1. *Clone* repositori ini: `git clone https://github.com/[username-github-kamu]/uns-medical-center.git`
2. Buka folder proyek.
3. Buka file `login.html` menggunakan *browser* pilihan kamu (disarankan Chrome atau Firefox).

---

## 📖 Penjelasan Blok Kode Utama (Sesuai Syarat Laprak)

Berikut adalah penjelasan mengenai cara kerja blok kode utama yang menjadi inti dari fungsionalitas aplikasi ini:

### 1. Sistem Registrasi & Login (login.html)
Aplikasi ini tidak menggunakan *database backend*. Semua data pengguna disimpan di dalam *browser* menggunakan `localStorage`.

```javascript
function handleRegister(e){
  e.preventDefault();
  const name     = document.getElementById('reg-name').value.trim();
  const email    = document.getElementById('reg-email').value.trim().toLowerCase();
  const password = document.getElementById('reg-password').value;
  const users    = JSON.parse(localStorage.getItem('uns_users')||'[]');
  
  // Validasi email duplikat
  if(users.find(u=>u.email===email)){ 
    showAlert('Email sudah terdaftar.'); 
    return; 
  }
  
  // Menyimpan pengguna baru
  users.push({name,email,password});
  localStorage.setItem('uns_users',JSON.stringify(users));
  showAlert('Akun berhasil dibuat! Silakan masuk.','success');
  
  // Reset form dan alihkan ke tab login
  e.target.reset(); checkStrength('');
  setTimeout(()=>switchTab('login'), 1300);
}
