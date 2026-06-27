<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <title>Programmed Love with Music</title>
    <style>
        body {
            margin: 0;
            background-color: black;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            overflow: hidden;
            color: #ff69b4;
            font-family: Arial, sans-serif;
        }

        .container {
            position: relative;
        }

        .text {
            position: absolute;
            white-space: nowrap;
            font-size: 14px;
            font-weight: bold;
            animation: blink 2s infinite ease-in-out;
        }

        @keyframes blink {
            0%, 100% { opacity: 0.2; }
            50% { opacity: 1; }
        }

        /* Pengaturan tombol audio agar terlihat jelas */
        .audio-controls {
            position: absolute;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 10;
            background: rgba(255,255,255,0.15);
            padding: 8px 12px;
            border-radius: 25px;
            backdrop-filter: blur(4px);
        }

        audio {
            width: 240px;
        }
    </style>
</head>
<body>

    <div class="container" id="heart-container"></div>

    <!-- ✅ AUDIO DIOPTIMALKAN UNTUK CHROME & SUARA JELAS -->
    <div class="audio-controls">
        <audio 
            id="background-music" 
            controls 
            loop 
            preload="auto"
            volume="1.0"
        >
            <source src="https://media1.vocaroo.com/mp3/1jMux2xuOGIR" type="audio/mpeg">
            Browser Anda tidak mendukung pemutaran audio.
        
    </div>

    <script>
        const container = document.getElementById('heart-container');
        const text = "I love you ";
        
        // Membentuk pola jantung dari teks
        for (let i = 0; i < 70; i++) {
            const span = document.createElement('span');
            span.className = 'text';
            span.innerText = text;
            
            const t = (i / 70) * Math.PI * 2;
            const x = 16 * Math.pow(Math.sin(t), 3);
            const y = -(13 * Math.cos(t) - 5 * Math.cos(2 * t) - 2 * Math.cos(3 * t) - Math.cos(4 * t));
            
            span.style.left = `${x * 15}px`;
            span.style.top = `${y * 15}px`;
            span.style.animationDelay = `${(i * 0.05)}s`;
            
            container.appendChild(span);
        }

        // ✅ MENAMBAH PERINTAH AGAR CHROME MENGENALI DAN MEMUAT MUSIK DENGAN BAIK
        const audio = document.getElementById('background-music');
        
        // Memuat berkas lebih awal agar tidak tersendat
        audio.load();

        // Mengatasi aturan Chrome: pemutaran hanya setelah ada interaksi pengguna
        document.addEventListener('click', function mulaiAudio() {
            audio.play().catch(err => console.log("Siap diputar lewat tombol kontrol", err));
            document.removeEventListener('click', mulaiAudio);
        });
    </script>
</body>
</html>
