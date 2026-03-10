# API-Postman

Dokumentasi Pengujian Alur Firebase Auth & Backend API
Repositori ini berisi dokumentasi teknis mengenai pengujian alur End-to-End Authentication menggunakan Firebase Identity Toolkit REST API yang diintegrasikan dengan Backend API. Pengujian dilakukan menggunakan Postman untuk memastikan validitas token sebelum diimplementasikan ke dalam aplikasi mobile.

Persiapan awal sebelum melakukan request pada Postman, langkah pertama adalah melakukan setup pada Firebase Console:
1. Akses Firebase.com
<img width="1882" height="828" alt="image" src="https://github.com/user-attachments/assets/027ed070-3e3f-4ea9-9104-8193857be387" />

2. Setelah itu membuat project dengan mengAkses Firebase Console 
<img width="1782" height="808" alt="image" src="https://github.com/user-attachments/assets/794795ce-a8cd-4abc-8c8b-33cf06588cf8" />


3. Buat project baru di Firebase
<img width="1215" height="721" alt="image" src="https://github.com/user-attachments/assets/c5cfee89-d4d6-4bf6-80e4-97a7ea6bd52f" />


4. Aktifkan Authentication: Pilih metode Email/Password pada menu Authentication
<img width="1595" height="753" alt="image" src="https://github.com/user-attachments/assets/27484775-7d39-42bc-a4dc-21783eb68bb1" />


6. Untuk Mendapatkan Web API Key kita Pergi ke Project Settings lalu General
<img width="1897" height="811" alt="image" src="https://github.com/user-attachments/assets/5d908a21-4628-4db1-a8c1-0c26e91c7e59" />


7. Salin Web API Key
<img width="1910" height="832" alt="image" src="https://github.com/user-attachments/assets/d4e2897c-2b17-4a51-98ac-b4a399fddc9d" />

8. Lalu buat Web App
<img width="1757" height="739" alt="image" src="https://github.com/user-attachments/assets/e76e3308-45a8-436e-a5ac-7e9b60646975" />

Setelah menyelesaikan konfigurasi di Firebase Console (membuat project, mengaktifkan Auth, dan menyalin Web API Key), Lalu buka aplikasi Postman dan ikuti urutan berikut:
1. Buat Environment baru di Postman, lalu beri nama "Firebase Auth Dev", namun saya memberi nama dengan Global Environment
<img width="785" height="384" alt="image" src="https://github.com/user-attachments/assets/2c02e9e4-13b2-48a1-ae4a-d5ce446bbfb9" />

2. Ubah method nya menjadi POST
<img width="766" height="653" alt="image" src="https://github.com/user-attachments/assets/6370ea96-985d-47b8-be01-be8da006f4ae" />

3. Masukkan URL berikut di kolom URL : https://identitytoolkit.googleapis.com/v1/accounts:signUp?key={{FIREBASE_API_KEY}}
4. Pindah ke Tab Headers, tambahkan key = Content-Type, Value = application/json
<img width="1896" height="378" alt="image" src="https://github.com/user-attachments/assets/6be9f56c-89f6-4841-a1b8-db098e0b228c" />

5. Lalu pindah ke Tab Body (raw JSON)
pilih raw, lalu Masukkan ini pada body: { "email": "{{USER_EMAIL}}", "password": "{{USER_PASSWORD}}", "returnSecureToken": true }
<img width="1342" height="388" alt="image" src="https://github.com/user-attachments/assets/84eb35b6-fe8c-465d-bf50-ad8d9e22c65c" />

 6. Setekah ke bagian body, kita lanjut ke Pre-request Scripts di Postman agar idToken tersimpan otomatis
Dengan memasukkan Scripts
if (pm.response.code === 200) {
pm.environment.set("FIREBASE_ID_TOKEN", json.idToken);
pm.environment.set("FIREBASE_LOCAL_ID", json.localId);
pm.environment.set("FIREBASE_REFRESH_TOKEN", json.refreshToken);
console.log("Register sukses. UID:", json.localId);
console.log("PERHATIAN: Email belum diverifikasi. Lanjut ke Step 2.");
} else {
console.log("Register gagal:", json.error.message);
}
<img width="1250" height="490" alt="image" src="https://github.com/user-attachments/assets/e0d0f784-bfcd-4f96-b34e-98effd2c5eff" />
terlihat digambar saya ada penambahan code "let json = pm.response.json();
console.log("isi json", json) karena code yang diatas sebelum gambar itu ID_Token nya belum muncul, namun ketika saya menambahkan code tersebut  bisa langsung muncul dan merespons 200 ok, Agar Postman bisa "membaca" dan mengambil data spesifik, setelah selesai bisa langsung Send

 Langkah selanjutnya yaitu Verifikasi
 1. Buka tab baru pada Postman
 2. Ubah method menjadi POST
<img width="766" height="653" alt="image" src="https://github.com/user-attachments/assets/6370ea96-985d-47b8-be01-be8da006f4ae" />

3. Masukkan URL berikut di kolom URL : https://identitytoolkit.googleapis.com/v1/accounts:sendOobCode?key={{FIREBASE_API_KEY}}
4. Pindah ke tab Headers, tambahkan : key = Content-Type, Value = application/json
<img width="1344" height="304" alt="image" src="https://github.com/user-attachments/assets/b715e1ca-2ae2-4465-a03a-ea37a995c323" />

5. Pindah ke tab Body, pilih raw, selanjutnya masukkan ini: { "requestType": "VERIFY_EMAIL", "idToken": "{{FIREBASE_ID_TOKEN}}" }
<img width="1309" height="334" alt="image" src="https://github.com/user-attachments/assets/f85fc98b-e26f-4ef0-bb19-304501b6d113" />

6. Masuk ke bagian Scripts, pastikan pilih yang Post-reponse: if (pm.response.code === 200) { const json = pm.response.json(); console.log("Email verifikasi dikirim ke:", json.email); console.log("Sekarang buka inbox email dan klik link verifikasi."); console.log("Setelah klik, lanjut ke Step 3 untuk cek status."); } else { console.log("Gagal kirim email:", pm.response.json().error.message); }
setelah selesai langsung klik Send
<img width="1339" height="517" alt="image" src="https://github.com/user-attachments/assets/786a0d94-648e-412c-acfa-bbf160b766ad" />

Dan kita bisa klik link yang sudah masuk pesan di Email, dan lihat di inbox di email akan muncul seperti ini 
<img width="1814" height="439" alt="image" src="https://github.com/user-attachments/assets/f4faadc7-9e0b-4c90-a3fa-f20cca061c0a" />


Langkah 3 (Cek Status Verifikasi Email): Untuk Cek Verifikasi Email ada 2 Cara, bisa langsung ke firebase atau Via Backend.

Cara A Cek langsung ke Firebase (accounts:lookup):

1. Pakai URL (Endpoint) yang ini: https://identitytoolkit.googleapis.com/v1/accounts:lookup?key={{FIREBASE_API_KEY}}
2. Request Body: { "idToken": "{{FIREBASE_ID_TOKEN}}" }
<img width="1330" height="403" alt="image" src="https://github.com/user-attachments/assets/09f14fac-cd8c-4082-9eef-818b4b405163" />
Dan untuk Response Sukses nya seperti ini
<img width="1327" height="765" alt="image" src="https://github.com/user-attachments/assets/6735262c-6e89-41fe-b651-331a9495b302" />

Cara B Cek via Backend (POST /auth/verify-token):
1. Endpoint: {{BACKEND_BASE_URL}}/auth/verify-token
2. Request Body: { "firebase_token": "{{FIREBASE_ID_TOKEN}}" }
<img width="1787" height="434" alt="image" src="https://github.com/user-attachments/assets/f2d1f231-3588-4dbc-a2b5-ab2ded2ad7f6" />

Langkah 4 selanjutnya dengan (Login dengan Email & Password):

1. Endpoint : https://identitytoolkit.googleapis.com/v1/accounts:signInWithPassword?key={{FIREBASE_API_KEY}}
2. Untuk Pre-Request Body: { "email": "{{USER_EMAIL}}", "password": "{{USER_PASSWORD}}", "returnSecureToken": true }
<img width="1266" height="424" alt="image" src="https://github.com/user-attachments/assets/40ee79e0-86af-4823-8f3d-0d7db177f33a" />
3. Dan untuk Test Script — Auto-update Token: // Postman → Tests tab: const json = pm.response.json(); if (pm.response.code === 200) { // Update environment dengan idToken BARU hasil login pm.environment.set("FIREBASE_ID_TOKEN", json.idToken); pm.environment.set("FIREBASE_REFRESH_TOKEN", json.refreshToken); console.log("Login berhasil. Token diperbarui."); console.log("Lanjut ke Step 5: kirim token ke backend."); } else { console.log("Login gagal:", json.error.message); }
<img width="1282" height="644" alt="image" src="https://github.com/user-attachments/assets/6a26f09f-c9e5-4daf-a44a-75a08f293e40" />
(Catatan: di Login ini ada code yang saya tambahkan yaitu const diganti let, console.log("isi json", json), dan console.log("tes", json.idToken)
karena jika saya memakai code yang seperti di modul tersebut, dia tidak bisa membaca dan memberikan response)

Dan untuk Response Sukses nya seperti ini
<img width="1334" height="405" alt="image" src="https://github.com/user-attachments/assets/c4d2ece0-0b71-486e-9a29-1fa69801744c" />
<img width="1279" height="412" alt="image" src="https://github.com/user-attachments/assets/863eed16-8dd6-43fd-9939-b7205005d43e" />







