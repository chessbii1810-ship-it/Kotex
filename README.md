<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trademate · pro trading dashboard</title>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <!-- Google Fonts: Inter + JetBrains Mono for numbers -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,400;14..32,500;14..32,600;14..32,700&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', sans-serif;
            background: #0b0e14;
            color: #e8edf5;
            line-height: 1.5;
            overflow-x: hidden;
            padding: 16px;
        }

        :root {
            --bg-deep: #0b0e14;
            --bg-panel: #131a24;
            --bg-panel-elevated: #1a232f;
            --border-subtle: #222e3c;
            --border-light: #2d3a4a;
            --text-bright: #f0f4fc;
            --text-soft: #8b9bb0;
            --text-dim: #5c6f85;
            --green: #0ecb81;
            --green-soft: rgba(14, 203, 129, 0.12);
            --red: #f6465d;
            --red-soft: rgba(246, 70, 93, 0.12);
            --blue: #2f80ed;
            --blue-soft: rgba(47, 128, 237, 0.12);
            --yellow: #f0b90b;
            --card-shadow: 0 15px 35px -10px rgba(0, 0, 0, 0.6);
            --transition: all 0.12s ease;
        }

        /* subtle scrollbar */
        ::-webkit-scrollbar {
            width: 5px;
            height: 5px;
        }

        ::-webkit-scrollbar-track {
            background: var(--bg-deep);
        }

        ::-webkit-scrollbar-thumb {
            background: var(--border-light);
            border-radius: 10px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: #3e4d60;
        }

        .app {
            max-width: 1600px;
            margin: 0 auto;
        }

        /* header / top bar */
        .top-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 20px;
            background: var(--bg-panel);
            border: 1px solid var(--border-subtle);
            border-radius: 18px;
            margin-bottom: 16px;
            backdrop-filter: blur(8px);
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.3);
        }

        .logo-area {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .logo-icon {
            background: linear-gradient(135deg, #0ecb81, #2f80ed);
            width: 34px;
            height: 34px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.1rem;
            color: #fff;
        }

        .logo-text {
            font-weight: 700;
            font-size: 1.25rem;
            letter-spacing: -0.02em;
            color: var(--text-bright);
        }

        .logo-text span {
            color: var(--green);
            font-weight: 600;
        }

        .market-pulse {
            display: flex;
            gap: 28px;
            align-items: center;
            background: var(--bg-deep);
            padding: 6px 22px;
            border-radius: 60px;
            border: 1px solid var(--border-subtle);
        }

        .pulse-item {
            display: flex;
            align-items: baseline;
            gap: 8px;
            font-size: 0.85rem;
        }

        .pulse-label {
            color: var(--text-dim);
            font-weight: 500;
            font-size: 0.75rem;
            text-transform: uppercase;
            letter-spacing: 0.03em;
        }

        .pulse-value {
            font-family: 'JetBrains Mono', monospace;
            font-weight: 600;
            color: var(--text-bright);
        }

        .pulse-change {
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.75rem;
            font-weight: 600;
        }

        .positive {
            color: var(--green);
        }

        .negative {
            color: var(--red);
        }

        .user-actions {
            display: flex;
            align-items: center;
            gap: 16px;
        }

        .balance-chip {
            background: var(--bg-deep);
            padding: 6px 16px;
            border-radius: 40px;
            border: 1px solid var(--border-subtle);
            font-family: 'JetBrains Mono', monospace;
            font-weight: 600;
            font-size: 0.9rem;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .balance-chip i {
            color: var(--yellow);
            font-size: 0.9rem;
        }

        .avatar {
            width: 40px;
            height: 40px;
            border-radius: 12px;
            background: linear-gradient(145deg, #1e2c3c, #0f1822);
            border: 1px solid var(--border-light);
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 600;
            font-size: 0.9rem;
            color: var(--text-bright);
            cursor: default;
        }

        /* main grid */
        .dashboard-grid {
            display: grid;
            grid-template-columns: 1fr 320px;
            gap: 16px;
            margin-bottom: 16px;
        }

        /* panels */
        .panel {
            background: var(--bg-panel);
            border: 1px solid var(--border-subtle);
            border-radius: 20px;
            padding: 20px;
            box-shadow: var(--card-shadow);
        }

        .panel-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 18px;
        }

        .panel-title {
            font-weight: 600;
            font-size: 1.1rem;
            letter-spacing: -0.01em;
            color: var(--text-bright);
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .panel-title i {
            color: var(--blue);
            font-size: 1rem;
        }

        .timeframe {
            display: flex;
            gap: 4px;
            background: var(--bg-deep);
            padding: 4px;
            border-radius: 30px;
            border: 1px solid var(--border-subtle);
        }

        .timeframe span {
            padding: 5px 14px;
            font-size: 0.75rem;
            font-weight: 600;
            border-radius: 30px;
            color: var(--text-dim);
            cursor: default;
            transition: var(--transition);
        }

        .timeframe span.active {
            background: var(--border-light);
            color: var(--text-bright);
        }

        /* main chart */
        .chart-container {
            height: 240px;
            width: 100%;
            position: relative;
            margin-bottom: 8px;
        }

        .chart-svg {
            width: 100%;
            height: 100%;
            display: block;
        }

        .chart-tooltip {
            position: absolute;
            background: var(--bg-panel-elevated);
            border: 1px solid var(--border-light);
            padding: 8px 12px;
            border-radius: 10px;
            font-size: 0.8rem;
            font-family: 'JetBrains Mono', monospace;
            pointer-events: none;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.5);
            opacity: 0;
            transition: opacity 0.1s;
            white-space: nowrap;
            color: var(--text-bright);
            z-index: 10;
        }

        .chart-legend {
            display: flex;
            gap: 24px;
            font-size: 0.8rem;
            color: var(--text-soft);
            margin-top: 10px;
            padding-top: 10px;
            border-top: 1px solid var(--border-subtle);
        }

        .legend-item {
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .legend-color {
            width: 10px;
            height: 10px;
            border-radius: 3px;
        }

        /* order book + trades row */
        .dual-panel {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 16px;
        }

        .order-book-list {
            display: flex;
            flex-direction: column;
            gap: 6px;
        }

        .order-row {
            display: flex;
            justify-content: space-between;
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.8rem;
            padding: 4px 8px;
            border-radius: 6px;
            background: rgba(255, 255, 255, 0.01);
        }

        .order-row.bid .price {
            color: var(--green);
        }

        .order-row.ask .price {
            color: var(--red);
        }

        .order-row .amount {
            color: var(--text-soft);
        }

        .depth-bar {
            height: 4px;
            border-radius: 4px;
            margin-top: 4px;
            background: var(--border-light);
            overflow: hidden;
        }

        .depth-fill {
            height: 100%;
            border-radius: 4px;
        }

        /* market table */
        .market-table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.85rem;
        }

        .market-table th {
            text-align: left;
            color: var(--text-dim);
            font-weight: 500;
            font-size: 0.7rem;
            text-transform: uppercase;
            letter-spacing: 0.05em;
            padding-bottom: 12px;
            border-bottom: 1px solid var(--border-subtle);
        }

        .market-table td {
            padding: 10px 0;
            border-bottom: 1px solid var(--border-subtle);
            font-family: 'JetBrains Mono', monospace;
        }

        .market-table tr:last-child td {
            border-bottom: none;
        }

        .market-table .pair {
            font-family: 'Inter', sans-serif;
            font-weight: 600;
            color: var(--text-bright);
        }

        .market-table .pair span {
            font-weight: 400;
            color: var(--text-dim);
            font-size: 0.75rem;
        }

        /* trade panel (right column) */
        .trade-panel {
            display: flex;
            flex-direction: column;
            gap: 16px;
        }

        .trade-tabs {
            display: flex;
            gap: 8px;
            background: var(--bg-deep);
            padding: 4px;
            border-radius: 40px;
            border: 1px solid var(--border-subtle);
        }

        .trade-tab {
            flex: 1;
            text-align: center;
            padding: 8px;
            font-size: 0.85rem;
            font-weight: 600;
            border-radius: 30px;
            color: var(--text-dim);
            cursor: default;
            transition: var(--transition);
        }

        .trade-tab.active {
            background: var(--border-light);
            color: var(--text-bright);
        }

        .trade-form {
            display: flex;
            flex-direction: column;
            gap: 14px;
        }

        .input-group {
            display: flex;
            flex-direction: column;
            gap: 4px;
        }

        .input-group label {
            font-size: 0.7rem;
            font-weight: 600;
            color: var(--text-dim);
            text-transform: uppercase;
            letter-spacing: 0.05em;
        }

        .input-wrapper {
            display: flex;
            align-items: center;
            background: var(--bg-deep);
            border: 1px solid var(--border-subtle);
            border-radius: 12px;
            padding: 0 12px;
            transition: var(--transition);
        }

        .input-wrapper:focus-within {
            border-color: var(--blue);
        }

        .input-wrapper input {
            background: transparent;
            border: none;
            padding: 12px 0;
            width: 100%;
            color: var(--text-bright);
            font-family: 'JetBrains Mono', monospace;
            font-size: 1rem;
            outline: none;
        }

        .input-wrapper span {
            color: var(--text-dim);
            font-size: 0.8rem;
            font-weight: 500;
        }

        .quick-percent {
            display: flex;
            gap: 8px;
            margin-top: 4px;
        }

        .quick-percent span {
            background: var(--bg-deep);
            border: 1px solid var(--border-subtle);
            padding: 4px 12px;
            border-radius: 30px;
            font-size: 0.7rem;
            font-weight: 600;
            color: var(--text-soft);
            cursor: default;
            transition: var(--transition);
        }

        .quick-percent span:hover {
            border-color: var(--blue);
            color: var(--text-bright);
        }

        .trade-info {
            display: flex;
            justify-content: space-between;
            font-size: 0.8rem;
            color: var(--text-soft);
            padding: 8px 0;
            border-top: 1px solid var(--border-subtle);
            border-bottom: 1px solid var(--border-subtle);
        }

        .trade-info .value {
            font-family: 'JetBrains Mono', monospace;
            color: var(--text-bright);
        }

        .btn {
            padding: 14px;
            border-radius: 14px;
            border: none;
            font-weight: 700;
            font-size: 0.9rem;
            cursor: default;
            transition: var(--transition);
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            letter-spacing: 0.01em;
        }

        .btn-buy {
            background: var(--green);
            color: #04110b;
        }

        .btn-buy:hover {
            background: #0daf6c;
        }

        .btn-sell {
            background: var(--red);
            color: white;
        }

        .btn-sell:hover {
            background: #e03a50;
        }

        /* positions */
        .positions-list {
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        .position-item {
            display: grid;
            grid-template-columns: 2fr 1.5fr 1fr 1fr;
            gap: 8px;
            font-size: 0.8rem;
            font-family: 'JetBrains Mono', monospace;
            padding: 8px 0;
            border-bottom: 1px solid var(--border-subtle);
        }

        .position-item.header {
            color: var(--text-dim);
            font-family: 'Inter', sans-serif;
            font-size: 0.7rem;
            text-transform: uppercase;
            font-weight: 500;
            letter-spacing: 0.05em;
            border-bottom: 1px solid var(--border-subtle);
            padding-bottom: 10px;
        }

        .position-item .pair {
            font-weight: 600;
            color: var(--text-bright);
        }

        .position-item .pnl {
            font-weight: 600;
        }

        /* responsive */
        @media (max-width: 1100px) {
            .dashboard-grid {
                grid-template-columns: 1fr;
            }

            .market-pulse {
                display: none;
            }
        }

        @media (max-width: 700px) {
            .dual-panel {
                grid-template-columns: 1fr;
            }

            .top-bar {
                flex-wrap: wrap;
                gap: 12px;
            }

            .balance-chip {
                font-size: 0.8rem;
                padding: 5px 12px;
            }

            .position-item {
                grid-template-columns: 1.5fr 1fr 1fr 1fr;
                font-size: 0.7rem;
            }
        }

        /* animated pulse dot */
        .pulse-dot {
            display: inline-block;
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: var(--green);
            margin-right: 6px;
            box-shadow: 0 0 10px var(--green);
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% { opacity: 1; transform: scale(1); }
            50% { opacity: 0.5; transform: scale(0.9); }
            100% { opacity: 1; transform: scale(1); }
        }

        /* live price ticker animation (simulated) */
        .live-tick {
            transition: color 0.2s;
        }

        .flash-green {
            animation: flashGreen 0.5s;
        }

        .flash-red {
            animation: flashRed 0.5s;
        }

        @keyframes flashGreen {
            0% { background-color: rgba(14, 203, 129, 0.3); }
            100% { background-color: transparent; }
        }

        @keyframes flashRed {
            0% { background-color: rgba(246, 70, 93, 0.3); }
            100% { background-color: transparent; }
        }
    </style>
</head>
<body>
    <div class="app">
        <!-- top navigation bar -->
        <header class="top-bar">
            <div class="logo-area">
                <div class="logo-icon"><i class="fas fa-chart-line"></i></div>
                <div class="logo-text">Trade<span>mate</span></div>
            </div>

            <!-- live market pulse -->
            <div class="market-pulse">
                <div class="pulse-item">
                    <span class="pulse-label">BTC/USD</span>
                    <span class="pulse-value" id="btcPrice">64,230.50</span>
                    <span class="pulse-change positive" id="btcChange">+2.45%</span>
                </div>
                <div class="pulse-item">
                    <span class="pulse-label">ETH/USD</span>
                    <span class="pulse-value" id="ethPrice">3,420.80</span>
                    <span class="pulse-change positive" id="ethChange">+1.80%</span>
                </div>
                <div class="pulse-item">
                    <span class="pulse-label">S&P 500</span>
                    <span class="pulse-value">5,240.30</span>
                    <span class="pulse-change positive">+0.62%</span>
                </div>
            </div>

            <div class="user-actions">
                <div class="balance-chip">
                    <i class="fas fa-wallet"></i> $28,420.50
                </div>
                <div class="avatar">JD</div>
            </div>
        </header>

        <!-- main dashboard grid: chart + trade panel -->
        <div class="dashboard-grid">
            <!-- left column: chart & market data -->
            <div style="display: flex; flex-direction: column; gap: 16px;">
                <!-- chart panel -->
                <div class="panel">
                    <div class="panel-header">
                        <div class="panel-title">
                            <i class="fas fa-chart-area"></i> BTC / USD
                            <span style="font-family: 'JetBrains Mono'; color: var(--green); margin-left: 8px; font-size: 0.9rem;" id="chartPrice">$64,230.50</span>
                            <span class="positive" style="font-family: 'JetBrains Mono'; font-size: 0.8rem; margin-left: 4px;">+2.45%</span>
                        </div>
                        <div class="timeframe">
                            <span>1H</span>
                            <span>4H</span>
                            <span class="active">1D</span>
                            <span>1W</span>
                            <span>1M</span>
                        </div>
                        
