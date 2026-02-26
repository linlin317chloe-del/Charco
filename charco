
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>恰口科研 - 永續農法訂購系統</title>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-green: #2E7D32;
            --secondary-green: #81C784;
            --eco-beige: #F9FBF7;
            --text-dark: #37474F;
            --accent-orange: #FF8F00;
            --input-bg: #F0F4EF;
        }
        body {
            font-family: 'Noto Sans TC', sans-serif;
            background-color: var(--eco-beige);
            color: var(--text-dark);
            margin: 0; padding: 20px 15px;
            display: flex; justify-content: center;
        }
        .app-container {
            width: 100%; max-width: 550px;
            background: #ffffff;
            border-radius: 32px; /* 更圓潤的容器 */
            box-shadow: 0 15px 40px rgba(46, 125, 50, 0.08);
            overflow: hidden;
            border: 1px solid rgba(46, 125, 50, 0.1);
        }
        .header {
            background: linear-gradient(135deg, var(--primary-green), var(--secondary-green));
            color: white; padding: 40px 20px; text-align: center;
        }
        .header h1 { margin: 0; font-size: 1.7rem; letter-spacing: 2px; }
        .header p { margin: 8px 0 0; opacity: 0.9; font-size: 0.95rem; font-weight: 300; }

        .content { padding: 25px; }
        .section-title {
            font-size: 1.2rem; font-weight: bold; color: var(--primary-green);
            margin: 30px 0 15px; display: flex; align-items: center;
        }
        .section-title::after { 
            content: ''; flex: 1; height: 1px; background: #eee; margin-left: 15px;
        }

        /* 產品卡片 */
        .product-card {
            background: #fff; border: 1.5px solid #F0F4EF; border-radius: 24px;
            padding: 20px; margin-bottom: 20px; transition: 0.3s ease;
        }
        .product-card:hover { border-color: var(--secondary-green); transform: translateY(-2px); }
        .product-name { font-weight: bold; font-size: 1.15rem; color: #1b5e20; display: block; margin-bottom: 12px;}
        .product-tag { font-size: 0.75rem; background: #FFF3E0; color: #E65100; padding: 3px 10px; border-radius: 10px; margin-left: 8px; vertical-align: middle;}
        
        table { width: 100%; border-collapse: separate; border-spacing: 0 10px; }
        td { padding: 5px 0; font-size: 1rem; vertical-align: middle;}
        
        /* 圓潤填寫框設計 */
        .qty-input {
            width: 70px; padding: 10px; border-radius: 18px; /* 膠囊形 */
            border: 2px solid var(--input-bg); background: var(--input-bg);
            text-align: center; font-size: 1rem; outline: none; transition: 0.3s;
            font-weight: bold; color: var(--primary-green);
        }
        .qty-input:focus { 
            border-color: var(--secondary-green); background: #fff;
            box-shadow: 0 0 10px rgba(129, 199, 132, 0.2);
        }

        /* 表單欄位 */
        .form-group { margin-bottom: 18px; }
        .form-group label { display: block; margin-bottom: 8px; font-weight: bold; font-size: 0.95rem; color: #546E7A;}
        .form-group input, .form-group textarea {
            width: 100%; padding: 14px 18px; border: 2px solid var(--input-bg); 
            border-radius: 20px; box-sizing: border-box; font-size: 1rem;
            background: var(--input-bg); transition: 0.3s;
        }
        .form-group input:focus, .form-group textarea:focus {
            border-color: var(--secondary-green); background: #fff; outline: none;
        }

        /* 結帳與運費提示區 */
        .summary-box {
            background: linear-gradient(to bottom, #f9fbf7, #f1f8e9);
            border-radius: 28px; padding: 25px; margin-top: 35px;
        }
        .shipping-policy {
            background: #fff; color: var(--primary-green);
            padding: 12px 15px; border-radius: 18px; 
            font-size: 0.9rem; font-weight: bold; margin-bottom: 20px;
            display: flex; align-items: center; box-shadow: 0 4px 10px rgba(0,0,0,0.03);
        }
        .summary-line { display: flex; justify-content: space-between; margin-bottom: 10px; color: #607D8B; font-size: 0.95rem; }
        .total-line { 
            display: flex; justify-content: space-between; margin-top: 20px; padding-top: 15px;
            border-top: 2px dashed #dcedc8; font-size: 1.5rem; font-weight: bold; color: var(--accent-orange);
        }

        .btn-submit {
            width: 100%; padding: 20px; border: none; border-radius: 25px;
            background: linear-gradient(135deg, #2e7d32, #43a047);
            color: white; font-size: 1.25rem; font-weight: bold; cursor: pointer;
            margin-top: 25px; box-shadow: 0 8px 25px rgba(46, 125, 50, 0.25);
            transition: 0.4s ease;
        }
        .btn-submit:hover { transform: translateY(-3px); box-shadow: 0 12px 30px rgba(46, 125, 50, 0.35); }

        #loader {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(255,255,255,0.9); display: none;
            flex-direction: column; justify-content: center; align-items: center; z-index: 1000;
        }
        .spinner { width: 45px; height: 45px; border: 5px solid #f3f3f3; border-top: 5px solid var(--primary-green); border-radius: 50%; animation: spin 1s linear infinite; }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
    </style>
</head>
<body>

<div class="app-container">
    <div class="header">
        <h1>恰口科研 Charco</h1>
        <p>優質生物製劑 ‧ 永續大地守護者</p>
    </div>

    <div class="content">
        <div class="section-title">產品選購</div>

        <div class="product-card">
            <span class="product-name">碳晶讚<span class="product-tag">❄️ 需冷藏</span></span>
            <table>
                <tr><td>1 公升裝 ($1,000)</td><td align="right"><input type="number" min="0" placeholder="0" class="qty-input" data-name="碳晶讚 1L" data-price="1000" data-vol="1"></td></tr>
                <tr><td>4 公升裝 ($3,800)</td><td align="right"><input type="number" min="0" placeholder="0" class="qty-input" data-name="碳晶讚 4L" data-price="3800" data-vol="4"></td></tr>
                <tr><td>10 公升裝 ($9,500)</td><td align="right"><input type="number" min="0" placeholder="0" class="qty-input" data-name="碳晶讚 10L" data-price="9500" data-vol="10"></td></tr>
            </table>
        </div>

        <div class="product-card">
            <span class="product-name">甲晶讚</span>
            <table>
                <tr><td>4 公升裝 ($600)</td><td align="right"><input type="number" min="0" placeholder="0" class="qty-input" data-name="甲晶讚 4L" data-price="600" data-vol="4"></td></tr>
                <tr><td>10 公升裝 ($1,300)</td><td align="right"><input type="number" min="0" placeholder="0" class="qty-input" data-name="甲晶讚 10L" data-price="1300" data-vol="10"></td></tr>
            </table>
        </div>

        <div class="product-card">
            <span class="product-name">展著劑</span>
            <table>
                <tr><td>4 公升裝 ($1,280)</td><td align="right"><input type="number" min="0" placeholder="0" class="qty-input" data-name="展著劑 4L" data-price="1280" data-vol="4"></td></tr>
                <tr><td>10 公升裝 ($3,000)</td><td align="right"><input type="number" min="0" placeholder="0" class="qty-input" data-name="展著劑 10L" data-price="3000" data-vol="10"></td></tr>
            </table>
        </div>

        <div class="section-title">收件資訊</div>
        <div class="form-group"><label>收件姓名 *</label><input type="text" id="name" placeholder="請填寫姓名"></div>
        <div class="form-group"><label>聯絡電話 *</label><input type="tel" id="phone" placeholder="填寫手機或市話"></div>
        <div class="form-group"><label>配送地址 *</label><input type="text" id="address" placeholder="完整收件地址"></div>
        <div class="form-group"><label>種植作物 *</label><input type="text" id="crop" placeholder="填寫目前種植作物 (如：鳳梨、芒果)"></div>
        <div class="form-group"><label>其他備註</label><textarea id="note" rows="2" placeholder="如有特殊需求請在此說明"></textarea></div>

        <div class="summary-box">
            <div class="shipping-policy">
                💡 備註：運費 200 元，滿 20 公升以上免運
            </div>
            <div class="summary-line"><span>總公升數累積</span><span id="display-vol" style="font-weight:bold; color:var(--primary-green);">0 L</span></div>
            <div class="summary-line"><span>系統預估運費</span><span id="display-ship">$0</span></div>
            <div class="total-line"><span>訂單總金額</span><span id="display-total">$0</span></div>
        </div>

        <button class="btn-submit" onclick="submitOrder()">確認送出訂單</button>
    </div>
</div>

<div id="loader"><div class="spinner"></div><p style="color:var(--primary-green); font-weight:bold; margin-top:15px;">訂單建立中...</p></div>

<script>
    // 請務必更新下方的 Apps Script URL
    const scriptURL = 'https://script.google.com/macros/s/AKfycbzCr2KTpmmjDI9y0kGHDhRphQY2I1tN1wfsZGEkRBfBuo-Pu72Nd0MnN84prIq0pqJn/exec';

    function calculate() {
        let totalVal = 0, totalVol = 0, items = [];
        document.querySelectorAll('.qty-input').forEach(input => {
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
            alert('請至少填寫一項商品數量，並輸入完整收件人資訊與作物！');
            return;
        }

        document.getElementById('loader').style.display = 'flex';

        const data = {
            "訂購時間": new Date().toLocaleString('zh-TW'),
            "姓名": name, "電話": phone, "地址": address, "種植作物": crop,
            "訂購明細": order.items, "總公升數": order.totalVol, "運費": order.ship, "總金額": order.finalTotal,
            "備註": document.getElementById('note').value
        };

        try {
            await fetch(scriptURL, { method: 'POST', mode: 'no-cors', body: JSON.stringify(data) });
            alert('謝謝訂購，訂單已成功送出！稍待提供【訂單明細】及【匯款資料】給您確認，謝謝您→恰口科研感謝您的支持 。');
            location.reload();
        } catch (e) {
            alert('連線失敗，請檢查網址設定或網路狀態。');
            document.getElementById('loader').style.display = 'none';
        }
    }
</script>
</body>
</html>
