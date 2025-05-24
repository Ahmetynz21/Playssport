<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Play TV Maç Yayınları</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-color: #FF5E14;
            --secondary-color: #FF8C42;
            --accent-color: #FF3D00;
            --dark-color: #121212;
            --light-color: #FFFFFF;
            --success-color: #00E676;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            transition: all 0.3s ease;
        }
        
        body {
            font-family: 'Poppins', sans-serif;
            background: var(--dark-color);
            color: var(--light-color);
            min-height: 100vh;
            overflow-x: hidden;
        }
        
        .container {
            display: flex;
            min-height: 100vh;
            position: relative;
            flex-direction: column;
        }

        .main-content {
            flex: 1;
            padding: 80px 20px 20px;
            display: flex;
            justify-content: center;
            margin-right: 0;
            margin-left: 0;
        }

        .player-container {
            width: 100%;
            max-width: 850px;
            margin: 0 auto;
        }
        
        .player-wrapper {
            position: relative;
            padding-bottom: 56.25%;
            height: 0;
            overflow: hidden;
            background: #000;
            border-radius: 8px;
            box-shadow: 0 8px 20px rgba(0,0,0,0.3);
        }
        
        .player-wrapper iframe {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            border: none;
            border-radius: 8px;
        }
        
        .player-info {
            padding: 1rem;
            background: rgba(30,30,30,0.9);
            border-radius: 0 0 8px 8px;
            margin-top: -8px;
        }
        
        /* KANAL LİSTESİ */
        .channel-list-container {
            position: fixed;
            top: 0;
            right: -350px;
            width: 350px;
            height: 90vh;
            background: rgba(30,30,30,0.95);
            backdrop-filter: blur(10px);
            box-shadow: -5px 0 15px rgba(0, 0, 0, 0.2);
            display: flex;
            flex-direction: column;
            z-index: 99;
            overflow-y: auto;
            transition: right 0.3s ease;
        }
        
        .channel-list-container.active {
            right: 0;
        }
        
        .channel-list-header {
            padding: 1.2rem;
            background: linear-gradient(90deg, #FF5E14 0%, #FF3D00 100%);
            color: white;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 0;
            z-index: 10;
        }
        
        .channel-list-header h3 {
            font-size: 1.5rem;
            font-weight: 600;
            margin: 0;
            text-shadow: 1px 1px 3px rgba(0,0,0,0.2);
        }
        
        .channel-list {
            flex: 1;
            overflow-y: auto;
            padding: 0.8rem;
        }
        
        .channel-item {
            background: rgba(255,255,255,0.05);
            border-radius: 8px;
            padding: 0.8rem;
            margin-bottom: 0.8rem;
            cursor: pointer;
            border-left: 4px solid var(--accent-color);
            transition: all 0.2s ease;
        }
        
        .channel-item:hover {
            background: rgba(255,255,255,0.1);
            transform: translateX(5px);
        }
        
        .channel-item.active {
            background: rgba(255,94,20,0.2);
            border-left: 4px solid var(--primary-color);
        }
        
        .channel-time {
            font-size: 0.85rem;
            color: var(--success-color);
            margin-bottom: 0.3rem;
            font-weight: 500;
        }
        
        .channel-teams {
            font-weight: 600;
            margin-bottom: 0.3rem;
            font-size: 1.05rem;
        }
        
        .channel-league {
            font-size: 0.8rem;
            color: rgba(255,255,255,0.7);
            font-weight: 400;
        }
        
        .search-box {
            padding: 1rem;
            background: rgba(40,40,40,0.9);
            position: sticky;
            top: 70px;
            z-index: 10;
        }
        
        .search-input {
            width: 100%;
            padding: 0.7rem 1.2rem;
            border-radius: 50px;
            border: none;
            background: rgba(255,255,255,0.1);
            color: white;
            outline: none;
            font-size: 0.95rem;
        }
        
        .header {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            padding: 1rem 1.5rem;
            background: linear-gradient(90deg, #FF5E14 0%, #000033 100%);
            box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
            display: flex;
            justify-content: space-between;
            align-items: center;
            z-index: 100;
            height: 70px;
        }
        
        .logo {
            font-size: 1.8rem;
            font-weight: 700;
            color: var(--light-color);
            text-decoration: none;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            text-shadow: 1px 1px 3px rgba(0,0,0,0.2);
        }
        
        .toggle-channel-list {
            display: flex;
            background: rgba(255,94,20,0.9);
            color: white;
            border: none;
            padding: 0.7rem 1.2rem;
            border-radius: 50px;
            cursor: pointer;
            font-weight: 600;
            z-index: 1000;
            font-size: 0.95rem;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
            min-width: 110px;
            text-align: center;
            justify-content: center;
            align-items: center;
            height: 40px;
            transition: all 0.2s ease;
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255,255,255,0.1);
        }
        
        .toggle-channel-list:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0,0,0,0.4);
        }
        
        .footer {
            padding: 1rem;
            text-align: center;
            background: rgba(30,30,30,0.9);
            font-size: 0.8rem;
            color: rgba(255,255,255,0.6);
        }
        
        .overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 98;
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s ease;
        }
        
        .overlay.active {
            opacity: 1;
            visibility: visible;
        }
        
        /* MOBİL DÜZEN */
        @media (max-width: 768px) {
            .main-content {
                padding: 70px 0 0;
                width: 100%;
                display: block;
            }
            
            .player-container {
                max-width: 100%;
                border-radius: 0;
                padding: 0;
                margin: 0;
            }
            
            .player-wrapper {
                position: fixed;
                top: 70px;
                left: 0;
                width: 100%;
                height: calc(100vh - 140px);
                padding-bottom: 0;
                z-index: 90;
                border-radius: 0;
            }
            
            .player-wrapper iframe {
                border-radius: 0;
            }
            
            .player-info {
                position: fixed;
                bottom: 0;
                left: 0;
                width: 100%;
                padding: 0.8rem;
                z-index: 95;
                background: rgba(30,30,30,0.95);
                border-radius: 0;
            }
            
            .header {
                padding: 0.8rem 1rem;
                height: 70px;
                justify-content: flex-end;
            }
            
            .logo {
                display: none;
            }
            
            .channel-list-container {
                right: -100%;
                width: 90%;
                z-index: 1000;
            }
            
            .channel-list-container.active {
                right: 0;
            }
            
            .toggle-channel-list {
                position: fixed;
                top: 1rem;
                right: 1rem;
            }
            
            .channel-list-header {
                padding-top: 1.5rem;
            }
            
            .footer {
                padding: 0.8rem;
                position: fixed;
                bottom: 0;
                width: 100%;
                z-index: 110;
            }
            
            .channel-item {
                padding: 0.7rem;
                margin-bottom: 0.6rem;
            }
            
            .channel-teams {
                font-size: 1rem;
            }
        }

        /* Çok küçük ekranlar */
        @media (max-width: 480px) {
            .toggle-channel-list {
                top: 0.8rem;
                right: 0.8rem;
                padding: 0.6rem 1rem;
                font-size: 0.85rem;
                min-width: 100px;
                height: 36px;
            }
            
            .player-wrapper {
                height: calc(100vh - 130px);
            }
        }
        
        /* Animasyonlar */
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        .fade-in {
            animation: fadeIn 0.5s ease forwards;
        }
        
        /* Scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
        }
        
        ::-webkit-scrollbar-track {
            background: rgba(255,255,255,0.05);
            border-radius: 10px;
        }
        
        ::-webkit-scrollbar-thumb {
            background: var(--primary-color);
            border-radius: 10px;
        }

        #infoText {
            margin-bottom: 20px;
            padding: 10px;
            background: rgba(255, 94, 20, 0.2);
            border-radius: 8px;
            text-align: center;
        }
    </style>
</head>
<body>
    <div class="container">
        <header class="header">
            <a href="#" class="logo">
                <span class="logo-icon">▶️</span>
                <span>S Sports Plus</span>
            </a>
            <button class="toggle-channel-list" id="toggleButton">
                <span id="toggleButtonText">Kanal Listesi</span>
            </button>
        </header>
        
        <div class="main-content">
            <div class="player-container fade-in">
                <div class="player-wrapper">
                    <iframe id="player" src="https://sakatv.serv00.net/m3u/player.html?link=https://test.dreamboxserver.net/ssportplus/tracks-v1a1/mono.m3u8" allowfullscreen></iframe>
                </div>
                <div class="player-info">
                    <div id="infoText">Bein Sports 1 aktif</div>
                </div>
            </div>
        </div>

        <div class="channel-list-container" id="channelListContainer">
            <div class="channel-list-header">
                <h3>Kanal Listesi</h3>
                <button class="close-button" id="closeButton">×</button>
            </div>
            <div class="search-box">
                <input type="text" class="search-input" placeholder="Kanal ara...">
            </div>
            <div class="channel-list" id="sideChannelList">
                <!-- Kanal listesi buraya eklenecek -->
            </div>
        </div>

        <div class="overlay" id="overlay"></div>

        <footer class="footer">
            © 2025 Play Sports TV - Tüm hakları saklıdır.
        </footer>
    </div>

    <script>
        // Kanalların sabit olarak girildiği M3U verisi
        const channelsData = [
            {
                name: "S SPORTS 1",
                url: "https://217.30.11.74/e/3030.m3u8",
                logo: "https://sakatv.serv00.net/Arxafonsekiller/ssport.jpg"
            },
            {
                name: "S SPORTS 2",
                url: "https://koprulu3.global.ssl.fastly.net/yt.m3u8/?id=HWPlCP9k3ho",
                logo: "https://sakatv.serv00.net/Arxafonsekiller/ssport.jpg"
            },
            {
                name: "S SPORTS PLUS 1",
                url: "https://test.dreamboxserver.net/ssportplus/tracks-v1a1/mono.m3u8",
                logo: "https://sakatv.serv00.net/Arxafonsekiller/ssport.jpg"
            },
            {
                name: "S SPORTS PLUS 2",
                url: "https://test.dreamboxserver.net/ssportplus2/tracks-v1a1/mono.m3u8",
                logo: "https://sakatv.serv00.net/Arxafonsekiller/ssport.jpg"
            },
            {
                name: "S SPORTS PLUS 3",
                url: "https://test.dreamboxserver.net/ssportplus3/tracks-v1a1/mono.m3u8",
                logo: "https://sakatv.serv00.net/Arxafonsekiller/ssport.jpg"
            },
            
            
             {
                name: "S SPORTS PLUS 4",
                url: "https://test.dreamboxserver.net/ssportplus4/tracks-v1a1/mono.m3u8",
                logo: "https://sakatv.serv00.net/Arxafonsekiller/ssport.jpg"
            },
            
            
            
             {
                name: "S SPORTS PLUS 5",
                url: "https://test.dreamboxserver.net/ssportplus5/tracks-v1a1/mono.m3u8",
                logo: "https://sakatv.serv00.net/Arxafonsekiller/ssport.jpg"
            },
            
            
             {
                name: "S SPORTS PLUS 6",
                url: "https://test.dreamboxserver.net/ssportplus6/tracks-v1a1/mono.m3u8",
                logo: "https://sakatv.serv00.net/Arxafonsekiller/ssport.jpg"
            },
            
            
            
            
        ];

        const sideChannelList = document.getElementById("sideChannelList");
        const infoText = document.getElementById("infoText");
        const toggleButton = document.getElementById("toggleButton");
        const channelListContainer = document.getElementById("channelListContainer");
        const overlay = document.getElementById("overlay");
        const closeButton = document.getElementById("closeButton");
        const searchInput = document.querySelector(".search-input");

        // Kanal listesi aç/kapa
        toggleButton.addEventListener("click", () => {
            channelListContainer.classList.toggle("active");
            overlay.classList.toggle("active");
        });

        closeButton.addEventListener("click", () => {
            channelListContainer.classList.remove("active");
            overlay.classList.remove("active");
        });

        overlay.addEventListener("click", () => {
            channelListContainer.classList.remove("active");
            overlay.classList.remove("active");
        });

        // Arama fonksiyonu
        searchInput.addEventListener("input", (e) => {
            const searchTerm = e.target.value.toLowerCase();
            const channelItems = document.querySelectorAll(".channel-item");
            
            channelItems.forEach(item => {
                const channelName = item.querySelector(".channel-teams").textContent.toLowerCase();
                if (channelName.includes(searchTerm)) {
                    item.style.display = "block";
                } else {
                    item.style.display = "none";
                }
            });
        });

        function displayChannels() {
            sideChannelList.innerHTML = "";
            
            channelsData.forEach(channel => {
                // Yan kanal listesi
                const sideDiv = document.createElement("div");
                sideDiv.className = "channel-item";
                sideDiv.innerHTML = `
                    <div class="channel-teams">${channel.name}</div>
                `;
                sideDiv.onclick = () => {
                    playChannel(channel.url, channel.name);
                    channelListContainer.classList.remove("active");
                    overlay.classList.remove("active");
                };
                sideChannelList.appendChild(sideDiv);
            });
        }

        // Videoyu oynatacak fonksiyon
        function playChannel(url, name) {
            const playerIframe = document.getElementById("player");
            playerIframe.src = `https://sakatv.serv00.net/m3u/player.html?link=${encodeURIComponent(url)}`;
            infoText.textContent = `${name} aktif`;
        }

        // Sayfa yüklendikten sonra kanalları yükle
        window.onload = function() {
            displayChannels();
            // Varsayılan olarak ilk kanalı oynat
            if (channelsData.length > 0) {
                playChannel(channelsData[0].url, channelsData[0].name);
            }
        };
    </script>
</body>
</html>
