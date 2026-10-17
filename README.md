<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Gallery — Another Visual</title>

<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=Playfair+Display:wght@500;600;700&display=swap" rel="stylesheet">

<style>
:root {
  --bg: #0b0c0e;
  --panel: #131518;
  --text: #f5f3ee;
  --muted: #96999e;
  --accent: #d6b783;
  --line: rgba(255,255,255,.10);
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

img, video, .photo, .lightbox {
  -webkit-user-select: none;
  user-select: none;
  -webkit-touch-callout: none;
}

img, video {
  -webkit-user-drag: none;
}

html { scroll-behavior: smooth; }

body {
  background: var(--bg);
  color: var(--text);
  font-family: 'DM Sans', sans-serif;
}

a { color: inherit; text-decoration: none; }

nav {
  position: sticky;
  top: 0;
  z-index: 10;
  height: 76px;
  padding: 0 7%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: rgba(11,12,14,.88);
  backdrop-filter: blur(18px);
  border-bottom: 1px solid var(--line);
}

.logo {
  font-size: 17px;
  font-weight: 700;
  letter-spacing: 3px;
}

.logo span { color: var(--accent); }

.nav-label {
  color: var(--muted);
  font-size: 11px;
  letter-spacing: 2px;
  text-transform: uppercase;
}

.hero {
  padding: 100px 7% 75px;
  position: relative;
  overflow: hidden;
}

.hero::after {
  content: "";
  position: absolute;
  width: 400px;
  height: 400px;
  right: -150px;
  top: 0;
  background: radial-gradient(circle, rgba(214,183,131,.09), transparent 70%);
  pointer-events: none;
}

.eyebrow {
  color: var(--accent);
  font-size: 11px;
  letter-spacing: 4px;
  text-transform: uppercase;
  margin-bottom: 24px;
}

h1 {
  font-family: 'Playfair Display', serif;
  font-size: clamp(48px, 8vw, 100px);
  line-height: 1.05;
  font-weight: 500;
  letter-spacing: -2px;
}

h1 em {
  color: var(--accent);
  font-weight: 500;
}

.hero-bottom {
  margin-top: 32px;
  display: flex;
  align-items: end;
  justify-content: space-between;
  gap: 24px;
}

.hero p {
  max-width: 430px;
  color: var(--muted);
  line-height: 1.9;
  font-size: 14px;
}

.photo-count {
  color: var(--accent);
  font-size: 12px;
  letter-spacing: 2px;
  white-space: nowrap;
}

.gallery-section { padding: 0 7% 100px; }

.toolbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 22px;
  margin-bottom: 30px;
  padding: 22px 0;
  border-top: 1px solid var(--line);
  border-bottom: 1px solid var(--line);
}

.toolbar-title {
  font-size: 12px;
  letter-spacing: 2px;
  text-transform: uppercase;
}

.filters {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.filter {
  cursor: pointer;
  border: 1px solid var(--line);
  background: transparent;
  color: var(--muted);
  border-radius: 30px;
  padding: 10px 17px;
  font: inherit;
  font-size: 12px;
  transition: .25s;
}

.filter:hover,
.filter.active {
  color: var(--bg);
  background: var(--accent);
  border-color: var(--accent);
}

/* GALERI FOTO RASIO 1:1 */
.gallery {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 15px;
  align-items: start;
}

.photo {
  position: relative;
  overflow: hidden;
  background: var(--panel);
  cursor: pointer;
  border-radius: 3px;
  aspect-ratio: 1 / 1;
  min-width: 0;
  animation: reveal .65s ease both;
}

.photo.tall,
.photo.wide {
  grid-row: auto;
  grid-column: auto;
}

.photo img, .photo video {
  pointer-events: none;
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  transition: transform .7s cubic-bezier(.2,.7,.2,1), filter .5s;
}

.photo::after {
  content: "";
  position: absolute;
  inset: 0;
  background: linear-gradient(to top, rgba(0,0,0,.85), transparent 55%);
  opacity: .8;
  transition: .3s;
  pointer-events: none;
}

.photo:hover img, .photo:hover video {
  transform: scale(1.06);
  filter: brightness(.8);
}

.photo-download {
  position: absolute;
  z-index: 3;
  top: 14px;
  right: 14px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 7px;
  min-height: 36px;
  padding: 0 13px;
  border: 1px solid rgba(214,183,131,.9);
  border-radius: 24px;
  background: rgba(11,12,14,.82);
  color: var(--accent);
  font: inherit;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: .5px;
  -webkit-tap-highlight-color: transparent;
  backdrop-filter: blur(8px);
  cursor: pointer;
  transition: background .25s, color .25s, transform .25s;
}

.photo-download:hover,
.photo-download:focus-visible {
  background: var(--accent);
  color: var(--bg);
  transform: translateY(-1px);
}

.photo-info {
  position: absolute;
  z-index: 2;
  left: 20px;
  right: 20px;
  bottom: 20px;
  display: flex;
  justify-content: space-between;
  align-items: end;
  gap: 12px;
}

.photo-info h3 {
  font-family: 'Playfair Display', serif;
  font-size: 20px;
  font-weight: 500;
}

.photo-info p {
  margin-top: 5px;
  font-size: 10px;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: #d5d2cb;
}

.zoom {
  width: 34px;
  height: 34px;
  flex-shrink: 0;
  display: grid;
  place-items: center;
  border: 1px solid rgba(255,255,255,.5);
  border-radius: 50%;
  font-size: 18px;
  transition: .3s;
}

.photo:hover .zoom {
  background: var(--accent);
  border-color: var(--accent);
  color: var(--bg);
}

.empty {
  display: none;
  color: var(--muted);
  text-align: center;
  padding: 60px 0;
}

footer {
  padding: 30px 7%;
  border-top: 1px solid var(--line);
  display: flex;
  justify-content: space-between;
  gap: 15px;
  flex-wrap: wrap;
  color: var(--muted);
  font-size: 11px;
  letter-spacing: 1px;
}

footer span { color: var(--accent); }

/* LIGHTBOX */
.lightbox {
  position: fixed;
  inset: 0;
  z-index: 100;
  display: none;
  align-items: center;
  justify-content: center;
  padding: 35px;
  background: rgba(0,0,0,.95);
}

.lightbox.open { display: flex; }

.lightbox-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 20px;
  width: min(100%, 1100px);
  max-height: 92vh;
}

.lightbox img, .lightbox video {
  -webkit-user-drag: none;
  pointer-events: auto;
  max-width: 100%;
  max-height: calc(85vh - 65px);
  object-fit: contain;
}

.lightbox-download {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
  min-height: 46px;
  padding: 0 24px;
  border: 1px solid var(--accent);
  border-radius: 30px;
  background: var(--accent);
  color: var(--bg);
  font: inherit;
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 1px;
  white-space: nowrap;
  cursor: pointer;
  transition: .25s;
  -webkit-tap-highlight-color: transparent;
}

.lightbox-download:hover {
  background: transparent;
  color: var(--accent);
}

.close {
  position: absolute;
  top: 22px;
  right: 28px;
  color: white;
  border: 0;
  background: none;
  font-size: 36px;
  cursor: pointer;
}

@keyframes reveal {
  from { opacity: 0; transform: translateY(15px); }
  to { opacity: 1; transform: translateY(0); }
}

/* RESPONSIVE */
@media (max-width: 760px) {
  nav { height: 65px; padding: 0 5%; }
  .hero { padding: 75px 5% 50px; }
  .hero-bottom { align-items: start; flex-direction: column; }
  .gallery-section { padding: 0 5% 65px; }

  .gallery {
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 9px;
  }

  .photo-info { left: 11px; right: 11px; bottom: 12px; }
  .photo-download { top: 8px; right: 8px; min-height: 31px; padding: 0 10px; font-size: 10px; }
  .photo-info h3 { font-size: 15px; }
  .photo-info p { font-size: 9px; letter-spacing: 1px; }
  .zoom { width: 27px; height: 27px; font-size: 15px; }
  .toolbar { align-items: start; flex-direction: column; }
}

@media (max-width: 420px) {
  .gallery { gap: 8px; }
  .photo-info h3 { font-size: 13px; }
  .photo-info p { font-size: 8px; letter-spacing: .5px; }
  .photo-download { min-height: 28px; padding: 0 8px; font-size: 9px; }
  .lightbox { padding: 15px; }
}
</style>
</head>

<body>

<nav>
  <a href="#" class="logo">VISUAL<span>.</span>ARCHIVE</a>
  <div class="nav-label">Another Visual</div>
</nav>

<header class="hero">
  <div class="eyebrow">A collection of moments</div>
  <h1>Moments<br>in <em>Frames.</em></h1>

  <div class="hero-bottom">
    <p>
      Setiap foto menyimpan cerita, perspektif, dan momen
      yang tidak akan terulang. Sebuah arsip visual dari
      apa yang saya lihat dan rasakan.
    </p>
    <div class="photo-count" id="count">00 PHOTOGRAPHS</div>
  </div>
</header>

<main class="gallery-section">
  <div class="toolbar">
    <div class="toolbar-title">Selected Works / Gallery</div>
    <div class="filters">
      <button class="filter active" data-filter="all">Semua</button>
    </div>
  </div>

  <div class="gallery" id="gallery"></div>
  <div class="empty" id="empty">Belum ada foto dalam kategori ini.</div>
</main>

<footer>
  <div>© 2026 <span>Another Visual</span></div>
  <div>CAPTURED WITH INTENTION.</div>
</footer>

<div class="lightbox" id="lightbox" role="dialog" aria-modal="true" aria-label="Pratinjau media">
  <button class="close" id="close" aria-label="Tutup">&times;</button>
  <div class="lightbox-content" id="lightbox-container">
    <button class="lightbox-download" id="lightbox-download">Download</button>
  </div>
</div>

<script>
// DAFTAR FOTO DAN VIDEO GOOGLE DRIVE (MENGGUNAKAN TAUTAN LENGKAP ASLI)
const photos = [
  { url: "https://drive.google.com/file/d/1HmYYsUgbQbr0ASooF0gHmnWElC1aeO9c/view?usp=drive_link", title: "Visual 01", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1k9740f8wNXwhYg-pe6IH2E_tB1MwzQWE/view?usp=drive_link", title: "Visual 02", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1q0kFW1qvjqLsNcER0y75rD7PZiCD6mFE/view?usp=drive_link", title: "Visual 03", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1sv_ZDSXu1ih1j1Wl7Nb6ZDJ1IJG54m1q/view?usp=drive_link", title: "Visual 04", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1C8hOeBxOWPYtGri0w07Cxy7IJKzl1rDH/view?usp=drive_link", title: "Visual 05", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1fCnKr1Es6W1e25B6-VaSvFDSdAWf5er6/view?usp=drive_link", title: "Visual 06", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1PcK0TA2xX9HW8yXiYZ247eQPLwnyxJAY/view?usp=drive_link", title: "Visual 07", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1BD7Yxi1fvv3MDJPhe8vMr_rGX_-V90VD/view?usp=drive_link", title: "Visual 08", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1GjWFiSvkKeJXq5_QREs2qd5EuEFeMG0i/view?usp=drive_link", title: "Visual 09", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1h302-hRw83CSYYX2i7D7HyiWFojiPywV/view?usp=drive_link", title: "Visual 10", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Yj3Bnl2kCr6dcveB_EQq1B2pgedWwav0/view?usp=drive_link", title: "Visual 11", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1vLBdLCl1sb-plg4MXR_EDsS7M3mLVNS1/view?usp=drive_link", title: "Visual 12", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1yDFcjDu3INMdjnHPeOOJiAfuA-bDereH/view?usp=drive_link", title: "Visual 13", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1hRDaz12uwksQecRfDmBXHfLhDdyhsR6q/view?usp=drive_link", title: "Visual 14", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1fOoP_2-mV-EpjEGGwi8D00uNbyCydpvV/view?usp=drive_link", title: "Visual 15", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/198R2s_UCWUKHElya0_E2fPtwkwt19CRP/view?usp=drive_link", title: "Visual 16", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/15gk9lqpKyseiFHJJb_ya-JOLZKIE0PzR/view?usp=drive_link", title: "Visual 17", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1KUTJKzcoZZ4I4TiKkhHfmDU0Dn00OvhY/view?usp=drive_link", title: "Visual 18", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1kjGIdT1dJRqpk5yf_nweVWM68kwp04Vp/view?usp=drive_link", title: "Visual 19", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1pT5OF6yCY3eEYEtSKoVQW0TpTgHLrG-f/view?usp=drive_link", title: "Visual 20", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/12-KjEWyHWu_5SiECyKhdtumx0BvXITqd/view?usp=drive_link", title: "Visual 21", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/17hZ8YrWGZLaiXsk-hbey2OdWwNB0z3gK/view?usp=drive_link", title: "Visual 22", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Z9FY_uRRwzAlGEQA8IChyQGF-VXf5Rw5/view?usp=drive_link", title: "Visual 23", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Qz0zzaXNTFMkHbK0FvV-PbjalHB6bwQ-/view?usp=drive_link", title: "Visual 24", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1FfpVMOkJIiKPoLQ1tvpE4-69TKGHjNVP/view?usp=drive_link", title: "Visual 25", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1XzTyDjgvPL3aOuqnGYN9ENnmA-6ED-1a/view?usp=drive_link", title: "Visual 26", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1LWk1UNwq-Cao_QzqLBnSl2stwsOxyjSB/view?usp=drive_link", title: "Visual 27", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1NdruPZh63O6-NgEMFPHY2hC-RdlDAHDR/view?usp=drive_link", title: "Visual 28", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1K1YI2XyXWWtmmndJumXmbo_7_quT7Ef7/view?usp=drive_link", title: "Visual 29", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1CfE9zdORjJR23eZy7BcuY3kZ7RBUkcoR/view?usp=drive_link", title: "Visual 30", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1bo2kBLThPIuIfl9ld1-DyJkAOUhOKQ6H/view?usp=drive_link", title: "Visual 31", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1jHtY2hNubzYp4fENTb64od6-I143dm-5/view?usp=drive_link", title: "Visual 32", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1jnJ_i5Apgq-7HQIS5FrmLAXJcUlCYd5W/view?usp=drive_link", title: "Visual 33", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/12xDeeMvKUZB_1ZQdT5CJVCEf0NYjv8Gf/view?usp=drive_link", title: "Visual 34", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1POWi6Qvr1pHl0PR_P-eUK6tfUzksMhIK/view?usp=drive_link", title: "Visual 35", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Z9JQINBDrBxxlpQsCrATPv9n_-ZV-eC7/view?usp=drive_link", title: "Visual 36", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1_nuOFCXFcMLZfKakxa1uG7nUY0XXSu7N/view?usp=drive_link", title: "Visual 37", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1TzFz6hcg5AxF2Bwb61j1Y2RUXWPNPb1M/view?usp=drive_link", title: "Visual 38", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1wxnUTl1g4HbQ9ZSwgc6mkTJkQ6S2c_U5/view?usp=drive_link", title: "Visual 39", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1s3S-1jepwIHV_dfv4DW9DZjj3tEZPoEZ/view?usp=drive_link", title: "Visual 40", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1bpK-aVRn_133SzARaGp3XO8Op4YhPemd/view?usp=drive_link", title: "Visual 41", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1jqy2HehaX1aA7C8V5IKXKhBK3JaCmaAU/view?usp=drive_link", title: "Visual 42", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1dUG_BrbvaCD5gX4XmwIC3zoh3YRZ2Rl0/view?usp=drive_link", title: "Visual 43", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1aYR17oZGmaTcXn5tCl_uESThc657RLY2/view?usp=drive_link", title: "Visual 44", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1PWmtSgZJhnZLPdgs-ii1_3tSw-KrGKWe/view?usp=drive_link", title: "Visual 45", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1bFV0K2ernyTLS7MFkkxAHSoke37lmEiM/view?usp=drive_link", title: "Visual 46", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1qFu2uvmHzbLJ2tGlzmCnfH2ygVfw3vOn/view?usp=drive_link", title: "Visual 47", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1aXABbCkilEjfEeWRdcJR5AsAI8np-X3n/view?usp=drive_link", title: "Visual 48", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1IeW9UGpFlI_5-U4zL0eIkFcaFbBEWPLI/view?usp=drive_link", title: "Visual 49", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1wubGfZwXGT9oF5SKf4W3SvKMMxf3tnPn/view?usp=drive_link", title: "Visual 50", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1drPJL2--LLKsTekVmu4p_HAj384J-1dM/view?usp=drive_link", title: "Visual 51", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Bx7ugP0xOQmFDZ8vlur5a76xlrsOOTUB/view?usp=drive_link", title: "Visual 52", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1VpDNMNHQSZCS0z3_gypZoIVOdaDYQbUt/view?usp=drive_link", title: "Visual 53", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1h3sLy_fIbVNTm2lD7nJ3PXNmRf6HUjNi/view?usp=drive_link", title: "Visual 54", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1fz-hHjXe4zvVNUrFBIJ9SgvOnkMjlzBW/view?usp=drive_link", title: "Visual 55", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1__SSvKH3U6Fo0D1T7ukqooivGiZEEmJb/view?usp=drive_link", title: "Visual 56", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1ajDRhS66byjj0YrWMZlar_YVLc296HCf/view?usp=drive_link", title: "Visual 57", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1PgTxkOqVc8D86m96WdB_gU4DKxBnCPKN/view?usp=drive_link", title: "Visual 58", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1-vokmAGcU92GW6DekdX3A8hoEh58rGgM/view?usp=drive_link", title: "Visual 59", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1OXbKG_IyWl2EoANX5YrFDQldzPOTtZOM/view?usp=drive_link", title: "Visual 60", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/13FH6hqIJWEVp7ZexsjV-g1-NJWW8bjhT/view?usp=drive_link", title: "Visual 61", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1oMOnF4TmEdh7OZ2hBRBSDmMC4d1tNpB-/view?usp=drive_link", title: "Visual 62", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1digFzGCRO143qZiEzVy_fjLD6qfGvF40/view?usp=drive_link", title: "Visual 63", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1OgfNcUoO9epDH_1i8Bz5rNeakikyC35s/view?usp=drive_link", title: "Visual 64", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1gDG6GbZgjysDN7zxrcmXNBLbOhc_VEDu/view?usp=drive_link", title: "Visual 65", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1R66g8qznOCQKO7XydQ8JVmYUlNbGUvbB/view?usp=drive_link", title: "Visual 66", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1iaYcqKXRvEc346rYUzBAQAqFGE8XZPap/view?usp=drive_link", title: "Visual 67", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1xNVL_nQcN0sWWL04SqK448TMfTAGYlTf/view?usp=drive_link", title: "Visual 68", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1LfL3r-vRMEDNg631wN9eUvqWMeLMZj2G/view?usp=drive_link", title: "Visual 69", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Zos2Dy8anlUSUtu5Q4WAI-FReY_YJ0H4/view?usp=drive_link", title: "Visual 70", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1yAmW-oYSu50-VqbiW36IhrbvuVk67koK/view?usp=drive_link", title: "Visual 71", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1-m8I3viX_VDyVYBq7EW8k-K7qM_QF3e7/view?usp=drive_link", title: "Visual 72", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1CNg9i-hZzu9Q3iFUcd8F_hWKAbeFAlbp/view?usp=drive_link", title: "Visual 73", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/14JuOh6FjFESWz13TDXwGdLSjc3V5U2lT/view?usp=drive_link", title: "Visual 74", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1AdMWWjqm9-p00kNLoP19amF1cyRs3vmf/view?usp=drive_link", title: "Visual 75", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/13RQ3utaGxJvhqMX1H3pl7zagezNXJzFS/view?usp=drive_link", title: "Visual 76", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1x1RjOzTbrZEoPfCE3CJ4ghwB8HVV1GUp/view?usp=drive_link", title: "Visual 77", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1fKkGRpkyHfJ0EbwCFp7n9aUoYoFKJcTP/view?usp=drive_link", title: "Visual 78", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1aVZOCx_f4KZI-bVcOeAjsoH-W_LPirkM/view?usp=drive_link", title: "Visual 79", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1p9AYDkltEJJvwdSMqPO4owPTPTKkQBaW/view?usp=drive_link", title: "Visual 80", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1MNAWE5BbkoGcWpQ_1jWh6FUMkdZyWc27/view?usp=drive_link", title: "Visual 81", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/17-O87sEF9eGLBi3368NUzBGK5e9Cb-4b/view?usp=drive_link", title: "Visual 82", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Tvo21lp5z5cjchf4buoRbUAA-9l6obUR/view?usp=drive_link", title: "Visual 83", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1LEg3RKBIDJXbcfk2LwyzA0Wfgs_rOib5/view?usp=drive_link", title: "Visual 84", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1uHlDxeD-yzU_C-0Y2sKqb9EfjOQ2CPdk/view?usp=drive_link", title: "Visual 85", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1ta2TTizbg3p-dLhnA4sDfnA3hj0N-mCO/view?usp=drive_link", title: "Visual 86", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1RVZ3IAeve8seotz6G_kKvFwRjTptdhma/view?usp=drive_link", title: "Visual 87", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1WLpoQnyEWF9p9KPkhiAQo3tK_Da8Zl8t/view?usp=drive_link", title: "Visual 88", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1iV-9pK3k35dmbBdUUb2tHQEOIUpu5zNT/view?usp=drive_link", title: "Visual 89", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1CB3yO5bSl6bIiVsljaMptGuRwnzl08HI/view?usp=drive_link", title: "Visual 90", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1wjE4c1ZeL1gi1NIZ9v6TC5bRWDiYpahc/view?usp=drive_link", title: "Visual 91", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/11HjSH0RI31weQzUQEUAb2gnzFtG-XfLD/view?usp=drive_link", title: "Visual 92", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1kl6CYHyHqDIr75xTxKl_IkLfUia1r5dF/view?usp=drive_link", title: "Visual 93", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/12RQ19rASmdJu756s4UXPgH1fN1mMmxWt/view?usp=drive_link", title: "Visual 94", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1tHWRdjBKw3t-bU-d-pEsNEaKmBL39mCY/view?usp=drive_link", title: "Visual 95", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1cw2qiMa4-x_WcIRXRl-OFO_69Z0UUjio/view?usp=drive_link", title: "Visual 96", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1nAw75mtfm9hyPStdmsjOw5DF2BptHtEM/view?usp=drive_link", title: "Visual 97", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1vx7_9wLlOeusJntHHVJ7SpYrfrRNyZiD/view?usp=drive_link", title: "Visual 98", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1749TsJTf9hq_vuDg1o0ACgMn1XJZn5cS/view?usp=drive_link", title: "Visual 99", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1J3ar_QjAOGYsiCDtP31MJwRDUIEXlWla/view?usp=drive_link", title: "Visual 100", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1dFBaUHrin-PNNFkpwbRPxT4vtnZ2LjTu/view?usp=drive_link", title: "Visual 101", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1bDlGnY02D2SrMQHAhaZKdbKtMjVpPyLV/view?usp=drive_link", title: "Visual 102", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1hLJ5DxZPJ_rTiZtL1p8MAr8lHusXffHq/view?usp=drive_link", title: "Visual 103", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/15miQxSZjo0-9NeRCgdq2jHhlSdanVNth/view?usp=drive_link", title: "Visual 104", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1nQ35_6bkry47lMafvzIKCeKl5r7DkmiM/view?usp=drive_link", title: "Visual 105", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1XHKl2rOAm7ChoXuJIo1P5dj5Z3icxY7Y/view?usp=drive_link", title: "Visual 106", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1yRbcT3DUYc7x3CovksuJCYG-hQ2l_d_O/view?usp=drive_link", title: "Visual 107", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1eUfrq3wmfl2egYMUuTu1WdWma_fO1vjJ/view?usp=drive_link", title: "Visual 108", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1LBR4c8auW3mlqReV2E1Rky4tBpCEYEo6/view?usp=drive_link", title: "Visual 109", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1tL7dNOgok9---DDQG9PbMshItY0mMuyV/view?usp=drive_link", title: "Visual 110", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1d_BleG4i2taP2hTFeMN_PIkwByERaaWv/view?usp=drive_link", title: "Visual 111", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/10Uha3_hEthjrJad46Rzw3_GWY_repgJp/view?usp=drive_link", title: "Visual 112", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1y_NmO0nnWmICc90iYKn6MURBnioy4GC2/view?usp=drive_link", title: "Visual 113", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1VxY5P2K4ai8uwCPs0KtnoVpaQKeohYvd/view?usp=drive_link", title: "Visual 114", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1iLXY3yMic9sh5uQlugKwqY2uzKhtdMTD/view?usp=drive_link", title: "Visual 115", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1TxtIMQ0q4tepivLxzW6KzXaKBLmzfPMp/view?usp=drive_link", title: "Visual 116", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1DizsJVmyFkg0-SY8iMYgwHGPlme9krIm/view?usp=drive_link", title: "Visual 117", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1g3R4SgQffKQPIb1-vDO5tL6YQ-v1SQsT/view?usp=drive_link", title: "Visual 118", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1wLoOgf_ToM30O62Kii3klm19Y1PL0uqe/view?usp=drive_link", title: "Visual 119", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1zPFFbGOIjQRSQVzU8E1FJdJXssWGN5cN/view?usp=drive_link", title: "Visual 120", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1OjLTz0aLuLDT13pDHqNipRVCxCBZfLLv/view?usp=drive_link", title: "Visual 121", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1_Rk08tDn2zIklOxQI4uZiJlAeuXAcNDZ/view?usp=drive_link", title: "Visual 122", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1CwT73Kl_mSKn2juMDHufoDTNw70iP5v1/view?usp=drive_link", title: "Visual 123", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/11k_7pU5S03wPwbdYWMSBhZ9z8awqTEEx/view?usp=drive_link", title: "Visual 124", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1r9_Ej1JwoCoWW-Ei99lIq3wS7AGYHyUv/view?usp=drive_link", title: "Visual 125", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1v1CBCjj7xVmPN5x8_m74htrA-M-Kn30L/view?usp=drive_link", title: "Visual 126", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1uWXXvCpQEgh8Ji_dL-X4_a0QSGbdosGa/view?usp=drive_link", title: "Visual 127", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1KPi9-xx3y8aWP5x14bc0GTJS21tHRYua/view?usp=drive_link", title: "Visual 128", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1zcAGS4pFLzUjUv0-0ql_UYR6x7W_loae/view?usp=drive_link", title: "Visual 129", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Ui3kaF5DhPEExG6M0ije9ZXkHPWgrM0m/view?usp=drive_link", title: "Visual 130", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1uogZ5IzIJmboybJdaqFsjdksRdheSX6r/view?usp=drive_link", title: "Visual 131", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Xg-pObyKG1pQiNrGfYDUxGa76nFREnGM/view?usp=drive_link", title: "Visual 132", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1UTv45mRfT7pOZvwIuNuS50f0pjbhE0H9/view?usp=drive_link", title: "Visual 133", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/10z_1QAcL6tefkUb462xHFrFiys96ofUq/view?usp=drive_link", title: "Visual 134", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1iLinZ6P5XF7BgAcve-Lsj9Hze_m2nfeu/view?usp=drive_link", title: "Visual 135", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1jyuLXF4YNO56O22GN3UnG6KVnG6JcoJo/view?usp=drive_link", title: "Visual 136", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1IDWjg74o-fJyBMiUEr3zpVzB-JK8SIjO/view?usp=drive_link", title: "Visual 137", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1RnjOZP2kIMROPpzZqVoBQ0zxTbxqf7Gz/view?usp=drive_link", title: "Visual 138", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1LA7vS8EexkkI_p_NYHfpJo2SyP6IrImf/view?usp=drive_link", title: "Visual 139", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1ffg_Y2az1hpn-ueZgGmq_4L9AEUI5JLC/view?usp=drive_link", title: "Visual 140", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1C1kSFc7tuwIYrtlVrrFBGYjsOfBHYX81/view?usp=drive_link", title: "Visual 141", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1PaDz7kWtb842gyEzeQQhe0n6dh51nOw3/view?usp=drive_link", title: "Visual 142", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1_WmQgaGNgAMRKJX83whnrgd2dSMISzfU/view?usp=drive_link", title: "Visual 143", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1ePN62juhRXsmzg-0Vh15NQicGThWq5TI/view?usp=drive_link", title: "Visual 144", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/17BBXfk9nwacodNrXws_Is4niRI3JxwjN/view?usp=drive_link", title: "Visual 145", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1_yClQoLtdnvTBkr_3CPX99rCouRbO8qQ/view?usp=drive_link", title: "Visual 146", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Y9mP_lnjYQsodq2oolNQtPBygOgI0D_3/view?usp=drive_link", title: "Visual 147", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1sF9UycllSV5ACBt_BTOG2Qkqdya6tuZ3/view?usp=drive_link", title: "Visual 148", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/16tQXudgNq1L_K4sW4ZdFhgfF3-r0ngkd/view?usp=drive_link", title: "Visual 149", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1SUtdqy4W-whCww5-eCEIfQhJ6QhraQYS/view?usp=drive_link", title: "Visual 150", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1lcYuuWF_stgxKjRVETxRUetiD3fAq3vL/view?usp=drive_link", title: "Visual 151", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Z3NqkRPNXDz7azUJHberj638RC-GJrVO/view?usp=drive_link", title: "Visual 152", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1izGlgNkGVobjYL9ymIi8B3PW_nIvCVm2/view?usp=drive_link", title: "Visual 153", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1fXjYFa0flwi3qHUerUsfsT7OsdPG0Q0y/view?usp=drive_link", title: "Visual 154", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1v5Nsq9VQlxwJ7xg450IE7y8dzpEXl51A/view?usp=drive_link", title: "Visual 155", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1XpGCYsJyIgOaG8nf84K9xP9Ux9D2QMey/view?usp=drive_link", title: "Visual 156", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1pv42gv8W8HimId-okjw8LbQ1BpnfIvhh/view?usp=drive_link", title: "Visual 157", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1F1K9H1aEIwMHjs2PW-iWlOpz5BYfSitu/view?usp=drive_link", title: "Visual 158", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1lgwX6TcgLsvT5JjCuJGpNaxjvGtHxM4y/view?usp=drive_link", title: "Visual 159", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1s_DvX0ocp4iGA_xYyskwyt3s0D3rV3Ak/view?usp=drive_link", title: "Visual 160", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1K4YTm52pHl-GC1wt0sTU5QhTDfsR6JFr/view?usp=drive_link", title: "Visual 161", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1FDCcwpWrRcvn4O3SOB4_E7OzcK5JETY_/view?usp=drive_link", title: "Visual 162", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1lgjpGrJEmjkPZVgG4J-qntmM6Ae_hw2K/view?usp=drive_link", title: "Visual 163", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/14raizWK2prvVJcmYmFVkpGJR8g-8z46B/view?usp=drive_link", title: "Visual 164", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1nkO-e0SwOfe3Cwd1-X23rqELJTbJWHT8/view?usp=drive_link", title: "Visual 165", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/10HrVUiTu42uAw70hwee0PSIwdNnJcY10/view?usp=drive_link", title: "Visual 166", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/18BAiIgLmlI_i0GvgNYI4cE1ksDBtSIiq/view?usp=drive_link", title: "Visual 167", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/17EKQzcQIBdFArkqDl-pRY4Rq-9UGT8iK/view?usp=drive_link", title: "Visual 168", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/12OBbs5pVaPYWXhvIENIM1ieMp97okpGW/view?usp=drive_link", title: "Visual 169", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1rvbBmb-Xy7J6m0UB_7ZNCDdt5XOTltnw/view?usp=drive_link", title: "Visual 170", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1ih2NiLjVr_wxwlt5-7KfpLY2y1rfkJyH/view?usp=drive_link", title: "Visual 171", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1kAAPdqPI4M6G1TsYc7Z2zyTJFDGaA_Mh/view?usp=drive_link", title: "Visual 172", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/14PSTr5iXoGHCgn7uVi35SrWFWDQHPxtQ/view?usp=drive_link", title: "Visual 173", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Z__zQP8xvIZrGDcpfquv-50g3iJOX-Y3/view?usp=drive_link", title: "Visual 174", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1lBD9W909iD1CpcQEGGbECua7kCzWd02h/view?usp=drive_link", title: "Visual 175", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1ENsHtUnz5ww83u6iorUnt92CpvbMfQSg/view?usp=drive_link", title: "Visual 176", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1qkwkMpgAkfIVUAEmj2t7R85e0KD7DvKa/view?usp=drive_link", title: "Visual 177", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1LyQ06tQEJ3haZ9Z1YzdDanSHZzle212v/view?usp=drive_link", title: "Visual 178", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1fSIuUHo2nle5JHOUxkv-fopf_gZT8Dnr/view?usp=drive_link", title: "Visual 179", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1SPOTMDUOrRsNtxHFvgLRdljT6zTzXQVq/view?usp=drive_link", title: "Visual 180", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1OeTJdalO7xpTIZfNNIYzd6NnJiMEhtAu/view?usp=drive_link", title: "Visual 181", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/15WQl8cMg5-uqq3ElHB-35uYf7LM1SJwz/view?usp=drive_link", title: "Visual 182", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1e-1XWAnBr3tu6Z9sSgmvvem8lLTgE-q5/view?usp=drive_link", title: "Visual 183", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1C1rwRJslGA4ZbiTF2MEgBNYNButwH3xg/view?usp=drive_link", title: "Visual 184", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1uJ66mfVDb_pNm4ukszpAKIED4K3lawHq/view?usp=drive_link", title: "Visual 185", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1kCaj3rO4U9Z83F5_igFSbrDq1iG-hyx3/view?usp=drive_link", title: "Visual 186", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1QwFELEj7AOBGHSKmDfnedl5oSkf04Acg/view?usp=drive_link", title: "Visual 187", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1t5tO049ty4Xx_oZUJpT8pPdi6kHrqDIz/view?usp=drive_link", title: "Visual 188", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1C_SJP1pGPx9BiJoGycZ0uzlLg12lQ5VJ/view?usp=drive_link", title: "Visual 189", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1OPPbGZJofLSgPhOB2JlbBNfGP_DjtyP4/view?usp=drive_link", title: "Visual 190", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1pfjb7-rdjJBZ0v1B8lz8te4ylEhF_6Dz/view?usp=drive_link", title: "Visual 191", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1VUxC39DdLNnM0lGg4_4BCKyLngWImBQw/view?usp=drive_link", title: "Visual 192", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1vM3axeTVnIu591C0OnXJQ0j4i0iI-2oq/view?usp=drive_link", title: "Visual 193", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1U7iQR9Y0x2t0uss8jacj2LKPxBdCUqd4/view?usp=drive_link", title: "Visual 194", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1UasR7QDedK-XKCjzlmtXu_e1-n7w45ep/view?usp=drive_link", title: "Visual 195", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1QnMdkSJr5oRK8ZNrCJrUL1pQwMoUiKKe/view?usp=drive_link", title: "Visual 196", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Vuxrnx2aHZg39BRXuQv_3JGlKoNEWw7Q/view?usp=drive_link", title: "Visual 197", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/13rPLgu9l8JQ0eSM-9A6SgaFRjpakjIl0/view?usp=drive_link", title: "Visual 198", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1vH-YbBBOey9UWlhP47K53cYH3DXgsxha/view?usp=drive_link", title: "Visual 199", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1rCuMQB6aWZwvKwOe5lQmDkA2SHnQzsAk/view?usp=drive_link", title: "Visual 200", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1qtZyEkPctTcJ6vP4a8SK00owj-3laE1m/view?usp=drive_link", title: "Visual 201", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/191kuEssrKXQJ5mSAJDoFw_mMsLZ72spZ/view?usp=drive_link", title: "Visual 202", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1vISVumcTLVKwKbPe92m5tQUNFKGwY-ax/view?usp=drive_link", title: "Visual 203", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1dYM6qlzWERh3M8VKqQXFVyUoDWD-hlMP/view?usp=drive_link", title: "Visual 204", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Houmde195VW-NyTRtWY-qUx9NDR2wQmK/view?usp=drive_link", title: "Visual 205", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/18JoYE-c4XQ6sjARDMeNnAeF_M130jHNR/view?usp=drive_link", title: "Visual 206", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1pgY1TQFHoNHVn8FpUnCb3uH1C8O7RqXA/view?usp=drive_link", title: "Visual 207", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1wAmdjdKUOKwf6pj6Hwh-jfhhv_qxmHn4/view?usp=drive_link", title: "Visual 208", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1sFLBNXGGrq_hqEnGHJjvGRX3uTs7GOM7/view?usp=drive_link", title: "Visual 209", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1BNcGgdnrpsBqPPt4eYQAbCW7b1eIWX2t/view?usp=drive_link", title: "Visual 210", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Z1YAvoHiHPOUS1Ek3P4-vy3jqoswycWP/view?usp=drive_link", title: "Visual 211", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1jmMxTQ3xkljHRE2lYlohRQ22BtBXSRFX/view?usp=drive_link", title: "Visual 212", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1s2Ew4bRtDrxETKyFv9ADDTF3TgNyVHhX/view?usp=drive_link", title: "Visual 213", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1H7cA95BQn6lvFr-GcMCbE7qt3KRVe8oN/view?usp=drive_link", title: "Visual 214", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1wvk0KBz3WmDxDhokxSoG8HKYjhpwlnot/view?usp=drive_link", title: "Visual 215", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1zOsPre8lswqsA5yTk_ArOYGYmk5q2KTk/view?usp=drive_link", title: "Visual 216", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1xOIEFHfw6FT_jbhX7VMxCjbceiH4_J5y/view?usp=drive_link", title: "Visual 217", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1FLn-CrPy9BW9aurWZ3ZxkSTb4FPnCRZg/view?usp=drive_link", title: "Visual 218", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1ZmsLIatlg5mC9LCCnBPZP0vOZxe6Ej39/view?usp=drive_link", title: "Visual 219", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1BMH1rIMwT_RMQ7-5yzhQTpxTT2JXgQOX/view?usp=drive_link", title: "Visual 220", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1_aipm2wk8O-OWE3-cMYbbsOBG3bZ0U8s/view?usp=drive_link", title: "Visual 221", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1bub07KpWX33sjTp3NLi1weJcjmXTyrKm/view?usp=drive_link", title: "Visual 222", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Rng1MlbfZPccfJo97r8bDr6oEvwUEJj0/view?usp=drive_link", title: "Visual 223", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1iRbPc3unP4F3GnR3oT2lduZ0Kxt2NEdO/view?usp=drive_link", title: "Visual 224", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1nPpzLKzKyto2CKBeP8GzcojQgOTnp3BA/view?usp=drive_link", title: "Visual 225", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1JN-o2sz97cAXFQ3DOW8E7Q6eNqfQlOki/view?usp=drive_link", title: "Visual 226", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1GxCNh9n9jpKziOxOxiQDUvf9EAYl572f/view?usp=drive_link", title: "Visual 227", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/18lItyithJgHtUkH2WwJ6UvG2ntLN8yNc/view?usp=drive_link", title: "Visual 228", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1eHNoH0lfDNCfEYrFJW3gsTF_4C0cCanv/view?usp=drive_link", title: "Visual 229", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1BEllPlXFrbsWkp91hz0knL38XtpFdipE/view?usp=drive_link", title: "Visual 230", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1OsHegQUjzQXBRvW1QK6-TpeV_L8pb9kM/view?usp=drive_link", title: "Visual 231", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1zzbpgYHIIVbUl7x4c6UL8-ScKWeWz0Wv/view?usp=drive_link", title: "Visual 232", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/12ywEPSWlLtKJBTncUEYCdgg65_QUS0d2/view?usp=drive_link", title: "Visual 233", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1y29SEt1bx2F7ef1fWG6pI2nMi2ojX5eX/view?usp=drive_link", title: "Visual 234", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1at9gLeM-LNnkj-aEDHVoNNYurRL3BwTe/view?usp=drive_link", title: "Visual 235", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1wAK6RgYz04Tr1OYfs0nW89YEGYakvArs/view?usp=drive_link", title: "Visual 236", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1_0CJzIbf60AhZXMmHbEfAxTZXsgUSlK2/view?usp=drive_link", title: "Visual 237", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1vzoNdPmgOvAsZ2R5j87GL71uqrys5DjI/view?usp=drive_link", title: "Visual 238", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/15mbevewApnBI7VcqBFjZq-iLDpdE2E0a/view?usp=drive_link", title: "Visual 239", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1RMrG3h43m1BY4m2vFKkNWHj0qUshjLv1/view?usp=drive_link", title: "Visual 240", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1a6MipEOcOe8XQEUtSTgowRZcYtk4qLLn/view?usp=drive_link", title: "Visual 241", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/15cxKo1uF0K_tcizpsw1ePBKOoVdSpTUN/view?usp=drive_link", title: "Visual 242", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1EpDVKP_Re9kE7OSToed2dbzE90einoFe/view?usp=drive_link", title: "Visual 243", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1XONtXa35wyBWgi3N5T-WuS35gOulm2Ft/view?usp=drive_link", title: "Visual 244", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1OTPB6EDgzlkwO65m__wUX6cjQNNS6UUf/view?usp=drive_link", title: "Visual 245", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1A1u46Na1mn3sV8G7hzjmoRMcXT5gqR0Z/view?usp=drive_link", title: "Visual 246", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/13aWTuGqqEcA6z4ku38nHRhWD2pxbP9rx/view?usp=drive_link", title: "Visual 247", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/15XQwscUjX8ptYbK4yE4yXxtKZ3S0WcdY/view?usp=drive_link", title: "Visual 248", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/11jSyzsDU-mlzkYKmLscArGX0T_YJ_ffM/view?usp=drive_link", title: "Visual 249", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1tVCMdzwJogAIrYwqKGg09XjfTLrreRse/view?usp=drive_link", title: "Visual 250", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1n1p_AvRXAnehopdXlN9zgPlq39jT9Zdy/view?usp=drive_link", title: "Visual 251", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1_TyF8dw2W0O0P9pvC1BCNWT6laekTEKK/view?usp=drive_link", title: "Visual 252", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1vfm9YJA1LUMUlS-FzmuONqbKRATphAXC/view?usp=drive_link", title: "Visual 253", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1PoYe2A5f1Ix7K2WNmYtfrdgS3ear9JEC/view?usp=drive_link", title: "Visual 254", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Oe5a8J16DrQgKeEAX-Zl_t1MQzNi7-Gw/view?usp=drive_link", title: "Visual 255", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1XZvumiXwCSGxWilsJ_AvgXyZ6jn4Xq17/view?usp=drive_link", title: "Visual 256", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1X0UQX-4xk3MKYFE9MFzd8OPiS3m9L5Du/view?usp=drive_link", title: "Visual 257", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1qphRN7X5zdB1owvFpon26KfywNf5bcCZ/view?usp=drive_link", title: "Visual 258", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1GpFRvdfqPYDK5kusHFUzC0YdOlHBGmT4/view?usp=drive_link", title: "Visual 259", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1F-496McE6E2tygSqvspPg7rZns4FNyue/view?usp=drive_link", title: "Visual 260", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1bdH-lJB71Y_z4T6k_RIvuHnikWTnPFsA/view?usp=drive_link", title: "Visual 261", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1vygACh6fLGTfEWmJudiXzZZt9jdTC8oB/view?usp=drive_link", title: "Visual 262", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/10g1VyGWE17xLyXDxWdXDKyi51kjG2VMB/view?usp=drive_link", title: "Visual 263", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1I0sowGUDkfma-jGb2pwPD1TrL8VFOqDW/view?usp=drive_link", title: "Visual 264", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1yx6Lq6O6q1jMRjMMkfV0V16qa05jBXHd/view?usp=drive_link", title: "Visual 265", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1je-6RwUJAckbz8AmyGdMVY28jqU1CnQF/view?usp=drive_link", title: "Visual 266", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1IgEZgAguAn-tcFtlmFr_7A_Zn5K6Ja0t/view?usp=drive_link", title: "Visual 267", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1MwHpsRmwB9sFe6Es98pEzRoWtFLPrL3K/view?usp=drive_link", title: "Visual 268", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1dUYJIi4Wq6yUSKIs-b9DPTPY5E0sN2yB/view?usp=drive_link", title: "Visual 269", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1E_7lqjFNv_BSfaA4cTr4lQ1Aixi649N2/view?usp=drive_link", title: "Visual 270", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1pJ6qGFMsgcBxWsILNCENaXBSMVKldVeY/view?usp=drive_link", title: "Visual 271", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1rsYTkvVkYFiC_hmfXf-yzJmL5rAFE1bD/view?usp=drive_link", title: "Visual 272", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1CsVc95royPanodGhoKxRFm1D6m72SRMC/view?usp=drive_link", title: "Visual 273", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1KFvIk8jEb1dnLVkiD7G9RgrCCDy-ADne/view?usp=drive_link", title: "Visual 274", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1XsGKojlUW60M62DiZzXwgePeecHNT_i4/view?usp=drive_link", title: "Visual 275", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1sX4yijTGBvhYmO_F3wHufQrvQ30ouKiC/view?usp=drive_link", title: "Visual 276", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1RALuzZRw40ipNMSgme-JTeYl-ylkjkE3/view?usp=drive_link", title: "Visual 277", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1crWn1qk0YJV70kSg_qqPRm4GFWnxvFrU/view?usp=drive_link", title: "Visual 278", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1j560g2oCxz7enW0n9DoUkblZR88XvWeH/view?usp=drive_link", title: "Visual 279", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Q0ye8br0vUpL3yJikn5GTMNiw5FkfR7g/view?usp=drive_link", title: "Visual 280", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1E5zouNBfntlKEqF_pQl7qO-vNPwVYqic/view?usp=drive_link", title: "Visual 281", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1sTeck4tVg18YuhoAf_uuTjgK-u7xg-kd/view?usp=drive_link", title: "Visual 282", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1TUqsvMCBDw_tbdPoR7UOtGsmRP0PZaFT/view?usp=drive_link", title: "Visual 283", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1z5CEWHDu-GnNQFfClTRgFhk3aKRvW1rH/view?usp=drive_link", title: "Visual 284", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1PBWq2H4WVqm_LqjfMD3xY8rppRXA6wNL/view?usp=drive_link", title: "Visual 285", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Avtu_ILxAh9rKgJ56Mm6kPE_D3GZ6MPk/view?usp=drive_link", title: "Visual 286", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1KqAOOn3Yw9iF-cfEe8LFLqrV-hLZz86i/view?usp=drive_link", title: "Visual 287", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1plussZTHJEYEDYW5JeICzz3JnvEG0NmC/view?usp=drive_link", title: "Visual 288", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1QHP1rUPSzfXpDCqBTL-pIKzRfAsrY2Um/view?usp=drive_link", title: "Visual 289", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Tk3h8MdRXKQqguovu7pT0CqwRQXOLjzy/view?usp=drive_link", title: "Visual 290", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1z0xBNoTwxDUJrXwsAwEkP00h-xZZ3PHC/view?usp=drive_link", title: "Visual 291", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1VKB0jGsa701A0DnWuTSpo1x2NyZ24DWf/view?usp=drive_link", title: "Visual 292", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1838mfH_w_eSZ-oQT_-FR88agAFT2TOv0/view?usp=drive_link", title: "Visual 293", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1HEILxuK-HzfRcCb-VxDncOZY1ViKvRqL/view?usp=drive_link", title: "Visual 294", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/12WzzM0FSmvj31gO9hr96NLtZ2wK_bCMl/view?usp=drive_link", title: "Visual 295", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1LGNxXCnesFkGtUE9YTbJmUMWYTiINWRb/view?usp=drive_link", title: "Visual 296", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1lNplNIh7IcemJxUiK9um6U-uhZt8qAAQ/view?usp=drive_link", title: "Visual 297", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1gB27SSZEe4tI-hRix5lmdrPCe21Rk7qC/view?usp=drive_link", title: "Visual 298", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1rMp9TbMILEZsSqrgsAGFdEiRiB9y6n_p/view?usp=drive_link", title: "Visual 299", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1nqY_yS106jsQYhkr0W-X2tuOSquofYbt/view?usp=drive_link", title: "Visual 300", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1JSSvQ0h4hiTke3MSXRhXOxfSycsN3PcP/view?usp=drive_link", title: "Visual 301", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1leMjmRl5dc9k_PzP9AdLoHgTpkK8PS5C/view?usp=drive_link", title: "Visual 302", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1rVJMW2T3yFZRH99AAKW59pBZmtcL3qag/view?usp=drive_link", title: "Visual 303", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Vplvgco-nZbXMjvCuF3sd5bKp9e-cKJR/view?usp=drive_link", title: "Visual 304", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1dLXlpXdL1M-Q4FXS8RrtXKwjFlglgWgm/view?usp=drive_link", title: "Visual 305", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Zt4FWTV9HXmFCcy4xjgtFfeGL923-Uww/view?usp=drive_link", title: "Visual 306", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1ABnVA-Dg3JBPeXhpNA-R8jJCa-tILvhF/view?usp=drive_link", title: "Visual 307", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1-Xalyrv74rFY7XmaLLO0QdIPtViAf_dX/view?usp=drive_link", title: "Visual 308", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/18SzXIDxEw3bNpeZbDGBdIDJS6RP4nze7/view?usp=drive_link", title: "Visual 309", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1nR7yV8xYjL09VwiHIWOSnRjamIasncLJ/view?usp=drive_link", title: "Visual 310", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1v_J4ZiZSmwyZFrigl8q2ByKbDyqpfIza/view?usp=drive_link", title: "Visual 311", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1GVORW27_DCs3G9f-zUFIC_6HdY6YWeOQ/view?usp=drive_link", title: "Visual 312", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1PZAuNok10vuVl0Q9hm8f5S5Sfp7klP0G/view?usp=drive_link", title: "Visual 313", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/10a7pbsd4MxmyKd1Js9c25RChN6kP_BFh/view?usp=drive_link", title: "Visual 314", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/15MolbFWtTJAJx1fKza9mhgqQDEpBOqk2/view?usp=drive_link", title: "Visual 315", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/17CZgT3pKC9pG-dKPkqdxoILG49CczZA1/view?usp=drive_link", title: "Visual 316", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1G3oacIdzjqBw8isOp53l1jOJO2lFqZjs/view?usp=drive_link", title: "Visual 317", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1p0-r6ww1P9lEHtznIo0cGXZe14eKI2bq/view?usp=drive_link", title: "Visual 318", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/152UizfG-KLsQSCgcRUDRw9Kdb0Q7m5xu/view?usp=drive_link", title: "Visual 319", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/15RTwQi-VodClvsQmvIYXsemGECchyUft/view?usp=drive_link", title: "Visual 320", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1XrUog6LwjdQa8l2dJDVjZQUz5RWHPN3S/view?usp=drive_link", title: "Visual 321", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1s3upMmjNPf7OeKTlrdFwpl5q16c4i0uC/view?usp=drive_link", title: "Visual 322", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1o3FgwCwfdY4Kw8xbRMYrA0rItIxCx6yL/view?usp=drive_link", title: "Visual 323", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/16jdPba1bcwbLmvIG8_K0wzhPO2MnHtA0/view?usp=drive_link", title: "Visual 324", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1RfBsDhhyjHnweoXT8wJrHAnqxF6N2l1X/view?usp=drive_link", title: "Visual 325", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1_r7KnRel2UFCtotD3MFP6MHLCeWb96Lg/view?usp=drive_link", title: "Visual 326", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1CEuecj2xJsDkeuTbqPwZndBOs0nxERfv/view?usp=drive_link", title: "Visual 327", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/19dNSwsma2z7CPyuktx1L0ucjUKzidwvy/view?usp=drive_link", title: "Visual 328", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1tKBvhMMVunBwrZ_nWEmjIAG6FvuKNFAI/view?usp=drive_link", title: "Visual 329", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1jVlXWNMTJ8isma9_pMZ_AuvC9uQq7IpY/view?usp=drive_link", title: "Visual 330", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1ntQWQ0niJ2jnAnKHRzsY9vOytWMOYSMd/view?usp=drive_link", title: "Visual 331", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1NWknQ4bkLTzeZ-AKLycYvzBZuef9EjvH/view?usp=drive_link", title: "Visual 332", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1aKIv19PdKdWd_SIPdqQ4occoheYDS1qz/view?usp=drive_link", title: "Visual 333", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1D-ifDKGFKTDccQHbBeTwCYTNoRjTpY-w/view?usp=drive_link", title: "Visual 334", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1e8HO1cWllSi2TGc8QjvqmuUgwIq0I21k/view?usp=drive_link", title: "Visual 335", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1ox4c-TIsVW8dp6HA4-wCMnmpy2bPbQ8-/view?usp=drive_link", title: "Visual 336", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1D8WeGV5-o3eQENWPbgOqbOgkX_E8nDR3/view?usp=drive_link", title: "Visual 337", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/18IC3i1jZhGbW8G7OsQA2UNivohq_8gww/view?usp=drive_link", title: "Visual 338", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1yB1KQrDCyARSBT90GeiAe5yU1Eih3TAV/view?usp=drive_link", title: "Visual 339", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1yF7FR6hFKT5UcU_Pl0iVa4kmwSBXH4gY/view?usp=drive_link", title: "Visual 340", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1reHOkfemXz0u8G2KnlpEn13Rz_xvO_OR/view?usp=drive_link", title: "Visual 341", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1SjJlJam9ikNCDicJRUSTqKjeoU2vsVA4/view?usp=drive_link", title: "Visual 342", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1KMgU-GGcVdRgA8feIu73oRIUOqSg3ETv/view?usp=drive_link", title: "Visual 343", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1VOqGL4Mc7CAA8yeCsVtAW1-bsGAL4p9e/view?usp=drive_link", title: "Visual 344", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Bc4MVdnsbNWnH1Yqw5vAF4EkZwNer1bD/view?usp=drive_link", title: "Visual 345", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1WmMe1P0x6zmZkeMbBJD14UZue4iCYX3n/view?usp=drive_link", title: "Visual 346", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1LA2H2ABfSnap_Cg8uHVBUjBMwzyNz4WW/view?usp=drive_link", title: "Visual 347", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1ipF4yznN1h9l5zkdiMhkLCMIuIO9_LVt/view?usp=drive_link", title: "Visual 348", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/18_zrNIgqAOOJEwo1AX57iv26Nm5EXFJN/view?usp=drive_link", title: "Visual 349", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/12qySLl-fQePzRLG8yyyE5ZpSIroPMX5Y/view?usp=drive_link", title: "Visual 350", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1lnkKz-A7qO1Nh9ndYh-zxNRTzVOAqsb0/view?usp=drive_link", title: "Visual 351", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1dmFCuAGb3tHgJxIHY_feuRRaRSPaDaN5/view?usp=drive_link", title: "Visual 352", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1GToQC4s0sceyDapVMwjXaEwIeNTp3r0z/view?usp=drive_link", title: "Visual 353", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/124JjBML74N4JWmdUMWbfP6Od7ltM5_dC/view?usp=drive_link", title: "Visual 354", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/15sTrKlRJEVDY_dmZG7xJ3c6z_fzcqODf/view?usp=drive_link", title: "Visual 355", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1RoyA2mbxn__z6zzt4QhLPDOo1a0t6zTy/view?usp=drive_link", title: "Visual 356", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1glrxpVaIw1cVVjE4ikSzIgYtpPqElUEx/view?usp=drive_link", title: "Visual 357", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1DwhZeVnJLovfyRn9rDd7XvqAlsozqO_N/view?usp=drive_link", title: "Visual 358", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1bx4TmRJ2BdPpKuqp8XbHB-BJnEU7zBVb/view?usp=drive_link", title: "Visual 359", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1S7kwig6fuI2Azpzxmi72ILOp7DJzU1Bn/view?usp=drive_link", title: "Visual 360", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1X7nH1gHEsYg8YQXPoJZOTEWjtH83zNPw/view?usp=drive_link", title: "Visual 361", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1vtVHZ5HIBXHL7QV1GwZMs-DOi2EpZNnQ/view?usp=drive_link", title: "Visual 362", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1NKcXcSZsXUFMQeJYdm6Ujbkp1b-PbQ-L/view?usp=drive_link", title: "Visual 363", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1VkZ7kaRRDLgQJSfBnK2a0npZMC9haQ5L/view?usp=drive_link", title: "Visual 364", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/14YAWXpMViITarvsHjtROR5B6giW5LO4h/view?usp=drive_link", title: "Visual 365", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1JTwVhVfOVZMO_Be6TAqtd4bHfaEPtS1g/view?usp=drive_link", title: "Visual 366", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1uwbomX5w7l_ASHXwS3zM7WECzrX3A_TT/view?usp=drive_link", title: "Visual 367", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/19vtrxeKretj8dYgx-Crl7sNNTpupA_p4/view?usp=drive_link", title: "Visual 368", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1rMSaoGpgir-0zGkWxjNpNVWUVwqYdFWP/view?usp=drive_link", title: "Visual 369", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1GDcawVmuDkAceHvjRsbDSwLucrvM8Z7y/view?usp=drive_link", title: "Visual 370", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1kVOC18bhW9d6dMjUC4SZknu6f0ccQaq6/view?usp=drive_link", title: "Visual 371", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/11BsjPmUGGQWkbYU57v3VJyo9AzF08Etu/view?usp=drive_link", title: "Visual 372", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1GXRWxqPiy7gl1cyUvc9u0VkW5S5XREXN/view?usp=drive_link", title: "Visual 373", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1RbgzjpK2uT_SHYEaWfjgebxBFHlpizQl/view?usp=drive_link", title: "Visual 374", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Es8dOTlc1DxbVKEcdwrE9IDgi6AXWgdV/view?usp=drive_link", title: "Visual 375", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1o3NTBE3xj4LbFsRo04fCZN_Qyj2UXaWO/view?usp=drive_link", title: "Visual 376", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1gVxjBRpsys8MABHr10ng3aPY-HmPi5cf/view?usp=drive_link", title: "Visual 377", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1sCYXkMxQTrDCZoXbp70LL4bQpDveaNKJ/view?usp=drive_link", title: "Visual 378", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/13DrvQSzTRSWJ414qeUQ5NZi5VQeXhuZ6/view?usp=drive_link", title: "Visual 379", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/18LjPaG3tIM0yUo-VTN0MXX34a3yUYYsh/view?usp=drive_link", title: "Visual 380", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1UmmN_IKdFO5STs45Cfu0S6lYdkluQSkq/view?usp=drive_link", title: "Visual 381", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1dr0fojMImVYOopusvfb7wp6VRVpdE0yV/view?usp=drive_link", title: "Visual 382", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1o5ZlF_c0eMXkgaoe7dkpPk9kFV-tP24y/view?usp=drive_link", title: "Visual 383", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1hJ_2iId9Mt8qfz2Z6nRHmiTettT4wkAe/view?usp=drive_link", title: "Visual 384", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Gc4usgF200OTOjks5aKnBf45zHYNm6JJ/view?usp=drive_link", title: "Visual 385", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1ulk0fdcmaHr8NNnuBiYHQYT-DBMz36Vc/view?usp=drive_link", title: "Visual 386", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1eTYjZMLmrZKCdh7s5uIiiuBExfVCZ6-k/view?usp=drive_link", title: "Visual 387", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1h5JpGcjpFXAzq0mUaza8JsvCDrTAk08Y/view?usp=drive_link", title: "Visual 388", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1faI9McYZZL15JZA5ywpdmHpVGp-fwarR/view?usp=drive_link", title: "Visual 389", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1uZPeQcDNFO9CtSRJhZkONvbllno9fxrl/view?usp=drive_link", title: "Visual 390", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/18hfrE0hZOUiRK3eXEEfwCWl1uJV8Nrq-/view?usp=drive_link", title: "Visual 391", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1ak2xpcLXaKdISTI5aEC3t9tDTM-htYPx/view?usp=drive_link", title: "Visual 392", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1gQekSD_LzJLcVX6u-R2YHDiNStTQKc-z/view?usp=drive_link", title: "Visual 393", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1PkTAcyAWBLxatbfeqsbyloTl0N8bTYLt/view?usp=drive_link", title: "Visual 394", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1GpW8ME6YC01WQMVnVni7-_Ih42qaWrdh/view?usp=drive_link", title: "Visual 395", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1FDYD8vex3IfDRkJku3PmEDjmOevads1U/view?usp=drive_link", title: "Visual 396", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1uQ6vhDH73q0gjN0HLbG-bgVtW2s6ENUi/view?usp=drive_link", title: "Visual 397", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/14vYZiTdpq0ggWX0x76FSIYbN5vpnQGqS/view?usp=drive_link", title: "Visual 398", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1xhcCQWSB4H18dA3pQZvAl-fxvGdoInW0/view?usp=drive_link", title: "Visual 399", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1PRe9RbNxR_YgI8oNNDUk-9JrU7r_sJj3/view?usp=drive_link", title: "Visual 400", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1iTDA5C8y0eUko4_Wud59URxXjMQqMylQ/view?usp=drive_link", title: "Visual 401", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1nZx5-aXjhrzA1xAD372vhENWXGF_aYkO/view?usp=drive_link", title: "Visual 402", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1BPvpnD8i6aeqQq-7te5cnT0__pIJ-S6n/view?usp=drive_link", title: "Visual 403", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1UjJsJsIoJ5AZwpBNEVqxotLSTTconxkX/view?usp=drive_link", title: "Visual 404", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1AdiOUjmeISsC1piZulVnvDPdXgGTtJdC/view?usp=drive_link", title: "Visual 405", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1oiTXwLF-UAO0GhK7oUBCED5sgHzKBbYN/view?usp=drive_link", title: "Visual 406", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1cfxbo5riGJtnKM6P1SEjDGEniwukO3zD/view?usp=drive_link", title: "Visual 407", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1PEg260TiCA9w7VVNoRSAOmBhdbEPNR0D/view?usp=drive_link", title: "Visual 408", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1gTLeCZf89-MFO4LVxgIh07fpP6QtBbKM/view?usp=drive_link", title: "Visual 409", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1TawcQuxq6yHTvD_SG10dxB3WGwvza16i/view?usp=drive_link", title: "Visual 410", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1-wkBInvYueFWZ-iwyQ8oP9V1uFFUaJQ7/view?usp=drive_link", title: "Visual 411", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1f5XQzHopD65Qf_jSzlzNjA5pSs_EX6GF/view?usp=drive_link", title: "Visual 412", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1q38TCTHUnp_evtXI2UDO2U5hk3aE63EO/view?usp=drive_link", title: "Visual 413", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1kUbiCVTwTgNoakT4qUtdohdHxwjZ1anw/view?usp=drive_link", title: "Visual 414", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1tGPQI32UtzCUSugPRb4Z-VMqzIWzjjmU/view?usp=drive_link", title: "Visual 415", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1OZ-03Hg4KfPHelcoUQO0MwpuKdRzBQAs/view?usp=drive_link", title: "Visual 416", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/12ZKg8MuyXb6WplWQVDJ4Y6pHNPMmlZYG/view?usp=drive_link", title: "Visual 417", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1oB-f_Bx0rBLFW1HT5Kr8_vN3qsbM8NWq/view?usp=drive_link", title: "Visual 418", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1HHjsvFy8q4i0Ly2h1qzG5SlfmM9N6jif/view?usp=drive_link", title: "Visual 419", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Iv1ThyO5l_eg3a1XCfUaEZ4AW9j6_ZOj/view?usp=drive_link", title: "Visual 420", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1FrfYvyNmg9F3RcCtEyocehASvrNmcS5m/view?usp=drive_link", title: "Visual 421", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1nKAQum0IICfxAVKgDfzVGjJYhuQ0BMHW/view?usp=drive_link", title: "Visual 422", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1kmWZNtouAuKxgxOENWyw8zH7YbhHWwXm/view?usp=drive_link", title: "Visual 423", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/12dJtoLZOOFRS0u4DYqzlJ091MSAlp8_d/view?usp=drive_link", title: "Visual 424", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1a5LbYs70txFOyEcLHtPFFb25xHyDmZsV/view?usp=drive_link", title: "Visual 425", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Hfoin7hsr4HSFtuEr2XFfHh6eWTIftae/view?usp=drive_link", title: "Visual 426", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1brBa1LPPdHoVMbocZF00BknvcLEKyqk6/view?usp=drive_link", title: "Visual 427", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/16B7AuYUQDTTFsJMVGHVtuJHq6vHtK33N/view?usp=drive_link", title: "Visual 428", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1BqWvdWQj3tALrdzN9ZL1vSDsOM3ef0uF/view?usp=drive_link", title: "Visual 429", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/143F2ZukEN7HQmz9OY8aXZxEzN3cN-CEF/view?usp=drive_link", title: "Visual 430", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1R4LqmNOcVAErvUgbwne3tjpTuovSxj2_/view?usp=drive_link", title: "Visual 431", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1W6kxtAbfOeqhMV4kPoakNypnaCPqEnuz/view?usp=drive_link", title: "Visual 432", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Iw0q1jjyoe8-jBia9gXMH4BCFMsz1izQ/view?usp=drive_link", title: "Visual 433", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1EIE60IZ1lW6RcIEi6uOANPdEoFn8Vvnj/view?usp=drive_link", title: "Visual 434", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/10CPjxebpOH-Y8th1Q00zde7iVI0lAOXq/view?usp=drive_link", title: "Visual 435", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1c3iJgB5p_l6EOJvGdQnR6J-ZTBhagoT_/view?usp=drive_link", title: "Visual 436", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1WpfQ6xqEukfYUR4gzA9BMLsA2nWMdbzZ/view?usp=drive_link", title: "Visual 437", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/13Fd83T_hDHiOhz3k0JiOPvoeBlbhJ3DV/view?usp=drive_link", title: "Visual 438", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1NVQiqUewwXoLgj-F_kifxrYjkQ1ZfF1c/view?usp=drive_link", title: "Visual 439", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1IiGlPics0-ZaMPpHk2fuc4reZkrL0fvq/view?usp=drive_link", title: "Visual 440", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1FfKxRnemtjVsREoeLLrpt4MM-2lP_dW1/view?usp=drive_link", title: "Visual 441", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1AuqGi7Z6F-usq11oBIUKbgg-jeD6RVSC/view?usp=drive_link", title: "Visual 442", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Bmaj8J22zGY86NAYMbEhnzKk5qONJcwC/view?usp=drive_link", title: "Visual 443", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Ojga4nc_2IHr2J8Cb0PQYCV1hwGFxpKd/view?usp=drive_link", title: "Visual 444", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1pY50QvRQSDzLOhytmxMm8ZO7T4LJ0zsO/view?usp=drive_link", title: "Visual 445", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Wrp9EI6ZkJUSNUvnNZAPUAIKhGG13965/view?usp=drive_link", title: "Visual 446", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1pnLBrMOFtAD70UvPJKaM_DWvm7D8wRmT/view?usp=drive_link", title: "Visual 447", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1M3NXGlZLypdwuqEc696uORYqc6IQDsfC/view?usp=drive_link", title: "Visual 448", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1PlWhX0gVDXX_P6ADz2CWQ3YkoYHDJA2Y/view?usp=drive_link", title: "Visual 449", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1eFf8u6UUFR7yzW-YXTtIs4QLXPNJHyzQ/view?usp=drive_link", title: "Visual 450", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1zFewjfoIF6CP_olFSIVBCON7GOyW8_mu/view?usp=drive_link", title: "Visual 451", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1bHVIqwfIVfDejU3M4Y7VY57zQt_R65eB/view?usp=drive_link", title: "Visual 452", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1NSEM2zefW5-anYEj_T-E5FUmhsi1oMmu/view?usp=drive_link", title: "Visual 453", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1iQhYljmQ2FnNkq6v2c-4K9KtSUp2cUCJ/view?usp=drive_link", title: "Visual 454", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1j6G1ASZmtWMAdH4by0h93SWwyCVJiAud/view?usp=drive_link", title: "Visual 455", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/15QdqXlmacZqTRq21lQNLO2aBwm_T5wFn/view?usp=drive_link", title: "Visual 456", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/14-NqCwE0MDyq2r2jVIMj_QK6HfrZPVRP/view?usp=drive_link", title: "Visual 457", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1mCRiJugFitbwqKMJoivFfK-3J3zb5BAb/view?usp=drive_link", title: "Visual 458", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1c1SDx0XvjvoEO1V9dh9xHce5LtjRbOBB/view?usp=drive_link", title: "Visual 459", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1thsI8-X26GkIOCBpVyR-l2tXMgY7-ATo/view?usp=drive_link", title: "Visual 460", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1wNPG6y3vzI3Xrhom3rJS2fkC30iHA42p/view?usp=drive_link", title: "Visual 461", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/19FioocGbDeyt_bfsR2Z1vzqouiYYtpEu/view?usp=drive_link", title: "Visual 462", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1-MhR64TvhA8t7LQC5tOM3epZb9guKoDh/view?usp=drive_link", title: "Visual 463", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1_-U1OiNRk6uV-BBr7pJ7YLM0sYHGEDJ7/view?usp=drive_link", title: "Visual 464", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/1Lrkz5Bqh2i-h5u7uAr56I7roID1N1rKH/view?usp=drive_link", title: "Visual 465", category: "other", description: "ARCHIVE" },
  { url: "https://drive.google.com/file/d/18h2VdM7fAwftFFvueT8KHfiOOjolG2sM/view?usp=drive_link", title: "Visual 466", category: "other", description: "ARCHIVE" }
];

// Fungsi helper untuk mengekstrak ID dari URL Google Drive asli
function extractFileId(url) {
  const match = url.match(/\/d\/([a-zA-Z0-9_-]+)/);
  return match ? match[1] : "";
}

const gallery = document.getElementById("gallery");
const count = document.getElementById("count");
const empty = document.getElementById("empty");
const lightbox = document.getElementById("lightbox");
const lightboxContainer = document.getElementById("lightbox-container");
const lightboxDownloadBtn = document.getElementById("lightbox-download");

let currentPhotoId = "";

function driveImage(url) {
  const id = extractFileId(url);
  return `https://drive.google.com/thumbnail?id=${encodeURIComponent(id)}&sz=w1600`;
}

function driveVideo(url) {
  const id = extractFileId(url);
  return `https://docs.google.com/uc?export=download&id=${encodeURIComponent(id)}`;
}

// DOWNLOAD DAN REDIRECT INSTAGRAM
function handleDownload(url) {
  const id = extractFileId(url);
  const downloadUrl = `https://drive.google.com/uc?export=download&id=${encodeURIComponent(id)}`;

  window.open(downloadUrl, "_blank");

  setTimeout(() => {
    window.location.href = "https://www.instagram.com/anothervisual_creative/";
  }, 300);
}

function renderPhotos(filter = "all") {
  const filtered = photos.filter(photo =>
    filter === "all" || photo.category === filter
  );

  gallery.innerHTML = "";
  empty.style.display = filtered.length ? "none" : "block";
  count.textContent = `${String(filtered.length).padStart(2, "0")} PHOTOGRAPHS`;

  filtered.forEach((photo, index) => {
    const card = document.createElement("article");
    card.className = "photo";
    card.style.animationDelay = `${index * 70}ms`;

    let mediaElement;

    if (photo.type === "video") {
      mediaElement = document.createElement("video");
      mediaElement.src = driveVideo(photo.url);
      mediaElement.muted = true;
      mediaElement.loop = true;
      mediaElement.playsInline = true;
      mediaElement.preload = "metadata";
    } else {
      mediaElement = document.createElement("img");
      mediaElement.src = driveImage(photo.url);
      mediaElement.alt = photo.title;
      mediaElement.loading = "lazy";
    }

    const info = document.createElement("div");
    info.className = "photo-info";

    const details = document.createElement("div");

    const title = document.createElement("h3");
    title.textContent = photo.title;

    const description = document.createElement("p");
    description.textContent = photo.description || "PHOTO COLLECTION";

    details.append(title, description);

    const zoom = document.createElement("span");
    zoom.className = "zoom";
    zoom.textContent = "+";

    info.append(details, zoom);

    const download = document.createElement("button");
    download.className = "photo-download";
    download.textContent = "Download";

    download.addEventListener("click", event => {
      event.stopPropagation();
      handleDownload(photo.url);
    });

    card.append(mediaElement, info, download);

    // BUKA FOTO ATAU VIDEO
    card.addEventListener("click", () => {
      currentPhotoId = photo.url;

      const existingMedia = lightboxContainer.querySelector("img, video");

      if (existingMedia) existingMedia.remove();

      if (photo.type === "video") {
        const vEl = document.createElement("video");
        vEl.src = driveVideo(photo.url);
        vEl.controls = true;
        vEl.autoplay = true;

        lightboxContainer.insertBefore(vEl, lightboxDownloadBtn);
      } else {
        const imgEl = document.createElement("img");
        imgEl.src = driveImage(photo.url);
        imgEl.alt = photo.title;

        lightboxContainer.insertBefore(imgEl, lightboxDownloadBtn);
      }

      lightbox.classList.add("open");
    });

    gallery.appendChild(card);
  });
}

lightboxDownloadBtn.addEventListener("click", () => {
  if (currentPhotoId) {
    handleDownload(currentPhotoId);
  }
});

function closeLightbox() {
  lightbox.classList.remove("open");

  const media = lightboxContainer.querySelector("img, video");
  if (media) media.remove();

  currentPhotoId = "";
}

document.getElementById("close").addEventListener("click", closeLightbox);

lightbox.addEventListener("click", event => {
  if (event.target === lightbox) closeLightbox();
});

document.addEventListener("keydown", event => {
  if (event.key === "Escape") closeLightbox();
});

renderPhotos();
</script>

</body>
</html>
```[cite: 3]
