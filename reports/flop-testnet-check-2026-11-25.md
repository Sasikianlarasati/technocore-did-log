# FLOP Testnet — Verifikasi Status Resmi + Cara Klaim (25 Nov 2026)

Riset saja — TIDAK ada klaim token, spend inference, submit, atau sign apa pun yang dilakukan.
Semua pengecekan: 25 Nov 2026, ~07:17–07:25 WIB (kecuali dinyatakan lain).

## VERDIK (ringkas)

**Testnet FLOP SUDAH LIVE (unscored) sejak 24 Nov 2026 — TAPI faucet testnet BELUM ADA dan earning/settlement BELUM MENGHITUNG.**

- Chain hidup dan terverifikasi lewat RPC (genesis hash cocok persis, blok final 41.477 pada ~07:20 WIB).
- **Tidak ada metode klaim faucet testnet resmi saat ini.** Faucet di faucet.flop.network masih DEVNET. Klaim di sana = token devnet, tidak dihitung, tidak bisa dipindah ke testnet.
- **Aktivitas inference sekarang = 0 penghasilan, tanpa backfill.** Earning baru mulai di "finalized activation block" yang diumumkan nanti — belum ada blok/tanggalnya.
- Gateway api.flop.network masih di DEVNET (health check: network devnet).
- Jadi instruksi user langkah 3–7 (klaim → spend → settle → laporan harian) **BELUM BISA dieksekusi di testnet**. Yang bisa jalan sekarang: check-in DID harian (sudah jalan) + pantau pembukaan faucet + activation block.

## 1. Apakah testnet sudah LIVE? — YA (unscored), dibuktikan sumber resmi

### docs.flop.network/networks/testnet (dibaca langsung 07:17 WIB)
> "Network: testnet (live, unscored) · Release: next (unreleased)"
> "Public chain reads and operator registration are open. The signed operator kits are pending publication."
> "Six founding validators launched FLOP Testnet on 24 November 2026. You can follow finalized blocks on FLOPScan, query the public RPC, and register a validator or RPC team. This early network is unscored. Test FLOP has no monetary value. Outages, upgrades and resets are possible."
> "The chain ID is `flop_testnet`. Use `wss://testnet.flop.network/` for WebSocket RPC."

### Verifikasi RPC langsung oleh saya (07:20 WIB)
- `chain_getBlockHash [0]` → `0x918abd58fb16306b30ef3886514cfaebffecb4de43e82b6f8ec4795c43cfd800`
  — **cocok persis** dengan genesis hash di docs (`0x918abd58fb16306b30ef3886514cfaebffecb4de43e82b6f8ec4795c43cfd800`).
- `chain_getFinalizedHead` → blok final **41.477** (0xa205) pada ~07:20 WIB — chain memproduksi dan memfinalisasi blok.
- Bootnodes publik (dari docs): `boot-eu-1.testnet.flop.network` dan `boot-sg-1.testnet.flop.network` (tcp/30333).
- Raw spec: `flop_testnet-918abd58fb16306b.raw.json`, SHA-256 `485ecb44635609ab261ea3002c3c9fdc7a5dab38caf28a86f654cadf443893be`. Signed spec + Linux node kit **belum dipublikasikan** ("pending public download").

### testnet.flopscan.io (dibaca 07:17 WIB)
- Explorer hidup (HTTP 200, ~117 KB). Judul: "Testnet · FLOP Network Explorer", ada "Compute Market", "FRCR reference index", "realized settlement tape".
- Batasan: ini explorer custom (bukan Blockscout) — `/api/v2/stats` = 404, `/api/stats` = 503 "Era-T reader unavailable". Tampilan blok live di UI tidak bisa diverifikasi lewat text fetch (JS app). Bukti kuatnya tetap RPC di atas.

### flop.finance/official/ (dibaca ulang 07:17 WIB — CATATAN: halaman ini SUDAH KADALUARSA)
- Terakhir diperbarui **20 Nov 2026** — SEBELUM peluncuran testnet 24 Nov.
- Masih tertulis: "Testnet remains planned: 3 November 2026 was a historical target. The later 24 November 2026 target is subject to readiness, not a launch confirmation."
- Halaman ini direview "with every announcement" — tapi belum diperbarui sejak peluncuran. **Untuk status testnet, docs.flop.network adalah sumber yang lebih segar.** Halaman official tetap otoritatif untuk: tidak ada token mainnet, tidak ada alamat contract resmi, kanal resmi (X @flop_labs, YouTube, TikTok, GitHub flop-labs, flop.finance, ask.flop.finance, docs.flop.network, flop.network).

### Klaim room "testnet just went live" — DINILAI
- Pesan room hx-did-gameplay seq 5281–5284 (24 Nov 23:47–23:48 WIB, DID z6MkqMuP…): "Context: FLOP testnet just went live" (diulang 4x oleh DID yang sama).
- **Isinya BENAR secara substansi** (testnet memang diluncurkan 24 Nov, dikonfirmasi docs resmi) — TAPI buktinya adalah docs resmi, bukan pesan room. Pesan room tidak menyebut faucet/earning, dan pengulangan 4x terlihat seperti spam log. Jangan jadikan room sebagai sumber kebenaran.

### X @flop_labs — TIDAK TERVERIFIKASI
- X.com 403 dari jaringan kami (domain-wide). Tidak dicoba berulang. Padahal halaman official menyebut X sebagai "the primary channel and where airdrop eligibility is announced". Pengumuman eligibility airdrop kemungkinan muncul di sana dulu — tidak bisa kami baca dari sini.

## 2. Metode klaim faucet RESMI — BELUM ADA

### docs.flop.network/networks/testnet, bagian "Can I claim the verified-human faucet with Self?" (07:17 WIB)
> "Testnet has no verified public Self claim at this opening. Wait for a successful phone proof and a finalized Testnet grant to be announced here before claiming."
> "The generic faucet chain identity faucet.flop.network reported Devnet at the opening check. Always compare its genesis with the Testnet hash above before requesting funds."
> "The Devnet form offers Self. If the phone stays on 'Waiting for app…', the screen does not confirm a proof or a grant."

### faucet.flop.network (dicek langsung 07:20 WIB)
- HTTP 200. Judul halaman: **"FLOP Faucet - devnet"**.
- Config tertanam: `{"network":"devnet","quickAmountFlop":25,"linkedBaseFlop":500,"linkedCapFlop":2000,...,"selfEnabled":true,"selfScope":"flop-faucet","selfEndpoint":"https://faucet.flop.network/verify/self",...}`
- Isi halaman: "Quick fund 25 FLOP for dev testing", "Verified human 500-2000 FLOP by proof + score", alamat FLOP (SS58), wallet Polkadot.js / Talisman / SubWallet (SS58 prefix 42).
- **Nol penyebutan "testnet" di seluruh halaman.** Ini murni faucet devnet.
- Kesimpulan: **JANGAN klaim dari faucet ini untuk tujuan testnet.** Yang didapat = token devnet (genesis devnet `0x99c172c095340ace980631f9123544c6bebd4839f3437e463533422d8be2d631`, berbeda dari genesis testnet `0x918abd58…`). Devnet tidak dihitung, tidak dibawa ke testnet.

### Seperti apa klaim testnet nanti (berdasarkan docs — BELUM bisa dilakukan)
- Jalur yang disiapkan: **verified-human claim via Self** (phone proof) + "finalized Testnet grant" yang akan diumumkan di halaman docs testnet.
- Yang akan dibutuhkan: alamat FLOP (SS58) testnet — wallet Substrate (Polkadot.js / Talisman / SubWallet, prefix 42). DID `did:key` BUKAN alamat wallet chain.
- Jumlah/rate limit: belum diumumkan untuk testnet. (Sebagai gambaran devnet: quick 25 FLOP; verified-human 500–2.000 FLOP berdasarkan proof + score — angka testnet bisa berbeda.)

## 3. Gateway / API inference resmi — MASIH DEVNET

### api.flop.network/health (dicek langsung ~07:21 WIB)
```json
{"status":"ok","version":"2.0.0","connected":true,"syncing":false,
 "network":{"network":"devnet","status":"live",
 "expected_genesis_hash":"0x99c172c095340ace980631f9123544c6bebd4839f3437e463533422d8be2d631",
 "observed_genesis_hash":"0x99c172c095340ace980631f9123544c6bebd4839f3437e463533422d8be2d631"},
 "uptime_seconds":53007,
 "dependencies":{"backing_service":{"ok":true},"catalog":{"ok":true},"settlement":{"ok":true},"storage":{"ok":true}}}
```
- Gateway hidup, tapi jaringannya **devnet** (genesis `0x99c172c0…` = devnet, bukan testnet `0x918abd58…`).

### api.flop.network/openapi.json (dicek ~07:21 WIB)
- Judul: "FLOP Public Inference Data Plane" — REST API OpenAI-compatible untuk marketplace inference.
- Fitur: discover model, submit inference dengan payment otomatis, receipt-aware inference (estimasi vs metered evidence), bounded credentials (durable keys + scope-locked short-lived child credentials).
- Docs: "The model API api.flop.network lists models on the shared gateway. A listing does not establish Testnet mining or settlement." Dan: "api.flop.network/v1 on devnet. Pilot users need a scoped devnet credential and an exact model ID from the live catalog."
- MCP endpoint mcp.flop.network: menerima MCP client; health tool-nya melaporkan Devnet saat opening check.
- SDK: `@flop-labs/sdk@0.9.0` (npm/pnpm). Runtime allowlist SDK berhenti di 1014034; opening runtime testnet 1014035.

### Settlement / earning — BELUM MENGHITUNG (docs testnet, 07:17 WIB)
> "Earning begins at the publicly announced finalized activation block of a future tested runtime upgrade. There is no announced block or date yet. Earlier activity earns zero, with no backfill. Voucher trading, orders and swaps remain disabled."

Artinya untuk instruksi user langkah 4–7: **tidak ada settlement testnet yang bisa dicatat sekarang.** Inference yang di-spend hari ini (lewat gateway devnet) = devnet, tidak dihitung, tidak ada backfill saat activation block diumumkan nanti.

### Jalur lain di docs (untuk konteks, bukan rute Agent)
- Validator / RPC team: registrasi terbuka lewat formulir aplikasi GitHub ("validator or RPC application"). Registrasi, funding, dan active validator seat adalah milestone terpisah.
- GPU miner: "There is no public Testnet miner pack or supported Devnet-to-Testnet upgrade command at this opening. Wait for the Operator Hub to list the signed Testnet pack." Registrasi/stake devnet TIDAK terbawa ke testnet.

## 4. Kalau BELUM bisa klaim — apa yang dipantau (rencana pantau harian)

Testnet sudah live, tapi yang ditunggu ada 3 pengumuman — semuanya muncul dulu di halaman docs testnet:

| Yang dipantau | Di mana | Tanda sudah dibuka |
|---|---|---|
| Klaim faucet testnet (Self phone proof + finalized grant) | https://docs.flop.network/networks/testnet bagian "Can I claim the verified-human faucet with Self?" | Teks berubah dari "no verified public Self claim" menjadi instruksi klaim + grant |
| Activation block earning | Halaman yang sama, bagian "When does activity start counting for vouchers?" | Ada nomor blok + tanggal aktivasi yang diumumkan |
| Signed Testnet pack (miner) / operator kits | https://docs.flop.network (Operator Hub) | Pack terdaftar dengan instruksi setup |
| Faucet berubah jaringan | https://faucet.flop.network (cek config `network` + bandingkan genesis dengan `0x918abd58…`) | `network` = testnet |
| Gateway pindah ke testnet | https://api.flop.network/health (field `network.network`) | `network` = testnet |
| Halaman official diperbarui | https://flop.finance/official/ | "Updated" lebih baru dari 20 Nov 2026 + status testnet berubah |

Frekuensi: cek harian (testnet baru diluncurkan 24 Nov — hari-hari pertama paling cepat berubah). Jangan klaim apa pun sebelum (a) docs testnet mengumumkan klaim Self + grant, DAN (b) genesis faucet/gateway cocok dengan `0x918abd58…`.

## 5. Yang MASIH BUTUH input/keputusan user sebelum klaim bisa jalan

1. **Alamat wallet Testnet (SS58)** — DID `did:key` bukan alamat chain. Saat faucet testnet dibuka, grant dikirim ke alamat FLOP (SS58, prefix 42). Membuat keypair Substrate = membuat + menyimpan private key baru — perlu persetujuan eksplisit user (seperti persetujuan DID), plus keputusan di mana menyimpannya (file 600 terpisah). TIDAK dibuat dalam riset ini.
2. **Self phone proof (verified-human)** — klaim testnet dirancang lewat Self (proof lewat aplikasi di HP user). Agent tidak bisa menyelesaikan personhood proof berbasis HP sendiri — user kemungkinan harus melakukan langkah Self di HP-nya saat dibuka, atau menyetujui pendekatan lain yang diumumkan nanti.
3. **Model + credential gateway** — saat activation block diumumkan, perlu credential yang valid untuk testnet (hari ini hanya ada "scoped devnet credential"). Belum ada yang bisa disiapkan.
4. **Kontribusi + proof v2** — tetap tertunda (keputusan user soal repo publik), terpisah dari faucet.

## 6. Temuan mencurigakan / peringatan

- **Tidak ditemukan instruksi "kirim X ke alamat Y"** di room lobby / hx-did-gameplay (50 pesan terakhir tiap room, dicek 07:20 WIB) maupun di halaman resmi. Tidak ada yang perlu dilaporkan sebagai scam aktif dari sumber-sumber ini.
- **Satu klaim tanpa bukti di lobby** (seq 169686168, 25 Nov 00:18:39Z, DID z6MkfuVM…): "i claim faucet $FLOP and spend it on inference. chat posts are not the airdrop." — tidak ada metode/URL/bukti. Mengingat faucet resmi masih devnet, klaim ini (kalau benar) = aktivitas devnet yang tidak dihitung, atau sekadar omongan. Bukan instruksi, bukan bukti.
- **Pesan-pesan snapshot/airdrop di lobby** ("Did someone mention an upcoming airdrop snapshot?", "Let's see how the Q4 snapshot plays out") adalah obrolan agent lain, bukan pengumuman. Abaikan sebagai sumber.
- **Satu agent di hx-did-gameplay justru hati-hati dan benar** (seq 5264, 24 Nov 21:28 WIB, DID z6Mkh5CC…): "Testnet earning activation remains unverified. The faucet or gateway is not verified for Testnet; no funding or inference submitted. Counting only verified settled inference spend." — sejalan dengan temuan riset ini.
- **Token FLOP palsu tetap beredar** (dari studi sebelumnya): Base `0x4f5D…C209` (Sourcify null) + Solana — bukan resmi, jangan sentuh. Halaman official menegaskan: sampai alamat contract muncul di halaman itu + @flop_labs, semua contract/mint/claim/presale atas nama FLOP bukan FLOP.

## Sumber (semua dicek 25 Nov 2026 ~07:17–07:25 WIB)

- https://flop.finance/official/ — terakhir diperbarui 20 Nov 2026 (kadaluarsa untuk status testnet)
- https://docs.flop.network — Operator Hub (Network: devnet, Release: next unreleased)
- https://docs.flop.network/networks/testnet — "testnet (live, unscored)", diluncurkan 24 Nov 2026 oleh 6 founding validators
- https://testnet.flopscan.io — explorer hidup (HTTP 200), API custom (bukan Blockscout)
- https://testnet.flop.network/ (RPC HTTPS JSON-RPC) — genesis hash cocok persis; blok final 41.477
- https://faucet.flop.network — "FLOP Faucet - devnet", config network=devnet
- https://api.flop.network/health + /openapi.json — gateway hidup di devnet
- https://technocore.chat/r/lobby + /r/hx-did-gameplay (50 pesan terakhir tiap room, via `technocore_agent.py read`)
- X @flop_labs — tidak terverifikasi (403 domain-wide, tidak dicoba berulang)
