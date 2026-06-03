<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>EcoKaizen · Sistema de Abastecimiento</title>
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@300;400;500;600&family=Barlow:wght@300;400;500;600;700&family=Barlow+Condensed:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
:root { --bg:#07090f; --s1:#0c101a; --s2:#111827; --s3:#1a2438; --border:#1e2d47; --accent:#1d6ef5; --text:#dce8f8; --muted:#4a6385; --success:#0af0a0; --danger:#f5341d; --mono:'IBM Plex Mono', monospace; --sans:'Barlow', sans-serif; --cond:'Barlow Condensed', sans-serif; }
body { background: var(--bg); color: var(--text); font-family: var(--sans); min-height: 100vh; }
#view-internal { display: block; }
#view-erp      { display: none; }
.int-wrap { max-width: 700px; margin: 0 auto; padding: 32px 20px 80px; }
.topbar { display:flex; align-items:center; gap:14px; padding-bottom:20px; border-bottom:1px solid var(--border); margin-bottom:32px; }
.ek-logo { width:40px; height:40px; border-radius:8px; background:linear-gradient(140deg, var(--accent), #0d3fa0); display:flex; align-items:center; justify-content:center; font-family:var(--mono); font-size:13px; color:#fff; }
.panel { background:var(--s1); border:1px solid var(--border); border-radius:10px; padding:20px; margin-bottom:14px; }
input, textarea, select { width:100%; background:var(--bg); border:1px solid var(--border); border-radius:6px; padding:12px; color:var(--text); font-family:var(--mono); font-size:13px; margin-top:8px; }
textarea { min-height:150px; resize:vertical; }
.btn-gen { width:100%; padding:16px; background:linear-gradient(135deg, var(--accent) 0%, #0d3fa0 100%); border:none; border-radius:8px; color:#fff; font-family:var(--cond); font-size:14px; font-weight:700; letter-spacing:2px; cursor:pointer; margin-top:16px; }
.loader { display:none; align-items:center; gap:12px; padding:14px; margin-top:14px; background:var(--s2); border-radius:8px; font-size:11px; color:var(--muted); }
.loader.on { display:flex; }
/* ERP Styles */
#view-erp { background:var(--bg); min-height:100vh; padding: 20px; }
.order-header-card { background:var(--s1); border:1px solid var(--border); border-radius:10px; padding:20px; margin-bottom:20px; }
.ohc-id-value { font-family:var(--mono); font-size:22px; color:var(--accent); }
.ticket-item { display:grid; grid-template-columns: 2fr 1fr 1fr; padding:15px; border-bottom:1px solid var(--border); align-items:center; }
.ticket-header { background:var(--s2); font-weight:bold; font-size:10px; text-transform:uppercase; }
.btn-confirm { padding:13px; border-radius:6px; border:none; cursor:pointer; background:#128c3e; color:#fff; width:100%; margin-top:10px; }
</style>
</head>
<body>

<div id="view-internal">
  <div class="int-wrap">
    <div class="topbar"><div class="ek-logo">EK</div><div><div style="font-weight:bold; letter-spacing:2px;">ECOKAIZEN</div><div style="font-size:9px; color:var(--muted);">SISTEMA DE ABASTECIMIENTO</div></div></div>
    
    <div class="panel">
      <label>PROVEEDOR</label>
      <input type="text" id="f-proveedor" placeholder="Ej: Don Pedro">
      <label style="margin-top:15px; display:block;">REQUERIMIENTO</label>
      <textarea id="f-detalle" placeholder="Dicta o escribe aquí tus ítems..."></textarea>
      <button class="btn-gen" id="btn-generar" onclick="generarOrden()">GENERAR ORDEN DE COMPRA</button>
      <div class="loader" id="loader"><div class="spin"></div><span>Procesando requerimiento...</span></div>
    </div>
  </div>
</div>

<div id="view-erp">
  <div class="container">
    <div class="order-header-card">
      <div class="ohc-id-label">N° ORDEN</div>
      <div class="ohc-id-value" id="erp-orden-num"></div>
      <div id="items-tbody" style="margin-top:20px;"></div>
      <button class="btn-confirm" onclick="confirmarOrden()">CONFIRMAR DISPONIBILIDAD (WhatsApp)</button>
    </div>
  </div>
</div>

<script>
async function generarOrden() {
  const p = document.getElementById('f-proveedor').value;
  const d = document.getElementById('f-detalle').value;
  document.getElementById('loader').classList.add('on');
  
  // Simulación de IA rápida
  setTimeout(() => {
    document.getElementById('loader').classList.remove('on');
    document.getElementById('erp-orden-num').textContent = 'OC-' + Date.now().toString().slice(-6);
    document.getElementById('items-tbody').innerHTML = `<div class="ticket-item ticket-header"><div>Producto</div><div>Cant.</div><div>Notas</div></div><div class="ticket-item"><div>${d}</div><div>-</div><div>-</div></div>`;
    document.getElementById('view-internal').style.display = 'none';
    document.getElementById('view-erp').style.display = 'block';
  }, 1500);
}

function confirmarOrden() {
  window.open('https://api.whatsapp.com/send?phone=51949546919&text=' + encodeURIComponent('Confirmo disponibilidad de la orden ' + document.getElementById('erp-orden-num').textContent));
}
</script>
</body>
</html>
