# CircuitCreation
IB JIO TECHNICAL
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Circuit Board Practice</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            min-height: 100vh;
            padding: 20px;
        }
        .container {
            max-width: 1400px;
            margin: 0 auto;
        }
        h1 {
            color: white;
            text-align: center;
            margin-bottom: 10px;
            font-size: 2em;
        }
        .instructions {
            background: rgba(255, 255, 255, 0.95);
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 20px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        .instructions h3 {
            color: #1e3c72;
            margin-bottom: 10px;
        }
        .instructions ul {
            margin-left: 20px;
            color: #333;
        }
        .workspace {
            display: grid;
            grid-template-columns: 1fr 3fr;
            gap: 20px;
            margin-bottom: 20px;
        }
        .components-panel {
            background: rgba(255, 255, 255, 0.95);
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        .components-panel h2 {
            color: #1e3c72;
            margin-bottom: 15px;
            font-size: 1.3em;
        }
        .component-list {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        .component-item {
            background: white;
            padding: 12px;
            border-radius: 8px;
            border: 2px solid #ddd;
            cursor: move;
            transition: all 0.2s;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .component-item:hover {
            border-color: #2a5298;
            transform: translateX(5px);
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
        }
        .component-icon {
            font-size: 1.5em;
        }
        .board {
            background: #1a4d2e;
            border-radius: 10px;
            position: relative;
            min-height: 600px;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
            overflow: hidden;
        }
        .board::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-image: 
                repeating-linear-gradient(0deg, transparent, transparent 49px, rgba(255,255,255,0.05) 49px, rgba(255,255,255,0.05) 50px),
                repeating-linear-gradient(90deg, transparent, transparent 49px, rgba(255,255,255,0.05) 49px, rgba(255,255,255,0.05) 50px);
            pointer-events: none;
        }
        .component {
            position: absolute;
            cursor: move;
            user-select: none;
            z-index: 10;
        }
        .component.selected {
            z-index: 100;
        }
        .switch, .socket, .battery, .bulb, .resistor, .terminal {
            background: white;
            border: 3px solid #333;
            border-radius: 8px;
            padding: 15px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 5px;
        }
        .switch {
            width: 80px;
            height: 100px;
        }
        .switch-toggle {
            width: 40px;
            height: 60px;
            background: #ccc;
            border: 2px solid #333;
            border-radius: 5px;
            position: relative;
            cursor: pointer;
        }
        .switch-lever {
            width: 30px;
            height: 40px;
            background: linear-gradient(135deg, #ff6b6b, #c92a2a);
            border: 2px solid #333;
            border-radius: 3px;
            position: absolute;
            top: 5px;
            left: 3px;
            transition: all 0.3s;
        }
        .switch.on .switch-lever {
            top: 35px;
            background: linear-gradient(135deg, #51cf66, #37b24d);
        }
        .socket {
            width: 90px;
            height: 90px;
        }
        .socket-holes {
            display: flex;
            gap: 15px;
        }
        .socket-hole {
            width: 20px;
            height: 30px;
            background: #222;
            border-radius: 3px;
        }
        .battery {
            width: 70px;
            height: 120px;
        }
        .battery-body {
            width: 50px;
            height: 80px;
            background: linear-gradient(135deg, #fab005, #fd7e14);
            border: 2px solid #333;
            border-radius: 5px;
            position: relative;
        }
        .battery-terminal {
            width: 20px;
            height: 10px;
            background: #888;
            border: 1px solid #333;
            position: absolute;
            top: -10px;
            left: 15px;
        }
        .bulb {
            width: 80px;
            height: 100px;
        }
        .bulb-glass {
            width: 50px;
            height: 50px;
            background: #fff;
            border: 3px solid #333;
            border-radius: 50%;
            position: relative;
            transition: all 0.3s;
        }
        .bulb.lit .bulb-glass {
            background: #ffd43b;
            box-shadow: 0 0 20px #ffd43b, 0 0 40px #ffd43b;
        }
        .bulb-base {
            width: 30px;
            height: 20px;
            background: #999;
            border: 2px solid #333;
            margin-top: 5px;
        }
        .resistor {
            width: 100px;
            height: 60px;
        }
        .resistor-body {
            width: 80px;
            height: 30px;
            background: linear-gradient(90deg, #e67700, #ff922b);
            border: 2px solid #333;
            border-radius: 5px;
            position: relative;
        }
        .resistor-band {
            width: 6px;
            height: 30px;
            background: #333;
            position: absolute;
            top: 0;
        }
        .terminal {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            background: #ffd43b;
        }
        .connection-point {
            width: 16px;
            height: 16px;
            background: #ff6b6b;
            border: 2px solid #333;
            border-radius: 50%;
            position: absolute;
            cursor: crosshair;
            z-index: 20;
            transition: all 0.2s;
        }
        .connection-point:hover {
            background: #ff0000;
            transform: scale(1.3);
        }
        .connection-point.connected {
            background: #51cf66;
        }
        .wire {
            position: absolute;
            pointer-events: none;
            z-index: 5;
        }
        .wire line {
            stroke-width: 4;
            stroke: #ffd43b;
        }
        .wire.active line {
            stroke: #51cf66;
            stroke-width: 5;
        }
        .controls {
            background: rgba(255, 255, 255, 0.95);
            padding: 15px;
            border-radius: 10px;
            display: flex;
            gap: 15px;
            justify-content: center;
            flex-wrap: wrap;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        button {
            padding: 12px 24px;
            border: none;
            border-radius: 8px;
            font-size: 1em;
            cursor: pointer;
            transition: all 0.3s;
            font-weight: 600;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        .test-btn {
            background: linear-gradient(135deg, #51cf66, #37b24d);
            color: white;
        }
        .test-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }
        .clear-btn {
            background: linear-gradient(135deg, #ff6b6b, #c92a2a);
            color: white;
        }
        .clear-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }
        .wire-mode-btn {
            background: linear-gradient(135deg, #4dabf7, #228be6);
            color: white;
        }
        .wire-mode-btn.active {
            background: linear-gradient(135deg, #ffd43b, #fab005);
        }
        .status {
            background: rgba(255, 255, 255, 0.95);
            padding: 15px;
            border-radius: 10px;
            margin-top: 20px;
            text-align: center;
            font-size: 1.1em;
            font-weight: 600;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        .status.success {
            color: #37b24d;
            background: #d3f9d8;
        }
        .status.error {
            color: #c92a2a;
            background: #ffe3e3;
        }
        .label {
            font-size: 0.8em;
            font-weight: 600;
            color: #333;
            text-align: center;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>⚡ Circuit Board Connection Practice ⚡</h1>
        
        <div class="instructions">
            <h3>How to Use:</h3>
            <ul>
                <li><strong>Drag components</strong> from the left panel onto the circuit board</li>
                <li><strong>Click "Wire Mode"</strong> button, then click connection points to create wires</li>
                <li><strong>Click switches</strong> to toggle them ON/OFF</li>
                <li><strong>Click "Test Circuit"</strong> to see if your circuit works (bulbs will light up!)</li>
                <li><strong>Try building:</strong> Connect battery → switch → bulb → back to battery</li>
                <li><strong>Drag components</strong> to reposition them on the board</li>
            </ul>
        </div>

        <div class="workspace">
            <div class="components-panel">
                <h2>Components</h2>
                <div class="component-list">
                    <div class="component-item" draggable="true" data-type="switch">
                        <span class="component-icon">🔘</span>
                        <span>Switch</span>
                    </div>
                    <div class="component-item" draggable="true" data-type="socket">
                        <span class="component-icon">🔌</span>
                        <span>Socket</span>
                    </div>
                    <div class="component-item" draggable="true" data-type="battery">
                        <span class="component-icon">🔋</span>
                        <span>Battery</span>
                    </div>
                    <div class="component-item" draggable="true" data-type="bulb">
                        <span class="component-icon">💡</span>
                        <span>Bulb</span>
                    </div>
                    <div class="component-item" draggable="true" data-type="resistor">
                        <span class="component-icon">🎚️</span>
                        <span>Resistor</span>
                    </div>
                    <div class="component-item" draggable="true" data-type="terminal">
                        <span class="component-icon">⭕</span>
                        <span>Terminal</span>
                    </div>
                </div>
            </div>

            <div class="board" id="board">
                <svg id="wiresSvg" style="position: absolute; width: 100%; height: 100%; pointer-events: none;"></svg>
            </div>
        </div>

        <div class="controls">
            <button class="wire-mode-btn" id="wireModeBtn">🔌 Wire Mode (OFF)</button>
            <button class="test-btn" id="testBtn">⚡ Test Circuit</button>
            <button class="clear-btn" id="clearBtn">🗑️ Clear Board</button>
        </div>

        <div class="status" id="status">Drag components to the board to start building your circuit!</div>
    </div>

    <script>
        const board = document.getElementById('board');
        const wiresSvg = document.getElementById('wiresSvg');
        const wireModeBtn = document.getElementById('wireModeBtn');
        const testBtn = document.getElementById('testBtn');
        const clearBtn = document.getElementById('clearBtn');
        const status = document.getElementById('status');

        let componentId = 0;
        let wireMode = false;
        let firstPoint = null;
        let wires = [];
        let components = [];

        // Component templates
        const templates = {
            switch: `<div class="switch-toggle"><div class="switch-lever"></div></div>
                     <div class="connection-point" style="bottom: -8px; left: 10px;"></div>
                     <div class="connection-point" style="bottom: -8px; right: 10px;"></div>
                     <div class="label">Switch</div>`,
            socket: `<div class="socket-holes"><div class="socket-hole"></div><div class="socket-hole"></div></div>
                    <div class="connection-point" style="bottom: -8px; left: 15px;"></div>
                    <div class="connection-point" style="bottom: -8px; right: 15px;"></div>
                    <div class="label">Socket</div>`,
            battery: `<div class="battery-terminal"></div><div class="battery-body"></div>
                     <div class="connection-point" style="top: -8px; left: 22px;"></div>
                     <div class="connection-point" style="bottom: -8px; left: 22px;"></div>
                     <div class="label">Battery</div>`,
            bulb: `<div class="bulb-glass"></div><div class="bulb-base"></div>
                  <div class="connection-point" style="bottom: -8px; left: 10px;"></div>
                  <div class="connection-point" style="bottom: -8px; right: 10px;"></div>
                  <div class="label">Bulb</div>`,
            resistor: `<div class="resistor-body">
                      <div class="resistor-band" style="left: 15px;"></div>
                      <div class="resistor-band" style="left: 30px;"></div>
                      <div class="resistor-band" style="left: 45px;"></div>
                      </div>
                      <div class="connection-point" style="bottom: 10px; left: -8px;"></div>
                      <div class="connection-point" style="bottom: 10px; right: -8px;"></div>
                      <div class="label">Resistor</div>`,
            terminal: `<div class="connection-point" style="top: 20px; left: 20px;"></div>
                      <div class="label">Terminal</div>`
        };

        // Drag from panel
        document.querySelectorAll('.component-item').forEach(item => {
            item.addEventListener('dragstart', e => {
                e.dataTransfer.setData('componentType', e.target.dataset.type);
            });
        });

        board.addEventListener('dragover', e => e.preventDefault());
        
        board.addEventListener('drop', e => {
            e.preventDefault();
            const type = e.dataTransfer.getData('componentType');
            if (type) {
                const rect = board.getBoundingClientRect();
                const x = e.clientX - rect.left - 40;
                const y = e.clientY - rect.top - 50;
                createComponent(type, x, y);
            }
        });

        function createComponent(type, x, y) {
            const comp = document.createElement('div');
            comp.className = `component ${type}`;
            comp.id = `comp-${componentId++}`;
            comp.style.left = `${x}px`;
            comp.style.top = `${y}px`;
            comp.innerHTML = templates[type];
            
            board.appendChild(comp);
            components.push({id: comp.id, type, element: comp, state: false});

            makeDraggable(comp);
            
            if (type === 'switch') {
                comp.querySelector('.switch-toggle').addEventListener('click', e => {
                    e.stopPropagation();
                    toggleSwitch(comp);
                });
            }

            comp.querySelectorAll('.connection-point').forEach(point => {
                point.addEventListener('click', e => {
                    e.stopPropagation();
                    if (wireMode) handleConnectionClick(point);
                });
            });

            updateStatus('Component added! Click Wire Mode to connect components.');
        }

        function makeDraggable(el) {
            let pos = {x: 0, y: 0, mouseX: 0, mouseY: 0};
            
            el.addEventListener('mousedown', e => {
                if (e.target.classList.contains('connection-point') || 
                    e.target.classList.contains('switch-toggle')) return;
                
                e.preventDefault();
                pos.mouseX = e.clientX;
                pos.mouseY = e.clientY;
                
                document.addEventListener('mousemove', drag);
                document.addEventListener('mouseup', stopDrag);
            });

            function drag(e) {
                e.preventDefault();
                pos.x = pos.mouseX - e.clientX;
                pos.y = pos.mouseY - e.clientY;
                pos.mouseX = e.clientX;
                pos.mouseY = e.clientY;
                
                const newLeft = el.offsetLeft - pos.x;
                const newTop = el.offsetTop - pos.y;
                
                el.style.left = Math.max(0, Math.min(board.clientWidth - el.offsetWidth, newLeft)) + 'px';
                el.style.top = Math.max(0, Math.min(board.clientHeight - el.offsetHeight, newTop)) + 'px';
                
                updateWires();
            }

            function stopDrag() {
                document.removeEventListener('mousemove', drag);
                document.removeEventListener('mouseup', stopDrag);
            }
        }

        function toggleSwitch(switchEl) {
            const comp = components.find(c => c.element === switchEl);
            if (comp) {
                comp.state = !comp.state;
                switchEl.classList.toggle('on');
                updateStatus(`Switch ${comp.state ? 'ON' : 'OFF'}`);
            }
        }

        wireModeBtn.addEventListener('click', () => {
            wireMode = !wireMode;
            wireModeBtn.classList.toggle('active');
            wireModeBtn.textContent = wireMode ? '🔌 Wire Mode (ON)' : '🔌 Wire Mode (OFF)';
            firstPoint = null;
            updateStatus(wireMode ? 'Wire mode ON - Click connection points to create wires' : 'Wire mode OFF');
        });

        function handleConnectionClick(point) {
            if (!firstPoint) {
                firstPoint = point;
                point.style.background = '#4dabf7';
                updateStatus('Click another connection point to complete the wire');
            } else {
                if (firstPoint !== point) {
                    createWire(firstPoint, point);
                    firstPoint.style.background = '#ff6b6b';
                    point.classList.add('connected');
                    firstPoint.classList.add('connected');
                }
                firstPoint = null;
            }
        }

        function createWire(point1, point2) {
            const rect1 = point1.getBoundingClientRect();
            const rect2 = point2.getBoundingClientRect();
            const boardRect = board.getBoundingClientRect();
            
            const x1 = rect1.left - boardRect.left + rect1.width / 2;
            const y1 = rect1.top
