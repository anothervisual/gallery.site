
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Gallery — Visual Archive</title>

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
  background: radial-gradient(circle,
    rgba(214,183,131,.09), transparent 70%);
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

.gallery {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  grid-auto-rows: 245px;
  gap: 15px;
}

.photo {
  position: relative;
  overflow: hidden;
  background: var(--panel);
  cursor: pointer;
  border-radius: 3px;
  animation: reveal .65s ease both;
}

.photo.tall { grid-row: span 2; }
.photo.wide { grid-column: span 2; }

.photo img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  transition: transform .7s cubic-bezier(.2,.7,.2,1),
              filter .5s;
}

.photo::after {
  content: "";
  position: absolute;
  inset: 0;
  background: linear-gradient(
    to top, rgba(0,0,0,.85), transparent 55%);
  opacity: .8;
  transition: .3s;
  pointer-events: none;
}

.photo:hover img {
  transform: scale(1.06);
  filter: brightness(.8);
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

.lightbox img {
  max-width: 100%;
  max-height: 85vh;
  object-fit: contain;
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

@media (max-width: 760px) {
  nav { height: 65px; padding: 0 5%; }
  .hero { padding: 75px 5% 50px; }
  .hero-bottom { align-items: start; flex-direction: column; }
  .gallery-section { padding: 0 5% 65px; }
  .gallery {
    grid-template-columns: repeat(2, minmax(0, 1fr));
    grid-auto-rows: 190px;
    gap: 9px;
  }
  .photo-info { left: 11px; right: 11px; bottom: 12px; }
  .photo-info h3 { font-size: 15px; }
  .photo-info p { font-size: 9px; letter-spacing: 1px; }
  .zoom { width: 27px; height: 27px; font-size: 15px; }
  .toolbar { align-items: start; flex-direction: column; }
}

@media (max-width: 420px) {
  .gallery { grid-auto-rows: 155px; }
  .photo.tall { grid-row: span 2; }
  .photo-info h3 { font-size: 13px; }
}
</style>
</head>

<body>

<nav>
  <a href="#" class="logo">VISUAL<span>.</span>ARCHIVE</a>
  <div class="nav-label">Photography Portfolio</div>
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
      <button class="filter" data-filter="nature">Nature</button>
      <button class="filter" data-filter="portrait">Portrait</button>
      <button class="filter" data-filter="street">Street</button>
      <button class="filter" data-filter="other">Lainnya</button>
    </div>
  </div>

  <div class="gallery" id="gallery"></div>
  <div class="empty" id="empty">Belum ada foto dalam kategori ini.</div>
</main>

<footer>
  <div>© 2026 <span>VISUAL.ARCHIVE</span></div>
  <div>CAPTURED WITH INTENTION.</div>
</footer>

<div class="lightbox" id="lightbox" role="dialog"
     aria-modal="true" aria-label="Pratinjau foto">
  <button class="close" id="close" aria-label="Tutup">&times;</button>
  <img id="lightbox-img" src="" alt="Foto dalam ukuran besar">
</div>

<script>
// ============================================
// MASUKKAN FOTO GOOGLE DRIVE KAMU DI SINI
// ============================================

const photos = [
  {
    id: "1UUFY5cjJVWRZcpjdXHUkh-ofB7OL7byJ",
    title: "Captured Moment",
    category: "other",
    description: "PERSONAL COLLECTION",
    size: "tall"
  },

  // Tambahkan foto lainnya dengan format yang sama:
  // {
  //   id: "ID_FOTO_GOOGLE_DRIVE",
  //   title: "Nama Foto",
  //   category: "nature",
  //   description: "PHOTO SERIES",
  //   size: ""
  // },
];

const gallery = document.getElementById("gallery");
const count = document.getElementById("count");
const empty = document.getElementById("empty");
const lightbox = document.getElementById("lightbox");
const lightboxImg = document.getElementById("lightbox-img");

function driveImage(id) {
  return `https://drive.google.com/thumbnail?id=${encodeURIComponent(id)}&sz=w1600`;
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
    card.className = "photo " + (photo.size || "");
    card.style.animationDelay = `${index * 70}ms`;

    const img = document.createElement("img");
    img.src = driveImage(photo.id);
    img.alt = photo.title;
    img.loading = "lazy";
    img.onerror = () => {
      img.alt = "Foto tidak dapat dimuat. Periksa akses Google Drive.";
      img.style.opacity = ".15";
    };

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
    zoom.setAttribute("aria-hidden", "true");

    info.append(details, zoom);
    card.append(img, info);

    card.addEventListener("click", () => {
      lightboxImg.src = driveImage(photo.id);
      lightbox.classList.add("open");
    });

    gallery.appendChild(card);
  });
}

document.querySelectorAll(".filter").forEach(button => {
  button.addEventListener("click", () => {
    document.querySelector(".filter.active")
      ?.classList.remove("active");

    button.classList.add("active");
    renderPhotos(button.dataset.filter);
  });
});

function closeLightbox() {
  lightbox.classList.remove("open");
  lightboxImg.src = "";
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
