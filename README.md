<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>恰口科研 - 生物製劑訂購系統</title>
    <style>
        :root {
            --primary-green: #2E7D32;
            --secondary-green: #81C784;
            --eco-beige: #F1F8E9;
            --text-dark: #37474F;
            --accent-red: #D32F2F;
        }
        body { font-family: sans-serif; background-color: var(--eco-beige); color: var(--text-dark); margin: 0; padding: 20px 10px; }
        .container { max-width: 800px; margin: 0 auto; background: #fff; padding: 25px; border-radius: 16px; box-shadow: 0 8px 20px rgba(46, 125, 50, 0.15); border-top: 5px solid var(--primary-green); }
        h1 { text-align: center; color: var(--primary-green); margin-bottom: 5px; }
        h2 { text-align: center; font-size: 1.1rem; font-weight: normal; margin-top: 0; padding-bottom: 15px; border-bottom: 1px solid #eee; }
        .product-card { border-radius: 12px; padding: 15px; margin-bottom: 20px; background: #fff; border-left: 4px solid var(--secondary-green); box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
        .product-title { font-size: 1.3em; font-weight: bold; color: var(--primary-green); }
        .warning { color: var(--accent-red); font-weight: bold; font-size: 0.85em; }
        table { width: 100%; border-collapse: collapse; margin-top: 10px; }
        th { background: var(--primary-green); color: white; padding: 8px; text-align: left; }
        td { padding: 10px; border-bottom: 1px solid #eee; }
        input[type="number"] { width: 50px; padding: 5px; border-radius: 10px; border: 1px solid #ccc; text-align: center; }
        .form-group { margin-bottom: 15px; }
        .form-group label { display: block; font-weight: bold; color: var(--primary-green); margin-bottom: 5px; }
        .form-group input, .form-group textarea { width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 8px; box-sizing: border-box; }
        .summary-box { background: #fdfdfd; border: 2px solid var(--secondary-green); padding: 15px; border-radius: 12px; margin-top: 20px; }
        .btn-submit { display: block; width: 100%; padding: 15px; background: var(--primary-green); color: white; font-size: 1.2em; font-weight: bold; border: none; border-radius: 30px; cursor: pointer; margin-top: 20px; }
        #loading { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(255,255,255,0.8); display: none; justify-content: center; align-items: center; z-index: 100; }
    </style>
</head>
<body>

<div class="container">
    <h1>恰口科研股份有限公司</h1>
    <h2>生物製劑購買表單 (Web App)</h2>

    <div class="product-card">
        <div class="product-title">碳晶讚</div>
        <div class="warning">⚠️ 此產品需要冷藏保存</div>
        <table>
            <tr><th>規格</th><th>單價</th><th>數量</th></tr>
            <tr><td>1公升</td><td>$1000</td><td><input type="number" min="0" value="0" class="item-qty" data-name="碳晶讚 1L" data-price="1000" data-vol="1"></td></tr>
            <tr><td>4公升</td><td>$3800</td><td><input type="number" min="0" value="0" class="item-qty" data-name="碳晶讚 4L" data-price="3800" data-vol="4"></td></tr>
            <tr><td>10公升</td><td>$9500</td><td><input type="number" min="0" value="0" class="item-qty" data-name="碳晶讚 10L" data-price="9500" data-vol="10"></td></tr>
        </table>
    </div>

    <div class="product-card">
        <div class="product-title">甲晶讚</div>
        <table>
            <tr><th>規格</th><th>單價</th><th>數量</th></tr>
            <tr><td>4公升</td><td>$600</td><td><input type="number" min="0" value="0" class="item-qty" data-name="甲晶讚 4L" data-price="600" data-vol="4"></td></tr>
            <tr><td>10公升</td><td>$1300</td><td><input type="number" min="0" value="0" class="item-qty" data-name="甲晶讚 10L" data-price="1300" data-vol="10"></td></tr>
        </table>
    </div>

    <div class="product-card">
        <div class="product-title">展著劑</div>
        <table>
            <tr><th>規格</th><th>單價</th><th>數量</th></tr>
            <tr><td>4公升</td><td>$1280</td><td><input type="number" min="0" value="0" class="item-qty" data-name="展著劑 4L" data-price="1280" data-vol="4"></td></tr>
            <tr><td>10公升</td><td>$3000</td><td><input type="number" min="0" value="0" class="item-qty" data-name="展著劑 10L" data-price="3000" data-vol="10"></td></tr>
        </table>
    </div>

    <div class="form-group">
        <label>姓名 *</label>
        <input type="text" id="name" required>
    </div>
    <div class="form-group">
        <label>聯絡電話 *</label>
        <input type="tel" id="phone" required>
    </div>
    <div class="form-group">
        <label>收件地址 *</label>
        <input type="text" id="address" required>
    </div>
    <div class="form-group">
        <label>種植作物 *</label>
        <input type="text" id="crop" placeholder="例如：芒果、草莓" required>
    </div>
    <div class="form-group">
        <label>備註事項</label>
        <textarea id="notes" rows="2"></textarea>
    </div>

    <div class="summary-box">
        <div id="summary-text" style="white-space: pre-wrap; font-size: 0.9rem;">請選擇商品...</div>
        <div style="text-align: right; margin-top: 10px; font-weight: bold; color: var(--accent-red);">
            總公升：<span id="vol">0</span> L / 運費：$<span id="ship">0</span><br>
            <span style="font-size: 1.4em;">總計：$<span id="total">0</span></span>
        </div>
    </div>

    <button class="btn-submit" onclick="sendOrder()">確認送出訂單</button>
</div>

<div id="loading">傳送中...</div>

<script>
    const scriptURL = '請在這裡貼上您的Google腳本網址'; 

    function update() {
        let subtotal = 0, vol = 0, items = [];
        document.querySelectorAll('.item-qty').forEach(i => {
            let q = parseInt(i.value) || 0;
            if (q > 0) {
                subtotal += i.dataset.price * q;
                vol += i.dataset.vol * q;
                items.push(`${i.dataset.name} x ${q}`);
            }
        });
        let ship = (vol > 0 && vol < 20) ? 200 : 0;
        document.getElementById('vol').innerText = vol;
        document.getElementById('ship').innerText = ship;
        document.getElementById('total').innerText = (subtotal + ship).toLocaleString();
        
        let info = `【訂購明細】\n${items.join('\n') || '未選購'}\n\n【收件資訊】\n姓名：${document.getElementById('name').value}\n電話：${document.getElementById('phone').value}\n作物：${document.getElementById('crop').value}`;
        document.getElementById('summary-text').innerText = info;
        return { items, vol, ship, total: subtotal + ship };
    }

    document.querySelectorAll('input, textarea').forEach(el => el.addEventListener('input', update));

    function sendOrder() {
        let res = update();
        if (res.total === 0 || !document.getElementById('name').value || !document.getElementById('crop').value) {
            alert("請完整填寫資料與作物名稱！"); return;
        }
        document.getElementById('loading').style.display = 'flex';
        
        fetch(scriptURL, {
            method: 'POST',
            mode: 'no-cors',
            body: JSON.stringify({
                "訂購時間": new Date().toLocaleString(),
                "姓名": document.getElementById('name').value,
                "電話": document.getElementById('phone').value,
                "地址": document.getElementById('address').value,
                "種植作物": document.getElementById('crop').value,
                "訂購明細": res.items.join(', '),
                "總公升數": res.vol,
                "運費": res.ship,
                "總金額": res.total,
                "備註": document.getElementById('notes').value
            })
        }).then(() => {
            alert("訂單送出成功！");
            location.reload();
        }).catch(() => {
            alert("送出失敗，請檢查網址設定。");
            document.getElementById('loading').style.display = 'none';
        });
    }
</script>
</body>
</html>
