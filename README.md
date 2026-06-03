<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>EcoKaizen | Portal de Gestión</title>
<style>
    :root { --bg: #0b1120; --card: #161e31; --accent: #3b82f6; --text: #ffffff; }
    body { background: var(--bg); color: var(--text); font-family: 'Segoe UI', sans-serif; padding: 20px; }
    .header { display: flex; align-items: center; gap: 15px; margin-bottom: 20px; }
    .logo { background: var(--accent); padding: 10px; border-radius: 12px; font-weight: bold; }
    .card { background: var(--card); padding: 20px; border-radius: 16px; margin-bottom: 20px; border: 1px solid #2d3748; }
    label { color: #94a3b8; font-size: 12px; text-transform: uppercase; }
    input, select, textarea { width: 100%; background: #0f172a; border: 1px solid #334155; padding: 12px; border-radius: 8px; color: white; margin-top: 5px; box-sizing: border-box; }
    .btn { background: var(--accent); color: white; padding: 15px; border: none; border-radius: 8px; width: 100%; font-weight: bold; cursor: pointer; }
</style>
</head>
<body>

<div class="header">
    <div class="logo">EK</div>
    <div>
        <div style="font-weight:bold">ECOKAIZEN</div>
        <div style="font-size: 10px; color: #94a3b8;">CONTROL Y ABASTECIMIENTO</div>
    </div>
</div>

<div class="card">
    <label>Proveedor</label>
    <select id="prov">
        <option>Don Pedro (Materiales)</option>
        <option>Almacén Principal</option>
    </select>
    
    <label style="margin-top:15px; display:block;">Detalle del Requerimiento</label>
    <textarea id="detalle" rows="4" placeholder="Ingrese suministros..."></textarea>
    
    <button class="btn" onclick="enviar()" style="margin-top: 20px;">GENERAR ORDEN FORMAL</button>
</div>

<script>
function enviar() {
    const p = document.getElementById('prov').value;
    const d = document.getElementById('detalle').value;
    const msg = `🧾 *ECOKAIZEN - ORDEN OFICIAL*\n\n*Proveedor:* ${p}\n*Detalle:* ${d}\n\n*Estado:* PENDIENTE`;
    window.open("https://api.whatsapp.com/send?phone=51949546919&text=" + encodeURIComponent(msg));
}
</script>
</body>
</html>
