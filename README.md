<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>恰口科研 - 永續農法訂購系統</title>
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="theme-color" content="#2E7D32">
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-green: #2E7D32; /* 深綠-專業 */
            --secondary-green: #81C784; /* 草綠-永續 */
            --eco-beige: #F9FBF7; /* 淺米-環保基底 */
            --text-dark: #37474F;
            --accent-orange: #FF8F00; /* 強調色 */
        }
        body {
            font-family: 'Noto Sans TC', sans-serif;
            background-color: var(--eco-beige);
            color: var(--text-dark);
            margin: 0; padding: 20px 15px;
            display: flex; justify-content: center;
        }
        .app-container {
            width: 100%; max-width: 600px;
            background: #ffffff;
            border-radius: 24px;
            box-shadow: 0 10px 30px rgba(46, 125, 50, 0.1);
            overflow: hidden;
            border-top: 8px solid var(--primary-green);
        }
        .header {
            background: linear-gradient(135deg, var(--primary-green), var(--secondary-green));
            color: white; padding: 30px 20px; text-align: center;
        }
        .header h1 { margin: 0; font-size: 1.6rem; letter-spacing: 1px; }
        .header p { margin: 5px 0 0; opacity: 0.9; font-size: 0.9rem; }

        .content { padding: 20px; }
        .section-title {
            font-size: 1.1rem; font-weight: bold; color: var(--primary-green);
            margin: 25px 0 15px; display: flex; align-items: center;
        }
        .section-title::before { content: '🌱'; margin-right: 8px; }

        /* 產品卡片 */
        .product-card {
            background: #fff; border: 1px solid #edf2ed; border-radius: 15px;
            padding: 15px; margin-bottom: 15px; transition: 0.3s;
        }
        .product-card:hover { border-color: var(--secondary-green); box-shadow: 0 4px 12px rgba(0,0,0,0.05); }
        .product-info { margin-bottom: 10px; }
        .product-name { font-weight: bold; font-size: 1.1rem; color: #1b5e20; }
        .product-tag { font-size: 0.8rem; background: #e8f5e9; color: #2e7d32; padding: 2px 8px; border-radius: 4px; margin-left: 5px; }
        
        table { width: 100%; border-collapse: collapse; font-size: 0.95rem; }
        td { padding: 10px 5px; border-bottom: 1px dotted #eee; }
        .qty-input {
            width: 60px; padding: 8px; border-radius: 12px; border: 2px solid #eee;
            text-align: center; font-size: 1rem; outline: none; transition: 0.3s;
        }
        .qty-input:focus { border-color: var(--secondary-green); background: #f1f8e9; }

        /* 表單樣式 */
        .form-group { margin-bottom: 15px; }
        .form-group label { display: block; margin-bottom: 6px; font-weight: bold; font-size: 0.9rem; }
        .form-group input, .form-group textarea {
            width: 100%; padding: 12px; border: 2px solid #eee; border-radius: 12px;
            box-sizing: border-box; font-size: 1rem; font-family: inherit;
        }
        .form-group input:focus { border-color: var(--secondary-green); outline: none; }

        /* 結帳區 */
        .summary-box {
            background: #f1f8e9; border-radius: 15px; padding: 20px; margin-top: 30px;
        }
        .summary-line { display: flex; justify-content: space-between; margin-bottom: 8px; font-size: 0.95rem; }
        .total-line { 
            display: flex; justify-content: space-between; margin-top: 15px; padding-top: 15px;
            border-top: 2px solid #dcedc8; font-size: 1.3rem; font-weight: bold; color: var(--accent-orange);
        }
        .shipping-note { font-size: 0.8rem; color: #689f38; margin-top: 5px; text-align: right; }

        .btn-submit {
            width: 100%; padding: 18px; border: none; border-radius: 15px;
            background: linear-gradient(to right, #2e7d32, #43a047);
            color: white; font-size: 1.2rem; font-weight: bold; cursor: pointer;
            margin-top: 20px; box-shadow: 0 6px 20px rgba(46, 125, 50, 0.2);
            transition: 0.3s;
        }
        .btn-submit:active { transform: translateY(2px); box-shadow: none; }

        #loader {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(255,255,255,0.9); display: none;
            flex-direction: column; justify-content: center; align-items: center; z-index: 1000;
        }
        .spinner { width: 40px; height: 40px; border: 4px solid #f3f3f3; border-top: 4px solid var(--primary-green); border-radius: 50%; animation: spin 1s linear infinite; }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
    </style>
</head>
<body>

<div class="app-container">
    <div class="header">
        <h1>恰口科研 Charco</h1>
        <p>優質生物製劑 ‧ 守護土地永續</p>
    </div>

    <div class="content">
        <div class="section-title">選擇產品</div>

        <div class="product-card">
            <div class="product-info">
                <span class="product-name">碳晶讚</span>
                <span class="product-tag">需冷藏</span>
            </div>
            <table>
                <tr><td>1 公升裝 ($1,000)</td><td align="right"><input type="number" min="0" value="0" class="qty" data-name="碳晶讚 1L" data-price="1000" data-vol="1"></td></tr>
                <tr><td>4 公升裝 ($3,800)</td><td align="right"><input type="number" min="0" value="0" class="qty" data-name="碳晶讚 4L" data-price="3800" data-vol="4"></td></tr>
                <tr><td>10 公升裝 ($9,500)</td><td align="right"><input type="number" min="0" value="0" class="qty" data-name="碳晶讚 10L" data-price="9500" data-vol="10"></td></tr>
            </table>
        </div>

        <div class="product-card">
            <div class="product-info"><span class="product-name">甲晶讚</span></div>
            <table>
                <tr><td>4 公升裝 ($600)</td><td align="right"><input type="number" min="0" value="0" class="qty" data-name="甲晶讚 4L" data-price="600" data-vol="4"></td></tr>
                <tr><td>10 公升裝 ($1,300)</td><td align="right"><input type="number" min="0" value="0" class="qty" data-name="甲晶讚 10L" data-price="1300" data-vol="10"></td></tr>
            </table>
        </div>

        <div class="product-card">
            <div class="product-info"><span class="product-name">展著劑</span></div>
            <table>
                <tr><td>4 公升裝 ($1,280)</td><td align="right"><input type="number" min="0" value="0" class="qty" data-name="展著劑 4L" data-price="1280" data-vol="4"></td></tr>
                <tr><td>10 公升裝 ($3,000)</td><td align="right"><input type="number" min="0" value="0" class="qty" data-name="展著劑 10L" data-price="3000" data-vol="10"></td></tr>
            </table>
        </div>

        <div class="section-title">收件人資訊</div>
        <div class="form-group">
            <label>姓名 *</label>
            <input type="text" id="name" placeholder="請輸入姓名">
        </div>
        <div class="form-group">
            <label>聯絡電話 *</label>
            <input type="tel" id="phone" placeholder="例如: 0912345678">
        </div>
        <div class="form-group">
            <label>配送地址 *</label>
            <input type="text" id="address" placeholder="請輸入收件地址">
        </div>
        <div class="form-group">
            <label>種植作物 *</label>
            <input type="text" id="crop" placeholder="請填寫目前種植的作物(如:芒果、草莓)">
        </div>
        <div class="form-group">
            <label>備註</label>
            <textarea id="note" rows="2" placeholder="如有其他特殊需求請告知"></textarea>
        </div>

        <div class="summary-box">
            <div class="summary-line"><span>總公升數</span><span id="display-vol">0 L</span></div>
            <div class="summary-line"><span>運費</span><span id="display-ship">$0</span></div>
            <div class="shipping-note">※ 滿 20 公升免運，未滿酌收 200 元</div>
            <div class="total-line"><span>總計</span><span id="display-total">$0</span></div>
        </div>

        <button class="btn-submit" onclick="submitOrder()">確認送出訂單</button>
    </div>
</div>

<div id="loader"><div class="spinner"></div><p>訂單傳送中，請稍候...</p></div>

<script>
    // 請將下方的 URL 替換為您部署 Apps Script 產生的 /exec 網址
    const scriptURL = 'https://script.google.com/macros/s/AKfycbzCr2KTpmmjDI9y0kGHDhRphQY2I1tN1wfsZGEkRBfBuo-Pu72Nd0MnN84prIq0pqJn/exec';

    function calculate() {
        let totalVal = 0, totalVol = 0, items = [];
        document.querySelectorAll('.qty').forEach(input => {
            let q = parseInt(input.value) || 0;
            if (q > 0) {
                totalVal += q * parseInt(input.dataset.price);
                totalVol += q * parseInt(input.dataset.vol);
                items.push(`${input.dataset.name} x ${q}`);
            }
        });

        let ship = (totalVol > 0 && totalVol < 20) ? 200 : 0;
        let finalTotal = totalVal + ship;

        document.getElementById('display-vol').innerText = `${totalVol} L`;
        document.getElementById('display-ship').innerText = `$${ship}`;
        document.getElementById('display-total').innerText = `$${finalTotal.toLocaleString()}`;

        return { items: items.join(', '), totalVol, ship, finalTotal };
    }

    document.querySelectorAll('input').forEach(el => el.addEventListener('input', calculate));

    async function submitOrder() {
        const order = calculate();
        const name = document.getElementById('name').value;
        const phone = document.getElementById('phone').value;
        const address = document.getElementById('address').value;
        const crop = document.getElementById('crop').value;

        if (order.finalTotal === 0 || !name || !phone || !address || !crop) {
            alert('請填寫完整訂購數量及收件人資訊(含作物名稱)！');
            return;
        }

        document.getElementById('loader').style.display = 'flex';

        const data = {
            "訂購時間": new Date().toLocaleString('zh-TW'),
            "姓名": name,
            "電話": phone,
            "地址": address,
            "種植作物": crop,
            "訂購明細": order.items,
            "總公升數": order.totalVol,
            "運費": order.ship,
            "總金額": order.finalTotal,
            "備註": document.getElementById('note').value
        };

        try {
            await fetch(scriptURL, {
                method: 'POST',
                mode: 'no-cors',
                body: JSON.stringify(data)
            });
            alert('訂單已成功送出！恰口科研將盡快連繫您。');
            location.reload();
        } catch (e) {
            alert('傳送發生錯誤，請檢查網址或連繫客服。');
            document.getElementById('loader').style.display = 'none';
        }
    }
</script>

</body>
</html>
