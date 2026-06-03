<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>EcoKaizen | Portal de Adquisiciones</title>
<link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600&family=Bebas+Neue&display=swap" rel="stylesheet">
<style>
    :root { --ink: #03060f; --gold: #ffd700; --glass: rgba(20, 20, 25, 0.8); }
    body { background: radial-gradient(circle at center, #1a1a2e 0%, #03060f 100%); font-family: 'Outfit', sans-serif; color: #e0e0e0; display: flex; justify-content: center; align-items: center; min-height: 100vh; margin: 0; padding: 20px; }
    .panel { background: var(--glass); backdrop-filter: blur(20px); border: 1px solid var(--gold); padding: 40px; border-radius: 8px; width: 100%; max-width: 450px; box-shadow: 0 0 30px rgba(255, 215, 0, 0.15); }
    h2 { font-family: 'Bebas Neue'; color: var(--gold); letter-spacing: 3px; margin-bottom: 5px; font-size: 28px; text-transform: uppercase; text-align: center; }
    .manual { font-size: 10px; color: #888; text-align: center; margin-bottom: 25px; border-top: 1px solid #333; pt: 10px; }
    label { font-size: 10px; text-transform: uppercase; letter-spacing: 2px; color: var(--gold); display: block; margin-bottom: 8px; }
    input, textarea, select { width: 100%; padding: 14px; background: rgba(255,255,255,0.03); border: 1px solid #333; border-radius: 4px; color: white; margin-bottom: 20px; box-sizing: border-box; }
    .btn-pro { background: transparent; color: var(--gold); border: 1px solid var(--gold); padding: 16px; width: 100%; font-family: 'Bebas Neue'; font-size: 18px; letter-spacing: 2px; cursor: pointer; transition: 0.4s; }
    .btn-pro:hover { background: var(--gold); color: var(--ink); }
</style>
</head>
<body>

<div class="panel">
    <h2>ADQUISICIONES</h2>
    <div class="manual">Protocolo: ORD-YYYY-XXX | Uso exclusivo ECOKAIZEN</div>
    
    <label>N° DE ORDEN</label>
    <input type="text" id="ref" value="ORD-2026-001">

    <label>Proveedor</label>
    <select id="prov">
        <option>Don Pedro (Materiales)</option>
        <option>Almacén Principal</option>
        <option>Proveedores Varios</option>
    </select>

    <label>Detalle del Lote</label>
    <textarea id="detalle" rows="6" placeholder="🔹 Ítem 01: [Producto] | [Cantidad]&#10;🔹 Ítem 02: [Producto] | [Cantidad]"></textarea>

    <button class="btn-pro" onclick="enviar()">ENVIAR REQUERIMIENTO FORMAL</button>
</div>

<script>
function enviar() {
    const ref = document.getElementById('ref').value;
    const prov = document.getElementById('prov').value;
    const det = document.getElementById('detalle').value;
    
    const msg = `𝐀𝐃𝐐𝐔𝐈𝐒𝐈𝐂𝐈𝐎𝐍𝐄𝐒 | 𝐑𝐄𝐐𝐔𝐄𝐑𝐈𝐌𝐈𝐄𝐍𝐓𝐎 𝐅𝐎𝐑𝐌𝐀𝐋 📑\n` +
                `Ref: ${ref}\n\n` +
                `Estimados, un gusto saludarles. Por encargo de 𝐄𝐂𝐎𝐊𝐀𝐈𝐙𝐄𝐍 𝐏𝐀𝐂𝐊, solicitamos la cotización detallada del siguiente lote:\n\n` +
                `𝐏𝐑𝐎𝐕𝐄𝐄𝐃𝐎𝐑: ${prov}\n\n` +
                `𝐃𝐄𝐓𝐀𝐋𝐋𝐄 𝐃𝐄 𝐒𝐔𝐌𝐈𝐍𝐈𝐒𝐓𝐑𝐎𝐒:\n` +
                `━━━━━━━━━━━━━━━━━━\n` +
                `${det}\n` +
                `━━━━━━━━━━━━━━━━━━`;
    
    window.open("https://api.whatsapp.com/send?phone=51949546919&text=" + encodeURIComponent(msg));
}
</script>
</body>
</html>
