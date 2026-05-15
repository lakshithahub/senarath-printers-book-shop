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
            background-color: #1e293b
