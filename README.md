# Raw<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حاسبات الأسمنت والطاحونة الخام</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .container {
            width: 80%;
            max-width: 900px;
            background-color: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
        }
        h1 {
            text-align: center;
            color: #333;
        }
        .icon-container {
            display: flex;
            justify-content: space-around;
            margin-top: 30px;
        }
        .icon-button {
            background-color: #3498db;
            color: white;
            padding: 15px 40px;
            border-radius: 10px;
            font-size: 16px;
            text-align: center;
            cursor: pointer;
            width: 45%;
            transition: background-color 0.3s;
        }
        .icon-button:hover {
            background-color: #2980b9;
        }
        label {
            font-size: 14px;
            color: #555;
            display: block;
            margin-top: 10px;
        }
        input[type="number"], input[type="text"] {
            width: 100%;
            padding: 10px;
            font-size: 14px;
            margin-top: 5px;
            border-radius: 5px;
            border: 1px solid #ddd;
        }
        .button-container {
            display: flex;
            justify-content: space-between;
            margin-top: 20px;
        }
        button {
            background-color: #3498db;
            color: white;
            padding: 12px 25px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }
        button:hover {
            background-color: #2980b9;
        }
        .result {
            margin-top: 20px;
            padding: 15px;
            background-color: #27ae60;
            color: white;
            border-radius: 5px;
            display: none;
        }
        .navigation-buttons {
            display: flex;
            justify-content: space-around;
            margin-top: 20px;
        }
        .navigation-buttons button {
            background-color: #f39c12;
        }
        .navigation-buttons button:hover {
            background-color: #e67e22;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>حاسبات الأسمنت والطاحونة الخام</h1>

    <!-- Icon Navigation -->
    <div class="icon-container">
        <div class="icon-button" onclick="showCementForm()">
            حاسبة الأسمنت
        </div>
        <div class="icon-button" onclick="showRawForm()">
            حاسبة طاحونة الخام
        </div>
    </div>

    <!-- Cement Form -->
    <div id="cementForm" style="display:none;">
        <h2>حاسبة الأسمنت</h2>
        <label for="cementR">عدد الساعات (R):</label>
        <input type="number" id="cementR" placeholder="أدخل عدد الساعات">

        <label for="cementA">إجمالي تغذية الأمس (A):</label>
        <input type="number" id="cementA" placeholder="أدخل إجمالي تغذية الأمس">

        <label for="cementB">التغذية لكل ساعة (B):</label>
        <input type="number" id="cementB" placeholder="أدخل التغذية لكل ساعة">

        <label for="cementC">إجمالي تغذية اليوم (C):</label>
        <input type="number" id="cementC" placeholder="أدخل إجمالي تغذية اليوم">

        <div class="button-container">
            <button onclick="calculateCement()">احسب</button>
        </div>

        <div class="result" id="cementResult"></div>

        <div class="navigation-buttons">
            <button onclick="changeType('OPCtoSRC')">تغيير من OPC إلى SRC</button>
            <button onclick="changeType('SRCtoOPC')">تغيير من SRC إلى OPC</button>
        </div>
    </div>

    <!-- Raw Form -->
    <div id="rawForm" style="display:none;">
        <h2>حاسبة طاحونة الخام</h2>
        <label for="rawF">عدد الساعات (F):</label>
        <input type="number" id="rawF" placeholder="أدخل عدد الساعات">

        <label for="rawG">إجمالي تغذية الأمس (G):</label>
        <input type="number" id="rawG" placeholder="أدخل إجمالي تغذية الأمس">

        <label for="rawH">التغذية لكل ساعة (H):</label>
        <input type="number" id="rawH" placeholder="أدخل التغذية لكل ساعة">

        <label for="rawI">إجمالي تغذية اليوم (I):</label>
        <input type="number" id="rawI" placeholder="أدخل إجمالي تغذية اليوم">

        <div class="button-container">
            <button onclick="calculateRaw()">احسب</button>
        </div>

        <div class="result" id="rawResult"></div>

        <div class="navigation-buttons">
            <button onclick="showPileOptions()">تغيير الكومة</button>
            <button onclick="noChangePile()">لا تغيير</button>
        </div>
    </div>

    <!-- Piles Form -->
    <div id="pilesForm" style="display:none;">
        <h2>حاسبة الأكوام</h2>
        <label for="rawK">الحجر الجيري بالأمس (K):</label>
        <input type="number" id="rawK" placeholder="أدخل الحجر الجيري بالأمس">

        <label for="rawL">الحجر الجيري لكل ساعة (L):</label>
        <input type="number" id="rawL" placeholder="أدخل الحجر الجيري لكل ساعة">

        <label for="rawM">الحجر الجيري اليوم (M):</label>
        <input type="number" id="rawM" placeholder="أدخل الحجر الجيري اليوم">

        <label for="rawO">الحجر الجيري عند التغيير (O):</label>
        <input type="number" id="rawO" placeholder="أدخل الحجر الجيري عند التغيير">

        <label for="rawP">كومة المكدس (P):</label>
        <input type="number" id="rawP" placeholder="أدخل كومة المكدس">

        <label for="rawQ">كومة الأمس (Q):</label>
        <input type="number" id="rawQ" placeholder="أدخل كومة الأمس">

        <div class="navigation-buttons">
            <button onclick="changePile()">تغيير كومة</button>
            <button onclick="noChangePile()">لا يوجد تغيير</button>
        </div>

        <div class="result" id="pileResult"></div>
    </div>
</div>

<script>
    // Display Cement Form
    function showCementForm() {
        document.getElementById('cementForm').style.display = 'block';
        document.getElementById('rawForm').style.display = 'none';
        document.getElementById('pilesForm').style.display = 'none';
    }

    // Display Raw Form
    function showRawForm() {
        document.getElementById('rawForm').style.display = 'block';
        document.getElementById('cementForm').style.display = 'none';
        document.getElementById('pilesForm').style.display = 'none';
    }

    // Calculate Cement values
    function calculateCement() {
        const R = parseFloat(document.getElementById('cementR').value);
        const A = parseFloat(document.getElementById('cementA').value);
        const B = parseFloat(document.getElementById('cementB').value);
        const C = parseFloat(document.getElementById('cementC').value);

        const D = C + B;
        const Average = (D - A) / R;

        document.getElementById('cementResult').innerHTML = `
            <p><strong>المتوسط:</strong> ${Average.toFixed(2)}</p>
        `;
        document.getElementById('cementResult').style.display = 'block';
    }

    // Change Cement Type
    function changeType(type) {
        const A = parseFloat(document.getElementById('cementA').value);
        const C = parseFloat(document.getElementById('cementC').value);
        let OPC, SRC;

        if (type === 'OPCtoSRC') {
            OPC = C - A;
            SRC = C - OPC;
        } else if (type === 'SRCtoOPC') {
            OPC = C - A;
            SRC = A - OPC;
        }

        document.getElementById('cementResult').innerHTML += `
            <p><strong>OPC:</strong> ${OPC.toFixed(2)}</p>
            <p><strong>SRC:</strong> ${SRC.toFixed(2)}</p>
        `;
    }

    // Calculate Raw values
    function calculateRaw() {
        const F = parseFloat(document.getElementById('rawF').value);
        const G = parseFloat(document.getElementById('rawG').value);
        const H = parseFloat(document.getElementById('rawH').value);
        const I = parseFloat(document.getElementById('rawI').value);

        const N = I + H;
        const Average = (N - G) / F;

        document.getElementById('rawResult').innerHTML = `
            <p><strong>المتوسط:</strong> ${Average.toFixed(2)}</p>
        `;
        document.getElementById('rawResult').style.display = 'block';
    }

    // Show Pile Options
    function showPileOptions() {
        document.getElementById('pilesForm').style.display = 'block';
    }

    // Change Pile values
    function changePile() {
        const K = parseFloat(document.getElementById('rawK').value);
        const L = parseFloat(document.getElementById('rawL').value);
        const M = parseFloat(document.getElementById('rawM').value);
        const O = parseFloat(document.getElementById('rawO').value);
        const P = parseFloat(document.getElementById('rawP').value);
        const Q = parseFloat(document.getElementById('rawQ').value);

        const total = K + L + M + O + P + Q;

        document.getElementById('pileResult').innerHTML = `
            <p><strong>الإجمالي الكلي:</strong> ${total.toFixed(2)}</p>
        `;
        document.getElementById('pileResult').style.display = 'block';
    }

    // No Change in Pile
    function noChangePile() {
        document.getElementById('pileResult').innerHTML = `
            <p><strong>لا يوجد تغيير في الكومة.</strong></p>
        `;
        document.getElementById('pileResult').style.display = 'block';
    }
</script>

</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Raw Mill Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }
        .container {
            width: 90%;
            max-width: 800px;
            margin: 20px auto;
            background: #fff;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            padding: 20px;
        }
        h1, h2 {
            text-align: center;
            color: #333;
        }
        .calculator {
            display: none;
        }
        .calculator.active {
            display: block;
        }
        .buttons {
            display: flex;
            justify-content: center;
            margin-bottom: 20px;
        }
        .buttons button {
            margin: 5px;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            background-color: #007BFF;
            color: white;
            font-size: 16px;
        }
        .buttons button:hover {
            background-color: #0056b3;
        }
        .form-group {
            margin-bottom: 15px;
        }
        .form-group label {
            display: block;
            margin-bottom: 5px;
            color: #333;
        }
        .form-group input, .form-group select {
            width: 100%;
            padding: 10px;
            font-size: 16px;
            border: 1px solid #ddd;
            border-radius: 5px;
        }
        .result {
            margin-top: 15px;
            padding: 10px;
            background: #f9f9f9;
            border: 1px solid #ddd;
            border-radius: 5px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Raw Mill Calculator</h1>
        <div class="buttons">
            <button onclick="showCalculator('cement')">Cement Mill Calculator</button>
            <button onclick="showCalculator('raw')">Raw Mill Calculator</button>
        </div>

        <!-- Cement Mill Calculator -->
        <div id="cement" class="calculator">
            <h2>Cement Mill Calculator</h2>
            <div class="form-group">
                <label for="r">Running Hours (R):</label>
                <input type="number" id="r" />
            </div>
            <div class="form-group">
                <label for="a">Total Feed Yesterday (A):</label>
                <input type="number" id="a" />
            </div>
            <div class="form-group">
                <label for="b">Feed Per Hour (B):</label>
                <input type="number" id="b" />
            </div>
            <div class="form-group">
                <label for="c">Total Feed Today (C):</label>
                <input type="number" id="c" />
            </div>
            <div class="result">
                <p>Total Feed (D): <span id="d"></span></p>
                <p>Average: <span id="average"></span></p>
            </div>
            <button onclick="calculateCement()">Calculate</button>
            <div>
                <h3>Change Type</h3>
                <button onclick="changeType('opc-to-src')">Change from OPC to SRC</button>
                <button onclick="changeType('src-to-opc')">Change from SRC to OPC</button>
            </div>
            <div id="change-result"></div>
        </div>

        <!-- Raw Mill Calculator -->
        <div id="raw" class="calculator">
            <h2>Raw Mill Calculator</h2>
            <div class="form-group">
                <label for="f">Running Hours (F):</label>
                <input type="number" id="f" />
            </div>
            <div class="form-group">
                <label for="g">Total Feed Yesterday (G):</label>
                <input type="number" id="g" />
            </div>
            <div class="form-group">
                <label for="h">Feed Per Hour (H):</label>
                <input type="number" id="h" />
            </div>
            <div class="form-group">
                <label for="i">Total Feed Today (I):</label>
                <input type="number" id="i" />
            </div>
            <div class="result">
                <p>Total Feed (J): <span id="j"></span></p>
                <p>Average: <span id="avr"></span></p>
            </div>
            <h3>Limestone</h3>
            <div class="form-group">
                <label for="k">Limestone Yesterday (K):</label>
                <input type="number" id="k" />
            </div>
            <div class="form-group">
                <label for="l">Limestone Per Hour (L):</label>
                <input type="number" id="l" />
            </div>
            <div class="form-group">
                <label for="m">Limestone Today (M):</label>
                <input type="number" id="m" />
            </div>
            <div class="result">
                <p>Total Limestone (N): <span id="n"></span></p>
            </div>
            <button onclick="calculateRaw()">Calculate</button>
            <div>
                <h3>Change Pile</h3>
                <button onclick="changePile(true)">Change Pile</button>
                <button onclick="changePile(false)">No Change</button>
            </div>
            <div id="pile-result"></div>
        </div>
    </div>

    <script>
        function showCalculator(id) {
            document.querySelectorAll('.calculator').forEach(calculator => {
                calculator.classList.remove('active');
            });
            document.getElementById(id).classList.add('active');
        }

        // Cement Mill Calculator
        function calculateCement() {
            const r = parseFloat(document.getElementById('r').value) || 0;
            const a = parseFloat(document.getElementById('a').value) || 0;
            const b = parseFloat(document.getElementById('b').value) || 0;
            const c = parseFloat(document.getElementById('c').value) || 0;

            const d = c + b;
            const average = (d - a) / r;

            document.getElementById('d').textContent = d.toFixed(2);
            document.getElementById('average').textContent = average.toFixed(2);
        }

        function changeType(type) {
            const e = parseFloat(prompt("Enter Total Feed at Change (E):")) || 0;
            const a = parseFloat(document.getElementById('a').value) || 0;
            const d = parseFloat(document.getElementById('d').textContent) || 0;

            let opc, src;

            if (type === 'opc-to-src') {
                opc = e - a;
                src = d - e;
            } else {
                opc = d - e;
                src = e - a;
            }

            document.getElementById('change-result').innerHTML = `
                <p>OPC: ${opc.toFixed(2)}</p>
                <p>SRC: ${src.toFixed(2)}</p>
            `;
        }

        // Raw Mill Calculator
        function calculateRaw() {
            const f = parseFloat(document.getElementById('f').value) || 0;
            const g = parseFloat(document.getElementById('g').value) || 0;
            const h = parseFloat(document.getElementById('h').value) || 0;
            const i = parseFloat(document.getElementById('i').value) || 0;

            const j = i + h;
            const avr = (j - g) / f;

            const k = parseFloat(document.getElementById('k').value) || 0;
            const l = parseFloat(document.getElementById('l').value) || 0;
            const m = parseFloat(document.getElementById('m').value) || 0;

            const n = m + l;

            document.getElementById('j').textContent = j.toFixed(2);
            document.getElementById('avr').textContent = avr.toFixed(2);
            document.getElementById('n').textContent = n.toFixed(2);
        }

        function changePile(change) {
            if (change) {
                const o = parseFloat(prompt("Enter Limestone at Change Pile (O):")) || 0;
                const p = parseFloat(prompt("Enter Stacker Pile (P):")) || 0;
                const q = parseFloat(prompt("Enter Reclaimer Pile Yesterday (Q):")) || 0;

                const k = parseFloat(document.getElementById('k').value) || 0;
                const n = parseFloat(document.getElementById('n').textContent) || 0;

                const s = o - k;
                const stacker = q - s;
                const t = n - o;
                const reclaimerNew = p - t;

                document.getElementById('pile-result').innerHTML = `
                    <p>Stacker: ${stacker.toFixed(2)}</p>
                    <p>Reclaimer New: ${reclaimerNew.toFixed(2)}</p>
                `;
            } else {
                const v = parseFloat(prompt("Enter Reclaimer Pile (V):")) || 0;

                const k = parseFloat(document.getElementById('k').value) || 0;
                const n = parseFloat(document.getElementById('n').textContent) || 0;

                const x = n - k;
                const reclaimer = v - x;

                document.getElementById('pile-result').innerHTML = `
                    <p>Reclaimer: ${reclaimer.toFixed(2)}</p>
                `;
            }
        }
    </script>
</body>
</html>
