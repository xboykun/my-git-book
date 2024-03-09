# ❕ Tentang

## Google Firebase Cloud Firestore

_**Google Firebase Cloud Firestore**_ adalah _Backend as a Services_ (BaaS) yang menyediakan beragam tools dan layanan untuk membantu developer mengembangkan suatu aplikasi (web dan mobile) dengan lebih cepat.&#x20;

Backend as a Services sendiri adalah kategori layanan cloud yang mengelola backend aplikasi. Artinya, Firebase sebagai BaaS akan mengurusi segala hal mengenai backend seperti database, authentication, hosting, API dan lainnya.

Dengan bantuan Firebase, developer bisa lebih fokus membangun bagian _front-end_ aplikasi. Sebab, sisi _backend_ akan dikerjakan menggunakan Firebase dengan lebih praktis.&#x20;

## Google Pub Sub

Pub/Sub adalah singkatan dari publish/subscribe, merupakan sebuah teknologi messaging yang mengizinkan komunikasi dalam microservice terjadi secara paralel atau asynchronous, dan prosesnya terjadi secara real time.

Pub/Sub sendiri lebih ditujukan untuk keperluan backend (service-to-service), untuk komunikasi antar service dan end-user (service-to-client) bisa menggunakan teknologi messaging lainnya seperti [Firebase Realtime Database](https://firebase.google.com/docs/database) atau [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging).

## Collection Core

_**Collection Core**_ merupakan yang bertujuan untuk pemusatan penggunaan dari _**Google Firebase Cloud Firestore**_, selain itu juga membantu anda dalam menghubungkan service anda ke _**Google Firebase Cloud Firestore**_.

#### Server

Collection core server dapat melayani dengan beberapa metode api yaitu :&#x20;

| API             | Metode        |
| --------------- | ------------- |
| PubSub As Async | Save          |
| GRPC            | Retrive, Save |

#### Client SDK

Collection core dapat digunakan dengan hanya mengintegrasikan service anda dengan SDK.&#x20;

## Source

{% embed url="https://www.niagahoster.co.id/blog/firebase-adalah/" %}
Firebase
{% endembed %}

{% embed url="https://medium.com/@rezaindra/apa-itu-pub-sub-6ab0591329c9" %}
Pub/Sub
{% endembed %}
