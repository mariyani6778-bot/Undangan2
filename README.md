<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ultimate Wedding Invitation</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&family=Playfair+Display:wght@500;700&display=swap" rel="stylesheet">

<style>
*{margin:0;padding:0;box-sizing:border-box}
body{font-family:Poppins,sans-serif;background:#0f1226;color:#fff}

.cover{height:100vh;display:flex;flex-direction:column;justify-content:center;align-items:center;background:linear-gradient(135deg,#1a1f4b,#3b3f9c)}
.cover h1{font-family:'Playfair Display';font-size:48px}
.btn{margin-top:20px;padding:12px 25px;border-radius:30px;background:#fff;color:#000;cursor:pointer}

.section{padding:60px 20px;text-align:center;opacity:0;transform:translateY(40px);transition:1s}
.section.show{opacity:1;transform:translateY(0)}
.card{max-width:800px;margin:auto;background:#1b1f3a;padding:30px;border-radius:20px}

.slider{position:relative;overflow:hidden}
.slide{display:none}
.slide img{width:100%;border-radius:15px}

.countdown{display:flex;justify-content:center;gap:10px;margin-top:20px}
.countdown div{background:#2a2f5a;padding:10px;border-radius:10px}

.timeline{text-align:left;margin-top:20px}
.timeline div{border-left:2px solid #fff;padding-left:10px;margin:10px 0}

footer{text-align:center;padding:20px;color:#aaa}
</style>
</head>

<body>

<div class="cover" id="cover">
<h1>Andi & Siti</h1>
<p>Kepada Yth: <span id="guest"></span></p>
<button class="btn" onclick="openInvite()">Buka Undangan</button>
</div>

<div id="content" style="display:none">

<div class="section">
<div class="card">
<h2>Detail Acara</h2>
<p>📅 20 Desember 2026</p>
<p>⏰ 10.00 WIB</p>
<p>📍 Gedung Bahagia</p>
<iframe src="https://maps.google.com/maps?q=jakarta&t=&z=13&ie=UTF8&iwloc=&output=embed" width="100%" height="200"></iframe>
<div class="countdown" id="countdown"></div>
</div>
</div>

<div class="section">
<div class="card">
<h2>Love Story</h2>
<div class="timeline">
<div>💖 2020 - Pertemuan</div>
<div>💍 2025 - Lamaran</div>
<div>🎉 2026 - Menikah</div>
</div>
</div>
</div>

<div class="section">
<div class="card">
<h2>Galeri</h2>
<div class="slider">
<div class="slide"><img src="https://via.placeholder.com/600x400"></div>
<div class="slide"><img src="https://via.placeholder.com/600x400"></div>
<div class="slide"><img src="https://via.placeholder.com/600x400"></div>
</div>
</div>
</div>

<div class="section">
<div class="card">
<h2>RSVP Form</h2>
<form onsubmit="sendWA(event)">
<input type="text" id="nama" placeholder="Nama" required><br><br>
<select id="kehadiran">
<option>Hadir</option>
<option>Tidak Hadir</option>
</select><br><br>
<button class="btn">Kirim</button>
</form>
</div>
</div>

<footer>Terima kasih atas doa Anda</footer>
</div>

<audio id="music" loop>
<source src="https://www.bensound.com/bensound-music/bensound-romantic.mp3" type="audio/mp3">
</audio>

<script>
function openInvite(){
 document.getElementById('cover').style.display='none';
 document.getElementById('content').style.display='block';
 document.getElementById('music').play();
}

// Nama tamu
const params=new URLSearchParams(window.location.search);
document.getElementById('guest').innerText=params.get('to')||'Tamu Undangan';

// Scroll animasi
const sections=document.querySelectorAll('.section');
window.addEventListener('scroll',()=>{
sections.forEach(sec=>{
 if(window.scrollY+window.innerHeight>sec.offsetTop+100){sec.classList.add('show');}
});
});

// Countdown
const target=new Date("Dec 20, 2026 10:00:00").getTime();
setInterval(()=>{
 const now=new Date().getTime();
 const gap=target-now;
 const d=Math.floor(gap/(1000*60*60*24));
 const h=Math.floor((gap%(1000*60*60*24))/(1000*60*60));
 const m=Math.floor((gap%(1000*60*60))/(1000*60));
 const s=Math.floor((gap%(1000*60))/1000);
 document.getElementById('countdown').innerHTML=`<div>${d}d</div><div>${h}h</div><div>${m}m</div><div>${s}s</div>`;
},1000);

// Slider
let slideIndex=0;
const slides=document.querySelectorAll('.slide');
function showSlides(){
 slides.forEach(s=>s.style.display='none');
 slideIndex++;
 if(slideIndex>slides.length) slideIndex=1;
 slides[slideIndex-1].style.display='block';
 setTimeout(showSlides,3000);
}
showSlides();

// RSVP WA
function sendWA(e){
 e.preventDefault();
 const nama=document.getElementById('nama').value;
 const hadir=document.getElementById('kehadiran').value;
 const text=`Halo, saya ${nama}, konfirmasi: ${hadir}`;
 window.open(`https://wa.me/628123456789?text=${encodeURIComponent(text)}`);
}
</script>

</body>
</html>
