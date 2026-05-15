<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Unutulmaz Döner Online</title>
    <style>
        body { margin: 0; background: #222; color: white; font-family: 'Arial', sans-serif; text-align: center; }
        #game-wrap { position: relative; width: 800px; height: 500px; margin: 20px auto; border: 5px solid #e67e22; border-radius: 15px; overflow: hidden; background: url('https://img.freepik.com/free-vector/isometric-city-street-map-constructor_1284-32543.jpg'); background-size: cover; }
        #player { position: absolute; width: 40px; height: 40px; background: #e67e22; border: 2px solid white; border-radius: 5px; font-size: 10px; display: flex; align-items: center; justify-content: center; transition: transform 0.1s; z-index: 10; }
        .building { position: absolute; background: rgba(255,255,255,0.9); color: #333; border: 2px solid #555; padding: 5px; font-weight: bold; border-radius: 5px; }
        #hud { position: absolute; top: 10px; left: 10px; background: rgba(0,0,0,0.7); padding: 10px; border-radius: 8px; text-align: left; pointer-events: none; }
        #speedo { position: absolute; bottom: 10px; right: 10px; background: rgba(0,0,0,0.7); padding: 10px; border-radius: 50%; width: 60px; height: 60px; display: flex; align-items: center; justify-content: center; border: 2px solid #f1c40f; }
        #chat { position: absolute; bottom: 10px; left: 10px; width: 200px; height: 100px; background: rgba(0,0,0,0.5); font-size: 10px; overflow-y: auto; text-align: left; padding: 5px; }
        .turbo-fire { box-shadow: 0 0 20px #f1c40f; border-color: #f1c40f !important; }
    </style>
</head>
<body>
    <h2>UNUTULMAZ DÖNER: SAVAŞ ŞEHRİ (V2.0)</h2>
    <div id="game-wrap">
        <div id="hud">
            💰 KASA: <span id="m">25.000</span> TL<br>
            🌯 STOK: <span id="s">500</span> KG<br>
            ⚔️ ROL: DADAŞ ŞEF
        </div>
        
        <div class="building" style="top:50px; left:300px; width:200px; height:100px; background:#f39c12;">80 KATLI HOLDİNG</div>
        <div class="building" style="top:300px; left:50px;">RESTORAN 1</div>
        <div class="building" style="top:300px; left:600px;">POLİS MERKEZİ</div>

        <div id="player">DADAŞ</div>
        
        <div id="speedo">0 KM/H</div>
        <div id="chat">Sistem: Online bağlandı.<br>Dadaş06: Restoran 1 hazır!</div>
    </div>
    <p><b>WASD</b> ile sür, <b>SHIFT</b> ile Turbo aç! (Canva'da tıkla ve oyna)</p>

    <script>
        let p = { x: 400, y: 250, v: 0, ang: 0, t: false };
        let keys = {};
        const playerEl = document.getElementById('player');
        const speedo = document.getElementById('speedo');

        window.onkeydown = (e) => keys[e.key.toLowerCase()] = true;
        window.onkeyup = (e) => keys[e.key.toLowerCase()] = false;

        function update() {
            p.t = keys['shift'];
            let maxV = p.t ? 10 : 4;
            
            if (keys['w']) p.v = Math.min(p.v + 0.2, maxV);
            else if (keys['s']) p.v = Math.max(p.v - 0.2, -2);
            else p.v *= 0.95;

            if (keys['a']) p.ang -= 0.05;
            if (keys['d']) p.ang += 0.05;

            p.x += Math.cos(p.ang) * p.v;
            p.y += Math.sin(p.ang) * p.v;

            // Sınırlar
            p.x = Math.max(0, Math.min(760, p.x));
            p.y = Math.max(0, Math.min(460, p.y));

            playerEl.style.left = p.x + 'px';
            playerEl.style.top = p.y + 'px';
            playerEl.style.transform = `rotate(${p.ang * 57}deg)`;
            playerEl.className = p.t ? 'turbo-fire' : '';
            
            speedo.innerText = Math.round(p.v * 40) + " KM/H";
            speedo.style.color = p.t ? "#f1c40f" : "white";

            requestAnimationFrame(update);
        }
        update();
    </script>
</body>
</html>
