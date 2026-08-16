<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#050505">
<title>Another Visual — HUT RI 81</title>

<style>
*{margin:0;padding:0;box-sizing:border-box}
html{scroll-behavior:smooth}
body{
    font-family:Arial,Helvetica,sans-serif;
    background:#050505;
    color:#fff;
    overflow-x:hidden;
}

header{
    position:fixed;
    top:0;left:0;right:0;
    height:72px;
    padding:0 5%;
    display:flex;
    align-items:center;
    justify-content:space-between;
    background:rgba(5,5,5,.78);
    backdrop-filter:blur(18px);
    -webkit-backdrop-filter:blur(18px);
    border-bottom:1px solid rgba(255,255,255,.08);
    z-index:1000;
}
.logo{font-size:18px;font-weight:800;letter-spacing:3px}
.logo span{font-weight:400;opacity:.5}
.clock-mini{font-family:monospace;font-size:13px;letter-spacing:2px;color:#ddd}

.hero{
    min-height:100vh;
    padding:120px 20px 80px;
    display:flex;
    align-items:center;
    justify-content:center;
    text-align:center;
    position:relative;
    overflow:hidden;
}
.hero::before{
    content:"";
    position:absolute;
    width:720px;height:720px;
    left:50%;top:-330px;
    transform:translateX(-50%);
    background:radial-gradient(circle,rgba(210,0,0,.20),transparent 68%);
    pointer-events:none;
}
.hero-content{position:relative;z-index:2;max-width:900px}
.kicker{font-size:11px;letter-spacing:7px;color:#999;margin-bottom:24px}
.hero h1{
    font-size:clamp(58px,11vw,135px);
    line-height:.88;
    letter-spacing:-6px;
    font-weight:900;
}
.hero h1 span{display:block;color:#e50914}
.red-line{width:65px;height:3px;background:#e50914;margin:28px auto}
.greeting{
    max-width:700px;
    margin:auto;
    color:#aaa;
    font-size:16px;
    line-height:1.9;
}
.live-clock{
    margin:38px auto 0;
    display:inline-flex;
    flex-direction:column;
    gap:8px;
    padding:18px 30px;
    border:1px solid rgba(255,255,255,.12);
    background:rgba(255,255,255,.025);
    box-shadow:0 20px 80px rgba(0,0,0,.35);
}
.clock-label{font-size:9px;letter-spacing:4px;color:#666}
.clock{
    font-family:monospace;
    font-size:clamp(28px,5vw,48px);
    letter-spacing:4px;
    font-weight:700;
}

.gallery-section{padding:100px 5% 120px}
.section-heading{max-width:1500px;margin:0 auto 45px}
.section-kicker{color:#e50914;font-size:10px;font-weight:700;letter-spacing:5px;margin-bottom:14px}
.section-heading h2{font-size:clamp(35px,5vw,64px);letter-spacing:-2px}
.section-heading p{margin-top:12px;color:#666;font-size:13px}

.gallery{
    max-width:1500px;
    margin:auto;
    display:grid;
    grid-template-columns:repeat(auto-fill,minmax(250px,1fr));
    gap:10px;
}
.photo-card{
    position:relative;
    aspect-ratio:4/3;
    overflow:hidden;
    background:#111;
    cursor:pointer;
    border-radius:3px;
}
.photo-card img{
    width:100%;height:100%;
    display:block;
    object-fit:cover;
    transition:transform .6s cubic-bezier(.2,.7,.2,1),filter .4s ease;
}
.photo-card:hover img{transform:scale(1.06);filter:brightness(.68)}
.photo-overlay{
    position:absolute;inset:0;
    display:flex;
    align-items:flex-end;
    justify-content:space-between;
    padding:16px;
    background:linear-gradient(transparent 45%,rgba(0,0,0,.75));
    opacity:0;
    transition:.3s;
}
.photo-card:hover .photo-overlay{opacity:1}
.photo-number,.view-text{font-size:10px;letter-spacing:2px}
.view-text{color:#ddd}

.viewer{
    position:fixed;inset:0;
    display:none;
    align-items:center;
    justify-content:center;
    padding:25px;
    background:rgba(0,0,0,.97);
    z-index:3000;
}
.viewer.active{display:flex}
.viewer-image{
    max-width:94vw;
    max-height:86vh;
    object-fit:contain;
    box-shadow:0 30px 100px rgba(0,0,0,.8);
}
.close-viewer{
    position:absolute;
    top:24px;right:28px;
    width:45px;height:45px;
    border:1px solid rgba(255,255,255,.18);
    border-radius:50%;
    background:rgba(0,0,0,.5);
    color:#fff;
    font-size:23px;
    cursor:pointer;
}
.viewer-bottom{
    position:absolute;
    bottom:22px;left:50%;
    transform:translateX(-50%);
    display:flex;
    align-items:center;
    gap:12px;
}
.viewer-counter{font:11px monospace;color:#777;letter-spacing:2px}
.download-button{
    border:0;
    background:#fff;
    color:#000;
    padding:13px 19px;
    font-size:10px;
    font-weight:700;
    letter-spacing:1px;
    cursor:pointer;
}
.download-button:hover{background:#e50914;color:#fff}

.modal{
    position:fixed;inset:0;
    display:none;
    align-items:center;
    justify-content:center;
    padding:20px;
    background:rgba(0,0,0,.84);
    backdrop-filter:blur(16px);
    z-index:4000;
}
.modal.active{display:flex}
.modal-box{
    width:min(430px,100%);
    padding:38px 30px;
    text-align:center;
    background:#111;
    border:1px solid rgba(255,255,255,.1);
}
.modal-box h3{font-size:25px;margin-bottom:12px}
.modal-box p{color:#777;font-size:13px;line-height:1.7;margin-bottom:25px}
.actions{display:flex;justify-content:center;gap:10px}
.btn{padding:13px 20px;border:0;cursor:pointer;font-size:10px;font-weight:700;letter-spacing:1px}
.primary{background:#fff;color:#000}
.secondary{background:#222;color:#aaa}

.thankyou{
    position:fixed;inset:0;
    display:none;
    align-items:center;
    justify-content:center;
    padding:20px;
    background:rgba(0,0,0,.92);
    backdrop-filter:blur(20px);
    z-index:5000;
}
.thankyou.active{display:flex}
.thankyou-box{max-width:550px;text-align:center}
.check{
    width:68px;height:68px;
    margin:0 auto 24px;
    display:flex;align-items:center;justify-content:center;
    border:2px solid #e50914;border-radius:50%;
    color:#e50914;font-size:28px;
}
.thankyou-box h2{font-size:36px;margin-bottom:12px}
.thankyou-box p{color:#777;font-size:13px;line-height:1.8}
.stars{margin-top:25px;display:flex;justify-content:center;gap:7px}
.star{border:0;background:none;color:#444;font-size:29px;cursor:pointer}
.star.active,.star:hover{color:#fff}

footer{
    padding:60px 20px 40px;
    text-align:center;
    border-top:1px solid rgba(255,255,255,.07);
}
.footer-brand{font-size:14px;font-weight:800;letter-spacing:4px}
.footer-text{margin-top:12px;color:#555;font-size:11px;line-height:1.8}
.footer-ri{margin-top:25px;color:#e50914;font-size:11px;letter-spacing:4px}

@media(max-width:700px){
    header{height:62px;padding:0 18px}
    .logo{font-size:13px}
    .clock-mini{font-size:10px}
    .hero{padding:90px 18px 60px}
    .hero h1{letter-spacing:-3px}
    .greeting{font-size:14px}
    .gallery-section{padding:70px 12px 90px}
    .gallery{grid-template-columns:repeat(2,1fr);gap:5px}
    .photo-overlay{opacity:1;padding:9px}
    .view-text{display:none}
    .viewer{padding:10px}
    .viewer-image{max-width:100%;max-height:80vh}
    .viewer-bottom{bottom:14px}
}
</style>

<style>
.device-info-panel{
    position:fixed;
    left:18px;
    bottom:18px;
    z-index:9998;
    width:min(360px,calc(100vw - 36px));
    padding:16px;
    border:1px solid rgba(255,255,255,.12);
    border-radius:18px;
    background:rgba(10,10,10,.88);
    backdrop-filter:blur(18px);
    -webkit-backdrop-filter:blur(18px);
    color:#fff;
    box-shadow:0 18px 50px rgba(0,0,0,.35);
    font-family:inherit;
    display:none;
}
.device-info-panel.show{display:block}
.device-info-panel .device-title{
    font-weight:800;
    font-size:13px;
    letter-spacing:.12em;
    text-transform:uppercase;
    margin-bottom:10px;
}
.device-info-grid{
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:7px 14px;
    font-size:11px;
    line-height:1.45;
}
.device-info-grid span{
    color:rgba(255,255,255,.58);
}
.device-info-grid b{
    display:block;
    font-weight:600;
    overflow:hidden;
    text-overflow:ellipsis;
    white-space:nowrap;
}
.device-close{
    position:absolute;
    top:8px;
    right:10px;
    width:26px;
    height:26px;
    border:0;
    border-radius:50%;
    background:rgba(255,255,255,.08);
    color:#fff;
    cursor:pointer;
}
.device-badge{
    display:inline-flex;
    align-items:center;
    gap:6px;
    margin-top:10px;
    padding:6px 9px;
    border-radius:999px;
    background:rgba(255,255,255,.07);
    font-size:10px;
}
.device-dot{
    width:6px;
    height:6px;
    border-radius:50%;
    background:#43d17a;
}
@media(max-width:600px){
    .device-info-panel{
        left:10px;
        bottom:10px;
        width:calc(100vw - 20px);
    }
}
</style>

</head>

<body>

<header>
    <div class="logo">ANOTHER <span>VISUAL</span></div>
    <div class="clock-mini" id="miniClock">00:00:00</div>
</header>

<section class="hero">
    <div class="hero-content">
        <div class="kicker">ANOTHER VISUAL PRESENTS</div>

        <h1>HUT RI <span>81</span></h1>

        <div class="red-line"></div>

        <p class="greeting">
            Dirgahayu Republik Indonesia.
            Semoga semangat kemerdekaan terus menyala,
            mempererat persatuan, dan menginspirasi kita
            untuk terus berkarya, berbagi, dan melangkah bersama.
        </p>

        <div class="live-clock">
            <div class="clock-label">WAKTU SEKARANG</div>
            <div class="clock" id="mainClock">00:00:00</div>
        </div>
    </div>
</section>

<section class="gallery-section">
    <div class="section-heading">
        <div class="section-kicker">ANOTHER VISUAL</div>
        <h2>Visual Memories</h2>
        <p>Kumpulan momen yang diabadikan dalam sebuah cerita visual.</p>
    </div>

    <div class="gallery" id="gallery"></div>
</section>

<div class="viewer" id="viewer">
    <button class="close-viewer" onclick="closeViewer()">×</button>
    <img id="viewerImage" class="viewer-image" src="" alt="Another Visual">
    <div class="viewer-bottom">
        <div class="viewer-counter" id="viewerCounter">001</div>
        <button class="download-button" onclick="openDownload()">DOWNLOAD FOTO</button>
    </div>
</div>

<div class="modal" id="downloadModal">
    <div class="modal-box">
        <h3>Download Foto?</h3>
        <p></p>
        <div class="actions">
            <button class="btn primary" onclick="downloadPhoto()">YA, DOWNLOAD</button>
            <button class="btn secondary" onclick="closeDownload()">BATAL</button>
        </div>
    </div>
</div>

<div class="thankyou" id="thankyou">
    <div class="thankyou-box">
        <div class="check">✓</div>
        <h2>Terima Kasih</h2>
        <p>
            Terima kasih telah menikmati karya visual
            dari Another Visual.
        </p>

        <div class="stars">
            <button class="star" onclick="rate(1)">★</button>
            <button class="star" onclick="rate(2)">★</button>
            <button class="star" onclick="rate(3)">★</button>
            <button class="star" onclick="rate(4)">★</button>
            <button class="star" onclick="rate(5)">★</button>
        </div>
    </div>
</div>

<footer>
    <div class="footer-brand">ANOTHER VISUAL</div>
    <div class="footer-text">Photography & Visual Documentation</div>
    <div class="footer-ri">DIRGAHAYU REPUBLIK INDONESIA</div>
</footer>

<script>
const photoIds = [
    "1_1kCiUQRi5xT4BjsoF1PadjsBUBUpIcC",
    "16iMzxCkegmddixVjUUvUXRD_JYuTgpsP",
    "1wgm09fbLeIVydJ02bnGFuHzUPLarc5Js",
    "1BUfsVdyQBoKwA5tGXXvHJ-G9peSU9RHm",
    "1kEo8o-I15M4JyDV-j889uXMLnbIBkABv",
    "1IJhYmaMyvpU6w2SQAUCQSU8TBlFpadNF",
    "1R-vRUmCugaxBhDn5qpEJ5nQKdjrrblxY",
    "1DBmiC4tBasxCIKERIK1eBEVQEj03CkKc",
    "1HsnSh26roOO27CDzq_6qgnbXsuDg6MxR",
    "1BAWiJ-3aJHDe91p8tKHf-EQiJpIwlAqH",
    "1L0lIkeJDhGDqHbMdXRWex3G9gEiKUMVc",
    "1hvQfyMqGFLTeWtugTA5NKH3b9XLw2YLF",
    "1ou3Lhr30N_Q3Dwu2tIyfncYGvPh3qd0a",
    "1_xr5Z2MxkPWGj-qFIvMn0BOR7TfJ2ZW-",
    "1Y6xM3lBMnhKQxUnLKy-Pid3UJ9SfTHXI",
    "1XTD3suCrR-BRwlLmOoS2XILj8kJybwXH",
    "10fFX4wUsU9t4HQtzsvNS0L-OK24OuJbH",
    "1WP4sU52yKno_nTBCURd37a_cgMQUJmYP",
    "19a5-ni0Lx7o4RmMRcSgjvTj1Zmzwd_2P",
    "1Z5wINLQpQHO6Lb5bKZwncX_AC2IikmAN",
    "1MBLFcaQ-RrKnTFUmd9MUTOwg9WWQhL_a",
    "1BPM5nBjv2aER9hpACCqmjuJ8mk8Ncbv5",
    "16f7SEOZ4EDV6ehdOm2s6x_DQBzPgrp0L",
    "1ksGVF_gVQr9vxOKJS8yYTvy3jBltXFBp",
    "1KN-OrY0ao-h5tHQglPT8gfDEmW2SbqhH",
    "1Qb3vVdhwXhj23z3lCufpBYuwwULI9Uid",
    "18EFxE7-JBYE_lY_di7wjUsB4XhFUEWOe",
    "1BKYI4ZszjOCygVnsSX4WpojABJveSijp",
    "1WsjY19mhc3uH0MaBcogj5D2TloLn_iVt",
    "1OzSHsXeJL-LtmCJrRIwFXSahiA0MNyIU",
    "1p9ocOtiQ9k1yI2oxFr9sYyt-QnIYBgNy",
    "10REORnbDyCs2xz1YghIatjZzn-UaZ7TK",
    "1Nt4mnxWoqhLEvxra0MKBYpYERhj0D6P5",
    "1quzNLIy9iEw9tTg-vFq3eYvTRDskF5VW",
    "1w_ykfF1D7_6I5ph7tTO-Z88otFOY68et",
    "1nGcbi9bUe_V_RYLnsUssTszSK86c2tAO",
    "16DzZYdVSerSXOs2kzabEKdnLr5H__dKx",
    "1vxVB0gaEpS_kNOKdb59Q9gGqWIXzHSDc",
    "1AMb3nY05QAZRZeBMufDh5PnPXNT6OgMQ",
    "1BvDgREO5nroHtkMj9BzxNRO37-M9Rz0v",
    "1mi7syF7u5WMfDzKYHKmXLMtKshsbIRYc",
    "1ACV_Fgzk1vF9Ymz-wM7kwdIQ4fwd7qOW",
    "1a1wxyCQwc7Z5wWEpk7u9GI6nfYED1ZIu",
    "1Bm1SKB9PKfaE6ash-w5I6F2HlnbeVnUX",
    "1ReU_-Zn2fIN-zni5EH-5B_NInYIsoRob",
    "19b_G445G-e8bU4sG5gbkX_amygajjJQC",
    "1MAsBK3l3tTcVqAhuMfTv145SB3C9hO3a",
    "1_8SV1EpfleajcKm1XPAnekv6juA7kEmS",
    "1nI3uJq-BOznI7JaWToAGyDJniffaW-fB",
    "13CBl3RMWjsdogXUTRk9jlDVb8iV5PRae",
    "121AdnuP6cujx3HMAZiA4zplQT_pyyIfn",
    "1RyodPozF9IVoG1H-Xx0-mmWf1OB9K0XX",
    "1FAV_IMxDvTHHfLpV44UNOnm1WKAI437t",
    "1MFb29hD1wbO_kBcIOByfwCRhe2DbEUyx",
    "1lPFgfWairzbmTsvTSRAWpTd9FyHxw4MO",
    "1vJ_n6HIcU0cG6bCD5OIPe6aU3rtz2Mdq",
    "1Xx8UKiEPpUBgdx9NfHhXlf5FBRcwTqkc",
    "1SEfHoBfbcc67cK-wNh6CxFbHMFWFRP19",
    "1nqVkF9kFeZAN75Di6QlWfG2G82gwTJEf",
    "1xb84_Mt7Hh47t49bnARFl3LUE8Y5cisR",
    "1egAJzZEChTCPtAf9KD5CZaUyVzDoKt2J",
    "1u9itdMd3iSNSYI97L3GpdjIQmUVXC-FQ",
    "1EAwQNEt9De-f0TP-3XuZPDI__GcFKAPl",
    "1-kdJAl5aSBpU29D8ln90IzQQKeRlZnh1",
    "1yxXOmr5uPa1cGmLXKbOrNwPPjB_gVVtk",
    "1JjoLZ_B_HJ1eQSywI0GjQDB3YiYaHgFx",
    "1hL4PbOcgnjFa1BZqDg3E6j6qjQ3ILHqs",
    "1XgQ7RFdBmkS0p2A13FbV-12QMntaviyX",
    "1UnWcrToNV1aFpRyh2FeuOElFQm1_AcuY",
    "1utiJw-NYs39b3WrpI7l9KodUd4bH__O8",
    "1XRYG0ijox6MLURw5pA30DfEjN_xmAliG",
    "1xRES5c6ZySg7tK5sPOB11tz9MmWQfElC",
    "1i4lCZoBzMGCN0jAWfmDwzB4fcA27v2LP",
    "10bST5Y2zUv3cma0UW0LWXm-Hg8bA-IZf",
    "1eGAAoyp7SxgQBWoEbSvR6hURRzZzRUVR",
    "1GY4dyvmy77DceLAeYbpwKGdj8xAp7fVM",
    "1UbuFZQruoKFM9upXXY5FnBoMSafYovYB",
    "1zoJSIyUuTr4BxfWpPwrqfZwxccUioZAd",
    "1WDt8GBr4eQcDp3F24SykMnwUSy8II_DP",
    "182c8pBYV5a6LwKtjdcyGSdDkoqGPSf_5",
    "1gs7aCokfhPBNaZvwhAQR_f75ECeRuKD9",
    "1jDJ-nI6ZHZyNcoC3gG7A5nwPeVgm-Ic3",
    "1sbn9wly0GzEXCag5L09V89QzjSVESMzA",
    "110Ixcglo_2Lxhrr1S81S_6syXjTuK0uz",
    "1O1Kitya7GYJNLy_YNTIf1NTd69Mt1XLh",
    "1h9v69hsDUJk6i3tqMbTplD8rZ7Vfq49-",
    "13mFbwr4uLKlBlDQnxqv9JEnyLFL_o9LY",
    "1ltDn84EI7XM4wH7TyFchFJiQcmizAR6b",
    "1xHN1AEcqLavv6ugPWc7HRHvRwpF4RqKA",
    "1iHtmIoZzD-D40T9ZP7L47cZ2dRBA7Bzc",
    "1v0fNFmko6KF_FBjf9QBtJMd4UZIkUa3j",
    "1v0axrFjT6t5ptqOYb9HOVMxLi4TEmm0d",
    "1pEOayGMEfUi1Q3O43kuSuFwMI35q5-sv",
    "1_c7GHcLI1nEGleG_CtGne36LFB9c6m8x",
    "1ZleTY_frj_TwoBOmKnIEsmcOiJg7LSDO",
    "1hzfsxfxHqfNrm6_0UwQ8Amz2y71VOFG8",
    "1MzOkRsD3eNykaJFpoYxEJZmv_MBqpWHo",
    "1u2LtQe-MgRqr9-FpKvXIlj2qr5kc1Tyb",
    "1_knRVZTjtzamp9AXNAIgFIKycaVTWsPh",
    "1EECiNmkIdkPqJltLYgpjPlJFc9hQkNBJ",
    "1xytnaN8aDT0TErced300tt7FyoEqN1o8",
    "1-Ua4EazC9KQE7ql4qMZclezrPZZtxAPk",
    "1-Hzs_QXRTWB9iorLOV00MJBVUUy5LCIp",
    "1-A61fLC-TbBl5LTT6NVjGm_YT1tPFZXr",
    "1f9ep5m7GkxsC9YIiPtRRR7t3m9hoPwIg",
    "1VAqHmp8voDG5PUjYtC4yew0EEqD8zzjh",
    "1jiwMayZu-nMiswuBqDyZx7l0gKTRwHVY",
    "11XNHhtbW0s6Z7THG2IVlAT6K3Jc0fXZ4",
    "1ah6dx863VV1k2dgjoMIUeB8VlW7GkTgL",
    "1r9xRZH9mtJuQd7uLx8nzfhn9mSaCP0Bl",
    "191YfW7MRocGiDKvjmv6Zrzx3pWnctVPJ",
    "16t2XgFf_2-XsWVReHTmQlYa7o9n5KheE",
    "1IKq0bOOwRpaviYZ6HG_-BNhK6H8hV2SF",
    "1dgEzpPpd4ADujN_vU1nHX7D_RexSoChO",
    "1xSrFTjX4L5Le9UqkhSCD0Pu_An-aOhnk",
    "10xjUQ7irtuIwMFT4efck1DHshvEYVQNT",
    "1v_IcoqUxfJInHAAxHaUypbZYmycyvjhH",
    "1dHR5GlzRReIdeYYl7G-fzlnpOEXjDuy_",
    "1PrXpGMonIVr2vrGEuFsEGDq4ToyU-ESG",
    "10IHv_VCdQHGmh0B1F1qpxMhj96RFIa-n",
    "1Km4f3bIC0SVqtZoEW3ZPn5wefQk-keP-",
    "1XYBYcCVh77YVI5XPs0f_zTQfPRTcI2kV",
    "1sx0kfoRiiGMGNBKEFOmsBSMTnN4M0QK1",
    "15_nx6yagvLluUuMbMMHxNWs5JTKfWVxs",
    "1beiUDjbJUVo6Of1GGdTFkn_w_WFAes5c",
    "1yiT1ly6sLKgHZvG9dcT-SdHerHvFrU3t",
    "1HjOr4Ozy08YUIKnIRxIt_rPxKkdcN9qF",
    "1OKIVcxFiaRbt_JGU_uBj2VmnRz62gRew",
    "1kIJVGdzuGLHo7Mrl-iUTjym-SmsXxudY",
    "1sSo6NfEu7pXuj-nbLg_o-eC3ihfdBLUV",
    "1GRk-g9PH33K8KjG_d-_LpVW-sQ8GRjP7",
    "1r-vN_ZkOlholqOTR67shNp5v1b1j8HM2",
    "1_R_5F0cIi8fyS_8fIacRRRZdvac6pbsb",
    "1F7NOxS8wb1eMDK2tN1TuFP3di07XfQDZ",
    "1cg8lvIsZjBdeVrRrmAAzptNzXDvlWgk4",
    "1_evg_SLaEhOY68KS6iL_UFyVUdcNVgHR",
    "1txWOuWLxiqV7zLzh6V8eaayguv_sWk44",
    "1cItHfO62Es6PzfvvuZm9yXLPYG7Zk6Ft",
    "1tkQl2t3SHVOe3SzIIzw_AAaOtiI24YM0",
    "1BvIGAMBU3DTnzCd44M3QsPlS39T7_72W",
    "1zRppt_WVmN0g0qFFT8qPx6rPI55K1vy4",
    "1orpGC48MezEMkgeJDZ-n_UqiBt8g64PG",
    "1HQgp1PYQaU_7bL5UMfWk-rTOC23nteWW"
];

let currentPhoto = null;
let currentIndex = 0;

const gallery = document.getElementById("gallery");
const viewer = document.getElementById("viewer");
const viewerImage = document.getElementById("viewerImage");
const viewerCounter = document.getElementById("viewerCounter");
const downloadModal = document.getElementById("downloadModal");
const thankyou = document.getElementById("thankyou");

function driveImage(id){
    return "https://drive.google.com/thumbnail?id=" + id + "&sz=w2000";
}

function driveDownload(id){
    return "https://drive.google.com/uc?export=download&id=" + id;
}

function updateClock(){
    const now = new Date();
    const h = String(now.getHours()).padStart(2,"0");
    const m = String(now.getMinutes()).padStart(2,"0");
    const s = String(now.getSeconds()).padStart(2,"0");
    const time = h + ":" + m + ":" + s;

    document.getElementById("mainClock").textContent = time;
    document.getElementById("miniClock").textContent = time;
}

setInterval(updateClock,1000);
updateClock();

function renderGallery(){
    gallery.innerHTML = "";

    photoIds.forEach((id,index)=>{
        const card = document.createElement("div");
        card.className = "photo-card";

        const img = document.createElement("img");
        img.loading = "lazy";
        img.alt = "Another Visual " + (index + 1);
        img.src = driveImage(id);

        img.onerror = function(){
            if(!this.dataset.retry){
                this.dataset.retry = "1";
                this.src = "https://drive.google.com/thumbnail?id=" + id + "&sz=w1600";
            }
        };

        const overlay = document.createElement("div");
        overlay.className = "photo-overlay";

        const number = document.createElement("div");
        number.className = "photo-number";
        number.textContent = String(index + 1).padStart(3,"0");

        const view = document.createElement("div");
        view.className = "view-text";
        view.textContent = "LIHAT";

        overlay.appendChild(number);
        overlay.appendChild(view);
        card.appendChild(img);
        card.appendChild(overlay);

        card.onclick = () => openViewer(id,index);
        gallery.appendChild(card);
    });
}

function openViewer(id,index){
    currentPhoto = id;
    currentIndex = index;
    viewerImage.src = driveImage(id);
    viewerCounter.textContent =
        String(index + 1).padStart(3,"0") +
        " / " + photoIds.length;
    viewer.classList.add("active");
    document.body.style.overflow = "hidden";
}

function closeViewer(){
    viewer.classList.remove("active");
    document.body.style.overflow = "";
}

function openDownload(){
    if(currentPhoto) downloadModal.classList.add("active");
}

function closeDownload(){
    downloadModal.classList.remove("active");
}

async function downloadPhoto(){
    if(!currentPhoto) return;

    const url = driveImage(currentPhoto);
    closeDownload();

    try {
        const response = await fetch(url, {mode:"cors"});
        if(!response.ok) throw new Error("Download gagal");

        const blob = await response.blob();
        const blobUrl = URL.createObjectURL(blob);

        const link = document.createElement("a");
        link.href = blobUrl;
        link.download =
            "Another-Visual-" +
            String(currentIndex + 1).padStart(3,"0") +
            ".jpg";

        document.body.appendChild(link);
        link.click();
        link.remove();

        setTimeout(() => URL.revokeObjectURL(blobUrl), 3000);

        setTimeout(() => {
            thankyou.classList.add("active");
        }, 700);

    } catch(error) {
        alert(
            "Foto belum bisa diunduh langsung dari halaman ini. " +
            "Sumber foto masih menggunakan Google Drive dan " +
            "Google Drive dapat membatasi download langsung dari website."
        );
    }
}

function nextPhoto(){
    if(currentIndex >= photoIds.length - 1) return;
    openViewer(photoIds[currentIndex + 1], currentIndex + 1);
}

function previousPhoto(){
    if(currentIndex <= 0) return;
    openViewer(photoIds[currentIndex - 1], currentIndex - 1);
}

function rate(value){
    localStorage.setItem("another_visual_rating",value);

    document.querySelectorAll(".star").forEach((star,index)=>{
        star.classList.toggle("active",index < value);
    });

    setTimeout(() => {
        thankyou.classList.remove("active");
    },1000);
}

document.addEventListener("keydown",(event)=>{
    if(event.key === "Escape"){
        closeViewer();
        closeDownload();
        thankyou.classList.remove("active");
    }
    if(event.key === "ArrowRight") nextPhoto();
    if(event.key === "ArrowLeft") previousPhoto();
});

viewer.addEventListener("click",(event)=>{
    if(event.target === viewer) closeViewer();
});

let touchStartX = 0;

viewer.addEventListener("touchstart",(event)=>{
    touchStartX = event.changedTouches[0].screenX;
},{passive:true});

viewer.addEventListener("touchend",(event)=>{
    const touchEndX = event.changedTouches[0].screenX;
    const diff = touchStartX - touchEndX;

    if(Math.abs(diff) < 50) return;

    if(diff > 0) nextPhoto();
    else previousPhoto();
},{passive:true});

renderGallery();


/* ============================
   ADVANCED DEVICE DETECTION
   ============================ */

function detectOS(ua){
    if(/Windows NT/i.test(ua)) return "Windows";
    if(/Android/i.test(ua)) return "Android";
    if(/iPhone|iPad|iPod/i.test(ua)) return "iOS";
    if(/Mac OS X/i.test(ua)) return "macOS";
    if(/CrOS/i.test(ua)) return "ChromeOS";
    if(/Linux/i.test(ua)) return "Linux";
    return "Unknown";
}

function detectBrowser(ua){
    if(/Edg\//i.test(ua)) return "Microsoft Edge";
    if(/OPR\//i.test(ua)) return "Opera";
    if(/SamsungBrowser/i.test(ua)) return "Samsung Internet";
    if(/Firefox\//i.test(ua)) return "Mozilla Firefox";
    if(/CriOS\//i.test(ua)) return "Chrome iOS";
    if(/FxiOS\//i.test(ua)) return "Firefox iOS";
    if(/Chrome\//i.test(ua)) return "Google Chrome";
    if(/Safari\//i.test(ua) && !/Chrome|CriOS/i.test(ua)) return "Safari";
    return "Browser lain";
}

function detectDeviceType(ua){
    if(/iPad/i.test(ua)) return "Tablet · iPad";
    if(/Android/i.test(ua) && !/Mobile/i.test(ua)) return "Tablet · Android";
    if(/Mobile|iPhone|iPod|Android/i.test(ua)) return "Mobile";
    return "Desktop / Laptop";
}

function detectDeviceName(ua){
    if(/iPhone/i.test(ua)) return "Apple iPhone";
    if(/iPad/i.test(ua)) return "Apple iPad";
    if(/Android/i.test(ua)){
        const match = ua.match(/Android[^;)]*;\s*(?:[a-z]{2}-[A-Z]{2};\s*)?([^;)]+?)(?:\s+Build\/[^;)]*)?[;)]/i);
        if(match && match[1]) return match[1].trim();
        return "Android Device";
    }
    if(/Macintosh/i.test(ua)) return "Mac";
    if(/Windows/i.test(ua)) return "Windows PC";
    if(/CrOS/i.test(ua)) return "Chromebook";
    if(/Linux/i.test(ua)) return "Linux PC";
    return detectDeviceType(ua);
}

function getNetworkInfo(){
    const c = navigator.connection || navigator.mozConnection || navigator.webkitConnection;
    if(!c) return "Tidak tersedia";
    const type = c.effectiveType || c.type || "Unknown";
    const down = typeof c.downlink === "number" ? c.downlink + " Mbps" : "";
    return down ? type + " · " + down : type;
}

function getMemory(){
    return navigator.deviceMemory ? navigator.deviceMemory + " GB" : "Tidak tersedia";
}

function updateDeviceDetection(){
    const ua = navigator.userAgent || "";
    const screenText = `${screen.width} × ${screen.height}`;
    const viewportText = `${window.innerWidth} × ${window.innerHeight}`;
    const orientation = window.innerWidth >= window.innerHeight ? "Landscape" : "Portrait";
    const touch = navigator.maxTouchPoints > 0 ? "Ya" : "Tidak";
    const dpr = window.devicePixelRatio ? window.devicePixelRatio.toFixed(2) : "1";
    const cpu = navigator.hardwareConcurrency || "Tidak tersedia";
    const timezone = Intl.DateTimeFormat().resolvedOptions().timeZone || "Unknown";
    const device = detectDeviceName(ua);
    const type = detectDeviceType(ua);
    const os = detectOS(ua);
    const browser = detectBrowser(ua);

    const values = {
        diDevice: `${device} · ${type}`,
        diOS: os,
        diBrowser: browser,
        diScreen: screenText,
        diViewport: viewportText,
        diOrientation: orientation,
        diTouch: touch,
        diDpr: dpr,
        diCpu: String(cpu),
        diMemory: getMemory(),
        diNetwork: getNetworkInfo(),
        diTimezone: timezone,
        diMode: type
    };

    Object.keys(values).forEach(id => {
        const el = document.getElementById(id);
        if(el) el.textContent = values[id];
    });

    // Update when connection information changes, where supported.
    const connection = navigator.connection || navigator.mozConnection || navigator.webkitConnection;
    if(connection && !connection.__avBound){
        connection.addEventListener?.("change", updateDeviceDetection);
        connection.__avBound = true;
    }
}

function showDeviceInfo(){
    updateDeviceDetection();
    const panel = document.getElementById("deviceInfoPanel");
    if(panel){
        panel.classList.add("show");
        panel.setAttribute("aria-hidden","false");
    }
}

function hideDeviceInfo(){
    const panel = document.getElementById("deviceInfoPanel");
    if(panel){
        panel.classList.remove("show");
        panel.setAttribute("aria-hidden","true");
    }
}

/*
 * Device information is collected locally in the browser only.
 * It is not automatically sent to a server.
 * For testing, press D to toggle the panel.
 */
document.addEventListener("keydown", function(e){
    if(e.key.toLowerCase() === "d" && !["INPUT","TEXTAREA"].includes(document.activeElement?.tagName)){
        const panel = document.getElementById("deviceInfoPanel");
        if(panel?.classList.contains("show")) hideDeviceInfo();
        else showDeviceInfo();
    }
});

window.addEventListener("resize", updateDeviceDetection);
window.addEventListener("orientationchange", updateDeviceDetection);
document.addEventListener("DOMContentLoaded", updateDeviceDetection);

</script>


<div id="deviceInfoPanel" class="device-info-panel" aria-hidden="true">
    <button class="device-close" onclick="hideDeviceInfo()" aria-label="Tutup">×</button>
    <div class="device-title">Device Detection</div>
    <div class="device-info-grid">
        <div><span>Perangkat</span><b id="diDevice">-</b></div>
        <div><span>OS</span><b id="diOS">-</b></div>
        <div><span>Browser</span><b id="diBrowser">-</b></div>
        <div><span>Layar</span><b id="diScreen">-</b></div>
        <div><span>Viewport</span><b id="diViewport">-</b></div>
        <div><span>Orientasi</span><b id="diOrientation">-</b></div>
        <div><span>Touch</span><b id="diTouch">-</b></div>
        <div><span>DPR</span><b id="diDpr">-</b></div>
        <div><span>CPU Threads</span><b id="diCpu">-</b></div>
        <div><span>Memory</span><b id="diMemory">-</b></div>
        <div><span>Network</span><b id="diNetwork">-</b></div>
        <div><span>Timezone</span><b id="diTimezone">-</b></div>
    </div>
    <div class="device-badge"><i class="device-dot"></i><span id="diMode">Web visitor</span></div>
</div>

</body>
</html>
