# NPCNormal_001
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>修仙炼丹交互系统 - 勤勉型炼丹师</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Microsoft YaHei', 'SimHei', sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #1a1f25 0%, #0c0e13 100%);
            color: #e0d6c2;
            min-height: 100vh;
            overflow-x: hidden;
            position: relative;
        }
        
        body::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" viewBox="0 0 100 100"><rect width="100" height="100" fill="none" stroke="%233a3f45" stroke-width="0.5"/></svg>');
            opacity: 0.1;
            z-index: -1;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            text-align: center;
            padding: 30px 0;
            border-bottom: 1px solid #3a3f45;
            margin-bottom: 30px;
            position: relative;
        }
        
        header h1 {
            font-size: 3rem;
            background: linear-gradient(to right, #d4af37, #ffd700, #d4af37);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 10px rgba(212, 175, 55, 0.3);
            margin-bottom: 10px;
            letter-spacing: 3px;
        }
        
        header p {
            font-size: 1.2rem;
            color: #a9a194;
            max-width: 800px;
            margin: 0 auto;
            line-height: 1.6;
        }
        
        .alchemist-types {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 25px;
            margin-bottom: 40px;
        }
        
        .alchemist-card {
            background: linear-gradient(145deg, #232830, #1a1f25);
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            border: 1px solid #3a3f45;
            position: relative;
            cursor: pointer;
            opacity: 0.6;
        }
        
        .alchemist-card.active {
            opacity: 1;
            transform: translateY(-5px);
            box-shadow: 0 15px 35px rgba(212, 175, 55, 0.3);
            border-color: #d4af37;
        }
        
        .card-header {
            padding: 20px;
            background: linear-gradient(90deg, #2c313a, #232830);
            text-align: center;
            border-bottom: 1px solid #3a3f45;
        }
        
        .card-header h3 {
            font-size: 1.5rem;
            color: #ffd700;
            margin-bottom: 5px;
        }
        
        .card-header .type-icon {
            font-size: 2.5rem;
            margin-bottom: 15px;
            color: #d4af37;
        }
        
        .card-body {
            padding: 20px;
        }
        
        .traits {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-bottom: 15px;
        }
        
        .trait {
            background: rgba(212, 175, 55, 0.15);
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 0.9rem;
            color: #d4af37;
            border: 1px solid rgba(212, 175, 55, 0.3);
        }
        
        .card-body p {
            color: #b8b0a0;
            line-height: 1.6;
            margin-bottom: 20px;
        }
        
        .interaction-panel {
            background: linear-gradient(145deg, #1e2329, #171b21);
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.6);
            border: 1px solid #3a3f45;
            margin-bottom: 30px;
            min-height: 400px;
            position: relative;
            overflow: hidden;
        }
        
        .panel-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            padding-bottom: 15px;
            border-bottom: 1px solid #3a3f45;
        }
        
        .panel-header h2 {
            font-size: 1.8rem;
            color: #ffd700;
        }
        
        .interaction-type {
            display: flex;
            gap: 15px;
            margin-bottom: 25px;
        }
        
        .type-btn {
            flex: 1;
            padding: 15px;
            background: linear-gradient(145deg, #2c313a, #232830);
            border: 1px solid #3a3f45;
            border-radius: 10px;
            color: #b8b0a0;
            font-size: 1.1rem;
            cursor: pointer;
            transition: all 0.3s ease;
            text-align: center;
        }
        
        .type-btn:hover, .type-btn.active {
            background: linear-gradient(145deg, #3a2e1a, #2d2415);
            border-color: #d4af37;
            color: #ffd700;
            box-shadow: 0 0 15px rgba(212, 175, 55, 0.3);
        }
        
        .dialogue-box {
            background: rgba(26, 31, 37, 0.8);
            border: 1px solid #3a3f45;
            border-radius: 12px;
            padding: 25px;
            margin-bottom: 25px;
            min-height: 150px;
            position: relative;
        }
        
        .npc-dialogue {
            font-size: 1.2rem;
            line-height: 1.7;
            color: #e0d6c2;
            margin-bottom: 20px;
        }
        
        .dialogue-character {
            position: absolute;
            bottom: -20px;
            right: 20px;
            font-size: 0.9rem;
            color: #d4af37;
            background: #1a1f25;
            padding: 5px 15px;
            border-radius: 15px;
            border: 1px solid #3a3f45;
        }
        
        .options-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 15px;
            margin-bottom: 25px;
        }
        
        .option-btn {
            background: linear-gradient(145deg, #2c313a, #232830);
            border: 1px solid #3a3f45;
            border-radius: 10px;
            padding: 18px;
            color: #b8b0a0;
            font-size: 1.1rem;
            cursor: pointer;
            transition: all 0.3s ease;
            text-align: center;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }
        
        .option-btn:hover {
            background: linear-gradient(145deg, #3a2e1a, #2d2415);
            border-color: #d4af37;
            color: #ffd700;
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
        
        .result-panel {
            background: rgba(40, 30, 15, 0.3);
            border: 1px solid #d4af37;
            border-radius: 12px;
            padding: 25px;
            margin-top: 25px;
            display: none;
        }
        
        .result-title {
            color: #ffd700;
            font-size: 1.5rem;
            margin-bottom: 15px;
            text-align: center;
        }
        
        .result-content {
            font-size: 1.1rem;
            line-height: 1.7;
            margin-bottom: 20px;
        }
        
        .rewards {
            display: flex;
            justify-content: center;
            gap: 20px;
            flex-wrap: wrap;
        }
        
        .reward-item {
            background: rgba(212, 175, 55, 0.15);
            border: 1px solid rgba(212, 175, 55, 0.3);
            border-radius: 10px;
            padding: 15px;
            text-align: center;
            min-width: 120px;
        }
        
        .reward-value {
            font-size: 1.3rem;
            color: #ffd700;
            font-weight: bold;
            margin-top: 5px;
        }
        
        .action-buttons {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-top: 25px;
            flex-wrap: wrap;
        }
        
        .action-btn {
            padding: 12px 30px;
            border-radius: 30px;
            font-size: 1.1rem;
            cursor: pointer;
            transition: all 0.3s ease;
            border: none;
            font-weight: bold;
        }
        
        .primary-btn {
            background: linear-gradient(145deg, #d4af37, #b8972e);
            color: #1a1f25;
        }
        
        .secondary-btn {
            background: transparent;
            border: 1px solid #d4af37;
            color: #d4af37;
        }
        
        .tertiary-btn {
            background: linear-gradient(145deg, #8c2a2a, #6d1f1f);
            color: #ffd700;
        }
        
        .action-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(212, 175, 55, 0.4);
        }
        
        .minigame-container {
            background: rgba(26, 31, 37, 0.8);
            border: 1px solid #3a3f45;
            border-radius: 12px;
            padding: 25px;
            margin: 25px 0;
            text-align: center;
            display: none;
        }
        
        .minigame-title {
            color: #ffd700;
            margin-bottom: 20px;
        }
        
        .minigame-controls {
            display: flex;
            justify-content: center;
            gap: 15px;
            flex-wrap: wrap;
        }
        
        .control-btn {
            width: 80px;
            height: 80px;
            border-radius: 50%;
            background: linear-gradient(145deg, #2c313a, #232830);
            border: 2px solid #3a3f45;
            color: #b8b0a0;
            font-size: 1.5rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.2s ease;
        }
        
        .control-btn:hover {
            border-color: #d4af37;
            color: #ffd700;
            transform: scale(1.1);
        }
        
        .timer {
            font-size: 1.3rem;
            color: #ffd700;
            margin: 15px 0;
            font-family: monospace;
        }
        
        .flame-effect {
            width: 100%;
            height: 100px;
            background: linear-gradient(to top, rgba(26, 31, 37, 0.8), transparent), 
                        url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><path d="M20,80 Q40,20 50,50 T80,80" fill="none" stroke="%23d4af37" stroke-width="2"/></svg>');
            background-size: 100% 100%;
            margin: 20px 0;
            opacity: 0.7;
        }
        
        .teaching-game {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 20px;
        }
        
        .cauldron {
            width: 200px;
            height: 200px;
            background: linear-gradient(145deg, #3a2e1a, #2d2415);
            border-radius: 50% 50% 30% 30%;
            position: relative;
            border: 3px solid #d4af37;
            overflow: hidden;
        }
        
        .flame-indicator {
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 50%;
            background: linear-gradient(to top, #ff6b6b, #ffd700);
            border-radius: 50% 50% 0 0;
            transition: height 0.5s ease;
        }
        
        .instruction {
            font-size: 1.2rem;
            color: #ffd700;
            margin: 15px 0;
            text-align: center;
            min-height: 60px;
        }
        
        .status-bar {
            width: 100%;
            height: 15px;
            background: #2c313a;
            border-radius: 10px;
            overflow: hidden;
            border: 1px solid #3a3f45;
            margin-top: 10px;
        }
        
        .stability-fill {
            height: 100%;
            background: linear-gradient(90deg, #ff6b6b, #ffd700, #4caf50);
            width: 70%;
            transition: width 0.5s ease;
        }
        
        .stability-labels {
            display: flex;
            justify-content: space-between;
            width: 100%;
            color: #b8b0a0;
            font-size: 0.9rem;
            margin-top: 5px;
        }
        
        .teaching-controls {
            display: flex;
            gap: 15px;
        }
        
        .teaching-btn {
            padding: 12px 20px;
            border-radius: 8px;
            background: linear-gradient(145deg, #2c313a, #232830);
            border: 1px solid #3a3f45;
            color: #b8b0a0;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .teaching-btn:hover {
            background: linear-gradient(145deg, #3a2e1a, #2d2415);
            border-color: #d4af37;
            color: #ffd700;
        }
        
        .analysis-panel {
            background: rgba(26, 31, 37, 0.8);
            border: 1px solid #3a3f45;
            border-radius: 12px;
            padding: 20px;
            margin-top: 20px;
            display: none;
        }
        
        .analysis-title {
            color: #ffd700;
            text-align: center;
            margin-bottom: 15px;
        }
        
        .analysis-content {
            font-size: 1rem;
            line-height: 1.6;
        }
        
        .analysis-point {
            margin-bottom: 10px;
            padding-left: 20px;
            position: relative;
        }
        
        .analysis-point::before {
            content: "•";
            position: absolute;
            left: 5px;
            color: #d4af37;
        }
        
        .steal-options {
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin-top: 20px;
        }
        
        .steal-option {
            padding: 15px;
            background: rgba(40, 30, 15, 0.5);
            border-radius: 10px;
            border: 1px solid #3a3f45;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .steal-option:hover {
            background: rgba(60, 45, 20, 0.7);
            border-color: #d4af37;
            transform: translateY(-3px);
        }
        
        .steal-option i {
            font-size: 1.5rem;
            color: #d4af37;
        }
        
        /* 弹窗样式 */
        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            overflow: auto;
            background-color: rgba(0,0,0,0.8);
        }
        
        .modal-content {
            background: linear-gradient(145deg, #232830, #1a1f25);
            margin: 5% auto;
            padding: 30px;
            border: 1px solid #3a3f45;
            border-radius: 15px;
            width: 80%;
            max-width: 800px;
            color: #e0d6c2;
            position: relative;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        }
        
        .close {
            color: #d4af37;
            position: absolute;
            top: 15px;
            right: 25px;
            font-size: 35px;
            font-weight: bold;
            cursor: pointer;
        }
        
        .close:hover {
            color: #ffd700;
        }
        
        .modal-title {
            text-align: center;
            margin-bottom: 20px;
            color: #ffd700;
            font-size: 1.8rem;
        }
        
        .process-section {
            margin-bottom: 25px;
            padding: 15px;
            background: rgba(30, 35, 40, 0.5);
            border-radius: 10px;
            border: 1px solid #3a3f45;
        }
        
        .process-section h3 {
            color: #d4af37;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 1px solid #3a3f45;
        }
        
        .process-point {
            margin-bottom: 12px;
            padding-left: 20px;
            position: relative;
        }
        
        .process-point::before {
            content: "•";
            position: absolute;
            left: 5px;
            color: #d4af37;
        }
        
        .process-subpoint {
            margin-left: 20px;
            margin-top: 8px;
            color: #b8b0a0;
        }
        
        .feature-icon {
            display: inline-block;
            width: 30px;
            height: 30px;
            background: rgba(212, 175, 55, 0.2);
            border-radius: 50%;
            text-align: center;
            line-height: 30px;
            margin-right: 10px;
            color: #d4af37;
        }
        
        .success-effect {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle, rgba(212, 175, 55, 0.3) 0%, transparent 70%);
            animation: glow 1.5s ease-in-out;
            z-index: 10;
            pointer-events: none;
        }
        
        @keyframes glow {
            0% { opacity: 0; transform: scale(0.5); }
            50% { opacity: 1; transform: scale(1.2); }
            100% { opacity: 0; transform: scale(1.5); }
        }
        
        .failure-effect {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle, rgba(255, 0, 0, 0.3) 0%, transparent 70%);
            animation: shake 0.5s ease-in-out;
            z-index: 10;
            pointer-events: none;
        }
        
        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            10%, 30%, 50%, 70%, 90% { transform: translateX(-10px); }
            20%, 40%, 60%, 80% { transform: translateX(10px); }
        }
        
        @media (max-width: 768px) {
            .alchemist-types {
                grid-template-columns: 1fr;
            }
            
            .options-container {
                grid-template-columns: 1fr;
            }
            
            header h1 {
                font-size: 2.2rem;
            }
            
            .interaction-type {
                flex-direction: column;
            }
            
            .action-buttons {
                flex-direction: column;
            }
            
            .modal-content {
                width: 95%;
                padding: 15px;
            }
            
            .control-btn {
                width: 60px;
                height: 60px;
                font-size: 1.2rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1><i class="fas fa-fire-alt"></i> 修仙炼丹交互系统</h1>
            <p>与勤勉型炼丹师王铁柱深入互动，在炼丹之道上留下你的传奇</p>
        </header>
        
        <div class="alchemist-types">
            <div class="alchemist-card active" data-type="diligent">
                <div class="card-header">
                    <div class="type-icon"><i class="fas fa-hammer"></i></div>
                    <h3>勤勉型炼丹师</h3>
                    <p>废寝忘食追求丹道极致</p>
                </div>
                <div class="card-body">
                    <div class="traits">
                        <span class="trait">追求完美</span>
                        <span class="trait">勤奋刻苦</span>
                        <span class="trait">虚心求教</span>
                    </div>
                    <p>炉火旁日夜钻研的炼丹痴人，常因过于专注导致丹炉失控。他们的丹炉普通但维护用心，磨损的痕迹诉说着无数次的尝试。</p>
                </div>
            </div>
            
            <div class="alchemist-card" data-type="merchant">
                <div class="card-header">
                    <div class="type-icon"><i class="fas fa-coins"></i></div>
                    <h3>商人型炼丹师</h3>
                    <p>利益至上精于算计</p>
                </div>
                <div class="card-body">
                    <div class="traits">
                        <span class="trait">精打细算</span>
                        <span class="trait">花言巧语</span>
                        <span class="trait">利益至上</span>
                    </div>
                    <p>花哨丹炉上贴着促销符文的生意人，炼丹只是谋利手段。他们深谙人心，总能用各种方式让顾客掏出灵石。</p>
                </div>
            </div>
            
            <div class="alchemist-card" data-type="expert">
                <div class="card-header">
                    <div class="type-icon"><i class="fas fa-user-graduate"></i></div>
                    <h3>专家型炼丹师</h3>
                    <p>丹道大师技艺超群</p>
                </div>
                <div class="card-body">
                    <div class="traits">
                        <span class="trait">技艺精湛</span>
                        <span class="trait">知识渊博</span>
                        <span class="trait">严格自律</span>
                    </div>
                    <p>丹炉配备教学投影功能的大师，对丹道有近乎偏执的追求。他们容不得半点差错，但欣赏真正有天赋的后辈。</p>
                </div>
            </div>
            
            <div class="alchemist-card" data-type="novice">
                <div class="card-header">
                    <div class="type-icon"><i class="fas fa-seedling"></i></div>
                    <h3>初学者炼丹师</h3>
                    <p>初涉丹道小心翼翼</p>
                </div>
                <div class="card-body">
                    <div class="traits">
                        <span class="trait">谨慎小心</span>
                        <span class="trait">缺乏自信</span>
                        <span class="trait">求知若渴</span>
                    </div>
                    <p>在角落偷偷练习的炼丹新手，常因紧张导致炸炉。他们需要耐心指导，一旦获得信任会成为你最忠实的追随者。</p>
                </div>
            </div>
        </div>
        
        <div class="interaction-panel">
            <div class="panel-header">
                <h2>勤勉型炼丹师 · 炸炉危机</h2>
                <div class="dialogue-character">王铁柱 · 勤勉型炼丹师</div>
            </div>
            
            <div class="interaction-type">
                <div class="type-btn active">被动流程：炸炉危机</div>
                <div class="type-btn">主动流程：丹道授业</div>
            </div>
            
            <div class="dialogue-box">
                <div class="npc-dialogue">
                    <i class="fas fa-quote-left" style="color: #d4af37; margin-right: 10px;"></i>
                    唉！又失败了！这已经是本月第七炉废丹了...火候明明已经严格控制，药材比例也分毫不差，为何总是差那么一点？
                    <br><br>
                    <i class="fas fa-fire" style="color: #ff6b6b;"></i> 不好！炉火失控了！火焰窜起八丈高！丹炉开始剧烈震动！谁来帮帮我！
                </div>
            </div>
            
            <div class="options-container">
                <div class="option-btn" data-action="rescue">
                    <i class="fas fa-hands-helping"></i> 出手相助，施展控火术
                </div>
                <div class="option-btn" data-action="observe">
                    <i class="fas fa-eye"></i> 冷眼旁观，静观其变
                </div>
                <div class="option-btn" data-action="sabotage">
                    <i class="fas fa-skull"></i> 暗中捣乱，加速炸炉
                </div>
            </div>
            
            <!-- 被动流程小游戏：控火术挑战 -->
            <div class="minigame-container" id="rescue-minigame">
                <h3 class="minigame-title">控火术挑战</h3>
                <p>在10秒内按正确顺序输入方位，稳定丹炉火势</p>
                <div class="timer">剩余时间: <span id="time">10</span>秒</div>
                <div class="minigame-controls">
                    <div class="control-btn" data-direction="up">↑</div>
                    <div class="control-btn" data-direction="down">↓</div>
                    <div class="control-btn" data-direction="left">←</div>
                    <div class="control-btn" data-direction="right">→</div>
                </div>
                <div class="flame-effect"></div>
                <p>正确序列: ↑ → ↓ ← ↑</p>
            </div>
            
            <!-- 主动流程小游戏：丹道授业 -->
            <div class="minigame-container" id="teaching-minigame">
                <h3 class="minigame-title">丹道授业</h3>
                <p>指导王铁柱控制丹炉火候，在30秒内保持稳定</p>
                <div class="timer">剩余时间: <span id="teaching-time">30</span>秒</div>
                
                <div class="teaching-game">
                    <div class="cauldron">
                        <div class="flame-indicator" id="flame-level"></div>
                    </div>
                    
                    <div class="instruction" id="instruction">
                        丹火过旺，请降低火势！
                    </div>
                    
                    <div class="status-bar">
                        <div class="stability-fill" id="stability-bar"></div>
                    </div>
                    <div class="stability-labels">
                        <span>危险</span>
                        <span>稳定</span>
                        <span>完美</span>
                    </div>
                    
                    <div class="teaching-controls">
                        <button class="teaching-btn" id="increase-btn">
                            <i class="fas fa-arrow-up"></i> 增强火力
                        </button>
                        <button class="teaching-btn" id="decrease-btn">
                            <i class="fas fa-arrow-down"></i> 减弱火力
                        </button>
                        <button class="teaching-btn" id="stabilize-btn">
                            <i class="fas fa-balance-scale"></i> 稳定丹炉
                        </button>
                    </div>
                </div>
            </div>
            
            <!-- 分析报告面板 -->
            <div class="analysis-panel" id="analysis-panel">
                <h3 class="analysis-title">《讲学评析》</h3>
                <div class="analysis-content" id="analysis-content">
                    <!-- 分析内容由JS动态生成 -->
                </div>
            </div>
            
            <!-- 结果面板 -->
            <div class="result-panel" id="result-panel">
                <h3 class="result-title">炼丹结果</h3>
                <div class="result-content" id="result-content">
                    <!-- 结果内容由JS动态生成 -->
                </div>
                
                <div class="rewards" id="rewards-container">
                    <!-- 奖励内容由JS动态生成 -->
                </div>
                
                <div class="action-buttons" id="action-buttons">
                    <!-- 操作按钮由JS动态生成 -->
                </div>
                
                <!-- 偷窃选项面板 -->
                <div class="steal-options" id="steal-options" style="display: none;">
                    <h3 style="color: #ffd700; text-align: center; margin-bottom: 15px;">选择偷窃方式</h3>
                    <div class="steal-option" data-option="1">
                        <i class="fas fa-weight-hanging"></i>
                        <div>
                            <h4>直接搬走</h4>
                            <p>尝试直接搬走火纹玄铁</p>
                        </div>
                    </div>
                    <div class="steal-option" data-option="2">
                        <i class="fas fa-running"></i>
                        <div>
                            <h4>快速顺走</h4>
                            <p>趁人不备快速顺走玄铁</p>
                        </div>
                    </div>
                    <div class="steal-option" data-option="3">
                        <i class="fas fa-exchange-alt"></i>
                        <div>
                            <h4>声东击西</h4>
                            <p>制造混乱后趁机偷走玄铁</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <!-- 弹窗结构 -->
    <div id="alchemist-modal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <h2 id="modal-title" class="modal-title">炼丹师流程详情</h2>
            <div id="modal-content"></div>
        </div>
    </div>

    <script>
        // 炼丹师卡片选择
        const alchemistCards = document.querySelectorAll('.alchemist-card');
        alchemistCards.forEach(card => {
            card.addEventListener('click', () => {
                document.querySelector('.alchemist-card.active').classList.remove('active');
                card.classList.add('active');
                
                // 更新面板标题
                const type = card.dataset.type;
                const title = card.querySelector('h3').textContent;
                document.querySelector('.panel-header h2').textContent = `${title} · 炸炉危机`;
                document.querySelector('.dialogue-character').textContent = 
                    type === 'diligent' ? '王铁柱 · 勤勉型炼丹师' :
                    type === 'merchant' ? '钱掌柜 · 商人型炼丹师' :
                    type === 'expert' ? '李大师 · 专家型炼丹师' : 
                    '张小凡 · 初学者炼丹师';
                    
                // 如果是非勤勉型炼丹师，显示弹窗
                if (type !== 'diligent') {
                    showAlchemistModal(type);
                }
            });
        });
        
        // 交互类型切换
        const typeBtns = document.querySelectorAll('.type-btn');
        typeBtns.forEach(btn => {
            btn.addEventListener('click', () => {
                document.querySelector('.type-btn.active').classList.remove('active');
                btn.classList.add('active');
                
                // 隐藏所有小游戏和结果面板
                document.getElementById('rescue-minigame').style.display = 'none';
                document.getElementById('teaching-minigame').style.display = 'none';
                document.getElementById('result-panel').style.display = 'none';
                document.getElementById('analysis-panel').style.display = 'none';
                document.getElementById('steal-options').style.display = 'none';
                
                // 更新内容
                if(btn.textContent.includes('被动流程')) {
                    document.querySelector('.panel-header h2').textContent = '勤勉型炼丹师 · 炸炉危机';
                    
                    document.querySelector('.npc-dialogue').innerHTML = `
                        <i class="fas fa-quote-left" style="color: #d4af37; margin-right: 10px;"></i>
                        唉！又失败了！这已经是本月第七炉废丹了...火候明明已经严格控制，药材比例也分毫不差，为何总是差那么一点？
                        <br><br>
                        <i class="fas fa-fire" style="color: #ff6b6b;"></i> 不好！炉火失控了！火焰窜起八丈高！丹炉开始剧烈震动！谁来帮帮我！
                    `;
                    
                    document.querySelector('.options-container').innerHTML = `
                        <div class="option-btn" data-action="rescue">
                            <i class="fas fa-hands-helping"></i> 出手相助，施展控火术
                        </div>
                        <div class="option-btn" data-action="observe">
                            <i class="fas fa-eye"></i> 冷眼旁观，静观其变
                        </div>
                        <div class="option-btn" data-action="sabotage">
                            <i class="fas fa-skull"></i> 暗中捣乱，加速炸炉
                        </div>
                    `;
                } else {
                    document.querySelector('.panel-header h2').textContent = '勤勉型炼丹师 · 丹道授业';
                    
                    document.querySelector('.npc-dialogue').innerHTML = `
                        <i class="fas fa-quote-left" style="color: #d4af37; margin-right: 10px;"></i>
                        道友炼丹技艺高超，令人佩服！这炉丹药火候掌控精妙，药材融合完美无瑕，定是上品无疑！
                        <br><br>
                        不知能否指点在下一二？我已在筑基后期徘徊三年，始终无法突破金丹瓶颈...
                    `;
                    
                    document.querySelector('.options-container').innerHTML = `
                        <div class="option-btn" data-action="teach">
                            <i class="fas fa-chalkboard-teacher"></i> 欣然应允，传授丹道
                        </div>
                        <div class="option-btn" data-action="refuse">
                            <i class="fas fa-times-circle"></i> 婉言谢绝，专注炼丹
                        </div>
                        <div class="option-btn" data-action="mock">
                            <i class="fas fa-grin-squint-tears"></i> 假意答应，实则戏弄
                        </div>
                    `;
                }
                
                // 重新绑定事件
                bindOptionEvents();
            });
        });
        
        // 选项按钮事件绑定
        function bindOptionEvents() {
            const optionBtns = document.querySelectorAll('.option-btn');
            optionBtns.forEach(btn => {
                btn.addEventListener('click', () => {
                    const action = btn.dataset.action;
                    const resultPanel = document.getElementById('result-panel');
                    
                    // 隐藏其他元素
                    document.getElementById('analysis-panel').style.display = 'none';
                    document.getElementById('steal-options').style.display = 'none';
                    
                    // 根据不同类型显示不同结果
                    if(action === 'rescue') {
                        // 重置小游戏
                        playerSequence = [];
                        timeLeft = 10;
                        document.getElementById('time').textContent = timeLeft;
                        document.getElementById('rescue-minigame').style.display = 'block';
                        startGameTimer();
                    } 
                    else if(action === 'teach') {
                        // 重置教学小游戏
                        resetTeachingGame();
                        document.getElementById('teaching-minigame').style.display = 'block';
                        startTeachingGame();
                    }
                    else {
                        let resultText = '';
                        let rewards = '';
                        let actions = '';
                        
                        // 被动流程选项
                        if(action === 'observe') {
                            resultText = '你选择袖手旁观，只见丹炉剧烈震动后轰然炸裂！王铁柱被炸得灰头土脸，但幸运地躲过了致命伤害。他收拾残局时发现了一块罕见的火纹玄铁，眼神复杂地看了你一眼。';
                            rewards = ` 
                                <div class="reward-item"> 
                                    <div>火纹玄铁</div> 
                                    <div class="reward-value">x1</div> 
                                </div> 
                                <div class="reward-item"> 
                                    <div>好感度</div> 
                                    <div class="reward-value">-10</div> 
                                </div> 
                                <div class="reward-item"> 
                                    <div>道德评价</div> 
                                    <div class="reward-value">-15</div> 
                                </div> 
                            `;
                            actions = `
                                <button class="action-btn primary-btn" onclick="closeResult()">离开现场</button>
                                <button class="action-btn secondary-btn" onclick="showStealOptions()">趁机偷取玄铁</button>
                            `;
                        } 
                        else if(action === 'sabotage') {
                            resultText = '你暗中催动灵力扰乱炉火，丹炉瞬间爆炸！王铁柱身受重伤，本命法宝受损。爆炸的冲击波将你震飞，你失去了意识...醒来时发现储物袋中多了几块炸飞的丹药碎片。';
                            rewards = ` 
                                <div class="reward-item"> 
                                    <div>丹药碎片</div> 
                                    <div class="reward-value">x3</div> 
                                </div> 
                                <div class="reward-item"> 
                                    <div>伤势</div> 
                                    <div class="reward-value">-15% HP</div> 
                                </div> 
                                <div class="reward-item"> 
                                    <div>门派声望</div> 
                                    <div class="reward-value">-30</div> 
                                </div> 
                                <div class="reward-item"> 
                                    <div>心魔印记</div> 
                                    <div class="reward-value">+1</div> 
                                </div> 
                            `;
                            actions = `
                                <button class="action-btn primary-btn" onclick="closeResult()">悄悄离开</button>
                                <button class="action-btn secondary-btn" onclick="helpVictim()">救助伤者</button>
                            `;
                        } 
                        // 主动流程选项
                        else if(action === 'refuse') {
                            resultText = '你婉言谢绝了王铁柱的请求，专注于自己的丹炉。王铁柱神情失落，但仍恭敬地站在一旁观摩。三日后，你发现他仍在原处尝试炼丹，眼中充满执着。';
                            rewards = `
                                <div class="reward-item">
                                    <div>专注力</div>
                                    <div class="reward-value">+10%</div>
                                </div>
                                <div class="reward-item">
                                    <div>炼丹效率</div>
                                    <div class="reward-value">+5%</div>
                                </div>
                                <div class="reward-item">
                                    <div>好感度</div>
                                    <div class="reward-value">-5</div>
                                </div>
                            `;
                            actions = `
                                <button class="action-btn primary-btn" onclick="closeResult()">继续炼丹</button>
                                <button class="action-btn secondary-btn" onclick="changeMind()">改变主意</button>
                            `;
                        } 
                        else if(action === 'mock') {
                            resultText = '你假意答应指导，却故意给出错误指示。王铁柱的丹炉冒出黑烟，药材全部报废。当他意识到被戏弄后，愤怒地举起丹炉残片："我视你为前辈，你竟如此戏弄于我！"';
                            rewards = `
                                <div class="reward-item">
                                    <div>门派声望</div>
                                    <div class="reward-value">-40</div>
                                </div>
                                <div class="reward-item">
                                    <div>心魔</div>
                                    <div class="reward-value">+1</div>
                                </div>
                                <div class="reward-item">
                                    <div>炼丹堂权限</div>
                                    <div class="reward-value">-1级</div>
                                </div>
                            `;
                            actions = `
                                <button class="action-btn primary-btn" onclick="apologize()">道歉赔偿</button>
                                <button class="action-btn secondary-btn" onclick="fight()">武力镇压</button>
                            `;
                        }
                        
                        showResultPanel(resultText, rewards, actions);
                    }
                });
            });
        }
        
        // 显示结果面板
        function showResultPanel(content, rewards, actions) {
            const resultPanel = document.getElementById('result-panel');
            const resultContent = document.getElementById('result-content');
            const rewardsContainer = document.getElementById('rewards-container');
            const actionButtons = document.getElementById('action-buttons');
            
            resultContent.innerHTML = content;
            rewardsContainer.innerHTML = rewards || '';
            actionButtons.innerHTML = actions || '<button class="action-btn primary-btn" onclick="closeResult()">继续</button>';
            document.getElementById('steal-options').style.display = 'none';
            
            resultPanel.style.display = 'block';
        }
        
        // 显示偷窃选项
        function showStealOptions() {
            document.getElementById('result-content').innerHTML = '你决定趁机偷取火纹玄铁，但需要选择偷窃方式：';
            document.getElementById('rewards-container').innerHTML = '';
            document.getElementById('action-buttons').innerHTML = '';
            document.getElementById('steal-options').style.display = 'flex';
            
            // 绑定偷窃选项事件
            const stealOptions = document.querySelectorAll('.steal-option');
            stealOptions.forEach(option => {
                option.addEventListener('click', () => {
                    const optionNum = option.dataset.option;
                    stealOption(parseInt(optionNum));
                });
            });
        }
        
        // 偷窃选项处理
        function stealOption(option) {
            let resultText = '';
            let rewards = '';
            let actions = '';
            
            switch(option) {
                case 1: // 直接搬走
                    if(Math.random() > 0.7) {
                        resultText = '你试图直接搬走火纹玄铁，但这块玄铁比想象中沉重得多！"哐当"一声巨响，玄铁落地惊动了所有人。王铁柱转身看到这一幕，眼中充满失望："道友竟行此苟且之事？"';
                        rewards = `
                            <div class="reward-item">
                                <div>门派声望</div>
                                <div class="reward-value">-50</div>
                            </div>
                            <div class="reward-item">
                                <div>好感度</div>
                                <div class="reward-value">-30</div>
                            </div>
                        `;
                        actions = '<button class="action-btn primary-btn" onclick="closeResult()">尴尬离开</button>';
                    } else {
                        resultText = '你咬紧牙关，用尽全身灵力搬起了沉重的火纹玄铁，趁着混乱溜出了炼丹房。这块玄铁足够打造三件上品法器！';
                        rewards = `
                            <div class="reward-item">
                                <div>火纹玄铁</div>
                                <div class="reward-value">x1</div>
                            </div>
                            <div class="reward-item">
                                <div>灵力消耗</div>
                                <div class="reward-value">-20%</div>
                            </div>
                        `;
                        actions = '<button class="action-btn primary-btn" onclick="closeResult()">迅速离开</button>';
                    }
                    break;
                    
                case 2: // 快速顺走
                    if(Math.random() > 0.4) {
                        resultText = '你施展轻身术，如鬼魅般闪过，瞬间将火纹玄铁收入储物袋。王铁柱毫无察觉，仍在清理残局。';
                        rewards = `
                            <div class="reward-item">
                                <div>火纹玄铁</div>
                                <div class="reward-value">x1</div>
                            </div>
                            <div class="reward-item">
                                <div>敏捷</div>
                                <div class="reward-value">+5</div>
                            </div>
                        `;
                        actions = '<button class="action-btn primary-btn" onclick="closeResult()">满意离开</button>';
                    } else {
                        resultText = '就在你即将得手时，一位路过的长老突然出现："小贼安敢！"一道金光将你定在原地。王铁柱见状痛心疾首："我视你为同道，你却..."';
                        rewards = `
                            <div class="reward-item">
                                <div>禁制</div>
                                <div class="reward-value">x1</div>
                            </div>
                            <div class="reward-item">
                                <div>门派惩罚</div>
                                <div class="reward-value">-100</div>
                            </div>
                        `;
                        actions = '<button class="action-btn primary-btn" onclick="plead()">跪地求饶</button>';
                    }
                    break;
                    
                case 3: // 声东击西
                    if(Math.random() > 0.5) {
                        resultText = '你弹出一道灵力击中远处丹炉，引发小规模爆炸。趁众人分神之际，你轻松取走火纹玄铁，神不知鬼不觉。';
                        rewards = `
                            <div class="reward-item">
                                <div>火纹玄铁</div>
                                <div class="reward-value">x1</div>
                            </div>
                            <div class="reward-item">
                                <div>谋略</div>
                                <div class="reward-value">+10</div>
                            </div>
                        `;
                        actions = '<button class="action-btn primary-btn" onclick="closeResult()">从容离开</button>';
                    } else {
                        resultText = '你制造混乱的计策被识破，执法弟子将你当场擒获。王铁柱摇头叹息："为了一块玄铁，值得吗？"';
                        rewards = `
                            <div class="reward-item">
                                <div>门派惩罚</div>
                                <div class="reward-value">-80</div>
                            </div>
                            <div class="reward-item">
                                <div>禁闭</div>
                                <div class="reward-value">3日</div>
                            </div>
                        `;
                        actions = `
                            <button class="action-btn primary-btn" onclick="offerRecipe()">献出丹方赎罪</button>
                            <button class="action-btn tertiary-btn" onclick="resistArrest()">武力反抗</button>
                        `;
                    }
                    break;
            }
            
            document.getElementById('steal-options').style.display = 'none';
            showResultPanel(resultText, rewards, actions);
        }
        
        // 被动流程小游戏逻辑
        const controlBtns = document.querySelectorAll('.control-btn');
        let sequence = ['up', 'right', 'down', 'left', 'up'];
        let playerSequence = [];
        let timeLeft = 10;
        let timer;
        
        controlBtns.forEach(btn => {
            btn.addEventListener('click', () => {
                const direction = btn.dataset.direction;
                playerSequence.push(direction);
                btn.style.borderColor = '#4caf50';
                btn.style.color = '#4caf50';
                
                setTimeout(() => {
                    btn.style.borderColor = '#3a3f45';
                    btn.style.color = '#b8b0a0';
                }, 300);
                
                // 检查序列
                if(playerSequence.length === sequence.length) {
                    clearInterval(timer);
                    const correct = playerSequence.every((move, index) => move === sequence[index]);
                    
                    let resultText = '';
                    let rewards = '';
                    let actions = '';
                    
                    if(correct) {
                        resultText = '你以精湛的控火术稳定了狂暴的炉火，丹炉逐渐平静下来。王铁柱激动地握住你的手："道友救命之恩，铁柱永世不忘！"炉盖开启时，九颗金光闪闪的丹药缓缓升起。';
                        rewards = ` 
                            <div class="reward-item"> 
                                <div>上品聚气丹</div> 
                                <div class="reward-value">x6</div> 
                            </div> 
                            <div class="reward-item"> 
                                <div>好感度</div> 
                                <div class="reward-value">+40</div> 
                            </div> 
                            <div class="reward-item"> 
                                <div>门派声望</div> 
                                <div class="reward-value">+20</div> 
                            </div> 
                        `;
                        actions = ` 
                            <button class="action-btn primary-btn" onclick="acceptReward()">接受谢礼</button> 
                            <button class="action-btn secondary-btn" onclick="askRecipe()">询问丹方</button> 
                        `;
                        
                        // 添加成功特效
                        const effect = document.createElement('div');
                        effect.className = 'success-effect';
                        document.getElementById('rescue-minigame').appendChild(effect);
                        setTimeout(() => effect.remove(), 1500);
                    } else {
                        resultText = '你手忙脚乱的操作反而加剧了炉火暴动！只听一声巨响，丹炉炸裂开来，滚烫的丹液四处飞溅！';
                        rewards = `
                            <div class="reward-item">
                                <div>伤势</div>
                                <div class="reward-value">-20% HP</div>
                            </div>
                            <div class="reward-item">
                                <div>门派声望</div>
                                <div class="reward-value">-25</div>
                            </div>
                            <div class="reward-item">
                                <div>灵石赔偿</div>
                                <div class="reward-value">-500</div>
                            </div>
                        `;
                        actions = `
                            <button class="action-btn primary-btn" onclick="compensate()">赔偿损失</button>
                            <button class="action-btn secondary-btn" onclick="escape()">趁机逃跑</button>
                        `;
                        
                        // 添加失败特效
                        const effect = document.createElement('div');
                        effect.className = 'failure-effect';
                        document.getElementById('rescue-minigame').appendChild(effect);
                        setTimeout(() => effect.remove(), 500);
                    }
                    
                    showResultPanel(resultText, rewards, actions);
                    document.getElementById('rescue-minigame').style.display = 'none';
                }
            });
        });
        
        // 开始小游戏计时
        function startGameTimer() {
            timeLeft = 10;
            document.getElementById('time').textContent = timeLeft;
            clearInterval(timer);
            
            timer = setInterval(() => {
                timeLeft--;
                document.getElementById('time').textContent = timeLeft;
                
                if(timeLeft <= 0) {
                    clearInterval(timer);
                    const resultText = '你犹豫太久，错失了控制炉火的最佳时机！狂暴的火焰吞噬了整个丹炉，伴随着震耳欲聋的爆炸声，炼丹室瞬间化为火海！';
                    const rewards = `
                        <div class="reward-item">
                            <div>伤势</div>
                            <div class="reward-value">-10% HP</div>
                        </div>
                        <div class="reward-item">
                            <div>门派惩罚</div>
                            <div class="reward-value">-50</div>
                        </div>
                        <div class="reward-item">
                            <div>心魔</div>
                            <div class="reward-value">+1</div>
                        </div>
                    `;
                    const actions = `
                        <button class="action-btn primary-btn" onclick="helpVictim()">照料伤者</button>
                        <button class="action-btn secondary-btn" onclick="escape()">逃离现场</button>
                    `;
                    
                    showResultPanel(resultText, rewards, actions);
                    document.getElementById('rescue-minigame').style.display = 'none';
                }
            }, 1000);
        }
        
        // 主动流程小游戏逻辑
        let teachingTimer;
        let teachingTimeLeft = 30;
        let flameLevel = 60;
        let stability = 70;
        let mistakes = 0;
        let instructionInterval;
        let lastInstruction = '';
        
        // 重置教学小游戏
        function resetTeachingGame() {
            flameLevel = 60;
            stability = 70;
            mistakes = 0;
            teachingTimeLeft = 30;
            document.getElementById('teaching-time').textContent = teachingTimeLeft;
            updateFlameIndicator();
            updateStabilityBar();
            clearInterval(instructionInterval);
            
            // 开始随机生成指令
            instructionInterval = setInterval(generateInstruction, 4000);
            generateInstruction();
        }
        
        // 更新火焰指示器
        function updateFlameIndicator() {
            const flameElement = document.getElementById('flame-level');
            flameElement.style.height = `${flameLevel}%`;
            
            // 根据火焰级别改变颜色
            if(flameLevel > 80) {
                flameElement.style.background = 'linear-gradient(to top, #ff0000, #ff6b6b)';
            } else if(flameLevel > 60) {
                flameElement.style.background = 'linear-gradient(to top, #ff6b6b, #ffd700)';
            } else if(flameLevel > 40) {
                flameElement.style.background = 'linear-gradient(to top, #ffd700, #4caf50)';
            } else {
                flameElement.style.background = 'linear-gradient(to top, #4caf50, #2196f3)';
            }
        }
        
        // 更新稳定性条
        function updateStabilityBar() {
            const stabilityBar = document.getElementById('stability-bar');
            stabilityBar.style.width = `${stability}%`;
        }
        
        // 生成随机指令
        function generateInstruction() {
            const instructions = [
                "丹火过旺，请降低火势！",
                "火力不足，请增强火势！",
                "丹炉震动，请稳定丹炉！",
                "药香外泄，请加强密封！",
                "灵气紊乱，请调整法诀！"
            ];
            
            let newInstruction;
            do {
                newInstruction = instructions[Math.floor(Math.random() * instructions.length)];
            } while (newInstruction === lastInstruction);
            
            lastInstruction = newInstruction;
            document.getElementById('instruction').textContent = newInstruction;
        }
        
        // 结束教学小游戏
        function endTeachingGame() {
            let resultText = '';
            let rewards = '';
            let actions = '';
            let showAnalysis = false;
            
            if(stability >= 80 && mistakes <= 2) {
                resultText = '在你的悉心指导下，王铁柱成功炼制出一炉上品聚气丹！他激动得热泪盈眶："今日方知丹道真谛！"为表感谢，他不仅与你分享丹药，还赠送了一张珍藏的古丹方。';
                rewards = ` 
                    <div class="reward-item"> 
                        <div>上品聚气丹</div> 
                        <div class="reward-value">x8</div> 
                    </div> 
                    <div class="reward-item"> 
                        <div>古丹方</div> 
                        <div class="reward-value">x1</div> 
                    </div> 
                    <div class="reward-item"> 
                        <div>好感度</div> 
                        <div class="reward-value">+50</div> 
                    </div> 
                    <div class="reward-item"> 
                        <div>师道威望</div> 
                        <div class="reward-value">+30</div> 
                    </div> 
                `;
                actions = ` 
                    <button class="action-btn primary-btn" onclick="acceptReward()">接受谢礼</button> 
                    <button class="action-btn secondary-btn" onclick="offerJob()">邀请合作</button> 
                `;
            } else if(stability >= 60 && mistakes <= 4) {
                resultText = '经过你的指导，王铁柱勉强完成了炼丹，但成丹率不高。他有些沮丧但仍感激："多谢道友指点，看来我还需勤加练习。"他送你几颗成丹作为谢礼。';
                rewards = `
                    <div class="reward-item">
                        <div>中品聚气丹</div>
                        <div class="reward-value">x4</div>
                    </div>
                    <div class="reward-item">
                        <div>好感度</div>
                        <div class="reward-value">+20</div>
                    </div>
                `;
                actions = `
                    <button class="action-btn primary-btn" onclick="acceptReward()">接受丹药</button>
                    <button class="action-btn secondary-btn" onclick="offerAdvice()">给予建议</button>
                `;
                showAnalysis = true;
            } else {
                resultText = '教学过程中多次失误，丹炉最终冒出黑烟，药材全部报废。王铁柱跪地泣血："我终究是废物..."他深受打击，三日内不愿见人。';
                rewards = `
                    <div class="reward-item">
                        <div>愧疚药渣</div>
                        <div class="reward-value">x1</div>
                    </div>
                    <div class="reward-item">
                        <div>好感度</div>
                        <div class="reward-value">-15</div>
                    </div>
                `;
                actions = `
                    <button class="action-btn primary-btn" onclick="comfort()">安慰劝解</button>
                    <button class="action-btn secondary-btn" onclick="closeResult()">默默离开</button>
                `;
                showAnalysis = true;
            }
            
            showResultPanel(resultText, rewards, actions);
            document.getElementById('teaching-minigame').style.display = 'none';
            
            if(showAnalysis) {
                generateAnalysisReport();
                document.getElementById('analysis-panel').style.display = 'block';
            }
        }
        
        // 生成分析报告
        function generateAnalysisReport() {
            const analysisContent = document.getElementById('analysis-content');
            let content = '';
            
            if(stability >= 60) {
                content = `
                    <div class="analysis-point">控火能力：良好</div>
                    <div class="analysis-point">指导耐心：中等</div>
                    <div class="analysis-point">王铁柱领悟：基础丹道</div>
                    <div class="analysis-point">建议：多练习控火技巧，提高稳定性</div>
                `;
            } else {
                content = `
                    <div class="analysis-point">控火能力：较差</div>
                    <div class="analysis-point">指导耐心：不足</div>
                    <div class="analysis-point">王铁柱领悟：无</div>
                    <div class="analysis-point">建议：先提升自身丹道修为再教学</div>
                `;
            }
            
            analysisContent.innerHTML = content;
        }
        
        // 关闭结果面板
        function closeResult() {
            document.getElementById('result-panel').style.display = 'none';
        }
        
        // 示例操作函数
        function acceptReward() {
            showResultPanel('你接受了谢礼，王铁柱深深一揖："道友大恩，永世不忘！他日若有需要，尽管吩咐！"', '', '<button class="action-btn primary-btn" onclick="closeResult()">继续</button>');
        }
        
        function askRecipe() {
            showResultPanel('王铁柱面露难色："这...此乃家传秘方..."犹豫片刻后他咬牙道："但道友救命之恩，无以为报！"他取出一张泛黄的丹方塞入你手中。', '<div class="reward-item"><div>古丹方</div><div class="reward-value">x1</div></div>', '<button class="action-btn primary-btn" onclick="closeResult()">感谢离开</button>');
        }
        
        function helpVictim() {
            showResultPanel('你救助了受伤的王铁柱，他虚弱地说："多谢...道友..."三日后他登门道谢，并带来一份珍贵谢礼。', '<div class="reward-item"><div>千年灵芝</div><div class="reward-value">x1</div></div><div class="reward-item"><div>好感度</div><div class="reward-value">+30</div></div>', '<button class="action-btn primary-btn" onclick="closeResult()">接受谢礼</button>');
        }
        
        function offerRecipe() {
            showResultPanel('你献出一张珍贵丹方："此方价值远超玄铁，请长老宽恕！"长老查看后点头："念你知错能改，此次小惩大诫。"', '<div class="reward-item"><div>门派惩罚</div><div class="reward-value">-50</div></div><div class="reward-item"><div>丹方</div><div class="reward-value">-1</div></div>', '<button class="action-btn primary-btn" onclick="closeResult()">谢恩离开</button>');
        }

        function changeMind() {
            showResultPanel('你来到王铁柱的丹房，发现他正对着一炉废丹发呆。"道友？"他惊讶转身，眼中重燃希望。你挽起衣袖："今日便与你同炼此丹！"',
            '<div class="reward-item"><div>好感度</div><div class="reward-value">+20</div></div>',
            '<button class="action-btn primary-btn" onclick="startTeachingAfterChangeMind()">开始指导</button>');
        }

        function startTeachingAfterChangeMind() {
            closeResult();
            resetTeachingGame();
            document.getElementById('teaching-minigame').style.display = 'block';
            startTeachingGame();
        }

        function apologize() {
            showResultPanel('你取出三块上品灵石："方才是在下鬼迷心窍，这些灵石权当赔偿。"王铁柱神色稍缓："道友既知错...罢了，望你好自为之。"',
            '<div class="reward-item"><div>灵石</div><div class="reward-value">-300</div></div>'+
            '<div class="reward-item"><div>好感度</div><div class="reward-value">-15</div></div>',
            '<button class="action-btn primary-btn" onclick="closeResult()">尴尬离开</button>');
        }

        function fight() {
            showResultPanel('你祭出法宝："区区杂役也敢放肆！"王铁柱怒极反笑："好！好！今日便领教高招！"战斗引来了执法长老...',
            '<div class="reward-item"><div>门派惩罚</div><div class="reward-value">-100</div></div>'+
            '<div class="reward-item"><div>伤势</div><div class="reward-value">-25% HP</div></div>',
            '<button class="action-btn primary-btn" onclick="pleadGuilty()">认罪受罚</button>'+
            '<button class="action-btn tertiary-btn" onclick="escapeSect()">叛逃宗门</button>');
        }
        
        function pleadGuilty() {
            showResultPanel('你低头认罪："弟子知错，甘愿受罚。"执法长老点头："念你知错，面壁思过一月，罚俸半年。"王铁柱看着你被带走，神情复杂。',
            '<div class="reward-item"><div>禁闭</div><div class="reward-value">30天</div></div>'+
            '<div class="reward-item"><div>灵石</div><div class="reward-value">-500</div></div>',
            '<button class="action-btn primary-btn" onclick="closeResult()">接受惩罚</button>');
        }
        
        function escapeSect() {
            showResultPanel('你施展遁术逃离宗门，身后传来执法长老的怒喝："叛徒休走！"从此你成为宗门通缉要犯，开始了逃亡生涯。',
            '<div class="reward-item"><div>通缉令</div><div class="reward-value">x1</div></div>'+
            '<div class="reward-item"><div>灵石</div><div class="reward-value">-1000</div></div>',
            '<button class="action-btn primary-btn" onclick="closeResult()">继续逃亡</button>');
        }
        
        function resistArrest() {
            showResultPanel('你祭出法宝反抗执法弟子："休想擒我！"双方战作一团，引来更多长老。最终你寡不敌众被擒，修为被废去大半。',
            '<div class="reward-item"><div>修为</div><div class="reward-value">-70%</div></div>'+
            '<div class="reward-item"><div>禁闭</div><div class="reward-value">100年</div></div>',
            '<button class="action-btn primary-btn" onclick="closeResult()">接受命运</button>');
        }
        
        function comfort() {
            showResultPanel('你轻拍王铁柱的肩膀："丹道之路漫长，失败乃成功之母。"他擦干眼泪："多谢道友开导，我会继续努力的！"',
            '<div class="reward-item"><div>好感度</div><div class="reward-value">+10</div></div>',
            '<button class="action-btn primary-btn" onclick="closeResult()">离开</button>');
        }
        
        function offerJob() {
            showResultPanel('你邀请王铁柱："不如加入我的炼丹团队，共同研习丹道？"他惊喜万分："真的吗？多谢道友提携！"',
            '<div class="reward-item"><div>助手</div><div class="reward-value">x1</div></div>'+
            '<div class="reward-item"><div>炼丹效率</div><div class="reward-value">+20%</div></div>',
            '<button class="action-btn primary-btn" onclick="closeResult()">欢迎加入</button>');
        }
        
        function offerAdvice() {
            showResultPanel('你指出王铁柱炼丹中的关键问题："火候转换要如行云流水，不可生硬。"他恍然大悟："原来如此！多谢指点！"',
            '<div class="reward-item"><div>丹道感悟</div><div class="reward-value">+10</div></div>'+
            '<div class="reward-item"><div>好感度</div><div class="reward-value">+15</div></div>',
            '<button class="action-btn primary-btn" onclick="closeResult()">离开</button>');
        }
        
        // 显示炼丹师流程弹窗
        function showAlchemistModal(type) {
            const modal = document.getElementById('alchemist-modal');
            const modalTitle = document.getElementById('modal-title');
            const modalContent = document.getElementById('modal-content');
            
            modal.style.display = 'block';
            
            let title = '';
            let content = '';
            
            switch(type) {
                case 'merchant':
                    title = '商人型炼丹师交互流程';
                    content = `
                        <div class="process-section">
                            <h3><i class="fas fa-coins feature-icon"></i>被动流程：市井揽客</h3>
                            <div class="process-point">金光绳索拦路、法螺吆喝、试吃丹雾</div>
                            <div class="process-point">参与交互：正价购买（50灵石）/八折赌药袋（40灵石选五色袋）</div>
                            <div class="process-point">结果：金袋暴赚、赤袋血亏，可怒砸药摊或威胁举报</div>
                        </div>
                        <div class="process-section">
                            <h3><i class="fas fa-balance-scale feature-icon"></i>主动流程：砍价炼丹</h3>
                            <div class="process-point">玩家携带稀有药材，商人提议炼药</div>
                            <div class="process-point">尝试交互：砍价小游戏（初始300灵石，可用人情/威胁/利诱牌降价）</div>
                            <div class="process-point">等待进展：炼丹时商人偷减料，需手速检测</div>
                            <div class="process-point">结果：成功监视则成丹品质+30%，漏检则得劣质丹</div>
                            <div class="process-point">感受归因：连续赌中触发分成，砍价过低触发打手</div>
                            <div class="process-point">操作自由点：赌袋可贿赂炉灵、砍价可假装离去、发现减料可敲诈</div>
                        </div>
                    `;
                    break;
                    
                case 'expert':
                    title = '专家型炼丹师交互流程';
                    content = `
                        <div class="process-section">
                            <h3><i class="fas fa-fire feature-icon"></i>被动流程：丹狂暴走</h3>
                            <div class="process-point">炉火青转炽白，专家嘶吼，炉壁裂纹</div>
                            <div class="process-point">参与交互：QTE描补裂纹，失败则开启灵力疏导迷宫</div>
                            <div class="process-point">结果：成功炼出焚脉丹（火系伤害+50%减寿），失败道基受损</div>
                        </div>
                        <div class="process-section">
                            <h3><i class="fas fa-user-secret feature-icon"></i>主动流程：偷师问道</h3>
                            <div class="process-point">专家开坛讲道，玩家观摩开启偷师模式</div>
                            <div class="process-point">尝试交互：双轨系统（偷学条+警戒值），需屏息隐蔽气息</div>
                            <div class="process-point">等待进展：九转阶段，每转扫视全场，炉火化形金乌巡场</div>
                            <div class="process-point">结果：完美偷师领悟控术，被发现则根据好感度拜师或战斗</div>
                            <div class="process-point">感受归因：完美偷师解锁禁术，试药获抗毒体</div>
                            <div class="process-point">策略操作：故意暴露触发拜师、论道虚构典籍、试药前服中和剂</div>
                        </div>
                    `;
                    break;
                    
                case 'novice':
                    title = '初学者炼丹师交互流程';
                    content = `
                        <div class="process-section">
                            <h3><i class="fas fa-moon feature-icon"></i>被动流程：夜半惊炉</h3>
                            <div class="process-point">子时炼丹堂角落藤炉微颤，玩家踩断枯枝</div>
                            <div class="process-point">参与交互：吓唬（拍肩）/指点（寒玉髓寅时放）/悄悄离开（消音符）</div>
                            <div class="process-point">结果：吓唬导致炸炉，指点成功成丹，离开留毒雾陷阱</div>
                        </div>
                        <div class="process-section">
                            <h3><i class="fas fa-dove feature-icon"></i>主动流程：笨鸟归巢</h3>
                            <div class="process-point">玩家炼丹成功率>80%，初学者偷瞄</div>
                            <div class="process-point">尝试交互：冷眼驱赶/招手教学，教学需解答蠢问题</div>
                            <div class="process-point">等待进展：耐心值系统（初始100，答错扣20）</div>
                            <div class="process-point">结果：耐心>60则炼成萤辉丸，<30则打翻丹炉哭跑</div>
                            <div class="process-point">深度养成：丹道启蒙日记、情绪连锁反应、坚持教学触发逆袭</div>
                            <div class="process-point">温情细节：炸炉残渣成哭脸、答对问题冒烟花、瑕疵丹有手写标签</div>
                        </div>
                    `;
                    break;
            }
            
            modalTitle.textContent = title;
            modalContent.innerHTML = content;
        }
        
        // 关闭弹窗
        document.querySelector('.close').addEventListener('click', function() {
            document.getElementById('alchemist-modal').style.display = 'none';
        });
        
        // 点击弹窗外部关闭
        window.addEventListener('click', function(event) {
            const modal = document.getElementById('alchemist-modal');
            if (event.target === modal) {
                modal.style.display = 'none';
            }
        });
        
        // 初始绑定
        bindOptionEvents();
        
        // 初始化教学按钮事件
        document.getElementById('increase-btn').addEventListener('click', () => {
            flameLevel = Math.min(100, flameLevel + 10);
            updateFlameIndicator();
        });
        
        document.getElementById('decrease-btn').addEventListener('click', () => {
            flameLevel = Math.max(10, flameLevel - 10);
            updateFlameIndicator();
        });
        
        document.getElementById('stabilize-btn').addEventListener('click', () => {
            // 稳定操作有概率成功
            if(Math.random() > 0.3) {
                stability = Math.min(100, stability + 5);
                updateStabilityBar();
            } else {
                stability = Math.max(0, stability - 10);
                updateStabilityBar();
                mistakes++;
            }
        });
        
        // 开始教学小游戏
        function startTeachingGame() {
            resetTeachingGame();
            clearInterval(teachingTimer);
            
            teachingTimer = setInterval(() => {
                teachingTimeLeft--;
                document.getElementById('teaching-time').textContent = teachingTimeLeft;
                
                // 自然稳定性变化
                stability += (Math.random() * 6 - 3);
                stability = Math.max(0, Math.min(100, stability));
                updateStabilityBar();
                
                // 自然火焰变化
                flameLevel += (Math.random() * 4 - 2);
                flameLevel = Math.max(10, Math.min(100, flameLevel));
                updateFlameIndicator();
                
                if(teachingTimeLeft <= 0) {
                    clearInterval(teachingTimer);
                    clearInterval(instructionInterval);
                    endTeachingGame();
                }
            }, 1000);
        }
    </script>
</body>
</html>
