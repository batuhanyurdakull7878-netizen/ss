<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Yurdakul Network - Emek Skyblock</title>
    <!-- Google Fonts ve İkonlar -->
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Poppins', sans-serif;
        }

        body {
            background-color: #0f172a;
            color: #f8fafc;
        }

        /* Header Tasarımı */
        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px 8%;
            background-color: rgba(15, 23, 42, 0.95);
            border-bottom: 1px solid #1e293b;
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .logo h2 {
            color: #fff;
            font-weight: 800;
            cursor: pointer;
        }

        .logo span {
            color: #38bdf8;
        }

        nav a {
            color: #94a3b8;
            text-decoration: none;
            margin: 0 15px;
            font-weight: 600;
            transition: 0.3s;
            cursor: pointer;
        }

        nav a:hover, nav a.active {
            color: #38bdf8;
        }

        .auth-buttons button {
            background: #38bdf8;
            color: #0f172a;
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            transition: 0.3s;
        }

        .auth-buttons button:hover {
            background: #0ea5e9;
        }

        /* İçerik Alanları */
        .page-section {
            display: none;
            padding: 50px 8%;
            min-height: 80vh;
        }

        .page-section.active {
            display: block;
        }

        /* Ana Sayfa (Hero) */
        .hero {
            height: 75vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            background: linear-gradient(rgba(15, 23, 42, 0.75), rgba(15, 23, 42, 0.95)), #0f172a;
        }

        .hero h1 {
            font-size: 3rem;
            font-weight: 800;
            margin-bottom: 15px;
        }

        .hero p {
            color: #94a3b8;
            font-size: 1.1rem;
            margin-bottom: 30px;
        }

        /* IP Kopyalama Kutusu */
        .ip-box {
            background-color: #1e293b;
            border: 2px solid #334155;
            padding: 15px 30px;
            border-radius: 12px;
            display: inline-flex;
            align-items: center;
            gap: 15px;
            cursor: pointer;
            transition: 0.3s;
        }

        .ip-box:hover {
            border-color: #38bdf8;
            transform: translateY(-2px);
        }

        .ip-box span {
            font-size: 1.2rem;
            font-weight: 600;
            color: #fff;
        }

        .ip-box i {
            color: #38bdf8;
            font-size: 1.2rem;
        }

        /* Mağaza Kartları */
        .section-title {
            font-size: 2rem;
            margin-bottom: 30px;
            text-align: center;
            color: #fff;
        }

        .shop-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 25px;
        }

        .shop-card {
            background: #1e293b;
            border: 1px solid #334155;
            border-radius: 12px;
            padding: 25px;
            text-align: center;
            transition: 0.3s;
        }

        .shop-card:hover {
            border-color: #38bdf8;
            transform: translateY(-5px);
        }

        .shop-card h3 {
            font-size: 1.5rem;
            color: #38bdf8;
            margin-bottom: 10px;
        }

        .shop-card p {
            color: #94a3b8;
            font-size: 0.95rem;
            margin-bottom: 20px;
        }

        .price {
            font-size: 1.3rem;
            font-weight: 800;
            color: #4ade80;
            margin-bottom: 20px;
        }

        .buy-btn {
            background: #38bdf8;
            color: #0f172a;
            border: none;
            width: 100%;
            padding: 12px;
            border-radius: 8px;
            font-weight: 700;
            cursor: pointer;
            transition: 0.3s;
        }

        .buy-btn:hover {
            background: #0ea5e9;
        }

        /* Sıralamalar ve Kurallar Tabloları */
        .content-box {
            background: #1e293b;
            border: 1px solid #334155;
            border-radius: 12px;
            padding: 30px;
            max-width: 800px;
            margin: 0 auto;
        }

        .rank-item, .rule-item {
            display: flex;
            justify-content: space-between;
            padding: 15px 0;
            border-bottom: 1px solid #334155;
        }

        .rank-item:last-child, .rule-item:last-child {
            border-bottom: none;
        }

        /* Modal (Giriş/Kayıt ve Google Giriş Penceresi) */
        .modal {
            display: none;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0, 0, 0, 0.8);
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }

        .modal-content {
            background: #1e293b;
            padding: 40px;
            border-radius: 16px;
            width: 100%;
            max-width: 400px;
            text-align: center;
            position: relative;
            border: 1px solid #334155;
        }

        .modal-content h3 {
            margin-bottom: 20px;
            color: #fff;
        }

        .close-btn {
            position: absolute;
            top: 15px; right: 20px;
            font-size: 1.5rem;
            color: #94a3b8;
            cursor: pointer;
        }

        .google-btn {
            background: #fff;
            color: #334155;
            border: none;
            width: 100%;
            padding: 12px;
            border-radius: 8px;
            font-weight: 600;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            cursor: pointer;
            transition: 0.3s;
            margin-top: 15px;
        }

        .google-btn:hover {
            background: #f1f5f9;
        }

        .google-btn i {
            color: #ea4335;
            font-size: 1.2rem;
        }
    </style>
</head>
<body>

    <!-- Üst Menü -->
    <header>
        <div class="logo" onclick="sayfaGoster('anasayfa')">
            <h2>YURDAKUL<span>NW</span></h2>
        </div>
        <nav>
            <a onclick="sayfaGoster('anasayfa')" class="nav-link active" id="link-anasayfa">Ana Sayfa</a>
            <a onclick="sayfaGoster('magaza')" class="nav-link" id="link-magaza">Mağaza</a>
            <a onclick="sayfaGoster('siralamalar')" class="nav-link" id="link-siralamalar">Sıralamalar</a>
            <a onclick="sayfaGoster('kurallar')" class="nav-link" id="link-kurallar">Kurallar</a>
        </nav>
        <div class="auth-buttons">
            <button onclick="modalAc()">Giriş / Kayıt Ol</button>
        </div>
    </header>

    <!-- 1. ANA SAYFA -->
    <section id="anasayfa" class="page-section hero active">
        <div class="hero-content">
            <h1>En İyi Emek Skyblock Deneyimi</h1>
            <p>Özel minyonlar, çiftçi sistemi, rütbe hammadde ve gelişmiş kasalar seni bekliyor!</p>
            
            <div class="ip-box" onclick="ipKopyala()">
                <span id="sunucuIp">oyna.yurdakulnw.com</span>
                <i class="fa-solid fa-copy"></i>
            </div>
            <br>
            <span id="kopyaBilgi" style="display:none; color: #4ade80; font-size: 14px; margin-top: 10px;">IP Kopyalandı!</span>
        </div>
    </section>

    <!-- 2. MAĞAZA (VIP, Spawner, Kasalar, Minyonlar) -->
    <section id="magaza" class="page-section">
        <h2 class="section-title">Sunucu Mağazası</h2>
        <div class="shop-grid">
            <!-- VIP -->
            <div class="shop-card">
                <h3>VIP Üyelik (30 Gün)</h3>
                <p>Özel uçuş, /kit vip, /feed, ek sefert ve renkli sohbet özellikleri.</p>
                <div class="price">50 TL</div>
                <button class="buy-btn" onclick="satinAl('VIP Üyelik')">Satın Al</button>
            </div>
            <!-- Spawner -->
            <div class="shop-card">
                <h3>İnek Spawner</h3>
                <p>Adanda otomatik para ve deri kasmanı sağlayacak spawner.</p>
                <div class="price">30 TL</div>
                <button class="buy-btn" onclick="satinAl('İnek Spawner')">Satın Al</button>
            </div>
            <!-- Anahtar Kasalar -->
            <div class="shop-card">
                <h3>5x Efsanevi Kasa Anahtarı</h3>
                <p>En değerli eşyaların çıktığı özel kasaları açmak için anahtar.</p>
                <div class="price">25 TL</div>
                <button class="buy-btn" onclick="satinAl('5x Kasa Anahtarı')">Satın Al</button>
            </div>
            <!-- Minyon Paketi -->
            <div class="shop-card">
                <h3>Madenci Minyonu (Lv. 3)</h3>
                <p>Sen oyunda yokken bile senin için maden kazan ve depolayan minyon.</p>
                <div class="price">40 TL</div>
                <button class="buy-btn" onclick="satinAl('Madenci Minyonu')">Satın Al</button>
            </div>
        </div>
    </section>

    <!-- 3. SIRALAMALAR -->
    <section id="siralamalar" class="page-section">
        <h2 class="section-title">En İyi Adalar (Ada Top)</h2>
        <div class="content-box">
            <div class="rank-item">
                <span>🥇 1. Oyuncu: <strong>KaanYurdakul</strong></span>
                <span style="color: #38bdf8;">Ada Seviyesi: 1,450,200</span>
            </div>
            <div class="rank-item">
                <span>🥈 2. Oyuncu: <strong>Nelvoka</strong></span>
                <span style="color: #38bdf8;">Ada Seviyesi: 1,120,000</span>
            </div>
            <div class="rank-item">
                <span>🥉 3. Oyuncu: <strong>ProGamerTR</strong></span>
                <span style="color: #38bdf8;">Ada Seviyesi: 950,400</span>
            </div>
        </div>
    </section>

    <!-- 4. KURALLAR -->
    <section id="kurallar" class="page-section">
        <h2 class="section-title">Sunucu Kuralları</h2>
        <div class="content-box">
            <div class="rule-item">
                <span>1. Küfür, hakaret ve argo kesinlikle yasaktır.</span>
                <strong style="color: #ef4444;">Mute / Ban</strong>
            </div>
            <div class="rule-item">
                <span>2. Hile, macro veya hileli mod kullanmak yasaktır.</span>
                <strong style="color: #ef4444;">Sınırsız Ban</strong>
            </div>
            <div class="rule-item">
                <span>3. Adada dolandırıcılık (ada güvenliği hariç) yasaktır.</span>
                <strong style="color: #ef4444;">İşlem</strong>
            </div>
            <div class="rule-item">
                <span>4. Sohbeti kirletmek, spam ve reklam yapmak yasaktır.</span>
                <strong style="color: #ef4444;">Susturma</strong>
            </div>
        </div>
    </section>

    <!-- GİRİŞ / KAYIT MODALI (Gmail ile Kayıt Seçeneği) -->
    <div id="authModal" class="modal">
        <div class="modal-content">
            <span class="close-btn" onclick="modalKapat()">&times;</span>
            <h3>Sunucuya Giriş Yap</h3>
            <p style="color: #94a3b8; font-size: 14px; margin-bottom: 20px;">Oyun içi hesabınızla senkronize olmak için giriş yapın.</p>
            
            <button class="google-btn" onclick="googleIleGiris()">
                <i class="fa-brands fa-google"></i> Google (Gmail) ile Devam Et
            </button>
        </div>
    </div>

    <!-- JavaScript Kodları -->
    <script>
        // Sayfa geçiş fonksiyonu
        function sayfaGoster(sayfaId) {
            document.querySelectorAll('.page-section').forEach(sec => sec.classList.remove('active'));
            document.querySelectorAll('.nav-link').forEach(link => link.classList.remove('active'));
            
            document.getElementById(sayfaId).classList.add('active');
            document.getElementById('link-' + sayfaId).classList.add('active');
        }

        // IP Kopyalama Fonksiyonu ve Bildirimi
        function ipKopyala() {
            const ipText = document.getElementById("sunucuIp").innerText;
            navigator.clipboard.writeText(ipText);
            const bilgi = document.getElementById("kopyaBilgi");
            bilgi.style.display = "inline-block";
            setTimeout(() => { 
                bilgi.style.display = "none"; 
            }, 2000);
        }

        // Modal (Giriş Penceresi) İşlemleri
        function modalAc() { document.getElementById("authModal").style.display = "flex"; }
        function modalKapat() { document.getElementById("authModal").style.display = "none"; }

        function googleIleGiris() {
            alert("Google (Gmail) ile giriş tetiklendi!");
            modalKapat();
        }

        // Mağaza Satın Alım Uyarısı
        function satinAl(urunAdi) {
            alert(urunAdi + " sepete eklendi! Ödeme ekranına yönlendiriliyorsunuz...");
        }
    </script>
</body>
</html>
