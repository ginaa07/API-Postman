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


 
