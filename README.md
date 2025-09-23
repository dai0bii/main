<html lang="vi">

<head>
    <meta charset="UTF-8">
    <title>Ultimate Hyper VIP UI</title>
    <style>
        body {
            margin: 0;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(-45deg, #0f0c29, #302b63, #24243e, #ff0080, #00f2fe);
            background-size: 400% 400%;
            animation: gradientMove 15s ease infinite;
        }
        
        @keyframes gradientMove {
            0% {
                background-position: 0% 50%;
            }
            50% {
                background-position: 100% 50%;
            }
            100% {
                background-position: 0% 50%;
            }
        }
        /* Particles */
        
        canvas {
            position: absolute;
            top: 0;
            left: 0;
            z-index: -1;
        }
        
        .container {
            display: flex;
            flex-direction: column;
            gap: 50px;
            text-align: center;
            animation: fadeSlide 2s ease;
        }
        
        @keyframes fadeSlide {
            0% {
                opacity: 0;
                transform: translateY(100px) scale(0.8);
            }
            100% {
                opacity: 1;
                transform: translateY(0) scale(1);
            }
        }
        
        a {
            font-size: 55px;
            font-weight: 900;
            text-decoration: none;
            color: #fff;
            padding: 20px 40px;
            border-radius: 30px;
            letter-spacing: 4px;
            position: relative;
            overflow: hidden;
            background: rgba(255, 255, 255, 0.05);
            border: 2px solid rgba(255, 255, 255, 0.3);
            animation: neonPulse 3s infinite alternate;
            transition: all 0.4s ease;
            text-transform: uppercase;
            text-shadow: 0 0 20px #00f2fe, 0 0 40px #ff0080;
        }
        /* Neon nhấp nháy */
        
        @keyframes neonPulse {
            0% {
                text-shadow: 0 0 15px #00f2fe, 0 0 30px #00f2fe;
            }
            50% {
                text-shadow: 0 0 30px #ff0080, 0 0 60px #ff0080;
            }
            100% {
                text-shadow: 0 0 25px #2af598, 0 0 50px #2af598;
            }
        }
        /* Ripple hover */
        
        a::before {
            content: "";
            position: absolute;
            top: 100%;
            left: 50%;
            width: 400%;
            height: 400%;
            background: radial-gradient(circle, rgba(255, 255, 255, 0.6) 20%, transparent 70%);
            border-radius: 50%;
            transform: translateX(-50%) scale(0.1);
            opacity: 0;
            transition: all 0.7s ease;
            z-index: -1;
        }
        
        a:hover::before {
            top: 50%;
            transform: translateX(-50%) scale(1);
            opacity: 1;
        }
        /* Hover glow */
        
        a:hover {
            transform: scale(1.2) rotate(-2deg);
            box-shadow: 0 0 60px rgba(255, 255, 255, 0.9);
        }
        /* Rung khi click */
        
        a:active {
            animation: clickShake 0.4s ease;
        }
        
        @keyframes clickShake {
            0% {
                transform: scale(1.1) rotate(0deg);
            }
            25% {
                transform: scale(1.1) rotate(3deg);
            }
            50% {
                transform: scale(1.1) rotate(-3deg);
            }
            75% {
                transform: scale(1.1) rotate(2deg);
            }
            100% {
                transform: scale(1.1) rotate(0deg);
            }
        }
    </style>
</head>

<body>
    <canvas id="stars"></canvas>
    <div class="container">
        <a href="https://dai0bii.github.io/randomname/" target="_blank">random</a>
        <a href="https://dai0bii.github.io/gamealtp/" target="_blank">altp1</a>
        <a href="https://dai0bii.github.io/gamealtp1/" target="_blank">altp2</a>
        <a href="https://dai0bii.github.io/hangman/" target="_blank">HangMan</a>
    </div>

    <!-- Âm thanh -->
    <audio id="hoverSound" src="https://assets.mixkit.co/sfx/preview/mixkit-video-game-mystery-alert-234.wav"></audio>
    <audio id="clickSound" src="https://assets.mixkit.co/sfx/preview/mixkit-video-game-retro-click-237.wav"></audio>

    <script>
        // Play sound on hover/click
        const links = document.querySelectorAll("a");
        const hoverSound = document.getElementById("hoverSound");
        const clickSound = document.getElementById("clickSound");

        links.forEach(link => {
            link.addEventListener("mouseenter", () => {
                hoverSound.currentTime = 0;
                hoverSound.play();
            });
            link.addEventListener("click", () => {
                clickSound.currentTime = 0;
                clickSound.play();
            });
        });

        // Particles (stars)
        const canvas = document.getElementById("stars");
        const ctx = canvas.getContext("2d");
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        let stars = [];
        for (let i = 0; i < 150; i++) {
            stars.push({
                x: Math.random() * canvas.width,
                y: Math.random() * canvas.height,
                radius: Math.random() * 2,
                dx: (Math.random() - 0.5) * 0.5,
                dy: (Math.random() - 0.5) * 0.5
            });
        }

        function animateStars() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.fillStyle = "white";
            stars.forEach(s => {
                ctx.beginPath();
                ctx.arc(s.x, s.y, s.radius, 0, Math.PI * 2);
                ctx.fill();
                s.x += s.dx;
                s.y += s.dy;

                if (s.x < 0 || s.x > canvas.width) s.dx *= -1;
                if (s.y < 0 || s.y > canvas.height) s.dy *= -1;
            });
            requestAnimationFrame(animateStars);
        }
        animateStars();
    </script>
</body>

</html>
