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
console.log("isi json", json) karena code yang diatas sebelum gambar itu ID_Token nya belum muncul, namun ketika saya menambahkan code tersebut  bisa langsung muncul di dan merespons 200 ok, Agar Postman bisa "membaca" dan mengambil data spesifik
