# Infografik isometrik — gaya explainer ketujuh

Satu sistem diperlihatkan sebagai diorama isometrik di atas papan yang melayang:
balok warna datar bernada tiga, label bertinta tipis, angka yang dibangun dari
ikon. Benda membuka diri untuk memperlihatkan isinya; angka digambar, bukan
diucapkan. Starter: `assets/starter-explainer-iso.html`.

Cocok untuk: proses dan rantai pasok, cara kerja sistem (air, listrik, data,
pabrik, kota), laporan angka, perbandingan dua tempat/era. Kurang cocok untuk
cerita berkarakter emosional (pakai kartun panggung) atau berita berfoto
(pakai jurnalisme visual).

## Kenapa gaya ini lolos uji PPT

- Papan diorama adalah **benang merah dunia** (Larangan struktural #2): semua
  adegan terjadi di satu dunia yang disusuri kamera, bukan section yang di-fade.
- Informasi baru = perubahan keadaan di dunia (dinding dipotong, air naik,
  ikon bertambah), bukan teks baru di atas latar diam.
- Teks maksimal dua tingkat: judul label pin + angkanya. Legenda di akhir
  dihitung objek.

## Hukum gaya

1. **Isometrik sejati, tidak pernah berputar.** Sumbu 30°; x ke kanan-bawah,
   y ke kiri-bawah, z naik. `sx = (x − y)·cos30°·k`, `sy = ((x + y)/2 − z)·k`.
   Kamera hanya bergeser dan zoom (titik dunia di tengah layar + `k` px per
   unit). Tidak ada perspektif, tidak ada tilt, tidak ada roll.
2. **Tiga nada per sisi, tanpa outline pada benda.** Atas terang, sisi kiri
   (+y) sedang, sisi kanan (+x) gelap. Semua diturunkan dari satu warna dasar
   (`tri(hex)`: dicampur ke putih hangat untuk atas, ke gelap kebiruan untuk
   sisi kanan, sehingga bayangan sedikit dingin).
3. **Tinta hanya untuk perabot infografik.** Garis 2 px: pin, leader, garis
   potong putus-putus, arsir penampang, cincin pelacak, rute. Perabot ini
   tinggal DI DUNIA, ikut kamera.
4. **Papan diorama.** Melayang di atas latar pucat berkisi titik isometrik,
   dengan bayangan lembut. Tepi depan papan memperlihatkan strata (tanah, batu,
   air, lantai, pipa); strata itu bisa menjadi cerita sendiri.
5. **Angka = ikon (Isotype).** Ikon identik berulang mewakili jumlah, dan
   jumlahnya benar. Ikon muncul memantul satu per satu mengikuti ketukan;
   angka berjalan pada rentang yang sama.
6. **Solid masuk lewat gerak, bukan alpha.** Benda jatuh, tumbuh, atau
   meluncur masuk. Benda solid setengah transparan terlihat seperti hantu.
   Pengecualian: kulit yang dilepas saat cutaway boleh memudar sambil bergeser.
7. **Tidak ada yang bergerak tanpa garis yang mendahului.** Rute digambar
   sedikit di depan benda yang menempuhnya; leader tumbuh sebelum inset terbuka;
   garis potong digambar sebelum kulit bergeser.

## Warna

- Latar netral pucat (krem, abu kertas, biru pucat) + 5–7 rona datar, masing-
  masing bernada tiga, + satu warna tinta.
- **Satu rona = satu makna**, seperti legenda peta: air selalu biru yang sama,
  subjek selalu ronanya sendiri. Rona tidak dipakai untuk dua arti.
- Rona subjek dicadangkan untuk **fokus + konteks**: saat cerita menunjuk
  "yang ini", semuanya memudar ke abu hangat (`iso.desat`) dan hanya subjek
  (`iso.keep = true`) yang tetap berwarna.
- Palet diturunkan dari topik (Hukum #3), bukan disalin dari starter.

## Tipografi

- Satu sans geometris (starter: Jost, OFL). Judul label 600 kapital berspasi
  lebar; angka 400 besar (≈ 44 px), satuan setengah ukuran. Semua teks diberi
  halo warna latar ≈ 7 px agar terbaca di atas balok mana pun.
- **Pin label**: titik (cincin tinta, isi pucat) → leader tegak → garis
  mendatar → teks. Arah pin dipilih per objek supaya tidak menutup subjek.
- Judul boleh berupa huruf isometrik di permukaan dunia (`iso.text3`), boleh
  diekstrusi.
- Tetap patuh batas ukuran skill: tidak ada teks < 30 px pada panggung 1080
  (label pin 25 px di starter sudah di batas bawah; naikkan untuk 9:16).

## Gerak

- **Cutaway**: garis potong (≈ 0,3 dtk) → kulit dekat bergeser keluar
  sepanjang normalnya sambil memudar (≈ 0,35 dtk, ease-out) → arsir penampang
  muncul di tepi potongan. Atap/kulit atas ikut terangkat bila menutupi isi.
- **Akumulasi = percepatan**: kedatangan per ketukan, lalu setengah ketukan,
  lalu gelombang — sistem terasa makin penuh.
- **Benda beraksi**: squash ≈ 18 % saat mendarat, pantulan kecil, perubahan
  warna yang menunjukkan proses (mentah → matang, kosong → penuh).
- Kendaraan mengikuti polyline dengan ease-in-out dan menghadap arah lajunya
  (`iso.push(x, y, z, rot)`).
- Orang = billboard minimal (kepala bulat, badan dua nada, satu lengan tebal,
  topi/rambut sebagai identitas, tanpa wajah), melangkah 12 fps.

## Kamera (menu, bukan rute)

Zoom diinterpolasi secara logaritmik (tween `Math.log(k)`, lalu `k = exp`),
sehingga dorong dan tarik terasa rata. Semua state kamera ada di objek `S`
dan di-tween GSAP — Hukum #2 terpenuhi.

| Gerak | Artinya | Contoh |
|---|---|---|
| Ikuti rute | proses, sebab → akibat | rantai pasok, perjalanan sinyal |
| Tahan wide + inset bulat | sistem dan individu sekaligus | satu pekerja di pabrik |
| Dorong menembus cutaway bersarang | turun skala, mencari satu di antara jutaan | ke dalam mesin |
| Tarik mundur cepat | lega, gambaran besar setelah detail | angka dibuat fisik |
| Bingkai terkunci, benda menumpuk | sistem penuh, beban berlebih | antrean, lalu lintas |
| Turun menembus strata | lapisan, kedalaman, sejarah | geologi, tumpukan software |
| Ganti papan | sebelum/sesudah, sini vs sana | dua kota, dua era |

Ukuran shot tetap berlaku (`techniques.md` §3b): subjek ≥ 1/3 tinggi frame di
momen kunci; label tidak menutupi subjek.

## Gerak khas (pilih yang dibutuhkan cerita)

- **Cutaway** — jantung, rak server, sarang lebah, tangki di dalam rumah.
- **Angka Isotype** — ikon identik dalam susunan baru tiap kali (kalender,
  batang, siluet yang dibentuk ikon itu sendiri).
- **Fokus + konteks** — satu pasien di rumah sakit, satu paket di jaringan.
- **Bingkai dalam bingkai** — leader tumbuh menjadi inset bulat close-up
  (`inset()`).
- **Pengungkapan skala** — tarik mundur sampai semua label terlihat; frame
  terakhir adalah infografik yang utuh.
- **Subjek terlacak** — satu benda diikuti dengan cincin "di sini" (`ring()`).
- **Penampang strata** — tepi papan menjadi cerita (lapisan ditambah/dibuang).

## Suara

Musik akustik ringan (kalimba, marimba, gitar nilon, pizzicato, woodblock,
perkusi tangan) atau denyut elektronik bersih untuk sistem teknis. Satu bunyi
per ikon saat angka terisi; ambience per stasiun di-crossfade; foley menurut
bahannya (air dituang dengan nada naik, keramik berdenting, kertas sobek).
Musik di-duck ≈ 8 dB di bawah VO; akhir −14 LUFS.

## Jebakan

| Gejala | Sebab | Obat |
|---|---|---|
| Dinding belakang/tangki hilang di balik tanah | papan raksasa menang di urutan painter (pusat kedalamannya ≈ 0) | papan dan lantai di `layer:0`; benda di layer 1 |
| Sisi benda hilang | normal Newell tergantung urutan titik → dianggap back face | beri `out` (arah keluar) pada `face3` |
| Benda gabungan (bukit bertingkat, derek di atas kapal) tersusun salah | sorting generik per primitif | gambar sebagai satu item berurutan, atau beri `bias` |
| Isi tak terlihat walau kulit depan sudah lepas | atap/kulit atas masih menutup | angkat atap bersama kulit |
| Cakram raksasa melintas saat close-up | detail dunia di belakang ikut membesar | lewati detail kecil di atas ambang zoom; latar datar di belakang benda utama |
| Satu frame jelek saat tarik mundur melewati benda tinggi | benda tinggi muncul mendadak | pudarkan benda tinggi menurut zoom |
| Benda terbaca sebagai benda lain | siluet salah (kotak putih beratap merah = rumah) | beri mesin bagian khasnya |
| Roda/lambung menembus permukaan | tanpa celah | beri celah yang terlihat |

## Engine

`assets/starter-explainer-iso.html` meng-inline engine Canvas 2D tanpa
dependensi (diadaptasi dari Lemo-Opuscar, MIT): `Iso` (proyeksi, kamera,
antrean tersortir: `box`, `prism`, `cyl`, `cone`, `roof`, `sphere`, `flat`,
`line3`, `bill`, `text3`, `push/pop`, `sub`, `desat` + `keep`), `tri()`,
`pin`, `inset`, `cutLine`, `hatch`, `ring`, `ICON.*` + `iconGrid`, `person`,
dan `shape()` yang mengubah garis bentuk 2D apa pun menjadi solid isometrik
bernada tiga. Pola starter: semua yang berubah ada di `S`, GSAP men-tween `S`,
`render()` menggambar ulang seluruh kanvas dari `S` + `tl.time()`. Gerak terus-
menerus (hujan, tetes di pipa, cincin berputar) dihitung dari `t`, dan
"acak" berasal dari `hash(i)` — tidak pernah `Math.random()`.

Teks yang digambar di kanvas tidak terbaca oleh pemeriksa DOM. Bila proyekmu
memeriksa teks lewat DOM (mis. safe zone), proyeksikan titik pin dengan
`iso.P()` dan taruh teksnya sebagai elemen HTML di atas kanvas.

## Varian gelap berlampu

Starter: `assets/starter-explainer-iso-gelap.html`. Hukum gaya tetap sama (proyeksi tetap, tiga nada,
perabot tinta, Isotype); yang berganti kulitnya. Cocok untuk penjara, bawah tanah, tambang, ruang
mesin, kota malam, atau topik kelam.

- **Latar hampir hitam** dengan gradien radial pelan + debu hangat melayang (dari `hash`), vinyet.
- **Batu dingin bertekstur**: ubin lantai satu per satu dengan nada sedikit berbeda (`hash`), nat
  bata digambar di dalam giliran kotaknya lewat `decal` + `line3(..., {now:true})` sehingga urutan
  painter tetap benar. Warna untuk engine selalu hex; `rgba()` merusak `rgb()` (dinding jadi hijau).
- **Cahaya = lapisan additive setelah `flush()`**: tiap obor/anglo/lentera satu gradien radial
  elips (rasio ≈ .62, mengikuti lantai isometrik) dengan `globalCompositeOperation='lighter'`.
  Kedip = jumlah tiga sinus dari `t` — deterministik. Api menyala satu per satu = "akumulasi".
- **Tinta dibalik**: `PAL.ink` terang, `PAL.paper` gelap, `haloText` di-override dengan halo gelap.
- **Fokus + konteks memudar ke abu GELAP**: `iso.col` di-override; target krem bawaan membuat
  close-up pucat. Cahaya non-subjek ikut diredupkan; subjek mendapat satu cahaya tambahan.
- Lentera yang dibawa tokoh adalah cahaya yang bergerak: subjek terlacak yang paling murah.

## Variasi (jauhi contoh starter)

- Struktur: satu gedung lantai demi lantai (turun menembus cutaway); dua
  papan dibandingkan; siklus (rute melingkar kembali ke awal dengan satu angka
  berubah tiap putaran).
- Pembuka: infografik jadi yang lalu terurai; satu ikon yang berlipat ganda
  sampai menjadi lanskap; pertanyaan sebagai judul isometrik di papan kosong.
- Penutup: stasiun tanpa jawaban (rute berhenti di pelat kosong bertanda
  tanya); legenda saja setelah papan memudar; close-up satu ikon dengan angka
  utuh kabur di belakangnya.

---

Gaya ini diturunkan dari *Isometric Infographic* di Lemo-Opuscar (LemoLab,
https://github.com/lemomo-ai/lemo-opuscar). Dokumen ini ditulis ulang; teks
aslinya berlisensi CC BY-NC 4.0 dan tidak disalin. Engine di starter berlisensi
MIT, header aslinya dipertahankan.
