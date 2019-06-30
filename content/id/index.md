---
layout: about.hbs
title: Tentang
trademark: Merek Dagang
---
# Tentang Node.js&reg;

Sebagai runtime JavaScript yang didorong peristiwa asinkron, Node dirancang untuk dibuat
aplikasi jaringan yang dapat diskalakan. Dalam contoh "halo dunia" berikut, banyak
koneksi dapat ditangani secara bersamaan. Pada setiap koneksi, panggilan baliknya adalah
dipecat, tetapi jika tidak ada pekerjaan yang harus dilakukan, Node akan tidur.

```javascript
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Halo Dunia\n');
});

server.listen(port, hostname, () => {
  console.log(`Server berjalan di http://${hostname}:${port}/`);
});
```

Ini berbeda dengan model konkurensi yang lebih umum saat ini di mana benang OS
dipekerjakan. Jaringan berbasis thread relatif tidak efisien dan sangat
sulit digunakan. Selain itu, pengguna Node bebas dari kekhawatiran
proses penguncian mati, karena tidak ada kunci. Hampir tidak ada fungsi di Node
langsung melakukan I/O, jadi prosesnya tidak pernah menghalangi. Karena tidak ada yang menghalangi,
sistem scalable sangat masuk akal untuk dikembangkan di Node.

Jika beberapa bahasa ini tidak dikenal, ada artikel lengkap di
[Blocking vs Non-Blocking][].

---

Node serupa dalam desainnya dengan, dan dipengaruhi oleh, sistem seperti Ruby
[Event Machine][] atau Python [Twisted][]. Node mengambil model acara sedikit
lebih lanjut. Ini menyajikan *[event loop][]* (mengulang kejadian) sebagai konstruk runtime alih-alih sebagai pustaka. Di sistem lain selalu ada panggilan pemblokiran untuk memulai
*event-loop*.
Biasanya perilaku didefinisikan melalui panggilan balik di awal skrip
dan pada akhirnya memulai server melalui panggilan pemblokiran seperti
`EventMachine::run()`. Di Node tidak ada panggilan start-the-event-loop tersebut. Node
cukup masukkan loop acara setelah menjalankan skrip input. Node keluar dari
event loop ketika tidak ada lagi panggilan balik untuk dilakukan. Perilaku ini seperti
JavaScript browser-loop acara disembunyikan dari pengguna.

HTTP adalah warga negara kelas satu di Node, dirancang dengan streaming dan latensi rendah
dalam pikiran. Ini membuat Node cocok untuk fondasi pustaka web atau
kerangka.

Hanya karena Node dirancang tanpa utas, bukan berarti Anda tidak dapat menggunakannya
keuntungan dari beberapa core di lingkungan Anda. Proses anak dapat muncul
dengan menggunakan API [`child_process.fork()`][] kami, dan dirancang agar mudah
berkomunikasi dengan. Dibangun di atas antarmuka yang sama adalah modul [`cluster`][],
yang memungkinkan Anda berbagi soket di antara berbagai proses untuk memungkinkan penyeimbangan muatan
lebih dari inti Anda.

[Blocking vs Non-Blocking]: https://nodejs.org/en/docs/guides/blocking-vs-non-blocking/
[`child_process.fork()`]: https://nodejs.org/api/child_process.html#child_process_child_process_fork_modulepath_args_options
[`cluster`]: https://nodejs.org/api/cluster.html
[event loop]: https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/
[Event Machine]: https://github.com/eventmachine/eventmachine
[Twisted]: http://twistedmatrix.com/
