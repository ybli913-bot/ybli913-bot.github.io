# ybli913-bot.github.io
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Soundcore 支持 - 产品手册</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', sans-serif;
            color: #333;
            background-color: #f5f7fa;
            line-height: 1.6;
        }

        /* 顶部编辑工具栏 */
        .edit-toolbar {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            padding: 12px 24px;
            box-shadow: 0 2px 12px rgba(0, 0, 0, 0.15);
            position: sticky;
            top: 0;
            z-index: 2000;
            display: flex;
            align-items: center;
            gap: 12px;
            flex-wrap: wrap;
        }

        .edit-toolbar button {
            background-color: rgba(255, 255, 255, 0.2);
            color: #fff;
            border: 1px solid rgba(255, 255, 255, 0.3);
            padding: 8px 16px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 13px;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .edit-toolbar button:hover {
            background-color: rgba(255, 255, 255, 0.3);
            transform: translateY(-1px);
        }

        .edit-toolbar .mode-indicator {
            margin-left: auto;
            color: #fff;
            font-size: 13px;
            padding: 8px 16px;
            background-color: rgba(255, 255, 255, 0.2);
            border-radius: 6px;
        }

        /* 头部导航 */
        header {
            background-color: #fff;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.06);
            position: sticky;
            top: 48px;
            z-index: 1000;
        }

        .header-container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 16px 32px;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .logo-text {
            font-size: 26px;
            font-weight: 700;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .logo-sub {
            font-size: 13px;
            color: #666;
            font-weight: 400;
        }

        nav {
            display: flex;
            gap: 32px;
        }

        nav a {
            color: #666;
            text-decoration: none;
            font-size: 14px;
            transition: color 0.3s;
            padding: 8px 12px;
            border-radius: 4px;
        }

        nav a:hover {
            color: #667eea;
            background-color: #f5f7fa;
        }

        /* 主要内容区 */
        .main-container {
            max-width: 1400px;
            margin: 32px auto;
            padding: 0 32px;
            display: grid;
            grid-template-columns: 280px 1fr;
            gap: 32px;
        }

        /* 侧边栏 */
        .sidebar {
            background-color: #fff;
            border-radius: 12px;
            padding: 24px;
            height: fit-content;
            box-shadow: 0 2px 12px rgba(0, 0, 0, 0.06);
            position: sticky;
            top: 120px;
        }

        .sidebar h3 {
            font-size: 17px;
            margin-bottom: 20px;
            color: #222;
            font-weight: 600;
        }

        .sidebar ul {
            list-style: none;
        }

        .sidebar li {
            margin-bottom: 8px;
        }

        .sidebar a {
            color: #666;
            text-decoration: none;
            font-size: 14px;
            display: block;
            padding: 10px 14px;
            border-radius: 8px;
            transition: all 0.3s;
        }

        .sidebar a:hover {
            background-color: #f5f7fa;
            color: #667eea;
            padding-left: 18px;
        }

        .sidebar a.active {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: #fff;
            font-weight: 500;
        }

        /* 内容区域 */
        .content {
            background-color: #fff;
            border-radius: 12px;
            padding: 48px;
            box-shadow: 0 2px 12px rgba(0, 0, 0, 0.06);
            min-height: 600px;
        }

        .content[contenteditable="true"] {
            outline: 2px dashed #667eea;
            outline-offset: -2px;
        }

        .content h1 {
            font-size: 36px;
            margin-bottom: 12px;
            color: #1a1a1a;
            font-weight: 700;
        }

        .content .subtitle {
            color: #666;
            font-size: 15px;
            margin-bottom: 32px;
            padding-bottom: 20px;
            border-bottom: 2px solid #f0f0f0;
        }

        .content h2 {
            font-size: 26px;
            margin-top: 40px;
            margin-bottom: 20px;
            color: #222;
            font-weight: 600;
            border-left: 4px solid #667eea;
            padding-left: 16px;
        }

        .content h2:first-of-type {
            margin-top: 24px;
        }

        .content h3 {
            font-size: 20px;
            margin-top: 28px;
            margin-bottom: 14px;
            color: #333;
            font-weight: 600;
        }

        .content p {
            margin-bottom: 18px;
            font-size: 15px;
            color: #555;
            line-height: 1.8;
        }

        .content ul, .content ol {
            margin-left: 28px;
            margin-bottom: 18px;
        }

        .content li {
            margin-bottom: 10px;
            font-size: 15px;
            color: #555;
            line-height: 1.8;
        }

        .content strong {
            color: #333;
            font-weight: 600;
        }

        /* 信息卡片 */
        .info-card {
            background: linear-gradient(135deg, #f5f7ff 0%, #e8ebff 100%);
            border-left: 4px solid #667eea;
            padding: 20px 24px;
            margin: 28px 0;
            border-radius: 8px;
            box-shadow: 0 2px 8px rgba(102, 126, 234, 0.1);
        }

        .info-card h4 {
            font-size: 16px;
            margin-bottom: 10px;
            color: #667eea;
            font-weight: 600;
        }

        .info-card p {
            margin-bottom: 0;
            font-size: 14px;
            color: #555;
        }

        /* 按钮样式 */
        .btn {
            display: inline-block;
            padding: 14px 28px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: #fff;
            text-decoration: none;
            border-radius: 8px;
            font-size: 14px;
            font-weight: 500;
            transition: all 0.3s;
            border: none;
            cursor: pointer;
            box-shadow: 0 4px 12px rgba(102, 126, 234, 0.3);
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(102, 126, 234, 0.4);
        }

        .btn-secondary {
            background: #fff;
            color: #667eea;
            border: 2px solid #667eea;
            box-shadow: none;
        }

        .btn-secondary:hover {
            background-color: #f5f7ff;
        }

        /* 表格 */
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 28px 0;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.06);
        }

        th, td {
            padding: 14px 16px;
            text-align: left;
            border-bottom: 1px solid #f0f0f0;
        }

        th {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: #fff;
            font-weight: 600;
            font-size: 14px;
        }

        td {
            font-size: 14px;
            color: #555;
            background-color: #fff;
        }

        tr:hover td {
            background-color: #f9fafb;
        }

        /* 图片样式 */
        .content img {
            max-width: 100%;
            height: auto;
            border-radius: 12px;
            margin: 24px 0;
            box-shadow: 0 4px 16px rgba(0, 0, 0, 0.1);
            display: block;
        }

        /* 视频样式 */
        .content video {
            max-width: 100%;
            height: auto;
            border-radius: 12px;
            margin: 24px 0;
            box-shadow: 0 4px 16px rgba(0, 0, 0, 0.1);
            display: block;
        }

        /* 媒体占位符 */
        .media-placeholder {
            background: #f5f7fa;
            border: 2px dashed #ccc;
            border-radius: 12px;
            padding: 40px;
            text-align: center;
            margin: 24px 0;
            cursor: pointer;
            transition: all 0.3s;
        }

        .media-placeholder:hover {
            background: #e8ebff;
            border-color: #667eea;
        }

        .media-placeholder p {
            color: #999;
            margin: 0;
        }

        /* 响应式设计 */
        @media (max-width: 1024px) {
            .main-container {
                grid-template-columns: 1fr;
            }

            .sidebar {
                position: static;
            }

            nav {
                display: none;
            }
        }

        @media (max-width: 768px) {
            .content {
                padding: 28px 20px;
            }

            .content h1 {
                font-size: 28px;
            }

            .content h2 {
                font-size: 22px;
            }

            .edit-toolbar {
                top: 0;
            }

            header {
                top: 48px;
            }
        }

        /* 页脚 */
        footer {
            background-color: #fff;
            margin-top: 48px;
            padding: 40px 32px;
            text-align: center;
            box-shadow: 0 -2px 12px rgba(0, 0, 0, 0.06);
        }

        footer p {
            color: #999;
            font-size: 13px;
        }

        /* 文件上传隐藏输入 */
        #imageInput, #videoInput {
            display: none;
        }

        /* 编辑提示 */
        .edit-hint {
            background: #fffbea;
            border: 1px solid #ffd666;
            border-radius: 8px;
            padding: 12px 16px;
            margin-bottom: 20px;
            color: #8c6d1f;
            font-size: 13px;
            display: none;
        }

        .edit-mode .edit-hint {
            display: block;
        }
    </style>
</head>
<body>
    <!-- 编辑工具栏 -->
    <div class="edit-toolbar">
        <button onclick="toggleEditMode()" id="editModeBtn">
            <span>✏️</span> 开启编辑模式
        </button>
        <button onclick="formatText('bold')">
            <span>B</span> 加粗
        </button>
        <button onclick="formatText('italic')">
            <span>I</span> 斜体
        </button>
        <button onclick="addHeading('h2')">
            <span>H2</span> 标题2
        </button>
        <button onclick="addHeading('h3')">
            <span>H3</span> 标题3
        </button>
        <button onclick="insertImage()">
            <span>🖼️</span> 插入图片
        </button>
        <button onclick="insertVideo()">
            <span>🎬</span> 插入视频
        </button>
        <button onclick="addInfoCard()">
            <span>💡</span> 添加提示卡片
        </button>
        <button onclick="addTable()">
            <span>📊</span> 插入表格
        </button>
        <button onclick="saveContent()">
            <span>💾</span> 保存内容
        </button>
        <div class="mode-indicator" id="modeIndicator">查看模式</div>
    </div>

    <!-- 隐藏的文件上传输入 -->
    <input type="file" id="imageInput" accept="image/*" onchange="handleImageUpload(event)">
    <input type="file" id="videoInput" accept="video/*" onchange="handleVideoUpload(event)">

    <!-- 头部导航 -->
    <header>
        <div class="header-container">
            <div class="logo">
                <div>
                    <div class="logo-text">soundcore</div>
                    <div class="logo-sub">Support Center</div>
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
                <li><a href="#unboxing">开箱指南</a></li>
                <li><a href="#specs">技术规格</a></li>
                <li><a href="#setup">快速设置</a></li>
                <li><a href="#features">功能特性</a></li>
                <li><a href="#controls">按键说明</a></li>
                <li><a href="#app">APP使用</a></li>
                <li><a href="#troubleshooting">故障排除</a></li>
                <li><a href="#care">保养维护</a></li>
                <li><a href="#support">技术支持</a></li>
            </ul>
        </aside>

        <!-- 内容区域 -->
        <main class="content" id="editableContent">
            <div class="edit-hint">
                💡 编辑模式已开启：点击任意文字可直接编辑，使用工具栏添加图片、视频等内容
            </div>

            <h1>Soundcore Life Q30 使用手册</h1>
            <p class="subtitle">型号: D1301 | 主动降噪无线耳机</p>

            <div class="info-card">
                <h4>⚠️ 开始使用前请阅读</h4>
                <p>在使用产品之前，请仔细阅读本手册的安全须知和使用说明，以确保正确使用产品并获得最佳体验。</p>
            </div>

            <h2 id="overview">产品概述</h2>
            <p>感谢您选择 Soundcore Life Q30 主动降噪无线耳机。Life Q30 采用先进的混合式主动降噪技术，配备 40mm 动圈单元，支持 LDAC 高清音频编码，为您带来沉浸式的音频体验。</p>

            <p><strong>主要特点：</strong></p>
            <ul>
                <li>混合式主动降噪技术，降噪深度可达 95%</li>
                <li>3 种降噪模式：交通、室内、户外</li>
                <li>40 小时超长续航（ANC 开启）</li>
                <li>支持 LDAC 高清音频编码</li>
                <li>多点连接，可同时连接 2 台设备</li>
                <li>舒适的蛋白皮耳罩设计</li>
            </ul>

            <h2 id="unboxing">包装清单</h2>
            <p>请确认您的包装内包含以下物品：</p>
            <ul>
                <li>Soundcore Life Q30 耳机 × 1</li>
                <li>USB-C 充电线 × 1</li>
                <li>3.5mm 音频线 × 1</li>
                <li>便携收纳包 × 1</li>
                <li>快速入门指南 × 1</li>
                <li>安全卡片 × 1</li>
            </ul>

            <h2 id="specs">技术规格</h2>
            <table>
                <thead>
                    <tr>
                        <th>规格项目</th>
                        <th>参数详情</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>产品型号</td>
                        <td>D1301</td>
                    </tr>
                    <tr>
                        <td>蓝牙版本</td>
                        <td>5.0</td>
                    </tr>
                    <tr>
                        <td>蓝牙编码</td>
                        <td>LDAC, AAC, SBC</td>
                    </tr>
                    <tr>
                        <td>驱动单元</td>
                        <td>40mm 动圈单元</td>
                    </tr>
                    <tr>
                        <td>频响范围</td>
                        <td>16Hz - 40kHz</td>
                    </tr>
                    <tr>
                        <td>电池容量</td>
                        <td>750mAh</td>
                    </tr>
                    <tr>
                        <td>续航时间</td>
                        <td>40小时 (ANC开) / 60小时 (ANC关)</td>
                    </tr>
                    <tr>
                        <td>充电时间</td>
                        <td>约 2 小时</td>
                    </tr>
                    <tr>
                        <td>重量</td>
                        <td>约 260g</td>
                    </tr>
                </tbody>
            </table>

            <h2 id="setup">快速设置指南</h2>

            <h3>1. 充电</h3>
            <p>首次使用前，请先为耳机充满电。将 USB-C 充电线连接到耳机和电源适配器，充电指示灯会显示充电状态。</p>

            <h3>2. 开机与配对</h3>
            <ol>
                <li>长按电源键 3 秒开机，蓝色指示灯亮起</li>
                <li>首次开机会自动进入配对模式，蓝色和红色指示灯交替闪烁</li>
                <li>在您的设备上打开蓝牙设置</li>
                <li>在可用设备列表中选择 "Soundcore Life Q30"</li>
                <li>配对成功后，蓝色指示灯常亮 3 秒</li>
            </ol>

            <div class="info-card">
                <h4>💡 配对小提示</h4>
                <p>如需手动进入配对模式，请在关机状态下长按电源键 5 秒，直到蓝色和红色指示灯交替闪烁。</p>
            </div>

            <h2 id="features">功能特性详解</h2>

            <h3>主动降噪 (ANC)</h3>
            <p>Life Q30 配备混合式主动降噪技术，通过内外双麦克风实时监测环境噪音，并产生反向声波进行抵消。降噪深度可达 95%，有效隔绝外界干扰。</p>

            <p><strong>三种降噪模式：</strong></p>
            <ul>
                <li><strong>交通模式：</strong>专为飞机、火车、地铁等交通工具优化，有效降低低频引擎噪音</li>
                <li><strong>室内模式：</strong>适用于办公室、咖啡厅等室内环境，降低人声和环境噪音</li>
                <li><strong>户外模式：</strong>平衡降噪与环境音，适合街道行走时使用</li>
            </ul>

            <h3>通透模式</h3>
            <p>开启通透模式后，耳机会放大环境音，让您在佩戴耳机时也能听清周围的声音，方便与他人交流或注意周围环境。</p>

            <h3>LDAC 高清音质</h3>
            <p>支持 Sony LDAC 音频编码技术，传输速率可达 990kbps，是普通蓝牙音频的 3 倍，保留更多音乐细节。</p>

            <h2 id="controls">按键功能说明</h2>

            <h3>电源键</h3>
            <ul>
                <li>开机：长按 3 秒</li>
                <li>关机：长按 3 秒</li>
                <li>配对模式：关机状态长按 5 秒</li>
            </ul>

            <h3>播放控制键</h3>
            <ul>
                <li>播放/暂停：单击</li>
                <li>下一曲：双击</li>
                <li>上一曲：三击</li>
                <li>接听/挂断电话：单击</li>
                <li>拒接来电：长按 2 秒</li>
            </ul>

            <h3>音量键</h3>
            <ul>
                <li>音量+：短按增加音量</li>
                <li>音量-：短按减小音量</li>
            </ul>

            <h3>降噪/通透键</h3>
            <ul>
                <li>切换模式：短按循环切换 ANC 模式、通透模式、普通模式</li>
                <li>长按 2 秒：切换不同的 ANC 降噪场景</li>
            </ul>

            <h2 id="app">Soundcore APP 使用</h2>
            <p>下载 Soundcore APP 可以解锁更多功能和自定义设置：</p>
            <ul>
                <li>自定义 EQ 均衡器设置</li>
                <li>选择降噪模式和强度</li>
                <li>固件更新</li>
                <li>查看电池电量</li>
                <li>设置自动关机时间</li>
                <li>使用睡眠模式</li>
            </ul>

            <p>
                <a href="#" class="btn">下载 iOS 版本</a>
                <a href="#" class="btn btn-secondary" style="margin-left: 12px;">下载 Android 版本</a>
            </p>

            <h2 id="troubleshooting">常见问题与解决方案</h2>

            <h3>无法开机</h3>
            <ul>
                <li>检查电池电量，尝试充电 30 分钟后再开机</li>
                <li>确保充电线连接牢固</li>
                <li>尝试使用不同的充电器和充电线</li>
            </ul>

            <h3>无法连接蓝牙</h3>
            <ul>
                <li>确保耳机已开机并处于配对模式</li>
                <li>删除设备蓝牙列表中的配对记录，重新配对</li>
                <li>确保耳机与设备距离在 10 米以内，中间无障碍物</li>
                <li>关闭其他蓝牙设备的干扰</li>
            </ul>

            <h3>音质不佳或断断续续</h3>
            <ul>
                <li>检查蓝牙连接稳定性，尽量靠近播放设备</li>
                <li>在 APP 中选择更高质量的音频编码 (LDAC)</li>
                <li>清理耳机和设备的蓝牙缓存</li>
                <li>更新耳机固件到最新版本</li>
            </ul>

            <h3>降噪效果不明显</h3>
            <ul>
                <li>确保耳机佩戴正确，耳罩完全覆盖耳朵</li>
                <li>在 APP 中选择适合当前环境的降噪模式</li>
                <li>检查降噪功能是否已开启（指示灯显示）</li>
            </ul>


            <h2 id="care">保养与维护</h2>
            <p>正确的保养可以延长耳机的使用寿命：</p>
            <ul>
                <li>使用干燥柔软的布清洁耳机表面</li>
                <li>避免将耳机暴露在极端温度环境中</li>
                <li>不使用时，请将耳机存放在收纳包中</li>
                <li>定期清洁耳罩，保持卫生</li>
                <li>避免耳机接触液体</li>
                <li>建议每 3-6 个月进行一次完全充放电</li>
            </ul>

            <div class="info-card">
                <h4>🔋 电池保养建议</h4>
                <p>为保持最佳电池性能，建议避免长时间将电量耗尽，保持电量在 20%-80% 之间使用。长期不用时，建议每月充电一次。</p>
            </div>

            <h2 id="support">技术支持与保修</h2>
            <p>Soundcore Life Q30 享有 18 个月质保（注册产品后可延长至 24 个月）。如果您在使用过程中遇到任何问题，请通过以下方式联系我们：</p>

            <ul>
                <li><strong>在线支持：</strong>访问 support.soundcore.com</li>
                <li><strong>邮箱：</strong>support@soundcore.com</li>
                <li><strong>电话：</strong>400-xxx-xxxx (周一至周五 9:00-18:00)</li>
            </ul>

            <p>
                <a href="#" class="btn">联系技术支持</a>
                <a href="#" class="btn btn-secondary" style="margin-left: 12px;">注册产品</a>
            </p>

            <hr style="margin: 40px 0; border: none; border-top: 1px solid #e0e0e0;">

            <p style="text-align: center; color: #999; font-size: 13px;">
                感谢您选择 Soundcore，祝您使用愉快！
            </p>
        </main>
    </div>

    <!-- 页脚 -->
    <footer>
        <p>&copy; 2024 Soundcore. All Rights Reserved. | 隐私政策 | 服务条款 | 联系我们</p>
    </footer>

    <script>
        let isEditMode = false;
        const content = document.getElementById('editableContent');
        const editModeBtn = document.getElementById('editModeBtn');
        const modeIndicator = document.getElementById('modeIndicator');

        // 切换编辑模式
        function toggleEditMode() {
            isEditMode = !isEditMode;
            content.contentEditable = isEditMode;

            if (isEditMode) {
                document.body.classList.add('edit-mode');
                editModeBtn.innerHTML = '<span>👁️</span> 退出编辑';
                modeIndicator.textContent = '编辑模式';
                modeIndicator.style.backgroundColor = 'rgba(255, 255, 255, 0.3)';
            } else {
                document.body.classList.remove('edit-mode');
                editModeBtn.innerHTML = '<span>✏️</span> 开启编辑';
                modeIndicator.textContent = '查看模式';
                modeIndicator.style.backgroundColor = 'rgba(255, 255, 255, 0.2)';
            }
        }

        // 文本格式化
        function formatText(command) {
            if (!isEditMode) {
                alert('请先开启编辑模式');
                return;
            }
            document.execCommand(command, false, null);
        }

        // 添加标题
        function addHeading(tag) {
            if (!isEditMode) {
                alert('请先开启编辑模式');
                return;
            }
            const selection = window.getSelection();
            if (selection.rangeCount > 0) {
                const range = selection.getRangeAt(0);
                const heading = document.createElement(tag);
                heading.textContent = selection.toString() || '新标题';
                range.deleteContents();
                range.insertNode(heading);
            }
        }

        // 插入图片
        function insertImage() {
            if (!isEditMode) {
                alert('请先开启编辑模式');
                return;
            }
            document.getElementById('imageInput').click();
        }

        // 处理图片上传
        function handleImageUpload(event) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    const img = document.createElement('img');
                    img.src = e.target.result;
                    img.style.maxWidth = '100%';
                    img.style.borderRadius = '12px';
                    img.style.margin = '24px 0';
                    content.appendChild(img);
                };
                reader.readAsDataURL(file);
            }
        }

        // 插入视频
        function insertVideo() {
            if (!isEditMode) {
                alert('请先开启编辑模式');
                return;
            }
            const choice = confirm('点击"确定"上传本地视频，点击"取消"插入视频链接');
            if (choice) {
                document.getElementById('videoInput').click();
            } else {
                const url = prompt('请输入视频URL (支持 MP4, WebM):');
                if (url) {
                    const video = document.createElement('video');
                    video.src = url;
                    video.controls = true;
                    video.style.maxWidth = '100%';
                    video.style.borderRadius = '12px';
                    video.style.margin = '24px 0';
                    content.appendChild(video);
                }
            }
        }

        // 处理视频上传
        function handleVideoUpload(event) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    const video = document.createElement('video');
                    video.src = e.target.result;
                    video.controls = true;
                    video.style.maxWidth = '100%';
                    video.style.borderRadius = '12px';
                    video.style.margin = '24px 0';
                    content.appendChild(video);
                };
                reader.readAsDataURL(file);
            }
        }

        // 添加信息卡片
        function addInfoCard() {
            if (!isEditMode) {
                alert('请先开启编辑模式');
                return;
            }
            const card = document.createElement('div');
            card.className = 'info-card';
            card.innerHTML = `
                <h4>💡 提示标题</h4>
                <p>在这里输入提示内容...</p>
            `;
            content.appendChild(card);
        }

        // 添加表格
        function addTable() {
            if (!isEditMode) {
                alert('请先开启编辑模式');
                return;
            }
            const table = document.createElement('table');
            table.innerHTML = `
                <thead>
                    <tr>
                        <th>列1</th>
                        <th>列2</th>
                        <th>列3</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>数据1</td>
                        <td>数据2</td>
                        <td>数据3</td>
                    </tr>
                    <tr>
                        <td>数据4</td>
                        <td>数据5</td>
                        <td>数据6</td>
                    </tr>
                </tbody>
            `;
            content.appendChild(table);
        }

        // 保存内容
        function saveContent() {
            const htmlContent = content.innerHTML;
            const blob = new Blob([htmlContent], { type: 'text/html' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'content_' + new Date().getTime() + '.html';
            a.click();
            URL.revokeObjectURL(url);
            alert('内容已保存！');
        }

        // 侧边栏导航平滑滚动
        document.querySelectorAll('.sidebar a').forEach(anchor => {
            anchor.addEventListener('click', function(e) {
                e.preventDefault();
                const targetId = this.getAttribute('href').substring(1);
                const targetElement = document.getElementById(targetId);
                if (targetElement) {
                    targetElement.scrollIntoView({ behavior: 'smooth', block: 'start' });

                    // 更新激活状态
                    document.querySelectorAll('.sidebar a').forEach(a => a.classList.remove('active'));
                    this.classList.add('active');
                }
            });
        });

        // 键盘快捷键
        document.addEventListener('keydown', function(e) {
            if (e.ctrlKey || e.metaKey) {
                switch(e.key) {
                    case 's':
                        e.preventDefault();
                        saveContent();
                        break;
                    case 'b':
                        e.preventDefault();
                        formatText('bold');
                        break;
                    case 'i':
                        e.preventDefault();
                        formatText('italic');
                        break;
                }
            }
        });
    </script>
</body>
</html>
