<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Soundcore 支持 - 产品手册 (云端同步版)</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', sans-serif;
            color: #333; background-color: #f5f7fa; line-height: 1.6;
        }
        /* 顶部编辑工具栏 */
        .edit-toolbar {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            padding: 12px 24px; box-shadow: 0 2px 12px rgba(0, 0, 0, 0.15);
            position: sticky; top: 0; z-index: 2000;
            display: flex; align-items: center; gap: 12px; flex-wrap: wrap;
        }
        .edit-toolbar button {
            background-color: rgba(255, 255, 255, 0.2); color: #fff;
            border: 1px solid rgba(255, 255, 255, 0.3); padding: 8px 16px;
            border-radius: 6px; cursor: pointer; font-size: 13px; transition: all 0.3s;
            display: flex; align-items: center; gap: 6px;
        }
        .edit-toolbar button:hover { background-color: rgba(255, 255, 255, 0.3); transform: translateY(-1px); }
        .edit-toolbar button:disabled { opacity: 0.5; cursor: not-allowed; }
        .edit-toolbar .mode-indicator {
            margin-left: auto; color: #fff; font-size: 13px;
            padding: 8px 16px; background-color: rgba(255, 255, 255, 0.2); border-radius: 6px;
        }
        .sync-status { display: inline-flex; align-items: center; gap: 6px; }
        .sync-dot {
            width: 8px; height: 8px; border-radius: 50%; background-color: #4ade80;
            animation: pulse 2s infinite;
        }
        @keyframes pulse { 0%, 100% { opacity: 1; } 50% { opacity: 0.5; } }

        /* 头部导航 */
        header { background-color: #fff; box-shadow: 0 2px 8px rgba(0, 0, 0, 0.06); position: sticky; top: 48px; z-index: 1000; }
        .header-container { max-width: 1400px; margin: 0 auto; padding: 16px 32px; display: flex; align-items: center; justify-content: space-between; }
        .logo { display: flex; align-items: center; gap: 12px; }
        .logo-text {
            font-size: 26px; font-weight: 700;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
        }
        .logo-sub { font-size: 13px; color: #666; font-weight: 400; }
        nav { display: flex; gap: 32px; }
        nav a { color: #666; text-decoration: none; font-size: 14px; transition: color 0.3s; padding: 8px 12px; border-radius: 4px; }
        nav a:hover { color: #667eea; background-color: #f5f7fa; }

        /* 主要内容区 */
        .main-container { max-width: 1400px; margin: 32px auto; padding: 0 32px; display: grid; grid-template-columns: 280px 1fr; gap: 32px; }
        /* 侧边栏 */
        .sidebar { background-color: #fff; border-radius: 12px; padding: 24px; height: fit-content; box-shadow: 0 2px 12px rgba(0, 0, 0, 0.06); position: sticky; top: 120px; }
        .sidebar h3 { font-size: 17px; margin-bottom: 20px; color: #222; font-weight: 600; }
        .sidebar ul { list-style: none; }
        .sidebar li { margin-bottom: 8px; }
        .sidebar a { color: #666; text-decoration: none; font-size: 14px; display: block; padding: 10px 14px; border-radius: 8px; transition: all 0.3s; }
        .sidebar a:hover { background-color: #f5f7fa; color: #667eea; padding-left: 18px; }
        .sidebar a.active { background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: #fff; font-weight: 500; }

        /* 内容区域 */
        .content { background-color: #fff; border-radius: 12px; padding: 48px; box-shadow: 0 2px 12px rgba(0, 0, 0, 0.06); min-height: 600px; }
        .content[contenteditable="true"] { outline: 2px dashed #667eea; outline-offset: -2px; }
        .content h1 { font-size: 36px; margin-bottom: 12px; color: #1a1a1a; font-weight: 700; }
        .content .subtitle { color: #666; font-size: 15px; margin-bottom: 32px; padding-bottom: 20px; border-bottom: 2px solid #f0f0f0; }
        .content h2 { font-size: 26px; margin-top: 40px; margin-bottom: 20px; color: #222; font-weight: 600; border-left: 4px solid #667eea; padding-left: 16px; }
        .content h2:first-of-type { margin-top: 24px; }
        .content h3 { font-size: 20px; margin-top: 28px; margin-bottom: 14px; color: #333; font-weight: 600; }
        .content p, .content li { margin-bottom: 18px; font-size: 15px; color: #555; line-height: 1.8; }
        .content ul, .content ol { margin-left: 28px; margin-bottom: 18px; }
        .content strong { color: #333; font-weight: 600; }

        /* 信息卡片 */
        .info-card { background: linear-gradient(135deg, #f5f7ff 0%, #e8ebff 100%); border-left: 4px solid #667eea; padding: 20px 24px; margin: 28px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(102, 126, 234, 0.1); }
        .info-card h4 { font-size: 16px; margin-bottom: 10px; color: #667eea; font-weight: 600; }
        .info-card p { margin-bottom: 0; font-size: 14px; color: #555; }

        /* 按钮样式 */
        .btn { display: inline-block; padding: 14px 28px; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: #fff; text-decoration: none; border-radius: 8px; font-size: 14px; font-weight: 500; transition: all 0.3s; border: none; cursor: pointer; box-shadow: 0 4px 12px rgba(102, 126, 234, 0.3); }
        .btn:hover { transform: translateY(-2px); box-shadow: 0 6px 20px rgba(102, 126, 234, 0.4); }
        
        /* 表格 */
        table { width: 100%; border-collapse: collapse; margin: 28px 0; border-radius: 8px; overflow: hidden; box-shadow: 0 2px 8px rgba(0, 0, 0, 0.06); }
        th, td { padding: 14px 16px; text-align: left; border-bottom: 1px solid #f0f0f0; }
        th { background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: #fff; font-weight: 600; font-size: 14px; }
        td { font-size: 14px; color: #555; background-color: #fff; }
        tr:hover td { background-color: #f9fafb; }

        /* 媒体 */
        .content img, .content video { max-width: 100%; height: auto; border-radius: 12px; margin: 24px 0; box-shadow: 0 4px 16px rgba(0, 0, 0, 0.1); display: block; }

        /* 响应式 */
        @media (max-width: 1024px) { .main-container { grid-template-columns: 1fr; } .sidebar { position: static; } nav { display: none; } }
        @media (max-width: 768px) { .content { padding: 28px 20px; } .edit-toolbar { top: 0; } header { top: 48px; } }

        /* 页脚 */
        footer { background-color: #fff; margin-top: 48px; padding: 40px 32px; text-align: center; box-shadow: 0 -2px 12px rgba(0, 0, 0, 0.06); }
        footer p { color: #999; font-size: 13px; }

        #imageInput, #videoInput { display: none; }
        
        /* 编辑提示 */
        .edit-hint { background: #fffbea; border: 1px solid #ffd666; border-radius: 8px; padding: 12px 16px; margin-bottom: 20px; color: #8c6d1f; font-size: 13px; display: none; }
        .edit-mode .edit-hint { display: block; }

        /* Firebase 配置提示 */
        .firebase-config-notice { background: linear-gradient(135deg, #fef3c7 0%, #fde68a 100%); border: 2px solid #f59e0b; border-radius: 12px; padding: 20px 24px; margin: 20px 0; box-shadow: 0 4px 12px rgba(245, 158, 11, 0.2); }
        .firebase-config-notice h3 { color: #92400e; font-size: 18px; margin-bottom: 12px; }
        .firebase-config-notice p { color: #78350f; font-size: 14px; line-height: 1.6; }
        .firebase-config-notice code { background: #fff; padding: 2px 6px; border-radius: 4px; font-family: 'Courier New', monospace; color: #dc2626; }
    </style>
</head>
<body>
    <!-- 编辑工具栏 -->
    <div class="edit-toolbar">
        <button onclick="toggleEditMode()" id="editModeBtn"><span>✏️</span> 开启编辑模式</button>
        <button onclick="formatText('bold')"><span>B</span> 加粗</button>
        <button onclick="formatText('italic')"><span>I</span> 斜体</button>
        <button onclick="addHeading('h2')"><span>H2</span> 标题2</button>
        <button onclick="addHeading('h3')"><span>H3</span> 标题3</button>
        <button onclick="insertImage()"><span>🖼️</span> 插入图片</button>
        <button onclick="insertVideo()"><span>🎬</span> 插入视频</button>
        <button onclick="addInfoCard()"><span>💡</span> 添加提示卡片</button>
        <button onclick="addTable()"><span>📊</span> 插入表格</button>
        <button onclick="saveContent()"><span>💾</span> 导出HTML</button>
        <button onclick="resetContent()"><span>🔄</span> 恢复默认</button>
        <div class="mode-indicator" id="modeIndicator">
            查看模式 | <span class="sync-status"><span class="sync-dot"></span><span id="syncStatus">未连接</span></span>
        </div>
    </div>

    <input type="file" id="imageInput" accept="image/*" onchange="handleImageUpload(event)">
    <input type="file" id="videoInput" accept="video/*" onchange="handleVideoUpload(event)">

    <!-- 头部导航 -->
    <header>
        <div class="header-container">
            <div class="logo">
                <div>
                    <div class="logo-text">soundcore</div>
                    <div class="logo-sub">Support Center - Cloud Sync</div>
                </div>
            </div>
            <nav>
                <a href="#">支持中心</a>
                <a href="#">产品手册</a>
                <a href="#">下载中心</a>
                <a href="#">常见问题</a>
                <a href="#">联系我们</a>
            </nav>
        </div>
    </header>

    <!-- 主要内容 -->
    <div class="main-container">
        <!-- 侧边栏 -->
        <aside class="sidebar">
            <h3>产品手册导航</h3>
            <ul>
                <li><a href="#overview" class="active">产品概述</a></li>
                <li><a href="#firebase-setup">Firebase 配置</a></li>
                <li><a href="#specs">技术规格</a></li>
                <li><a href="#setup">快速设置</a></li>
                <li><a href="#features">功能特性</a></li>
                <li><a href="#controls">按键说明</a></li>
                <li><a href="#app">APP使用</a></li>
                <li><a href="#troubleshooting">故障排除</a></li>
                <li><a href="#support">技术支持</a></li>
            </ul>
        </aside>

        <!-- 内容区域 -->
        <main class="content" id="editableContent">
            <div class="edit-hint">
                💡 编辑模式已开启：所有修改会自动同步到云端，所有设备实时更新！
            </div>

            <h1>Soundcore 云端同步版</h1>
            <p class="subtitle">支持全平台实时同步 | 配置 Firebase 后即可使用</p>

            <div class="firebase-config-notice" id="configNotice">
                <h3>🔥 Firebase 配置说明</h3>
                <p><strong>当前状态：</strong>需要配置 Firebase 才能可用云端同步功能</p>
                <p style="margin-top: 12px;"><strong>配置步骤：</strong></p>
                <ol style="margin-left: 20px; margin-top: 8px;">
                    <li>访问 <a href="https://console.firebase.google.com" target="_blank" style="color: #2563eb; text-decoration: underline;">Firebase Console</a></li>
                    <li>创建新项目（或使用现有项目）</li>
                    <li>在项目设置中找到 <code>firebaseConfig</code></li>
                    <li>复制配置对象，替换下方脚本中的配置</li>
                    <li>启用 Realtime Database（测试模式开启）</li>
                </ol>
            </div>

            <h2 id="overview">功能特性</h2>
            <p>本页面支持以下功能：</p>
            <ul>
                <li>✅ 全平台实时同步（手机、平板、电脑）</li>
                <li>✅ 毫秒级数据更新</li>
                <li>✅ 自动冲突解决</li>
                <li>✅ 离线编辑支持（联网后自动同步）</li>
                <li>✅ 完整的富文本编辑功能</li>
                <li>✅ 图片和视频支持</li>
            </ul>

            <h2 id="firebase-setup">Firebase 配置教程</h2>
            <h3>1. 创建 Firebase 项目</h3>
            <p>访问 Firebase Console，点击"添加项目"，按照提示完成创建。</p>
            <h3>2. 获取配置信息</h3>
            <p>在项目概览页面，点击网页图标 (</>)，复制 firebaseConfig 配置对象。</p>

            <h2 id="specs">使用说明</h2>
            <table>
                <thead>
                    <tr>
                        <th>功能</th>
                        <th>说明</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>自动同步</td>
                        <td>编辑后 1 秒自动同步到云端</td>
                    </tr>
                    <tr>
                        <td>实时更新</td>
                        <td>其他设备的修改会立即显示</td>
                    </tr>
                </tbody>
            </table>
            <p>
                <a href="#" class="btn" onclick="alert('请先完成 Firebase 配置'); return false;">开始配置</a>
            </p>
        </main>
    </div>

    <footer>
        <p>&copy; 2024 Soundcore. All Rights Reserved. | 云端同步版本 v1.0</p>
    </footer>

    <!-- Firebase SDK -->
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <script>
                // ============================================
        // Firebase 配置区域 - 已替换为你自己的配置
        // ============================================
        const firebaseConfig = {
            apiKey: "AIzaSyCaytyZix2KpGjDIB0Q54QVRRMq_G1N72E",
            authDomain: "soundcore-sync.firebaseapp.com",
            // 下面这一行是你之前的截图里找到的，非常重要！
            databaseURL: "https://soundcore-sync-default-rtdb.asia-southeast1.firebasedatabase.app",
            projectId: "soundcore-sync",
            storageBucket: "soundcore-sync.firebasestorage.app",
            messagingSenderId: "729835191028",
            appId: "1:729835191028:web:b9bd034acc6d0ae399bca1",
            measurementId: "G-S7ZLFZJLTS"
        };

        // ============================================
        // 应用逻辑
        // ============================================
        let isEditMode = false;
        let isFirebaseConfigured = false;
        let database = null;
        let contentRef = null;
        let isSyncing = false;
        let autoSaveTimer = null;

        const content = document.getElementById('editableContent');
        const editModeBtn = document.getElementById('editModeBtn');
        const syncStatus = document.getElementById('syncStatus');
        const STORAGE_KEY = 'soundcore_page_content_backup';
        const DEFAULT_CONTENT_KEY = 'soundcore_default_content';

        function checkFirebaseConfig() {
            return firebaseConfig.apiKey !== "YOUR_API_KEY";
        }

        function initFirebase() {
            if (!checkFirebaseConfig()) {
                console.warn('Firebase 未配置，使用本地存储模式');
                syncStatus.textContent = '本地模式';
                return false;
            }
            try {
                firebase.initializeApp(firebaseConfig);
                database = firebase.database();
                contentRef = database.ref('soundcore/content');
                isFirebaseConfigured = true;

                contentRef.on('value', (snapshot) => {
                    const data = snapshot.val();
                    if (data && data.html && !isSyncing) {
                        content.innerHTML = data.html;
                        console.log('已从云端同步内容');
                    }
                });

                const connectedRef = database.ref('.info/connected');
                connectedRef.on('value', (snapshot) => {
                    if (snapshot.val() === true) {
                        syncStatus.textContent = '已连接';
                        syncStatus.parentElement.querySelector('.sync-dot').style.backgroundColor = '#4ade80';
                        document.getElementById('configNotice')?.remove();
                    } else {
                        syncStatus.textContent = '离线';
                        syncStatus.parentElement.querySelector('.sync-dot').style.backgroundColor = '#f87171';
                    }
                });
                return true;
            } catch (error) {
                console.error('Firebase 初始化失败:', error);
                syncStatus.textContent = '配置错误';
                return false;
            }
        }

        window.addEventListener('DOMContentLoaded', function() {
            if (!localStorage.getItem(DEFAULT_CONTENT_KEY)) {
                localStorage.setItem(DEFAULT_CONTENT_KEY, content.innerHTML);
            }
            initFirebase();
            if (!isFirebaseConfigured) {
                const savedContent = localStorage.getItem(STORAGE_KEY);
                if (savedContent) {
                    content.innerHTML = savedContent;
                }
            }
        });

        function syncToCloud() {
            if (!isFirebaseConfigured || !contentRef) {
                localStorage.setItem(STORAGE_KEY, content.innerHTML);
                return;
            }
            clearTimeout(autoSaveTimer);
            syncStatus.textContent = '同步中...';
            autoSaveTimer = setTimeout(() => {
                isSyncing = true;
                contentRef.set({
                    html: content.innerHTML,
                    timestamp: Date.now()
                }).then(() => {
                    syncStatus.textContent = '已同步';
                    localStorage.setItem(STORAGE_KEY, content.innerHTML);
                    setTimeout(() => { isSyncing = false; syncStatus.textContent = '已连接'; }, 500);
                }).catch((error) => {
                    syncStatus.textContent = '同步失败';
                    isSyncing = false;
                    localStorage.setItem(STORAGE_KEY, content.innerHTML);
                });
            }, 1000);
        }

        content.addEventListener('input', syncToCloud);
        content.addEventListener('DOMSubtreeModified', function(e) {
            if (!isSyncing) syncToCloud();
        });

        function toggleEditMode() {
            isEditMode = !isEditMode;
            content.contentEditable = isEditMode;
            if (isEditMode) {
                document.body.classList.add('edit-mode');
                editModeBtn.innerHTML = '<span>👁️</span> 退出编辑';
            } else {
                document.body.classList.remove('edit-mode');
                editModeBtn.innerHTML = '<span>✏️</span> 开启编辑模式';
            }
        }

        function resetContent() {
            if (confirm('确定要恢复到默认内容吗？当前的修改将会丢失。')) {
                const defaultContent = localStorage.getItem(DEFAULT_CONTENT_KEY);
                if (defaultContent) {
                    content.innerHTML = defaultContent;
                    syncToCloud();
                }
            }
        }

        function formatText(command) {
            if (!isEditMode) return alert('请先开启编辑模式');
            document.execCommand(command, false, null);
        }
        
        function addHeading(tag) {
            if (!isEditMode) return alert('请先开启编辑模式');
            const selection = window.getSelection();
            if (selection.rangeCount > 0) {
                const range = selection.getRangeAt(0);
                const heading = document.createElement(tag);
                heading.textContent = selection.toString() || '新标题';
                range.deleteContents();
                range.insertNode(heading);
                syncToCloud();
            }
        }

        function insertImage() { if (!isEditMode) return alert('请先开启编辑模式'); document.getElementById('imageInput').click(); }
        function handleImageUpload(event) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    const img = document.createElement('img');
                    img.src = e.target.result;
                    content.appendChild(img);
                    syncToCloud();
                };
                reader.readAsDataURL(file);
            }
        }

        function insertVideo() { if (!isEditMode) return alert('请先开启编辑模式'); document.getElementById('videoInput').click(); }
        function handleVideoUpload(event) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    const video = document.createElement('video');
                    video.src = e.target.result; video.controls = true;
                    content.appendChild(video);
                    syncToCloud();
                };
                reader.readAsDataURL(file);
            }
        }

        function addInfoCard() {
            if (!isEditMode) return alert('请先开启编辑模式');
            const card = document.createElement('div');
            card.className = 'info-card';
            card.innerHTML = '<h4>💡 提示标题</h4><p>在这里输入提示内容...</p>';
            content.appendChild(card);
            syncToCloud();
        }

        function addTable() {
            if (!isEditMode) return alert('请先开启编辑模式');
            const table = document.createElement('table');
            table.innerHTML = '<thead><tr><th>列1</th><th>列2</th></tr></thead><tbody><tr><td>数据1</td><td>数据2</td></tr></tbody>';
            content.appendChild(table);
            syncToCloud();
        }

        function saveContent() {
            const htmlContent = content.innerHTML;
            const blob = new Blob([htmlContent], { type: 'text/html' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url; a.download = 'soundcore_content.html';
            a.click(); URL.revokeObjectURL(url);
        }
        
        // 侧边栏导航
         document.querySelectorAll('.sidebar a').forEach(anchor => {
            anchor.addEventListener('click', function(e) {
                const href = this.getAttribute('href');
                if(href.startsWith('#')) {
                    e.preventDefault();
                    const targetId = href.substring(1);
                    const targetElement = document.getElementById(targetId);
                    if (targetElement) {
                        targetElement.scrollIntoView({ behavior: 'smooth', block: 'start' });
                        document.querySelectorAll('.sidebar a').forEach(a => a.classList.remove('active'));
                        this.classList.add('active');
                    }
                }
            });
        });
    </script>
</body>
</html>
