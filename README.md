<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>怡口科研 - 生物製劑訂購系統</title>
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="theme-color" content="#2E7D32">
    <link rel="manifest" href="manifest.json">
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;700&display=swap" rel="stylesheet">
    
    <style>
        /* --- 核心主題色設定 --- */
        :root {
            --primary-green: #2E7D32; /* 深綠色 - 專業主色 */
            --secondary-green: #81C784; /* 淺綠色 - 點綴與活力 */
            --eco-beige: #F1F8E9; /* 米色/淺草綠 - 背景基底 */
            --text-dark: #37474F; /* 深灰 - 文字色 */
            --accent-red: #D32F2F; /* 強調色 - 價格與警告 */
        }

        body {
            font-family: 'Noto Sans TC', 'Microsoft JhengHei', sans-serif;
            background-color: var(--eco-beige);
            /* 加入一點點細微的自然紋理背景 (選用) */
            background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='100' height='100' viewBox='0 0 100 100'%3E%3Cg fill-rule='evenodd'%3E%3Cg fill='%232e7d32' fill-opacity='0.03'%3E%3Cpath opacity='.5' d='M96 95h4v1h-4v4h-1v-4h-9v4h-1v-4h-9v4h-1v-4h-9v4h-1v-4h-9v4h-1v-4h-9v4h-1v-4h-9v4h-1v-4h-9v4h-1v-4h-9v4h-1v-4H0v-1h15v-9H0v-1h15v-9H0v-1h15v-9H0v-1h15v-9H0v-1h15v-9H0v-1h15v-9H0v-1h15v-9H0v-1h15v-9H0v-1h15v-9H0v-1h15v-9H0v-1h15v-9H0v-1h15v-9H0v-1h15v-9H0v-1h15v-9H0v-1h15v-9H0v-1h15v-9L0 0h96v95zM16 16h64v64H16V16z'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
            color: var(--text-dark);
            line-height: 1.6;
            margin: 0;
            padding: 20px 10px;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            background: #fff;
            padding: 25px;
            border-radius: 16px; /* 更圓潤的邊角 */
            box-shadow: 0 8px 20px rgba(46, 125, 50, 0.15); /* 帶綠色調的陰影 */
            border-top: 5px solid var(--primary-green);
        }

        h1 {
            text-align: center;
            color: var(--primary-green);
            font-size: 1.8rem;
            margin-bottom: 5px;
        }
        
        h2 {
            text-align: center;
            color: var(--text-dark);
            font-size: 1.2rem;
            font-weight: normal;
            margin-top: 0;
            position: relative;
            padding-bottom: 15px;
        }

        h2::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 60px;
            height: 3px;
            background-color: var(--secondary-green);
            border-radius: 2px;
        }

        .section-header {
            font-size: 1.3rem;
            color: var(--primary-green);
            margin-top: 30px;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
        }
        
        /* 加入一個小葉子圖示在標題前 */
        .section-header::before {
            content: '🌿';
            margin-right: 8px;
        }

        .product-card {
            border: none;
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 25px;
            background: #ffffff;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
            border-left: 4px solid var(--secondary-green);
            transition: transform 0.2s;
        }
        
        /* 手機上觸碰時的微互動 */
        .product-card:active {
            transform: scale(0.99);
        }

        .product-title {
            font-size: 1.4em;
            font-weight: bold;
            color: var(--primary-green);
            margin-bottom: 10px;
        }

        .product-desc {
            font-size: 0.95em;
            color: #666;
            margin-bottom: 15px;
            background-color: var(--eco-beige);
            padding: 12px;
            border-radius: 8px;
        }

        .warning {
            color: var(--accent-red);
            font-weight: bold;
            display: block;
            margin-top: 5px;
        }

        /* 表格優化 */
        table {
            width: 100%;
            border-collapse: separate;
            border-spacing: 0;
            margin-bottom: 10px;
            border-radius: 8px;
            overflow: hidden;
        }
        th {
            background-color: var(--primary-green);
            color: white;
            padding: 12px;
            text-align: left;
            font-weight: normal;
        }
        td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid #eee;
            background-color: #fff;
        }
        tr:last-child td {
            border-bottom: none;
        }

        /* 輸入框優化 (適合手指點擊) */
        input[type="number"] {
            width: 70px;
            padding: 8px;
            border: 2px solid #ddd;
            border-radius: 25px; /* 膠囊狀 */
            text-align: center;
            font-size: 16px;
            outline: none;
            transition: border-color 0.3s;
        }
        
        input[type="number"]:focus, 
        input[type="text"]:focus,
        input[type="tel"]:focus,
        textarea:focus {
            border-color: var(--secondary-green);
        }

        .form-section {
            background-color: #fff;
            padding: 5px;
            margin-top: 30px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            font-weight: bold;
            margin-bottom: 8px;
            color: var(--primary-green);
        }

        .form-group input, .form-group textarea {
            width: 100%;
            padding: 12px;
            border: 2px solid #eee;
            border-radius: 8px;
            box-sizing: border-box;
            font-size: 16px; /* 防止 iOS 縮放 */
            background-color: #fafafa;
        }

        .summary-box {
            background: linear-gradient(to bottom right, #ffffff, var(--eco-beige));
            border: 2px solid var(--secondary-green);
            padding: 20px;
            border-radius: 12px;
            margin-top: 30px;
        }

        #order-summary-text {
            white-space: pre-wrap;
            margin-bottom: 15px;
            background: #fff;
            padding: 15px;
            border-radius: 8px;
            border: 1px dashed var(--secondary-green);
            font-family: monospace;
            font-size: 0.9rem;
        }

        .total-row {
            display: flex;
            justify-content: space-between;
            margin-top: 15px;
            font-size: 1.1rem;
        }

        .total-price {
            font-size: 1.6em;
            font-weight: bold;
            color: var(--accent-red);
            text-align: right;
            margin-top: 10px;
            padding-top: 10px;
            border-top: 2px solid #eee;
        }
        
        .shipping-hint {
            font-size: 0.85rem;
            color: var(--primary-green);
        }

        /* 按鈕優化 */
        .btn-submit {
            display: block;
            width: 100%;
            padding: 18px;
            /* 漸層綠色按鈕 */
            background: linear-gradient(to right, var(--primary-green), #43a047);
            color: white;
            text-align: center;
            font-size: 1.3em;
            font-weight: bold;
            border: none;
            border-radius: 30px; /* 大圓角 */
            cursor: pointer;
            margin-top: 25px;
            box-shadow: 0 4px 15px rgba(46, 125, 50, 0.3);
            transition: all 0.3s;
            -webkit-tap-highlight-color: transparent;
        }

        .btn-submit:hover, .btn-submit:active {
            background: linear-gradient(to right, #1b5e20, var(--primary-green));
            box-shadow: 0 2px 5px rgba(46, 125, 50, 0.3);
            transform: translateY(2px);
        }
        
        /* 讀取中遮罩 */
        #loading-overlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(255,255,255,0.9);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 999;
            flex-direction: column;
            color: var(--primary-green);
        }
        .spinner {
            border: 4px solid #f3f3f3;
            border-top: 4px solid var(--primary-green);
            border-radius: 50%;
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
            margin-bottom: 10px;
        }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }

    </style>
</head>
<body>

<div class="container">
    <h1>怡口科研股份有限公司</h1>
    <h2>環保永續・生物製劑訂購</h2>

    <div class="section-header">選擇產品</div>
    
    <div class="product-card">
        <div class="product-title">碳晶讚</div>
        <div class="product-desc">
            <p>抗真菌及細菌類病害(炭疽病、白粉病等)，對部分蟲害有效。</p>
            <span class="warning">❄️ 此產品需要冷藏保存</span>
        </div>
        <table>
            <tr><th>規格</th><th>單價</th><th>數量</th></tr>
            <tr><td>1 公升</td><td>$1,000</td><td><input type="number" min="0" value="0" class="item-qty" data-name="碳晶讚 1公升" data-price="1000" data-vol="1"></td></tr>
            <tr><td>4 公升</td><td>$3,800</td><td><input type="number" min="0" value="0" class="item-qty" data-name="碳晶讚 4公升" data-price="3800" data-vol="4"></td></tr>
            <tr><td>10 公升</td><td>$9,500</td><td><input type="number" min="0" value="0" class="item-qty" data-name="碳晶讚 10公升" data-price="9500" data-vol="10"></td></tr>
        </table>
    </div>

    <div class="product-card">
        <div class="product-title">甲晶讚</div>
        <div class="product-desc">
            <p>高濃度5%水溶性甲殼素。提供田間益菌養分，防治線蟲與病害。獨特微奈米化製程，土壤長效緩釋。</p>
        </div>
        <table>
            <tr><th>規格</th><th>單價</th><th>數量</th></tr>
            <tr><td>4 公升</td><td>$600</td><td><input type="number" min="0" value="0" class="item-qty" data-name="甲晶讚 4公升" data-price="600" data-vol="4"></td></tr>
            <tr><td>10 公升</td><td>$1,300</td><td><input type="number" min="0" value="0" class="item-qty" data-name="甲晶讚 10公升" data-price="1300" data-vol="10"></td></tr>
        </table>
    </div>

    <div class="product-card">
        <div class="product-title">展著劑</div>
        <div class="product-desc">
             <p>增加藥劑附著力與展布性，提升防治效果。</p>
        </div>
        <table>
            <tr><th>規格</th><th>單價</th><th>數量</th></tr>
            <tr><td>4 公升</td><td>$1,280</td><td><input type="number" min="0" value="0" class="item-qty" data-name="展著劑 4公升" data-price="1280" data-vol="4"></td></tr>
            <tr><td>10 公升</td><td>$3,000</td><td><input type="number" min="0" value="0" class="item-qty" data-name="展著劑 10公升" data-price="3000" data-vol="10"></td></tr>
        </table>
    </div>

    <div class="form-section">
        <div class="section-header">收件人資料</div>
        <div class="form-group">
            <label for="buyer-name">姓名 *</label>
            <input type="text" id="buyer-name" placeholder="請輸入您的稱呼">
        </div>
        <div class="form-group">
            <label for="buyer-phone">聯絡電話 *</label>
            <input type="tel" id="buyer-phone" placeholder="例如: 0912345678">
        </div>
        <div class="form-group">
            <label for="buyer-address">收件地址 *</label>
            <input type="text" id="buyer-address" placeholder="請輸入詳細地址">
        </div>
        <div class="form-group">
            <label for="buyer-notes">備註事項</label>
            <textarea id="buyer-notes" rows="3" placeholder="如有特殊需求請填寫"></textarea>
        </div>
    </div>

    <div class="summary-box">
        <div class="section-header" style="margin-top:0">訂單確認</div>
        <div id="order-summary-text">請選擇商品...</div>
        
        <div class="total-row">
            <span>總公升數：</span>
            <span><strong id="total-vol">0</strong> 公升</span>
        </div>
        <div class="total-row">
            <span>運費：<br><span class="shipping-hint">(滿20L免運，未滿收$200)</span></span>
            <span>$ <strong id="shipping-fee">0</strong></span>
        </div>
        
        <div class="total-price">
            總計：$ <span id="total-price">0</span>
        </div>
    </div>

    <button class="btn-submit" id="submit-btn" onclick="submitOrder()">確認送出訂單</button>

</div>

<div id="loading-overlay">
    <div class="spinner"></div>
    <div>正在傳送訂單，請稍候...</div>
</div>

<script>
    const inputs = document.querySelectorAll('.item-qty');
    const nameInput = document.getElementById('buyer-name');
    const phoneInput = document.getElementById('buyer-phone');
    const addressInput = document.getElementById('buyer-address');
    const notesInput = document.getElementById('buyer-notes');
    const loadingOverlay = document.getElementById('loading-overlay');
    
    // 綁定事件：即時計算
    ['input', 'change'].forEach(evt => {
        inputs.forEach(input => input.addEventListener(evt, calculateTotal));
    });
    [nameInput, phoneInput, addressInput, notesInput].forEach(el => {
        el.addEventListener('input', updateSummaryText);
    });

    let currentOrderData = {
        subtotal: 0,
        totalVol: 0,
        shippingFee: 0,
        finalTotal: 0,
        itemsText: ""
    };

    function calculateTotal() {
        let subtotal = 0;
        let totalVol = 0;
        let itemLines = [];

        inputs.forEach(input => {
            const qty = parseInt(input.value) || 0;
            if (qty > 0) {
                const name = input.getAttribute('data-name');
                const price = parseInt(input.getAttribute('data-price'));
                const vol = parseInt(input.getAttribute('data-vol'));
                subtotal += price * qty;
                totalVol += vol * qty;
                itemLines.push(`${name} x ${qty}`);
            }
        });

        let shippingFee = (totalVol > 0 && totalVol < 20) ? 200 : 0;
        const finalTotal = subtotal + shippingFee;

        // 更新畫面數字
        document.getElementById('total-vol').innerText = totalVol;
        document.getElementById('shipping-fee').innerText = shippingFee;
        document.getElementById('total-price').innerText = finalTotal.toLocaleString();

        // 儲存當前數據供送出使用
        currentOrderData = {
            subtotal, totalVol, shippingFee, finalTotal,
            itemsText: itemLines.join('\n')
        };
        updateSummaryText();
    }

    function updateSummaryText() {
        if (currentOrderData.itemsText === "") {
             document.getElementById('order-summary-text').innerText = "尚未選擇商品";
             return;
        }
        let summaryText = `【訂購商品】\n${currentOrderData.itemsText}\n\n`;
        summaryText += `【收件資料】\n`;
        summaryText += `姓名：${nameInput.value || '-'}\n`;
        summaryText += `電話：${phoneInput.value || '-'}\n`;
        summaryText += `地址：${addressInput.value || '-'}\n`;
        document.getElementById('order-summary-text').innerText = summaryText;
    }

    // --- 關鍵：送出訂單到 Google Sheet ---
    function submitOrder() {
        // 1. 基本驗證
        if (currentOrderData.finalTotal === 0) {
            alert("請至少選擇一樣商品喔！");
            return;
        }
        if (!nameInput.value || !phoneInput.value || !addressInput.value) {
            alert("請完整填寫姓名、電話與地址，方便我們出貨！");
            return;
        }

        // 2. 準備要傳送的資料物件
        const dataToSend = {
            "訂購時間": new Date().toLocaleString('zh-TW', { timeZone: 'Asia/Taipei' }),
            "姓名": nameInput.value,
            "電話": phoneInput.value,
            "地址": addressInput.value,
            "備註": notesInput.value,
            "訂購明細": currentOrderData.itemsText,
            "總公升數": currentOrderData.totalVol,
            "運費": currentOrderData.shippingFee,
            "總金額": currentOrderData.finalTotal
        };

        // 3. 顯示讀取中，禁用按鈕
        loadingOverlay.style.display = 'flex';
        document.getElementById('submit-btn').disabled = true;

        // --- 【重要】請將下方的 URL 替換成您自己的 Google Apps Script 網址 ---
        const scriptURL = 'Y[OUR_GOOGLE_SCRIPT_URL_HER](https://script.google.com/macros/s/AKfycby9jyTwR4MW2K01SVgdQkp0krzCDKFrw-pOApvhd9jNyikUOn8Cnrris3pNrNykL0T6/exec)E'; 
        // -----------------------------------------------------------------

        if (scriptURL === '[YOUR_GOOGLE_SCRIPT_URL_HERE](https://script.google.com/macros/s/AKfycby9jyTwR4MW2K01SVgdQkp0krzCDKFrw-pOApvhd9jNyikUOn8Cnrris3pNrNykL0T6/exec)') {
            alert("請先設定 Google Apps Script 網址 (詳見說明文件)");
            loadingOverlay.style.display = 'none';
            document.getElementById('submit-btn').disabled = false;
            return;
        }

        // 4. 使用 fetch API 發送資料
        fetch(scriptURL, {
            method: 'POST',
            mode: 'no-cors', // 重要：跨域設定
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(dataToSend)
        })
        .then(response => {
            // 成功送出後
            loadingOverlay.style.display = 'none';
            alert("訂單已成功送出！我們會盡快為您處理。謝謝！");
            // 清空表單或重整頁面
            window.location.reload();
        })
        .catch(error => {
            loadingOverlay.style.display = 'none';
            document.getElementById('submit-btn').disabled = false;
            console.error('Error!', error.message);
            alert("抱歉，訂單傳送失敗，請稍後再試，或直接聯繫我們。");
        });
    }

    // 初始化
    calculateTotal();
</script>

</body>
</html>
