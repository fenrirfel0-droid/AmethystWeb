<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AMETHYST - Basic Education Curriculum Matrix</title>
    <link href="https://fonts.googleapis.com/css2?family=Finger+Paint&family=JetBrains+Mono:wght@400;700&family=Space+Grotesk:wght@400;700&display=swap" rel="stylesheet">
    
    <style>
        /* CSS Variables Matrix */
        :root {
            --bg-base: #0a0618;
            --purple-card: rgba(24, 18, 54, 0.6);
            --input-bg: #000000;
            --crystal-primary: #8a2be2;
            --crystal-accent: #b19ffb;
            --current-font: 'Space Grotesk', sans-serif;
            --global-padding: 24px;
            --global-text-size: 13px;
            --glow-style: 0 0 16px rgba(138, 43, 226, 0.35);
            --glass-blur: blur(12px);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: var(--current-font); transition: background 0.25s ease, border-color 0.25s ease, box-shadow 0.25s ease; }
        body { background-color: var(--bg-base); color: #e2d9ff; padding: var(--global-padding); font-size: var(--global-text-size); min-height: 100vh; }

        /* Premium Floating Glass Cards */
        .panel-card { 
            background: var(--purple-card); 
            backdrop-filter: var(--glass-blur); -webkit-backdrop-filter: var(--glass-blur);
            border: 1px solid rgba(255, 255, 255, 0.08); 
            border-radius: 16px; padding: 25px; margin-bottom: 24px; 
            box-shadow: var(--glow-style); position: relative;
        }
        .section-sub-card {
            background: rgba(0, 0, 0, 0.25);
            border: 1px solid rgba(255, 255, 255, 0.05);
            border-radius: 12px;
            padding: 18px;
            margin-bottom: 16px;
        }
        h2 { color: #fff; font-size: 14px; letter-spacing: 1px; margin-bottom: 15px; text-transform: uppercase; display: flex; align-items: center; gap: 8px; }
        h3 { color: var(--crystal-accent); font-size: 12px; text-transform: uppercase; margin-bottom: 12px; letter-spacing: 0.5px; display: flex; align-items: center; gap: 6px;}
        
        /* Input Fields */
        .search-bar, .simple-input, .custom-select { 
            width: 100%; background: var(--input-bg); border: 1px solid rgba(255, 255, 255, 0.12); 
            border-radius: 10px; padding: 14px; color: #fff; font-size: var(--global-text-size); outline: none; margin-bottom: 10px;
        }
        .search-bar:focus, .simple-input:focus, .custom-select:focus { border-color: var(--crystal-accent); box-shadow: 0 0 8px var(--crystal-primary); }

        /* Navigation Deck Row */
        .workspace-navbar { display: flex; gap: 10px; margin-bottom: 24px; border-bottom: 1px solid rgba(255, 255, 255, 0.08); padding-bottom: 18px; flex-wrap: wrap; align-items: center; }
        .nav-link-btn { background: transparent; color: #fff; border: 1px solid rgba(255, 255, 255, 0.1); padding: 10px 18px; border-radius: 10px; cursor: pointer; font-size: 11px; font-weight: bold; text-transform: uppercase; letter-spacing: 0.5px; display: flex; align-items: center; gap: 6px; }
        .nav-link-btn:hover, .nav-link-btn.active-tab { background: var(--crystal-primary); border-color: var(--crystal-accent); box-shadow: var(--glow-style); }

        /* Note Document Nodes */
        .widget-item-node { background: rgba(0, 0, 0, 0.35); padding: 16px; border-radius: 12px; margin-top: 14px; border: 1px solid rgba(255, 255, 255, 0.05); border-left: 4px solid var(--crystal-primary); }
        .widget-header-row { display: flex; justify-content: space-between; align-items: center; font-size: 10px; font-weight: bold; color: var(--crystal-accent); margin-bottom: 10px; letter-spacing: 0.5px; }
        .widget-text-area { width: 100%; height: 90px; background: rgba(0,0,0,0.4); border: 1px solid rgba(255,255,255,0.1); border-radius: 8px; padding: 12px; color: #fff; font-size: var(--global-text-size); outline: none; resize: none; line-height: 1.5; }

        /* Action Buttons */
        .luxury-action-btn { background: linear-gradient(135deg, var(--crystal-primary), #52189c); color: #fff; border: none; padding: 12px 16px; font-size: 10px; font-weight: 700; text-transform: uppercase; border-radius: 8px; cursor: pointer; letter-spacing: 0.5px; display: inline-flex; align-items: center; gap: 4px;}
        .luxury-action-btn:hover { filter: brightness(1.15); box-shadow: var(--glow-style); }
        
        /* Views & Filtering rules */
        .tab-content-panel { display: none; }
        .tab-content-panel.active-view { display: block; }
        .dynamic-created-view { display: none; }

        /* Theme Preset Grid */
        .preset-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(130px, 1fr)); gap: 8px; margin-bottom: 16px; }
        .preset-btn { border: 1px solid rgba(255,255,255,0.15); border-radius: 8px; padding: 12px; color: #fff; font-size: 11px; font-weight: bold; text-align: center; cursor: pointer; text-transform: uppercase; }

        /* Addon Marketplace Grid */
        .addon-market-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 14px; margin-top: 10px; }
        .addon-card { background: rgba(255, 255, 255, 0.02); border: 1px solid rgba(255, 255, 255, 0.06); border-radius: 12px; padding: 16px; display: flex; flex-direction: column; justify-content: space-between; }

        /* Drawer Overlay */
        #demonology-secret-menu { position: fixed; top: 0; bottom: 0; right: 0; width: 100%; max-width: 340px; background: #0c081f; border-left: 2px solid #00ffcc; z-index: 5000; padding: 25px; overflow-y: auto; display: none; box-shadow: -10px 0 30px rgba(0,0,0,0.6); }
        .session-user-row { background: rgba(0,0,0,0.3); border-radius: 8px; padding: 12px; margin-bottom: 8px; border-left: 4px solid var(--crystal-primary); }

        /* Toast Popup Notifiers */
        #activity-feed { position: fixed; bottom: 20px; left: 20px; z-index: 9999; display: flex; flex-direction: column; gap: 8px; pointer-events: none; }
        .feed-toast { background: var(--crystal-primary); color: #fff; padding: 10px 16px; border-radius: 8px; font-size: 11px; font-weight: bold; box-shadow: var(--glow-style); border: 1px solid var(--crystal-accent); }
        
        #identity-auth-gate { position: fixed; inset: 0; background: #05030f; z-index: 99999; display: flex; align-items: center; justify-content: center; padding: 15px; }
    </style>
</head>
<body>

    <div id="identity-auth-gate">
        <div class="panel-card" style="width: 100%; max-width: 400px; text-align: center;">
            <h2 style="display:block; font-family: 'Finger Paint', cursive; font-size: 24px; margin-bottom: 5px;">🔮 AMETHYST DECK</h2>
            <p id="gate-subtitle" style="font-size: 12px; color: var(--crystal-accent); margin-bottom: 18px;">Premium Custom Matrix Binder Deck</p>
            
            <label style="font-size:11px; color:#fff; font-weight:bold; text-transform:uppercase; display:block; margin-bottom:4px;">🌍 Select System Language / Piliin ang Wika</label>
            <select id="gate-language-selector" class="custom-select" style="text-align-last: center;" onchange="applyLanguagePackMatrix(this.value)">
                <option value="en">English (Default)</option>
                <option value="fil">Filipino (Tagalog)</option>
            </select>

            <input type="text" id="auth-username-input" class="simple-input" placeholder="Enter Connected Student Session Name..." style="text-align:center;">
            <button id="gate-connect-btn" class="luxury-action-btn" style="width:100%;" onclick="verifyGateLogin()">Establish Profile Core Connection</button>
        </div>
    </div>

    <div class="workspace-navbar" id="dynamic-navbar-container">
        <div style="font-size:16px; color:#fff; font-weight:900; margin-right:auto; letter-spacing:1px;" id="brand-logo-output">AMETHYST CORE</div>
        <button class="nav-link-btn active-tab" id="tab-btn-home" onclick="switchActiveViewTab('view-home', this)">📁 <span id="nav-lbl-home">Notes Binder</span></button>
        <button class="nav-link-btn" id="tab-btn-themes" onclick="switchActiveViewTab('view-themes-panel', this)">🔧 <span>Elite Settings</span></button>
        <button class="nav-link-btn" id="tab-btn-directory" onclick="switchActiveViewTab('view-directory', this)">👥 <span id="nav-lbl-roster">Member Roster</span></button>
        <button class="nav-link-btn" id="tab-btn-extensions" style="border-color:#ca9ffb; color:#ca9ffb;" onclick="switchActiveViewTab('view-extensions', this)">➕ <span id="nav-lbl-add">Add Page</span></button>
    </div>

    <div id="view-home" class="tab-content-panel active-view">
        <div id="global-addon-station-mount"></div>

        <div class="panel-card">
            <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 14px; flex-wrap: wrap; gap: 8px;">
                <h2 id="lbl-storage-title">Amethyst Operational Storage Locker</h2>
                <div style="display: flex; gap: 6px;">
                    <button id="btn-upload-file" class="luxury-action-btn" onclick="document.getElementById('native-file-pipe').click()">📂 Upload Plaintext Note</button>
                    <input type="file" id="native-file-pipe" style="display: none;" onchange="executeFileSystemUpload(event)">
                </div>
            </div>
            
            <div style="display: flex; justify-content: space-between; font-size: 11px; color: var(--crystal-accent); background: rgba(0,0,0,0.4); padding: 12px; border-radius: 8px; margin-bottom: 14px; border: 1px solid rgba(255,255,255,0.03)">
                <span id="stat-count">TOTAL ENROLLED ASSETS: 0</span>
                <span id="stat-weight">WEIGHT QUANTUM: 0.00 KB</span>
            </div>
            
            <input type="text" id="file-search-filter" class="search-bar" placeholder="🔍 Search written file token titles..." oninput="renderDriveFilesList()">
            
            <div class="file-system-list" id="uploaded-files-output-list">
                <div id="msg-empty-drive" style="color:#555; text-align:center; margin-top:140px; font-size:12px;">Operational file locker empty.</div>
            </div>
        </div>
    </div>

    <div id="view-themes-panel" class="tab-content-panel">
        
        <div class="panel-card">
            <h2 id="lbl-theme-panel-title">🔧 Ultimate Theme Engine Matrix Customizer</h2>
            
            <div style="background: linear-gradient(90deg, rgba(138,43,226,0.15), rgba(0,0,0,0.4)); padding: 14px; border-radius: 12px; border: 1px solid rgba(255,255,255,0.08); margin-bottom: 20px; display: flex; align-items: center; justify-content: space-between; flex-wrap: wrap; gap: 10px;">
                <span style="font-weight: bold; font-size: 12px; display:flex; align-items:center; gap:6px;"><span id="lbl-mid-lang-title">🌍 Hot-Swap Runtime Language / Baguhin ang Wika:</span></span>
                <select id="panel-language-selector" class="custom-select" style="width: auto; margin-bottom: 0; padding: 8px 16px;" onchange="document.getElementById('gate-language-selector').value = this.value; applyLanguagePackMatrix(this.value)">
                    <option value="en">English (Default)</option>
                    <option value="fil">Filipino (Tagalog)</option>
                </select>
            </div>

            <div class="section-sub-card">
                <h3 id="lbl-theme-sec1">🎨 1. Premium Core Presets</h3>
                <div class="preset-grid">
                    <div class="preset-btn" style="background:#0a0618; border-color:#8a2be2;" onclick="loadPremiumPreset('#0a0618','rgba(24,18,54,0.6)','#000000','#8a2be2','#b19ffb')">Amethyst Cyber</div>
                    <div class="preset-btn" style="background:#020205; border-color:#ffffff;" onclick="loadPremiumPreset('#020205','rgba(15,15,20,0.7)','#09090d','#ffffff','#999999')">Midnight Void</div>
                    <div class="preset-btn" style="background:#040e0a; border-color:#00ff88;" onclick="loadPremiumPreset('#040e0a','rgba(6,24,16,0.65)','#020805','#00ff88','#a3ffd6')">Emerald Terminal</div>
                    <div class="preset-btn" style="background:#0f0404; border-color:#ff1144;" onclick="loadPremiumPreset('#0f0404','rgba(31,8,8,0.65)','#070101','#ff1144','#ff99aa')">Crimson Rage</div>
                </div>
            </div>

            <div class="section-sub-card">
                <h3 id="lbl-theme-sec2">🎨 2. Granular Color Sheet Tuners</h3>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(130px, 1fr)); gap: 12px;">
                    <div><label id="lbl-col-bg" style="font-size:11px; display:block; margin-bottom:4px;">Core Background</label><input type="color" id="picker-bg" style="width:100%; height:34px; background:none; border:1px solid rgba(255,255,255,0.1); cursor:pointer;" oninput="document.documentElement.style.setProperty('--bg-base', this.value)"></div>
                    <div><label id="lbl-col-card" style="font-size:11px; display:block; margin-bottom:4px;">Panel Card Tint</label><input type="color" id="picker-card" style="width:100%; height:34px; background:none; border:1px solid rgba(255,255,255,0.1); cursor:pointer;" oninput="updateCardColorTransparency(this.value)"></div>
                    <div><label id="lbl-col-input" style="font-size:11px; display:block; margin-bottom:4px;">Input Base Fill</label><input type="color" id="picker-input" style="width:100%; height:34px; background:none; border:1px solid rgba(255,255,255,0.1); cursor:pointer;" oninput="document.documentElement.style.setProperty('--input-bg', this.value)"></div>
                    <div><label id="lbl-col-primary" style="font-size:11px; display:block; margin-bottom:4px;">Primary Core Hue</label><input type="color" id="picker-primary" style="width:100%; height:34px; background:none; border:1px solid rgba(255,255,255,0.1); cursor:pointer;" oninput="document.documentElement.style.setProperty('--crystal-primary', this.value)"></div>
                </div>
            </div>

            <div class="section-sub-card">
                <h3 id="lbl-theme-sec3">📏 3. Typography & Interface Scale Layout</h3>
                <div style="display:grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap:12px;">
                    <div>
                        <label id="lbl-typo" style="font-size:11px; display:block; margin-bottom:4px;">Workspace Typeface Grid</label>
                        <select class="custom-select" onchange="document.documentElement.style.setProperty('--current-font', this.value)">
                            <option value="'Space Grotesk', sans-serif">Modern Clean Sans</option>
                            <option value="'JetBrains Mono', monospace">Tactical Monospace</option>
                            <option value="'Finger Paint', cursive">Playful Brush Script</option>
                        </select>
                    </div>
                    <div>
                        <label id="lbl-pad" style="font-size:11px; display:block; margin-bottom:4px;">Interface Edge Padding</label>
                        <input type="range" min="10" max="45" value="24" style="width:100%; margin-top:10px; cursor:pointer;" oninput="document.documentElement.style.setProperty('--global-padding', this.value + 'px')">
                    </div>
                    <div>
                        <label id="lbl-text-size-slider" style="font-size:11px; display:block; margin-bottom:4px;">Global Engine Text Scale</label>
                        <input type="range" min="11" max="18" value="13" style="width:100%; margin-top:10px; cursor:pointer;" oninput="document.documentElement.style.setProperty('--global-text-size', this.value + 'px')">
                    </div>
                </div>
            </div>

            <div style="background:rgba(0,0,0,0.3); padding:12px; border-radius:10px; border:1px solid rgba(255,255,255,0.05); display:flex; flex-direction:column; gap:8px;">
                <div style="display:flex; justify-content:space-between; align-items:center;">
                    <span id="lbl-opt-glass" style="font-size:11px; font-weight:bold;">✨ GLASSMORPHISM FROSTED BACKDROP FILTER BLUR</span>
                    <input type="checkbox" checked style="transform:scale(1.2); cursor:pointer;" onchange="document.documentElement.style.setProperty('--glass-blur', this.checked ? 'blur(12px)' : 'none')">
                </div>
                <hr style="border:none; border-top:1px solid rgba(255,255,255,0.05);">
                <div style="display:flex; justify-content:space-between; align-items:center;">
                    <span id="lbl-opt-glow" style="font-size:11px; font-weight:bold;">🌌 HIGH-GLOW HIGH CONTRAST NEON REFLEX DROP SHADOWS</span>
                    <input type="checkbox" checked style="transform:scale(1.2); cursor:pointer;" onchange="toggleGlobalShadowGlows(this.checked)">
                </div>
            </div>

            <div style="margin-top: 15px; border-top: 1px dashed rgba(255,255,255,0.15); padding-top: 20px;">
                <h4 id="lbl-admin-entry-route" style="font-size:11px; margin-bottom:6px; color:#00ffcc;">🔑 ENTRANCE GATE ACCESS PASS TO ADMINISTRATIVE LAYERS</h4>
                <input type="password" id="theme-panel-pass-input" class="search-bar" style="border-color: rgba(0, 255, 204, 0.4);" placeholder="Type passphrase credential token to unlock configurations..." oninput="evaluateAdminPasswordRoute(this.value)">
            </div>
        </div>

        <div class="panel-card" style="border-color: var(--crystal-accent);">
            <h2>🔌 Built-In Premium Addon Marketplace</h2>
            <p style="font-size: 11px; color:#aaa; margin-bottom:12px;">Instantly inject advanced sub-modules into your curriculum console ecosystem without manual code injection layouts.</p>
            
            <div class="addon-market-grid">
                <div class="addon-card">
                    <div>
                        <strong style="color:#fff; font-size:13px;">⏱️ Curriculum Class Session Timer</strong>
                        <p style="font-size:11px; color:#888; margin-top:4px;">Adds an operational countdown clock widget at the top of your binder view to accurately manage lesson pacing milestones.</p>
                    </div>
                    <button class="luxury-action-btn" id="btn-addon-timer" style="margin-top:12px; width:100%; background:#227744;" onclick="toggleAddonInstallation('timer')">Install Addon Module</button>
                </div>
                <div class="addon-card">
                    <div>
                        <strong style="color:#fff; font-size:13px;">📊 K-12 Grade Weight Analyzer</strong>
                        <p style="font-size:11px; color:#888; margin-top:4px;">A quick calculation tool built for teachers to instantly calculate raw student scorecard points into final DepEd percentage weights.</p>
                    </div>
                    <button class="luxury-action-btn" id="btn-addon-grades" style="margin-top:12px; width:100%; background:#227744;" onclick="toggleAddonInstallation('grades')">Install Addon Module</button>
                </div>
                <div class="addon-card">
                    <div>
                        <strong style="color:#fff; font-size:13px;">📑 Student Core SF9 Profile Builder</strong>
                        <p style="font-size:11px; color:#888; margin-top:4px;">Generates a dynamic data-entry scheme template to track individual student general descriptors, actions, and progress flags.</p>
                    </div>
                    <button class="luxury-action-btn" id="btn-addon-sf9" style="margin-top:12px; width:100%; background:#227744;" onclick="toggleAddonInstallation('sf9')">Install Addon Module</button>
                </div>
            </div>
        </div>

    </div>

    <div id="view-directory" class="tab-content-panel">
        <div class="panel-card">
            <h2 id="lbl-roster-title">👥 Connected Active Session Roster</h2>
            <div class="session-network-box" id="network-user-registry"></div>
        </div>
    </div>

    <div id="view-extensions" class="tab-content-panel">
        <div class="panel-card">
            <h2 id="lbl-creator-title">➕ Infinite Custom Notebook Dispatcher Hub</h2>
            <p id="lbl-creator-subtitle" style="font-size:12px; color:#aaa; margin-bottom:12px;">Deploy separate, code-free custom notation tabs instantly using elite core functional templates.</p>
            
            <label id="lbl-inp-name-tag" style="font-size:11px; font-weight:bold; color:var(--crystal-accent); display:block; margin-bottom:4px;">Notebook Page Label Name</label>
            <input type="text" id="new-page-title-input" class="search-bar" placeholder="e.g., Chemistry Lab, History Timeline, Personal Goals Tracker...">
            
            <label id="lbl-inp-template-tag" style="font-size:11px; font-weight:bold; color:var(--crystal-accent); display:block; margin-bottom:4px; margin-top:6px;">Select Layout Blueprint Template</label>
            <select id="new-page-template-select" class="custom-select">
                <option value="blank">📄 Standard Blank Note Sheet (Clean Canvas)</option>
                <option value="matatag">🏫 MATATAG K-10 Curriculum Framework Block</option>
                <option value="shs">🎓 Senior High School Core Subject Outline</option>
            </select>

            <button id="btn-deploy-page" class="luxury-action-btn" style="background:#00ffcc; color:#000; width:100%; margin-top:8px;" onclick="createNewWorkspaceViewPage()">OK (Deploy Custom Templated Notebook Tab)</button>
        </div>
    </div>

    <div id="dynamic-pages-wrapper-zone"></div>

    <div id="demonology-secret-menu">
        <h3 style="color:#00ffcc; font-size:14px; margin-bottom:2px; font-family:'Finger Paint'; text-transform:uppercase;">🔮 ADMIN CONTROL LAYER</h3>
        <p style="font-size:9px; color:#888; text-transform:uppercase; margin-bottom:20px;">Workspace System Settings Console</p>
        
        <div style="background: rgba(0,0,0,0.5); padding: 10px; border-radius: 8px; font-size: 10px; border: 1px dashed rgba(0,255,204,0.3); color: #00ffcc; margin-bottom: 14px;">
            <div>⚡ SYSTEM HEALTH METRIC RATIO: ACTIVE</div>
            <div id="admin-perf-ticker">Core Modules Loaded: 100% | DOM Latency: Normal</div>
        </div>

        <div style="background:#000; padding:12px; border-radius:8px; margin-bottom:15px; border:1px solid rgba(0,255,204,0.15);">
            <span style="font-size:11px; color:#fff; font-weight:bold;">📝 REMODEL CORE BRAND HEADLINE TITLE LOGO</span>
            <input type="text" class="simple-input" style="padding:8px; margin-top:6px; margin-bottom:0;" value="Amethyst Core" oninput="document.getElementById('brand-logo-output').innerText = this.value.toUpperCase()">
        </div>

        <div style="background:#000; padding:12px; border-radius:8px; margin-bottom:15px; border:1px solid rgba(0,255,204,0.15);">
            <span style="font-size:11px; color:#fff; font-weight:bold;">🛡️ STUDENT ACCOUNT CLEARANCE RANK MODIFIER MATRIX</span>
            <div id="moderator-student-editor-list" style="display:flex; flex-direction:column; gap:4px; margin-top:6px;"></div>
        </div>

        <div style="background:#000; padding:12px; border-radius:8px; margin-bottom:15px; border:1px solid rgba(0,255,204,0.15); display: flex; justify-content: space-between; align-items: center;">
            <span style="font-size:11px; color:#fff; font-weight:bold;">❄️ FREEZE INTERACTIVE RENDERS</span>
            <input type="checkbox" id="admin-freeze-toggle" style="cursor: pointer;" onchange="pushSystemToast(this.checked ? '❄️ Interactive state frozen.' : '🔥 Application runtime unfrozen.')">
        </div>

        <div style="background:#000; padding:12px; border-radius:8px; margin-bottom:20px; border:1px solid rgba(0,255,204,0.15); display:flex; flex-direction:column; gap:6px;">
            <span style="font-size:11px; color:#fff; font-weight:bold;">📂 DATABASE CORE STORAGE LEDGER CONTROLS</span>
            <button class="luxury-action-btn" style="width:100%; background:#281b54;" onclick="exportWorkspaceSessionJSON()">📥 Package Binder Backup Packet (.JSON)</button>
            <button class="luxury-action-btn" style="background: #ff0055; width:100%;" onclick="triggerBulkErasure()">🗑️ Purge Locker Document Repositories</button>
        </div>

        <button class="luxury-action-btn" style="width:100%; background:#cc1144; margin-bottom:6px;" onclick="document.getElementById('identity-auth-gate').style.display='flex'; document.getElementById('demonology-secret-menu').style.display='none';">🚨 Force Profile Lockout Switch</button>
        <button class="luxury-action-btn" style="background:#222; width:100%;" onclick="document.getElementById('demonology-secret-menu').style.display='none'">Exit Admin Overlay</button>
    </div>

    <div id="activity-feed"></div>

    <script>
        let virtualDriveStorage = [];
        let networkOperatorRegistry = [];
        let dynamicPageCount = 0;
        let activeSystemLanguageToken = "en";
        
        // Addon States Tracking
        let installedAddonsRegistry = { timer: false, grades: false, sf9: false };
        let countdownTimerIntervalInstance = null;

        const translationLanguageMatrixPack = {
            en: {
                subtitle: "Premium Custom Matrix Binder Deck",
                navHome: "Notes Binder", navThemes: "Elite Settings", navRoster: "Member Roster", navAdd: "Add Page",
                storageTitle: "Amethyst Operational Storage Locker", btnUpload: "📂 Upload Plaintext Note",
                statCount: "TOTAL ENROLLED ASSETS: ", statWeight: "WEIGHT QUANTUM: ", searchPlaceholder: "🔍 Search written file token titles...",
                emptyDrive: "Operational file locker empty.", themeTitle: "🔧 Ultimate Theme Engine Matrix Customizer",
                midLangTitle: "🌍 Hot-Swap Runtime Language / Baguhin ang Wika:",
                themeSec1: "🎨 1. Premium Core Presets", themeSec2: "🎨 2. Granular Color Sheet Tuners",
                themeSec3: "📏 3. Typography & Interface Scale Layout", bgCol: "Core Canvas Background", cardCol: "Panel Card Tint",
                inputCol: "Input Base Fill", primaryCol: "Primary Core Hue", typoLbl: "Workspace Typeface Grid", padLbl: "Interface Edge Padding",
                textSizeLbl: "Global Engine Text Scale",
                optGlass: "✨ GLASSMORPHISM FROSTED BACKDROP FILTER BLUR", optGlow: "🌌 HIGH-GLOW HIGH CONTRAST NEON REFLEX DROP SHADOWS",
                rosterTitle: "👥 Connected Active Session Roster", creatorTitle: "➕ Infinite Custom Notebook Dispatcher Hub",
                creatorSubtitle: "Deploy separate, code-free custom notation tabs instantly using elite core functional templates.",
                lblInpName: "Notebook Page Label Name", lblInpTemp: "Select Layout Blueprint Template", btnDeploy: "OK (Deploy Custom Templated Notebook Tab)",
                adminRoute: "🔑 ENTRANCE GATE ACCESS PASS TO ADMINISTRATIVE LAYERS", usernamePlaceholder: "Enter Connected Student Session Name...",
                gateConnectBtn: "Establish Profile Core Connection", emptyCanvasMsg: "Notebook canvas empty. Trigger content cards utilizing key index commands above.",
                toastPageCreated: "📁 Spawned Notebook Space: ", toastThemeSwapped: "🎨 Swapped UI theme parameters to custom elite variant preset",
                toastProfileBound: "✨ Security node profile bound securely: ", toastAdminGranted: "🔮 ADMINISTRATIVE OVERLAY SYSTEM CONFIGURATIONS ACCESS GRANTED",
                toastUploadSuccess: "📂 Enrolled local note item inside workspace data stack ledger", toastClearance: "🔄 Shifted clearance permission parameter weights.",
                toastPurge: "🚨 REGISTER BULK DATA PURGE SUCCESSFUL", rankStr: "RANK ASSIGNMENT MATRIX STATUS LEVEL TOKEN: ",
                eraseNoteBtn: "✕ Erase Note", remodTitleBtn: "Remod Title", wipePageBtn: "🗑️ Wipe Page Canvas", appendRowBtn: "➕ Append Checkpoint Task Row",
                lblBlockBanner: "🎫 DISPLAY TITLE BANNER STRIP LAYOUT", lblBlockDoc: "📝 MULTI-LINE INDEPENDENT DOCUMENTATION NOTE CARD", lblBlockCheck: "✅ MILESTONE CHECKBOX LIST", appendTaskLineBtn: "➕ Append Task Line Check", dropBlockBtn: "✕ Drop Block"
            },
            fil: {
                subtitle: "Premium na Sistema ng Lalagyan ng mga Tala at Binder",
                navHome: "Binder ng Tala", navThemes: "Elite na Settings", navRoster: "Listahan ng Miyembro", navAdd: "Magdagdag ng Pahina",
                storageTitle: "Amethyst Operational na Taguan ng Dokumento", btnUpload: "📂 Mag-upload ng Plaintext na Tala",
                statCount: "KABUUANG NAIPONG DOKUMENTO: ", statWeight: "TIMBANG NG DATOS: ", searchPlaceholder: "🔍 Maghanap ng pamagat ng tala...",
                emptyDrive: "Walang laman ang iyong taguan ng mga dokumento.", themeTitle: "🔧 Pangunahing Matrix na Tagapamahala ng Tema",
                midLangTitle: "🌍 Hot-Swap Runtime Language / Baguhin ang Wika:",
                themeSec1: "🎨 1. Mga Preset ng Ultra-Premium Elite Core", themeSec2: "🎨 2. Mga Detalyadong Access Tuner ng Kulay at Estilo",
                themeSec3: "📏 3. Pagsasaayos ng Sulat at Laki ng mga Elemento", bgCol: "Pangunahing Background ng Canvas", cardCol: "Kulay ng Panel Card",
                inputCol: "Kulay ng Loob ng Kahon ng Input", primaryCol: "Pangunahing Neon Hue", typoLbl: "Estilo ng Letra sa Workspace", padLbl: "Laki ng Gilid at Pagitan",
                textSizeLbl: "Sukat at Zoom ng Teksto sa Sistema",
                optGlass: "✨ GLASSMORPHISM MALABONG EPEKTO NG BACKGROUND (BLUR)", optGlow: "🌌 NEON REFLEX DROP SHADOWS NA MATAAS ANG KINANG",
                rosterTitle: "👥 Mga Konektadong Account sa Kasalukuyang Session", creatorTitle: "➕ Sentro ng Walang Katapusang Malikhaing Pahina",
                creatorSubtitle: "Maglunsad agad ng hiwalay at malinis na mga tab ng kuwaderno gamit ang mga elite na functional template.",
                lblInpName: "Pangalan at Label ng Pahina ng Kuwaderno", lblInpTemp: "Pumili ng Blueprint at Estilo ng Template", btnDeploy: "OK (Ilatag ang Bagong Pahina ng Kuwaderno)",
                adminRoute: "🔑 LIHIM NA PASUKAN PATUNGO SA ADMINISTRATIVE CONFIGURATIONS", usernamePlaceholder: "Ilagay ang Pangalan ng Estudyante para sa Session...",
                gateConnectBtn: "Ikonekta ang Profile Core sa Workspace", emptyCanvasMsg: "Walang laman ang pahina ng kuwaderno. Gumamit ng mga command sa itaas para maglagay ng card.",
                toastPageCreated: "📁 Matagumpay na Nalikha ang Pahina: ", toastThemeSwapped: "🎨 Nabago ang mga setting ng kulay patungo sa piniling elite na preset",
                toastProfileBound: "✨ Ang iyong profile node ay ligtas na naikonekta: ", toastAdminGranted: "🔮 PINAYAGAN ANG ACCESS SA ADMINISTRATIVE OVERLAY CONFIGURATIONS",
                toastUploadSuccess: "📂 Ang lokal na dokumento ay naidagdag na sa imbakan ng datos", toastClearance: "🔄 Nabago ang antas ng kapangyarihan at pahintulot ng account.",
                toastPurge: "🚨 MATAGUMPAY NA PINURGE AT KINANSELA ANG LAHAT NG DATOS", rankStr: "ANTAS NG PAHINTULOT NG ACCOUNT SA MATRIX: ",
                eraseNoteBtn: "✕ Burahin ang Tala", remodTitleBtn: "Baguhin Titulo", wipePageBtn: "🗑️ Puksain ang Buong Pahina", appendRowBtn: "➕ Magdagdag ng Hanay ng Checkpoint",
                lblBlockBanner: "LAYOUT NG BANNER AT PAMAGAT NG DOKUMENTO", lblBlockDoc: "📝 MULTI-LINE INDEPENDENT DOCUMENTATION NOTE CARD", lblBlockCheck: "✅ LISTAHAN NG MGA LAYUNIN AT CHECKBOX", appendTaskLineBtn: "➕ Magdagdag ng Linya ng Gawain", dropBlockBtn: "✕ Alisin ang Block"
            }
        };

        function applyLanguagePackMatrix(langCode) {
            activeSystemLanguageToken = langCode;
            const dict = translationLanguageMatrixPack[langCode];

            document.getElementById('gate-subtitle').innerText = dict.subtitle;
            document.getElementById('auth-username-input').placeholder = dict.usernamePlaceholder;
            document.getElementById('gate-connect-btn').innerText = dict.gateConnectBtn;
            
            document.getElementById('nav-lbl-home').innerText = dict.navHome;
            document.getElementById('nav-lbl-directory').innerText = dict.navRoster;
            document.getElementById('nav-lbl-add').innerText = dict.navAdd;

            document.getElementById('lbl-storage-title').innerText = dict.storageTitle;
            document.getElementById('btn-upload-file').innerText = dict.btnUpload;
            document.getElementById('file-search-filter').placeholder = dict.searchPlaceholder;
            if(document.getElementById('msg-empty-drive')) document.getElementById('msg-empty-drive').innerText = dict.emptyDrive;

            document.getElementById('lbl-theme-panel-title').innerText = dict.themeTitle;
            document.getElementById('lbl-mid-lang-title').innerText = dict.midLangTitle;
            document.getElementById('lbl-theme-sec1').innerText = dict.themeSec1;
            document.getElementById('lbl-theme-sec2').innerText = dict.themeSec2;
            document.getElementById('lbl-theme-sec3').innerText = dict.themeSec3;
            document.getElementById('lbl-col-bg').innerText = dict.bgCol;
            document.getElementById('lbl-col-card').innerText = dict.cardCol;
            document.getElementById('lbl-col-input').innerText = dict.inputCol;
            document.getElementById('lbl-col-primary').innerText = dict.primaryCol;
            document.getElementById('lbl-typo').innerText = dict.typoLbl;
            document.getElementById('lbl-pad').innerText = dict.padLbl;
            document.getElementById('lbl-text-size-slider').innerText = dict.textSizeLbl;
            document.getElementById('lbl-opt-glass').innerText = dict.optGlass;
            document.getElementById('lbl-opt-glow').innerText = dict.optGlow;

            document.getElementById('lbl-roster-title').innerText = dict.rosterTitle;
            document.getElementById('lbl-creator-title').innerText = dict.creatorTitle;
            document.getElementById('lbl-creator-subtitle').innerText = dict.creatorSubtitle;
            document.getElementById('lbl-inp-name-tag').innerText = dict.lblInpName;
            document.getElementById('lbl-inp-template-tag').innerText = dict.lblInpTemp;
            document.getElementById('lbl-admin-entry-route').innerText = dict.adminRoute;

            document.getElementById('gate-language-selector').value = langCode;
            updateAnalyticsAndRender();
        }

        function switchActiveViewTab(targetPanelId, navigationButtonRef) {
            document.querySelectorAll('.tab-content-panel, .dynamic-created-view').forEach(view => view.style.display = 'none');
            document.querySelectorAll('.nav-link-btn').forEach(btn => btn.classList.remove('active-tab'));
            
            const target = document.getElementById(targetPanelId);
            if(target) target.style.display = 'block';
            if(navigationButtonRef) navigationButtonRef.classList.add('active-tab');
        }

        function loadPremiumPreset(bg, card, input, primary, accent) {
            document.documentElement.style.setProperty('--bg-base', bg);
            document.documentElement.style.setProperty('--purple-card', card);
            document.documentElement.style.setProperty('--input-bg', input);
            document.documentElement.style.setProperty('--crystal-primary', primary);
            document.documentElement.style.setProperty('--crystal-accent', accent);
            
            document.getElementById('picker-bg').value = bg;
            document.getElementById('picker-input').value = input;
            document.getElementById('picker-primary').value = primary;
            pushSystemToast(translationLanguageMatrixPack[activeSystemLanguageToken].toastThemeSwapped);
        }

        function updateCardColorTransparency(hexColorValue) {
            let targetColor = hexColorValue + "a6"; 
            document.documentElement.style.setProperty('--purple-card', targetColor);
        }

        function toggleGlobalShadowGlows(isChecked) {
            let primaryColor = getComputedStyle(document.documentElement).getPropertyValue('--crystal-primary').trim();
            document.documentElement.style.setProperty('--glow-style', isChecked ? `0 0 16px ${primaryColor}59` : 'none');
        }

        /* DYNAMIC ADDON MANAGEMENT MOTOR */
        function toggleAddonInstallation(addonKey) {
            const btn = document.getElementById('btn-addon-' + addonKey);
            
            if (!installedAddonsRegistry[addonKey]) {
                installedAddonsRegistry[addonKey] = true;
                btn.innerText = "Uninstall Addon Module";
                btn.style.background = "#cc1144";
                pushSystemToast(`🔌 Successfully deployed ${addonKey.toUpperCase()} engine core addon component.`);
                injectAddonWidgetUI(addonKey);
            } else {
                installedAddonsRegistry[addonKey] = false;
                btn.innerText = "Install Addon Module";
                btn.style.background = "#227744";
                pushSystemToast(`🗑️ Removed ${addonKey.toUpperCase()} addon module.`);
                removeAddonWidgetUI(addonKey);
            }
        }

        function injectAddonWidgetUI(addonKey) {
            const targetMount = document.getElementById('global-addon-station-mount');
            const wrapper = document.createElement('div');
            wrapper.id = "installed-addon-node-" + addonKey;
            wrapper.className = "panel-card";
            wrapper.style.borderColor = "var(--crystal-primary)";

            if (addonKey === 'timer') {
                wrapper.innerHTML = `
                    <h3>⏱️ Curriculum Pacing Session Timer</h3>
                    <div style="display:flex; gap:10px; align-items:center; margin-top:8px;">
                        <input type="number" id="addon-timer-minutes" class="simple-input" style="width:100px; margin-bottom:0;" value="45" min="1">
                        <span style="font-size:12px; font-weight:bold;">MINS</span>
                        <button class="luxury-action-btn" onclick="executeStartCountdownTimer()">▶️ Start Countdown</button>
                        <div id="countdown-timer-display" style="font-family:'JetBrains Mono'; font-size:18px; color:#00ffcc; font-weight:bold; margin-left:auto;">45:00</div>
                    </div>`;
            } 
            else if (addonKey === 'grades') {
                wrapper.innerHTML = `
                    <h3>📊 K-12 Score-to-Weight Calculator</h3>
                    <div style="display:grid; grid-template-columns: repeat(auto-fit, minmax(100px, 1fr)); gap:8px; margin-top:8px;">
                        <div><label style="font-size:10px;">Raw Score</label><input type="number" id="g-raw" class="simple-input" style="margin-bottom:0;" value="40" oninput="calculateK12PercentageScore()"></div>
                        <div><label style="font-size:10px;">Highest Possible</label><input type="number" id="g-total" class="simple-input" style="margin-bottom:0;" value="50" oninput="calculateK12PercentageScore()"></div>
                        <div><label style="font-size:10px;">Component Weight %</label><input type="number" id="g-weight" class="simple-input" style="margin-bottom:0;" value="30" oninput="calculateK12PercentageScore()"></div>
                        <div style="display:flex; flex-direction:column; justify-content:center; align-items:center; background:rgba(0,0,0,0.4); border-radius:8px;">
                            <span style="font-size:9px; color:#aaa;">WEIGHTED SCORE</span>
                            <strong id="grade-calc-output-score" style="color:#00ffcc; font-size:14px;">24.00%</strong>
                        </div>
                    </div>`;
            }
            else if (addonKey === 'sf9') {
                wrapper.innerHTML = `
                    <h3>📑 DepEd SF9 / Form 137 Student Profiler</h3>
                    <div style="display:grid; grid-template-columns:1fr 1fr; gap:8px; margin-top:8px;">
                        <input type="text" class="simple-input" style="margin-bottom:0;" placeholder="Student Full Name (Apelyido, Pangalan)">
                        <input type="text" class="simple-input" style="margin-bottom:0;" placeholder="LRN (Learner Reference Number)">
                    </div>
                    <textarea class="widget-text-area" style="margin-top:8px; height:50px;" placeholder="Remarks on Core Values / Observed Behavior Flags (e.g., Maka-Diyos, Makatao)..."></textarea>`;
            }

            targetMount.appendChild(wrapper);
        }

        function removeAddonWidgetUI(addonKey) {
            const targetNode = document.getElementById("installed-addon-node-" + addonKey);
            if(targetNode) {
                if (addonKey === 'timer' && countdownTimerIntervalInstance) clearInterval(countdownTimerIntervalInstance);
                targetNode.remove();
            }
        }

        /* TIMER IMPLEMENTATION LOGIC */
        function executeStartCountdownTimer() {
            if(countdownTimerIntervalInstance) clearInterval(countdownTimerIntervalInstance);
            let mins = parseInt(document.getElementById('addon-timer-minutes').value) || 45;
            let totalSeconds = mins * 60;

            const display = document.getElementById('countdown-timer-display');
            countdownTimerIntervalInstance = setInterval(() => {
                if(totalSeconds <= 0) {
                    clearInterval(countdownTimerIntervalInstance);
                    display.innerText = "TIME OUT";
                    pushSystemToast("🔔 Lesson period pacing milestone time window reached!");
                    return;
                }
                totalSeconds--;
                let m = Math.floor(totalSeconds / 60);
                let s = totalSeconds % 60;
                display.innerText = `${m.toString().padStart(2,'0')}:${s.toString().padStart(2,'0')}`;
            }, 1000);
        }

        /* K12 WEIGHTED GRADE CALCULATION */
        function calculateK12PercentageScore() {
            const raw = parseFloat(document.getElementById('g-raw').value) || 0;
            const total = parseFloat(document.getElementById('g-total').value) || 1;
            const weight = parseFloat(document.getElementById('g-weight').value) || 0;

            let percentage = (raw / total) * 100;
            let weighted = (percentage * (weight / 100));
            document.getElementById('grade-calc-output-score').innerText = weighted.toFixed(2) + "%";
        }

        /* PAGE CREATION MATRIX */
        function createNewWorkspaceViewPage() {
            if (document.getElementById('admin-freeze-toggle').checked) { return; }
            const pageTitle = document.getElementById('new-page-title-input').value.trim();
            const chosenTemplate = document.getElementById('new-page-template-select').value;
            const dict = translationLanguageMatrixPack[activeSystemLanguageToken];
            
            if(!pageTitle) { alert(activeSystemLanguageToken === "en" ? "Please enter a valid page name designation." : "Mangyaring maglagay ng wastong pangalan ng pahina."); return; }

            dynamicPageCount++;
            const uniquePageId = "dynamic-page-node-" + dynamicPageCount;
            const uniqueNavBtnId = "nav-btn-node-" + dynamicPageCount;

            const tabBtn = document.createElement('button');
            tabBtn.className = 'nav-link-btn'; tabBtn.id = uniqueNavBtnId;
            tabBtn.style.borderColor = 'var(--crystal-accent)';
            tabBtn.innerText = "📄 " + pageTitle.substring(0,12);
            tabBtn.onclick = function() { switchActiveViewTab(uniquePageId, this); };
            document.getElementById('dynamic-navbar-container').appendChild(tabBtn);

            const canvasView = document.createElement('div');
            canvasView.id = uniquePageId; canvasView.className = 'dynamic-created-view';
            canvasView.innerHTML = `
                <div class="panel-card" style="margin-top: 20px;">
                    <div style="display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:10px; border-bottom:1px dashed rgba(255,255,255,0.1); padding-bottom:12px;">
                        <h2 style="font-family:'Finger Paint'; text-transform:none;">✨ ${pageTitle} [${chosenTemplate.toUpperCase()}]</h2>
                        <button class="luxury-action-btn" style="background:#ff0055;" onclick="purgeDynamicCustomPage('${uniquePageId}', '${uniqueNavBtnId}')">${dict.wipePageBtn}</button>
                    </div>

                    <div style="background:rgba(0,0,0,0.3); padding:14px; border-radius:12px; border:1px solid rgba(255,255,255,0.04); display:flex; flex-direction:column; gap:6px; margin-top:12px;">
                        <span style="font-size:10px; font-weight:bold; color:var(--crystal-accent);" class="lbl-block-selection-header">🧱 APPEND STRUCTURAL CANVAS OBJECT CARDS:</span>
                        <div style="display:flex; gap:6px; flex-wrap:wrap;">
                            <button class="luxury-action-btn" style="padding:8px 14px; background:#4f2299;" onclick="injectComponentToCanvas('${uniquePageId}', 'heading')">➕ Title Banner</button>
                            <button class="luxury-action-btn" style="padding:8px 14px; background:#227744;" onclick="injectComponentToCanvas('${uniquePageId}', 'text')">➕ Note Canvas</button>
                            <button class="luxury-action-btn" style="padding:8px 14px; background:#aa5500;" onclick="injectComponentToCanvas('${uniquePageId}', 'todo')">➕ Checklist Matrix</button>
                        </div>
                    </div>

                    <div style="min-height:200px; margin-top:14px; display:flex; flex-direction:column; gap:12px;" id="mount-point-target-${uniquePageId}">
                        <div style="color:#555; text-align:center; padding-top:70px; font-size:12px;" id="empty-notice-${uniquePageId}">${dict.emptyCanvasMsg}</div>
                    </div>
                </div>`;
            
            document.getElementById('dynamic-pages-wrapper-zone').appendChild(canvasView);
            document.getElementById('new-page-title-input').value = "";
            
            executeTemplateInjectionBlueprint(uniquePageId, chosenTemplate);
            
            pushSystemToast(`${dict.toastPageCreated}${pageTitle}`);
            switchActiveViewTab(uniquePageId, tabBtn);
        }

        function executeTemplateInjectionBlueprint(pageId, templateType) {
            if (templateType === 'blank') return;

            const notice = document.getElementById(`empty-notice-${pageId}`);
            if(notice) notice.remove();

            if (templateType === 'matatag') {
                injectComponentToCanvas(pageId, 'heading', "🏫 MATATAG Lesson Exemplar & Competency Matrix");
                injectComponentToCanvas(pageId, 'text', "🎯 LEARNING COMPETENCIES (Mga Kasanayan):\n- Key Theme / Paksa:\n- Cognitive Process Dimensions:\n\n📝 LESSON FLOW / PAMAMARAAN:\n1. Balik-Aral (Review)\n2. Paghahabi sa Layunin (Motivation)\n3. Pagtalakay (Discussion)\n\n");
                injectComponentToCanvas(pageId, 'todo', "✅ FORMATIVE ASSESSMENT CHECKLIST (Pagtataya)");
            } 
            else if (templateType === 'shs') {
                injectComponentToCanvas(pageId, 'heading', "🎓 SHS Core Subject Syllabus & Performance Stand");
                injectComponentToCanvas(pageId, 'text', "📚 SUBJECT METRICS:\n- Core Strand Component (STEM/ABM/HUMSS/GAS/TVL):\n- Content Standard:\n- Performance Standard:\n\n💡 REFLECTION / REHIYON NG PAGKATUTO:\n\n");
                injectComponentToCanvas(pageId, 'todo', "📌 PERFORMANCE TASK CHECKPOINTS (Outputs)");
            }
        }

        function injectComponentToCanvas(pageId, category, customPresetValueText = "") {
            if (document.getElementById('admin-freeze-toggle').checked) { return; }
            const notice = document.getElementById(`empty-notice-${pageId}`);
            if(notice) notice.remove();
            
            const targetMount = document.getElementById(`mount-point-target-${pageId}`);
            const node = document.createElement('div');
            node.className = 'widget-item-node';

            const dict = translationLanguageMatrixPack[activeSystemLanguageToken];
            const closeBtnHtml = `<span style="color:#ff455f; cursor:pointer; font-weight:bold; font-size:11px;" onclick="this.parentElement.parentElement.remove()">${dict.dropBlockBtn}</span>`;

            if(category === 'heading') {
                let defaultTxt = customPresetValueText || "Type Custom Structural Title Text Heading Header Layer Here...";
                node.innerHTML = `
                    <div class="widget-header-row"><span>${dict.lblBlockBanner}</span>${closeBtnHtml}</div>
                    <input type="text" class="search-bar" value="${defaultTxt}" style="font-weight:bold; color:#fff; font-size:15px; background:transparent; border:none; border-bottom:1px dashed rgba(255,255,255,0.3); border-radius:0; padding:2px; margin-bottom:0;">`;
            } 
            else if (category === 'text') {
                let defaultAreaVal = customPresetValueText || "";
                node.innerHTML = `
                    <div class="widget-header-row"><span>${dict.lblBlockDoc}</span>${closeBtnHtml}</div>
                    <textarea class="widget-text-area" placeholder="Write comprehensive project files or information references inside this clean canvas entry card...">${defaultAreaVal}</textarea>`;
            } 
            else if (category === 'todo') {
                const listId = "todo-container-" + Date.now();
                let listLabelHeaderTitle = customPresetValueText || "Task Milestone Item checkpoint...";
                node.innerHTML = `
                    <div class="widget-header-row"><span>${dict.lblBlockCheck}</span>${closeBtnHtml}</div>
                    <div style="display:flex; flex-direction:column; gap:4px; background:rgba(0,0,0,0.3); padding:10px; border-radius:8px;" id="${listId}">
                        <div style="display:flex; gap:8px; align-items:center;"><input type="checkbox" style="transform:scale(1.1); cursor:pointer;"> <input type="text" value="${listLabelHeaderTitle}" style="background:transparent; color:#fff; border:none; border-bottom:1px solid rgba(255,255,255,0.05); outline:none; font-size:12px; width:100%; padding:2px;"></div>
                    </div>
                    <button class="luxury-action-btn" style="padding:6px 10px; font-size:8px; align-self:flex-start; margin-top:6px;" onclick="appendCheckboxRowItemNode('${listId}')">${dict.appendRowBtn}</button>`;
            }
            
            targetMount.appendChild(node);
            updateLiveAdminMetrics();
        }

        function appendCheckboxRowItemNode(targetListContainerElementId) {
            const listContainer = document.getElementById(targetListContainerElementId);
            if(!listContainer) return;
            const newRow = document.createElement('div');
            newRow.style.display = 'flex'; newRow.style.gap = '8px'; newRow.style.alignItems = 'center';
            newRow.innerHTML = `<input type="checkbox" style="transform:scale(1.1); cursor:pointer;"> <input type="text" class="search-bar" style="background:transparent; border:none; border-bottom:1px solid rgba(255,255,255,0.05); padding:2px; font-size:12px; margin-bottom:0;" placeholder="New checklist task note item...">`;
            listContainer.appendChild(newRow);
        }

        function purgeDynamicCustomPage(viewPanelId, navigationTabButtonElementId) {
            document.getElementById(viewPanelId).remove();
            document.getElementById(navigationTabButtonElementId).remove();
            switchActiveViewTab('view-home', document.getElementById('tab-btn-home'));
            updateLiveAdminMetrics();
        }

        /* ACCESS SECURITY VERIFICATION METHODS */
        function verifyGateLogin() {
            let nameInput = document.getElementById('auth-username-input').value.trim();
            if(!nameInput) { alert(activeSystemLanguageToken === "en" ? "Please input profile identifier string text name." : "Mangyaring maglagay ng pangalan."); return; }
            
            document.getElementById('brand-logo-output').innerText = "AMETHYST // " + nameInput.toUpperCase();
            networkOperatorRegistry.push({ id: "node_" + Date.now(), name: nameInput, role: "Student Node" });
            document.getElementById('identity-auth-gate').style.display = 'none';
            
            rebuildUserRegistryUI(); rebuildOrganizerAdminPanelUI();
            pushSystemToast(`${translationLanguageMatrixPack[activeSystemLanguageToken].toastProfileBound}${nameInput}`);
        }

        function evaluateAdminPasswordRoute(valueString) {
            if (valueString.toLowerCase().trim() === "amethyst") {
                document.getElementById('demonology-secret-menu').style.display = 'block';
                document.getElementById('theme-panel-pass-input').value = "";
                pushSystemToast(translationLanguageMatrixPack[activeSystemLanguageToken].toastAdminGranted);
            }
        }

        /* REPOSITORY AND LOCKER MANAGEMENT PIPES */
        function executeFileSystemUpload(event) {
            const file = event.target.files[0]; if(!file) return;
            const rdr = new FileReader();
            rdr.onload = function(e) {
                virtualDriveStorage.push({ 
                    name: file.name, size: (file.size / 1024).toFixed(2), 
                    content: e.target.result || "Blank data structural field." 
                });
                updateAnalyticsAndRender();
                pushSystemToast(translationLanguageMatrixPack[activeSystemLanguageToken].toastUploadSuccess);
            };
            rdr.readAsText(file);
        }

        function updateAnalyticsAndRender() {
            let totalWeight = 0; 
            for(let i = 0; i < virtualDriveStorage.length; i++) { totalWeight = totalWeight + parseFloat(virtualDriveStorage[i].size); }
            
            const dict = translationLanguageMatrixPack[activeSystemLanguageToken];
            document.getElementById('stat-count').innerText = `${dict.statCount}${virtualDriveStorage.length}`;
            document.getElementById('stat-weight').innerText = `${dict.statWeight}${totalWeight.toFixed(2)} KB`;
            renderDriveFilesList();
            updateLiveAdminMetrics();
        }

        function updateLiveAdminMetrics() {
            const currentTotalBlocksCount = document.querySelectorAll('.widget-item-node').length;
            const customCreatedTabsCount = document.querySelectorAll('.dynamic-created-view').length;
            document.getElementById('admin-perf-ticker').innerText = `Locker Assets: ${virtualDriveStorage.length} | Layout Blocks: ${currentTotalBlocksCount} | Active Custom Tabs: ${customCreatedTabsCount}`;
        }

        function renderDriveFilesList() {
            const searchKeywordFilterToken = document.getElementById('file-search-filter').value.toLowerCase().trim();
            const outputListContainer = document.getElementById('uploaded-files-output-list');
            const dict = translationLanguageMatrixPack[activeSystemLanguageToken];

            if(virtualDriveStorage.length === 0) { 
                outputListContainer.innerHTML = `<div id="msg-empty-drive" style="color:#555; text-align:center; margin-top:140px; font-size:12px;">${dict.emptyDrive}</div>`; 
                return; 
            }
            
            let accumulatedHtmlCodeBlocks = "";
            for(let index = 0; index < virtualDriveStorage.length; index++) {
                const currentFileRecordObject = virtualDriveStorage[index];
                if(searchKeywordFilterToken && !currentFileRecordObject.name.toLowerCase().includes(searchKeywordFilterToken)) { continue; }
                
                accumulatedHtmlCodeBlocks += `
                    <div class="file-item" style="background:rgba(255,255,255,0.02); border-radius:12px; padding:16px; margin-bottom:12px; border:1px solid rgba(255,255,255,0.06); border-left:4px solid var(--crystal-primary);">
                        <div style="display:flex; justify-content:space-between; align-items:center;">
                            <div><span style="color:#fff;"><strong>📄 ${currentFileRecordObject.name}</strong></span><br><span style="font-size:11px; color:var(--crystal-accent);">${currentFileRecordObject.size} KB</span></div>
                            <strong style="color:#ff455f; cursor:pointer; font-size:11px;" onclick="virtualDriveStorage.splice(${index},1); updateAnalyticsAndRender();">${dict.eraseNoteBtn}</strong>
                        </div>
                        <div style="margin-top:8px; display:flex; gap:6px;">
                            <input type="text" id="rename-box-${index}" class="search-bar" style="padding:8px 12px; font-size:11px; margin-bottom:0;" value="${currentFileRecordObject.name}">
                            <button class="luxury-action-btn" style="font-size:9px; padding:8px 12px;" onclick="virtualDriveStorage[${index}].name = document.getElementById('rename-box-${index}').value; updateAnalyticsAndRender();">${dict.remodTitleBtn}</button>
                        </div>
                        <textarea class="widget-text-area" style="margin-top:8px; height:60px;" oninput="virtualDriveStorage[${index}].content = this.value">${currentFileRecordObject.content}</textarea>
                    </div>`;
            }
            outputListContainer.innerHTML = accumulatedHtmlCodeBlocks;
        }

        function pushSystemToast(alertTextString) {
            const toastNotificationBoxNode = document.createElement('div'); 
            toastNotificationBoxNode.className = 'feed-toast'; toastNotificationBoxNode.innerText = alertTextString;
            document.getElementById('activity-feed').appendChild(toastNotificationBoxNode);
            setTimeout(function() { toastNotificationBoxNode.remove(); }, 2500);
        }

        function rebuildUserRegistryUI() {
            let innerHtmlCode = "";
            const dict = translationLanguageMatrixPack[activeSystemLanguageToken];
            for(let i = 0; i < networkOperatorRegistry.length; i++) {
                const u = networkOperatorRegistry[i];
                innerHtmlCode += `<div class="session-user-row"><strong style="color:#fff;">👤 ${u.name}</strong><br><span style="font-size:10px; color:#aaa;">${dict.rankStr}${u.role.toUpperCase()}</span></div>`;
            }
            document.getElementById('network-user-registry').innerHTML = innerHtmlCode;
        }

        function rebuildOrganizerAdminPanelUI() {
            let innerHtmlCode = "";
            for(let i = 0; i < networkOperatorRegistry.length; i++) {
                const user = networkOperatorRegistry[i];
                innerHtmlCode += `
                    <div style="background:#130e29; padding:8px; border-radius:8px; margin-bottom:4px; border:1px solid rgba(255,255,255,0.04);">
                        <div style="font-size:11px; color:#fff;"><strong>👤 ${user.name}</strong> [${user.role}]</div>
                        <select class="custom-select" style="padding:6px; font-size:11px; background:#000; margin-top:4px; margin-bottom:0;" onchange="updateUserRoleIndexMatrix('${user.id}', this.value)">
                            <option value="Student Node">Student Node Permission</option>
                            <option value="Admin Core">Admin Core Authority</option>
                        </select>
                    </div>`;
            }
            document.getElementById('moderator-student-editor-list').innerHTML = innerHtmlCode;
        }

        function updateUserRoleIndexMatrix(userIdTokenString, selectionRoleValueString) {
            for(let i = 0; i < networkOperatorRegistry.length; i++) {
                if(networkOperatorRegistry[i].id === userIdTokenString) { networkOperatorRegistry[i].role = selectionRoleValueString; }
            }
            rebuildUserRegistryUI(); rebuildOrganizerAdminPanelUI();
            pushSystemToast(translationLanguageMatrixPack[activeSystemLanguageToken].toastClearance);
        }

        function triggerBulkErasure() { virtualDriveStorage = []; updateAnalyticsAndRender(); pushSystemToast(translationLanguageMatrixPack[activeSystemLanguageToken].toastPurge); }
        function exportWorkspaceSessionJSON() { 
            const dataStringPacket = JSON.stringify(virtualDriveStorage, null, 2);
            const blobFileSourcePipe = new Blob([dataStringPacket], { type: "application/json" }); 
            const invisibleDownloadLinkAnchorNode = document.createElement('a'); 
            invisibleDownloadLinkAnchorNode.href = URL.createObjectURL(blobFileSourcePipe); 
            invisibleDownloadLinkAnchorNode.download = `amethyst_binder_ledger.json`; 
            invisibleDownloadLinkAnchorNode.click(); 
        }
    </script>
</body>
</html>
