<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Bing</title>
    <link rel="icon" href="icon.png" type="image/png">
    <link rel="apple-touch-icon" href="icon.png">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
        }

        body {
            background: #0a1628;
            color: #e8f0fe;
            min-height: 100vh;
            overflow-x: hidden;
            position: relative;
            padding-bottom: 110px; /* مساحة تحت عشان ما يختبئ تحت الشريط السفلي */
        }

        /* ================= الشاشة الترحيبية الاحترافية ================= */
        .bing-splash-screen {
            position: fixed;
            inset: 0;
            background: #050b14;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 99999;
            overflow: hidden;
            transition: opacity 0.8s cubic-bezier(0.4, 0, 0.2, 1), visibility 0.8s, transform 0.8s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .bing-splash-screen.hidden {
            opacity: 0;
            visibility: hidden;
            transform: scale(1.12);
            pointer-events: none;
        }

        .bing-splash-bg {
            position: absolute;
            inset: 0;
            background-image: 
                radial-gradient(circle at 50% 50%, rgba(0, 195, 255, 0.15), transparent 60%),
                linear-gradient(rgba(255, 255, 255, 0.03) 1px, transparent 1px),
                linear-gradient(90deg, rgba(255, 255, 255, 0.03) 1px, transparent 1px);
            background-size: 100% 100%, 30px 30px, 30px 30px;
            background-position: 0 0, 15px 15px, 15px 15px;
            animation: bgPulse 4s ease-in-out infinite alternate;
        }

        .bing-spinner-wrapper {
            position: relative;
            width: 130px;
            height: 130px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 32px;
            animation: iconPulse 2.5s ease-in-out infinite alternate;
        }

        .bing-spinner-wrapper::before {
            content: '';
            position: absolute;
            inset: -8px;
            border-radius: 38px;
            background: conic-gradient(from 0deg, #00c3ff, #087fff, #7000ff, #00f0ff, #00c3ff);
            animation: rotateConic 2s linear infinite;
            filter: blur(12px);
            opacity: 0.85;
        }

        .bing-spinner-wrapper::after {
            content: '';
            position: absolute;
            inset: -4px;
            border-radius: 35px;
            background: conic-gradient(from 0deg, #00c3ff, #087fff, #7000ff, #00f0ff, #00c3ff);
            animation: rotateConic 2s linear infinite;
        }

        .bing-icon-cover {
            position: absolute;
            inset: 1px;
            background: #050b14;
            border-radius: 31px;
            z-index: 1;
        }

        .bing-splash-icon {
            position: relative;
            z-index: 2;
            width: 110px;
            height: 110px;
            border-radius: 26px;
            object-fit: cover;
            box-shadow: 0 15px 35px rgba(0, 195, 255, 0.3);
        }

        .bing-splash-title {
            position: relative;
            z-index: 2;
            margin-top: 25px;
            font-size: 1.25rem;
            font-weight: 800;
            letter-spacing: 1px;
            background: linear-gradient(135deg, #ffffff 30%, #6fb7ff 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 10px 20px rgba(0, 195, 255, 0.2);
        }

        @keyframes rotateConic {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        @keyframes iconPulse {
            0% { transform: scale(0.96); }
            100% { transform: scale(1.04); }
        }

        @keyframes bgPulse {
            0% { opacity: 0.6; }
            100% { opacity: 1; }
        }
        /* =============================================================== */

        /* الخلفية مثل الصورة */
        .bg {
            position: fixed;
            inset: 0;
            background: url('https://images.unsplash.com/photo-1506905925346-21bda4d32df4?w=1200&q=80') center/cover no-repeat;
            z-index: 0;
        }

        .bg::after {
            content: '';
            position: absolute;
            inset: 0;
            background: linear-gradient(180deg, 
                rgba(5, 15, 35, 0.55) 0%, 
                rgba(5, 20, 45, 0.35) 35%, 
                rgba(8, 25, 55, 0.75) 70%, 
                rgba(6, 18, 40, 0.92) 100%);
        }

        /* شريط الحالة */
        .status-bar {
            position: relative;
            z-index: 10;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 8px 16px 4px;
            font-size: 13px;
            font-weight: 600;
            color: #fff;
            text-shadow: 0 1px 3px rgba(0,0,0,0.5);
        }

        .status-right {
            display: flex;
            align-items: center;
            gap: 6px;
            font-size: 12px;
        }

        /* أيقونة الحساب */
        .profile {
            position: relative;
            z-index: 10;
            margin: 8px 16px 0;
        }

        .profile-btn {
            width: 42px;
            height: 42px;
            border-radius: 50%;
            background: linear-gradient(135deg, #1e3a5f, #0d2137);
            border: 2px solid rgba(100, 180, 255, 0.4);
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 4px 12px rgba(0,0,0,0.4);
            overflow: hidden;
        }

        .profile-btn img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .profile-btn .default-icon {
            width: 24px;
            height: 24px;
            fill: #7eb8ff;
        }

        /* منطقة البحث الرئيسية */
        .main {
            position: relative;
            z-index: 5;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 0 18px;
            margin-top: 28vh;
            min-height: 45vh;
        }

        /* شريط البحث */
        .search-box {
            width: 100%;
            max-width: 520px;
            background: rgba(12, 28, 52, 0.92);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border-radius: 50px;
            padding: 14px 18px;
            display: flex;
            align-items: center;
            gap: 12px;
            box-shadow: 0 8px 32px rgba(0, 20, 50, 0.6), 
                        0 0 0 1px rgba(80, 160, 255, 0.25);
            transition: all 0.25s ease;
        }

        .search-box:focus-within {
            box-shadow: 0 8px 36px rgba(0, 40, 90, 0.7), 
                        0 0 0 2px rgba(100, 180, 255, 0.5);
            background: rgba(15, 35, 65, 0.95);
        }

        .search-icon {
            width: 22px;
            height: 22px;
            fill: #6ba3e0;
            flex-shrink: 0;
        }

        .search-input {
            flex: 1;
            background: transparent;
            border: none;
            outline: none;
            color: #e8f4ff;
            font-size: 17px;
            font-weight: 400;
            direction: rtl;
        }

        .search-input::placeholder {
            color: #7a9cc0;
        }

        .search-actions {
            display: flex;
            align-items: center;
            gap: 14px;
        }

        .action-btn {
            width: 26px;
            height: 26px;
            fill: #6ba3e0;
            cursor: pointer;
            transition: fill 0.2s;
        }

        .action-btn:active {
            fill: #a8d4ff;
        }

        /* البطاقات السفلية */
        .cards {
            width: 100%;
            max-width: 520px;
            display: flex;
            gap: 10px;
            margin-top: 28px;
            overflow-x: auto;
            padding-bottom: 8px;
            scrollbar-width: none;
        }

        .cards::-webkit-scrollbar {
            display: none;
        }

        .card {
            flex: 0 0 auto;
            background: rgba(12, 30, 58, 0.88);
            backdrop-filter: blur(12px);
            border-radius: 18px;
            padding: 14px 16px;
            min-width: 130px;
            box-shadow: 0 4px 20px rgba(0, 15, 40, 0.5);
            border: 1px solid rgba(70, 140, 220, 0.2);
            cursor: pointer;
            transition: transform 0.2s, background 0.2s;
        }

        .card:active {
            transform: scale(0.97);
            background: rgba(18, 40, 75, 0.95);
        }

        .card-title {
            font-size: 14px;
            font-weight: 600;
            color: #d0e6ff;
            margin-bottom: 4px;
        }

        .card-desc {
            font-size: 12px;
            color: #8bb0d8;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        /* شريط التنقل السفلي */
        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            z-index: 20;
            background: rgba(8, 20, 42, 0.96);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border-top: 1px solid rgba(60, 120, 200, 0.25);
            padding: 10px 0 max(12px, env(safe-area-inset-bottom));
            display: flex;
            justify-content: space-around;
            align-items: center;
        }

        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 4px;
            text-decoration: none;
            color: #7a9cc0;
            font-size: 11px;
            font-weight: 500;
            padding: 6px 12px;
            border-radius: 12px;
            transition: color 0.2s, background 0.2s;
            min-width: 64px;
        }

        .nav-item.active {
            color: #5eb0ff;
        }

        .nav-item:active {
            background: rgba(40, 90, 160, 0.25);
        }

        .nav-icon {
            width: 26px;
            height: 26px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 22px;
            line-height: 1;
        }

        .gemini-logo {
            width: 28px;
            height: 28px;
            background: linear-gradient(135deg, #4a90e2, #1a5fb4, #0d47a1);
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 14px;
            font-weight: 700;
            color: #fff;
            box-shadow: 0 2px 8px rgba(30, 100, 200, 0.5);
        }

        @media (max-width: 480px) {
            .main {
                margin-top: 26vh;
            }
            .search-box {
                padding: 13px 16px;
            }
            .card {
                min-width: 120px;
                padding: 12px 14px;
            }
        }
    </style>
</head>
<body>
    <!-- الشاشة الترحيبية -->
    <div class="bing-splash-screen" id="bingSplash">
        <div class="bing-splash-bg"></div>
        <div class="bing-spinner-wrapper">
            <div class="bing-icon-cover"></div>
            <img src="icon.png" class="bing-splash-icon" alt="Bing Icon" onerror="this.src='data:image/svg+xml;utf8,<svg xmlns=\'http://www.w3.org/2000/svg\' viewBox=\'0 0 100 100\'><rect width=\'100\' height=\'100\' rx=\'25\' fill=\'%23087fff\'/><text x=\'50\' y=\'68\' font-size=\'55\' font-weight=\'bold\' text-anchor=\'middle\' fill=\'white\'>B</text></svg>'">
        </div>
        <div class="bing-splash-title">Alislamiah Bing</div>
    </div>

    <div class="bg"></div>

    <!-- شريط الحالة -->
    <div class="status-bar">
        <span>01:05</span>
        <div class="status-right">
            <span>58.1 KB/s</span>
            <span>4G</span>
            <span>21</span>
            <span>⚡</span>
        </div>
    </div>

    <!-- أيقونة الحساب -->
    <div class="profile">
        <div class="profile-btn">
            <img src="icon.png" alt="Icon" onerror="this.style.display='none'; this.nextElementSibling.style.display='block';">
            <svg class="default-icon" style="display:none;" viewBox="0 0 24 24">
                <path d="M12 12c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm0 2c-2.67 0-8 1.34-8 4v2h16v-2c0-2.66-5.33-4-8-4z"/>
            </svg>
        </div>
    </div>

    <!-- المحتوى الرئيسي -->
    <div class="main">
        <!-- شريط البحث -->
        <form class="search-box" action="results_full.html" method="GET" id="searchForm">
            <svg class="search-icon" viewBox="0 0 24 24">
                <path d="M15.5 14h-.79l-.28-.27A6.471 6.471 0 0 0 16 9.5 6.5 6.5 0 1 0 9.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"/>
            </svg>
            <input type="text" name="q" class="search-input" placeholder="Search" autocomplete="off" autofocus>
            <div class="search-actions">
                <svg class="action-btn" viewBox="0 0 24 24" onclick="alert('الكاميرا')">
                    <path d="M12 15.2c1.76 0 3.2-1.44 3.2-3.2s-1.44-3.2-3.2-3.2-3.2 1.44-3.2 3.2 1.44 3.2 3.2 3.2zm0-8c2.65 0 4.8 2.15 4.8 4.8s-2.15 4.8-4.8 4.8-4.8-2.15-4.8-4.8 2.15-4.8 4.8-4.8zm8.4-2H18l-1.2-1.6c-.3-.4-.8-.6-1.3-.6H8.5c-.5 0-1 .2-1.3.6L6 5.2H3.6C2.7 5.2 2 5.9 2 6.8v12.4c0 .9.7 1.6 1.6 1.6h16.8c.9 0 1.6-.7 1.6-1.6V6.8c0-.9-.7-1.6-1.6-1.6z"/>
                </svg>
                <svg class="action-btn" viewBox="0 0 24 24" onclick="alert('الميكروفون')">
                    <path d="M12 14c1.66 0 3-1.34 3-3V5c0-1.66-1.34-3-3-3S9 3.34 9 5v6c0 1.66 1.34 3 3 3zm-1-9c0-.55.45-1 1-1s1 .45 1 1v6c0 .55-.45 1-1 1s-1-.45-1-1V5zm6 6c0 2.76-2.24 5-5 5s-5-2.24-5-5H5c0 3.53 2.61 6.43 6 6.92V21h2v-3.08c3.39-.49 6-3.39 6-6.92h-2z"/>
                </svg>
            </div>
        </form>

        <!-- البطاقات -->
        <div class="cards">
            <a href="https://mohamedmadoui5195.github.io/Alislamiah-search-console/" class="card" style="text-decoration:none;color:inherit;">
                <div class="card-title">Alislamiah Search</div>
                <div class="card-desc">
                    Search Console
                    <span style="width:14px;height:14px;background:linear-gradient(135deg,#4fc3f7,#0288d1);border-radius:4px;display:inline-block;"></span>
                </div>
            </a>
            <a href="https://mohamedmadoui5195.github.io/Alislamiah-services/" class="card" style="text-decoration:none;color:inherit;">
                <div class="card-title">Alislamiah Services</div>
                <div class="card-desc">
                    الخدمات
                    <span style="width:14px;height:14px;background:linear-gradient(135deg,#64b5f6,#1565c0);border-radius:4px;display:inline-block;"></span>
                </div>
            </a>
            <a href="https://mohamedmadoui5195.github.io/Alislamiah-_net/" class="card" style="text-decoration:none;color:inherit;">
                <div class="card-title">Alislamiah Net</div>
                <div class="card-desc">
                    الشبكة
                    <span style="width:14px;height:14px;background:linear-gradient(135deg,#42a5f5,#0d47a1);border-radius:4px;display:inline-block;"></span>
                </div>
            </a>
        </div>
    </div>

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

.ad-card-image {
  width: 100%;
  height: 180px;
  object-fit: cover;
  display: block;
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

.ad-card-btn.green {
  background: linear-gradient(135deg, #48bb78 0%, #38a169 100%);
  box-shadow: 0 4px 14px rgba(72,187,120,0.35);
}
.ad-card-btn.green:hover {
  background: linear-gradient(135deg, #38a169 0%, #2f855a 100%);
}

.ad-card-btn.purple {
  background: linear-gradient(135deg, #9f7aea 0%, #805ad5 100%);
  box-shadow: 0 4px 14px rgba(159,122,234,0.35);
}
.ad-card-btn.purple:hover {
  background: linear-gradient(135deg, #805ad5 0%, #6b46c1 100%);
}
</style>

<!-- البطاقة الأولى -->
<div class="ad-card">
  <span class="ad-badge">مادة إعلانية</span>
  <img src="Screenshot_20261011-191020.jpg" alt="مداد" class="ad-card-image">
  <div class="ad-card-content">
    <h2 class="ad-card-title">مداد</h2>
    <p class="ad-card-desc">أقوى منصة لصنع الألعاب والمواقع والبرامج، حول أفكارك إلى واقع</p>
    <a href="https://nazim10-u.github.io/nazim/" class="ad-card-btn" target="_blank">زيارة الموقع</a>
  </div>
</div>

<!-- البطاقة الثانية -->
<div class="ad-card">
  <span class="ad-badge">مادة إعلانية</span>
  <img src="Screenshot_20261011-195632.jpg" alt="alarabiya.net" class="ad-card-image">
  <div class="ad-card-content">
    <h2 class="ad-card-title">alarabiya.net</h2>
    <p class="ad-card-desc">تابعوا الأخبار العربية والعالمية هنا</p>
    <a href="https://www.alarabiya.net" class="ad-card-btn green" target="_blank">زيارة الموقع</a>
  </div>
</div>

<!-- البطاقة الثالثة -->
<div class="ad-card">
  <span class="ad-badge">مادة إعلانية</span>
  <img src="Screenshot_20261011-200809.jpg" alt="Alislamiah search console" class="ad-card-image">
  <div class="ad-card-content">
    <h2 class="ad-card-title">Alislamiah search console</h2>
    <p class="ad-card-desc">آداة مشرفي المواقع... إن كان لديك موقع أطلب هنا لكي نفهرسه لك ويظهر في نتائج البحث</p>
    <a href="https://mohamedmadoui5195.github.io/Alislamiah-search-console/" class="ad-card-btn purple" target="_blank">زيارة الموقع</a>
  </div>
</div>

    <!-- شريط التنقل السفلي -->
    <nav class="bottom-nav">
        <a href="index.html" class="nav-item active">
            <div class="nav-icon">🏠</div>
            <span>البحث</span>
        </a>
        <a href="results_full.html" class="nav-item">
            <div class="nav-icon">🔍</div>
            <span>بحث</span>
        </a>
        <a href="https://mohamedmadoui5195.github.io/Gemalot/" class="nav-item">
            <div class="nav-icon">
                <div class="gemini-logo">G</div>
            </div>
            <span>Gemalot</span>
        </a>
    </nav>

    <script>
        // مؤقت الـ 5 ثوانٍ لإخفاء الشاشة الترحيبية
        window.addEventListener("DOMContentLoaded", function () {
            setTimeout(function () {
                var splash = document.getElementById("bingSplash");
                if (splash) {
                    splash.classList.add("hidden");
                }
            }, 5000);
        });

        // إرسال البحث إلى صفحة النتائج
        document.getElementById('searchForm').addEventListener('submit', function(e) {
            const q = this.querySelector('input[name="q"]').value.trim();
            if (!q) {
                e.preventDefault();
                return;
            }
        });

        // دعم الضغط على Enter
        document.querySelector('.search-input').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                document.getElementById('searchForm').submit();
            }
        });

        if ('serviceWorker' in navigator) {
            window.addEventListener('load', () => {
                navigator.serviceWorker.register('/sw.js')
                    .then((reg) => console.log('Service Worker registered', reg))
                    .catch((err) => console.error('Service Worker failed', err));
            });
        }
    </script>
</body>
</html>
