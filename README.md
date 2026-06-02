<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>EcoKaizen · Enterprise Procurement</title>
<link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600&family=Bebas+Neue&display=swap" rel="stylesheet">
<style>
    :root {
        --ink: #03060f;
        --gold: #ffd700;
        --glass: rgba(20, 20, 25, 0.8);
    }
    body {
        background: radial-gradient(circle at center, #1a1a2e 0%, #03060f 100%);
        font-family: 'Outfit', sans-serif;
        color: #e0e0e0;
        display: flex;
        justify-content: center;
        align-items: center;
        min-height: 100vh;
        margin: 0;
    }
    .panel {
        background: var(--glass);
        backdrop-filter: blur(20px);
        border: 1px solid var(--gold);
        padding: 40px;
        border-radius: 8px; /* Estilo corporativo */
        width: 90%;
        max-width: 450px;
        box-shadow: 0 0 30px rgba(255, 215, 0, 0.15);
    }
    h2 { font-family: 'Bebas Neue'; color: var(--gold); letter-spacing: 3px; margin-bottom: 5px; font-size: 32px; text-transform: uppercase; }
    .subtitle { color: var(--gold); font-size: 10px; letter-spacing: 2px; margin-bottom: 30px; opacity: 0.8; }
    label { font-size: 10px; text-transform: uppercase; letter-spacing: 2px; color: var(--gold); display: block; margin-bottom: 8px; }
    input, select, textarea {
        width: 100%;
        padding: 14px;
        background: rgba(255,255,255,0.03);
        border: 1px solid #333;
        border-radius: 4px;
        color: white;
        margin-bottom: 20px;
    }
    .btn-pro {
        background: transparent;
        color: var(--gold);
        border: 1px solid var(--gold);
        padding: 16px;
        width: 100%;
        font-family: 'Bebas Neue';
        font-size: 18px;
        letter-spacing: 2px;
        cursor: pointer;
        transition: 0.4s;
    }
    .btn-pro:hover { background: var(--gold); color: var(--ink); }
</style>
</head>
<body>

<div class="panel">
    <h2>EcoKaizen</h2>
    <div class="subtitle">SISTEMA DE ABASTECIMIENTO INTEGRADO</div>
    
    <label>Proveedor Autorizado</label>
    <select id="prov">
        <option>Don Pedro (Materiales)</option>
        <option>Almacén Principal</option>
        <option>Proveedores Varios</option>
    </select>

    <label>Detalle Técnico de la Orden</label>
    <textarea id="detalle" rows="4" placeholder="Ingrese ítems y cantidades exactas..."></textarea>

    <button class="btn-pro" onclick="enviar()">EMITIR ORDEN DIGITAL</button>
</div>

<script>
function enviar() {
    const p = document.getElementById('prov').value;
    const d = document.getElementById('detalle').value;
    const id = "EK-" + Date.now().toString().slice(-6);
    
    const msg = `━━━━━━━━━━━━━━━━━━━━\n` +
                `*ECOKAIZEN - ORDEN DE COMPRA*\n` +
                `━━━━━━━━━━━━━━━━━━━━\n` +
                `*ID ORDEN:* ${id}\n` +
                `*FECHA:* ${new Date().toLocaleDateString()}\n` +
                `*PROVEEDOR:* ${p}\n\n` +
                `*REQUERIMIENTO:* \n${d}\n\n` +
                `━━━━━━━━━━━━━━━━━━━━\n` +
                `*ESTADO:* PENDIENTE DE VALIDACIÓN\n` +
                `Favor de confirmar recepción inmediata.`;
    
    window.open("https://api.whatsapp.com/send?phone=51949546919&text=" + encodeURIComponent(msg));
}
</script>
</body>
</html>
