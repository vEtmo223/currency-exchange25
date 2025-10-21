# currency-exchange25
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Курсы валют | Калькулятор и прогнозы</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f5f7fa;
            color: #333;
            line-height: 1.6;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            color: white;
            padding: 30px 0;
            text-align: center;
            border-radius: 0 0 10px 10px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
        }
        
        h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }
        
        .subtitle {
            font-size: 1.1rem;
            opacity: 0.9;
        }
        
        .last-update {
            margin-top: 15px;
            font-size: 0.9rem;
            opacity: 0.8;
        }
        
        .currency-section {
            margin: 30px 0;
        }
        
        .section-title {
            font-size: 1.8rem;
            margin-bottom: 20px;
            color: #2a5298;
            border-bottom: 2px solid #eaeaea;
            padding-bottom: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .toggle-btn {
            background: #2a5298;
            color: white;
            border: none;
            border-radius: 5px;
            padding: 8px 15px;
            cursor: pointer;
            transition: background 0.3s;
            font-size: 0.9rem;
        }
        
        .toggle-btn:hover {
            background: #1e3c72;
        }
        
        .currency-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 20px;
        }
        
        .currency-card {
            background: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.05);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            display: flex;
            flex-direction: column;
        }
        
        .currency-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);
        }
        
        .currency-header {
            display: flex;
            align-items: center;
            margin-bottom: 15px;
        }
        
        .currency-icon {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-right: 15px;
            font-weight: bold;
            color: white;
        }
        
        .fiat .currency-icon {
            background-color: #2a5298;
        }
        
        .crypto .currency-icon {
            background-color: #f7931a;
        }
        
        .currency-name {
            font-size: 1.2rem;
            font-weight: 600;
        }
        
        .currency-code {
            color: #777;
            font-size: 0.9rem;
        }
        
        .currency-rate {
            font-size: 1.5rem;
            font-weight: 700;
            margin: 10px 0;
        }
        
        .currency-change {
            display: flex;
            align-items: center;
            margin-top: auto;
        }
        
        .change-positive {
            color: #2ecc71;
        }
        
        .change-negative {
            color: #e74c3c;
        }
        
        .change-icon {
            margin-right: 5px;
        }
        
        /* Стили для калькулятора */
        .calculator {
            background: white;
            border-radius: 10px;
            padding: 25px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.05);
            margin: 30px 0;
        }
        
        .calculator-title {
            font-size: 1.5rem;
            margin-bottom: 20px;
            color: #2a5298;
        }
        
        .calculator-form {
            display: grid;
            grid-template-columns: 1fr auto 1fr auto 1fr;
            gap: 15px;
            align-items: end;
        }
        
        .form-group {
            display: flex;
            flex-direction: column;
        }
        
        .form-group label {
            margin-bottom: 8px;
            font-weight: 500;
            color: #555;
        }
        
        .form-control {
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1rem;
            transition: border-color 0.3s;
        }
        
        .form-control:focus {
            border-color: #2a5298;
            outline: none;
        }
        
        .swap-btn {
            background: #2a5298;
            color: white;
            border: none;
            border-radius: 5px;
            padding: 12px;
            cursor: pointer;
            transition: background 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .swap-btn:hover {
            background: #1e3c72;
        }
        
        .result {
            font-size: 1.2rem;
            font-weight: 600;
            color: #2a5298;
            padding: 12px;
            background: #f0f5ff;
            border-radius: 5px;
            text-align: center;
        }
        
        /* Стили для прогнозов */
        .forecast-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 20px;
        }
        
        .forecast-card {
            background: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.05);
        }
        
        .forecast-header {
            display: flex;
            align-items: center;
            margin-bottom: 15px;
        }
        
        .forecast-icon {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-right: 15px;
            font-weight: bold;
            color: white;
        }
        
        .forecast-name {
            font-size: 1.2rem;
            font-weight: 600;
        }
        
        .forecast-code {
            color: #777;
            font-size: 0.9rem;
        }
        
        .forecast-chart {
            height: 60px;
            margin: 15px 0;
            position: relative;
            overflow: hidden;
        }
        
        .chart-line {
            position: absolute;
            bottom: 0;
            width: 100%;
            height: 100%;
            display: flex;
            align-items: flex-end;
        }
        
        .chart-bar {
            flex: 1;
            background: #e0e0e0;
            margin: 0 1px;
            border-radius: 2px 2px 0 0;
            transition: height 0.5s;
        }
        
        .forecast-info {
            display: flex;
            justify-content: space-between;
            margin-top: 10px;
        }
        
        .forecast-value {
            font-size: 1.1rem;
            font-weight: 600;
        }
        
        .forecast-change {
            display: flex;
            align-items: center;
        }
        
        .loader {
            text-align: center;
            padding: 30px;
            font-size: 1.2rem;
            color: #666;
        }
        
        footer {
            text-align: center;
            margin-top: 40px;
            padding: 20px;
            color: #777;
            font-size: 0.9rem;
            border-top: 1px solid #eaeaea;
        }
        
        .hidden {
            display: none;
        }
        
        @media (max-width: 768px) {
            .currency-grid, .forecast-container {
                grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            }
            
            .calculator-form {
                grid-template-columns: 1fr;
            }
            
            .swap-btn {
                order: 1;
                margin-top: 10px;
            }
            
            h1 {
                font-size: 2rem;
            }
            
            .section-title {
                flex-direction: column;
                align-items: flex-start;
            }
            
            .toggle-btn {
                margin-top: 10px;
            }
        }
        
        @media (max-width: 480px) {
            .currency-grid, .forecast-container {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <header>
        <div class="container">
            <h1>Курсы валют и криптовалют</h1>
            <p class="subtitle">Актуальные курсы, калькулятор и прогнозы</p>
            <p class="last-update" id="last-update">Обновление данных...</p>
        </div>
    </header>
    
    <div class="container">
        <section class="calculator">
            <h2 class="calculator-title">Калькулятор валют</h2>
            <div class="calculator-form">
                <div class="form-group">
                    <label for="amount">Сумма</label>
                    <input type="number" id="amount" class="form-control" value="100" min="0" step="0.01">
                </div>
                
                <div class="form-group">
                    <label for="from-currency">Из</label>
                    <select id="from-currency" class="form-control">
                        <option value="RUB">RUB - Российский рубль</option>
                        <option value="USD">USD - Доллар США</option>
                        <option value="EUR">EUR - Евро</option>
                        <option value="GBP">GBP - Фунт стерлингов</option>
                        <option value="JPY">JPY - Японская иена</option>
                        <option value="CNY">CNY - Китайский юань</option>
                        <option value="CHF">CHF - Швейцарский франк</option>
                        <option value="CAD">CAD - Канадский доллар</option>
                        <option value="AUD">AUD - Австралийский доллар</option>
                        <option value="NZD">NZD - Новозеландский доллар</option>
                        <option value="SGD">SGD - Сингапурский доллар</option>
                        <option value="HKD">HKD - Гонконгский доллар</option>
                        <option value="SEK">SEK - Шведская крона</option>
                        <option value="NOK">NOK - Норвежская крона</option>
                        <option value="KRW">KRW - Южнокорейская вона</option>
                        <option value="TRY">TRY - Турецкая лира</option>
                        <option value="BRL">BRL - Бразильский реал</option>
                        <option value="INR">INR - Индийская рупия</option>
                        <option value="ZAR">ZAR - Южноафриканский рэнд</option>
                        <option value="MXN">MXN - Мексиканское песо</option>
                        <option value="BTC">BTC - Bitcoin</option>
                        <option value="ETH">ETH - Ethereum</option>
                    </select>
                </div>
                
                <button class="swap-btn" id="swap-currencies">
                    ⇄
                </button>
                
                <div class="form-group">
                    <label for="to-currency">В</label>
                    <select id="to-currency" class="form-control">
                        <option value="USD">USD - Доллар США</option>
                        <option value="RUB">RUB - Российский рубль</option>
                        <option value="EUR">EUR - Евро</option>
                        <option value="GBP">GBP - Фунт стерлингов</option>
                        <option value="JPY">JPY - Японская иена</option>
                        <option value="CNY">CNY - Китайский юань</option>
                        <option value="CHF">CHF - Швейцарский франк</option>
                        <option value="CAD">CAD - Канадский доллар</option>
                        <option value="AUD">AUD - Австралийский доллар</option>
                        <option value="NZD">NZD - Новозеландский доллар</option>
                        <option value="SGD">SGD - Сингапурский доллар</option>
                        <option value="HKD">HKD - Гонконгский доллар</option>
                        <option value="SEK">SEK - Шведская крона</option>
                        <option value="NOK">NOK - Норвежская крона</option>
                        <option value="KRW">KRW - Южнокорейская вона</option>
                        <option value="TRY">TRY - Турецкая лира</option>
                        <option value="BRL">BRL - Бразильский реал</option>
                        <option value="INR">INR - Индийская рупия</option>
                        <option value="ZAR">ZAR - Южноафриканский рэнд</option>
                        <option value="MXN">MXN - Мексиканское песо</option>
                        <option value="BTC">BTC - Bitcoin</option>
                        <option value="ETH">ETH - Ethereum</option>
                    </select>
                </div>
                
                <div class="result" id="conversion-result">
                    Результат конвертации
                </div>
            </div>
        </section>
        
        <section class="currency-section">
            <h2 class="section-title">
                Фиатные валюты
                <button class="toggle-btn" id="toggle-fiat">Показать все валюты</button>
            </h2>
            <div class="currency-grid" id="fiat-currencies">
                <div class="loader">Загрузка данных о валютах...</div>
            </div>
        </section>
        
        <section class="currency-section">
            <h2 class="section-title">Криптовалюты</h2>
            <div class="currency-grid" id="crypto-currencies">
                <div class="loader">Загрузка данных о криптовалютах...</div>
            </div>
        </section>
        
        <section class="currency-section">
            <h2 class="section-title">Прогнозы на неделю</h2>
            <div class="forecast-container" id="forecast-currencies">
                <div class="loader">Загрузка прогнозов...</div>
            </div>
        </section>
    </div>
    
    <footer>
        <div class="container">
            <p>Данные о курсах валют обновляются автоматически. Информация предоставляется только в ознакомительных целях.</p>
            <p>Прогнозы являются предположительными и не гарантируют точности.</p>
        </div>
    </footer>
    
    <script>
        // Основные фиатные валюты
        const mainFiatCurrencies = [
            { code: "USD", name: "Доллар США", rate: 92.45, change: 0.35 },
            { code: "EUR", name: "Евро", rate: 99.80, change: -0.42 },
            { code: "GBP", name: "Фунт стерлингов", rate: 116.20, change: 0.15 },
            { code: "JPY", name: "Японская иена", rate: 0.59, change: 0.02 },
            { code: "CNY", name: "Китайский юань", rate: 12.75, change: -0.08 },
            { code: "CHF", name: "Швейцарский франк", rate: 102.30, change: 0.25 }
        ];
        
        // Все фиатные валюты
        const allFiatCurrencies = [
            { code: "USD", name: "Доллар США", rate: 92.45, change: 0.35 },
            { code: "EUR", name: "Евро", rate: 99.80, change: -0.42 },
            { code: "GBP", name: "Фунт стерлингов", rate: 116.20, change: 0.15 },
            { code: "JPY", name: "Японская иена", rate: 0.59, change: 0.02 },
            { code: "CNY", name: "Китайский юань", rate: 12.75, change: -0.08 },
            { code: "CHF", name: "Швейцарский франк", rate: 102.30, change: 0.25 },
            { code: "CAD", name: "Канадский доллар", rate: 67.50, change: 0.12 },
            { code: "AUD", name: "Австралийский доллар", rate: 60.20, change: -0.30 },
            { code: "NZD", name: "Новозеландский доллар", rate: 55.80, change: 0.18 },
            { code: "SGD", name: "Сингапурский доллар", rate: 68.40, change: 0.05 },
            { code: "HKD", name: "Гонконгский доллар", rate: 11.85, change: -0.10 },
            { code: "SEK", name: "Шведская крона", rate: 8.75, change: 0.22 },
            { code: "NOK", name: "Норвежская крона", rate: 8.60, change: -0.15 },
            { code: "KRW", name: "Южнокорейская вона", rate: 0.067, change: 0.08 },
            { code: "TRY", name: "Турецкая лира", rate: 2.85, change: -1.20 },
            { code: "BRL", name: "Бразильский реал", rate: 18.20, change: 0.45 },
            { code: "INR", name: "Индийская рупия", rate: 1.10, change: -0.05 },
            { code: "ZAR", name: "Южноафриканский рэнд", rate: 4.95, change: 0.30 },
            { code: "MXN", name: "Мексиканское песо", rate: 5.40, change: -0.25 },
            { code: "AED", name: "Дирхам ОАЭ", rate: 25.18, change: 0.15 },
            { code: "SAR", name: "Саудовский риял", rate: 24.65, change: 0.12 },
            { code: "THB", name: "Тайский бат", rate: 2.52, change: -0.08 },
            { code: "MYR", name: "Малайзийский ринггит", rate: 19.65, change: 0.05 },
            { code: "IDR", name: "Индонезийская рупия", rate: 0.0058, change: 0.02 },
            { code: "PHP", name: "Филиппинское песо", rate: 1.62, change: -0.10 },
            { code: "VND", name: "Вьетнамский донг", rate: 0.0037, change: 0.01 },
            { code: "PLN", name: "Польский злотый", rate: 23.15, change: 0.18 },
            { code: "CZK", name: "Чешская крона", rate: 3.95, change: -0.12 },
            { code: "HUF", name: "Венгерский форинт", rate: 0.25, change: 0.05 },
            { code: "RON", name: "Румынский лей", rate: 20.10, change: -0.08 },
            { code: "DKK", name: "Датская крона", rate: 13.38, change: 0.10 },
            { code: "ISK", name: "Исландская крона", rate: 0.66, change: -0.03 },
            { code: "HRK", name: "Хорватская куна", rate: 13.20, change: 0.07 }
        ];
        
        const cryptoCurrencies = [
            { code: "BTC", name: "Bitcoin", rate: 5120000, change: 2.35 },
            { code: "ETH", name: "Ethereum", rate: 285000, change: -1.42 },
            { code: "BNB", name: "Binance Coin", rate: 35200, change: 0.85 },
            { code: "XRP", name: "Ripple", rate: 48.50, change: 3.15 },
            { code: "ADA", name: "Cardano", rate: 32.75, change: -0.75 },
            { code: "DOGE", name: "Dogecoin", rate: 8.20, change: 5.20 },
            { code: "SOL", name: "Solana", rate: 12500, change: 4.50 },
            { code: "DOT", name: "Polkadot", rate: 650, change: -1.20 },
            { code: "AVAX", name: "Avalanche", rate: 2800, change: 2.80 },
            { code: "MATIC", name: "Polygon", rate: 95, change: -0.50 }
        ];
        
        // Данные для прогнозов
        const forecastData = [
            {
                code: "USD",
                name: "Доллар США",
                currentRate: 92.45,
                forecast: "рост",
                change: 1.2,
                trend: [85, 87, 89, 90, 91, 92, 92.45]
            },
            {
                code: "EUR",
                name: "Евро",
                currentRate: 99.80,
                forecast: "падение",
                change: -0.8,
                trend: [102, 101, 100.5, 100, 99.9, 99.8, 99.8]
            },
            {
                code: "GBP",
                name: "Фунт стерлингов",
                currentRate: 116.20,
                forecast: "стабильность",
                change: 0.1,
                trend: [115.5, 115.8, 116, 116.2, 116.1, 116.2, 116.2]
            },
            {
                code: "BTC",
                name: "Bitcoin",
                currentRate: 5120000,
                forecast: "рост",
                change: 3.5,
                trend: [4800000, 4900000, 4950000, 5000000, 5050000, 5100000, 5120000]
            },
            {
                code: "ETH",
                name: "Ethereum",
                currentRate: 285000,
                forecast: "нестабильность",
                change: 0.2,
                trend: [280000, 282000, 284000, 286000, 284000, 285000, 285000]
            },
            {
                code: "JPY",
                name: "Японская иена",
                currentRate: 0.59,
                forecast: "падение",
                change: -0.5,
                trend: [0.61, 0.60, 0.60, 0.59, 0.59, 0.59, 0.59]
            }
        ];
        
        // Функция для форматирования чисел
        function formatNumber(num, decimals = 2) {
            return num.toLocaleString('ru-RU', {
                minimumFractionDigits: decimals,
                maximumFractionDigits: decimals
            });
        }
        
        // Функция для создания HTML карточки валюты
        function createCurrencyCard(currency, type) {
            const changeClass = currency.change >= 0 ? 'change-positive' : 'change-negative';
            const changeIcon = currency.change >= 0 ? '▲' : '▼';
            const changeValue = Math.abs(currency.change);
            
            return `
                <div class="currency-card ${type}">
                    <div class="currency-header">
                        <div class="currency-icon">${currency.code.substring(0, 2)}</div>
                        <div>
                            <div class="currency-name">${currency.name}</div>
                            <div class="currency-code">${currency.code}</div>
                        </div>
                    </div>
                    <div class="currency-rate">${formatNumber(currency.rate, currency.rate < 1 ? 4 : 2)} ₽</div>
                    <div class="currency-change ${changeClass}">
                        <span class="change-icon">${changeIcon}</span>
                        <span>${changeValue}%</span>
                    </div>
                </div>
            `;
        }
        
        // Функция для создания HTML карточки прогноза
        function createForecastCard(currency) {
            const changeClass = currency.change >= 0 ? 'change-positive' : 'change-negative';
            const changeIcon = currency.change >= 0 ? '▲' : '▼';
            const changeValue = Math.abs(currency.change);
            
            // Нормализуем данные для отображения на графике
            const maxValue = Math.max(...currency.trend);
            const minValue = Math.min(...currency.trend);
            const range = maxValue - minValue;
            
            return `
                <div class="forecast-card">
                    <div class="forecast-header">
                        <div class="forecast-icon" style="background-color: ${currency.code === 'BTC' || currency.code === 'ETH' ? '#f7931a' : '#2a5298'}">
                            ${currency.code.substring(0, 2)}
                        </div>
                        <div>
                            <div class="forecast-name">${currency.name}</div>
                            <div class="forecast-code">${currency.code}</div>
                        </div>
                    </div>
                    <div class="forecast-chart">
                        <div class="chart-line">
                            ${currency.trend.map(value => {
                                const height = range > 0 ? ((value - minValue) / range) * 100 : 50;
                                return `<div class="chart-bar" style="height: ${height}%"></div>`;
                            }).join('')}
                        </div>
                    </div>
                    <div class="forecast-info">
                        <div class="forecast-value">${formatNumber(currency.currentRate, currency.currentRate < 1 ? 4 : 2)} ₽</div>
                        <div class="forecast-change ${changeClass}">
                            <span class="change-icon">${changeIcon}</span>
                            <span>${changeValue}%</span>
                        </div>
                    </div>
                    <div style="margin-top: 10px; font-size: 0.9rem; color: #666;">
                        Прогноз: <strong>${currency.forecast}</strong>
                    </div>
                </div>
            `;
        }
        
        // Функция для отображения валют
        function displayCurrencies(showAllFiat = false) {
            const fiatContainer = document.getElementById('fiat-currencies');
            const cryptoContainer = document.getElementById('crypto-currencies');
            const forecastContainer = document.getElementById('forecast-currencies');
            const toggleBtn = document.getElementById('toggle-fiat');
            
            fiatContainer.innerHTML = '';
            cryptoContainer.innerHTML = '';
            forecastContainer.innerHTML = '';
            
            // Отображаем фиатные валюты (основные или все)
            const fiatToShow = showAllFiat ? allFiatCurrencies : mainFiatCurrencies;
            fiatToShow.forEach(currency => {
                fiatContainer.innerHTML += createCurrencyCard(currency, 'fiat');
            });
            
            // Обновляем текст кнопки
            toggleBtn.textContent = showAllFiat ? 'Показать только основные' : 'Показать все валюты';
            
            cryptoCurrencies.forEach(currency => {
                cryptoContainer.innerHTML += createCurrencyCard(currency, 'crypto');
            });
            
            forecastData.forEach(currency => {
                forecastContainer.innerHTML += createForecastCard(currency);
            });
            
            // Обновляем время последнего обновления
            const now = new Date();
            document.getElementById('last-update').textContent = 
                `Последнее обновление: ${now.toLocaleString('ru-RU')}`;
        }
        
        // Функция для конвертации валют
        function convertCurrency() {
            const amount = parseFloat(document.getElementById('amount').value);
            const fromCurrency = document.getElementById('from-currency').value;
            const toCurrency = document.getElementById('to-currency').value;
            
            if (isNaN(amount) || amount < 0) {
                document.getElementById('conversion-result').textContent = 'Введите корректную сумму';
                return;
            }
            
            // В реальном проекте здесь был бы запрос к API для получения актуальных курсов
            // Для демонстрации используем статические данные
            
            let fromRate, toRate;
            
            // Находим курс для исходной валюты
            if (fromCurrency === 'RUB') {
                fromRate = 1;
            } else {
                const allCurrencies = [...allFiatCurrencies, ...cryptoCurrencies];
                const fromCurrencyData = allCurrencies.find(c => c.code === fromCurrency);
                fromRate = fromCurrencyData ? fromCurrencyData.rate : 1;
            }
            
            // Находим курс для целевой валюты
            if (toCurrency === 'RUB') {
                toRate = 1;
            } else {
                const allCurrencies = [...allFiatCurrencies, ...cryptoCurrencies];
                const toCurrencyData = allCurrencies.find(c => c.code === toCurrency);
                toRate = toCurrencyData ? toCurrencyData.rate : 1;
            }
            
            // Выполняем конвертацию
            let result;
            if (fromCurrency === 'RUB') {
                // Из рублей в другую валюту
                result = amount / toRate;
            } else if (toCurrency === 'RUB') {
                // Из другой валюты в рубли
                result = amount * fromRate;
            } else {
                // Конвертация между двумя валютами через рубли
                result = (amount * fromRate) / toRate;
            }
            
            // Форматируем результат
            const formattedResult = formatNumber(result, result < 1 ? 6 : 2);
            document.getElementById('conversion-result').textContent = 
                `${amount} ${fromCurrency} = ${formattedResult} ${toCurrency}`;
        }
        
        // Функция для обмена валют местами
        function swapCurrencies() {
            const fromCurrency = document.getElementById('from-currency');
            const toCurrency = document.getElementById('to-currency');
            
            const temp = fromCurrency.value;
            fromCurrency.value = toCurrency.value;
            toCurrency.value = temp;
            
            convertCurrency();
        }
        
        // Переменная для отслеживания состояния отображения фиатных валют
        let showAllFiatCurrencies = false;
        
        // Инициализация при загрузке страницы
        document.addEventListener('DOMContentLoaded', function() {
            // Отображаем валюты (изначально только основные)
            displayCurrencies(showAllFiatCurrencies);
            
            // Настраиваем калькулятор
            document.getElementById('amount').addEventListener('input', convertCurrency);
            document.getElementById('from-currency').addEventListener('change', convertCurrency);
            document.getElementById('to-currency').addEventListener('change', convertCurrency);
            document.getElementById('swap-currencies').addEventListener('click', swapCurrencies);
            
            // Настраиваем кнопку переключения отображения валют
            document.getElementById('toggle-fiat').addEventListener('click', function() {
                showAllFiatCurrencies = !showAllFiatCurrencies;
                displayCurrencies(showAllFiatCurrencies);
            });
            
            // Выполняем первоначальную конвертацию
            convertCurrency();
            
            // В реальном проекте здесь был бы код для получения данных через API
            // Например, с использованием fetch для получения данных с сервера
        });
    </script>
</body>
</html>
