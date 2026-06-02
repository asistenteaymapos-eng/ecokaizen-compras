<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>EcoKaizen · Portal de Abastecimiento</title>
<link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600&family=Bebas+Neue&display=swap" rel="stylesheet">
<style>
    :root {
        --ink: #03060f;
        --glass: rgba(255, 255, 255, 0.05);
        --cyan: #00e5ff;
        --txt: #ddeaff;
    }
    body {
        background: var(--ink);
        font-family: 'Outfit', sans-serif;
        color: var(--txt);
        display: flex;
        justify-content: center;
        align-items: center;
        min-height: 100vh;
        margin: 0;
    }
    .panel {
        background: var(--glass);
        backdrop-filter: blur(15px);
        border: 1px solid rgba(255, 255, 255, 0.1);
        padding: 40px;
        border-radius: 24px;
        width: 90%;
        max-width: 450px;
        box-shadow: 0 20px 40px rgba(0,0,0,0.4);
    }
    h2 { font-family: 'Bebas Neue'; color: var(--cyan); letter-spacing: 2px; margin-bottom: 25px; font-size: 28px; }
    .input-box { margin-bottom: 20px; }
    label { font-size: 11px; text-transform: uppercase; letter-spacing: 1px; color: var(--cyan); display: block; margin-bottom: 8px; }
    input, select, textarea {
        width: 100%;
        padding: 12px;
        background: rgba(0,0,0,0.3);
        border: 1px solid rgba(255,255,255,0.1);
        border-radius: 12px;
        color: white;
        font-size: 14px;
    }
    .btn-pro {
        background: var(--cyan);
        color: var(--ink);
        padding: 16px;
        width: 100%;
        border: none;
        border-radius: 12px;
        font-family: 'Bebas Neue';
        font-size: 18px;
        letter-spacing: 1px;
        cursor: pointer;
        transition: 0.3s;
        margin-top: 10px;
    }
    .btn-pro:hover { transform: translateY(-2px); box-shadow: 0 5px 15px rgba(0,229,255,0.3); }
</style>
</head>
<body>

<div class="panel">
    <h2>NUEVA ORDEN EK</h2>
    
    <div class="input-box">
        <label>Proveedor</label>
        <select id="prov">
            <option>Don Pedro (Materiales)</option>
            <option>Almacén Principal</option>
            <option>Proveedores Varios</option>
        </select>
    </div>

    <div class="input-box">
        <label>Especificaciones del Requerimiento</label>
        <textarea id="detalle" rows="4" placeholder="Detalle los materiales y cantidades..."></textarea>
    </div>

    <button class="btn-pro" onclick="enviar()">ENVIAR ORDEN OFICIAL</button>
</div>

<script>
function enviar() {
    const p = document.getElementById('prov').value;
    const d = document.getElementById('detalle').value;
    const id = "EK-" + Date.now().toString().slice(-5);
    
    const msg = `*ORDEN OFICIAL DE COMPRA ${id}*\n\n` +
                `*FECHA:* ${new Date().toLocaleDateString()}\n` +
                `*PROVEEDOR:* ${p}\n\n` +
                `*REQUERIMIENTO:* \n${d}\n\n` +
                `Por favor confirmar recepción de esta orden.`;
    
    window.open("https://api.whatsapp.com/send?phone=51949546919&text=" + encodeURIComponent(msg));
}
</script>
</body>
</html>
