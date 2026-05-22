index.html<img width="1101" height="1114" alt="Gemini_Generated_Image_8j60cl8j60cl8j60 (1)" src="https://github.com/user-attachments/assets/78c1d0ef-c757-4bfb-b5df-4e3385e9dbf8" /><!DOCTYPE html>
<html lang="zh-TW">
<head>
<link rel="apple-touch-icon" href="logo.png">
    <link rel="icon" type="image/png" href="logo.png">
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>智慧行動雲端筆記本 v5.0 (含刪除功能)</title>
    <style>
        :root {
            --bg-color: #f6f8fa;
            --card-bg: #ffffff;
            --text-main: #24292e;
            --text-muted: #586069;
            --primary: #2196f3;
            --primary-grad: linear-gradient(135deg, #2196f3 0%, #047edf 100%);
            --ai-grad: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
            --success: #2e7d32;
            --dashboard-bg: linear-gradient(135deg, #1b5e20 0%, #2e7d32 100%);
        }

        body { 
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; 
            max-width: 480px; margin: 0 auto; padding: 20px 15px; background-color: var(--bg-color); color: var(--text-main); line-height: 1.4;
        }

        h2 { 
            text-align: center; font-size: 22px; font-weight: 800;
            background: linear-gradient(135deg, #24292e 0%, #586069 100%);
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
            margin-bottom: 4px; letter-spacing: -0.5px;
        }

        .today-date-display { text-align: center; font-size: 13px; font-weight: 700; color: #666; margin-bottom: 18px; letter-spacing: 0.5px; }
        
        .status-panel { 
            margin-bottom: 15px; padding: 12px; background: var(--card-bg); border-radius: 16px; 
            box-shadow: 0 4px 12px rgba(0,0,0,0.03); border: 1px solid rgba(0,0,0,0.02);
        }
        .sync-status { text-align: center; font-size: 13px; font-weight: 700; margin-bottom: 8px; }
        
        .dashboard-box { 
            display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 8px; margin-bottom: 18px; 
            padding: 16px 12px; background: var(--dashboard-bg); color: white; border-radius: 16px; 
            box-shadow: 0 6px 16px rgba(46,125,50,0.25); 
        }
        .dashboard-item { text-align: center; position: relative; }
        .dashboard-item:not(:last-child)::after {
            content: ''; position: absolute; right: -4px; top: 15%; height: 70%; width: 1px; background: rgba(255,255,255,0.2);
        }
        .dashboard-item span { display: block; font-size: 10px; opacity: 0.85; font-weight: 600; margin-bottom: 4px; }
        .dashboard-item strong { font-size: 16px; font-weight: 800; font-variant-numeric: lining-nums; }

        .filters, .search-box, .quick-record-box, .dynamic-form-box { 
            margin-bottom: 16px; padding: 16px; background: var(--card-bg); border-radius: 16px; box-shadow: 0 4px 14px rgba(0,0,0,0.04); border: 1px solid rgba(0,0,0,0.01);
        }
        
        .quick-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-top: 12px; }
        .btn-quick { 
            border: none; padding: 15px 10px; border-radius: 12px; font-weight: 700; color: white; cursor: pointer; font-size: 15px; 
            display: flex; align-items: center; justify-content: center; gap: 8px; transition: transform 0.1s ease;
        }
        .btn-food { background: linear-gradient(135deg, #ff9800 0%, #f57c00 100%); }     
        .btn-expense { background: linear-gradient(135deg, #ff4081 0%, #e91e63 100%); }  
        .btn-work { background: linear-gradient(135deg, #8d6e63 0%, #6d4c41 100%); }     
        .btn-traffic { background: linear-gradient(135deg, #00b0ff 0%, #2196f3 100%); }  
        .btn-quick:active { transform: scale(0.96); }
        
        .dynamic-form-box { border: 2px solid #2196f3; background: #fafbfc; }
        .form-group { margin-bottom: 12px; }
        .form-group label { display: block; font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #444; }
        
        .ai-btn { 
            background: var(--ai-grad); color: white; border: none; padding: 12px; border-radius: 10px; font-size: 14px; font-weight: 700; 
            cursor: pointer; margin-top: 8px; width: 100%; display: block; box-shadow: 0 4px 12px rgba(37,117,252,0.2);
        }
        .ai-btn:disabled { background: #bbb; box-shadow: none; cursor: not-allowed; }

        .memory-status-box { font-size: 12px; font-weight: 700; color: #2e7d32; margin-top: 6px; display: none; }
        .ai-preview { background: #f0f5ff; border-left: 4px solid #2575fc; padding: 12px; margin-top: 12px; border-radius: 8px; font-size: 13px; color: #1e3a8a; line-height: 1.6; }

        /* 歷史記錄與刪除按鈕排版 */
        .note-item { border-bottom: 1px solid #f1f3f5; padding: 14px 0; display: flex; justify-content: space-between; align-items: flex-start; }
        .note-item:last-child { border-bottom: none; }
        .note-meta { font-size: 11px; color: var(--text-muted); margin-top: 6px; font-weight: 500; display: flex; justify-content: space-between; align-items: center; width: 100%; }
        
        /* 💡 獨立優美的紅圈垃圾桶按鈕 */
        .btn-delete-note {
            background: #ffebee; color: #c2185b; border: none; width: 28px; height: 28px; border-radius: 50%; 
            font-size: 12px; cursor: pointer; display: flex; align-items: center; justify-content: center; 
            transition: all 0.2s; margin-left: 8px; flex-shrink: 0;
        }
        .btn-delete-note:active { background: #c2185b; color: white; transform: scale(0.9); }

        .clickable-date-tag { background: #e8eaed; color: #444; padding: 3px 8px; border-radius: 6px; cursor: pointer; font-weight: 600; }

        .tag { padding: 3px 10px; border-radius: 20px; font-size: 11px; margin-left: 6px; font-weight: 700; }
        .tag-食野 { background: #fff3e0; color: #e65100; }
        .tag-洗費 { background: #fce4ec; color: #c2185b; }
        .tag-工作 { background: #f5f5f5; color: #4e342e; }
        .tag-交通 { background: #e3f2fd; color: #0d47a1; }

        .filter-area-wrapper { display: flex; flex-wrap: wrap; gap: 6px; margin-top: 6px; margin-bottom: 10px; }
        .filter-btn { background: #e8eaed; border: none; padding: 6px 12px; border-radius: 20px; font-size: 12px; font-weight: 600; color: #5f6368; cursor: pointer; }
        .filter-btn.active { background: #2196F3; color: white; box-shadow: 0 3px 8px rgba(33,150,243,0.3); }
        .filter-btn.month-btn.active { background: #764ba2; box-shadow: 0 3px 8px rgba(118,75,162,0.3); } 
        
        .clear-filter-btn { background: #fce4ec; color: #c2185b; border: none; padding: 6px 12px; border-radius: 20px; font-size: 12px; font-weight: 700; cursor: pointer; display: none; margin-left: auto; }

        input, textarea, select { box-sizing: border-box; width: 100%; padding: 12px; border: 1px solid #dde1e5; border-radius: 10px; font-size: 15px; background: white; color: var(--text-main); }
        
        .submit-btn { background: var(--primary-grad); color: white; border: none; padding: 14px; border-radius: 10px; font-weight: 700; font-size: 16px; width: 100%; margin-top: 10px; cursor: pointer; box-shadow: 0 4px 12px rgba(33,150,243,0.25); }
        .btn-refresh { background: transparent; border: 1px solid #ced4da; padding: 7px 14px; border-radius: 20px; font-size: 12px; font-weight: 700; color: var(--text-muted); cursor: pointer; display: block; margin: 0 auto; }
        
        h3 { font-size: 16px; font-weight: 800; color: #1a1a1a; margin-top: 22px; margin-bottom: 10px; }
    </style>
</head>
<body>

    <h2>☁️ 智慧雲端生活筆記</h2>
    
    <div class="today-date-display" id="currentDateLabel">📅 讀取日期中...</div>

    <div class="status-panel">
        <div class="sync-status" id="syncLabel" style="color: #ff9800;">🔄 正在連線至 Google 雲端資料庫...</div>
        <button class="btn-refresh" onclick="loadCloudData()">🔄 手動重新整理資料</button>
    </div>

    <div class="dashboard-box">
        <div class="dashboard-item">
            <span>💵 本月洗費總計</span>
            <strong>$<span id="totalExpense">0</span></strong>
        </div>
        <div class="dashboard-item">
            <span>🍔 本月食野開銷</span>
            <strong>$<span id="totalFood">0</span></strong>
        </div>
        <div class="dashboard-item">
            <span>🔥 今日攝取熱量</span>
            <strong><span id="todayCalories">0</span> <span style="font-size:9px;">kcal</span></strong>
        </div>
    </div>

    <div class="quick-record-box">
        <strong style="font-size: 14px; color: #444;">🚀 請選擇記錄項目：</strong>
        <div class="quick-grid">
            <button class="btn-quick btn-food" onclick="switchForm('食野')">🍔 食野</button>
            <button class="btn-quick btn-expense" onclick="switchForm('洗費')">💵 洗費</button>
            <button class="btn-quick btn-work" onclick="switchForm('工作')">💼 工作</button>
            <button class="btn-quick btn-traffic" onclick="switchForm('交通')">🚗 交通</button>
        </div>
    </div>

    <div id="dynamicFormArea" class="dynamic-form-box">
        <h4 id="formTitle" style="margin-top: 0; font-size: 16px; font-weight: 800; color: #1a1a1a; margin-bottom: 12px;">動態表單</h4>
        <div id="formFields"></div>
        <div id="aiPreviewBox" class="ai-preview"></div>
        <button class="submit-btn" id="saveBtn" onclick="submitDynamicForm()">確定</button>
    </div>

    <div class="search-box">
        <div style="display: flex; align-items: center; margin-bottom: 6px;">
            🔍 <input type="text" id="searchBar" oninput="renderNotes()" style="margin-left:5px;" placeholder="搜尋關鍵字...">
            <button class="clear-filter-btn" id="clearFilterBtn" onclick="resetAllFilters()">❌ 清除篩選</button>
        </div>
    </div>

    <div class="filters">
        <span style="font-size: 13px; font-weight: 700; color: #555;">📁 分類：</span>
        <div id="filterButtonsArea" class="filter-area-wrapper"></div>
        
        <span style="font-size: 13px; font-weight: 700; color: #555; margin-top: 5px; display:block;">📅 月份快選：</span>
        <div id="monthButtonsArea" class="filter-area-wrapper"></div>
    </div>

    <h3>📌 記錄</h3>
    <div id="notesList" style="background: white; padding: 6px 16px; border-radius: 16px; box-shadow: 0 4px 14px rgba(0,0,0,0.04); border: 1px solid rgba(0,0,0,0.01);"></div>

    <script>
        const CLOUD_URL = "https://script.google.com/macros/s/AKfycbzH0yTVyy270mziu9z6HD9bXrC8C8DTlCo4x493S0pdnNL6JZxogZQOHNU2-S0YVrBp/exec"; 
        const GEMINI_API_KEY = "你的_GEMINI_API_KEY_鑰匙"; // 👈 ⚠️ 記得貼回你的金鑰！

        let notes = [];
        let currentFilter = '全部'; 
        let currentMonthFilter = '全部月份'; 
        let currentDayFilter = ''; 
        let activeTagType = ''; 
        let aiParsedRecord = { title: '', content: '' };

        let foodMemoryDB = JSON.parse(localStorage.getItem('food_memory_db')) || {};

        function showTodayDate() {
            const now = new Date();
            const days = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
            const label = document.getElementById('currentDateLabel');
            label.innerText = `📅 ${now.getFullYear()}年${now.getMonth() + 1}月${now.getDate()}日 ${days[now.getDay()]}`;
            if (now.getDay() === 0 || now.getDay() === 6) { label.style.color = '#ff5722'; }
        }

        async function loadCloudData() {
            updateStatus("🔄 正在從雲端更新資料...", "#ff9800");
            try {
                const response = await fetch(CLOUD_URL);
                notes = await response.json();
                updateStatus("✅ 雲端連線成功！資料已即時同步", "#2e7d32");
                calculateStats(); 
                refreshUI();
            } catch (error) {
                updateStatus("❌ 雲端同步失敗", "#c2185b");
                notes = JSON.parse(localStorage.getItem('my_notes')) || [];
                calculateStats();
                refreshUI();
            }
        }

        function updateStatus(text, color) {
            const label = document.getElementById('syncLabel');
            label.innerText = text; label.style.color = color;
        }

        function calculateStats() {
            const now = new Date();
            const monthPrefix = `${now.getFullYear()}/${(now.getMonth() + 1).toString().padStart(2, '0')}`; 
            const todayPrefix = `${now.getFullYear()}/${(now.getMonth() + 1).toString().padStart(2, '0')}/${now.getDate().toString().padStart(2, '0')}`; 

            let expenseSum = 0, foodSum = 0, todayCalorieSum = 0;

            notes.forEach(note => {
                if (!note.time) return;
                if (note.time.startsWith(monthPrefix)) {
                    const costMatch = note.content.match(/(?:花費|金額|車資|項目金額)：\$([0-9.]+)/);
                    if (costMatch) {
                        const amount = parseFloat(costMatch[1]) || 0;
                        if (note.tag === '洗費' || note.tag === '交通' || note.tag === '食野') expenseSum += amount;
                        if (note.tag === '食野') foodSum += amount;
                    }
                }
                if (note.time.startsWith(todayPrefix) && note.tag === '食野') {
                    const calorieMatch = note.content.match(/熱量：([0-9.]+)\s*kcal/);
                    if (calorieMatch) todayCalorieSum += parseFloat(calorieMatch[1]) || 0;
                }
            });

            document.getElementById('totalExpense').innerText = expenseSum.toLocaleString();
            document.getElementById('totalFood').innerText = foodSum.toLocaleString();
            document.getElementById('todayCalories').innerText = todayCalorieSum.toLocaleString();
        }

        function switchForm(type) {
            activeTagType = type;
            const formBox = document.getElementById('dynamicFormArea');
            const formTitle = document.getElementById('formTitle');
            const fieldsDiv = document.getElementById('formFields');
            const previewBox = document.getElementById('aiPreviewBox');
            const saveBtn = document.getElementById('saveBtn');
            
            formBox.style.display = 'block'; previewBox.style.display = 'none'; saveBtn.style.display = 'none'; fieldsDiv.innerHTML = ''; 

            if (type === '食野') {
                formTitle.innerText = '🍔 智慧一句話記飲食';
                fieldsDiv.innerHTML = `<div class="form-group"><label>請直接輸入食物與金額</label><input type="text" id="rawAIInput" oninput="checkFoodMemory()" placeholder="例如：叉燒飯 55" required><div id="memoryNotice" class="memory-status-box"></div><button type="button" class="ai-btn" id="aiBtn" onclick="parseWithAI('食野')">✨ 輸入</button></div>`;
            } else if (type === '洗費') {
                formTitle.innerText = '💰 智慧一句話記開銷';
                fieldsDiv.innerHTML = `<div class="form-group"><label>請直接輸入日常開銷項目與金額</label><input type="text" id="rawAIInput" placeholder="例如：去萬寧買洗頭水 $138" required><button type="button" class="ai-btn" id="aiBtn" onclick="parseWithAI('洗費')">✨ 輸入</button></div>`;
            } else if (type === '交通') {
                formTitle.innerText = '🚗 智慧一句話記交通';
                fieldsDiv.innerHTML = `<div class="form-group"><label>請直接輸入起點、終點與車資</label><input type="text" id="rawAIInput" placeholder="例如：旺角地鐵去尖沙咀 12" required><button type="button" class="ai-btn" id="aiBtn" onclick="parseWithAI('交通')">✨ 輸入</button></div>`;
            } else if (type === '工作') {
                formTitle.innerText = '💼 工作進度記錄';
                fieldsDiv.innerHTML = `<div class="form-group"><label>任務標題</label><input type="text" id="workTitle" placeholder="常規事務" required></div><div class="form-group"><label>詳細內容</label><textarea id="workDetail" style="height: 60px;" placeholder="寫下具體進度..."></textarea></div>`;
                saveBtn.style.display = 'block';
            }
            formBox.scrollIntoView({ behavior: 'smooth' });
        }

        function checkFoodMemory() {
            if (activeTagType !== '食野') return;
            const text = document.getElementById('rawAIInput').value.trim();
            const notice = document.getElementById('memoryNotice');
            const saveBtn = document.getElementById('saveBtn');
            const previewBox = document.getElementById('aiPreviewBox');

            if (text.length < 2) { notice.style.display = 'none'; saveBtn.style.display = 'none'; previewBox.style.display = 'none'; return; }
            let cleanFoodKey = text.replace(/[0-9.]+/, '').replace(/[$蚊元]/g, '').replace(/(早餐|午餐|晚餐|宵夜|點心|晏晝|放工|頭先)/g, '').trim();

            if (foodMemoryDB[cleanFoodKey]) {
                let savedData = foodMemoryDB[cleanFoodKey];
                let costMatch = text.match(/([0-9.]+)/);
                let currentCost = costMatch ? costMatch[1] : savedData.cost;

                aiParsedRecord.title = `處理膳食 (${savedData.timeZone})`;
                aiParsedRecord.content = `食物：${savedData.food}\n花費：$${currentCost}\n熱量：${savedData.calories} kcal`;
                previewBox.innerHTML = `<strong>⚡ 已從智慧記憶庫精準自動輸入：</strong><br>• 時段：${savedData.timeZone}<br>• 食物：${savedData.food}<br>• 金額：$${currentCost}<br>• 熱量：${savedData.calories} kcal`;
                previewBox.style.display = 'block';
                notice.innerText = `💡 偵測到完全吻合歷史食物「${cleanFoodKey}」，已自動配對熱量！`;
                notice.style.color = "#2e7d32"; notice.style.display = 'block';
                saveBtn.style.display = 'block'; 
            } else {
                notice.style.display = 'none'; saveBtn.style.display = 'none'; previewBox.style.display = 'none';
            }
        }

        async function parseWithAI(mode) {
            const rawInput = document.getElementById('rawAIInput').value.trim();
            const aiBtn = document.getElementById('aiBtn');
            const previewBox = document.getElementById('aiPreviewBox');
            const saveBtn = document.getElementById('saveBtn');

            if (!rawInput) { alert("請先輸入記錄內容喔！"); return; }
            aiBtn.innerText = "⚡ AI 智慧解析中..."; aiBtn.disabled = true;

            const url = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash:generateContent?key=${GEMINI_API_KEY}`;
            let systemPrompt = '';
            if (mode === '食野') {
                systemPrompt = `請精準拆解句子並估算食物總卡路里(kcal)。你必須判斷出三個數值：1. 用餐時段 (早餐, 午餐, 晚餐, 宵夜/點心) 2. 提取花費金額 (預設 0) 3. 估算總熱量 (純數字 kcal)。請嚴格只輸出 JSON：{"timeZone": "午餐", "cost": 55, "calories": 650, "food": "叉燒飯"}`;
            } else if (mode === '洗費') {
                systemPrompt = `請精準拆解日常洗費句子，提取出開銷的項目描述與金額。請嚴格只輸出 JSON，不要解釋：{"item": "買洗頭水護髮素", "cost": 138}`;
            } else if (mode === '交通') {
                systemPrompt = `請精準拆解交通行程句子，提取出出發起點、到達終點與車資金額。請嚴格只輸出 JSON，不要解釋：{"from": "旺角", "to": "尖沙咀", "cost": 12}`;
            }

            const prompt = `你是一個精通香港生活與飲食文化的智能記帳專家。${systemPrompt} \n\n 用戶輸入的句子：「${rawInput}」`;

            try {
                const response = await fetch(url, { method: "POST", headers: { "Content-Type": "application/json" }, body: JSON.stringify({ contents: [{ parts: [{ text: prompt }] }] }) });
                const data = await response.json();
                let cleanJsonText = data.candidates[0].content.parts[0].text.trim().replace(/```json|```/g, '');
                const result = JSON.parse(cleanJsonText);
                
                if (mode === '食野') {
                    aiParsedRecord.title = `處理膳食 (${result.timeZone})`;
                    aiParsedRecord.content = `食物：${result.food}\n花費：$${result.cost}\n熱量：${result.calories} kcal`;
                    previewBox.innerHTML = `<strong>🤖 AI 新分析結果：</strong><br>• 時段：${result.timeZone}<br>• 食物：${result.food}<br>• 金額：$${result.cost}<br>• 熱量：${result.calories} kcal`;
                    foodMemoryDB[result.food] = { timeZone: result.timeZone, cost: result.cost, calories: result.calories, food: result.food };
                    localStorage.setItem('food_memory_db', JSON.stringify(foodMemoryDB));
                } else if (mode === '洗費') {
                    aiParsedRecord.title = `日常開銷記帳`;
                    aiParsedRecord.content = `項目：${result.item}\n項目金額：$${result.cost}`;
                    previewBox.innerHTML = `<strong>🤖 AI 自動識別結果：</strong><br>• 項目：${result.item}<br>• 金額：$${result.cost}`;
                } else if (mode === '交通') {
                    aiParsedRecord.title = `交通路程記錄`;
                    aiParsedRecord.content = `行程：${result.from} ➡️ ${result.to}\n車資：$${result.cost}`;
                    previewBox.innerHTML = `<strong>🤖 AI 自動識別結果：</strong><br>• 行程：${result.from} ➡️ ${result.to}<br>• 車資：$${result.cost}`;
                }

                previewBox.style.display = 'block'; aiBtn.innerText = "✨ 輸入"; saveBtn.style.display = 'block'; 
            } catch (error) {
                alert("AI 解析失敗。"); aiBtn.innerText = "✨ 輸入"; aiBtn.disabled = false;
            }
        }

        async function submitDynamicForm() {
            const saveBtn = document.getElementById('saveBtn'); saveBtn.disabled = true;
            const now = new Date();
            const timeStr = `${now.getFullYear()}/${(now.getMonth()+1).toString().padStart(2,'0')}/${now.getDate().toString().padStart(2,'0')} ${now.getHours().toString().padStart(2,'0')}:${now.getMinutes().toString().padStart(2,'0')}`;
            
            let finalTitle = aiParsedRecord.title; let finalContent = aiParsedRecord.content;
            if (activeTagType === '工作') {
                finalTitle = `工作任務：${document.getElementById('workTitle').value.trim()}`;
                finalContent = document.getElementById('workDetail').value.trim() || '無';
            }

            const newRecord = { title: finalTitle, content: finalContent, tag: activeTagType, time: timeStr };

            try {
                await fetch(CLOUD_URL, { method: "POST", body: JSON.stringify(newRecord) });
                notes.unshift(newRecord); localStorage.setItem('my_notes', JSON.stringify(notes));
                document.getElementById('dynamicFormArea').style.display = 'none';
                updateStatus("✅ 雲端同步寫入成功！", "#2e7d32"); calculateStats(); 
            } catch (e) {
                alert("雲端同步失敗，已暫存。");
            } finally {
                saveBtn.disabled = false; refreshUI();
            }
        }

        // 💡💡 全新黑科技：真．一鍵雲端同步刪除功能 💡💡
        async function deleteNoteByTime(timeStr) {
            if (!confirm(`⚠️ 確定要刪除這筆在 [${timeStr}] 的記錄嗎？\n此動作將同步從 Google 雲端試算表中抹除！`)) return;

            updateStatus("🗑️ 正在從雲端刪除記錄...", "#ff4d4d");

            try {
                // 向 Google GAS 發送帶有 action: "delete" 的指令
                const response = await fetch(CLOUD_URL, {
                    method: "POST",
                    body: JSON.stringify({ action: "delete", time: timeStr })
                });
                
                const resData = await response.json();
                
                if (resData.status === "deleted") {
                    // 雲端刪除成功後，同步更新網頁本地暫存
                    notes = notes.filter(note => note.time !== timeStr);
                    localStorage.setItem('my_notes', JSON.stringify(notes));
                    updateStatus("🗑️ 記錄已成功從雲端及本地永久刪除！", "#2e7d32");
                    calculateStats(); // 重新計算頂部消費與熱量
                    refreshUI();
                } else {
                    alert("雲端找不到該時間點的記錄，請手動更新網頁再試。");
                    loadCloudData();
                }
            } catch (error) {
                console.error(error);
                alert("❌ 刪除失敗，請檢查網絡或雲端大腦設定。");
                loadCloudData();
            }
        }

        function selectSpecificDay(dateStr) { currentDayFilter = dateStr; document.getElementById('clearFilterBtn').style.display = 'block'; renderNotes(); }
        function resetAllFilters() { currentDayFilter = ''; currentMonthFilter = '全部月份'; currentFilter = '全部'; document.getElementById('searchBar').value = ''; document.getElementById('clearFilterBtn').style.display = 'none'; refreshUI(); }
        function refreshUI() { renderFilterButtons(); renderMonthButtons(); renderNotes(); }

        function renderFilterButtons() {
            const btnArea = document.getElementById('filterButtonsArea'); btnArea.innerHTML = ''; 
            ['全部', '食野', '洗費', '工作', '交通'].forEach(tag => {
                const btn = document.createElement('button'); btn.className = `filter-btn ${currentFilter === tag ? 'active' : ''}`;
                btn.innerText = tag === '全部' ? '全部' : `#${tag}`;
                btn.onclick = () => { currentFilter = tag; renderNotes(); renderFilterButtons(); };
                btnArea.appendChild(btn);
            });
        }

        function renderMonthButtons() {
            const monthArea = document.getElementById('monthButtonsArea'); monthArea.innerHTML = '';
            let monthsSet = new Set();
            notes.forEach(note => {
                if (note.time && note.time.includes('/')) {
                    const parts = note.time.split(' ')[0].split('/');
                    if (parts[0] && parts[1]) monthsSet.add(`${parts[0]}/${parts[1]}`);
                }
            });
            let sortedMonths = Array.from(monthsSet).sort().reverse(); sortedMonths.unshift('全部月份');
            sortedMonths.forEach(m => {
                const btn = document.createElement('button'); btn.className = `filter-btn month-btn ${currentMonthFilter === m ? 'active' : ''}`;
                btn.innerText = m === '全部月份' ? '全部月份' : `${parseInt(m.split('/')[1])}月`;
                btn.onclick = () => { currentMonthFilter = m; currentDayFilter = ''; if(m !== '全部月份') document.getElementById('clearFilterBtn').style.display = 'block'; renderNotes(); renderMonthButtons(); };
                monthArea.appendChild(btn);
            });
        }

        function renderNotes() {
            const listDiv = document.getElementById('notesList'); const searchText = document.getElementById('searchBar').value.toLowerCase(); listDiv.innerHTML = ''; let hasContent = false;
            notes.forEach((note) => {
                if (currentFilter !== '全部' && note.tag !== currentFilter) return;
                if (currentDayFilter !== '') { if (!note.time || !note.time.startsWith(currentDayFilter)) return; } 
                else if (currentMonthFilter !== '全部月份') { if (!note.time || !note.time.startsWith(currentMonthFilter)) return; }
                if (!note.title.toLowerCase().includes(searchText) && !note.content.toLowerCase().includes(searchText) && !note.time.toLowerCase().includes(searchText)) return;
                hasContent = true;
                
                const noteEl = document.createElement('div'); noteEl.className = 'note-item'; const datePart = note.time ? note.time.split(' ')[0] : '';
                
                // 💡 渲染每一行時，包進獨立的 🗑️ 刪除按鈕
                noteEl.innerHTML = `
                    <div style="width: 100%; display: flex; justify-content: space-between; align-items: flex-start;">
                        <div style="flex: 1;">
                            <div style="display:flex; justify-content:space-between; align-items:center;">
                                <strong style="font-size:15px; color:#24292e;">${note.title}</strong> 
                                <span class="tag tag-${note.tag}">#${note.tag}</span>
                            </div>
                            <p style="margin: 6px 0 0 0; color: #444; font-size: 14px; line-height: 1.6; background:#fafbfc; padding:8px 12px; border-radius:8px; border:1px solid #f1f3f5;">${note.content.replace(/\n/g, '<br>')}</p>
                            <div class="note-meta">
                                <span class="clickable-date-tag" onclick="selectSpecificDay('${datePart}')">📅 查看此日 (${datePart})</span>
                                <span>🕒 ${note.time.split(' ')[1] || ''}</span>
                            </div>
                        </div>
                        <button class="btn-delete-note" onclick="deleteNoteByTime('${note.time}')" title="刪除此筆記錄">🗑️</button>
                    </div>`;
                listDiv.appendChild(noteEl);
            });
            if (!hasContent) listDiv.innerHTML = '<p style="text-align:center; color:#999; font-style:italic; padding:20px; font-size:13px;">沒有找到記錄...</p>';
        }

        showTodayDate(); loadCloudData();
    </script>
</body>
</html>
