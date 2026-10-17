

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

/* Semua foto tetap persegi, tanpa ukuran tall/wide */
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
// DAFTAR FOTO DAN VIDEO GOOGLE DRIVE
const photos = [
  { id: "1HmYYsUgbQbr0ASooF0gHmnWElC1aeO9c", title: "Visual 01", category: "other", description: "ARCHIVE", size: "" },
  { id: "1k9740f8wNXwhYg-pe6IH2E_tB1MwzQWE", title: "Visual 02", category: "other", description: "ARCHIVE", size: "" },
  { id: "1q0kFW1qvjqLsNcER0y75rD7PZiCD6mFE", title: "Visual 03", category: "other", description: "ARCHIVE", size: "tall" },
  { id: "1sv_ZDSXu1ih1j1Wl7Nb6ZDJ1IJG54m1q", title: "Visual 04", category: "other", description: "ARCHIVE", size: "" },
  { id: "1C8hOeBxOWPYtGri0w07Cxy7IJKzl1rDH", title: "Visual 05", category: "other", description: "ARCHIVE", size: "" },
  { id: "1fCnKr1Es6W1e25B6-VaSvFDSdAWf5er6", title: "Visual 06", category: "other", description: "ARCHIVE", size: "wide" },
  { id: "1PcK0TA2xX9HW8yXiYZ247eQPLwnyxJAY", title: "Visual 07", category: "other", description: "ARCHIVE", size: "" },
  { id: "1BD7Yxi1fvv3MDJPhe8vMr_rGX_-V90VD", title: "Visual 08", category: "other", description: "ARCHIVE", size: "" },
  { id: "1GjWFiSvkKeJXq5_QREs2qd5EuEFeMG0i", title: "Visual 09", category: "other", description: "ARCHIVE", size: "" },
  { id: "1h302-hRw83CSYYX2i7D7HyiWFojiPywV", title: "Visual 10", category: "other", description: "ARCHIVE", size: "tall" },
  { id: "1Yj3Bnl2kCr6dcveB_EQq1B2pgedWwav0", title: "Visual 11", category: "other", description: "ARCHIVE", size: "" },
  { id: "1vLBdLCl1sb-plg4MXR_EDsS7M3mLVNS1", title: "Visual 12", category: "other", description: "ARCHIVE", size: "" },
  { id: "1yDFcjDu3INMdjnHPeOOJiAfuA-bDereH", title: "Visual 13", category: "other", description: "ARCHIVE", size: "" },
  { id: "1hRDaz12uwksQecRfDmBXHfLhDdyhsR6q", title: "Visual 14", category: "other", description: "ARCHIVE", size: "" },
  { id: "1fOoP_2-mV-EpjEGGwi8D00uNbyCydpvV", title: "Visual 15", category: "other", description: "ARCHIVE", size: "wide" },
  { id: "198R2s_UCWUKHElya0_E2fPtwkwt19CRP", title: "Visual 16", category: "other", description: "ARCHIVE", size: "" },
  { id: "15gk9lqpKyseiFHJJb_ya-JOLZKIE0PzR", title: "Visual 17", category: "other", description: "ARCHIVE", size: "" },
  { id: "1KUTJKzcoZZ4I4TiKkhHfmDU0Dn00OvhY", title: "Visual 18", category: "other", description: "ARCHIVE", size: "" },
  { id: "1kjGIdT1dJRqpk5yf_nweVWM68kwp04Vp", title: "Visual 19", category: "other", description: "ARCHIVE", size: "" },
  { id: "1pT5OF6yCY3eEYEtSKoVQW0TpTgHLrG-f", title: "Visual 20", category: "other", description: "ARCHIVE", size: "tall" },
  { id: "12-KjEWyHWu_5SiECyKhdtumx0BvXITqd", title: "Visual 21", category: "other", description: "ARCHIVE", size: "" },
  { id: "17hZ8YrWGZLaiXsk-hbey2OdWwNB0z3gK", title: "Visual 22", category: "other", description: "ARCHIVE", size: "" },
  { id: "1Z9FY_uRRwzAlGEQA8IChyQGF-VXf5Rw5", title: "Visual 23", category: "other", description: "ARCHIVE", size: "" },
  { id: "1Qz0zzaXNTFMkHbK0FvV-PbjalHB6bwQ-", title: "Visual 24", category: "other", description: "ARCHIVE", size: "" },
  { id: "1FfpVMOkJIiKPoLQ1tvpE4-69TKGHjNVP", title: "Visual 25", category: "other", description: "ARCHIVE", size: "wide" },
  { id: "1XzTyDjgvPL3aOuqnGYN9ENnmA-6ED-1a", title: "Visual 26", category: "other", description: "ARCHIVE", size: "" },
  { id: "1LWk1UNwq-Cao_QzqLBnSl2stwsOxyjSB", title: "Visual 27", category: "other", description: "ARCHIVE", size: "" },
  { id: "1NdruPZh63O6-NgEMFPHY2hC-RdlDAHDR", title: "Visual 28", category: "other", description: "ARCHIVE", size: "" },
  { id: "1K1YI2XyXWWtmmndJumXmbo_7_quT7Ef7", title: "Visual 29", category: "other", description: "ARCHIVE", size: "" },
  { id: "1CfE9zdORjJR23eZy7BcuY3kZ7RBUkcoR", title: "Visual 30", category: "other", description: "ARCHIVE", size: "tall" },
  { id: "1bo2kBLThPIuIfl9ld1-DyJkAOUhOKQ6H", title: "Visual 31", category: "other", description: "ARCHIVE", size: "" },
  { id: "1jHtY2hNubzYp4fENTb64od6-I143dm-5", title: "Visual 32", category: "other", description: "ARCHIVE", size: "" },
  { id: "1jnJ_i5Apgq-7HQIS5FrmLAXJcUlCYd5W", title: "Visual 33", category: "other", description: "ARCHIVE", size: "" },
  { id: "12xDeeMvKUZB_1ZQdT5CJVCEf0NYjv8Gf", title: "Visual 34", category: "other", description: "ARCHIVE", size: "" },
  { id: "1POWi6Qvr1pHl0PR_P-eUK6tfUzksMhIK", title: "Visual 35", category: "other", description: "ARCHIVE", size: "wide" },
  { id: "1Z9JQINBDrBxxlpQsCrATPv9n_-ZV-eC7", title: "Visual 36", category: "other", description: "ARCHIVE", size: "" },
  { id: "1_nuOFCXFcMLZfKakxa1uG7nUY0XXSu7N", title: "Visual 37", category: "other", description: "ARCHIVE", size: "" },
  { id: "1TzFz6hcg5AxF2Bwb61j1Y2RUXWPNPb1M", title: "Visual 38", category: "other", description: "ARCHIVE", size: "" },
  { id: "1wxnUTl1g4HbQ9ZSwgc6mkTJkQ6S2c_U5", title: "Visual 39", category: "other", description: "ARCHIVE", size: "" },
  { id: "1s3S-1jepwIHV_dfv4DW9DZjj3tEZPoEZ", title: "Visual 40", category: "other", description: "ARCHIVE", size: "tall" }
];

const gallery = document.getElementById("gallery");
const count = document.getElementById("count");
const empty = document.getElementById("empty");
const lightbox = document.getElementById("lightbox");
const lightboxContainer = document.getElementById("lightbox-container");
const lightboxDownloadBtn = document.getElementById("lightbox-download");

let currentPhotoId = "";

function driveImage(id) {
  return `https://drive.google.com/thumbnail?id=${encodeURIComponent(id)}&sz=w1600`;
}

function driveVideo(id) {
  return `https://docs.google.com/uc?export=download&id=${encodeURIComponent(id)}`;
}

// DOWNLOAD DAN REDIRECT INSTAGRAM
function handleDownload(id) {
  const downloadUrl =
    `https://drive.google.com/uc?export=download&id=${encodeURIComponent(id)}`;

  window.open(downloadUrl, "_blank");

  setTimeout(() => {
    window.location.href =
      "https://www.instagram.com/anothervisual_creative/";
  }, 300);
}

function renderPhotos(filter = "all") {
  const filtered = photos.filter(photo =>
    filter === "all" || photo.category === filter
  );

  gallery.innerHTML = "";
  empty.style.display = filtered.length ? "none" : "block";
  count.textContent =
    `${String(filtered.length).padStart(2, "0")} PHOTOGRAPHS`;

  filtered.forEach((photo, index) => {
    const card = document.createElement("article");
    card.className = "photo";
    card.style.animationDelay = `${index * 70}ms`;

    let mediaElement;

    if (photo.type === "video") {
      mediaElement = document.createElement("video");
      mediaElement.src = driveVideo(photo.id);
      mediaElement.muted = true;
      mediaElement.loop = true;
      mediaElement.playsInline = true;
      mediaElement.preload = "metadata";
    } else {
      mediaElement = document.createElement("img");
      mediaElement.src = driveImage(photo.id);
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
      handleDownload(photo.id);
    });

    card.append(mediaElement, info, download);

    // BUKA FOTO ATAU VIDEO
    card.addEventListener("click", () => {
      currentPhotoId = photo.id;

      const existingMedia =
        lightboxContainer.querySelector("img, video");

      if (existingMedia) existingMedia.remove();

      if (photo.type === "video") {
        const vEl = document.createElement("video");
        vEl.src = driveVideo(photo.id);
        vEl.controls = true;
        vEl.autoplay = true;

        lightboxContainer.insertBefore(vEl, lightboxDownloadBtn);
      } else {
        const imgEl = document.createElement("img");
        imgEl.src = driveImage(photo.id);
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
