<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Bing - Alislamiah</title>
<link rel="icon" href="icon.png">
<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Arial,sans-serif;-webkit-tap-highlight-color:transparent}
body{background:#0a1628;color:#e8f0fe;min-height:100vh;overflow-x:hidden;padding-bottom:110px;position:relative}
/* شاشة ترحيب احترافية أصلية */
.bing-splash-screen{position:fixed;inset:0;background:#050b14;display:flex;flex-direction:column;justify-content:center;align-items:center;z-index:99999;overflow:hidden;transition:opacity 0.8s cubic-bezier(0.4,0,0.2,1),visibility 0.8s,transform 0.8s cubic-bezier(0.4,0,0.2,1)}
.bing-splash-screen.hidden{opacity:0;visibility:hidden;transform:scale(1.12);pointer-events:none}
.bing-splash-bg{position:absolute;inset:0;background-image:radial-gradient(circle at 50% 50%,rgba(0,195,255,0.15),transparent 60%),linear-gradient(rgba(255,255,255,0.03) 1px,transparent 1px),linear-gradient(90deg,rgba(255,255,255,0.03) 1px,transparent 1px);background-size:100% 100%,30px 30px,30px 30px;background-position:0 0,15px 15px,15px 15px;animation:bgPulse 4s ease-in-out infinite alternate}
.bing-spinner-wrapper{position:relative;width:130px;height:130px;display:flex;align-items:center;justify-content:center;border-radius:32px;animation:iconPulse 2.5s ease-in-out infinite alternate}
.bing-spinner-wrapper::before{content:'';position:absolute;inset:-8px;border-radius:38px;background:conic-gradient(from 0deg,#00c3ff,#087fff,#7000ff,#00f0ff,#00c3ff);animation:rotateConic 2s linear infinite;filter:blur(12px);opacity:0.85}
.bing-spinner-wrapper::after{content:'';position:absolute;inset:-4px;border-radius:35px;background:conic-gradient(from 0deg,#00c3ff,#087fff,#7000ff,#00f0ff,#00c3ff);animation:rotateConic 2s linear infinite}
.bing-icon-cover{position:absolute;inset:1px;background:#050b14;border-radius:31px;z-index:1}
.bing-splash-icon{position:relative;z-index:2;width:110px;height:110px;border-radius:26px;object-fit:cover;box-shadow:0 15px 35px rgba(0,195,255,0.3)}
.bing-splash-title{position:relative;z-index:2;margin-top:25px;font-size:1.25rem;font-weight:800;letter-spacing:1px;background:linear-gradient(135deg,#ffffff 30%,#6fb7ff 100%);-webkit-background-clip:text;-webkit-text-fill-color:transparent;text-shadow:0 10px 20px rgba(0,195,255,0.2)}
@keyframes rotateConic{0%{transform:rotate(0deg)}100%{transform:rotate(360deg)}}
@keyframes iconPulse{0%{transform:scale(0.96)}100%{transform:scale(1.04)}}
@keyframes bgPulse{0%{opacity:0.6}100%{opacity:1}}
.bg{position:fixed;inset:0;background:url('https://images.unsplash.com/photo-1506905925346-21bda4d32df4?w=1200&q=80') center/cover no-repeat;z-index:0}
.bg::after{content:'';position:absolute;inset:0;background:linear-gradient(180deg,rgba(5,15,35,0.55) 0%,rgba(5,20,45,0.35) 35%,rgba(8,25,55,0.75) 70%,rgba(6,18,40,0.92) 100%)}
.status-bar{position:relative;z-index:10;display:flex;justify-content:space-between;align-items:center;padding:8px 16px 4px;font-size:13px;font-weight:600;color:#fff;text-shadow:0 1px 3px rgba(0,0,0,0.5)}
.status-right{display:flex;align-items:center;gap:6px;font-size:12px}
.profile{position:relative;z-index:10;margin:8px 16px 0}
.profile-btn{width:42px;height:42px;border-radius:50%;background:linear-gradient(135deg,#1e3a5f,#0d2137);border:2px solid rgba(100,180,255,0.4);display:flex;align-items:center;justify-content:center;overflow:hidden}
.profile-btn img{width:100%;height:100%;object-fit:cover}
.main{position:relative;z-index:10;margin-top:28vh;display:flex;flex-direction:column;align-items:center;padding:0 18px;margin-bottom:24px;min-height:50vh}
.search-box{width:100%;max-width:520px;background:rgba(12,28,52,0.92);backdrop-filter:blur(16px);border-radius:50px;padding:12px 14px;display:flex;align-items:center;gap:8px;box-shadow:0 8px 32px rgba(0,20,50,0.6),0 0 0 1px rgba(80,160,255,0.25);transition:all 0.25s ease;overflow:visible !important}
.search-box:focus-within{box-shadow:0 8px 36px rgba(0,40,90,0.7),0 0 0 2px rgba(100,180,255,0.5);background:rgba(15,35,65,0.95)}
.search-icon{width:22px;height:22px;fill:#6ba3e0;flex-shrink:0}
.search-input{flex:1;background:transparent;border:none;outline:none;color:#e8f4ff;font-size:17px;direction:rtl;min-width:80px}
.search-input::placeholder{color:#7a9cc0}
.search-left{display:flex;align-items:center;gap:8px;flex-shrink:0}
.search-actions{display:flex;align-items:center;gap:10px;flex-shrink:0}
.action-btn{width:26px;height:26px;fill:#6ba3e0;cursor:pointer;flex-shrink:0;transition:all 0.2s}
.action-btn:hover{fill:#a8d4ff;transform:scale(1.1)}
.ai-mode-pill{display:flex;align-items:center;background:rgba(159,122,234,0.14);border:1px solid rgba(159,122,234,0.45);color:#c4b5fd;border-radius:20px;padding:5px 12px;font-size:13px;font-weight:800;cursor:pointer;white-space:nowrap}
.ai-mode-pill.active{background:linear-gradient(135deg,#9f7aea,#667eea);color:#fff !important;border-color:transparent;box-shadow:0 0 0 2px rgba(255,255,255,0.7),0 4px 14px rgba(102,126,234,0.7)}
.cards{width:100%;max-width:520px;display:flex;gap:12px;margin-top:36px;overflow-x:auto;padding-bottom:8px;scrollbar-width:none}
.cards::-webkit-scrollbar{display:none}
.card{flex:0 0 auto;background:rgba(12,30,58,0.88);backdrop-filter:blur(12px);border-radius:18px;padding:14px 16px;min-width:130px;border:1px solid rgba(70,140,220,0.2);text-decoration:none;color:inherit}
.card-title{font-size:14px;font-weight:600;color:#d0e6ff;margin-bottom:4px}
.card-desc{font-size:12px;color:#8bb0d8;display:flex;align-items:center;gap:6px}
.ad-card{font-family:'Tajawal',sans-serif;background:#ffffff;border-radius:24px;overflow:hidden;width:100%;max-width:360px;margin:48px auto 32px;box-shadow:0 10px 25px -5px rgba(0,0,0,0.08);position:relative;z-index:5}
.ad-badge{position:absolute;top:14px;right:14px;background:rgba(255,255,255,0.92);color:#718096;font-size:0.72rem;padding:5px 12px;border-radius:50px;z-index:10}
.ad-card-image{width:100%;height:180px;object-fit:cover;display:block}
.ad-card-content{padding:20px 18px 24px;text-align:right}
.ad-card-title{font-size:1.3rem;font-weight:800;color:#1a202c;margin-bottom:8px}
.ad-card-desc{font-size:0.92rem;color:#4a5568;line-height:1.65;margin-bottom:18px}
.ad-card-btn{display:block;text-align:center;background:#1a73e8;color:#fff !important;text-decoration:none !important;font-size:0.95rem;font-weight:700;padding:14px 24px;border-radius:12px;width:100%}
.bottom-nav{position:fixed;bottom:0;left:0;right:0;z-index:20;background:rgba(8,20,42,0.96);backdrop-filter:blur(20px);border-top:1px solid rgba(60,120,200,0.25);padding:10px 0 12px;display:flex;justify-content:space-around;align-items:center}
.nav-item{display:flex;flex-direction:column;align-items:center;gap:4px;text-decoration:none;color:#7a9cc0;font-size:11px;padding:6px 12px;border-radius:12px;min-width:64px}
.nav-item.active{color:#5eb0ff}
.nav-icon{width:26px;height:26px;display:flex;align-items:center;justify-content:center;font-size:22px}
.gemini-logo{width:28px;height:28px;background:linear-gradient(135deg,#4a90e2,#1a5fb4);border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:14px;font-weight:700;color:#fff}
</style>
</head>
<body>
<div class="bing-splash-screen" id="bingSplash"><div class="bing-splash-bg"></div><div class="bing-spinner-wrapper"><div class="bing-icon-cover"></div><img src="icon.png" class="bing-splash-icon" alt="Bing"></div><div class="bing-splash-title">Alislamiah Bing</div></div>
<div class="bg"></div>
<div class="status-bar"><span>01:05</span><div class="status-right"><span>58.1 KB/s</span><span>4G</span><span>21</span><span>⚡</span></div></div>
<div class="profile"><div class="profile-btn"><img src="icon.png" alt="Icon"></div></div>
<div class="main">
<form class="search-box" action="results_full.html" method="GET" id="searchForm">
<div class="search-left">
<svg class="search-icon" viewBox="0 0 24 24"><path d="M15.5 14h-.79l-.28-.27A6.471 6.471 0 0 0 16 9.5 6.5 6.5 0 1 0 9.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"/></svg>
<button type="button" class="ai-mode-pill" id="aiModeBtn" onclick="toggleAIMode()">AI mode</button>
</div>
<input type="text" name="q" class="search-input" placeholder="Search" autocomplete="off" autofocus>
<div class="search-actions">
<input type="file" id="imageSearchInput" accept="image/*" style="display:none;" onchange="handleImageSearch(this)">
<svg class="action-btn" viewBox="0 0 24 24" onclick="document.getElementById('imageSearchInput').click()" title="بحث بالصور"><path d="M12 15.2c1.76 0 3.2-1.44 3.2-3.2s-1.44-3.2-3.2-3.2-3.2 1.44-3.2 3.2 1.44 3.2 3.2 3.2zm0-8c2.65 0 4.8 2.15 4.8 4.8s-2.15 4.8-4.8 4.8-4.8-2.15-4.8-4.8 2.15-4.8 4.8-4.8zm8.4-2H18l-1.2-1.6c-.3-.4-.8-.6-1.3-.6H8.5c-.5 0-1 .2-1.3.6L6 5.2H3.6C2.7 5.2 2 5.9 2 6.8v12.4c0 .9.7 1.6 1.6 1.6h16.8c.9 0 1.6-.7 1.6-1.6V6.8c0-.9-.7-1.6-1.6-1.6z"/></svg>
<svg class="action-btn" id="micBtn" viewBox="0 0 24 24" onclick="startVoiceSearch()" title="بحث صوتي"><path d="M12 14c1.66 0 3-1.34 3-3V5c0-1.66-1.34-3-3-3S9 3.34 9 5v6c0 1.66 1.34 3 3 3zm-1-9c0-.55.45-1 1-1s1 .45 1 1v6c0 .55-.45 1-1 1s-1-.45-1-1V5zm6 6c0 2.76-2.24 5-5 5s-5-2.24-5-5H5c0 3.53 2.61 6.43 6 6.92V21h2v-3.08c3.39-.49 6-3.39 6-6.92h-2z"/></svg>
</div>
</form>
<div class="cards">
<a href="https://mohamedmadoui5195.github.io/Alislamiah-search-console/" class="card"><div class="card-title">Alislamiah Search</div><div class="card-desc">Search Console</div></a>
<a href="https://mohamedmadoui5195.github.io/Alislamiah-services/" class="card"><div class="card-title">Alislamiah Services</div><div class="card-desc">الخدمات</div></a>
<a href="https://mohamedmadoui5195.github.io/Alislamiah-_net/" class="card"><div class="card-title">Alislamiah Net</div><div class="card-desc">الشبكة</div></a>
</div>
</div>
<style>@import url('https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700;800&display=swap');</style>
<div class="ad-card"><span class="ad-badge">مادة إعلانية</span><img src="Screenshot_20261011-191020.jpg" alt="مداد" class="ad-card-image"><div class="ad-card-content"><h2 class="ad-card-title">مداد</h2><p class="ad-card-desc">أقوى منصة لصنع الألعاب والمواقع والبرامج، حول أفكارك إلى واقع</p><a href="https://nazim10-u.github.io/nazim/" class="ad-card-btn" target="_blank">زيارة الموقع</a></div></div>

<style>
@import url('https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700;800&display=swap');

.ad-card {
  font-family: 'Tajawal', sans-serif;
  background: #ffffff;
  border-radius: 24px;
  overflow: hidden;
  width: 100%;
  max-width: 360px;
  margin: 20px auto 30px;
  box-shadow: 0 10px 25px -5px rgba(0,0,0,0.08), 0 8px 10px -6px rgba(0,0,0,0.04);
  transition: all 0.35s cubic-bezier(0.4, 0, 0.2, 1);
  border: 1px solid rgba(255,255,255,0.8);
  position: relative;
  z-index: 5;
}

.ad-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 20px 40px -10px rgba(0,0,0,0.12);
}

.ad-badge {
  position: absolute;
  top: 14px;
  right: 14px;
  background: rgba(255,255,255,0.92);
  backdrop-filter: blur(8px);
  color: #718096;
  font-size: 0.72rem;
  font-weight: 500;
  padding: 5px 12px;
  border-radius: 50px;
  z-index: 10;
  box-shadow: 0 2px 8px rgba(0,0,0,0.06);
}

.ad-card-content {
  padding: 20px 18px 24px;
  text-align: right;
}

.ad-card-title {
  font-size: 1.3rem;
  font-weight: 800;
  color: #1a202c;
  margin-bottom: 8px;
  line-height: 1.3;
}

.ad-card-desc {
  font-size: 0.92rem;
  color: #4a5568;
  line-height: 1.65;
  margin-bottom: 18px;
}

.ad-card-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, #4299e1 0%, #3182ce 100%);
  color: white !important;
  text-decoration: none !important;
  font-size: 0.95rem;
  font-weight: 600;
  padding: 12px 24px;
  border-radius: 50px;
  transition: all 0.3s ease;
  box-shadow: 0 4px 14px rgba(66,153,225,0.35);
  width: 100%;
}

.ad-card-btn:hover {
  background: linear-gradient(135deg, #3182ce 0%, #2b6cb0 100%);
  transform: translateY(-2px);
}
</style>


<style>
@import url('https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700;800&display=swap');

.ad-card-outhub {
  font-family: 'Tajawal', sans-serif;
  background: #ffffff;
  border-radius: 24px;
  overflow: hidden;
  width: 100%;
  max-width: 360px;
  margin: 20px auto 30px;
  box-shadow: 0 10px 25px -5px rgba(0,0,0,0.08), 0 8px 10px -6px rgba(0,0,0,0.04);
  transition: all 0.35s cubic-bezier(0.4, 0, 0.2, 1);
  border: 1px solid rgba(255,255,255,0.8);
  position: relative;
  z-index: 5;
}

.ad-card-outhub:hover {
  transform: translateY(-6px);
  box-shadow: 0 20px 40px -10px rgba(0,0,0,0.12);
}

.ad-badge-outhub {
  position: absolute;
  top: 14px;
  right: 14px;
  background: rgba(255,255,255,0.92);
  backdrop-filter: blur(8px);
  color: #718096;
  font-size: 0.72rem;
  font-weight: 500;
  padding: 5px 12px;
  border-radius: 50px;
  z-index: 10;
  box-shadow: 0 2px 8px rgba(0,0,0,0.06);
}

.ad-card-outhub .ad-card-content {
  padding: 20px 18px 24px;
  text-align: right;
}

.ad-card-outhub .ad-card-title {
  font-size: 1.3rem;
  font-weight: 800;
  color: #1a202c;
  margin-bottom: 8px;
  line-height: 1.3;
}

.ad-card-outhub .ad-card-desc {
  font-size: 0.92rem;
  color: #4a5568;
  line-height: 1.65;
  margin-bottom: 18px;
}

.ad-card-outhub .ad-card-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, #4299e1 0%, #3182ce 100%);
  color: white !important;
  text-decoration: none !important;
  font-size: 0.95rem;
  font-weight: 600;
  padding: 12px 24px;
  border-radius: 50px;
  transition: all 0.3s ease;
  box-shadow: 0 4px 14px rgba(66,153,225,0.35);
  width: 100%;
}

.ad-card-outhub .ad-card-btn:hover {
  background: linear-gradient(135deg, #3182ce 0%, #2b6cb0 100%);
  transform: translateY(-2px);
}
</style>

<!-- بطاقة Outhub -->
<div class="ad-card-outhub">
  <span class="ad-badge-outhub">مادة إعلانية</span>
  
  <div style="position:relative; width:100%; height:200px; background:#000; overflow:hidden;">
    <video id="outhubVideo" 
           src="Outhub.mp4" 
           muted 
           loop 
           playsinline 
           preload="auto"
           style="width:100%; height:100%; object-fit:cover; display:block;">
    </video>
    
    <div id="playOverlay" onclick="playOuthubVideo()" 
         style="position:absolute; inset:0; display:flex; align-items:center; justify-content:center; background:rgba(0,0,0,0.35); cursor:pointer; z-index:5;">
      <div style="width:60px; height:60px; background:rgba(255,255,255,0.9); border-radius:50%; display:flex; align-items:center; justify-content:center; box-shadow:0 4px 15px rgba(0,0,0,0.3);">
        <div style="width:0; height:0; border-top:12px solid transparent; border-bottom:12px solid transparent; border-left:20px solid #1a202c; margin-left:4px;"></div>
      </div>
    </div>
  </div>

  <div class="ad-card-content">
    <h2 class="ad-card-title">Outhub</h2>
    <p class="ad-card-desc">منصتك لإنشاء المواقع والتطبيقات.. ابدأ مشروعك الرقمي من هنا</p>
    <a href="https://mohamedmadoui5195.github.io/outhub/" class="ad-card-btn" target="_blank">زيارة الموقع</a>
  </div>
</div>

<script>
function playOuthubVideo() {
  const video = document.getElementById('outhubVideo');
  const overlay = document.getElementById('playOverlay');
  if (video) {
    video.play().then(function() {
      if (overlay) overlay.style.display = 'none';
    }).catch(function() {});
  }
}

document.addEventListener('DOMContentLoaded', function() {
  const video = document.getElementById('outhubVideo');
  if (video) {
    video.play().then(function() {
      const overlay = document.getElementById('playOverlay');
      if (overlay) overlay.style.display = 'none';
    }).catch(function() {});
  }
});
</script>


<div class="ad-card"><span class="ad-badge">مادة إعلانية</span><img src="Screenshot_20261011-200809.jpg" alt="alarabiya.net" class="ad-card-image"><div class="ad-card-content"><h2 class="ad-card-title">alarabiya.net</h2><p class="ad-card-desc">تابعوا الأخبار العربية والعالمية هنا</p><a href="https://www.alarabiya.net" class="ad-card-btn" target="_blank">زيارة الموقع</a></div></div>
<div class="ad-card"><span class="ad-badge">مادة إعلانية</span><img src="Screenshot_20261011-195632.jpg" alt="Alislamiah search console" class="ad-card-image"><div class="ad-card-content"><h2 class="ad-card-title">Alislamiah search console</h2><p class="ad-card-desc">آداة مشرفي المواقع... إن كان لديك موقع أطلب هنا لكي نفهرسه لك ويظهر في نتائج البحث</p><a href="https://mohamedmadoui5195.github.io/Alislamiah-search-console/" class="ad-card-btn" target="_blank">زيارة الموقع</a></div></div>
<nav class="bottom-nav">
<a href="index.html" class="nav-item active"><div class="nav-icon">🏠</div><span>البحث</span></a>
<a href="results_full.html" class="nav-item"><div class="nav-icon">🔍</div><span>بحث</span></a>
<a href="https://mohamedmadoui5195.github.io/Gemalot/" class="nav-item"><div class="nav-icon"><div class="gemini-logo">G</div></div><span>Gemalot</span></a>
</nav>
<script>
let aiMode=false;
window.addEventListener("DOMContentLoaded",function(){setTimeout(function(){var s=document.getElementById("bingSplash");if(s)s.classList.add("hidden");},5000);});
document.getElementById('searchForm').addEventListener('submit',function(e){
    const q=this.querySelector('input[name="q"]').value.trim();
    if(!q){e.preventDefault();return;}
    if(aiMode){
        e.preventDefault();
        window.location.href='https://mohamedmadoui5195.github.io/Gemalot/?q='+encodeURIComponent(q);
        return;
    }
});
document.querySelector('.search-input').addEventListener('keypress',function(e){if(e.key==='Enter'){document.getElementById('searchForm').submit();}});
function toggleAIMode(){
    aiMode=!aiMode;
    const btn=document.getElementById('aiModeBtn');
    const input=document.querySelector('.search-input');
    const box=document.querySelector('.search-box');
    if(aiMode){
        btn.classList.add('active');
        btn.textContent='AI mode ✓';
        input.placeholder='اسأل AI أي شيء...';
        if(box) box.style.boxShadow='0 0 0 2px #9f7aea, 0 8px 32px rgba(102,126,234,0.5)';
    }else{
        btn.classList.remove('active');
        btn.textContent='AI mode';
        input.placeholder='Search';
        if(box) box.style.boxShadow='';
    }
}
function handleImageSearch(input){
    if(!input.files||!input.files[0])return;
    const file=input.files[0];
    const searchInput=document.querySelector('.search-input');
    searchInput.value='جاري قراءة محتوى الصورة...';
    searchInput.disabled=true;
    const reader=new FileReader();
    reader.onload=function(e){
        const img=new Image();
        img.onload=function(){
            if(!window.Tesseract){
                const s=document.createElement('script');
                s.src='https://cdn.jsdelivr.net/npm/tesseract.js@5/dist/tesseract.min.js';
                s.onload=function(){doOCR(e.target.result);};
                s.onerror=function(){doDirect(e.target.result);};
                document.head.appendChild(s);
            }else{doOCR(e.target.result);}
            function doOCR(dataUrl){
                searchInput.value='جاري استخراج النصوص والعناوين والألوان...';
                Tesseract.recognize(dataUrl,'ara+eng').then(function(r){
                    const txt=r.data.text.trim();
                    if(txt.length>2){
                        searchInput.disabled=false;
                        searchInput.value=txt.substring(0,200);
                        setTimeout(function(){document.getElementById('searchForm').submit();},400);
                    }else{doDirect(dataUrl);}
                }).catch(function(){doDirect(dataUrl);});
            }
            function doDirect(dataUrl){
                searchInput.disabled=false;
                try{localStorage.setItem('lastSearchedImage',dataUrl);}catch(err){}
                if(aiMode){
                    window.location.href='https://mohamedmadoui5195.github.io/Gemalot/?q='+encodeURIComponent('حلل محتوى هذه الصورة');
                }else{
                    searchInput.value='صورة';
                    setTimeout(function(){document.getElementById('searchForm').submit();},400);
                }
            }
        };
        img.src=e.target.result;
    };
    reader.readAsDataURL(file);
}
let recognition=null;
function startVoiceSearch(){
    const SR=window.SpeechRecognition||window.webkitSpeechRecognition;
    if(!SR){alert('المتصفح لا يدعم البحث الصوتي - استخدم Chrome');return;}
    const mic=document.getElementById('micBtn');
    if(recognition){try{recognition.stop();}catch(e){}recognition=null;mic.style.fill='#6ba3e0';return;}
    try{
        recognition=new SR();
        recognition.lang='';
        recognition.interimResults=false;
        mic.style.fill='#ff3b30';
        recognition.onresult=function(ev){
            const txt=ev.results[0][0].transcript.trim();
            document.querySelector('.search-input').value=txt;
            mic.style.fill='#6ba3e0';recognition=null;
            setTimeout(function(){document.getElementById('searchForm').submit();},500);
        };
        recognition.onerror=function(){mic.style.fill='#6ba3e0';recognition=null;};
        recognition.onend=function(){mic.style.fill='#6ba3e0';recognition=null;};
        recognition.start();
    }catch(err){alert('خطأ: '+err.message);}
}
</script>
</body>
</html>
