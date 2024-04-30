# TUTORIAL 9 ADPRO  (High Level Networking)
#### Daffa Mohamad Fathoni (2206824161)
#### Advanced Programming B / GEN

<hr>

## REFLECTION

>1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?

- RPC Unary merupakan metode RPC paling dasar yang melibatkan pengiriman satu permintaan oleh klien ke server yang kemudian merespons dengan satu balasan. Metode ini sangat efektif untuk tugas-tugas yang hanya memerlukan pertukaran informasi sederhana, seperti verifikasi identitas atau pengisian formulir.
- RPC Streaming Server memungkinkan klien untuk mengirim satu permintaan dan menerima serangkaian balasan dalam bentuk stream dari server. Klien terus menerima data hingga stream tersebut selesai. Pendekatan ini sangat berguna ketika server harus mengirimkan jumlah data yang besar, seperti list panjang atau file, kepada klien.
- RPC Bi-directional Streaming adalah proses di mana klien dan server saling bertukar pesan melalui stream yang dapat dibaca dan ditulis. Stream ini berfungsi secara mandiri, memungkinkan kedua belah pihak untuk mengirim dan menerima pesan tanpa urutan tertentu. Ini sangat cocok untuk aplikasi yang memerlukan komunikasi dua arah yang intensif, seperti dalam aplikasi chatting.

>2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?

Dalam penerapan gRPC menggunakan Rust, ada beberapa aspek keamanan krusial yang harus diperhatikan, termasuk autentikasi, otorisasi, dan pengamanan data. Setiap elemen data yang ditransfer melalui gRPC harus melalui proses autentikasi dan otorisasi untuk menjamin keamanannya. Sistem autentikasi harus mengadopsi sertifikat SSL/TLS klien atau token yang terverifikasi dengan baik, dan mekanisme otorisasi harus efisien dalam menerapkan kebijakan akses. Selain itu, penting untuk mengenkripsi data yang dikirim antara server dan klien untuk memastikan kerahasiaannya. Penggunaan SSL/TLS dalam enkripsi membantu melindungi komunikasi dan harus didukung oleh validasi input yang ketat untuk menghindari kerentanan yang sering terjadi.

>3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?

Dalam penerapan streaming dua arah dengan gRPC, ada beberapa aspek kritis yang harus dikelola dengan baik, termasuk penanganan konkurensi, pengelolaan kesalahan, urutan pesan, back-pressure, alokasi sumber daya, keamanan, skalabilitas, dan latensi. Aspek-aspek ini harus ditangani untuk memastikan bahwa komunikasi antara klien dan server berjalan mulus, pesan tetap utuh, dan masalah konkurensi seperti kondisi balapan diatasi. Selain itu, penting untuk mengalokasikan sumber daya dengan bijak sambil mempertahankan keamanan dan kemampuan untuk meningkatkan sistem. Mengurangi latensi dan meningkatkan performa jaringan juga penting untuk memberikan pengalaman pengguna yang lebih baik, meski ini menimbulkan tantangan tersendiri dalam hal pemantauan dan peningkatan kinerja sistem.

>4. What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?

Penggunaan `tokio_stream::wrappers::ReceiverStream` dalam Rust membawa manfaat seperti kemampuan streaming asinkron, integrasi yang efisien dengan ekosistem Tokio untuk peningkatan performa, serta kemampuan untuk mengatasi back-pressure, yang membantu dalam pencegahan kelelahan sumber daya. Namun, penggunaannya juga menambah tingkat kerumitan pada kode, khususnya bagi pengembang yang belum terbiasa dengan asinkronisitas dalam Rust, dan memerlukan strategi penanganan kesalahan yang lebih matang untuk memastikan komunikasi yang akurat. Selain itu, pengelolaan waktu asinkron bisa menjadi kompleks dan jika tidak ditangani dengan baik, dapat menyebabkan terminasi yang tidak diinginkan.

>5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?

Untuk menjamin bahwa layanan gRPC di Rust dapat diperluas dan dipelihara dengan mudah, penting untuk memanfaatkan perpustakaan yang tersedia guna mengulang penggunaan dan pemeliharaan kode. Mengadopsi pendekatan desain yang modular, dengan mengorganisir kode ke dalam unit-unit modul yang memiliki tanggung jawab yang terdefinisi dengan baik, akan sangat membantu. Selain itu, memanfaatkan fitur-fitur yang memungkinkan pembuatan antarmuka yang efisien dan dapat digunakan kembali juga akan meningkatkan kualitas keseluruhan layanan.

>6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?

Untuk mengelola proses pembayaran yang kompleks, kita bisa memperbaiki `MyPaymentService` dengan mengubah fungsi `process_payment` menjadi layanan streaming. Ini akan memungkinkan kita untuk mengirimkan data ke klien secara bertahap dan efisien, sehingga memfasilitasi transfer informasi yang lebih rumit.

>7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?

Penggunaan gRPC sebagai protokol komunikasi mengubah cara kita mendesain dan membangun sistem terdistribusi. gRPC mengeliminasi keperluan untuk mempertimbangkan akses modul melalui metode HTTP tradisional, karena ia menyediakan mekanisme otomatis untuk menghubungkan dan memanggil metode yang diperlukan. Berkat file proto yang menyediakan kontrak bersama antara klien dan server, klien dapat dengan mudah memanggil metode server seakan-akan ada interaksi langsung. Ini memudahkan interaksi antar berbagai teknologi dan platform, serta meningkatkan kemampuan sistem yang berbeda untuk bekerja bersama dalam arsitektur yang kompleks.

>8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?

HTTP/2 membawa peningkatan signifikan atas HTTP/1.1, termasuk WebSocket untuk REST API. Fitur-fiturnya seperti multiplexing yang memungkinkan permintaan simultan, server push yang mengirim sumber daya tanpa diminta, kompresi header yang mengurangi beban data, protokol yang berbasis biner untuk efisiensi lebih tinggi, dan pengaturan prioritas untuk manajemen sumber daya yang optimal. Meskipun demikian, HTTP/2 juga menambahkan kerumitan dalam implementasi dan pemeliharaan, meningkatkan overhead karena enkripsi, dan dapat mengalami masalah dengan kemacetan TCP serta tantangan dalam kompatibilitas browser. Di sisi lain, WebSocket menyediakan komunikasi dua arah yang terus-menerus melalui satu koneksi TCP, yang ideal untuk interaksi real-time. HTTP/2 lebih cocok untuk aplikasi web standar yang melibatkan banyak permintaan dan respons kecil.

>9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?

REST API terkenal karena kemudahan penggunaannya, menggunakan metode HTTP yang umum dan bersifat stateless. Namun, kekurangannya terletak pada tidak adanya dukungan untuk komunikasi real-time, seringkali bergantung pada polling atau long-polling yang bisa menambah kompleksitas dan latensi. Sebaliknya, gRPC menyediakan fitur streaming dua arah yang memungkinkan klien dan server untuk saling mengirim data secara mandiri, menjadikannya pilihan yang tepat untuk kasus penggunaan real-time dan meningkatkan responsivitas. Meskipun lebih kompleks, streaming dua arah yang ditawarkan oleh gRPC dapat memberikan performa yang lebih unggul dan keuntungan dalam komunikasi real-time dibandingkan dengan REST API untuk beberapa skenario tertentu.

>10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?

gRPC bersama Protocol Buffer memberikan keuntungan dalam hal kompatibilitas dan efisiensi berkat struktur yang berbasis skema. Di sisi lain, JSON yang digunakan dalam REST API menawarkan keleluasaan dan kemudahan baca lintas bahasa serta platform, walaupun mungkin memerlukan biaya lebih. Dalam memilih antara keduanya, gRPC lebih cocok untuk situasi yang memerlukan tipe data yang ketat dan performa tinggi, sedangkan JSON lebih sesuai untuk kebutuhan yang lebih mengutamakan fleksibilitas dan kemudahan baca.