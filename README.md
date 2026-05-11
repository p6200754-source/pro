<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Dream Portfolio | Blue Hour</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* 1. 引入复古打字机字体 */
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;700&family=Special+Elite&family=Courier+Prime:wght@400;700&display=swap');

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        /* 全局梦幻基础样式 - 保持原型 */
        body {
            font-family: 'Inter', sans-serif;
            background: linear-gradient(45deg, #0c1427, #102040, #1e3a8a, #0c1427);
            background-size: 400% 400%;
            animation: gradientShift 15s ease infinite;
            color: #e0e7ff;
            overflow: hidden; 
            filter: blur(0.2px) brightness(1.05) saturate(1.1);
            opacity: 0;
            transition: opacity 1.5s ease-in-out;
            position: relative;
        }

        @keyframes gradientShift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        body.loaded { opacity: 1; }

        body::after {
            content: '';
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noiseFilter'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.65' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noiseFilter)'/%3E%3C/svg%3E");
            opacity: 0.06;
            pointer-events: none;
            z-index: 999;
        }

        .mouse-glow {
            position: fixed;
            width: 300px;
            height: 300px;
            background: radial-gradient(circle, rgba(96, 165, 250, 0.18) 0%, transparent 70%);
            border-radius: 50%;
            pointer-events: none;
            z-index: 1;
            transform: translate(-50%, -50%);
            transition: transform 0.1s ease;
        }

        .stars {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            pointer-events: none; z-index: 0;
        }
        .star {
            position: absolute;
            background: white;
            border-radius: 50%;
            animation: twinkle 3s infinite alternate;
        }
        @keyframes twinkle {
            0% { opacity: 0.2; transform: scale(0.8); }
            100% { opacity: 1; transform: scale(1); }
        }

        .main-container {
            display: flex;
            height: 100vh;
            position: relative;
            z-index: 2;
        }

        /* --- 左侧面板保持原型 --- */
        .left-panel {
            width: 40%;
            background-color: rgba(15, 23, 42, 0.7);
            position: relative;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 2rem;
            backdrop-filter: blur(8px);
        }

        .window {
            width: 100%;
            height: 80vh;
            background-color: rgba(15, 23, 42, 0.85);
            border: 12px solid rgba(59, 130, 246, 0.4);
            border-radius: 8px;
            display: flex;
            flex-direction: column;
            gap: 8px;
            position: relative;
            box-shadow: 0 0 50px rgba(59, 130, 246, 0.35), 0 0 100px rgba(37, 99, 235, 0.2);
        }

        .window-top { height: 60px; background-color: rgba(17, 24, 39, 0.75); border-radius: 4px; overflow: hidden; position: relative; }
        .window-bottom { flex: 1; background-color: rgba(17, 24, 39, 0.75); border-radius: 4px; overflow: hidden; position: relative; }

        .window-glass {
            width: 100%; height: 100%;
            background: linear-gradient(to bottom, #3b82f6 0%, #60a5fa 30%, #93c5fd 60%, #0c1427 100%);
            opacity: 0.85; position: relative; overflow: hidden;
        }

        .light-stream {
            position: absolute; width: 150%; height: 3px;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.5), transparent);
            animation: stream 8s infinite linear;
        }
        @keyframes stream {
            0% { transform: translateX(-100%) translateY(0); }
            100% { transform: translateX(100%) translateY(0); }
        }

        .light-reflect { position: absolute; background: rgba(147, 197, 253, 0.75); filter: blur(3px); border-radius: 4px; }
        .reflect-1 { top: 20%; left: 5%; width: 120px; height: 4px; }
        .reflect-2 { top: 30%; right: 15%; width: 180px; height: 4px; }
        .reflect-3 { top: 40%; right: 5%; width: 100px; height: 3px; }

        .cloud { position: absolute; border-radius: 50%; filter: blur(15px); animation: floatDream 30s infinite linear alternate; }
        .cloud-1 { top: 25%; left: 10%; width: 180px; height: 70px; background: rgba(147, 197, 253, 0.25); }
        .cloud-2 { top: 45%; left: 40%; width: 220px; height: 90px; background: rgba(129, 187, 246, 0.25); animation-delay: -5s; }
        .cloud-3 { top: 35%; right: 15%; width: 160px; height: 60px; background: rgba(191, 219, 254, 0.2); animation-delay: -10s; }

        @keyframes floatDream {
            0% { transform: translate(0, 0) scale(1); opacity: 0.7; }
            100% { transform: translate(40px, -20px) scale(1.1); opacity: 1; }
        }

        .moon {
            position: absolute; top: 12%; right: 25%; width: 45px; height: 45px;
            background: #f8fafc; border-radius: 50%;
            box-shadow: 0 0 40px rgba(147, 197, 253, 0.8), 0 0 80px rgba(59, 130, 246, 0.5);
            animation: moonBreath 5s infinite alternate ease-in-out;
        }
        @keyframes moonBreath {
            0% { transform: scale(1); }
            100% { transform: scale(1.05); }
        }

        .text-overlay { position: absolute; bottom: 15%; left: 10%; z-index: 10; }
        .work-title {
            font-size: clamp(3rem, 8vw, 5rem); font-weight: 700;
            background: linear-gradient(90deg, #c7d2fe, #93c5fd, #60a5fa);
            -webkit-background-clip: text; background-clip: text; color: transparent;
            text-shadow: 0 0 20px rgba(59, 130, 246, 0.5);
            animation: textBreath 4s infinite alternate;
        }
        @keyframes textBreath {
            0% { transform: scale(1); }
            100% { transform: scale(1.02); }
        }

        .subtitle { font-size: clamp(1rem, 2vw, 1.5rem); color: #c7d2fe; margin-top: 1rem; opacity: 0.9; cursor: pointer; }

        /* --- 右侧作品区保持原型 --- */
        .right-panel {
            flex: 1;
            background-color: rgba(15, 23, 42, 0.4);
            position: relative;
            overflow-y: auto;
            scrollbar-width: none;
            perspective: 1000px;
        }
        .right-panel::-webkit-scrollbar { display: none; }

        .parallax-container {
            padding: 10vh 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 15vh;
        }

        .work-card {
            width: 80%;
            max-width: 500px;
            aspect-ratio: 4 / 5;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            overflow: hidden;
            position: relative;
            border: 1px solid rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            box-shadow: 0 20px 50px rgba(0,0,0,0.5);
            transform-style: preserve-3d;
            transition: transform 0.6s cubic-bezier(0.23, 1, 0.32, 1), box-shadow 0.6s;
            cursor: pointer;
        }

        .work-card:hover {
            transform: scale(1.05) translateY(-10px);
            box-shadow: 0 30px 60px rgba(59, 130, 246, 0.3);
            border: 1px solid rgba(147, 197, 253, 0.4);
        }

        .work-card img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 1s ease;
        }

        .work-card:hover img {
            transform: scale(1.1);
        }

        .card-info {
            position: absolute;
            bottom: 0; left: 0; width: 100%;
            padding: 20px;
            background: linear-gradient(to top, rgba(12, 20, 39, 0.9), transparent);
            transform: translateY(20px);
            opacity: 0;
            transition: all 0.4s ease;
        }

        .work-card:hover .card-info {
            transform: translateY(0);
            opacity: 1;
        }

        @media (max-width: 768px) {
            .main-container { flex-direction: column; }
            .left-panel { width: 100%; height: 60vh; }
            .right-panel { width: 100%; height: 100vh; }
        }

        /* --- 植入：美化后的详情页样式 --- */
        #detailOverlay {
            position: fixed; inset: 0; z-index: 2000; opacity: 0; pointer-events: none;
            background: rgba(12, 20, 39, 0.98); backdrop-filter: blur(40px);
            transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
            overflow-y: auto; transform: translateY(50px);
        }
        #detailOverlay.active { opacity: 1; pointer-events: auto; transform: translateY(0); }

        .typewriter-text { 
            font-family: 'Courier Prime', monospace; 
            letter-spacing: 0.15em; 
            text-shadow: 0 0 8px rgba(147, 197, 253, 0.3);
        }
        
        .detail-content { max-width: 900px; margin: 0 auto; padding: 10vh 5%; }
        
        .album-title {
            font-family: 'Special Elite', cursive;
            font-size: clamp(2.5rem, 5vw, 4rem);
            background: linear-gradient(90deg, #fff, #93c5fd);
            -webkit-background-clip: text; color: transparent;
            letter-spacing: 2px;
        }

        .album-media-label {
            font-size: 0.75rem;
            padding-left: 10px;
            border-left: 3px solid #3b82f6;
            margin-bottom: 1.5rem;
            color: rgba(147, 197, 253, 0.6);
            letter-spacing: 2px;
        }

        .back-btn { 
            color: #93c5fd; border: 1px solid rgba(147, 197, 253, 0.3); 
            padding: 12px 30px; border-radius: 30px; background: none; 
            cursor: pointer; transition: all 0.3s;
        }
        .back-btn:hover { background: rgba(147, 197, 253, 0.1); border-color: #93c5fd; }
    </style>
</head>
<body>
    <div class="mouse-glow"></div>
    <div class="stars"></div>

    <div class="main-container">
        <div class="left-panel">
            <div class="window">
                <div class="window-top"><div class="window-glass"><div class="light-stream"></div><div class="light-reflect reflect-1"></div><div class="moon" style="width:25px;height:25px;top:20%;right:30%"></div></div></div>
                <div class="window-bottom">
                    <div class="window-glass">
                        <div class="light-stream" style="top:20%"></div>
                        <div class="light-stream" style="top:50%;animation-delay:-4s"></div>
                        <div class="light-reflect reflect-1"></div><div class="light-reflect reflect-2"></div><div class="light-reflect reflect-3"></div>
                        <div class="moon"></div>
                        <div class="cloud cloud-1"></div><div class="cloud cloud-2"></div><div class="cloud cloud-3"></div>
                    </div>
                </div>
            </div>
            <div class="text-overlay">
                <h1 class="work-title">My Work?</h1>
                <p class="subtitle">scroll to explore my dream</p>
            </div>
        </div>

        <div class="right-panel" id="scrollContainer">
            <div class="parallax-container" id="parallaxContainer">
                <div class="work-card" data-id="traffic">
                    <img src="作品集贴图/海报定稿.jpg" alt="Traffic Control">
                    <div class="card-info"><h1>Traffic Control</h1><p>短片</p></div>
                </div>
                <div class="work-card" data-id="meiyu">
                    <img src="作品集贴图/goldfish.jpg" alt="梅雨">
                    <div class="card-info"><h1>梅雨</h1><p>动画</p></div>
                </div>
                <div class="work-card" data-id="seoul">
                    <img src="作品集贴图/Seoul.jpg" alt="Only Seoul Knows">
                    <div class="card-info"><h1>Only Seoul Knows</h1><p>动画OST</p></div>
                </div>
                <div class="work-card" data-id="stars">
                    <img src="作品集贴图/still frame6.jpg" alt="遥远的星辰">
                    <div class="card-info"><h1>遥远的星辰</h1><p>动画</p></div>
                </div>
                <div class="work-card" data-id="ritual">
                    <img src="作品集贴图/p5.js.jpg" alt="The Ritual Gazette">
                    <div class="card-info"><h1>The Ritual Gazette</h1><p>交互设计</p></div>
                </div>
            </div>
        </div>
    </div>

    <div id="detailOverlay">
        <button onclick="closeDetail()" style="position:fixed; top:40px; right:40px; color:#fff; font-size:2rem; background:none; border:none; cursor:pointer; z-index:2100; opacity: 0.5;">✕</button>
        <div class="detail-content" id="detailContent"></div>
    </div>

    <script>
        // 1. 扩展作品详细数据（已增加参数字段）
        const projectDetails = {
            "traffic": {
                title: "Traffic Control",
                year: "2026",
                role: "Director / Editor",
                tools: "Premiere, After Effects, DaVinci",
                desc: `PROJECT LOG: 2026 | TRAFFIC CONTROL\n这是一部聚焦城市交通秩序与人文情绪的实验短片。\n以静默的镜头语言，捕捉红绿灯下的城市脉搏，探索机械秩序与生命温度之间的微妙平衡。\n\n每一次红灯的等待，都是城市故事的暂停键；每一次绿灯的通行，都是生活轨迹的继续。用镜头记录城市的呼吸，用画面诠释秩序的美学。`,
                video: "clips/1.mp4",
                images: ["作品集贴图/海报定稿.jpg"]
            },
            "meiyu": {
                title: "梅雨",
                year: "2025",
                role: "Animator / Visual Artist",
                tools: "Procreate, After Effects",
                desc: "捕捉南方梅雨季节特有的青蓝色调。光影在潮湿空气中的折射效果，试图呈现一种被水气包裹的忧郁与宁静。",
                video: "",
                images: ["作品集贴图/goldfish.jpg"]
            },
            "seoul": {
                title: "Only Seoul Knows",
                year: "2025",
                role: "Sound Designer",
                tools: "Ableton Live, Logic Pro",
                desc: "城市记忆的视觉化呈现。通过声音采样与视觉元素的错位拼接，还原一个只属于深夜首尔的梦境。",
                video: "",
                images: ["作品集贴图/Seoul.jpg"]
            },
            "stars": {
                title: "遥远的星辰",
                year: "2024",
                role: "Visual Designer",
                tools: "Cinema 4D, Octane Render",
                desc: "关于孤独与远方的叙事。利用粒子系统模拟星辰的明灭，探讨人类情感在宏大宇宙尺度下的微弱回响。",
                video: "",
                images: ["作品集贴图/still frame6.jpg"]
            },
            "ritual": {
                title: "The Ritual Gazette",
                year: "2024",
                role: "Interactive Designer",
                tools: "p5.js, JavaScript",
                desc: "基于 p5.js 的交互实验。将传统的‘仪式感’抽象为代码算法，通过鼠标交互生成独特的视觉图形报刊。",
                video: "",
                images: ["作品集贴图/p5.js.jpg"]
            }
        };

        window.addEventListener('load', () => {
            document.body.classList.add('loaded');
            createStars();
            initInfiniteScroll();
            initClickEvents();
        });

        // 保持原型的鼠标跟随和星光逻辑
        const mouseGlow = document.querySelector('.mouse-glow');
        window.addEventListener('mousemove', (e) => {
            mouseGlow.style.left = `${e.clientX}px`;
            mouseGlow.style.top = `${e.clientY}px`;
        });

        function createStars() {
            const starsContainer = document.querySelector('.stars');
            for(let i=0; i<80; i++){
                const star = document.createElement('div');
                star.className = 'star';
                const size = Math.random() * 2 + 1;
                star.style.width = star.style.height = `${size}px`;
                star.style.left = `${Math.random() * 100}%`;
                star.style.top = `${Math.random() * 100}%`;
                star.style.animationDuration = `${Math.random() * 3 + 2}s`;
                starsContainer.appendChild(star);
            }
        }

        // 保持原型的滚动逻辑
        function initInfiniteScroll() {
            const container = document.getElementById('scrollContainer');
            const content = document.getElementById('parallaxContainer');
            const clone = content.cloneNode(true);
            container.appendChild(clone);

            container.addEventListener('scroll', () => {
                const scrollTop = container.scrollTop;
                const scrollHeight = content.offsetHeight;
                if (scrollTop >= scrollHeight) { container.scrollTop = 1; }
                else if (scrollTop <= 0) { container.scrollTop = scrollHeight - 1; }

                const allCards = document.querySelectorAll('.work-card');
                allCards.forEach(card => {
                    const rect = card.getBoundingClientRect();
                    const cardCenter = rect.top + rect.height / 2;
                    const screenCenter = window.innerHeight / 2;
                    const distanceFromCenter = (cardCenter - screenCenter) / screenCenter;
                    const scale = 1 - Math.abs(distanceFromCenter) * 0.1;
                    const rotate = distanceFromCenter * 10;
                    card.style.transform = `scale(${scale}) rotateX(${rotate}deg)`;
                });
            });
        }

        function initClickEvents() {
            document.addEventListener('click', (e) => {
                const card = e.target.closest('.work-card');
                if (card) {
                    const pid = card.getAttribute('data-id');
                    if (pid && projectDetails[pid]) openDetail(projectDetails[pid]);
                }
            });
        }

        // 2. 深度美化后的 openDetail 函数
        function openDetail(data) {
            const overlay = document.getElementById('detailOverlay');
            const content = document.getElementById('detailContent');
            
            content.innerHTML = `
                <div class="opacity-0 translate-y-10 transition-all duration-1000 ease-out" id="detailAnimate">
                    <header class="border-b border-blue-400/30 pb-8 mb-12">
                        <h1 class="album-title mb-6">${data.title}</h1>
                        
                        <div class="flex flex-wrap gap-8 text-xs typewriter-text uppercase text-blue-300/70">
                            <div><span class="text-blue-400/40 mr-2">Year:</span>${data.year}</div>
                            <div><span class="text-blue-400/40 mr-2">Role:</span>${data.role}</div>
                            <div><span class="text-blue-400/40 mr-2">Tech:</span>${data.tools}</div>
                        </div>
                    </header>

                    <div class="grid grid-cols-1 md:grid-cols-3 gap-12 mb-20">
                        <div class="md:col-span-2">
                            <p class="text-lg leading-loose text-blue-100/90 whitespace-pre-line italic font-light">
                                ${data.desc}
                            </p>
                        </div>
                        <div class="text-xs typewriter-text text-blue-400/40 leading-loose border-l border-blue-400/20 pl-6">
                            // MISSION_LOG: EXTRACTING_METADATA...
                            <br>Status: Archive_Completed
                            <br>Format: 4K_UHD_LOG
                            <br>Location: Virtual_Blue_Hour
                        </div>
                    </div>

                    <div class="media-grid space-y-24">
                        ${data.video ? `
                            <div class="group">
                                <p class="album-media-label">// SEQUENCE_CLIP.01</p>
                                <div class="relative overflow-hidden rounded shadow-2xl border border-white/10">
                                    <video class="w-full" autoplay loop muted src="${data.video}"></video>
                                </div>
                            </div>` : ''}
                        
                        ${data.images.map((img, index) => `
                            <div class="group">
                                <p class="album-media-label">// VISUAL_RECORD.0${index + 1}</p>
                                <img src="${img}" class="w-full rounded shadow-2xl border border-white/10 transition-transform duration-700 group-hover:scale-[1.01]" alt="Detail View">
                            </div>
                        `).join('')}
                    </div>

                    <div class="mt-32 pb-20 text-center">
                        <button onclick="closeDetail()" class="back-btn typewriter-text group">
                            <span class="inline-block transition-transform group-hover:-translate-x-2">←</span> 
                            TERMINATE_SESSION & RETURN
                        </button>
                    </div>
                </div>
            `;

            overlay.classList.add('active');
            document.body.style.overflow = 'hidden';

            // 触发入场动画
            setTimeout(() => {
                const anim = document.getElementById('detailAnimate');
                if(anim) anim.classList.remove('opacity-0', 'translate-y-10');
            }, 100);
        }

        function closeDetail() {
            document.getElementById('detailOverlay').classList.remove('active');
            document.body.style.overflow = '';
        }
    </script>
</body>
</html>
