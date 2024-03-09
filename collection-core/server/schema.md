# 🗺️ Schema

### Firestore

**Collection Core** akan membuat dokumen koleksi berdasarkan service dan environment kamu. \
Kamu tidak dapat mengakses koleksi lain di luar koleksi inti koleksi.

<figure><img src="../.gitbook/assets/Collection Core - Firestore Schema.png" alt=""><figcaption><p>Firestore Schema</p></figcaption></figure>

### Pub/Sub

**Collection Core** untuk pubsub tidak ada spesifikasi khusus untuk nama **Topic**-nya, kamu hanya perlu menambahkan **Topic** pada **Project GCP** kamu dan serta buat **Service Account**-nya (untuk authentikasi).

<figure><img src="../.gitbook/assets/Screenshot 2023-02-21 at 09.55.47.png" alt=""><figcaption><p>Create Topic Pub/Sub</p></figcaption></figure>
