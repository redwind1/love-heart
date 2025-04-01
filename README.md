<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>红色爱心雨</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            overflow: hidden;
            background: linear-gradient(135deg, #87CEEB 0%, #E0F6FF 100%);
            font-family: 'Segoe UI', sans-serif;
        }

        .heart {
            position: absolute;
            width: 24px;
            height: 24px;
            background: linear-gradient(45deg, #ff4754, #ff2d55);
            transform: translateY(0) scale(1);
            animation: float 5s linear infinite, fadeInOut 5s ease-in-out;
            filter: drop-shadow(0 0 15px rgba(255,79,90,0.8));
            opacity: 0;
        }

        .heart::before,
        .heart::after {
            content: '';
            position: absolute;
            width: 24px;
            height: 24px;
            background: inherit;
            border-radius: 50%;
        }

        .heart::before {
            top: -12px;
            left: 0;
        }

        .heart::after {
            top: 0;
            left: 12px;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0) scale(1); }
            50% { transform: translateY(-20px) scale(1.1); }
        }

        @keyframes fadeInOut {
            0%, 100% { opacity: 0; }
            10% { opacity: 1; }
            90% { opacity: 1; }
        }

        .star {
            position: absolute;
            width: 2px;
            height: 2px;
            background: #fff;
            border-radius: 50%;
            animation: twinkle 3s linear infinite;
        }

        @keyframes twinkle {
            0%, 100% { opacity: 0.5; transform: scale(0.8); }
            50% { opacity: 1; transform: scale(1.2); }
        }
    </style>
</head>
<body>
    <script>
        // 创建爱心
        function createHeart() {
            const heart = document.createElement('div');
            heart.classList.add('heart');
            
            // 随机位置
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.top = Math.random() * 100 + 'vh';
            
            // 随机大小
            const size = 20 + Math.random()*10;
            heart.style.width = heart.style.height = size + 'px';
            
            document.body.appendChild(heart);
            
            // 自动移除
            setTimeout(() => heart.remove(), 5000);
        }

        // 创建星光
        function createStars() {
            for(let i = 0; i < 20; i++) {
                const star = document.createElement('div');
                star.classList.add('star');
                
                star.style.left = Math.random() * 100 + 'vw';
                star.style.top = Math.random() * 100 + 'vh';
                star.style.animationDuration = (Math.random() * 3 + 2).toFixed(1) + 's';
                
                document.body.appendChild(star);
            }
        }

        // 初始化场景
        function init() {
            // 创建基础爱心
            for(let i = 0; i < 10; i++) {
                createHeart();
            }
            
            // 定期补充爱心
            setInterval(createHeart, 200);
            setInterval(createStars, 1000);
        }

        // 启动
        init();

        // 点击特效
        document.addEventListener('click', (e) => {
            // 创建爱心爆炸
            for(let i = 0; i < 15; i++) {
                const particle = document.createElement('div');
                particle.style.left = e.clientX + 'px';
                particle.style.top = e.clientY + 'px';
                particle.style.background = `hsl(${Math.random()*360}, 100%, 80%)`;
                particle.style.animation = `explosion ${Math.random()*2+1}s linear`;
                document.body.appendChild(particle);
            }
        });
    </script>
</body>
</html>
