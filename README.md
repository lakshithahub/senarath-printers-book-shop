<!DOCTYPE html>
<html lang='en'>
<head>
    <meta charset='utf-8'>
    <meta name='viewport' content='width=device-width, initial-scale=1'>
    <title>Stock Inventory - Lakshitha POS (Dark Mode)</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            /* Dark Theme Colors */
            --primary: #2ecc71;
            --dark-bg: #0f172a; /* Deep blue-black */
            --card-bg: #1e293b; /* Slate blue-gray */
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --accent: #f1c40f;
            --danger: #ff4757;
            --border: #334155;
            --input-bg: #0f172a;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Inter', sans-serif; }
        
        body { 
            background-color: var(--dark-bg); 
            color: var(--text-main); 
            padding-bottom: 50px; 
        }

        /* Navbar */
        .navbar {
            display: flex; justify-content: space-between; align-items: center;
            background-color: var(--card-bg); padding: 15px 5%; color: white;
            position: sticky; top: 0; z-index: 1000; 
            border-bottom: 1px solid var(--border);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.3);
        }
        .nav-links { list-style: none; display: flex; gap: 20px; }
        .nav-links a { color: var(--text-muted); text-decoration: none; font-size: 14px; font-weight: 600; transition: 0.3s; }
        .nav-links a:hover { color: var(--primary); }

        /* Floating Logo */
        .logo-container { position: fixed; bottom: 30px; right: 30px; z-index: 999; }
        .floating-logo {
            width: 80px; height: 80px; 
            background: var(--card-bg);
            border: 4px solid var(--primary); border-radius: 50%;
            display: flex; align-items: center; justify-content: center;
            box-shadow: 0 10px 25px rgba(0,0,0,0.5);
            animation: bounce 3s ease-in-out infinite;
        }
        @keyframes bounce { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-10px); } }

        /* Main Content */
        .header-section { text-align: center; padding: 40px 20px; }
        .title-text { color: var(--text-main); font-size: 32px; font-weight: 800; letter-spacing: -1px; }
        
        .inventory-container { max-width: 1000px; margin: 0 auto; padding: 0 20px; }
        
        .action-card { 
            background: var(--card-bg); padding: 25px; border-radius: 16px; 
            border: 1px solid var(--border);
            margin-bottom: 30px;
        }

        .input-grid { 
            display: grid; grid-template-columns: 2fr 1fr 1fr auto; gap: 12px; 
        }

        input { 
            padding: 14px; 
            background-color: var(--input-bg);
            border: 2px solid var(--border); 
            color: var(--text-main);
            border-radius: 10px; 
            outline: none; font-size: 15px; transition: 0.3s;
        }
        input:focus { border-color: var(--primary); }
        input::placeholder { color: #475569; }

        .add-btn { 
            background: var(--primary); color: white; border: none; 
            padding: 0 25px; border-radius: 10px; cursor: pointer; 
            font-weight: 700; transition: 0.3s;
        }
        .add-btn:hover { background: #27ae60; transform: translateY(-2px); }

        /* Search Box */
        .search-box { margin-bottom: 15px; width: 100%; position: relative; }
        .search-box input { width: 100%; padding-left: 20px; background: var(--card-bg); }

        /* Table Design */
        .table-wrapper { 
            background: var(--card-bg); border-radius: 16px; overflow: hidden; 
            border: 1px solid var(--border);
        }
        .stocktable { width: 100%; border-collapse: collapse; }
        .stocktable th { 
            background-color: #1e293b; color: var(--text-muted); 
            padding: 18px; text-align: left; font-size: 13px; 
            text-transform: uppercase; border-bottom: 1px solid var(--border);
        }
        .stocktable td { 
            padding: 18px; border-bottom: 1px solid var(--border); 
            font-size: 15px; color: var(--text-main);
        }
        
        .qty-badge {
            padding: 5px 12px; border-radius: 20px; font-weight: 700; font-size: 14px;
        }
        .qty-low { background: #451a1a; color: #f87171; }
        .qty-ok { background: #064e3b; color: #34d399; }

        .del-btn { 
            color: var(--danger); background: none; border: 1px solid #451a1a; 
            padding: 6px 12px; border-radius: 6px; cursor: pointer; font-size: 12px; transition: 0.3s;
        }
        .del-btn:hover { background: var(--danger); color: white; }

        .btn-print { 
            background: var(--primary); color: white; border: none; 
            padding: 15px; border-radius: 12px; cursor: pointer; 
            width: 100%; font-weight: 600; margin-top: 20px; transition: 0.3s;
        }
        .btn-print:hover { filter: brightness(1.1); }

        /* Print Style */
        @media print {
            .navbar, .logo-container, .action-card, .del-btn, .btn-print, .search-box { display: none !important; }
            body { background: white; color: black; }
            .table-wrapper { border: 1px solid #000; }
            .stocktable th { color: black; background: #eee; }
            .stocktable td { color: black; }
        }
    </style>
</head>
<body>

    <nav class="navbar">
        <div style="font-weight: 800; color: var(--primary); letter-spacing: 1px;">LAKSHITHA POS</div>
        <ul class="nav-links">
            <li><a href="udara{sell inter fase}.html">SELL PAGE</a></li>
            <li><a href="#" onclick="location.reload()">REFRESH</a></li>
        </ul>
    </nav>

    <div class="logo-container">
        <div class="floating-logo">
            <img src="file:///C:/LAKSHITHA/test%20one/UDARA[LOGO].jpeg" alt="Logo" style="width: 80%; height: 80%; border-radius: 50%; object-fit: cover;">
        </div>
    </div>

    <div class="header-section">
        <h1 class="title-text">Stock Inventory</h1>
        <p style="color: var(--text-muted); margin-top: 8px;">Date: <span id="currentDate"></span></p>
    </div>

    <div class="inventory-container">
        <div class="action-card">
            <div class="input-grid">
                <input type="text" id="itemName" placeholder="Item Name (බඩුවේ නම)" onkeydown="if(event.key==='Enter') document.getElementById('itemPrice').focus()">
                <input type="number" id="itemPrice" placeholder="Price (Rs.)" onkeydown="if(event.key==='Enter') document.getElementById('itemQty').focus()">
                <input type="number" id="itemQty" placeholder="Qty" onkeydown="if(event.key==='Enter') updateStock()">
                <button class="add-btn" onclick="updateStock()">Update Stock</button>
            </div>
        </div>

        <div class="search-box">
            <input type="text" id="searchInput" placeholder="Search items... (බඩු සොයන්න)" onkeyup="renderStock()">
        </div>

        <div class="table-wrapper">
            <table class="stocktable">
                <thead>
                    <tr>
                        <th>Item Description</th>
                        <th>Price (Rs.)</th>
                        <th>Availability</th>
                        <th style="text-align: center;">Action</th>
                    </tr>
                </thead>
                <tbody id="stockBody"></tbody>
            </table>
        </div>

        <button class="btn-print" onclick="window.print()">🖨️ GENERATE PDF REPORT</button>
    </div>

    <script>
        const STOCK_KEY = 'inventory_stock';

        window.onload = function() {
            document.getElementById('currentDate').innerText = new Date().toLocaleDateString('en-GB');
            renderStock();
        };

        function updateStock() {
            let name = document.getElementById('itemName').value.trim();
            let price = parseFloat(document.getElementById('itemPrice').value);
            let qty = parseInt(document.getElementById('itemQty').value);

            if (!name || isNaN(price) || isNaN(qty)) {
                alert("කරුණාකර සියලු විස්තර නිවැරදිව ඇතුළත් කරන්න.");
                return;
            }

            let stock = JSON.parse(localStorage.getItem(STOCK_KEY)) || [];
            let existingItem = stock.find(item => item.name.toLowerCase() === name.toLowerCase());

            if (existingItem) {
                existingItem.qty += qty;
                existingItem.price = price;
            } else {
                stock.push({ name, price, qty });
            }

            localStorage.setItem(STOCK_KEY, JSON.stringify(stock));
            renderStock();
            
            ['itemName', 'itemPrice', 'itemQty'].forEach(id => document.getElementById(id).value = "");
            document.getElementById('itemName').focus();
        }

        function deleteItem(index) {
            if (confirm("මෙම බඩුව ලැයිස්තුවෙන් ඉවත් කරන්නද?")) {
                let stock = JSON.parse(localStorage.getItem(STOCK_KEY)) || [];
                stock.splice(index, 1);
                localStorage.setItem(STOCK_KEY, JSON.stringify(stock));
                renderStock();
            }
        }

        function renderStock() {
            let stock = JSON.parse(localStorage.getItem(STOCK_KEY)) || [];
            let searchTerm = document.getElementById('searchInput').value.toLowerCase();
            let tableBody = document.getElementById('stockBody');
            tableBody.innerHTML = "";

            let filteredStock = stock.filter(item => item.name.toLowerCase().includes(searchTerm));

            filteredStock.forEach((item, index) => {
                let qtyClass = item.qty <= 5 ? 'qty-low' : 'qty-ok';
                let statusText = item.qty <= 5 ? 'Low Stock' : 'In Stock';

                tableBody.insertAdjacentHTML('beforeend', `
                    <tr>
                        <td style="font-weight: 600;">${item.name}</td>
                        <td style="color: var(--text-muted);">${item.price.toLocaleString('en-LK', {minimumFractionDigits: 2})}</td>
                        <td>
                            <span class="qty-badge ${qtyClass}">${item.qty}</span>
                            <small style="display:block; font-size:10px; margin-top:4px; color:var(--text-muted)">${statusText}</small>
                        </td>
                        <td style="text-align: center;">
                            <button class="del-btn" onclick="deleteItem(${index})">Remove</button>
                        </td>
                    </tr>
                `);
            });
        }
    </script>
</body>
</html>
