<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI Prediction Tool - Pro</title>
    <style>
        * { box-sizing: border-box; }
        body {
            /* নিচের লিঙ্কে আপনার লোগো বা ব্যাকগ্রাউন্ড ছবির লিঙ্কটি বসান */
            background: url('https://hgnice1.com/assets/png/logo-b9409860.png') no-repeat center center fixed;
            background-size: cover;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            font-family: 'Segoe UI', sans-serif;
            overflow: hidden;
        }

        /* ব্যাকগ্রাউন্ডের উপরে হালকা ঝাপসা কালো আবরণ */
        body::before {
            content: "";
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0, 0, 0, 0.6);
            z-index: -1;
        }

        .container {
            background-color: rgba(18, 20, 26, 0.9);
            width: 340px;
            padding: 25px;
            border-radius: 30px;
            border: 2px solid #ff0000; /* লোগোর সাথে মিল রেখে লাল বর্ডার */
            text-align: center;
            box-shadow: 0 0 20px rgba(255, 0, 0, 0.5);
            backdrop-filter: blur(10px);
            position: relative;
        }

        /* Header */
        .header { display: flex; align-items: center; justify-content: space-between; margin-bottom: 25px; }
        .profile-section { display: flex; align-items: center; gap: 10px; }
        .avatar { width: 55px; height: 55px; border-radius: 50%; border: 2px solid white; object-fit: cover; }
        .username { color: white; font-size: 18px; font-weight: bold; text-shadow: 0 0 10px red; }
        .telegram-btn { background: #24A1DE; color: white; width: 35px; height: 35px; border-radius: 50%; display: flex; justify-content: center; align-items: center; text-decoration: none; font-size: 20px; }

        /* Input Fields */
        .input-field {
            width: 100%; background: #1e1e2d; border: 2px solid #ff0000;
            border-radius: 15px; padding: 15px; margin-bottom: 15px;
            color: white; outline: none; text-align: center; font-size: 16px;
        }

        .login-btn {
            width: 100%; padding: 15px; border-radius: 20px; border: none;
            background: linear-gradient(to right, #ff3e3e, #ff8c00);
            color: white; font-weight: bold; font-size: 18px; cursor: pointer;
        }

        /* Prediction Page */
        #prediction-page { display: none; }
        .timer { color: #fff; font-size: 22px; margin-bottom: 15px; font-weight: bold; }
        .prediction-box {
            background: #1e222d; border: 1px solid #444;
            border-radius: 20px; padding: 35px 10px; margin-bottom: 20px;
        }
        .result { color: #00ff00; font-size: 55px; font-weight: bold; text-shadow: 0 0 20px #00ff00; }
        .analyzing { color: #00bcd4; font-size: 13px; display: flex; align-items: center; justify-content: center; gap: 8px; margin-top: 15px; }
        .dot { height: 10px; width: 10px; background-color: #00ff00; border-radius: 50%; animation: blink 1s infinite; }

        @keyframes blink { 50% { opacity: 0; } }
        .bottom-btns { display: flex; gap: 10px; margin-top: 15px; }
        .hide-btn, .exit-btn { flex: 1; padding: 15px; border: none; border-radius: 15px; font-weight: bold; cursor: pointer; color: white; }
        .hide-btn { background: #2d2d2d; }
        .exit-btn { background: #cc0000; }
        .footer-id { color: #888; font-size: 12px; margin-top: 15px; }
    </style>
</head>
<body>

    <audio id="successSound" src="https://www.soundjay.com/buttons/button-09.mp3"></audio>
    <audio id="errorSound" src="https://www.soundjay.com/buttons/button-10.mp3"></audio>

    <div class="container">
        <div class="header">
            <div class="profile-section">
                <img src="https://via.placeholder.com/60" alt="User" class="avatar">
                <div class="username">Sojol hasan</div>
            </div>
            <a href="https://t.me/yourlink" class="telegram-btn">✈</a>
        </div>

        <div id="login-page">
            <input type="password" id="passInput" class="input-field" placeholder="PASSWORD">
            <input type="text" id="nameInput" class="input-field" placeholder="YOUR NAME">
            <button class="login-btn" onclick="checkLogin()">LOGIN</button>
        </div>

        <div id="prediction-page">
            <div class="timer" id="clock">00:00:00</div>
            <div class="prediction-box">
                <div style="color:#aaa; font-size:12px; letter-spacing: 2px;">AI PREDICTION</div>
                <div id="resText" class="result">BIG</div>
                <div id="nextTimer" style="color:white; margin: 15px 0; font-size: 18px;">Next In: 30s</div>
                <div class="analyzing"><span class="dot"></span> AI ANALYZING</div>
            </div>
        </div>

        <div class="bottom-btns">
            <button class="hide-btn">HIDE</button>
            <button class="exit-btn" onclick="location.reload()">EXIT</button>
        </div>
        <div class="footer-id">ID: RHK-9688</div>
    </div>

    <script>
        function checkLogin() {
            const pass = document.getElementById('passInput').value;
            const name = document.getElementById('nameInput').value;

            if (pass === "1234" && name.toLowerCase() === "sojol") {
                document.getElementById('successSound').play();
                document.getElementById('login-page').style.display = 'none';
                document.getElementById('prediction-page').style.display = 'block';
                startPredictionEngine();
            } else {
                document.getElementById('errorSound').play();
                alert("Incorrect Password!");
            }
        }

        function startPredictionEngine() {
            setInterval(() => {
                document.getElementById('clock').textContent = new Date().toLocaleTimeString('en-GB');
            }, 1000);

            let timeLeft = 30;
            setInterval(() => {
                timeLeft--;
                document.getElementById('nextTimer').textContent = "Next In: " + timeLeft + "s";
                if (timeLeft <= 0) {
                    const results = ["BIG", "SMALL"];
                    const randomRes = results[Math.floor(Math.random() * results.length)];
                    const resElement = document.getElementById('resText');
                    resElement.textContent = randomRes;
                    resElement.style.color = (randomRes === "SMALL") ? "#ff3e3e" : "#00ff00";
                    resElement.style.textShadow = `0 0 20px ${(randomRes === "SMALL") ? "#ff3e3e" : "#00ff00"}`;
                    timeLeft = 30;
                }
            }, 1000);
        }
    </script>
</body>
</html>
