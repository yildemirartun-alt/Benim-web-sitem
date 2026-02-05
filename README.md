<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fen Lisesi 11 - Görsel Eğitim</title>
    <script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
        }

        .app {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            text-align: center;
            color: white;
            margin-bottom: 30px;
            padding: 20px;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
        }

        .dark-mode {
            background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
        }

        .dark-toggle {
            position: fixed;
            top: 20px;
            right: 20px;
            background: rgba(255,255,255,0.2);
            border: none;
            padding: 10px 20px;
            border-radius: 20px;
            color: white;
            cursor: pointer;
            font-size: 16px;
            backdrop-filter: blur(10px);
            z-index: 1000;
        }

        .dark-toggle:hover {
            background: rgba(255,255,255,0.3);
        }

        .subjects-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 25px;
            margin-bottom: 40px;
        }

        .subject-card {
            background: white;
            border-radius: 20px;
            padding: 30px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            position: relative;
            overflow: hidden;
        }

        .subject-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 40px rgba(0,0,0,0.2);
        }

        .subject-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 5px;
            background: linear-gradient(90deg, var(--color1), var(--color2));
        }

        .subject-icon {
            font-size: 4em;
            margin-bottom: 15px;
        }

        .subject-title {
            font-size: 1.5em;
            font-weight: bold;
            margin-bottom: 10px;
            color: #333;
        }

        .subject-description {
            color: #666;
            font-size: 0.9em;
        }

        .content-view {
            background: white;
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }

        .dark-mode .content-view,
        .dark-mode .subject-card,
        .dark-mode .topic-card,
        .dark-mode .visual-content {
            background: #2d3748;
            color: #e2e8f0;
        }

        .dark-mode .subject-title,
        .dark-mode .topic-title {
            color: #e2e8f0;
        }

        .dark-mode .subject-description,
        .dark-mode .topic-subtitle {
            color: #a0aec0;
        }

        .back-button {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            margin-bottom: 20px;
            transition: all 0.3s ease;
        }

        .back-button:hover {
            transform: scale(1.05);
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        .topics-list {
            display: grid;
            gap: 20px;
            margin-top: 20px;
        }

        .topic-card {
            background: #f8f9fa;
            border-radius: 15px;
            padding: 20px;
            cursor: pointer;
            transition: all 0.3s ease;
            border-left: 5px solid var(--color1);
        }

        .topic-card:hover {
            transform: translateX(10px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .topic-title {
            font-size: 1.3em;
            font-weight: bold;
            margin-bottom: 8px;
            color: #333;
        }

        .topic-subtitle {
            color: #666;
            font-size: 0.9em;
        }

        .visual-content {
            background: white;
            border-radius: 15px;
            padding: 30px;
            margin-top: 20px;
        }

        .visual-section {
            margin-bottom: 30px;
        }

        .visual-section h3 {
            color: var(--color1);
            font-size: 1.5em;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 3px solid var(--color1);
        }

        .diagram {
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            border-radius: 15px;
            padding: 30px;
            margin: 20px 0;
            text-align: center;
            border: 3px solid var(--color1);
        }

        .formula-box {
            background: #fff3cd;
            border-left: 5px solid #ffc107;
            padding: 20px;
            margin: 15px 0;
            border-radius: 10px;
            font-size: 1.2em;
            text-align: center;
        }

        .important-box {
            background: #d1ecf1;
            border-left: 5px solid #0dcaf0;
            padding: 20px;
            margin: 15px 0;
            border-radius: 10px;
        }

        .tip-box {
            background: #d4edda;
            border-left: 5px solid #28a745;
            padding: 20px;
            margin: 15px 0;
            border-radius: 10px;
        }

        .warning-box {
            background: #f8d7da;
            border-left: 5px solid #dc3545;
            padding: 20px;
            margin: 15px 0;
            border-radius: 10px;
        }

        .concept-map {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin: 20px 0;
            justify-content: center;
        }

        .concept-node {
            background: linear-gradient(135deg, var(--color1), var(--color2));
            color: white;
            padding: 15px 25px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        .flow-chart {
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin: 20px 0;
        }

        .flow-step {
            background: var(--color1);
            color: white;
            padding: 20px;
            border-radius: 15px;
            text-align: center;
            position: relative;
        }

        .flow-step::after {
            content: '↓';
            position: absolute;
            bottom: -30px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 2em;
            color: var(--color1);
        }

        .flow-step:last-child::after {
            display: none;
        }

        .info-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin: 20px 0;
        }

        .info-card {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px;
            border-radius: 15px;
            text-align: center;
        }

        .info-card h4 {
            margin-bottom: 10px;
            font-size: 1.2em;
        }

        .yks-badge {
            display: inline-block;
            background: #ff6b6b;
            color: white;
            padding: 5px 15px;
            border-radius: 20px;
            font-size: 0.8em;
            font-weight: bold;
            margin: 5px;
        }

        .memory-technique {
            background: linear-gradient(135deg, #fa709a 0%, #fee140 100%);
            padding: 20px;
            border-radius: 15px;
            margin: 20px 0;
            color: #333;
            font-weight: bold;
        }

        @media (max-width: 768px) {
            .header h1 {
                font-size: 1.8em;
            }
            
            .subjects-grid {
                grid-template-columns: 1fr;
            }
            
            .subject-icon {
                font-size: 3em;
            }
        }
    </style>
</head>
<body>
    <div id="root"></div>

    <script type="text/babel">
        const { useState, useEffect } = React;

        const subjects = [
            {
                id: 'matematik',
                name: 'Matematik',
                icon: '📐',
                color1: '#667eea',
                color2: '#764ba2',
                description: 'Fonksiyonlar, Polinomlar, Trigonometri ve daha fazlası',
                topics: [
                    { id: 1, title: 'Fonksiyonlar', subtitle: 'Tanım, Grafik, Özellikler' },
                    { id: 2, title: 'Polinomlar', subtitle: 'İşlemler, Çarpanlara Ayırma' },
                    { id: 3, title: '2. Derece Denklemler', subtitle: 'Çözüm Yöntemleri, Diskriminant' },
                    { id: 4, title: 'Trigonometri', subtitle: 'Trigonometrik Fonksiyonlar, Özdeşlikler' },
                    { id: 5, title: 'Analitik Geometri', subtitle: 'Doğru, Çember, Konikler' },
                    { id: 6, title: 'Diziler', subtitle: 'Aritmetik ve Geometrik Diziler' },
                    { id: 7, title: 'Limit ve Süreklilik', subtitle: 'Limit Kavramı, Belirsizlikler' },
                ]
            },
            {
                id: 'fizik',
                name: 'Fizik',
                icon: '⚛️',
                color1: '#f093fb',
                color2: '#f5576c',
                description: 'Kuvvet-Hareket, Enerji, Elektrik, Manyetizma',
                topics: [
                    { id: 1, title: 'Elektrik ve Manyetizma', subtitle: 'Elektrik Yük, Alan, Potansiyel' },
                    { id: 2, title: 'Kuvvet ve Hareket', subtitle: "Newton Yasaları, Momentum" },
                    { id: 3, title: 'Enerji', subtitle: 'İş, Güç, Mekanik Enerji' },
                    { id: 4, title: 'Tork', subtitle: 'Dönme Hareketi, Açısal Momentum' },
                    { id: 5, title: 'Basit Harmonik Hareket', subtitle: 'Yay, Sarkaç, Dalga' },
                    { id: 6, title: 'Elektrik Devreleri', subtitle: 'Ohm Yasası, Kirchhoff Kuralları' },
                ]
            },
            {
                id: 'kimya',
                name: 'Kimya',
                icon: '🧪',
                color1: '#4facfe',
                color2: '#00f2fe',
                description: 'Gazlar, Çözeltiler, Tepkimeler, Kimyasal Denge',
                topics: [
                    { id: 1, title: 'Gazlar', subtitle: 'Gaz Yasaları, İdeal Gaz Denklemi' },
                    { id: 2, title: 'Çözeltiler', subtitle: 'Derişim, Çözünürlük, Koligatif Özellikler' },
                    { id: 3, title: 'Tepkime Hızı ve Denge', subtitle: 'Hız Faktörleri, Denge Sabiti' },
                    { id: 4, title: 'Asit-Baz Dengesi', subtitle: 'pH, Tampon Çözeltiler' },
                    { id: 5, title: 'Çökelme Tepkimeleri', subtitle: 'Çözünürlük Çarpımı' },
                    { id: 6, title: 'Elektrokimya', subtitle: 'Redoks, Pil, Elektroliz' },
                ]
            },
            {
                id: 'biyoloji',
                name: 'Biyoloji',
                icon: '🧬',
                color1: '#43e97b',
                color2: '#38f9d7',
                description: 'Sistemler, Hücre, Genetik, Ekoloji',
                topics: [
                    { id: 1, title: 'Sinir Sistemi', subtitle: 'Nöron, Sinaps, MSS, SSS' },
                    { id: 2, title: 'Endokrin Sistem', subtitle: 'Hormonlar, Bezler' },
                    { id: 3, title: 'Dolaşım Sistemi', subtitle: 'Kalp, Damarlar, Kan' },
                    { id: 4, title: 'Solunum Sistemi', subtitle: 'Akciğerler, Gaz Alışverişi' },
                    { id: 5, title: 'Boşaltım Sistemi', subtitle: 'Böbrek, Nefron' },
                    { id: 6, title: 'Üreme Sistemi', subtitle: 'Eşeyli ve Eşeysiz Üreme' },
                    { id: 7, title: 'Destek ve Hareket', subtitle: 'İskelet, Kas Sistemi' },
                ]
            },
            {
                id: 'edebiyat',
                name: 'Türk Dili ve Edebiyatı',
                icon: '📚',
                color1: '#fa709a',
                color2: '#fee140',
                description: 'Edebi Akımlar, Dönemler, Yazarlar, Eserler',
                topics: [
                    { id: 1, title: 'Tanzimat Dönemi', subtitle: 'Yazarlar, Eserler, Özellikler' },
                    { id: 2, title: 'Servet-i Fünun', subtitle: 'Akımın Özellikleri, Temsilcileri' },
                    { id: 3, title: 'Fecr-i Ati', subtitle: 'Sanat Anlayışı, Yazarlar' },
                    { id: 4, title: 'Milli Edebiyat', subtitle: 'İlkeler, Şairler, Yazarlar' },
                    { id: 5, title: 'Cumhuriyet Dönemi Şiiri', subtitle: 'Akımlar, Şairler' },
                    { id: 6, title: 'Cumhuriyet Dönemi Romanı', subtitle: 'Yazarlar, Eserler' },
                    { id: 7, title: 'Tiyatro ve Deneme', subtitle: 'Türk Tiyatrosu, Denemeciler' },
                ]
            },
            {
                id: 'cografya',
                name: 'Coğrafya',
                icon: '🌍',
                color1: '#ffecd2',
                color2: '#fcb69f',
                description: 'Türkiye Coğrafyası, Ekonomi, Nüfus, Yer Şekilleri',
                topics: [
                    { id: 1, title: 'Türkiye\'nin Fiziki Coğrafyası', subtitle: 'Yer Şekilleri, İklim' },
                    { id: 2, title: 'Türkiye\'nin Beşeri Coğrafyası', subtitle: 'Nüfus, Yerleşme' },
                    { id: 3, title: 'Ekonomik Coğrafya', subtitle: 'Tarım, Sanayi, Ticaret' },
                    { id: 4, title: 'Doğal Kaynaklar', subtitle: 'Madenler, Enerji' },
                    { id: 5, title: 'Çevre ve Toplum', subtitle: 'Çevre Sorunları, Sürdürülebilirlik' },
                    { id: 6, title: 'Bölgeler Coğrafyası', subtitle: 'Türkiye\'nin Coğrafi Bölgeleri' },
                ]
            },
            {
                id: 'tarih',
                name: 'Tarih',
                icon: '📜',
                color1: '#ff9a56',
                color2: '#ff6a88',
                description: 'Osmanlı, İnkılaplar, Yakın Dönem Tarih',
                topics: [
                    { id: 1, title: 'Osmanlı Devleti\'nin Duraklama Dönemi', subtitle: 'Sebepleri, Gelişmeler' },
                    { id: 2, title: 'Osmanlı Devleti\'nin Gerileme Dönemi', subtitle: 'Savaşlar, Antlaşmalar' },
                    { id: 3, title: 'Islahat Hareketleri', subtitle: 'Lale Devri, Tanzimat, Meşrutiyet' },
                    { id: 4, title: 'XX. Yüzyıl Başlarında Osmanlı', subtitle: 'II. Abdülhamit, Balkan Savaşları' },
                    { id: 5, title: 'Birinci Dünya Savaşı', subtitle: 'Osmanlı\'nın Savaşa Girişi, Cepheler' },
                    { id: 6, title: 'Milli Mücadele', subtitle: 'Kurtuluş Savaşı, Kongreler' },
                    { id: 7, title: 'Atatürk İlkeleri ve İnkılap Tarihi', subtitle: 'Devrimler, İlkeler' },
                ]
            }
        ];

        const getTopicContent = (subjectId, topicId) => {
            const contentMap = {
                'matematik': {
                    1: {
                        title: 'Fonksiyonlar',
                        sections: [
                            {
                                title: '📊 Fonksiyon Tanımı ve Gösterimi',
                                content: 'Bir A kümesinin her elemanını B kümesinin yalnız bir elemanı ile eşleştiren kurala fonksiyon denir.',
                                diagram: `
                                    <div style="display: flex; justify-content: space-around; align-items: center; padding: 20px;">
                                        <div style="background: #667eea; color: white; padding: 20px; border-radius: 50%; width: 100px; height: 100px; display: flex; align-items: center; justify-content: center; font-size: 1.5em;">A Kümesi</div>
                                        <div style="font-size: 3em;">→</div>
                                        <div style="background: #764ba2; color: white; padding: 20px; border-radius: 50%; width: 100px; height: 100px; display: flex; align-items: center; justify-content: center; font-size: 1.5em;">B Kümesi</div>
                                    </div>
                                    <div style="text-align: center; margin-top: 20px; font-size: 1.2em; font-weight: bold;">f: A → B</div>
                                `,
                                formula: 'f(x) = y şeklinde gösterilir',
                                important: 'Her x değeri için sadece bir y değeri olmalıdır!',
                                yks: 'YKS\'de fonksiyon tanımı ve birebir-örten kavramları sıkça sorulur'
                            },
                            {
                                title: '🎯 Fonksiyon Türleri',
                                concepts: ['Birebir Fonksiyon', 'Örten Fonksiyon', 'Birebirörten (Bijektif)', 'Sabit Fonksiyon', 'Birim Fonksiyon'],
                                flowSteps: [
                                    'Her x farklı y\'ye gidiyorsa → BİREBİR',
                                    'Her y değeri kullanılıyorsa → ÖRTEN',
                                    'Hem birebir hem örten → BİJEKTİF',
                                    'f(x) = c (sabit) → SABİT FONKSİYON'
                                ],
                                tip: '💡 Grafik üzerinde yatay doğru testi: Grafiği birden fazla noktada kesiyorsa birebir değildir!',
                                warning: '⚠️ TUZAK: Tanım kümesi ile değer kümesini karıştırmayın!'
                            },
                            {
                                title: '📈 Özel Fonksiyonlar',
                                infoCards: [
                                    { title: 'Doğrusal Fonksiyon', value: 'f(x) = ax + b' },
                                    { title: 'Parabolik Fonksiyon', value: 'f(x) = ax² + bx + c' },
                                    { title: 'Hiperbolik Fonksiyon', value: 'f(x) = a/x' },
                                    { title: 'Üstel Fonksiyon', value: 'f(x) = aˣ' },
                                    { title: 'Logaritmik Fonksiyon', value: 'f(x) = logₐx' },
                                ],
                                memory: '🧠 HAFIZA TEKNİĞİ: "DoParHiÜsLo" → Doğrusal, Parabolik, Hiperbolik, Üstel, Logaritmik'
                            }
                        ]
                    },
                    2: {
                        title: 'Polinomlar',
                        sections: [
                            {
                                title: '🔢 Polinom Tanımı',
                                content: 'P(x) = aₙxⁿ + aₙ₋₁xⁿ⁻¹ + ... + a₁x + a₀ şeklindeki ifadelere polinom denir.',
                                formula: 'P(x) = aₙxⁿ + aₙ₋₁xⁿ⁻¹ + ... + a₁x + a₀',
                                important: 'En büyük üs derecesini belirler. aₙ ≠ 0 olmalıdır!',
                                concepts: ['Derece (n)', 'Katsayılar (aᵢ)', 'Sabit Terim (a₀)', 'Baş Katsayı (aₙ)'],
                                yks: 'Polinom derecesi ve işlemleri her yıl çıkar'
                            },
                            {
                                title: '➕➖ Polinom İşlemleri',
                                flowSteps: [
                                    'Toplama/Çıkarma: Aynı dereceli terimleri topla',
                                    'Çarpma: Her terimi her terimle çarp',
                                    'Bölme: Uzun bölme veya Horner yöntemi',
                                    'Kalan Teoremi: P(x)/(x-a) → Kalan = P(a)'
                                ],
                                tip: '💡 Hızlı çözüm için Horner şeması kullan!',
                                memory: '🧠 Kalan bulmak için: "x yerine kök yaz"'
                            },
                            {
                                title: '🎯 Çarpanlara Ayırma',
                                infoCards: [
                                    { title: 'Ortak Çarpan', value: 'ax + ay = a(x+y)' },
                                    { title: 'İki Kare Farkı', value: 'a² - b² = (a-b)(a+b)' },
                                    { title: 'Tam Kare', value: 'a² ± 2ab + b²' },
                                    { title: 'İki Küp Toplamı', value: 'a³ + b³ = (a+b)(a²-ab+b²)' },
                                ],
                                warning: '⚠️ İki küp farkında işaretlere dikkat! a³ - b³ = (a-b)(a²+ab+b²)'
                            }
                        ]
                    },
                    3: {
                        title: '2. Derece Denklemler',
                        sections: [
                            {
                                title: '📐 Genel Form ve Çözüm',
                                formula: 'ax² + bx + c = 0 (a ≠ 0)',
                                diagram: `
                                    <div style="background: linear-gradient(135deg, #667eea, #764ba2); color: white; padding: 30px; border-radius: 15px; text-align: center;">
                                        <h3 style="margin-bottom: 20px;">Çözüm Formülü</h3>
                                        <div style="font-size: 1.5em; font-weight: bold;">x = (-b ± √Δ) / 2a</div>
                                        <div style="margin-top: 20px; font-size: 1.2em;">Δ = b² - 4ac</div>
                                    </div>
                                `,
                                important: 'Diskriminant (Δ) köklerin durumunu belirler!',
                                yks: 'Diskriminant ve kök bağıntıları %100 çıkar'
                            },
                            {
                                title: '🔍 Diskriminant (Δ) Analizi',
                                flowSteps: [
                                    'Δ > 0 → İki farklı gerçek kök',
                                    'Δ = 0 → İki eşit gerçek kök (çakışık)',
                                    'Δ < 0 → Gerçek kök yok (karmaşık kökler)'
                                ],
                                memory: '🧠 PozİN: Pozitif → İki kök, Negatif → Kök yok',
                                tip: '💡 Δ tam kare ise kökler rasyoneldir!'
                            },
                            {
                                title: '🎯 Kök-Katsayı Bağıntıları',
                                infoCards: [
                                    { title: 'Kökler Toplamı', value: 'x₁ + x₂ = -b/a' },
                                    { title: 'Kökler Çarpımı', value: 'x₁ · x₂ = c/a' },
                                    { title: 'Kareler Toplamı', value: 'x₁² + x₂² = (x₁+x₂)² - 2x₁x₂' },
                                    { title: 'Denklem Yazma', value: 'x² - (x₁+x₂)x + x₁x₂ = 0' },
                                ],
                                warning: '⚠️ TUZAK: Kökler toplamında eksi işareti var!'
                            }
                        ]
                    }
                },
                'fizik': {
                    1: {
                        title: 'Elektrik ve Manyetizma',
                        sections: [
                            {
                                title: '⚡ Elektrik Yükü',
                                content: 'Maddenin temel özelliklerinden biridir. İki tür yük vardır: Pozitif (+) ve Negatif (-)',
                                diagram: `
                                    <div style="display: flex; justify-content: space-around; padding: 20px;">
                                        <div style="background: #f44336; color: white; padding: 30px; border-radius: 50%; font-size: 2em; width: 120px; height: 120px; display: flex; align-items: center; justify-content: center;">
                                            <div>+<br/>Proton</div>
                                        </div>
                                        <div style="background: #2196f3; color: white; padding: 30px; border-radius: 50%; font-size: 2em; width: 120px; height: 120px; display: flex; align-items: center; justify-content: center;">
                                            <div>-<br/>Elektron</div>
                                        </div>
                                    </div>
                                `,
                                important: 'Aynı işaretli yükler itişir, zıt işaretli yükler çekilir',
                                formula: 'e = 1.6 × 10⁻¹⁹ C (Elementer yük)',
                                yks: 'Coulomb yasası ve elektrik alan sorularına çok dikkat!'
                            },
                            {
                                title: '⚡ Coulomb Yasası',
                                formula: 'F = k · |q₁ · q₂| / r²',
                                concepts: ['k = 9×10⁹ N·m²/C² (Coulomb sabiti)', 'q₁, q₂: Yük miktarları', 'r: Yükler arası uzaklık'],
                                flowSteps: [
                                    'Yük miktarları arttıkça kuvvet artar',
                                    'Uzaklık arttıkça kuvvet azalır (ters kare)',
                                    'Yükler arası uzaklık 2 katına çıkarsa, kuvvet 4\'te 1\'e düşer'
                                ],
                                memory: '🧠 "Yük çok, uzak yok!" - Yük artar kuvvet artar, uzaklık artar kuvvet azalır',
                                tip: '💡 r yarıya inerse F 4 katına çıkar!'
                            },
                            {
                                title: '🌐 Elektrik Alan',
                                formula: 'E = F / q = k · Q / r²',
                                diagram: `
                                    <div style="text-align: center; padding: 20px;">
                                        <div style="background: #f093fb; color: white; padding: 20px; border-radius: 15px; display: inline-block; margin-bottom: 20px;">
                                            <div style="font-size: 2em; margin-bottom: 10px;">+Q</div>
                                            <div>Kaynak Yük</div>
                                        </div>
                                        <div style="font-size: 2em; margin: 20px;">↓ Alan Çizgileri ↓</div>
                                        <div style="display: flex; justify-content: center; gap: 20px;">
                                            <div>→</div>
                                            <div>→</div>
                                            <div>→</div>
                                            <div>→</div>
                                            <div>→</div>
                                        </div>
                                    </div>
                                `,
                                important: 'Elektrik alan bir vektör büyüklüktür. Yönü: (+) yükten çıkar, (-) yüke girer',
                                infoCards: [
                                    { title: 'Birim', value: 'N/C veya V/m' },
                                    { title: 'Yön', value: 'Pozitif yükün hissedeceği kuvvet yönü' },
                                    { title: 'Süperpozisyon', value: 'Alanlar vektörel toplanır' },
                                ],
                                warning: '⚠️ Alan çizgileri asla kesişmez!'
                            },
                            {
                                title: '🔋 Elektrik Potansiyel',
                                formula: 'V = k · Q / r',
                                content: 'Bir noktaya birim yükü sonsuzdan getirmek için yapılan iştir.',
                                infoCards: [
                                    { title: 'Birim', value: 'Volt (V)' },
                                    { title: 'Skaler', value: 'Yönü yoktur, cebirsel toplanır' },
                                    { title: 'Referans', value: 'Sonsuz noktada V = 0' },
                                    { title: 'Potansiyel Farkı', value: 'ΔV = V₂ - V₁' },
                                ],
                                memory: '🧠 "Alan VEKTÖR, Potansiyel SKALER" - Yön var/yok',
                                tip: '💡 Eşpotansiyel yüzeyler alan çizgilerine diktir'
                            }
                        ]
                    },
                    2: {
                        title: 'Kuvvet ve Hareket',
                        sections: [
                            {
                                title: '🚀 Newton\'un Hareket Yasaları',
                                flowSteps: [
                                    '1. YASA (Eylemsizlik): Net kuvvet = 0 → Hız sabit kalır',
                                    '2. YASA (F=ma): Net kuvvet → İvme oluşturur',
                                    '3. YASA (Etki-Tepki): Her etkiye eşit ve zıt tepki vardır'
                                ],
                                formula: 'F_net = m · a',
                                important: 'İkinci yasa vektörel! Kuvvetler bileşenlerine ayrılır',
                                memory: '🧠 "Eylem İle Etki-Tepki" → 1.Eylemsizlik, 2.İvme, 3.Etki-Tepki',
                                yks: 'Newton yasaları ve serbest cisim diyagramları mutlaka çıkar'
                            },
                            {
                                title: '⚖️ Sürtünme Kuvveti',
                                diagram: `
                                    <div style="padding: 30px; text-align: center;">
                                        <div style="background: #ff6b6b; color: white; padding: 20px; border-radius: 15px; margin: 20px auto; max-width: 400px;">
                                            <div style="font-size: 1.5em; margin-bottom: 15px;">Statik Sürtünme</div>
                                            <div style="font-size: 1.2em;">f_s ≤ μ_s · N</div>
                                            <div style="margin-top: 10px; font-size: 0.9em;">(Cisim hareket etmeden önceki maksimum)</div>
                                        </div>
                                        <div style="background: #4ecdc4; color: white; padding: 20px; border-radius: 15px; margin: 20px auto; max-width: 400px;">
                                            <div style="font-size: 1.5em; margin-bottom: 15px;">Kinetik Sürtünme</div>
                                            <div style="font-size: 1.2em;">f_k = μ_k · N</div>
                                            <div style="margin-top: 10px; font-size: 0.9em;">(Cisim hareket halindeyken)</div>
                                        </div>
                                    </div>
                                `,
                                important: 'μ_s > μ_k (Statik sürtünme katsayısı her zaman daha büyüktür)',
                                tip: '💡 Sürtünme yüzey alanına bağlı DEĞİLDİR!',
                                warning: '⚠️ TUZAK: Normal kuvvet her zaman ağırlığa eşit değildir!'
                            },
                            {
                                title: '💨 Momentum ve İtme',
                                formula: 'p = m · v (Momentum)',
                                infoCards: [
                                    { title: 'Momentum', value: 'p = m·v (kg·m/s)' },
                                    { title: 'İtme', value: 'I = F·Δt = Δp' },
                                    { title: 'Korunum', value: 'Σp_önce = Σp_sonra' },
                                    { title: 'Çarpışma', value: 'Esnek: KE korunur, Esnek olmayan: KE korunmaz' },
                                ],
                                memory: '🧠 "Momentum VEKTÖRdür" - Yön önemli!',
                                yks: 'Çarpışma ve momentum korunumu kesin çıkar'
                            }
                        ]
                    }
                },
                'kimya': {
                    1: {
                        title: 'Gazlar',
                        sections: [
                            {
                                title: '☁️ Gaz Yasaları',
                                flowSteps: [
                                    'BOYLE YASASI (T sabit): P · V = sabit',
                                    'CHARLES YASASI (P sabit): V / T = sabit',
                                    'GAY-LUSSAC YASASI (V sabit): P / T = sabit',
                                    'BİRLEŞİK GAZ YASASI: (P₁V₁)/T₁ = (P₂V₂)/T₂'
                                ],
                                memory: '🧠 "BoCaGa" → Boyle, Charles, Gay-Lussac',
                                important: 'Sıcaklık mutlaka Kelvin cinsinden olmalı! T(K) = T(°C) + 273',
                                yks: 'Gaz yasaları ve hesaplamaları her yıl çıkar'
                            },
                            {
                                title: '⚗️ İdeal Gaz Denklemi',
                                formula: 'P · V = n · R · T',
                                diagram: `
                                    <div style="background: linear-gradient(135deg, #4facfe, #00f2fe); color: white; padding: 30px; border-radius: 15px; text-align: center;">
                                        <h3 style="margin-bottom: 20px;">İdeal Gaz Denklemi</h3>
                                        <div style="font-size: 2em; font-weight: bold; margin-bottom: 20px;">PV = nRT</div>
                                        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px; text-align: left;">
                                            <div>P = Basınç (atm, Pa)</div>
                                            <div>V = Hacim (L, m³)</div>
                                            <div>n = Mol sayısı (mol)</div>
                                            <div>R = Gaz sabiti</div>
                                            <div style="grid-column: 1/-1; text-align: center; margin-top: 10px;">T = Sıcaklık (K)</div>
                                        </div>
                                    </div>
                                `,
                                infoCards: [
                                    { title: 'R = 0.082 atm·L/(mol·K)', value: 'En çok kullanılan' },
                                    { title: 'R = 8.314 J/(mol·K)', value: 'SI birimi' },
                                    { title: 'Standart Koşullar', value: '0°C, 1 atm → 22.4 L' },
                                ],
                                tip: '💡 Gaz sabiti R\'nin birimlerine göre diğer birimleri ayarla!',
                                warning: '⚠️ Sıcaklık mutlaka Kelvin olmalı!'
                            },
                            {
                                title: '🎈 Dalton\'un Kısmi Basınç Yasası',
                                formula: 'P_toplam = P₁ + P₂ + P₃ + ...',
                                content: 'Bir gaz karışımının toplam basıncı, gazların kısmi basınçları toplamına eşittir.',
                                infoCards: [
                                    { title: 'Kısmi Basınç', value: 'P_i = X_i · P_toplam' },
                                    { title: 'Mol Kesri', value: 'X_i = n_i / n_toplam' },
                                    { title: 'Toplam', value: 'ΣX_i = 1' },
                                ],
                                memory: '🧠 "Her gaz kendi basıncını yapar"'
                            }
                        ]
                    },
                    2: {
                        title: 'Çözeltiler',
                        sections: [
                            {
                                title: '💧 Derişim Birimleri',
                                infoCards: [
                                    { title: 'Molarite (M)', value: 'mol/L' },
                                    { title: 'Molalite (m)', value: 'mol/kg çözücü' },
                                    { title: 'Kütle Yüzdesi', value: '(m_çözünen/m_çözelti)×100' },
                                    { title: 'Hacim Yüzdesi', value: '(V_çözünen/V_çözelti)×100' },
                                    { title: 'ppm', value: 'mg/L veya (m/m)×10⁶' },
                                ],
                                formula: 'M = n / V (Molarite)',
                                memory: '🧠 "MoLar → mol/Litre, MoLal → mol/kiLoğram"',
                                yks: 'Seyreltme hesaplamaları: M₁V₁ = M₂V₂ çok önemli!'
                            },
                            {
                                title: '🌡️ Koligatif Özellikler',
                                flowSteps: [
                                    '1. Buhar Basıncı Düşmesi: ΔP = X_çözünen · P°',
                                    '2. Kaynama Noktası Yükselmesi: ΔT_k = K_k · m',
                                    '3. Donma Noktası Alçalması: ΔT_d = K_d · m',
                                    '4. Ozmotik Basınç: π = M · R · T'
                                ],
                                important: 'Koligatif özellikler sadece partikül sayısına bağlıdır, türüne değil!',
                                tip: '💡 İyonlaşan maddeler (NaCl gibi) daha fazla partikül verir',
                                warning: '⚠️ van\'t Hoff faktörü (i) elektrolitleri hesaba kat!'
                            }
                        ]
                    }
                },
                'biyoloji': {
                    1: {
                        title: 'Sinir Sistemi',
                        sections: [
                            {
                                title: '🧠 Nöron Yapısı',
                                diagram: `
                                    <div style="padding: 30px; background: linear-gradient(135deg, #43e97b, #38f9d7); border-radius: 15px; color: white;">
                                        <div style="text-align: center; margin-bottom: 20px; font-size: 1.5em; font-weight: bold;">NÖRON</div>
                                        <div style="display: flex; justify-content: space-around; align-items: center; flex-wrap: wrap; gap: 20px;">
                                            <div style="background: rgba(255,255,255,0.2); padding: 15px; border-radius: 10px;">
                                                <div style="font-size: 1.2em; margin-bottom: 5px;">Dendrit</div>
                                                <div style="font-size: 0.9em;">Uyarı alır</div>
                                            </div>
                                            <div style="font-size: 2em;">→</div>
                                            <div style="background: rgba(255,255,255,0.2); padding: 15px; border-radius: 10px;">
                                                <div style="font-size: 1.2em; margin-bottom: 5px;">Hücre Gövdesi</div>
                                                <div style="font-size: 0.9em;">İşler</div>
                                            </div>
                                            <div style="font-size: 2em;">→</div>
                                            <div style="background: rgba(255,255,255,0.2); padding: 15px; border-radius: 10px;">
                                                <div style="font-size: 1.2em; margin-bottom: 5px;">Akson</div>
                                                <div style="font-size: 0.9em;">Uyarı iletir</div>
                                            </div>
                                            <div style="font-size: 2em;">→</div>
                                            <div style="background: rgba(255,255,255,0.2); padding: 15px; border-radius: 10px;">
                                                <div style="font-size: 1.2em; margin-bottom: 5px;">Sinaps</div>
                                                <div style="font-size: 0.9em;">Diğer nörona iletir</div>
                                            </div>
                                        </div>
                                    </div>
                                `,
                                memory: '🧠 "DeHücAkSi" → Dendrit, Hücre gövdesi, Akson, Sinaps',
                                important: 'Uyarı tek yönlü: Dendrit → Akson → Sinaps',
                                yks: 'Nöron türleri ve sinir iletimi mutlaka çıkar'
                            },
                            {
                                title: '⚡ Sinir İletimi',
                                flowSteps: [
                                    'DİNLENME POTANSİYELİ: -70mV (dışarı +, içeri -)',
                                    'UYARILMA: Na⁺ içeri girer → Depolarizasyon (+40mV)',
                                    'REPOLARİZASYON: K⁺ dışarı çıkar → Tekrar (-)',
                                    'HİPERPOLARİZASYON: Geçici olarak -70mV\'nin altına düşer',
                                    'POMPA ÇALIŞIR: Na⁺-K⁺ pompası normale döndürür'
                                ],
                                infoCards: [
                                    { title: 'Dinlenme', value: '-70 mV' },
                                    { title: 'Eşik Değer', value: '-55 mV' },
                                    { title: 'Depolarizasyon', value: '+40 mV' },
                                    { title: 'Hız', value: '0.5-120 m/s' },
                                ],
                                tip: '💡 Miyelin kılıf uyarı iletimini hızlandırır (saltatory)',
                                warning: '⚠️ Hepsi ya hiç kanunu: Eşik değer aşılırsa tam uyarı oluşur'
                            },
                            {
                                title: '🔗 Sinaps',
                                content: 'İki nöron arasındaki bağlantı noktasıdır. Kimyasal veya elektriksel olabilir.',
                                diagram: `
                                    <div style="text-align: center; padding: 20px;">
                                        <div style="background: #ff6b6b; color: white; padding: 20px; border-radius: 15px; margin-bottom: 20px; display: inline-block;">
                                            Presinaptik Nöron<br/>(Sinaps öncesi)
                                        </div>
                                        <div style="font-size: 2em; margin: 20px;">↓ Nörotransmitter ↓</div>
                                        <div style="background: #4ecdc4; color: white; padding: 20px; border-radius: 15px; display: inline-block;">
                                            Postsinaptik Nöron<br/>(Sinaps sonrası)
                                        </div>
                                    </div>
                                `,
                                infoCards: [
                                    { title: 'Asetilkolin', value: 'Kas kasılması' },
                                    { title: 'Dopamin', value: 'Hareket, motivasyon' },
                                    { title: 'Serotonin', value: 'Ruh hali, uyku' },
                                    { title: 'GABA', value: 'İnhibitör (engelleyici)' },
                                ],
                                memory: '🧠 "AcDoSeGa" → Asetilkolin, Dopamin, Serotonin, GABA'
                            }
                        ]
                    }
                },
                'edebiyat': {
                    1: {
                        title: 'Tanzimat Dönemi',
                        sections: [
                            {
                                title: '📅 Tarihsel Bağlam',
                                content: '1839 Tanzimat Fermanı ile başlar, 1876\'ya kadar sürer.',
                                diagram: `
                                    <div style="background: linear-gradient(135deg, #fa709a, #fee140); padding: 30px; border-radius: 15px;">
                                        <div style="text-align: center; font-size: 1.8em; font-weight: bold; margin-bottom: 30px; color: white;">TANZİMAT DÖNEMİ ZAMAN ÇİZGİSİ</div>
                                        <div style="display: flex; justify-content: space-between; align-items: center; background: white; padding: 20px; border-radius: 10px;">
                                            <div style="text-align: center;">
                                                <div style="font-size: 1.5em; font-weight: bold; color: #fa709a;">1839</div>
                                                <div style="margin-top: 10px;">Tanzimat Fermanı</div>
                                            </div>
                                            <div style="font-size: 2em; color: #fa709a;">→</div>
                                            <div style="text-align: center;">
                                                <div style="font-size: 1.5em; font-weight: bold; color: #fa709a;">1860</div>
                                                <div style="margin-top: 10px;">Birinci Dönem</div>
                                            </div>
                                            <div style="font-size: 2em; color: #fa709a;">→</div>
                                            <div style="text-align: center;">
                                                <div style="font-size: 1.5em; font-weight: bold; color: #fa709a;">1876</div>
                                                <div style="margin-top: 10px;">İkinci Dönem</div>
                                            </div>
                                        </div>
                                    </div>
                                `,
                                important: 'Batılılaşma hareketi edebiyata yansır',
                                yks: 'Dönem özellikleri ve temsilciler sık sorulur'
                            },
                            {
                                title: '✍️ Önemli Yazarlar ve Eserleri',
                                infoCards: [
                                    { title: 'Şinasi', value: 'Şair Evlenmesi (İlk yerli oyun)' },
                                    { title: 'Namık Kemal', value: 'Vatan yahut Silistre' },
                                    { title: 'Ziya Paşa', value: 'Harabat, Terkib-i Bend' },
                                    { title: 'Ahmet Mithat Efendi', value: 'Felâtun Bey ile Rakım Efendi' },
                                    { title: 'Recaizade M. Ekrem', value: 'Araba Sevdası' },
                                    { title: 'Abdülhak Hamit', value: 'Makber' },
                                ],
                                memory: '🧠 "ŞiNaZiAhReAb" → Şinasi, Namık Kemal, Ziya Paşa, Ahmet Mithat, Recaizade, Abdülhak Hamit',
                                tip: '💡 Namık Kemal = Vatan şairi, hürriyet savunucusu'
                            },
                            {
                                title: '🎯 Dönem Özellikleri',
                                flowSteps: [
                                    'Batı edebiyatından etkilenme (Fransız edebiyatı)',
                                    'Yeni türler: Roman, hikâye, tiyatro',
                                    'Dil sadeleşme çabaları',
                                    'Didaktik (öğretici) yaklaşım',
                                    'Toplumsal sorunlara eğilme',
                                    'Vatan, hürriyet, vatan sevgisi temaları'
                                ],
                                warning: '⚠️ Henüz tam bir sanat anlayışı yok, fayda ön planda'
                            }
                        ]
                    }
                },
                'cografya': {
                    1: {
                        title: 'Türkiye\'nin Fiziki Coğrafyası',
                        sections: [
                            {
                                title: '🏔️ Yer Şekilleri',
                                diagram: `
                                    <div style="background: linear-gradient(135deg, #ffecd2, #fcb69f); padding: 30px; border-radius: 15px;">
                                        <div style="text-align: center; font-size: 1.8em; font-weight: bold; margin-bottom: 20px;">TÜRKİYE\'NİN YER ŞEKİLLERİ</div>
                                        <div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 20px;">
                                            <div style="background: white; padding: 20px; border-radius: 10px; text-align: center;">
                                                <div style="font-size: 3em;">🗻</div>
                                                <div style="font-weight: bold; margin: 10px 0;">DAĞLAR</div>
                                                <div>Kuzey Anadolu, Toros</div>
                                            </div>
                                            <div style="background: white; padding: 20px; border-radius: 10px; text-align: center;">
                                                <div style="font-size: 3em;">🏔️</div>
                                                <div style="font-weight: bold; margin: 10px 0;">YAYLALAR</div>
                                                <div>İç Anadolu, Doğu Anadolu</div>
                                            </div>
                                            <div style="background: white; padding: 20px; border-radius: 10px; text-align: center;">
                                                <div style="font-size: 3em;">🏖️</div>
                                                <div style="font-weight: bold; margin: 10px 0;">KIYILAR</div>
                                                <div>Ege, Akdeniz, Karadeniz</div>
                                            </div>
                                        </div>
                                    </div>
                                `,
                                infoCards: [
                                    { title: 'En Yüksek Dağ', value: 'Ağrı Dağı (5137m)' },
                                    { title: 'En Büyük Göl', value: 'Van Gölü' },
                                    { title: 'En Uzun Nehir', value: 'Kızılırmak (1355km)' },
                                    { title: 'Ortalama Yükseklik', value: '1132 m' },
                                ],
                                memory: '🧠 "AğVaKı" → Ağrı (dağ), Van (göl), Kızılırmak (nehir)',
                                yks: 'Yer şekilleri ve özellikleri sık çıkar'
                            },
                            {
                                title: '🌦️ İklim Özellikleri',
                                flowSteps: [
                                    'KARADENİZ: Yağışlı, ılıman, her mevsim yağış',
                                    'AKDENİZ: Yazı sıcak-kurak, kışı ılık-yağışlı',
                                    'EGE: Akdeniz benzeri, geçiş iklimi',
                                    'MARMARA: Geçiş iklimi, 4 mevsim belirgin',
                                    'İÇ ANADOLU: Karasal, sıcaklık farkı fazla',
                                    'DOĞU ANADOLU: Soğuk, kar yağışlı',
                                    'GÜNEYDOĞU: Sıcak, kurak'
                                ],
                                tip: '💡 Yükselti arttıkça sıcaklık azalır (100m → 0.5-1°C)',
                                important: 'Dağlar yağış engeli oluşturur (yağış gölgesi)'
                            }
                        ]
                    }
                },
                'tarih': {
                    1: {
                        title: 'Osmanlı\'nın Duraklama Dönemi',
                        sections: [
                            {
                                title: '📅 Kronoloji',
                                diagram: `
                                    <div style="background: linear-gradient(135deg, #ff9a56, #ff6a88); padding: 30px; border-radius: 15px; color: white;">
                                        <div style="text-align: center; font-size: 1.8em; font-weight: bold; margin-bottom: 30px;">DURAKLAMA DÖNEMİ (1579-1699)</div>
                                        <div style="background: white; color: #333; padding: 20px; border-radius: 10px;">
                                            <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px;">
                                                <div style="font-size: 1.3em; font-weight: bold;">1579</div>
                                                <div>→</div>
                                                <div>Başlangıç (II. Selim)</div>
                                            </div>
                                            <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px;">
                                                <div style="font-size: 1.3em; font-weight: bold;">1683</div>
                                                <div>→</div>
                                                <div>II. Viyana Kuşatması (Yenilgi)</div>
                                            </div>
                                            <div style="display: flex; justify-content: space-between; align-items: center;">
                                                <div style="font-size: 1.3em; font-weight: bold;">1699</div>
                                                <div>→</div>
                                                <div>Karlofça Antlaşması</div>
                                            </div>
                                        </div>
                                    </div>
                                `,
                                important: 'İlk kez toprak kaybedilen antlaşma: Karlofça (1699)',
                                yks: 'Antlaşmalar ve sonuçları kesin çıkar'
                            },
                            {
                                title: '⚠️ Duraklama Sebepleri',
                                flowSteps: [
                                    'COĞRAFÎ: Sınırlara ulaşıldı, genişleme durdu',
                                    'EKONOMİK: Yeni ticaret yolları, altın-gümüş akışı',
                                    'ASKERÎ: Savaş gelir-gider dengesi bozuldu',
                                    'İDARÎ: Kapıkulu ocakları bozuldu, rüşvet arttı',
                                    'SOSYAL: Celâli İsyanları, huzursuzluk',
                                    'BİLİMSEL: Avrupa\'da bilimsel devrim, Osmanlı geri kaldı'
                                ],
                                memory: '🧠 "CoEkAsİdSoBi" → Coğrafi, Ekonomik, Askerî, İdari, Sosyal, Bilimsel',
                                warning: '⚠️ Çok yönlü sebepleri karıştırmayın!'
                            },
                            {
                                title: '📜 Önemli Antlaşmalar',
                                infoCards: [
                                    { title: 'Karlofça (1699)', value: 'İlk toprak kaybı' },
                                    { title: 'Pasarofça (1718)', value: 'Daha fazla kayıp' },
                                    { title: 'İstanbul (1700)', value: 'Rusya ile' },
                                    { title: 'Prut (1711)', value: 'Osmanlı lehine' },
                                ],
                                tip: '💡 Antlaşma adları genelde yapıldıkları şehirdir'
                            }
                        ]
                    }
                }
            };

            return contentMap[subjectId]?.[topicId] || {
                title: 'İçerik Hazırlanıyor',
                sections: [
                    {
                        title: '🚧 Bu konu için detaylı içerik hazırlanıyor',
                        content: 'Çok yakında eklenecek!',
                        important: 'Diğer konuları inceleyebilirsiniz'
                    }
                ]
            };
        };

        function App() {
            const [darkMode, setDarkMode] = useState(false);
            const [selectedSubject, setSelectedSubject] = useState(null);
            const [selectedTopic, setSelectedTopic] = useState(null);

            useEffect(() => {
                if (darkMode) {
                    document.body.classList.add('dark-mode');
                } else {
                    document.body.classList.remove('dark-mode');
                }
            }, [darkMode]);

            const renderSubjects = () => (
                <>
                    <div className="header">
                        <h1>🎓 Fen Lisesi 11. Sınıf</h1>
                        <p>Görsel Eğitim Uygulaması - YKS Hazırlık</p>
                    </div>
                    <div className="subjects-grid">
                        {subjects.map(subject => (
                            <div
                                key={subject.id}
                                className="subject-card"
                                style={{'--color1': subject.color1, '--color2': subject.color2}}
                                onClick={() => setSelectedSubject(subject)}
                            >
                                <div className="subject-icon">{subject.icon}</div>
                                <div className="subject-title">{subject.name}</div>
                                <div className="subject-description">{subject.description}</div>
                            </div>
                        ))}
                    </div>
                </>
            );

            const renderTopics = () => {
                const subject = selectedSubject;
                return (
                    <div className="content-view">
                        <button className="back-button" onClick={() => setSelectedSubject(null)}>
                            ← Ana Menü
                        </button>
                        <h2 style={{color: subject.color1, marginBottom: '20px', fontSize: '2em'}}>
                            {subject.icon} {subject.name}
                        </h2>
                        <div className="topics-list">
                            {subject.topics.map(topic => (
                                <div
                                    key={topic.id}
                                    className="topic-card"
                                    style={{'--color1': subject.color1}}
                                    onClick={() => setSelectedTopic(topic)}
                                >
                                    <div className="topic-title">{topic.title}</div>
                                    <div className="topic-subtitle">{topic.subtitle}</div>
                                    <span className="yks-badge">YKS İÇİN ÖNEMLİ</span>
                                </div>
                            ))}
                        </div>
                    </div>
                );
            };

            const renderTopicContent = () => {
                const subject = selectedSubject;
                const topic = selectedTopic;
                const content = getTopicContent(subject.id, topic.id);

                return (
                    <div className="content-view">
                        <button className="back-button" onClick={() => setSelectedTopic(null)}>
                            ← Konulara Dön
                        </button>
                        <h2 style={{color: subject.color1, marginBottom: '10px', fontSize: '2em'}}>
                            {content.title}
                        </h2>
                        <p style={{color: '#666', marginBottom: '30px', fontSize: '1.1em'}}>
                            {topic.subtitle}
                        </p>

                        {content.sections.map((section, idx) => (
                            <div key={idx} className="visual-content" style={{'--color1': subject.color1, '--color2': subject.color2}}>
                                <div className="visual-section">
                                    <h3>{section.title}</h3>
                                    
                                    {section.content && (
                                        <p style={{fontSize: '1.1em', lineHeight: '1.8', marginBottom: '20px'}}>
                                            {section.content}
                                        </p>
                                    )}

                                    {section.diagram && (
                                        <div className="diagram" dangerouslySetInnerHTML={{__html: section.diagram}} />
                                    )}

                                    {section.formula && (
                                        <div className="formula-box">
                                            <strong>📐 Formül:</strong> {section.formula}
                                        </div>
                                    )}

                                    {section.important && (
                                        <div className="important-box">
                                            <strong>⭐ ÖNEMLİ:</strong> {section.important}
                                        </div>
                                    )}

                                    {section.tip && (
                                        <div className="tip-box">
                                            <strong>💡 PÜF NOKTASI:</strong> {section.tip}
                                        </div>
                                    )}

                                    {section.warning && (
                                        <div className="warning-box">
                                            <strong>⚠️ DİKKAT TUZAK:</strong> {section.warning}
                                        </div>
                                    )}

                                    {section.yks && (
                                        <div className="important-box" style={{background: '#fff3cd', borderLeftColor: '#ff6b6b'}}>
                                            <strong>🎯 YKS NOTU:</strong> {section.yks}
                                        </div>
                                    )}

                                    {section.memory && (
                                        <div className="memory-technique">
                                            {section.memory}
                                        </div>
                                    )}

                                    {section.concepts && (
                                        <div className="concept-map">
                                            {section.concepts.map((concept, i) => (
                                                <div key={i} className="concept-node">{concept}</div>
                                            ))}
                                        </div>
                                    )}

                                    {section.flowSteps && (
                                        <div className="flow-chart">
                                            {section.flowSteps.map((step, i) => (
                                                <div key={i} className="flow-step">{step}</div>
                                            ))}
                                        </div>
                                    )}

                                    {section.infoCards && (
                                        <div className="info-grid">
                                            {section.infoCards.map((card, i) => (
                                                <div key={i} className="info-card">
                                                    <h4>{card.title}</h4>
                                                    <p>{card.value}</p>
                                                </div>
                                            ))}
                                        </div>
                                    )}
                                </div>
                            </div>
                        ))}
                    </div>
                );
            };

            return (
                <div className="app">
                    <button className="dark-toggle" onClick={() => setDarkMode(!darkMode)}>
                        {darkMode ? '☀️ Aydınlık' : '🌙 Karanlık'}
                    </button>
                    
                    {!selectedSubject && renderSubjects()}
                    {selectedSubject && !selectedTopic && renderTopics()}
                    {selectedSubject && selectedTopic && renderTopicContent()}
                </div>
            );
        }

        ReactDOM.render(<App />, document.getElementById('root'));
    </script>
</body>
</html>