<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AMETHYST MATRIX - Supreme Core Engineering Platform</title>
    <link href="https://fonts.googleapis.com/css2?family=Finger+Paint&family=JetBrains+Mono:wght@400;700&family=Space+Grotesk:wght@400;500;700&display=swap" rel="stylesheet">
    
    <script src="https://cdn.jsdelivr.net/npm/gun/gun.js"></script>

    <style>
        :root {
            --bg-base: #06030d;
            --purple-card: rgba(18, 11, 38, 0.75);
            --input-bg: #010005;
            --crystal-primary: #8a2be2;
            --crystal-accent: #c4b5fd;
            --current-font: 'Space Grotesk', sans-serif;
            --global-padding: 20px;
            --global-text-size: 13px;
            --glow-style: 0 0 25px rgba(138, 43, 226, 0.45);
            --glass-blur: blur(20px);
            --card-radius: 16px;
            
            /* Structural Layout Customization Constants */
            --flex-direction-layout: row;
            --card-width-custom: 520px;
            --card-height-custom: 740px;
            --border-thickness: 1px;
            --border-glow-color: rgba(255, 255, 255, 0.08);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: var(--current-font); }
        body { background-color: var(--bg-base); color: #e9e3ff; padding: var(--global-padding); font-size: var(--global-text-size); min-height: 100vh; overflow-x: hidden; transition: background-color 0.3s ease; }

        /* Draggable & Swipable Category Track Layouts */
        .workspace-carousel-container {
            display: flex; 
            flex-direction: var(--flex-direction-layout);
            flex-wrap: var(--flex-wrap-layout, nowrap);
            gap: 20px; 
            overflow-x: var(--overflow-x-layout, auto); 
            overflow-y: var(--overflow-y-layout, hidden);
            padding: 15px 5px;
            scroll-behavior: smooth; cursor: grab; -webkit-overflow-scrolling: touch;
            scrollbar-width: thin; scrollbar-color: var(--crystal-primary) transparent;
        }
        .workspace-carousel-container:active { cursor: grabbing; }

        /* Super Massive Plugin Grid & Dynamic Board Geometry */
        .panel-card { 
            background: var(--purple-card); backdrop-filter: var(--glass-blur); -webkit-backdrop-filter: var(--glass-blur);
            border: var(--border-thickness) solid var(--border-glow-color); border-radius: var(--card-radius); 
            padding: 24px; min-width: calc(var(--card-width-custom) - 40px); width: var(--card-width-custom); flex-shrink: 0;
            box-shadow: var(--glow-style); position: relative; height: var(--card-height-custom); display: flex; flex-direction: column;
            transition: width 0.2s, height 0.2s, border-radius 0.2s;
        }
        .scrollable-body { flex-grow: 1; overflow-y: auto; padding-right: 4px; margin-top: 10px; }
        
        h2 { color: #fff; font-size: 14px; font-weight: 700; letter-spacing: 1px; text-transform: uppercase; padding-bottom: 10px; border-bottom: 1px solid rgba(255,255,255,0.1); display: flex; align-items: center; justify-content: space-between; }
        h3 { color: var(--crystal-accent); font-size: 11px; font-weight: 700; text-transform: uppercase; margin: 12px 0 6px 0; }
        
        .simple-input, .custom-select, .plugin-textarea { 
            width: 100%; background: var(--input-bg); border: 1px solid rgba(255, 255, 255, 0.12); 
            border-radius: 8px; padding: 10px 14px; color: #fff; font-size: 12px; outline: none; margin-bottom: 10px;
        }
        .plugin-textarea { height: 70px; resize: none; font-family: 'JetBrains Mono', monospace; font-size: 11px; }
        .simple-input:focus, .custom-select:focus, .plugin-textarea:focus { border-color: var(--crystal-accent); }

        .workspace-navbar { display: flex; gap: 10px; margin-bottom: 20px; border-bottom: 1px solid rgba(255, 255, 255, 0.08); padding-bottom: 15px; align-items: center; overflow-x: auto; }
        .nav-link-btn { background: transparent; color: #a5b4fc; border: 1px solid rgba(255, 255, 255, 0.08); padding: 8px 16px; border-radius: 8px; cursor: pointer; font-size: 11px; font-weight: bold; text-transform: uppercase; white-space: nowrap; }
        .nav-link-btn:hover, .nav-link-btn.active-tab { background: var(--crystal-primary); color: #fff; box-shadow: var(--glow-style); }

        .luxury-action-btn { background: linear-gradient(135deg, var(--crystal-primary), #5b21b6); color: #fff; border: none; padding: 10px 16px; font-size: 10px; font-weight: 700; text-transform: uppercase; border-radius: 8px; cursor: pointer; display: inline-flex; align-items: center; gap: 6px; justify-content: center; }
        .luxury-action-btn:hover { filter: brightness(1.2); }
        .luxury-action-btn:disabled { background: #1e1b4b; color: #475569; cursor: not-allowed; }
        
        /* Customization Sheet System Sliders */
        .luxury-slider-row { display: flex; align-items: center; justify-content: space-between; margin-bottom: 12px; background: rgba(0,0,0,0.2); padding: 10px 14px; border-radius: 10px; border: 1px solid rgba(255,255,255,0.02); }
        .luxury-slider-row label { font-size: 11px; color: #cbd5e1; }
        .luxury-slider { -webkit-appearance: none; width: 140px; background: #1e1b4b; height: 6px; border-radius: 3px; outline: none; }
        .luxury-slider::-webkit-slider-thumb { -webkit-appearance: none; width: 14px; height: 14px; border-radius: 50%; background: var(--crystal-accent); cursor: pointer; }

        /* Features Matrix Block Miniatures */
        .feature-plugin-node-box { background: rgba(0, 0, 0, 0.4); border: 1px solid rgba(255,255,255,0.05); border-radius: 8px; padding: 12px; margin-bottom: 10px; }

        .installed-pack-card { background: rgba(16, 185, 129, 0.1); border: 1px solid rgba(16, 185, 129, 0.3); border-radius: 8px; padding: 10px; margin-bottom: 8px; display: flex; justify-content: space-between; align-items: center; }
        .theme-swatch-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 8px; margin-top: 5px; }
        .theme-swatch-btn { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.08); padding: 10px; border-radius: 8px; cursor: pointer; text-align: left; transition: all 0.2s; }
        .theme-swatch-btn:hover { background: rgba(255,255,255,0.08); border-color: var(--crystal-accent); }

        /* Team Structure Classes */
        .roster-grid { display: flex; flex-direction: column; gap: 8px; margin-top: 10px; }
        .member-node-row { background: rgba(255,255,255,0.02); border: 1px solid rgba(255,255,255,0.05); padding: 10px; border-radius: 8px; display: flex; justify-content: space-between; align-items: center; }

        #activity-feed { position: fixed; bottom: 20px; right: 20px; z-index: 99999; display: flex; flex-direction: column; gap: 8px; }
        .feed-toast { background: #120b26; color: #fff; padding: 10px 16px; border-radius: 6px; font-size: 11px; font-weight: bold; border: 1px solid var(--crystal-accent); box-shadow: var(--glow-style); }
        #identity-auth-gate { position: fixed; inset: 0; background: #030107; z-index: 999999; display: flex; align-items: center; justify-content: center; padding: 20px; backdrop-filter: blur(20px); }
    </style>
</head>
<body>

    <div id="identity-auth-gate">
        <div class="panel-card" style="height:auto; max-width:460px; box-shadow: 0 0 50px rgba(138,43,226,0.45);">
            <h2 style="font-family:'Finger Paint'; border:none; font-size:22px; justify-content:center; margin-bottom:10px; color:var(--crystal-accent);">🔮 AMETHYST SYSTEM MATRIX</h2>
            <p style="font-size:11px; color:#aaa; margin-bottom:15px; text-align:center;">Enter credential configuration to synchronize peer terminal instances.</p>
            
            <div class="feature-plugin-node-box">
                <h3>Core Profile Registration</h3>
                <input type="text" id="auth-username-input" class="simple-input" placeholder="Create Handle Unique Name...">
                <select id="auth-role-select" class="custom-select" style="margin-bottom:0;">
                    <option value="Operator Node">Role: Station Operator</option>
                    <option value="Admin Vector">Role: Core System Admin Key</option>
                </select>
            </div>
            <button class="luxury-action-btn" style="width:100%; padding:14px;" onclick="verifyGateLogin()">Initialize Terminal Instance</button>
        </div>
    </div>

    <div class="workspace-navbar" id="master-top-navbar">
        <div style="font-size:14px; font-weight:900; margin-right:20px; letter-spacing:1px; color:#fff;" id="brand-logo-output">AMETHYST // CORE</div>
        <button class="nav-link-btn" onclick="scrollCarouselToCard(0)">📁 Data Vaults</button>
        <button class="nav-link-btn" onclick="scrollCarouselToCard(1)">🗳️ Balanced Ballot</button>
        <button class="nav-link-btn" onclick="scrollCarouselToCard(2)">⚙️ Studio Config</button>
        <button class="nav-link-btn" onclick="scrollCarouselToCard(3)">➕ Add Page Workspace</button>
        <button class="nav-link-btn" onclick="scrollCarouselToCard(4)">👥 Cluster Consortium</button>
    </div>

    <div class="workspace-carousel-container" id="master-carousel-track">
        
        <div class="panel-card" id="card-vaults">
            <h2>📁 Data Vaults Engine <span style="font-size:9px; color:var(--crystal-accent);">Category I</span></h2>
            <div class="scrollable-body">
                <div class="feature-plugin-node-box">
                    <h3>Document Upload Streams</h3>
                    <input type="file" id="native-file-pipe" style="display:none;" onchange="executeFileSystemUpload(event)">
                    <button class="luxury-action-btn" style="width:100%; margin-bottom:10px;" onclick="document.getElementById('native-file-pipe').click()">Upload Plaintext Document Layer</button>
                    <input type="text" id="file-search-filter" class="simple-input" placeholder="🔍 Filter documents over ledger..." oninput="renderDriveFilesList()">
                </div>

                <div class="feature-plugin-node-box" id="document-modify-workspace" style="display:none; border-color:var(--crystal-accent);">
                    <h3 style="color:#fff;">✏️ Live Modify Document Buffer</h3>
                    <input type="text" id="edit-file-title-input" class="simple-input" placeholder="Document Label Name...">
                    <textarea id="edit-file-body-textarea" class="plugin-textarea" placeholder="File context buffer sequence stream..."></textarea>
                    <input type="hidden" id="edit-file-target-id">
                    <div style="display:flex; gap:6px;">
                        <button class="luxury-action-btn" style="flex:1;" onclick="saveModifiedDocumentBuffer()">Commit Adjustments</button>
                        <button class="luxury-action-btn" style="background:#475569;" onclick="document.getElementById('document-modify-workspace').style.display='none'">Cancel</button>
                    </div>
                </div>

                <div id="uploaded-files-output-list" style="display:flex; flex-direction:column; gap:8px;"></div>
            </div>
        </div>

        <div class="panel-card" id="card-ballots">
            <h2>🗳️ Balanced Voting Core <span style="font-size:9px; color:var(--crystal-accent);">Category II</span></h2>
            <div class="scrollable-body">
                <div class="feature-plugin-node-box">
                    <h3>Nomination Registration Authority</h3>
                    <p style="font-size:10px; color:#888; margin-bottom:8px;">* Define the target operational role designation that candidates are competing for during this sync window.</p>
                    <input type="text" id="vote-nominee-name-input" class="simple-input" placeholder="Target Candidate Name...">
                    
                    <select id="vote-nominee-target-role" class="custom-select">
                        <option value="Lead Infrastructure Architect">Role: Lead Infrastructure Architect</option>
                        <option value="Consortium Representative Officer">Role: Consortium Representative Officer</option>
                        <option value="Security Perimeter Monitor">Role: Security Perimeter Monitor</option>
                        <option value="Data Layer Integrity Engineer">Role: Data Layer Integrity Engineer</option>
                    </select>

                    <button class="luxury-action-btn" style="width:100%;" onclick="submitPeerNominationToMesh()">Register Candidate Ballot Node</button>
                </div>
                <div class="feature-plugin-node-box">
                    <h3>Active Ballots Pool <span id="voted-receipt-status" style="color:var(--crystal-accent); font-size:10px; float:right;">[BALLOT OPEN]</span></h3>
                    <div id="vote-ballot-live-mountfield" style="margin-top:10px; display:flex; flex-direction:column; gap:6px;"></div>
                </div>
            </div>
        </div>

        <div class="panel-card" id="card-custom">
            <h2>⚙️ Studio Config <span style="font-size:9px; color:var(--crystal-accent);">Category III</span></h2>
            <div class="scrollable-body">
                
                <div class="feature-plugin-node-box" id="admin-pass-gate-box">
                    <h3>🔑 System Core Config Authentication</h3>
                    <p style="font-size:10px; color:#888; margin-bottom:8px;">Provide your password configuration matching string to manifest hidden horizons tabs into your layout.</p>
                    <input type="password" id="custom-secret-pass-input" class="simple-input" placeholder="Enter System Admin Key Passphrase...">
                    <button class="luxury-action-btn" style="width:100%;" onclick="evaluateCustomTabAccessPassphrase()">Verify Master Key</button>
                </div>

                <div class="feature-plugin-node-box" id="active-installed-packs-rack" style="display:none;">
                    <h3>📦 Installed Preset Packs</h3>
                    <div class="installed-pack-card">
                        <div>
                            <div style="font-size:11px; font-weight:bold; color:#fff;">⚡ Cyber Security Pack</div>
                            <div style="font-size:9px; color:#10b981;">Features Enabled</div>
                        </div>
                        <button class="luxury-action-btn" style="padding:4px 8px; font-size:9px;" onclick="pushSystemToast('Cyber Security Pack active')">Install</button>
                    </div>
                </div>

                <div class="feature-plugin-node-box">
                    <h3>📐 Advanced Layout System Modifications</h3>
                    <p style="font-size:10px; color:#888; margin-bottom:10px;">Re-engineer architectural geometry layouts on the fly.</p>
                    
                    <div class="luxury-slider-row">
                        <label>Ecosystem Layout Alignment</label>
                        <select id="layout-axis-select" class="custom-select" style="width:160px; margin-bottom:0; padding:4px;" onchange="alterEcosystemLayoutOrientation(this.value)">
                            <option value="row">Horizontal (Swipable)</option>
                            <option value="column">Vertical (Stacked Continuous)</option>
                            <option value="grid">Multi-Row Wrapping Grid</option>
                        </select>
                    </div>

                    <div class="luxury-slider-row">
                        <label>Panel Module Box Width</label>
                        <input type="range" class="luxury-slider" min="400" max="800" value="520" oninput="modifyPanelBoxGeometry('width', this.value)">
                    </div>

                    <div class="luxury-slider-row">
                        <label>Panel Module Box Height</label>
                        <input type="range" class="luxury-slider" min="500" max="1000" value="740" oninput="modifyPanelBoxGeometry('height', this.value)">
                    </div>

                    <div class="luxury-slider-row">
                        <label>Container Border Thickness</label>
                        <input type="range" class="luxury-slider" min="0" max="10" value="1" oninput="document.documentElement.style.setProperty('--border-thickness', this.value + 'px')">
                    </div>
                </div>

                <div class="feature-plugin-node-box">
                    <h3>🛠️ Live UI Label Transformation & Textures</h3>
                    <input type="text" id="dom-target-header-text" class="simple-input" placeholder="Change Main Title Text...">
                    <button class="luxury-action-btn" style="width:100%; margin-bottom:10px;" onclick="modifySystemGlobalLabels()">Mutate Top Title Text</button>

                    <div class="luxury-slider-row">
                        <label>Navbar Button Font Weight</label>
                        <select id="dom-font-weight-select" class="custom-select" style="width:150px; margin-bottom:0; padding:4px;" onchange="adjustInterfaceTypography()">
                            <option value="normal">Normal</option>
                            <option value="500">Medium</option>
                            <option value="bold">Bold</option>
                            <option value="900">Ultra-Black</option>
                        </select>
                    </div>

                    <div class="luxury-slider-row">
                        <label>Container Border Color Base</label>
                        <input type="color" value="#333333" style="background:none; border:none; cursor:pointer;" oninput="document.documentElement.style.setProperty('--border-glow-color', this.value)">
                    </div>
                </div>

                <div class="feature-plugin-node-box">
                    <h3>Dynamic Preset Themes Selection</h3>
                    <div class="theme-swatch-grid">
                        <button class="theme-swatch-btn" onclick="applyPresetThemeMatrix('#06030d', '#120b26', '#8a2be2', '#c4b5fd', '#010005')">
                            <span style="color:#fff; font-size:11px; font-weight:bold; display:block;">🔮 Amethyst Neon</span>
                        </button>
                        <button class="theme-swatch-btn" onclick="applyPresetThemeMatrix('#022c22', '#064e3b', '#10b981', '#a7f3d0', '#022c22')">
                            <span style="color:#fff; font-size:11px; font-weight:bold; display:block;">🌲 Emerald Matrix</span>
                        </button>
                        <button class="theme-swatch-btn" onclick="applyPresetThemeMatrix('#0f172a', '#1e293b', '#3b82f6', '#93c5fd', '#020617')">
                            <span style="color:#fff; font-size:11px; font-weight:bold; display:block;">🌊 Subzero Slate</span>
                        </button>
                        <button class="theme-swatch-btn" onclick="applyPresetThemeMatrix('#1c0a10', '#2d1520', '#f43f5e', '#fecdd3', '#0f0206')">
                            <span style="color:#fff; font-size:11px; font-weight:bold; display:block;">🍒 Crimson Fracture</span>
                        </button>
                        <button class="theme-swatch-btn" onclick="applyPresetThemeMatrix('#1a1503', '#332906', '#eab308', '#fef08a', '#0a0801')">
                            <span style="color:#fff; font-size:11px; font-weight:bold; display:block;">⚡ Amber Cyber</span>
                        </button>
                        <button class="theme-swatch-btn" onclick="applyPresetThemeMatrix('#0a192f', '#112240', '#64ffda', '#ccd6f6', '#020c1b')">
                            <span style="color:#fff; font-size:11px; font-weight:bold; display:block;">🤖 Synth Aquamarine</span>
                        </button>
                    </div>
                </div>

                <div class="feature-plugin-node-box">
                    <h3>📐 Interface Geometry Sliders</h3>
                    <div class="luxury-slider-row">
                        <label>Panel Corner Radius</label>
                        <input type="range" class="luxury-slider" min="0" max="40" value="16" oninput="document.documentElement.style.setProperty('--card-radius', this.value + 'px')">
                    </div>
                    <div class="luxury-slider-row">
                        <label>Global Canvas Padding</label>
                        <input type="range" class="luxury-slider" min="10" max="45" value="20" oninput="document.documentElement.style.setProperty('--global-padding', this.value + 'px')">
                    </div>
                    <div class="luxury-slider-row">
                        <label>Neon Blur Spread Depth</label>
                        <input type="range" class="luxury-slider" min="0" max="50" value="25" oninput="document.documentElement.style.setProperty('--glow-style', '0 0 ' + this.value + 'px var(--crystal-primary)')">
                    </div>
                </div>
            </div>
        </div>

        <div class="panel-card" id="card-add-page">
            <h2>➕ Add Page Workspace <span style="font-size:9px; color:var(--crystal-accent);">Category IV</span></h2>
            <div class="scrollable-body">
                <div class="feature-plugin-node-box">
                    <h3>Custom Node Constructor</h3>
                    <p style="font-size:10px; color:#888; margin-bottom:8px;">Dynamically manufacture template elements or structural list objects directly into this section matrix view.</p>
                    
                    <input type="text" id="add-page-component-title" class="simple-input" placeholder="Component Display Name...">
                    <textarea id="add-page-component-desc" class="plugin-textarea" placeholder="Enter custom documentation content, specs or values..."></textarea>
                    
                    <button class="luxury-action-btn" style="width:100%;" onclick="appendNewComponentToAddPageLedger()">Compile Object Into View</button>
                </div>

                <div class="feature-plugin-node-box">
                    <h3>Assembled Component Ledger Stack</h3>
                    <div id="add-page-dynamic-injection-zone" style="display:flex; flex-direction:column; gap:8px; margin-top:10px;">
                        <div style="font-size:11px; color:#555; text-align:center;">No custom objects compiled yet.</div>
                    </div>
                </div>
            </div>
        </div>

        <div class="panel-card" id="card-group">
            <h2>👥 Cluster Consortium <span style="font-size:9px; color:var(--crystal-accent);">Category V</span></h2>
            <div class="scrollable-body">
                <div class="feature-plugin-node-box">
                    <h3>Consortium Manifest Directory</h3>
                    <p style="font-size:10px; color:#888; margin-bottom:8px;">Add verified node operators to build synchronized network peer groups across your layout. Unhelpful mock entries/bots are completely omitted.</p>
                    <input type="text" id="group-member-name-input" class="simple-input" placeholder="Enter Operator Username...">
                    <input type="text" id="group-member-role-input" class="simple-input" placeholder="Assign Assignment Designation (e.g. Lead Engineer)...">
                    <button class="luxury-action-btn" style="width:100%;" onclick="registerNewConsortiumMember()">Attach Peer to Consortium</button>
                </div>

                <div class="feature-plugin-node-box">
                    <h3>Active Team Members Matrix List</h3>
                    <div class="roster-grid" id="consortium-roster-mountfield"></div>
                </div>
            </div>
        </div>

    </div>

    <div id="activity-feed"></div>

    <script>
        const gun = Gun(['https://gun-manhattan.herokuapp.com/gun', 'https://relay.peer.ooo/gun']);
        const sharedWorkspaceDataGraph = gun.get('amethyst_massive_universe_v7_run');

        let localUserSessionNodeName = "";
        let localUserSessionRole = "Operator Node";
        let localDriveFilesLedger = [];
        let electionBallotsMap = {};

        function initRealtimeP2PNetworkMeshListeners() {
            sharedWorkspaceDataGraph.get('election_candidates').map().on((cand, id) => {
                if (cand) {
                    electionBallotsMap[id] = { name: cand.name, roleTarget: cand.roleTarget || "General Operator", tally: cand.tally || 0 };
                    rebuildElectionBoothUI();
                } else {
                    delete electionBallotsMap[id];
                    rebuildElectionBoothUI();
                }
            });

            sharedWorkspaceDataGraph.get('shared_files_ledger').map().on((fileData, fileNodeId) => {
                if (fileData) {
                    const idx = localDriveFilesLedger.findIndex(f => f.id === fileNodeId);
                    const fileObj = { id: fileNodeId, title: fileData.title, dataStream: fileData.dataStream, author: fileData.author, size: fileData.size };
                    if (idx > -1) localDriveFilesLedger[idx] = fileObj; else localDriveFilesLedger.push(fileObj);
                    renderDriveFilesList();
                } else {
                    localDriveFilesLedger = localDriveFilesLedger.filter(f => f.id !== fileNodeId);
                    renderDriveFilesList();
                }
            });

            sharedWorkspaceDataGraph.get('consortium_roster').map().on((member, id) => {
                if(member) {
                    renderConsortiumRosterUI(id, member.name, member.role);
                } else {
                    const element = document.getElementById(`roster-id-${id}`);
                    if(element) element.remove();
                }
            });
        }

        function verifyGateLogin() {
            let nameInput = document.getElementById('auth-username-input').value.trim();
            if(!nameInput) return;

            localUserSessionNodeName = nameInput;
            localUserSessionRole = document.getElementById('auth-role-select').value;
            localStorage.setItem('amethyst_terminal_lock', nameInput);

            document.getElementById('brand-logo-output').innerText = `AMETHYST // ${nameInput.toUpperCase()} [${localUserSessionRole.toUpperCase()}]`;
            document.getElementById('identity-auth-gate').style.display = 'none';

            initRealtimeP2PNetworkMeshListeners();
            pushSystemToast(`🌟 Terminal Linked: ${nameInput}`);
        }

        function evaluateCustomTabAccessPassphrase() {
            const passField = document.getElementById('custom-secret-pass-input');
            if (passField.value === "amethyst") {
                pushSystemToast("🔑 Key Accepted! Studio Extended Horizons Unlocked.");
                document.getElementById('active-installed-packs-rack').style.display = "block";
                document.getElementById('admin-pass-gate-box').style.display = "none";
            } else {
                pushSystemToast("🚫 Access Violation: Invalid cryptographic key sequence.");
                passField.value = "";
            }
        }

        function alterEcosystemLayoutOrientation(layoutMode) {
            const track = document.getElementById('master-carousel-track');
            if (layoutMode === "row") {
                document.documentElement.style.setProperty('--flex-direction-layout', 'row');
                track.style.removeProperty('--flex-wrap-layout');
                track.style.removeProperty('--overflow-x-layout');
                track.style.removeProperty('--overflow-y-layout');
                pushSystemToast("📐 Layout: Swipable Horizontal Track Mode.");
            } else if (layoutMode === "column") {
                document.documentElement.style.setProperty('--flex-direction-layout', 'column');
                track.style.setProperty('--flex-wrap-layout', 'nowrap');
                track.style.setProperty('--overflow-x-layout', 'hidden');
                track.style.setProperty('--overflow-y-layout', 'visible');
                pushSystemToast("📐 Layout: Continuous Stacked Stream.");
            } else if (layoutMode === "grid") {
                document.documentElement.style.setProperty('--flex-direction-layout', 'row');
                track.style.setProperty('--flex-wrap-layout', 'wrap');
                track.style.setProperty('--overflow-x-layout', 'hidden');
                track.style.setProperty('--overflow-y-layout', 'visible');
                pushSystemToast("📐 Layout: Wrapping Matrix Grid.");
            }
        }

        function modifyPanelBoxGeometry(property, value) {
            if (property === 'width') {
                document.documentElement.style.setProperty('--card-width-custom', value + 'px');
            } else if (property === 'height') {
                document.documentElement.style.setProperty('--card-height-custom', value + 'px');
            }
        }

        function modifySystemGlobalLabels() {
            const val = document.getElementById('dom-target-header-text').value.trim();
            if(val) {
                document.getElementById('brand-logo-output').innerText = val;
                pushSystemToast("🔄 Heading configuration changed.");
                document.getElementById('dom-target-header-text').value = "";
            }
        }

        function adjustInterfaceTypography() {
            const weight = document.getElementById('dom-font-weight-select').value;
            document.querySelectorAll('.nav-link-btn').forEach(el => el.style.fontWeight = weight);
            pushSystemToast(`🔤 Weighting shifted to: ${weight}`);
        }

        function openDocumentModificationInterface(fileNodeId) {
            const doc = localDriveFilesLedger.find(f => f.id === fileNodeId);
            if(!doc) return;

            document.getElementById('edit-file-target-id').value = doc.id;
            document.getElementById('edit-file-title-input').value = doc.title;
            document.getElementById('edit-file-body-textarea').value = doc.dataStream;
            document.getElementById('document-modify-workspace').style.display = "block";
            scrollCarouselToCard(0);
        }

        function saveModifiedDocumentBuffer() {
            const targetId = document.getElementById('edit-file-target-id').value;
            const newTitle = document.getElementById('edit-file-title-input').value.trim();
            const newBody = document.getElementById('edit-file-body-textarea').value;

            if(!newTitle) return;

            sharedWorkspaceDataGraph.get('shared_files_ledger').get(targetId).put({
                title: newTitle, dataStream: newBody, author: localUserSessionNodeName + " (Modified)", size: (newBlobSizeCalc(newBody)) + " KB"
            });

            document.getElementById('document-modify-workspace').style.display = "none";
            pushSystemToast("✅ Data modifications saved.");
        }

        function removeDocumentFromLedger(fileNodeId) {
            sharedWorkspaceDataGraph.get('shared_files_ledger').get(fileNodeId).put(null);
            pushSystemToast("🗑️ Document entry successfully purged.");
        }

        function newBlobSizeCalc(str) { return (encodeURIComponent(str).replace(/%[0-9A-F]{2}/g, 'a').length / 1024).toFixed(1); }

        function appendNewComponentToAddPageLedger() {
            const title = document.getElementById('add-page-component-title').value.trim();
            const desc = document.getElementById('add-page-component-desc').value.trim();

            if(!title || !desc) { pushSystemToast("🚫 Error: Fields incomplete."); return; }

            const mountZone = document.getElementById('add-page-dynamic-injection-zone');
            if(mountZone.querySelector('div') && mountZone.querySelector('div').innerText.includes("No custom objects")) {
                mountZone.innerHTML = "";
            }

            const item = document.createElement('div');
            item.className = "feature-plugin-node-box";
            item.style.borderLeft = "4px solid var(--crystal-primary)";
            item.innerHTML = `
                <div style="font-weight:bold; color:#fff; font-size:12px; margin-bottom:4px;">⚙️ ${title}</div>
                <div style="font-size:11px; color:#aaa; font-family:'JetBrains Mono', monospace; white-space:pre-wrap;">${desc}</div>
                <button class="luxury-action-btn" style="padding:4px 8px; font-size:8px; margin-top:6px; background:#ef4444;" onclick="this.parentElement.remove()">Purge Component Node</button>
            `;
            mountZone.appendChild(item);
            
            document.getElementById('add-page-component-title').value = "";
            document.getElementById('add-page-component-desc').value = "";
            pushSystemToast(`⚡ Compiled component object: ${title}`);
        }

        function registerNewConsortiumMember() {
            const name = document.getElementById('group-member-name-input').value.trim();
            const role = document.getElementById('group-member-role-input').value.trim();

            if(!name || !role) return;

            const entryKey = 'peer_' + Date.now();
            sharedWorkspaceDataGraph.get('consortium_roster').get(entryKey).put({ name: name, role: role });

            document.getElementById('group-member-name-input').value = "";
            document.getElementById('group-member-role-input').value = "";
            pushSystemToast(`👥 Member registered: ${name}`);
        }

        function removeConsortiumMember(id) {
            sharedWorkspaceDataGraph.get('consortium_roster').get(id).put(null);
            pushSystemToast("🗑️ Node operator dropped from database manifest registry.");
        }

        function renderConsortiumRosterUI(id, name, role) {
            const container = document.getElementById('consortium-roster-mountfield');
            if(!container) return;

            let existing = document.getElementById(`roster-id-${id}`);
            if(!existing) {
                existing = document.createElement('div');
                existing.id = `roster-id-${id}`;
                existing.className = "member-node-row";
                container.appendChild(existing);
            }
            existing.innerHTML = `
                <div style="width:70%;">
                    <div style="font-weight:bold; font-size:12px; color:#fff;">👤 ${name}</div>
                    <div style="font-size:10px; color:var(--crystal-accent); font-family:'JetBrains Mono', monospace;">${role}</div>
                </div>
                <button class="luxury-action-btn" style="background:#ef4444; padding:4px 8px; font-size:8px;" onclick="removeConsortiumMember('${id}')">Remove</button>
            `;
        }

        function applyPresetThemeMatrix(bg, card, prim, accent, inputBg) {
            document.documentElement.style.setProperty('--bg-base', bg);
            document.documentElement.style.setProperty('--purple-card', card + "b3");
            document.documentElement.style.setProperty('--crystal-primary', prim);
            document.documentElement.style.setProperty('--crystal-accent', accent);
            document.documentElement.style.setProperty('--input-bg', inputBg);
            pushSystemToast("🎨 Color styles vector synchronized.");
        }

        window.addEventListener('DOMContentLoaded', () => {
            const currentLock = localStorage.getItem('amethyst_terminal_lock');
            if (currentLock) {
                document.getElementById('auth-username-input').value = currentLock;
                document.getElementById('auth-username-input').disabled = true;
                document.getElementById('auth-username-input').style.opacity = "0.5";
            }
            setupCarouselHorizontalGestureDragEngine();
            
            setTimeout(() => {
                const check = document.getElementById('consortium-roster-mountfield');
                if(check && check.children.length === 0) {
                    sharedWorkspaceDataGraph.get('consortium_roster').get('peer_default_1').put({ name: "Monkey D. Luffy", role: "Consortium Captain Vector" });
                    sharedWorkspaceDataGraph.get('consortium_roster').get('peer_default_2').put({ name: "Nico Robin", role: "Archaeological Data Layer Architect" });
                }
            }, 1500);
        });

        function setupCarouselHorizontalGestureDragEngine() {
            const track = document.getElementById('master-carousel-track');
            let isDown = false; let startX; let scrollLeft;

            track.addEventListener('mousedown', (e) => {
                if (document.getElementById('layout-axis-select').value !== "row") return;
                if(e.target.closest('.simple-input') || e.target.closest('.plugin-textarea') || e.target.closest('button') || e.target.closest('input[type="color"]') || e.target.closest('input[type="range"]') || e.target.closest('select')) return;
                isDown = true; track.classList.add('active'); startX = e.pageX - track.offsetLeft; scrollLeft = track.scrollLeft;
            });
            track.addEventListener('mouseleave', () => { isDown = false; });
            track.addEventListener('mouseup', () => { isDown = false; });
            track.addEventListener('mousemove', (e) => { if(!isDown) return; e.preventDefault(); const x = e.pageX - track.offsetLeft; const walk = (x - startX) * 1.5; track.scrollLeft = scrollLeft - walk; });
        }

        function scrollCarouselToCard(cardIdx) {
            const track = document.getElementById('master-carousel-track');
            const targetCards = Array.from(track.querySelectorAll('.panel-card')).filter(el => el.style.display !== "none");
            if(targetCards[cardIdx]) { track.scrollTo({ left: targetCards[cardIdx].offsetLeft - 20, behavior: 'smooth' }); }
        }

        function checkUserHasCastBallot() { return localStorage.getItem(`amethyst_ballot_receipt_v7_${localUserSessionNodeName}`) !== null; }

        function submitPeerNominationToMesh() {
            if (localUserSessionRole !== "Admin Vector") {
                pushSystemToast("🚫 Access Violation: Nominations restricted to verified Admin keys.");
                return;
            }
            const nomineeName = document.getElementById('vote-nominee-name-input').value.trim();
            const targetedRole = document.getElementById('vote-nominee-target-role').value;
            
            if (!nomineeName || nomineeName.length < 3) {
                pushSystemToast("🚫 Error: Invalid candidate sequence.");
                return;
            }
            const uniqueCandId = 'candidate_' + nomineeName.toLowerCase().replace(/\s+/g, '_') + '_' + Math.floor(Math.random() * 1000);
            sharedWorkspaceDataGraph.get('election_candidates').get(uniqueCandId).put({ name: nomineeName, roleTarget: targetedRole, tally: 0 });
            document.getElementById('vote-nominee-name-input').value = "";
            pushSystemToast(`🗳️ Ballot Candidate Added: ${nomineeName}`);
        }

        function castVoteToTargetCandidate(candidateId) {
            if(checkUserHasCastBallot()) { pushSystemToast("🚫 Token limit reached: already voted."); return; }
            const candidateRecord = electionBallotsMap[candidateId];
            if(candidateRecord && candidateRecord.name.toLowerCase() === localUserSessionNodeName.toLowerCase()) {
                pushSystemToast("🚫 Balancing Guard: Cannot vote for self node."); return;
            }
            const tally = electionBallotsMap[candidateId]?.tally || 0;
            sharedWorkspaceDataGraph.get('election_candidates').get(candidateId).get('tally').put(tally + 1);
            localStorage.setItem(`amethyst_ballot_receipt_v7_${localUserSessionNodeName}`, "voted");
            document.getElementById('voted-receipt-status').innerText = "[BALLOT ENFORCED]";
            pushSystemToast("✅ Ballot node securely registered.");
        }

        function purgeBallotCandidateNode(candidateId) {
            sharedWorkspaceDataGraph.get('election_candidates').get(candidateId).put(null);
            pushSystemToast("🗑️ Candidate entry purged.");
        }

        function rebuildElectionBoothUI() {
            const mount = document.getElementById('vote-ballot-live-mountfield'); if(!mount) return; mount.innerHTML = "";
            const keys = Object.keys(electionBallotsMap);
            const userLocked = checkUserHasCastBallot();

            if (keys.length === 0) { mount.innerHTML = '<div style="font-size:11px; color:#555; text-align:center;">No active candidates.</div>'; return; }
            let maxVal = Math.max(...keys.map(k => electionBallotsMap[k].tally), 1);

            keys.forEach(k => {
                const item = electionBallotsMap[k];
                const percentage = (item.tally / maxVal) * 100;
                const disableTag = userLocked ? "disabled" : "";

                const cardRow = document.createElement('div');
                cardRow.style = "background:rgba(0,0,0,0.2); padding:10px; border-radius:6px; display:flex; justify-content:space-between; align-items:center; border:1px solid rgba(255,255,255,0.02); margin-bottom:5px;";
                cardRow.innerHTML = `
                    <div style="width:60%;">
                        <div style="font-size:11px; font-weight:bold;">${item.name}</div>
                        <div style="font-size:9px; color:var(--crystal-accent); margin-bottom:4px; font-family:'JetBrains Mono', monospace;">For: ${item.roleTarget} (${item.tally} votes)</div>
                        <div style="background:#000; height:3px; border-radius:2px; width:100%;"><div style="background:var(--crystal-accent); height:100%; width:${percentage}%;"></div></div>
                    </div>
                    <div style="display:flex; gap:4px;">
                        <button class="luxury-action-btn" style="padding:4px 10px; font-size:8px;" ${disableTag} onclick="castVoteToTargetCandidate('${k}')">Vote</button>
                        <button class="luxury-action-btn" style="background:#ef4444; padding:4px 6px; font-size:8px;" onclick="purgeBallotCandidateNode('${k}')">❌</button>
                    </div>`;
                mount.appendChild(cardRow);
            });
        }

        function executeFileSystemUpload(ev) {
            const f = ev.target.files[0]; if(!f) return;
            const r = new FileReader();
            r.onload = function(e) {
                const uniqueId = 'note_' + Date.now();
                sharedWorkspaceDataGraph.get('shared_files_ledger').get(uniqueId).put({
                    title: f.name, dataStream: e.target.result, author: localUserSessionNodeName || "Station Client", size: (f.size/1024).toFixed(1) + " KB"
                });
                pushSystemToast("📁 Document stream synchronized.");
            };
            r.readAsText(f);
        }

        function renderDriveFilesList() {
            const container = document.getElementById('uploaded-files-output-list'); if(!container) return;
            const key = document.getElementById('file-search-filter').value.toLowerCase().trim();
            container.innerHTML = "";

            if(localDriveFilesLedger.length === 0) {
                container.innerHTML = '<div style="font-size:11px; color:#555; text-align:center;">Vault empty.</div>';
                return;
            }

            localDriveFilesLedger.forEach(file => {
                if(key && !file.title.toLowerCase().includes(key)) return;
                const row = document.createElement('div');
                row.className = "feature-plugin-node-box";
                row.style = "display:flex; justify-content:space-between; align-items:center; margin-bottom:5px;";
                row.innerHTML = `
                    <div style="overflow:hidden; text-overflow:ellipsis; white-space:nowrap; width:50%; font-size:11px;">📄 ${file.title} <br><span style="color:#666; font-size:9px;">By: ${file.author}</span></div>
                    <div style="display:flex; gap:4px;">
                        <button class="luxury-action-btn" style="padding:4px 6px; font-size:9px; background:#1e1b4b;" onclick="openDocumentModificationInterface('${file.id}')">Modify</button>
                        <button class="luxury-action-btn" style="padding:4px 6px; font-size:9px; background:#ef4444;" onclick="removeDocumentFromLedger('${file.id}')">Purge</button>
                    </div>`;
                container.appendChild(row);
            });
        }
    </script>
</body>
</html>
