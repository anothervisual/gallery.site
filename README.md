
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
    background:#050505;color:#fff;overflow-x:hidden
}
header{
    position:fixed;top:0;left:0;right:0;height:72px;padding:0 5%;
    display:flex;align-items:center;justify-content:space-between;
    background:rgba(5,5,5,.78);backdrop-filter:blur(18px);
    -webkit-backdrop-filter:blur(18px);border-bottom:1px solid rgba(255,255,255,.08);
    z-index:1000
}
.logo{font-size:18px;font-weight:800;letter-spacing:3px}
.logo span{font-weight:400;opacity:.5}
.clock-mini{font-family:monospace;font-size:13px;letter-spacing:2px;color:#ddd}

.hero{
    min-height:100vh;padding:120px 20px 80px;display:flex;align-items:center;
    justify-content:center;text-align:center;position:relative;overflow:hidden
}
.hero::before{
    content:"";position:absolute;width:720px;height:720px;left:50%;top:-330px;
    transform:translateX(-50%);
    background:radial-gradient(circle,rgba(210,0,0,.20),transparent 68%);
    pointer-events:none
}
.hero-content{position:relative;z-index:2;max-width:900px}
.kicker{font-size:11px;letter-spacing:7px;color:#999;margin-bottom:24px}
.hero h1{font-size:clamp(58px,11vw,135px);line-height:.88;letter-spacing:-6px;font-weight:900}
.hero h1 span{display:block;color:#e50914}
.red-line{width:65px;height:3px;background:#e50914;margin:28px auto}
.greeting{max-width:700px;margin:auto;color:#aaa;font-size:16px;line-height:1.9}
.live-clock{
    margin:38px auto 0;display:inline-flex;flex-direction:column;gap:8px;
    padding:18px 30px;border:1px solid rgba(255,255,255,.12);
    background:rgba(255,255,255,.025);box-shadow:0 20px 80px rgba(0,0,0,.35)
}
.clock-label{font-size:9px;letter-spacing:4px;color:#666}
.clock{font-family:monospace;font-size:clamp(28px,5vw,48px);letter-spacing:4px;font-weight:700}

.gallery-section{padding:100px 5% 120px}
.section-heading{max-width:1500px;margin:0 auto 45px}
.section-kicker{color:#e50914;font-size:10px;font-weight:700;letter-spacing:5px;margin-bottom:14px}
.section-heading h2{font-size:clamp(35px,5vw,64px);letter-spacing:-2px}
.section-heading p{margin-top:12px;color:#666;font-size:13px}
.gallery{
    max-width:1500px;margin:auto;display:grid;
    grid-template-columns:repeat(auto-fill,minmax(250px,1fr));gap:10px
}
.photo-card{
    position:relative;aspect-ratio:4/3;overflow:hidden;background:#111;
    cursor:pointer;border-radius:3px
}
.photo-card img{
    width:100%;height:100%;display:block;object-fit:cover;
    transition:transform .6s cubic-bezier(.2,.7,.2,1),filter .4s ease
}
.photo-card:hover img{transform:scale(1.06);filter:brightness(.68)}
.photo-overlay{
    position:absolute;inset:0;display:flex;align-items:flex-end;
    justify-content:space-between;padding:16px;
    background:linear-gradient(transparent 45%,rgba(0,0,0,.75));
    opacity:0;transition:.3s
}
.photo-card:hover .photo-overlay{opacity:1}
.photo-number,.view-text{font-size:10px;letter-spacing:2px}
.view-text{color:#ddd}

.viewer{
    position:fixed;inset:0;display:none;align-items:center;justify-content:center;
    padding:25px;background:rgba(0,0,0,.97);z-index:3000
}
.viewer.active{display:flex}
.viewer-image{
    max-width:94vw;max-height:86vh;object-fit:contain;
    min-width:1px;min-height:1px;
    box-shadow:0 30px 100px rgba(0,0,0,.8)
}
.close-viewer{
    position:absolute;top:24px;right:28px;width:45px;height:45px;
    border:1px solid rgba(255,255,255,.18);border-radius:50%;
    background:rgba(0,0,0,.5);color:#fff;font-size:23px;cursor:pointer;z-index:5
}
.viewer-bottom{
    position:absolute;bottom:22px;left:50%;transform:translateX(-50%);
    display:flex;align-items:center;gap:12px
}
.viewer-counter{font:11px monospace;color:#777;letter-spacing:2px}
.download-button{
    border:0;background:#fff;color:#000;padding:13px 19px;
    font-size:10px;font-weight:700;letter-spacing:1px;cursor:pointer
}
.download-button:hover{background:#e50914;color:#fff}

.nav-button{
    position:absolute;top:50%;transform:translateY(-50%);
    width:46px;height:46px;border:1px solid rgba(255,255,255,.15);
    border-radius:50%;background:rgba(0,0,0,.45);color:#fff;
    font-size:24px;cursor:pointer;z-index:5
}
.nav-button:hover{background:#fff;color:#000}
.prev-button{left:22px}.next-button{right:22px}

.modal{
    position:fixed;inset:0;display:none;align-items:center;justify-content:center;
    padding:20px;background:rgba(0,0,0,.84);backdrop-filter:blur(16px);z-index:4000
}
.modal.active{display:flex}
.modal-box{
    width:min(430px,100%);padding:38px 30px;text-align:center;
    background:#111;border:1px solid rgba(255,255,255,.1)
}
.modal-box h3{font-size:25px;margin-bottom:12px}
.modal-box p{color:#777;font-size:13px;line-height:1.7;margin-bottom:25px}
.actions{display:flex;justify-content:center;gap:10px}
.btn{padding:13px 20px;border:0;cursor:pointer;font-size:10px;font-weight:700;letter-spacing:1px}
.primary{background:#fff;color:#000}.secondary{background:#222;color:#aaa}

.thankyou{
    position:fixed;inset:0;display:none;align-items:center;justify-content:center;
    padding:20px;background:rgba(0,0,0,.92);backdrop-filter:blur(20px);z-index:5000
}
.thankyou.active{display:flex}
.thankyou-box{max-width:550px;text-align:center}
.check{
    width:68px;height:68px;margin:0 auto 24px;display:flex;
    align-items:center;justify-content:center;border:2px solid #e50914;
    border-radius:50%;color:#e50914;font-size:28px
}
.thankyou-box h2{font-size:36px;margin-bottom:12px}
.thankyou-box p{color:#777;font-size:13px;line-height:1.8}
.stars{margin-top:25px;display:flex;justify-content:center;gap:7px}
.star{border:0;background:none;color:#444;font-size:29px;cursor:pointer}
.star.active,.star:hover{color:#fff}

footer{
    padding:60px 20px 40px;text-align:center;
    border-top:1px solid rgba(255,255,255,.07)
}
.footer-brand{font-size:14px;font-weight:800;letter-spacing:4px}
.footer-text{margin-top:12px;color:#555;font-size:11px;line-height:1.8}
.footer-ri{margin-top:25px;color:#e50914;font-size:11px;letter-spacing:4px}

.device-info-panel{
    position:fixed;left:18px;bottom:18px;z-index:9998;
    width:min(360px,calc(100vw - 36px));padding:16px;
    border:1px solid rgba(255,255,255,.12);border-radius:18px;
    background:rgba(10,10,10,.88);backdrop-filter:blur(18px);
    -webkit-backdrop-filter:blur(18px);color:#fff;
    box-shadow:0 18px 50px rgba(0,0,0,.35);display:none
}
.device-info-panel.show{display:block}
.device-title{font-weight:800;font-size:13px;letter-spacing:.12em;text-transform:uppercase;margin-bottom:10px}
.device-info-grid{display:grid;grid-template-columns:1fr 1fr;gap:7px 14px;font-size:11px;line-height:1.45}
.device-info-grid span{color:rgba(255,255,255,.58)}
.device-info-grid b{display:block;font-weight:600;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.device-close{
    position:absolute;top:8px;right:10px;width:26px;height:26px;
    border:0;border-radius:50%;background:rgba(255,255,255,.08);color:#fff;cursor:pointer
}
.device-badge{
    display:inline-flex;align-items:center;gap:6px;margin-top:10px;
    padding:6px 9px;border-radius:999px;background:rgba(255,255,255,.07);font-size:10px
}
.device-dot{width:6px;height:6px;border-radius:50%;background:#43d17a}

.av-photo-loading{
    background:linear-gradient(90deg,rgba(255,255,255,.05),rgba(255,255,255,.12),rgba(255,255,255,.05));
    background-size:200% 100%;animation:avShimmer 1.2s linear infinite
}
@keyframes avShimmer{from{background-position:200% 0}to{background-position:-200% 0}}
.gallery img{content-visibility:auto}

@media(max-width:700px){
    header{height:62px;padding:0 18px}.logo{font-size:13px}.clock-mini{font-size:10px}
    .hero{padding:90px 18px 60px}.hero h1{letter-spacing:-3px}.greeting{font-size:14px}
    .gallery-section{padding:70px 12px 90px}.gallery{grid-template-columns:repeat(2,1fr);gap:5px}
    .photo-overlay{opacity:1;padding:9px}.view-text{display:none}
    .viewer{padding:10px}.viewer-image{max-width:100%;max-height:80vh}
    .viewer-bottom{bottom:14px}.nav-button{width:38px;height:38px;font-size:19px}
    .prev-button{left:8px}.next-button{right:8px}
}
@media(max-width:600px){
    .device-info-panel{left:10px;bottom:10px;width:calc(100vw - 20px)}
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

<div class="viewer" id="viewer" aria-hidden="true">
    <button class="close-viewer" onclick="closeViewer()" aria-label="Tutup">×</button>
    <button class="nav-button prev-button" onclick="previousPhoto()" aria-label="Foto sebelumnya">‹</button>
    <img id="viewerImage" class="viewer-image" src="" alt="Another Visual" decoding="async" fetchpriority="high">
    <button class="nav-button next-button" onclick="nextPhoto()" aria-label="Foto berikutnya">›</button>
    <div class="viewer-bottom">
        <div class="viewer-counter" id="viewerCounter">001 / 001</div>
        <button class="download-button" onclick="openDownload()">DOWNLOAD FOTO</button>
    </div>
</div>

<div class="modal" id="downloadModal"></p>
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
        <p>Terima kasih telah menikmati karya visual dari Another Visual.</p>
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

<script>
/* =========================================================
   GOOGLE DRIVE PHOTO IDS
   ========================================================= */
const photoIds = [
"1jrVbw3VbFPzOTp1crFjdi61RQ-9VDpsP",
"1Fobc6JJtVGg9LBcPrTIsDqzAAX3N_BVL",
"1mkzksU2C5_SzChjfjIarZoAWupttYw1C",
"1Pzs8yvONV2wnUTDXc6YZ5Rjo2GU2qr-b",
"1loDkjZZyl8DWzD8QT-GYrBABsBarsMKT",
"1iTmyOR0d1iJBDU1X7bBexH6YuIHnWTPh",
"1zO6ELF3J2BU8XOPaJ7u112gWMPWIn2l9",
"1tRRVCsG81VwOEGIxB5VyiRYkwy2nSI5a",
"1m1SRYWyeM2fYUv5XEtvEGUkcVkGJ6T9w",
"1kvzSYYzVqCzXB1DZzJl0hJLe0LwHprgl",
"1b6vIYD5taaXzYrzRhlb8y9vx3XYcffWB",
"1_LIKJmFsLfdPhiKOndFJ5nIu5nKoAa1K",
"1wGpYwoPQodFJ8prhuiZpz7K1yB_qp2mu",
"17l1A35ALKhgg5AI-P1t_t99wvYcK39Mm",
"1tAYjLdOzvtGgEz6RT51q7dEVW5tpOdrv",
"1qT-WFjWEE91K7XNc3IcQ8lvLt1zaX5Mp",
"1pYMvz1AWIoJL8XHFS1AJWe9a5sOWDAwj",
"1YBziaJgiGwk9rb8AY8OvuSseA5eVADdC",
"1DtS-5aLc77JTFqaN2yo6OkYvDsJsybow",
"1esWH9RJF1_aBImZTlGwsglTIsqr2FpGJ",
"1hjBtR_BuJa2mR2jB9E2jn0si4F7mz5Sh",
"1d9duPz6hMMjMQGijtbUwVvwBLAKMzjW7",
"1meOoKoTSLUxtKJudPz06k1Zjw5LJ_AGL",
"1MxNBwcG06CFie9-q4NQQRF-U58p_F5p0",
"1fWJ41tIEliYAQ77NG_-VpBzZcZUNdxUc",
"1BDz4UznuYdTuP3-d9VsLbGktUDAf-1Ac",
"1CoRWTKqbq3rzjSXhmPdaUHm4MphWAfom",
"1uxqTfMlPgh7Jg3lJQBSeMa0HCn9XwEdU",
"1DKdyKsKjVWHbDXS5259SvHr81AyVje_G",
"14WW-7-JyJmNL-0FxML7P0-3o2s_RJ9vb",
"1TRW3iFGK_8rYPSEMzCjPy4ZDdv28rYmb",
"1mdN_Y_qHPemyNrpl0SiY7c3ijW8UREW2",
"1rmE6sSxpwuOpTJVe2SmpTruDkAmUCCR7",
"1BIhQIJK49BrN8EdWrHALSF0TYIZKibJ-",
"1KgenXqavQbjro0sTz3R-3Al9Hj2_UCNv",
"1FKQS8fw5E_VHhCfjsG6c_JOqTKqiylz1",
"1IdANhY_Vqi9AiI6Nt51NKme4OOOC1qs4",
"1ctiZL0pWtxgdiA8anSGYzTdfpXzyXRTu",
"19O6lBqOOKP9WBBOiNBkHA9tYvvYRqj2Y",
"1YaeZaggiNvFzTAlDVaKblQzoe1oMKza6",
"1fNH4aZ8qvpXWz5OvO0543OKEGh8If3bM",
"1vekjDrONOLa0Gtd7dsXGGFH39QmV5a-S",
"1qXzav33s7-Tyjf2_amnmlIxPbkCVO9j8",
"1_HPy5G9d72X06aKKplRzsEew38LB2-TU",
"19L77VwF7JxMhWRVODUvHy649kxrX4ncE",
"1FPnpn1H882Z8CY5CCLXONuY8_xMB3cni",
"1F59beaqxWsNDrkF8589SOLUjz4HLkg36",
"1rcGoJR4rIyekLqlppssspRhWd0Nh7Gr5",
"1AZoYkS9BziwZ2UnpFdX0sjpsI7rI8grr",
"1XIkYsialnZMj3RB_PfiL7-MUovgMU0n-",
"1YPRlIHpZj8qObf4ZnaJgiffNbCCeQlLB",
"1dOWkkznRwBh2j3H2ezoA71mt1T4U7SLj",
"1ckkvZjItT5UwdnLwSV7QEB8jItnuILEQ",
"1TKMJkz5k36bd7J_kS9XWsBUa92TEYBLj",
"1Uy-TTfF5S5T9yjIIKAZ2gNWmiApVLAWG",
"1jMUJ7L3ijbLDnnQRJ3A2CYBLgMo_iDDX",
"1UBN3kv9uh1lKZr8MA-DggUINKecq_aXU",
"1AL9ofAdAgVGDi7bCWvcPJINXFpCPifvn",
"18t8UOBf2_xVdlgzY8OAWeC-DglOvSZYu",
"1y7UxITbmN1SmvtUaZE6fXXmouPXBEQ_E",
"13I-ghIDt4NUhVj5-Q14iUmrSGk_lpBut",
"1Yh_2Uic_77YeD3Z9R8hU7rkNLHQYPWF2",
"1zAvjiSvDtN50bUDzC_E0sYGim6NK9ioX",
"1ouo2Gev24vYOEVXgAgPNZDEfM_Ms6gPM",
"1jMeR627z12rOlCklLAJ0OryiBu1aOoWH",
"1C6MS94ZAPxLvbXR6KlrvbMU-hN6LemQT",
"1Wb-WhD_J9e8hBoURbYIG5Yn140IaR_Ey",
"1qEBMwmbKTgMOJNFKmmp4efGCJNUkVNAL",
"1CLif-9EgeJTwmZpXc8AIFGZjnZyc35Qn",
"1T2QQsMTm6o1C-mf9OmExg18C-VpD6Izc",
"17q4vEQLJF_sVT1HqufLKYtmsfqMu1Zul",
"1es9kSqw_Gm_RBSYXTygHHKPQy7TyWf4e",
"1mpZGqSZcszSReYyp4zCVDqdEcv1BDhDj",
"107K3ScT97yT3hurBQdgfpISOG20kXVHe",
"1NOch0YN-jW9_GxYViZg_uc2y7Dp1-JOK",
"1MBqV7wepXhsbjcCegHRQludjPuKnROlM",
"1s9TXu-HEY0O3FTh8NtJnlZlvtMgcRb7A",
"1vm0H0p8bprxbAKeiFK01QuZYug-zMbz-",
"1VnNWKh94KJVGsFSMdOUJ0YRPP8tBUjyp",
"1z5SKAbz27jFwHfWeLtMc1lSTSH8nnwD8",
"1ql1oQjAqc7LroO7XWcf41RFAvDT5JfBe",
"14SKj9IBR2YOho_ysbDw3ogonbNSm2wZa",
"1Wgfa4fsjWr8ewUzfdc-MULmf36mzXHHN",
"1IoFVvLA-YiXajNUO8rxPY2YCiU3EZU2E",
"16UWBNpOBVnxKbo5TKJwNB5Q89wZvN_3n",
"1lKw2n6Y0x9OutH3f_EEFUoCwfOa11ovT",
"1M5vbZ0zSDI-OUb5j-wWCc9RFGCZ-_fvK",
"1SepMmaehuN69sjzPxwUMK-mjg4rPhIg_",
"1nXzT5H6t60a0eugJA9NM-ntQbcDhm04S",
"1Ndp_TEzrGy0ILNoLDWdhwQXiAhAAyHfE",
"1dGqodxZ_UpMvZ8fw1Otj1QnZKp7FnEJC",
"109Zt_K0Qi8HC2w-033rY0MH_1Nm7ugs6",
"1FIV-koNYB8MtkB-Z5taoouTH3MoPok0b",
"1SM9BfraEmgCkKtBNgOoXOEgkxxYdtwcJ",
"17RONS__xPxYHgqXPs1LArWBAyPCv_jmX",
"1Bn7zlhkm4iLWSyIze0IakcWnx08dUJt9",
"1V1Y-hYWy5lRdrgE3EBrWeP_Y5QlZYsJg",
"1mmCmxqKQTMZPwaNnKUbf4Cu6kaVasrKX",
"1lcO9oTYSiFskCV-PQnqEq1VsscEiRAjk",
"1ECZ4EcxW887oUVOaW6sNz8BJ3rlLxlH9",
"1n4m_G9iIsjG9IcGhEdu03rlluRfuulh_",
"115NL64TZpg6vcYU8C8AVAHzZSD_z4kIO",
"1WkmWtuCFQcR-dYJaxzYpHH0W48C2ImVy",
"1OZF6RP0OCmMcj7KKm1-sksVese2jZhno",
"1ecQ1xHguq78F-oWe6t9oTWcTJ_N4skRL",
"1ewA_ANkCmc-M2m99mS7PZ8UjfVX_KJwY",
"1ErOMcq6rbDEa8idLF99noRZgRN8h6wWJ",
"1ZOeu2bv_QvN33Gx2lQ_XbOiXE3tHCAAD",
"1GS0qPTqA-Qk7TSZPBm1DlI6quImvc67q",
"1YSRksdLrC85i5Xbh7aHPkpyaGliDnqDj",
"1J7Q0netm_bVdGl9p2vC-wJ36HRzL7kB7",
"1zXP9M5RWKK4k7SEXWXSYlGAfAikCmHa_",
"1ov29zhpTDiiJPRkdcscGNIQKc4U3qCN_",
"1r13TGbbpWuMOT69w3Y1mZdhXuiu6XcfW",
"11zYax3SmCmcQpWKqMuwi-Zam48nq-R3p",
"1o1sBmTTowNftZEhGqKV41pJBazjpWoTL",
"1_-gu3GraqrccOICq3cEOng-c4ucMF2tZ",
"1Usf2kSDRG4LwDGY3-KmZCTgC8RtMX9tx",
"1OffJvjdv5SdlEoFc5zdsJwIJnaB3zepK",
"1gGG5_Vsk8xICQPOmM4gCDrOXM_cgRa6i",
"1oqC4l2kqRmmVZQC3SH2bJACKhvX746e3",
"1rMDrnbehulXfN10qhG4HPloUCBH_tKvf",
"1_Cnz0CWYP6blv4FAX9Bs3dxNKYWbAM1o",
"1ueVTl4-C4Qj3fRrFqDDiUYQsHzDN-dOP",
"1JowWlB31S20dj5DrFetbGPWO5BhqVKCa",
"1yK5BrE1ZFabAQdFEjMBdXFlJOeMGIeH_",
"1BV7JdPi_jPoCWi_6N-6SOk46XLwUsL5k",
"1DBGt-eQmuwNes5gCs8W50sAELlk_phK7",
"10vzL9HMWGNBgbO6xm22tQGnGoDZDC7yq",
"1X8AcT-XZoDaslTTZx1Sfq3ejx4oLq_wX",
"10gSUcQPTwYAcHApk22HFgJUExTnlacbj",
"1fxypOiPOg2Of1FU_NJQmE28RTVacDX3f",
"10JoWseLgqG5wTmRN-ms6iqoKJJEUsPAQ",
"1l8_U4DZ9Y7e_8nJGBU8TKQRta_Sbs3IO",
"1JKpGYJEIiNtLhGmCj68Rmdf2iT36xPiH",
"1FhKc9qIoexkwDyD6rvvIlkUCXbE0-71M",
"1POXkAbmvBBsa1NM8VDZLaaJahZztuRZn",
"1ch0t4r-Wb4rC7oIVTr6WimNpP4cm3wsK",
"1g8vkDm0zh8HoMo_RwIs6zS_C7n-z8qkL",
"11bexNEUjVRhRgQIc1dF199HLTvbGrGp4",
"17VbcqJdyE8KuXAEHsgJ0nKhIJExBBD5o",
"1M7M-DhtHbipMLYE_rHvr6_1H88Q1BPi0",
"1Sv66EnW1d2Bw03lCh_T3tYhygr3hk-BC",
"11I2vx5Puxz3V2zKKOzQtq0KOD43uDcB5"
];

let currentPhoto=null;
let currentIndex=0;

const gallery=document.getElementById("gallery");
const viewer=document.getElementById("viewer");
const viewerImage=document.getElementById("viewerImage");
const viewerCounter=document.getElementById("viewerCounter");
const downloadModal=document.getElementById("downloadModal");
const thankyou=document.getElementById("thankyou");

function driveImage(id,size="w1000"){
    return "https://drive.google.com/thumbnail?id="+encodeURIComponent(id)+"&sz="+size;
}

/*
 Google Drive download URL.
 Jika browser tidak mengizinkan download otomatis lintas-domain,
 fallback akan membuka URL Drive di tab baru.
*/
function driveDownload(id){
    return "https://drive.usercontent.google.com/download?id="+
        encodeURIComponent(id)+"&export=download&confirm=t";
}

function updateClock(){
    const now=new Date();
    const time=[
        String(now.getHours()).padStart(2,"0"),
        String(now.getMinutes()).padStart(2,"0"),
        String(now.getSeconds()).padStart(2,"0")
    ].join(":");
    document.getElementById("mainClock").textContent=time;
    document.getElementById("miniClock").textContent=time;
}
setInterval(updateClock,1000);
updateClock();

function renderGallery(){
    gallery.innerHTML="";

    photoIds.forEach((id,index)=>{
        const card=document.createElement("div");
        card.className="photo-card";

        const img=document.createElement("img");
        img.loading="lazy";
        img.decoding="async";
        img.alt="Another Visual "+(index+1);
        img.classList.add("av-photo-loading");
        img.src=driveImage(id,"w700");

        img.onload=function(){
            this.classList.remove("av-photo-loading");
        };

        img.onerror=function(){
            if(!this.dataset.retry){
                this.dataset.retry="1";
                this.src=driveImage(id,"w800");
            }else{
                this.classList.remove("av-photo-loading");
                this.alt="Foto tidak dapat dimuat";
            }
        };

        const overlay=document.createElement("div");
        overlay.className="photo-overlay";

        const number=document.createElement("div");
        number.className="photo-number";
        number.textContent=String(index+1).padStart(3,"0");

        const view=document.createElement("div");
        view.className="view-text";
        view.textContent="LIHAT";

        overlay.appendChild(number);
        overlay.appendChild(view);
        card.appendChild(img);
        card.appendChild(overlay);

        card.addEventListener("click",()=>openViewer(id,index));
        gallery.appendChild(card);
    });
}

const imageCache = new Map();

function preloadPhoto(index, size="w1800"){
    if(index < 0 || index >= photoIds.length) return;
    const id = photoIds[index];
    const key = id + "_" + size;
    if(imageCache.has(key)) return imageCache.get(key);

    const img = new Image();
    img.decoding = "async";
    const promise = new Promise(resolve=>{
        img.onload = ()=>resolve(img);
        img.onerror = ()=>resolve(null);
    });
    img.src = driveImage(id,size);
    imageCache.set(key,promise);
    return promise;
}

function openViewer(id,index){
    currentPhoto=id;
    currentIndex=index;

    // Tampilkan versi ringan SEGERA agar viewer tidak blank.
    viewerImage.classList.remove("av-photo-loading");
    viewerImage.src=driveImage(id,"w1000");
    viewerImage.alt="Another Visual "+(index+1);

    viewerCounter.textContent=
        String(index+1).padStart(3,"0")+" / "+photoIds.length;

    viewer.classList.add("active");
    viewer.setAttribute("aria-hidden","false");
    document.body.style.overflow="hidden";

    // Setelah viewer sudah tampil, naikkan kualitas tanpa membuat layar blank.
    preloadPhoto(index,"w1800").then(img=>{
        if(img && currentPhoto===id && currentIndex===index){
            viewerImage.src=img.src;
        }
    });

    // Foto sebelah dipanaskan di cache supaya Next/Previous terasa instan.
    preloadPhoto(index+1,"w1800");
    preloadPhoto(index-1,"w1800");
}

function closeViewer(){
    viewer.classList.remove("active");
    viewer.setAttribute("aria-hidden","true");
    viewerImage.src="";
    document.body.style.overflow="";
}

function openDownload(){
    if(currentPhoto) downloadModal.classList.add("active");
}

function closeDownload(){
    downloadModal.classList.remove("active");
}

async function downloadPhoto(){
    if(!currentPhoto)return;

    closeDownload();

    const filename="Another-Visual-"+String(currentIndex+1).padStart(3,"0")+".jpg";

    /*
      Download dibuat tanpa membuka tab/jendela Google Drive.
      Kita coba mengambil file sebagai Blob lalu membuat URL lokal
      sementara untuk memicu download di browser.

      Jika Google Drive menolak request cross-origin, fallback
      menggunakan endpoint download langsung tanpa target="_blank".
      Jadi website tidak sengaja membuka halaman Drive.
    */
    try{
        const response=await fetch(driveDownload(currentPhoto),{
            method:"GET",
            mode:"cors",
            credentials:"omit"
        });

        if(!response.ok) throw new Error("Download gagal");

        const blob=await response.blob();
        const blobUrl=URL.createObjectURL(blob);

        const link=document.createElement("a");
        link.href=blobUrl;
        link.download=filename;
        document.body.appendChild(link);
        link.click();
        link.remove();

        setTimeout(()=>URL.revokeObjectURL(blobUrl),30000);
    }catch(error){
        // Fallback: tetap download langsung, tanpa membuka tab Drive.
        const link=document.createElement("a");
        link.href=driveDownload(currentPhoto);
        link.download=filename;
        link.rel="noopener";
        document.body.appendChild(link);
        link.click();
        link.remove();
    }

    setTimeout(()=>{
        thankyou.classList.add("active");
    },1000);
}

function nextPhoto(){
    if(currentIndex<photoIds.length-1){
        openViewer(photoIds[currentIndex+1],currentIndex+1);
    }
}

function previousPhoto(){
    if(currentIndex>0){
        openViewer(photoIds[currentIndex-1],currentIndex-1);
    }
}

function rate(value){
    localStorage.setItem("another_visual_rating",String(value));

    document.querySelectorAll(".star").forEach((star,index)=>{
        star.classList.toggle("active",index<value);
    });

    setTimeout(()=>{
        thankyou.classList.remove("active");
    },1000);
}

document.addEventListener("keydown",(event)=>{
    if(event.key==="Escape"){
        closeViewer();
        closeDownload();
        thankyou.classList.remove("active");
    }

    if(event.key==="ArrowRight" && viewer.classList.contains("active")){
        nextPhoto();
    }

    if(event.key==="ArrowLeft" && viewer.classList.contains("active")){
        previousPhoto();
    }
});

viewer.addEventListener("click",(event)=>{
    if(event.target===viewer)closeViewer();
});

downloadModal.addEventListener("click",(event)=>{
    if(event.target===downloadModal)closeDownload();
});

let touchStartX=0;

viewer.addEventListener("touchstart",(event)=>{
    touchStartX=event.changedTouches[0].screenX;
},{passive:true});

viewer.addEventListener("touchend",(event)=>{
    const touchEndX=event.changedTouches[0].screenX;
    const diff=touchStartX-touchEndX;

    if(Math.abs(diff)<50)return;

    if(diff>0)nextPhoto();
    else previousPhoto();
},{passive:true});

renderGallery();

/* =========================================================
   DEVICE DETECTION
   Tekan D untuk membuka panel.
   Data hanya dibaca lokal oleh browser.
   ========================================================= */

function detectOS(ua){
    if(/Windows NT/i.test(ua))return"Windows";
    if(/Android/i.test(ua))return"Android";
    if(/iPhone|iPad|iPod/i.test(ua))return"iOS";
    if(/Mac OS X/i.test(ua))return"macOS";
    if(/CrOS/i.test(ua))return"ChromeOS";
    if(/Linux/i.test(ua))return"Linux";
    return"Unknown";
}

function detectBrowser(ua){
    if(/Edg\//i.test(ua))return"Microsoft Edge";
    if(/OPR\//i.test(ua))return"Opera";
    if(/SamsungBrowser/i.test(ua))return"Samsung Internet";
    if(/Firefox\//i.test(ua))return"Mozilla Firefox";
    if(/CriOS\//i.test(ua))return"Chrome iOS";
    if(/FxiOS\//i.test(ua))return"Firefox iOS";
    if(/Chrome\//i.test(ua))return"Google Chrome";
    if(/Safari\//i.test(ua)&&!/Chrome|CriOS/i.test(ua))return"Safari";
    return"Browser lain";
}

function detectDeviceType(ua){
    if(/iPad/i.test(ua))return"Tablet · iPad";
    if(/Android/i.test(ua)&&!/Mobile/i.test(ua))return"Tablet · Android";
    if(/Mobile|iPhone|iPod|Android/i.test(ua))return"Mobile";
    return"Desktop / Laptop";
}

function detectDeviceName(ua){
    if(/iPhone/i.test(ua))return"Apple iPhone";
    if(/iPad/i.test(ua))return"Apple iPad";

    if(/Android/i.test(ua)){
        const match=ua.match(/Android[^;)]*;\s*(?:[a-z]{2}-[A-Z]{2};\s*)?([^;)]+?)(?:\s+Build\/[^;)]*)?[;)]/i);
        if(match&&match[1])return match[1].trim();
        return"Android Device";
    }

    if(/Macintosh/i.test(ua))return"Mac";
    if(/Windows/i.test(ua))return"Windows PC";
    if(/CrOS/i.test(ua))return"Chromebook";
    if(/Linux/i.test(ua))return"Linux PC";

    return detectDeviceType(ua);
}

function getNetworkInfo(){
    const c=navigator.connection||navigator.mozConnection||navigator.webkitConnection;

    if(!c)return"Tidak tersedia";

    const type=c.effectiveType||c.type||"Unknown";
    const down=typeof c.downlink==="number"?c.downlink+" Mbps":"";

    return down?type+" · "+down:type;
}

function getMemory(){
    return navigator.deviceMemory?navigator.deviceMemory+" GB":"Tidak tersedia";
}

function updateDeviceDetection(){
    const ua=navigator.userAgent||"";
    const screenText=`${screen.width} × ${screen.height}`;
    const viewportText=`${window.innerWidth} × ${window.innerHeight}`;
    const orientation=window.innerWidth>=window.innerHeight?"Landscape":"Portrait";
    const touch=navigator.maxTouchPoints>0?"Ya":"Tidak";
    const dpr=window.devicePixelRatio?window.devicePixelRatio.toFixed(2):"1";
    const cpu=navigator.hardwareConcurrency||"Tidak tersedia";
    const timezone=Intl.DateTimeFormat().resolvedOptions().timeZone||"Unknown";

    const device=detectDeviceName(ua);
    const type=detectDeviceType(ua);
    const os=detectOS(ua);
    const browser=detectBrowser(ua);

    const values={
        diDevice:`${device} · ${type}`,
        diOS:os,
        diBrowser:browser,
        diScreen:screenText,
        diViewport:viewportText,
        diOrientation:orientation,
        diTouch:touch,
        diDpr:dpr,
        diCpu:String(cpu),
        diMemory:getMemory(),
        diNetwork:getNetworkInfo(),
        diTimezone:timezone,
        diMode:type
    };

    Object.keys(values).forEach(id=>{
        const el=document.getElementById(id);
        if(el)el.textContent=values[id];
    });

    const connection=navigator.connection||navigator.mozConnection||navigator.webkitConnection;

    if(connection&&!connection.__avBound){
        connection.addEventListener?.("change",updateDeviceDetection);
        connection.__avBound=true;
    }
}

function showDeviceInfo(){
    updateDeviceDetection();

    const panel=document.getElementById("deviceInfoPanel");

    if(panel){
        panel.classList.add("show");
        panel.setAttribute("aria-hidden","false");
    }
}

function hideDeviceInfo(){
    const panel=document.getElementById("deviceInfoPanel");

    if(panel){
        panel.classList.remove("show");
        panel.setAttribute("aria-hidden","true");
    }
}

document.addEventListener("keydown",function(e){
    if(e.key.toLowerCase()==="d" &&
       !["INPUT","TEXTAREA"].includes(document.activeElement?.tagName)){

        const panel=document.getElementById("deviceInfoPanel");

        if(panel?.classList.contains("show"))hideDeviceInfo();
        else showDeviceInfo();
    }
});

window.addEventListener("resize",updateDeviceDetection);
window.addEventListener("orientationchange",updateDeviceDetection);
document.addEventListener("DOMContentLoaded",updateDeviceDetection);
</script>

</body>
