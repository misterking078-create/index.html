<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes, viewport-fit=cover">
    <meta name="theme-color" content="#0a0f1c">
    <title>EarnMaster Calculator | Smart Ad-Ready App</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            user-select: none; /* prevents text selection on double tap, keeps app-like feel */
        }

        body {
            background: linear-gradient(145deg, #10131c 0%, #1a1f2e 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Segoe UI', 'Poppins', 'Inter', system-ui, -apple-system, 'Roboto', sans-serif;
            padding: 1rem;
        }

        /* main app card */
        .calculator-card {
            max-width: 500px;
            width: 100%;
            background: rgba(18, 22, 35, 0.85);
            backdrop-filter: blur(2px);
            border-radius: 3.5rem;
            box-shadow: 0 25px 45px rgba(0, 0, 0, 0.5), 0 0 0 1px rgba(255, 255, 255, 0.05);
            padding: 1.5rem 1.2rem 1.8rem;
            transition: all 0.2s ease;
        }

        /* ----- AD SPACE (MONETIZATION ZONE) ----- */
        .ad-container {
            background: #0e111b;
            border-radius: 1.2rem;
            margin-bottom: 1.2rem;
            padding: 0.6rem 0.5rem;
            text-align: center;
            border: 1px dashed rgba(255, 215, 0, 0.5);
            box-shadow: 0 2px 6px rgba(0,0,0,0.2);
            transition: all 0.2s;
        }
        .ad-placeholder {
            background: #1a1e2c;
            border-radius: 1rem;
            padding: 0.65rem 0.5rem;
            font-size: 0.8rem;
            font-weight: 500;
            color: #ffd966;
            letter-spacing: 0.5px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            font-family: monospace;
        }
        .ad-placeholder i {
            font-style: normal;
            background: #2a2f42;
            padding: 4px 8px;
            border-radius: 30px;
            font-size: 0.7rem;
            color: #ffc107;
        }
        .ad-note {
            font-size: 0.65rem;
            color: #9aa3c2;
            margin-top: 6px;
            text-align: center;
        }
        /* replace instruction for real ads */
        .monetize-tip {
            font-size: 0.6rem;
            background: #1e2338;
            display: inline-block;
            padding: 3px 8px;
            border-radius: 30px;
            color: #b9c3f0;
        }

        /* display panel */
        .display-area {
            background: #070a14;
            border-radius: 2rem;
            padding: 1.2rem 1.2rem;
            margin-bottom: 1.5rem;
            box-shadow: inset 0 4px 6px rgba(0, 0, 0, 0.4), 0 1px 0 rgba(255,255,255,0.05);
        }
        .previous-operand {
            min-height: 32px;
            font-size: 1.1rem;
            color: #8f9bb5;
            text-align: right;
            word-wrap: break-word;
            letter-spacing: 0.3px;
            font-weight: 400;
        }
        .current-operand {
            font-size: 2.8rem;
            font-weight: 600;
            color: #f0f3ff;
            text-align: right;
            word-wrap: break-word;
            word-break: break-all;
            line-height: 1.2;
            min-height: 80px;
            letter-spacing: 1px;
        }
        /* button grid */
        .buttons-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 0.75rem;
        }
        /* special row for equals (span 4) */
        .span-four {
            grid-column: span 4;
        }
        button {
            background: #1f253e;
            border: none;
            font-size: 1.5rem;
            font-weight: 500;
            padding: 1rem 0;
            border-radius: 1.8rem;
            color: #eef3ff;
            cursor: pointer;
            transition: all 0.1s ease;
            box-shadow: 0 5px 0 #0b0e16;
            font-family: inherit;
            letter-spacing: 1px;
            display: flex;
            align-items: center;
            justify-content: center;
            backdrop-filter: blur(4px);
        }
        button:active {
            transform: translateY(2px);
            box-shadow: 0 2px 0 #0b0e16;
        }
        .operator-btn {
            background: #2d3457;
            color: #ffcd7e;
            font-size: 1.7rem;
            font-weight: 600;
        }
        .equals-btn {
            background: #f5a623;
            color: #1e1f2c;
            font-weight: 800;
            font-size: 1.7rem;
            box-shadow: 0 5px 0 #b4621a;
        }
        .equals-btn:active {
            transform: translateY(2px);
            box-shadow: 0 2px 0 #b4621a;
        }
        .clear-btn {
            background: #3a2c44;
            color: #ffb4a2;
        }
        .function-btn {
            background: #2a2f48;
            color: #9dffb0;
        }
        .digit-btn {
            background: #1b213b;
            font-weight: 600;
        }
        /* responsive touch */
        @media (max-width: 480px) {
            .calculator-card {
                padding: 1rem 1rem 1.5rem;
            }
            button {
                font-size: 1.3rem;
                padding: 0.85rem 0;
            }
            .current-operand {
                font-size: 2.2rem;
                min-height: 70px;
            }
            .buttons-grid {
                gap: 0.6rem;
            }
        }
        /* footer earnings hint */
        .footer-earn {
            text-align: center;
            margin-top: 1.2rem;
            font-size: 0.7rem;
            color: #6a72a0;
            border-top: 1px solid #2a2f44;
            padding-top: 1rem;
        }
        .badge {
            background: #20273f;
            border-radius: 40px;
            padding: 0.2rem 0.8rem;
            display: inline-block;
            font-size: 0.7rem;
        }
    </style>
</head>
<body>

<div class="calculator-card">
    <!-- 🟡 MONETIZATION BLOCK: Replace this with your AdSense / AdMob banner code -->
    <div class="ad-container">
        <div class="ad-placeholder">
            <span>📢</span> YOUR AD SPACE <span>📢</span>
            <i>320x50 / responsive</i>
        </div>
        <div class="ad-note">
            <span class="monetize-tip">💰 REPLACE WITH REAL ADSENSE CODE → START EARNING 💰</span>
        </div>
    </div>
    <!-- end ad block (you can replace inner HTML with actual <ins> AdSense banner) -->

    <!-- CALCULATOR DISPLAY -->
    <div class="display-area">
        <div class="previous-operand" id="previousOperand"></div>
        <div class="current-operand" id="currentOperand">0</div>
    </div>

    <!-- BUTTON GRID -->
    <div class="buttons-grid">
        <!-- Row 1 -->
        <button class="clear-btn" data-action="clear">AC</button>
        <button class="clear-btn" data-action="delete">⌫</button>
        <button class="function-btn" data-action="percent">%</button>
        <button class="function-btn" data-action="sqrt">√</button>

        <!-- Row 2 -->
        <button class="digit-btn" data-number="7">7</button>
        <button class="digit-btn" data-number="8">8</button>
        <button class="digit-btn" data-number="9">9</button>
        <button class="operator-btn" data-operator="/">÷</button>

        <!-- Row 3 -->
        <button class="digit-btn" data-number="4">4</button>
        <button class="digit-btn" data-number="5">5</button>
        <button class="digit-btn" data-number="6">6</button>
        <button class="operator-btn" data-operator="*">×</button>

        <!-- Row 4 -->
        <button class="digit-btn" data-number="1">1</button>
        <button class="digit-btn" data-number="2">2</button>
        <button class="digit-btn" data-number="3">3</button>
        <button class="operator-btn" data-operator="-">−</button>

        <!-- Row 5 -->
        <button class="digit-btn" data-number="0">0</button>
        <button class="digit-btn" data-decimal=".">.</button>
        <button class="function-btn" data-action="sign">±</button>
        <button class="operator-btn" data-operator="+">+</button>

        <!-- Row 6 : Equals spans all columns -->
        <button class="equals-btn span-four" data-action="equals">=</button>
    </div>

    <div class="footer-earn">
        <span class="badge">💎 AD-READY CALCULATOR</span>   |   
        <span>💸 Replace ad box with AdSense / AdMob & monetize traffic</span>
    </div>
</div>

<script>
    // ------------------------------
    //   SMART CALCULATOR LOGIC
    //   Ready for high engagement & monetization
    // ------------------------------
    let currentOperand = '0';
    let previousOperand = '';
    let operation = null;        // '+', '-', '*', '/'
    let waitingForNewOperand = false;
    let errorFlag = false;

    // DOM elements
    const previousOperandElem = document.getElementById('previousOperand');
    const currentOperandElem = document.getElementById('currentOperand');

    // Helper: update display
    function updateDisplay() {
        // format current operand: avoid too long decimals
        let displayCurrent = currentOperand;
        if (!errorFlag) {
            if (displayCurrent === '') displayCurrent = '0';
            // truncate extremely long numbers for UI
            if (displayCurrent.length > 16) {
                displayCurrent = parseFloat(displayCurrent).toExponential(8);
            }
            currentOperandElem.innerText = displayCurrent;
        } else {
            currentOperandElem.innerText = 'ERROR';
        }

        if (operation && previousOperand !== '') {
            previousOperandElem.innerText = `${formatNumber(previousOperand)} ${getOperatorSymbol(operation)}`;
        } else if (previousOperand !== '' && !operation) {
            previousOperandElem.innerText = formatNumber(previousOperand);
        } else {
            previousOperandElem.innerText = '';
        }
    }

    function formatNumber(numStr) {
        if (numStr === '') return '';
        let num = parseFloat(numStr);
        if (isNaN(num)) return '';
        if (num.toString().length > 14) {
            return num.toExponential(6);
        }
        return num.toString();
    }

    function getOperatorSymbol(op) {
        if (op === '+') return '+';
        if (op === '-') return '−';
        if (op === '*') return '×';
        if (op === '/') return '÷';
        return '';
    }

    // Reset calculator completely
    function allClear() {
        currentOperand = '0';
        previousOperand = '';
        operation = null;
        waitingForNewOperand = false;
        errorFlag = false;
        updateDisplay();
    }

    // Delete last character
    function deleteLast() {
        if (errorFlag) {
            allClear();
            return;
        }
        if (waitingForNewOperand) return;
        if (currentOperand.length === 1) {
            currentOperand = '0';
        } else {
            currentOperand = currentOperand.slice(0, -1);
            if (currentOperand === '') currentOperand = '0';
        }
        updateDisplay();
    }

    // Append number
    function appendNumber(number) {
        if (errorFlag) {
            allClear();
        }
        if (waitingForNewOperand) {
            currentOperand = '';
            waitingForNewOperand = false;
        }
        // avoid multiple leading zeros
        if (number === '0' && currentOperand === '0') return;
        if (currentOperand === '0' && number !== '.') {
            currentOperand = number;
        } else {
            currentOperand += number;
        }
        // limit length
        if (currentOperand.length > 18) currentOperand = currentOperand.slice(0, 18);
        updateDisplay();
    }

    // Decimal point
    function appendDecimal() {
        if (errorFlag) {
            allClear();
        }
        if (waitingForNewOperand) {
            currentOperand = '0';
            waitingForNewOperand = false;
        }
        if (currentOperand.includes('.')) return;
        currentOperand += '.';
        updateDisplay();
    }

    // Sign toggle (+/-)
    function toggleSign() {
        if (errorFlag) {
            allClear();
            return;
        }
        if (currentOperand === '0') return;
        let num = parseFloat(currentOperand);
        if (isNaN(num)) return;
        num = -num;
        currentOperand = num.toString();
        updateDisplay();
    }

    // Percent: divide by 100
    function percentOperation() {
        if (errorFlag) {
            allClear();
            return;
        }
        let num = parseFloat(currentOperand);
        if (isNaN(num)) return;
        num = num / 100;
        currentOperand = num.toString();
        updateDisplay();
    }

    // Square root
    function squareRoot() {
        if (errorFlag) {
            allClear();
            return;
        }
        let num = parseFloat(currentOperand);
        if (isNaN(num)) return;
        if (num < 0) {
            errorFlag = true;
            updateDisplay();
            return;
        }
        let result = Math.sqrt(num);
        currentOperand = result.toString();
        waitingForNewOperand = true;
        previousOperand = '';
        operation = null;
        updateDisplay();
    }

    // Perform calculation
    function compute() {
        if (operation === null || previousOperand === '' || waitingForNewOperand) return;
        let prev = parseFloat(previousOperand);
        let current = parseFloat(currentOperand);
        if (isNaN(prev) || isNaN(current)) return;

        let computation;
        switch (operation) {
            case '+': computation = prev + current; break;
            case '-': computation = prev - current; break;
            case '*': computation = prev * current; break;
            case '/': 
                if (current === 0) {
                    errorFlag = true;
                    updateDisplay();
                    return;
                }
                computation = prev / current; 
                break;
            default: return;
        }
        // handle floating precision
        computation = parseFloat(computation.toFixed(10));
        currentOperand = computation.toString();
        operation = null;
        previousOperand = '';
        waitingForNewOperand = true;
        errorFlag = false;
        updateDisplay();
    }

    // Choose operator
    function chooseOperator(op) {
        if (errorFlag) {
            allClear();
        }
        if (currentOperand === '' && previousOperand !== '') {
            // just change operation
            operation = op;
            updateDisplay();
            return;
        }
        if (previousOperand !== '' && operation !== null && !waitingForNewOperand) {
            // compute pending operation before new one
            compute();
            if (errorFlag) return;
            waitingForNewOperand = true;
        }
        if (currentOperand === '') return;
        previousOperand = currentOperand;
        operation = op;
        waitingForNewOperand = true;
        updateDisplay();
    }

    // Equals
    function evaluate() {
        if (errorFlag) {
            allClear();
            return;
        }
        if (operation === null || previousOperand === '' || waitingForNewOperand) {
            // if no pending operation, do nothing or just refresh
            if (previousOperand !== '' && !operation && !waitingForNewOperand) {
                // nothing to evaluate
            }
            return;
        }
        compute();
        waitingForNewOperand = true;
        operation = null;
        previousOperand = '';
    }

    // ---- EVENT HANDLERS (CLICK + KEYBOARD) ----
    function handleButtonClick(event) {
        const target = event.target;
        if (!target.tagName === 'BUTTON') return;

        // Number
        if (target.hasAttribute('data-number')) {
            const num = target.getAttribute('data-number');
            appendNumber(num);
        }
        // Decimal
        else if (target.hasAttribute('data-decimal')) {
            appendDecimal();
        }
        // Operator
        else if (target.hasAttribute('data-operator')) {
            let op = target.getAttribute('data-operator');
            const opMap = { '÷': '/', '×': '*', '−': '-', '+': '+' };
            if (opMap[op]) op = opMap[op];
            chooseOperator(op);
        }
        // Special actions
        else if (target.hasAttribute('data-action')) {
            const action = target.getAttribute('data-action');
            switch (action) {
                case 'clear': allClear(); break;
                case 'delete': deleteLast(); break;
                case 'percent': percentOperation(); break;
                case 'sqrt': squareRoot(); break;
                case 'sign': toggleSign(); break;
                case 'equals': evaluate(); break;
                default: break;
            }
        }
    }

    // Attach click listeners to all buttons
    const buttons = document.querySelectorAll('button');
    buttons.forEach(btn => {
        btn.addEventListener('click', handleButtonClick);
    });

    // ---------- KEYBOARD SUPPORT (improve retention & ads views) ----------
    function handleKeyboard(e) {
        const key = e.key;
        // numbers
        if (/[0-9]/.test(key)) {
            e.preventDefault();
            appendNumber(key);
        }
        // decimal point
        else if (key === '.') {
            e.preventDefault();
            appendDecimal();
        }
        // operators
        else if (key === '+' || key === '-') {
            e.preventDefault();
            chooseOperator(key);
        }
        else if (key === '*') {
            e.preventDefault();
            chooseOperator('*');
        }
        else if (key === '/') {
            e.preventDefault();
            chooseOperator('/');
        }
        // Enter for equals
        else if (key === 'Enter' || key === '=') {
            e.preventDefault();
            evaluate();
        }
        // Backspace
        else if (key === 'Backspace') {
            e.preventDefault();
            deleteLast();
        }
        // Escape for AC
        else if (key === 'Escape') {
            e.preventDefault();
            allClear();
        }
        // % percentage
        else if (key === '%') {
            e.preventDefault();
            percentOperation();
        }
        // s for sqrt (optional)
        else if (key === 's' || key === 'S') {
            e.preventDefault();
            squareRoot();
        }
    }

    window.addEventListener('keydown', handleKeyboard);
    
    // initial display update
    updateDisplay();

    // add subtle ripple effect for better user experience (optional)
    document.querySelectorAll('button').forEach(btn => {
        btn.addEventListener('touchstart', function(e) {
            this.style.transform = 'translateY(2px)';
            this.style.boxShadow = '0 2px 0 #0b0e16';
            setTimeout(() => {
                this.style.transform = '';
                this.style.boxShadow = '';
            }, 100);
        });
        btn.addEventListener('mousedown', function() {
            this.style.transform = 'translateY(2px)';
            this.style.boxShadow = '0 2px 0 #0b0e16';
            setTimeout(() => {
                this.style.transform = '';
                this.style.boxShadow = '';
            }, 100);
        });
    });
</script>

<!-- MONETIZATION INSTRUCTIONS (embedded in code) -->
<!-- 
    ========== HOW TO EARN FROM THIS CALCULATOR APP ==========
    1. Replace the .ad-container div with your Google AdSense banner code or AdMob ad unit (for WebView apps).
    2. You can also add multiple ad placements: e.g., below buttons, or use anchor ads (AdSense auto ads).
    3. For Android/iOS: wrap this HTML/CSS/JS in a WebView and integrate AdMob banners / interstitials.
    4. Publish as PWA: add manifest.json, service worker to make installable, increase user retention.
    5. Drive traffic via social media, SEO, or app stores → every click on ads = revenue.
    
    ✅ Built with precision, modern UI, keyboard support, error handling, and smooth UX — maximize ad impressions.
    ✅ To replace ad slot: look for "ad-container" div and insert your AdSense <ins> code. Keep container responsive.
    ✅ For AdMob: Replace placeholder with native ad layout or use Google Mobile Ads SDK in WebView.
    
    ========== GOOD LUCK EARNING! ==========
-->
</body>
</html>
