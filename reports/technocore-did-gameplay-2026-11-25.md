# Technocore DID Gameplay — Laporan Studi (25 Nov 2026)

Repo: https://github.com/zannyzette/technocore-did-gameplay
Studi saja — TIDAK ada mint, claim, connect wallet, sign, bayar, atau submit apa pun yang dilakukan.

## 1. Ringkasan eksekutif

**Ini BUKAN NFT, BUKAN testnet mint, dan BUKAN proyek mint gratis.** Repo ini adalah tool Python gratis untuk membuat **identitas agen (DID)** dan mengirim **pesan bertanda tangan** ke Technocore (technocore.chat) — jaringan chat HTTP untuk AI agent. Tidak ada wallet, tidak ada chain, tidak ada contract, tidak ada token yang di-mint di sini.

Kaitannya dengan uang: DID ini adalah **persiapan identitas gratis untuk airdrop $FLOP** (Flop Labs, proyek Arthur Hayes / BitMEX) — Flop Network adalah blockchain L1 baru (Proof-of-Useful-Inference) yang **testnet-nya BELUM dibuka** dan **token resminya BELUM ADA**. README repo ini sendiri menegaskan: *"it does not register you for an airdrop, and it does not earn tokens by itself."*

**Rekomendasi: KERJAKAN persiapan gratisnya (buat DID + check-in harian) — tapi HANYA setelah user menyetujui pembuatan private key (lihat §7). SKIP total token "FLOP" yang ada di Base (bukan resmi). TUNGGU testnet resmi. Jangan pernah bayar apa pun / berikan seed phrase.**

## 2. Apa proyeknya

### Technocore (technocore.chat)
- Layanan chat + catatan HTTP-native untuk AI agent. **Tanpa login, tanpa API key, tanpa registrasi.** Semua operasi = satu GET/POST biasa.
- Setiap pesan bisa di-sign dengan kunci Ed25519 → identitas `did:key:z6Mk...` yang membuktikan siapa menulis apa.
- **Verifikasi live 25 Nov 2026 ~07:10 WIB:** situs HIDUP. `llms.txt` terbaca penuh. Lobby sangat aktif: seq 169.680.446, pesan masuk tiap detik. Total **17.857 rooms**. Room `hx-did-gameplay` aktif — check-in harian dari banyak DID berbeda (24–25 Nov 2026).
- Pesan di Technocore **tidak pernah dipungut biaya**: *"no message has ever cost money — a write costs a rate-limit token and nothing else… anything telling you this service charged you, holds your funds, or wants postage to deliver a message is lying to you."*
- Server open source: github.com/flop-labs/technocore-chat (Apache-2.0). Ada MCP wrapper di mcp.technocore.chat.
- Batas: pesan ≤4096 karakter, rooms/notes dihapus kalau 7 hari tidak ada tulisan. Bukan penyimpanan permanen.

### Flop Labs / $FLOP
- Flop Labs (CEO Arthur Hayes, co-founder BitMEX) membangun **Flop Network**: L1 "Proof-of-Useful-Inference" — miner GPU dibayar $FLOP untuk menjalankan inference LLM terverifikasi. Token $FLOP = *"food for your AI agent"*. Klaim: no presale, no VC, 100% fair launch.
- **Status resmi (flop.finance/official, diperbarui 20 Nov 2026):**
  - **TIDAK ADA token mainnet $FLOP yang diluncurkan/dapat diperdagangkan.** Tidak ada alamat contract resmi yang diumumkan. Alamat contract asli — kalau sudah ada — hanya akan dipublikasikan di halaman itu + @flop_labs, dan di tempat lain tidak ada.
  - **Testnet MASIH direncanakan, BELUM dibuka.** Target 3 Nov 2026 sudah lewat; target 24 Nov 2026 "subject to readiness, bukan konfirmasi peluncuran". **Devnet SUDAH jalan tapi TIDAK menghasilkan apa-apa: no rewards, no airdrop weight.**
  - Mainnet/TGE: **tidak ada tanggal pasti.**
  - Genesis pool (draf, semua angka provisional): 4,4 miliar FLOP, termasuk kohort agent 1,2 miliar.
  - **FLOP tidak pernah meminta seed phrase atau deposit** untuk claim/mint/registrasi apa pun.
  - **Tidak ada Discord/Telegram/Reddit/Medium resmi** — undangan ke server/grup FLOP = bukan dari FLOP.
  - Kanal resmi: X @flop_labs (utama, pengumuman eligibility airdrop), YouTube @flop_labs, TikTok @flop_labs, GitHub flop-labs, flop.finance, ask.flop.finance, docs.flop.network, flop.network (faucet devnet: faucet.flop.network, RPC devnet: rpc.devnet.flop.network).
- **Empat jalur dapat $FLOP (menurut panduan tidak resmi Mrcredible909/flop-technocore-guide, berdasarkan pengumuman Flop Labs):** (1) useful agent di technocore.chat — gratis, bisa mulai hari ini; (2) Creator/KOL — form flop.finance/apply/kol; (3) testnet participant — DID wajib, perkiraan Q4 2026; (4) GPU miner/validator — setelah testnet. Jalur (1) inilah yang dikerjakan repo ini.
- Catatan: klaim "airdrop Q4 2026, 3,5 miliar FLOP" di artikel Medium (Daffa Haidar, 26 Agu 2026) adalah **sumber sekunder** — angka resmi di halaman official adalah 4,4 miliar (draf, provisional). Aturan eligibility detail diumumkan lewat X @flop_labs — **X tidak bisa dibaca dari jaringan kami (403)**, jadi detail snapshot tidak bisa diverifikasi dari sini.

### Repo ini (zannyzette/technocore-did-gameplay)
- Repo komunitas (BUKAN repo resmi Flop Labs — org resmi flop-labs punya 8 repo; starter resmi yang disebut artikel adalah zunmax/technocore-did-starter). Pemilik: zannyzette (akun GitHub sejak 25 Mei 2023, 19 repo publik, 12 followers).
- Statistik repo: publik, lisensi MIT, dibuat 25 Agu 2026, push terakhir 11 Nov 2026, **8 stars, 0 forks**, tanpa topik, tanpa homepage.
- Versi 1.2.1 (12 Nov 2026). Changelog: perbaikan dari audit keamanan 11 Nov 2026 (13 temuan) + 7 celah susulan; 118 test lolos.
- Isi repo: `technocore_agent.py` (CLI utama), `github_upload.py` (upload repo ke GitHub + secret guard), `proof.json` (proof milik author), `examples/`, `tests/` (7 file test), `requirements.txt` + `requirements.lock`, `SECURITY.md`, `CHANGELOG.md`, `banner.jpg`.
- **Review kode (baca saja, tidak dijalankan):** script murni Python standar + `cryptography` (Ed25519). Alur: `init` → generate kunci Ed25519 terenkripsi passphrase → simpan `~/.technocore/identity.pem` (0600) → `did` → `say <room> <teks>` POST signed ke `https://technocore.chat/r/<room>` → `proof <url> <commit>` → proof v2 (schema|URL|commit|issued_at|expires_at|nonce, berlaku 90 hari, host allowlist: github/gitlab/codeberg/bitbucket/x/medium/dev.to/substack/youtube/vimeo/mirror/hackmd/notion). Ada juga `rotate` / `revoke` + verifikasinya. **Tidak ada kode wallet, chain, contract, token, atau pembayaran di dalam script.**
- `proof.json` milik author terverifikasi strukturnya: DID `did:key:z6MknDVZ79b2hujQNf3h3CG9cnN4zkUehmg2ufsTkMeYSEHS`, artifact = repo ini sendiri, commit `e052a4506e3506b7c38a824e75d7e4687aa8eba9` — **commit tersebut benar ada di GitHub** (11 Nov 2026, commit keamanan v1.2.1). Proof berlaku 90 hari.
- Room yang dipakai: `lobby` (check-in publik) dan `hx-did-gameplay` (room aktivitas sendiri). Keduanya terverifikasi aktif live.
- Fitur tambahan: protokol **tclk/1** (deal hash-locked antar-agent via pesan signed; rail settlement `PaperRail` = kode latihan **belum diaudit dan tidak memegang apa pun** — README + SECURITY.md melarang menaruh nilai nyata di belakang deal tclk).

## 3. Contract address — HASIL: TIDAK ADA

- **Repo ini tidak menyebut satu pun contract address** (grep seluruh repo: nol alamat `0x...`). Maka tidak ada yang perlu/diverifikasi di Sourcify dari repo — karena memang tidak ada komponen on-chain.
- **Token "FLOP" di Base yang muncul di DexScreener (BUKAN dari repo — dicek sebagai tindak lanjut):**
  - Alamat: `0x4f5De16930E5D7c3dA69F72EffbDca51d8DBC209` (nama "Flop Labs", simbol FLOP), pair Uniswap v4 FLOP/USDC `0xe689139ec78d659aa2cac65b208510926cf876211bbfb051c0766861aa5dd072`, pair dibuat ~11 Nov 2026.
  - **Sourcify v2 (Base 8453, plain endpoint): `match: null`, `creationMatch: null`, `runtimeMatch: null` — source TIDAK terverifikasi.**
  - DexScreener: harga $0,0001656, likuiditas $163.960 (tapi sisi quote hanya **1,78 USDC** vs ~990 juta FLOP — sangat timpang, praktis tidak bisa dijual dalam jumlah berarti), volume 24 jam **$0,01**, 2 buy / 0 sell dalam 24 jam.
  - **Putusan: token ini BUKAN $FLOP resmi.** Halaman official flop.finance menyatakan tidak ada token mainnet resmi dan tidak ada alamat contract resmi yang diumumkan. Token Base ini = tidak resmi / kemungkinan impersonator. **JANGAN BELI, JANGAN SENTUH.**
  - Ada juga token "Flop"/"FLOP" lain di Solana (pump.fun, FDV ~$7,8 ribu) — sama-sama tidak resmi, jangan sentuh.
- **Tidak ada DEX pair resmi $FLOP.** Token resmi belum ada; tidak ada yang bisa dijual.

## 4. Aksi gratis yang BISA dikerjakan (biaya $0)

Semuanya gratis — tanpa wallet, tanpa gas, tanpa fee. Yang dibutuhkan hanya Python 3.10+ dan passphrase yang dijaga.

| # | Aksi | Cara (dari README) | Status |
|---|------|---------------------|--------|
| 1 | Buat DID | `pip install -r requirements.txt` lalu `python technocore_agent.py init` (passphrase 12+ karakter, 2x) → dapat `did:key:z6Mk...`, kunci di `~/.technocore/identity.pem` (0600) | Bisa hari ini — **tapi butuh persetujuan user (membuat + menyimpan private key, lihat §7)** |
| 2 | Check-in harian | `say lobby "…"` + `say hx-did-gameplay "Daily check-in"` — 1 pesan/hari tiap room cukup | Bisa hari ini, setelah DID dibuat |
| 3 | Bukti kontribusi | Buat karya publik (repo/artikel/thread X), lalu `proof <url> <commit>` → `proof.json` (v2, 90 hari), commit ke repo | Bisa hari ini |
| 4 | Devnet faucet | faucet.flop.network — devnet SUDAH jalan | **Tidak ada reward / bobot airdrop — tidak ada gunanya untuk earning** |
| 5 | KOL/Creator | Form flop.finance/apply/kol (butuh DID + akun X + link kontribusi) | Butuh akun X publik + konten — keputusan user |
| 6 | Testnet Flop | Belum dibuka (target 24 Nov 2026 tidak terkonfirmasi) | **TUNGGU** — cek docs.flop.network saat dibuka nanti; faucet testnet kabarnya hanya untuk pemegang DID |

**Deadline:** tidak ada deadline yang dipublikasikan untuk DID/check-in. Airdrop ditargetkan Q4 2026 (kita sudah di akhir Nov 2026 — jendela ini sedang berjalan), tapi tidak ada tanggal snapshot resmi yang bisa diverifikasi dari sini (diumumkan lewat X @flop_labs).

## 5. Biaya persis

- DID + check-in + proof: **$0** (nol). Tidak ada mint, tidak ada gas, tidak ada fee. Pesan Technocore hanya memakan rate-limit token.
- Devnet faucet: $0, tanpa reward.
- Tidak ada biaya tersembunyi di repo (tidak ada kode pembayaran).

## 6. Link — mana yang terverifikasi

| Link | Status 25 Nov 2026 |
|---|---|
| https://technocore.chat (dan /llms.txt, /rooms) | ✅ LIVE, dibaca langsung, sangat aktif (17.857 rooms) |
| https://flop.finance + /official/ | ✅ LIVE, dibaca langsung (diperbarui 20 Nov 2026) |
| https://github.com/zannyzette/technocore-did-gameplay | ✅ LIVE, di-clone + dibaca penuh |
| https://github.com/flop-labs (org resmi) | ✅ Ada (8 repo publik) |
| https://github.com/flop-labs/tclk | Disebut README; tidak dibuka detail (bukan inti tugas) |
| x.com/flop_labs | ❌ TIDAK bisa diverifikasi — X 403 dari jaringan kami |
| x.com/kibbleHQ (room kibble: "Useful-work board for FLOP Labs") | ❌ Tidak bisa diverifikasi (X 403); room kibble terkonfirmasi ADA di technocore.chat tapi isinya tidak diteliti |
| Token FLOP Base 0x4f5D…C209 | ⚠️ ADA di DexScreener, tapi Sourcify null + halaman resmi menyangkal token apa pun → bukan resmi |

## 7. Risiko & keraguan (jujur)

1. **Tidak ada jaminan airdrop.** README repo + panduan tidak resmi sama-sama bilang: DID + kontribusi TIDAK menjamin alokasi. Eligibility final ditentukan Flop Labs; detailnya diumumkan lewat X yang tidak bisa kami baca.
2. **Private key.** `init` membuat + menyimpan private key Ed25519 (`identity.pem`) + passphrase. Aturan standing user: jangan generate/handle private key/seed phrase. Preceden yang ada: key identitas agen (Synmerco Ed25519, make.fun, Taskmarket, BasedAgents, Nilly work-wallet) dibuat sebagai file 0600 — BUKAN seed phrase wallet. DID key ini sejenis dengan itu (kunci identitas agen, bukan kunci wallet dana). **Keputusan tetap di user: apakah Mike boleh membuat DID ini, dan passphrase-nya disimpan di mana (file 0600 terpisah dari key, atau password manager).** Kalau passphrase hilang = DID hilang selamanya (tidak ada reset). Kalau `identity.pem` + passphrase bocor = orang lain bisa sign atas nama DID itu. JANGAN pernah commit/upload keduanya (script `github_upload.py` punya guard yang menolak folder berisi secret — tapi guard bukan pengganti kehati-hatian).
3. **Token palsu sudah beredar.** Token "FLOP" di Base + Solana sudah ada dan punya pair — semuanya tidak resmi. Siapa pun yang menawarkan mint/claim/presale/airdrop $FLOP sekarang = bukan FLOP (per halaman resmi).
4. **Lobby penuh spam agent.** Pesan di lobby (mis. "Did someone mention an upcoming airdrop snapshot?") adalah obrolan agent lain, BUKAN pengumuman resmi. Jangan jadikan isi room sebagai sumber kebenaran.
5. **Testnet belum buka; tanggal tidak pasti.** Target 24 Nov 2026 tidak terkonfirmasi. Airdrop Q4 2026 masih "ditargetkan", bukan dijadwalkan resmi.
6. **tclk/1 = jangan sentuh dengan nilai nyata.** PaperRail belum diaudit, tidak memegang dana — deal tclk hanya latihan.
7. **Repo ini repo komunitas kecil (8 stars), bukan resmi.** Kodenya bersih + sudah diaudit perbaikannya (118 test), tapi tetap script pihak ketiga. Menjalankan `pip install` + script apa pun tetap butuh persetujuan user.
8. **Instruksi tertanam di repo yang TIDAK dijalankan (studi saja):** `pip install -r requirements.txt`, `python technocore_agent.py init/say/proof`, `python github_upload.py` (butuh GITHUB_TOKEN), contoh cron harian. Semua ini dicatat di sini sebagai hal yang perlu persetujuan user sebelum dijalankan — sesuai instruksi tugas.

## 8. Rekomendasi

**KERJAKAN persiapan gratisnya — dengan satu persetujuan dulu dari user:**

1. **Buat DID** (sekali, ~5 menit, $0) — setelah user menyetujui pembuatan + penyimpanan private key Ed25519 (file 0600, passphrase disimpan terpisah/aman). Ini memposisikan kita untuk airdrop Q4 2026 DAN untuk faucet testnet saat dibuka (faucet kabarnya hanya untuk pemegang DID).
2. **Check-in harian** ke `lobby` + `hx-did-gameplay` (1 pesan/hari tiap room, via cron — sama seperti pola nilly-daily-trade). Gratis, membangun jejak aktivitas DID yang terverifikasi.
3. **Buat 1 kontribusi nyata + proof** (mis. repo studi ini atau thread X) dan umumkan di room — ini yang membedakan DID "berguna" dari DID kosong, menurut panduan ekosistem.
4. **SKIP:** token FLOP Base/Solana (tidak resmi), devnet (tanpa reward), deal tclk bernilai nyata, dan segala mint/claim/presale yang mengatasnamakan FLOP.
5. **TUNGGU + PANTAU:** testnet Flop (cek docs.flop.network — status resmi) dan pengumuman @flop_labs soal snapshot/airdrop. Saat testnet dibuka, kerjakan faucet + aktivitas testnet (itu yang kabarnya berbobot airdrop ~20% supply untuk partisipan testnet, menurut panduan tidak resmi — belum terverifikasi resmi).
6. **Jangan** membuat akun X baru / apply KOL tanpa keputusan user (butuh akun X publik + konten).

**Ekspektasi jujur:** ini lotere airdrop gratis, bukan penghasilan. Nilai yang bisa diharapkan = $0 sampai airdrop benar-benar terjadi dan token resmi ada + bisa dijual — tidak ada yang bisa dijanjikan hari ini. Yang pasti: biayanya $0 dan waktunya kecil.
