
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>體重紀錄平台</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Microsoft JhengHei', Arial, sans-serif;
            background: #fffacd;
            min-height: 100vh;
            color: #333;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        .header {
            text-align: center;
            margin-bottom: 30px;
        }
        
        .header h1 {
            color: #8b4513;
            font-size: 2.5em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(139,69,19,0.2);
        }
        
        .header p {
            color: #a0522d;
            font-size: 1.1em;
        }
        
        .card {
            background: #fff8dc;
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 20px 40px rgba(139,69,19,0.1);
            margin-bottom: 20px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255,215,0,0.2);
        }
        
        .screen {
            display: none;
        }
        
        .screen.active {
            display: block;
        }
        
        .top-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            flex-wrap: wrap;
            gap: 10px;
        }
        
        .search-bar {
            flex: 1;
            max-width: 300px;
            position: relative;
        }
        
        .search-bar input {
            width: 100%;
            padding: 10px 15px;
            border: 2px solid #e0e0e0;
            border-radius: 25px;
            font-size: 14px;
            transition: border-color 0.3s;
        }
        
        .search-bar input:focus {
            outline: none;
            border-color: #daa520;
        }
        
        .stats-bar {
            display: flex;
            gap: 20px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }
        
        .stat-item {
            background: #f0e68c;
            padding: 15px 20px;
            border-radius: 10px;
            text-align: center;
            flex: 1;
            min-width: 120px;
        }
        
        .stat-number {
            font-size: 1.8em;
            font-weight: bold;
            color: #8b4513;
        }
        
        .stat-label {
            font-size: 0.9em;
            color: #a0522d;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #555;
        }
        
        input, select {
            width: 100%;
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 16px;
            transition: border-color 0.3s, box-shadow 0.3s;
        }
        
        input:focus, select:focus {
            outline: none;
            border-color: #daa520;
            box-shadow: 0 0 0 3px rgba(218,165,32,0.2);
        }
        
        .btn {
            background: linear-gradient(45deg, #f39c12, #e67e22);
            color: white;
            padding: 12px 30px;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            cursor: pointer;
            transition: all 0.3s;
            margin-right: 10px;
            margin-bottom: 10px;
        }
        
        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(243,156,18,0.4);
        }
        
        .btn-secondary {
            background: #cd853f;
        }
        
        .btn-secondary:hover {
            background: #b8860b;
        }
        
        .btn-danger {
            background: #dc3545;
        }
        
        .btn-danger:hover {
            background: #c82333;
        }
        
        .btn-small {
            padding: 8px 16px;
            font-size: 14px;
        }
        
        .user-list {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .user-card {
            background: linear-gradient(135deg, #f39c12, #e67e22);
            color: white;
            padding: 20px;
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.3s;
            position: relative;
        }
        
        .user-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(243,156,18,0.3);
        }
        
        .user-card h3 {
            margin-bottom: 10px;
            font-size: 1.3em;
        }
        
        .user-card p {
            opacity: 0.9;
            font-size: 0.9em;
            margin-bottom: 5px;
        }
        
        .user-actions {
            position: absolute;
            top: 10px;
            right: 10px;
            display: flex;
            gap: 5px;
        }
        
        .user-actions button {
            background: rgba(255,255,255,0.2);
            border: none;
            color: white;
            padding: 5px 8px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 12px;
        }
        
        .user-actions button:hover {
            background: rgba(255,255,255,0.3);
        }
        
        .user-stats {
            margin-top: 10px;
            padding-top: 10px;
            border-top: 1px solid rgba(255,255,255,0.3);
        }
        
        .data-form {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
        }
        
        .data-group {
            background: #fffacd;
            padding: 20px;
            border-radius: 10px;
        }
        
        .data-group h3 {
            margin-bottom: 15px;
            color: #b8860b;
            border-bottom: 2px solid #daa520;
            padding-bottom: 5px;
        }
        
        .records-list {
            margin-top: 20px;
        }
        
        .record-item {
            background: #fffacd;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 10px;
            border-left: 4px solid #daa520;
            position: relative;
        }
        
        .record-date {
            font-weight: bold;
            color: #b8860b;
            margin-bottom: 5px;
        }
        
        .record-data {
            font-size: 0.9em;
            color: #666;
        }
        
        .record-actions {
            position: absolute;
            top: 10px;
            right: 10px;
        }
        
        .success-message {
            background: #f0e68c;
            color: #8b4513;
            padding: 10px;
            border-radius: 5px;
            margin-bottom: 20px;
            border: 1px solid #daa520;
        }
        
        .nav-buttons {
            margin-bottom: 20px;
        }
        
        .empty-state {
            text-align: center;
            color: #666;
            margin: 40px 0;
        }
        
        .empty-state h3 {
            margin-bottom: 10px;
            color: #8b4513;
        }
        
        .quick-add-form {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }
        
        .toggle-form {
            background: #f0e68c;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 20px;
        }
        
        .chart-container {
            background: white;
            padding: 20px;
            border-radius: 10px;
            margin-top: 20px;
        }
        
        @media (max-width: 768px) {
            .container {
                padding: 10px;
            }
            
            .header h1 {
                font-size: 2em;
            }
            
            .card {
                padding: 20px;
            }
            
            .data-form {
                grid-template-columns: 1fr;
            }
            
            .top-bar {
                flex-direction: column;
                align-items: stretch;
            }
            
            .search-bar {
                max-width: none;
            }
            
            .stats-bar {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>體重紀錄平台</h1>
            <p>綠色種子教練管理系統</p>
        </div>
        
        <!-- 主頁面 - 客戶列表 -->
        <div id="home-screen" class="screen active">
            <div class="card">
                <div class="top-bar">
                    <h2>客戶管理</h2>
                    <div class="search-bar">
                        <input type="text" id="search-users" placeholder="🔍 搜尋客戶姓名...">
                    </div>
                    <button class="btn" onclick="toggleAddForm()">➕ 新增客戶</button>
                </div>
                
                <div class="stats-bar">
                    <div class="stat-item">
                        <div class="stat-number" id="total-users">0</div>
                        <div class="stat-label">總用客數</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-number" id="today-records">0</div>
                        <div class="stat-label">今日記錄</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-number" id="total-records">0</div>
                        <div class="stat-label">總記錄數</div>
                    </div>
                </div>
                
                <div id="add-user-form" class="toggle-form" style="display: none;">
                    <h3>快速新增客戶</h3>
                    <form id="user-form">
                        <div class="quick-add-form">
                            <div class="form-group">
                                <label for="name">姓名 *</label>
                                <input type="text" id="name" name="name" required>
                            </div>
                            <div class="form-group">
                                <label for="gender">性別 *</label>
                                <select id="gender" name="gender" required>
                                    <option value="">請選擇</option>
                                    <option value="male">男性</option>
                                    <option value="female">女性</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label for="height">身高 (cm) *</label>
                                <input type="number" id="height" name="height" min="100" max="250" required>
                            </div>
                            <div class="form-group">
                                <label for="age">年齡 *</label>
                                <input type="number" id="age" name="age" min="1" max="150" required>
                            </div>
                        </div>
                        <button type="submit" class="btn">✅ 新增客戶</button>
                        <button type="button" class="btn btn-secondary" onclick="toggleAddForm()">取消</button>
                    </form>
                </div>
                
                <div id="user-list" class="user-list"></div>
            </div>
        </div>
        
        <!-- 數據記錄頁面 -->
        <div id="data-entry-screen" class="screen">
            <div class="card">
                <div class="nav-buttons">
                    <button class="btn btn-secondary" onclick="showScreen('home-screen')">← 返回客戶列表</button>
                    <button class="btn btn-secondary" onclick="showUserProfile()">👤 客戶資料</button>
                </div>
                <div id="user-info"></div>
                <div id="success-message" class="success-message" style="display: none;"></div>
                <form id="data-form">
                    <div class="form-group">
                        <label for="record-date">記錄日期 *</label>
                        <input type="date" id="record-date" name="date" required>
                    </div>
                    
                    <div class="data-form">
                        <div class="data-group">
                            <h3>📏 基本數據</h3>
                            <div class="form-group">
                                <label for="weight">體重 (kg)</label>
                                <input type="number" id="weight" name="weight" step="0.1" min="0">
                            </div>
                            <div class="form-group">
                                <label for="bmi">BMI</label>
                                <input type="number" id="bmi" name="bmi" step="0.1" min="0">
                            </div>
                            <div class="form-group">
                                <label for="body-age">身體年齡</label>
                                <input type="number" id="body-age" name="bodyAge" min="0">
                            </div>
                        </div>
                        
                        <div class="data-group">
                            <h3>💪 身體組成</h3>
                            <div class="form-group">
                                <label for="muscle-mass">肌肉量 (kg)</label>
                                <input type="number" id="muscle-mass" name="muscleMass" step="0.1" min="0">
                            </div>
                            <div class="form-group">
                                <label for="body-fat">體脂肪 (%)</label>
                                <input type="number" id="body-fat" name="bodyFat" step="0.1" min="0" max="100">
                            </div>
                            <div class="form-group">
                                <label for="bone-mass">骨量 (kg)</label>
                                <input type="number" id="bone-mass" name="boneMass" step="0.1" min="0">
                            </div>
                            <div class="form-group">
                                <label for="metabolism">代謝 (kcal)</label>
                                <input type="number" id="metabolism" name="metabolism" min="0">
                            </div>
                            <div class="form-group">
                                <label for="visceral-fat">內臟脂肪</label>
                                <input type="number" id="visceral-fat" name="visceralFat" step="0.1" min="0">
                            </div>
                            <div class="form-group">
                                <label for="body-water">身體水分率 (%)</label>
                                <input type="number" id="body-water" name="bodyWater" step="0.1" min="0" max="100">
                            </div>
                        </div>
                    </div>
                    
                    <div style="margin-top: 20px;">
                        <button type="submit" class="btn">💾 儲存數據</button>
                        <button type="button" class="btn btn-secondary" onclick="showRecords()">📈 查看記錄</button>
                        
                    </div>
                </form>
                
                <div id="records-section" class="records-list" style="display: none;">
                    <h3>📊 歷史記錄</h3>
                    <div id="records-list"></div>
                </div>
            </div>
        </div>
    </div>
    
    <script>
        // 數據存儲
        let users = [];
        let records = [];
        let currentUser = null;
        let filteredUsers = [];
        
        // 頁面切換
        function showScreen(screenId) {
            document.querySelectorAll('.screen').forEach(screen => {
                screen.classList.remove('active');
            });
            document.getElementById(screenId).classList.add('active');
            
            if (screenId === 'home-screen') {
                updateStats();
                renderUserList();
            }
        }
        
        // 切換新增客戶表單
        function toggleAddForm() {
            const form = document.getElementById('add-user-form');
            form.style.display = form.style.display === 'none' ? 'block' : 'none';
            if (form.style.display === 'block') {
                document.getElementById('name').focus();
            }
        }
        
        // 更新統計數據
        function updateStats() {
            const today = new Date().toISOString().split('T')[0];
            const todayRecords = records.filter(r => r.date === today).length;
            
            document.getElementById('total-users').textContent = users.length;
            document.getElementById('today-records').textContent = todayRecords;
            document.getElementById('total-records').textContent = records.length;
        }
        
        // 新增客戶
        document.getElementById('user-form').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const formData = new FormData(e.target);
            const userData = {
                id: Date.now(),
                name: formData.get('name'),
                gender: formData.get('gender'),
                height: parseInt(formData.get('height')),
                age: parseInt(formData.get('age')),
                createdAt: new Date().toLocaleDateString('zh-TW')
            };
            
            users.push(userData);
            e.target.reset();
            toggleAddForm();
            
            updateStats();
            renderUserList();
            
            // 顯示成功訊息
            alert('客戶新增成功！');
        });
        
        // 搜尋客戶
        document.getElementById('search-users').addEventListener('input', function(e) {
            const searchTerm = e.target.value.toLowerCase();
            filteredUsers = users.filter(user => 
                user.name.toLowerCase().includes(searchTerm)
            );
            renderUserList();
        });
        
        // 渲染客戶列表
        function renderUserList() {
            const userList = document.getElementById('user-list');
            const displayUsers = filteredUsers.length > 0 || document.getElementById('search-users').value ? filteredUsers : users;
            
            if (displayUsers.length === 0) {
                userList.innerHTML = `
                    <div class="empty-state">
                        <h3>🔍 ${document.getElementById('search-users').value ? '找不到符合的客戶' : '尚未新增任何客戶'}</h3>
                        <p>${document.getElementById('search-users').value ? '請嘗試其他搜尋關鍵字' : '點擊上方「新增客戶」按鈕開始使用'}</p>
                    </div>
                `;
                return;
            }
            
            userList.innerHTML = displayUsers.map(user => {
                const userRecords = records.filter(r => r.userId === user.id);
                const latestRecord = userRecords.sort((a, b) => new Date(b.date) - new Date(a.date))[0];
                
                return `
                    <div class="user-card" onclick="selectUser(${user.id})">
                        <div class="user-actions">
                            <button onclick="event.stopPropagation(); editUser(${user.id})">✏️</button>
                            <button onclick="event.stopPropagation(); deleteUser(${user.id})">🗑️</button>
                        </div>
                        <h3>${user.name}</h3>
                        <p>👤 ${user.gender === 'male' ? '男性' : '女性'} | 🎂 ${user.age}歲 | 📏 ${user.height}cm</p>
                        <p>📅 建立於: ${user.createdAt}</p>
                        <div class="user-stats">
                            <p>📊 記錄次數: ${userRecords.length}</p>
                            ${latestRecord ? `<p>⏰ 最後記錄: ${latestRecord.date}</p>` : ''}
                            ${latestRecord && latestRecord.weight ? `<p>⚖️ 最新體重: ${latestRecord.weight}kg</p>` : ''}
                        </div>
                    </div>
                `;
            }).join('');
        }
        
        // 選擇客戶
        function selectUser(userId) {
            currentUser = users.find(u => u.id === userId);
            document.getElementById('user-info').innerHTML = `
                <h2>📊 ${currentUser.name} 的數據記錄</h2>
                <p>👤 ${currentUser.gender === 'male' ? '男性' : '女性'} | 🎂 ${currentUser.age}歲 | 📏 ${currentUser.height}cm</p>
            `;
            
            // 設置今天的日期
            document.getElementById('record-date').value = new Date().toISOString().split('T')[0];
            
            showScreen('data-entry-screen');
        }
        
        // 刪除客戶
        function deleteUser(userId) {
            if (confirm('確定要刪除此客戶？這將同時刪除所有相關記錄。')) {
                users = users.filter(u => u.id !== userId);
                records = records.filter(r => r.userId !== userId);
                updateStats();
                renderUserList();
            }
        }
        
        // 編輯客戶
        function editUser(userId) {
            const user = users.find(u => u.id === userId);
            const newName = prompt('修改姓名:', user.name);
            if (newName && newName.trim()) {
                user.name = newName.trim();
                renderUserList();
            }
        }
        
        
        
        // 儲存數據
        document.getElementById('data-form').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const formData = new FormData(e.target);
            const recordData = {
                id: Date.now(),
                userId: currentUser.id,
                date: formData.get('date'),
                weight: parseFloat(formData.get('weight')) || null,
                bmi: parseFloat(formData.get('bmi')) || null,
                muscleMass: parseFloat(formData.get('muscleMass')) || null,
                bodyFat: parseFloat(formData.get('bodyFat')) || null,
                boneMass: parseFloat(formData.get('boneMass')) || null,
                bodyAge: parseInt(formData.get('bodyAge')) || null,
                metabolism: parseInt(formData.get('metabolism')) || null,
                visceralFat: parseFloat(formData.get('visceralFat')) || null,
                bodyWater: parseFloat(formData.get('bodyWater')) || null,
                createdAt: new Date().toLocaleString('zh-TW')
            };
            
            // 檢查是否已有同日期記錄
            const existingIndex = records.findIndex(r => r.userId === currentUser.id && r.date === recordData.date);
            if (existingIndex !== -1) {
                if (confirm('此日期已有記錄，是否要覆蓋？')) {
                    records[existingIndex] = recordData;
                } else {
                    return;
                }
            } else {
                records.push(recordData);
            }
            
            // 顯示成功訊息
            const successMessage = document.getElementById('success-message');
            successMessage.innerHTML = `✅ 數據已成功儲存！記錄日期: ${recordData.date}`;
            successMessage.style.display = 'block';
            
            // 清空表單
            e.target.reset();
            document.getElementById('record-date').value = new Date().toISOString().split('T')[0];
            
            // 3秒後隱藏成功訊息
            setTimeout(() => {
                successMessage.style.display = 'none';
            }, 3000);
        });
        
        // 查看記錄
        function showRecords() {
            const recordsSection = document.getElementById('records-section');
            const recordsList = document.getElementById('records-list');
            
            const userRecords = records.filter(r => r.userId === currentUser.id)
                                     .sort((a, b) => new Date(b.date) - new Date(a.date));
            
            if (userRecords.length === 0) {
                recordsList.innerHTML = '<p style="color: #666;">尚無記錄數據。</p>';
            } else {
                recordsList.innerHTML = userRecords.map(record => `
                    <div class="record-item">
                        <div class="record-actions">
                            <button class="btn btn-small btn-danger" onclick="deleteRecord(${record.id})">🗑️</button>
                        </div>
                        <div class="record-date">${record.date}</div>
                        <div class="record-data">
                            ${record.weight ? `⚖️ 體重: ${record.weight}kg` : ''}
                            ${record.bmi ? ` | 📊 BMI: ${record.bmi}` : ''}
                            ${record.bodyFat ? ` | 🧈 體脂肪: ${record.bodyFat}%` : ''}
                            ${record.muscleMass ? ` | 💪 肌肉量: ${record.muscleMass}kg` : ''}
                            ${record.boneMass ? ` | 🦴 骨量: ${record.boneMass}kg` : ''}
                            ${record.bodyAge ? ` | 🎂 身體年齡: ${record.bodyAge}歲` : ''}
                            ${record.metabolism ? ` | 🔥 代謝: ${record.metabolism}kcal` : ''}
                            ${record.visceralFat ? ` | 🫀 內臟脂肪: ${record.visceralFat}` : ''}
                            ${record.bodyWater ? ` | 💧 身體水分率: ${record.bodyWater}%` : ''}
                        </div>
                    </div>
                `).join('');
            }
            
            recordsSection.style.display = recordsSection.style.display === 'none' ? 'block' : 'none';
        }
        
        // 刪除記錄
        function deleteRecord(recordId) {
            if (confirm('確定要刪除此記錄？')) {
                records = records.filter(r => r.id !== recordId);
                showRecords(); // 重新渲染記錄列表
            }
        }
        
        // 初始化
        document.addEventListener('DOMContentLoaded', function() {
            // 設置今天的日期為默認值
            document.getElementById('record-date').value = new Date().toISOString().split('T')[0];
            
            // 初始化數據
            filteredUsers = users;
            updateStats();
            renderUserList();
        });
    </script>
</body>
</html>
