# ❕ Tentang

Tujuan kami membuat ini menjadi SDK yaitu agar memberikan kemudahan bagi service lain dalam penggunaan layanan API GRPC / Pub Sub pada Collection Core Service Feature-nya, yaitu:

* Konfigurasi GRPC Client
* Konfigurasi Publisher ke Pub/Sub
* Builder Object Request Data, yaitu:
  * GRPC Proto buffer
  * Publish JSON Object ke Pub/Sub
* Builder Response GRPC Client ke Response yang mudah dihandle

### Limitasi

* Tidak support document total
* Tidak support kombinasi not-in dan not equals (!=)
* Tidak support collection group
* Pagination masih memakai limit dan offset, cursor pagination belum di support
* Jika menggunakan range comparation (<, >, <=, >=), ordering pertama harus sama dengan field pada filter
* Tidak bisa mengkombinasi in, not-in dan array-contains-any pada satu query

