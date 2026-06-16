<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<meta name="theme-color" content="#03060f">
<title>EcoKaizen · Pedidos</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=Space+Mono:wght@400;700&family=Bebas+Neue&display=swap" rel="stylesheet">
<style>
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent}
:root{
  --ink:#03060f;--s2:#0c1530;--s3:#10203f;--b1:#182f5a;--b2:#1f3d77;
  --txt:#e8f0ff;--dim:#3d5585;--muted:#6080b0;
  --blue:#4a90ff;--cyan:#00e5ff;--green:#00ffb3;--red:#ff2d55;
  --amber:#ffcc00;--gold:#ffd700;--purple:#a855f7;
  --wa:#25D366;--wa2:#128C7E;
  --card:rgba(12,21,48,0.95);
}
body{background:var(--ink);font-family:'Space Grotesk',sans-serif;color:var(--txt);min-height:100vh;overflow-x:hidden}
#bg-canvas{position:fixed;inset:0;z-index:0;pointer-events:none;opacity:0.4}

/* SPLASH */
#splash{position:fixed;inset:0;z-index:9999;background:var(--ink);display:flex;flex-direction:column;align-items:center;justify-content:center;transition:opacity 0.8s,visibility 0.8s}
#splash.out{opacity:0;visibility:hidden;pointer-events:none}
.sp-ring{width:68px;height:68px;border:2px solid var(--b2);border-top-color:var(--cyan);border-right-color:var(--blue);border-radius:50%;animation:spin 1s linear infinite;margin-bottom:20px}
@keyframes spin{to{transform:rotate(360deg)}}
.sp-title{font-family:'Bebas Neue',sans-serif;font-size:26px;letter-spacing:4px;background:linear-gradient(135deg,#fff,var(--cyan));-webkit-background-clip:text;-webkit-text-fill-color:transparent;margin-bottom:4px}
.sp-sub{font-family:'Space Mono',monospace;font-size:10px;color:var(--muted);letter-spacing:2px;text-transform:uppercase;margin-bottom:20px}
.sp-bar{width:160px;height:1px;background:var(--b1);overflow:hidden}
.sp-fill{height:100%;width:0;background:linear-gradient(90deg,var(--blue),var(--cyan));animation:fillBar 2s ease forwards}
@keyframes fillBar{to{width:100%}}
@keyframes riseIn{from{opacity:0;transform:translateY(14px)}to{opacity:1;transform:translateY(0)}}

/* APP */
.app{position:relative;z-index:1;max-width:560px;margin:0 auto;padding:0 0 80px}

/* TOPBAR */
.topbar{display:flex;align-items:center;justify-content:space-between;padding:13px 16px;margin:14px 14px 0;background:var(--card);border:1px solid rgba(0,229,255,0.12);border-radius:16px;animation:riseIn 0.5s ease both;backdrop-filter:blur(20px)}
.brand{display:flex;align-items:center;gap:10px}
.brand-box{width:36px;height:36px;border-radius:10px;background:linear-gradient(135deg,var(--blue),var(--cyan));display:flex;align-items:center;justify-content:center;font-family:'Bebas Neue',sans-serif;font-size:13px;color:#03060f;box-shadow:0 0 12px rgba(74,144,255,0.3);flex-shrink:0}
.brand-name{font-family:'Bebas Neue',sans-serif;font-size:16px;letter-spacing:2px;background:linear-gradient(135deg,#fff,var(--cyan));-webkit-background-clip:text;-webkit-text-fill-color:transparent}
.brand-sub{font-family:'Space Mono',monospace;font-size:9px;color:var(--muted);margin-top:1px}
.topbar-badge{font-family:'Space Mono',monospace;font-size:9px;padding:4px 10px;border-radius:20px;border:1px solid rgba(0,229,255,0.2);color:var(--cyan);background:rgba(0,229,255,0.05);display:flex;align-items:center;gap:5px}
.topbar-badge.secure{border-color:rgba(0,255,179,0.2);color:var(--green);background:rgba(0,255,179,0.05)}
.live-dot{width:5px;height:5px;border-radius:50%;background:currentColor;box-shadow:0 0 5px currentColor;animation:blink 1.5s ease infinite}
@keyframes blink{0%,100%{opacity:1}50%{opacity:0.2}}

/* KPI */
.kpi-strip{display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;padding:10px 14px 0;animation:riseIn 0.5s 0.1s ease both}
.kc{background:var(--card);border:1px solid var(--b1);border-radius:12px;padding:12px;position:relative;overflow:hidden;backdrop-filter:blur(10px)}
.kc::before{content:'';position:absolute;top:0;left:0;right:0;height:2px}
.kc.t::before{background:linear-gradient(90deg,var(--blue),var(--cyan))}
.kc.p::before{background:linear-gradient(90deg,var(--amber),var(--red))}
.kc.r::before{background:linear-gradient(90deg,var(--green),var(--cyan))}
.kc-lbl{font-family:'Space Mono',monospace;font-size:8px;color:var(--muted);text-transform:uppercase;letter-spacing:0.5px;margin-bottom:4px}
.kc-val{font-family:'Bebas Neue',sans-serif;font-size:22px;letter-spacing:1px}
.kc.t .kc-val{color:var(--blue)}
.kc.p .kc-val{color:var(--amber)}
.kc.r .kc-val{color:var(--green)}
.kc-sub{font-family:'Space Mono',monospace;font-size:8px;color:var(--dim);margin-top:2px}

/* SEC */
.sec{padding:12px 14px 0;animation:riseIn 0.5s ease both}
.sec-hd{display:flex;align-items:center;justify-content:space-between;margin-bottom:10px}
.sec-title{font-family:'Space Mono',monospace;font-size:9px;color:var(--muted);text-transform:uppercase;letter-spacing:1.5px}
.sec-line{flex:1;height:1px;background:linear-gradient(90deg,var(--b1),transparent);margin-left:8px}

/* FINANCIERO */
.fin-card{background:linear-gradient(135deg,rgba(74,144,255,0.05),rgba(0,229,255,0.02));border:1px solid rgba(74,144,255,0.12);border-radius:13px;padding:14px}
.fin-row{display:flex;justify-content:space-between;align-items:center;font-size:13px;margin-bottom:7px}
.fin-row:last-child{margin-bottom:0;padding-top:8px;border-top:1px solid var(--b1)}
.fin-lbl{color:var(--muted)}
.fin-val{font-family:'Space Mono',monospace;font-weight:700}
.fin-val.amber{color:var(--amber)}
.fin-val.green{color:var(--green)}
.fin-val.blue{color:var(--blue)}

/* ALERTAS */
.alerta{display:none;background:rgba(255,45,85,0.06);border:1px solid rgba(255,45,85,0.2);border-radius:12px;padding:12px 14px;margin:10px 14px 0;animation:riseIn 0.4s ease both}
.alerta.show{display:flex;align-items:center;gap:10px}
.alerta-txt{font-family:'Space Mono',monospace;font-size:10px;color:var(--red);line-height:1.5}
.alerta-txt strong{color:var(--amber)}

/* FILTROS */
.filtros{display:flex;gap:6px;overflow-x:auto;-ms-overflow-style:none;scrollbar-width:none;margin-bottom:10px}
.filtros::-webkit-scrollbar{display:none}
.ftag{font-family:'Space Mono',monospace;font-size:9px;padding:5px 11px;border-radius:20px;border:1px solid var(--b2);background:transparent;color:var(--muted);cursor:pointer;white-space:nowrap;transition:all 0.2s;flex-shrink:0}
.ftag.active{background:var(--blue);border-color:var(--blue);color:#fff}
.ftag:hover:not(.active){border-color:var(--cyan);color:var(--cyan)}

/* BTN NUEVO */
.btn-new{display:flex;align-items:center;gap:5px;background:linear-gradient(135deg,var(--blue),var(--cyan));color:#03060f;font-family:'Bebas Neue',sans-serif;font-size:13px;letter-spacing:1px;padding:7px 13px;border-radius:8px;border:none;cursor:pointer;box-shadow:0 3px 12px rgba(74,144,255,0.3);transition:all 0.2s;flex-shrink:0}
.btn-new:hover{box-shadow:0 5px 18px rgba(74,144,255,0.5);transform:translateY(-1px)}
.btn-new:active{transform:scale(0.97)}

/* PEDIDO CARD */
#lista-pedidos{display:flex;flex-direction:column;gap:8px}
.pedido-card{background:var(--card);border:1px solid var(--b1);border-radius:14px;overflow:hidden;transition:border-color 0.2s;position:relative;backdrop-filter:blur(10px)}
.pedido-card:hover{border-color:var(--b2)}
.pedido-card::before{content:'';position:absolute;left:0;top:0;bottom:0;width:3px;border-radius:3px 0 0 3px}
.pedido-card.pendiente::before{background:var(--amber)}
.pedido-card.en-proceso::before{background:var(--blue)}
.pedido-card.en-transito::before{background:var(--purple)}
.pedido-card.recibido::before{background:var(--green)}
.pedido-card.cancelado::before{background:var(--red)}

.pedido-header{display:flex;align-items:center;gap:10px;padding:13px 14px 10px 17px;cursor:pointer;user-select:none}
.pedido-ico{width:38px;height:38px;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:17px;flex-shrink:0}
.pedido-info{flex:1;min-width:0}
.pedido-prov{font-size:14px;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.pedido-prod{font-family:'Space Mono',monospace;font-size:10px;color:var(--muted);margin-top:2px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.pedido-right{text-align:right;flex-shrink:0}
.pedido-monto{font-family:'Space Mono',monospace;font-size:14px;font-weight:700}
.pedido-fecha{font-family:'Space Mono',monospace;font-size:9px;color:var(--muted);margin-top:2px}
.st-tag{display:inline-flex;align-items:center;gap:3px;font-family:'Space Mono',monospace;font-size:9px;font-weight:700;padding:2px 7px;border-radius:4px;margin-top:4px}
.st-pendiente{background:rgba(255,204,0,0.1);color:var(--amber);border:1px solid rgba(255,204,0,0.2)}
.st-en-proceso{background:rgba(74,144,255,0.1);color:var(--blue);border:1px solid rgba(74,144,255,0.2)}
.st-en-transito{background:rgba(168,85,247,0.1);color:var(--purple);border:1px solid rgba(168,85,247,0.2)}
.st-recibido{background:rgba(0,255,179,0.1);color:var(--green);border:1px solid rgba(0,255,179,0.2)}
.st-cancelado{background:rgba(255,45,85,0.1);color:var(--red);border:1px solid rgba(255,45,85,0.2)}

.pedido-detalle{display:none;border-top:1px solid var(--b1);padding:12px 14px 14px 17px}
.pedido-detalle.open{display:block}
.det-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:10px}
.dg-lbl{font-family:'Space Mono',monospace;font-size:9px;color:var(--muted);text-transform:uppercase;letter-spacing:0.3px;margin-bottom:3px}
.dg-val{font-size:13px;font-weight:500}
.dg-val.money{font-family:'Space Mono',monospace;color:var(--amber)}
.dg-val.green{color:var(--green)}
.dg-val.red{color:var(--red)}
.dg-val.muted{color:var(--muted)}

.notas-box{background:rgba(255,255,255,0.02);border:1px solid var(--b1);border-radius:8px;padding:10px;font-size:12px;color:var(--muted);line-height:1.5;margin-bottom:10px;font-style:italic}

.pago-prog{margin-bottom:10px}
.pago-prog-hd{display:flex;justify-content:space-between;font-family:'Space Mono',monospace;font-size:9px;color:var(--muted);margin-bottom:4px}
.pago-bar{background:rgba(255,255,255,0.05);border-radius:4px;height:5px;overflow:hidden}
.pago-fill{height:100%;border-radius:4px;background:linear-gradient(90deg,var(--blue),var(--cyan));transition:width 0.8s ease}

/* ACCIONES */
.det-actions{display:flex;gap:6px;flex-wrap:wrap;margin-top:2px}
.btn-est{font-family:'Space Mono',monospace;font-size:10px;padding:6px 11px;border-radius:7px;border:1px solid var(--b2);background:var(--s2);color:var(--muted);cursor:pointer;transition:all 0.15s}
.btn-est:hover{border-color:var(--cyan);color:var(--txt)}
.btn-editar{font-family:'Space Mono',monospace;font-size:10px;padding:6px 11px;border-radius:7px;border:1px solid rgba(74,144,255,0.2);background:rgba(74,144,255,0.05);color:var(--blue);cursor:pointer;transition:all 0.15s}
.btn-editar:hover{border-color:var(--blue);background:rgba(74,144,255,0.1)}
.btn-del{font-family:'Space Mono',monospace;font-size:10px;padding:6px 11px;border-radius:7px;border:1px solid rgba(255,45,85,0.2);background:rgba(255,45,85,0.04);color:var(--red);cursor:pointer;transition:all 0.15s;margin-left:auto}
.btn-del:hover{border-color:var(--red);background:rgba(255,45,85,0.1)}

/* BTN WA */
.btn-wa-pedido{display:flex;align-items:center;justify-content:center;gap:7px;width:100%;padding:11px;border-radius:10px;background:linear-gradient(135deg,var(--wa),var(--wa2));color:#fff;font-family:'Bebas Neue',sans-serif;font-size:14px;letter-spacing:1px;border:none;cursor:pointer;box-shadow:0 3px 14px rgba(37,211,102,0.25);transition:all 0.2s;margin-bottom:8px}
.btn-wa-pedido:hover{box-shadow:0 5px 20px rgba(37,211,102,0.45);transform:translateY(-1px)}
.btn-wa-pedido:active{transform:scale(0.98)}
.btn-wa-pedido a{color:#fff;text-decoration:none;display:flex;align-items:center;gap:7px;width:100%;justify-content:center}

/* EMPTY */
.empty-state{text-align:center;padding:40px 20px;color:var(--muted)}
.empty-ico{font-size:38px;margin-bottom:12px;opacity:0.5}
.empty-txt{font-family:'Space Mono',monospace;font-size:11px;line-height:1.6}

/* MODAL */
.modal-bg{position:fixed;inset:0;background:rgba(3,6,15,0.92);backdrop-filter:blur(16px);z-index:800;display:flex;align-items:flex-end;justify-content:center;opacity:0;pointer-events:none;transition:opacity 0.25s}
.modal-bg.open{opacity:1;pointer-events:all}
.modal-sheet{background:var(--s2);border:1px solid var(--b2);border-radius:20px 20px 0 0;width:100%;max-width:560px;padding:20px;transform:translateY(100%);transition:transform 0.3s cubic-bezier(0.4,0,0.2,1);max-height:92vh;overflow-y:auto}
.modal-bg.open .modal-sheet{transform:translateY(0)}
.modal-handle{width:36px;height:3px;background:var(--b2);border-radius:3px;margin:0 auto 16px}
.modal-hd{display:flex;align-items:center;justify-content:space-between;margin-bottom:16px}
.modal-tit{font-family:'Bebas Neue',sans-serif;font-size:20px;letter-spacing:1px}
.modal-x{background:none;border:none;color:var(--muted);font-size:22px;cursor:pointer;line-height:1}

.fg{margin-bottom:11px}
.fg label{display:block;font-family:'Space Mono',monospace;font-size:9px;color:var(--muted);text-transform:uppercase;letter-spacing:0.5px;margin-bottom:5px}
.fg input,.fg select,.fg textarea{width:100%;background:rgba(16,32,63,0.8);border:1px solid var(--b2);border-radius:8px;padding:10px 12px;color:var(--txt);font-family:'Space Grotesk',sans-serif;font-size:14px;transition:border 0.2s;resize:none}
.fg input:focus,.fg select:focus,.fg textarea:focus{outline:none;border-color:var(--cyan);box-shadow:0 0 0 3px rgba(0,229,255,0.08)}
.fg select option{background:var(--s2)}
.fg2{display:grid;grid-template-columns:1fr 1fr;gap:10px}

.btn-save{width:100%;padding:14px;border-radius:12px;background:linear-gradient(135deg,var(--blue),var(--cyan));color:#03060f;font-family:'Bebas Neue',sans-serif;font-size:17px;letter-spacing:1.5px;border:none;cursor:pointer;font-weight:700;box-shadow:0 4px 18px rgba(74,144,255,0.3);transition:all 0.2s;margin-top:4px}
.btn-save:hover{box-shadow:0 6px 24px rgba(74,144,255,0.5);transform:translateY(-1px)}
.btn-save:active{transform:scale(0.98)}

/* PORTAL PROVEEDOR */
.prov-hero{margin:14px 14px 0;background:linear-gradient(135deg,#0d1f45,#091530);border:1px solid rgba(0,229,255,0.15);border-radius:18px;padding:20px;position:relative;overflow:hidden;animation:riseIn 0.5s ease both}
.prov-hero::before{content:'';position:absolute;top:0;left:0;right:0;height:1px;background:linear-gradient(90deg,transparent,var(--cyan),transparent)}
.prov-eyebrow{font-family:'Space Mono',monospace;font-size:9px;color:var(--muted);text-transform:uppercase;letter-spacing:1.5px;margin-bottom:8px}
.prov-nombre{font-family:'Bebas Neue',sans-serif;font-size:32px;letter-spacing:2px;background:linear-gradient(135deg,#fff,var(--cyan));-webkit-background-clip:text;-webkit-text-fill-color:transparent;margin-bottom:4px}
.prov-fecha{font-family:'Space Mono',monospace;font-size:10px;color:var(--muted)}

.pedido-vista{background:var(--card);border:1px solid var(--b1);border-radius:14px;overflow:hidden;backdrop-filter:blur(10px)}
.pv-section{padding:14px 16px;border-bottom:1px solid var(--b1)}
.pv-section:last-child{border-bottom:none}
.pv-label{font-family:'Space Mono',monospace;font-size:9px;color:var(--muted);text-transform:uppercase;letter-spacing:0.5px;margin-bottom:3px}
.pv-value{font-size:14px;font-weight:500}
.pv-value.big{font-family:'Bebas Neue',sans-serif;font-size:28px;letter-spacing:1px;color:var(--amber)}
.pv-value.green{color:var(--green)}
.pv-value.red{color:var(--red)}
.pv-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px;padding:14px 16px;border-bottom:1px solid var(--b1)}

.firma{margin:14px;background:rgba(74,144,255,0.03);border:1px solid rgba(74,144,255,0.1);border-radius:14px;padding:18px;text-align:center}
.firma-name{font-family:'Bebas Neue',sans-serif;font-size:18px;letter-spacing:3px;background:linear-gradient(135deg,#fff,var(--cyan));-webkit-background-clip:text;-webkit-text-fill-color:transparent;margin-bottom:3px}
.firma-sub{font-size:11px;color:var(--muted)}
.firma-seal{display:inline-flex;align-items:center;gap:5px;margin-top:10px;font-family:'Space Mono',monospace;font-size:9px;color:var(--blue);background:rgba(74,144,255,0.05);border:1px solid rgba(74,144,255,0.15);padding:5px 12px;border-radius:20px}
</style>
</head>
<body>
<canvas id="bg-canvas"></canvas>

<div id="splash">
  <div class="sp-ring"></div>
  <div class="sp-title">ECOKAIZEN</div>
  <div class="sp-sub">Gestión de Pedidos</div>
  <div class="sp-bar"><div class="sp-fill"></div></div>
</div>

<!-- MODAL NUEVO/EDITAR -->
<div class="modal-bg" id="modal" onclick="cerrarModal(event)">
  <div class="modal-sheet" onclick="event.stopPropagation()">
    <div class="modal-handle"></div>
    <div class="modal-hd">
      <div class="modal-tit" id="modal-tit">NUEVO PEDIDO</div>
      <button class="modal-x" onclick="cerrarModal()">×</button>
    </div>
    <div class="fg">
      <label>Proveedor *</label>
      <input type="text" id="f-prov" placeholder="Nombre del proveedor">
    </div>
    <div class="fg">
      <label>Teléfono WhatsApp</label>
      <input type="tel" id="f-tel" placeholder="51XXXXXXXXX (con código país)">
    </div>
    <div class="fg">
      <label>Producto / Descripción *</label>
      <input type="text" id="f-prod" placeholder="Ej: Vasos descartables 7oz">
    </div>
    <div class="fg2">
      <div class="fg">
        <label>Cantidad</label>
        <input type="number" id="f-cant" placeholder="0" min="0">
      </div>
      <div class="fg">
        <label>Unidad</label>
        <select id="f-uni">
          <option>Unid.</option><option>Docena</option><option>Ciento</option><option>Millar</option>
          <option>Kg</option><option>Fardo</option><option>Caja</option><option>Paquete</option>
        </select>
      </div>
    </div>
    <div class="fg2">
      <div class="fg">
        <label>Monto Total (S/)</label>
        <input type="number" id="f-monto" placeholder="0.00" min="0" step="0.01">
      </div>
      <div class="fg">
        <label>Ya Pagado (S/)</label>
        <input type="number" id="f-pagado" placeholder="0.00" min="0" step="0.01" value="0">
      </div>
    </div>
    <div class="fg2">
      <div class="fg">
        <label>Fecha Pedido</label>
        <input type="date" id="f-fped">
      </div>
      <div class="fg">
        <label>Entrega Esperada</label>
        <input type="date" id="f-fent">
      </div>
    </div>
    <div class="fg">
      <label>Estado</label>
      <select id="f-est">
        <option value="pendiente">⏳ Pendiente</option>
        <option value="en-proceso">⚙️ En Proceso</option>
        <option value="en-transito">🚚 En Tránsito</option>
        <option value="recibido">✅ Recibido</option>
        <option value="cancelado">❌ Cancelado</option>
      </select>
    </div>
    <div class="fg">
      <label>Notas / Condiciones</label>
      <textarea id="f-notas" rows="2" placeholder="Condiciones de pago, observaciones..."></textarea>
    </div>
    <button class="btn-save" onclick="guardar()">💾 GUARDAR PEDIDO</button>
  </div>
</div>

<!-- APP ADMIN -->
<div class="app" id="app-admin">

  <div class="topbar">
    <div class="brand">
      <div class="brand-box">EK</div>
      <div>
        <div class="brand-name">ECOKAIZEN</div>
        <div class="brand-sub">PEDIDOS · PROVEEDORES</div>
      </div>
    </div>
    <div class="topbar-badge"><div class="live-dot"></div>ADMIN</div>
  </div>

  <div class="alerta" id="alerta">
    <div style="font-size:20px">⚠️</div>
    <div class="alerta-txt" id="alerta-txt"></div>
  </div>

  <div class="kpi-strip">
    <div class="kc t"><div class="kc-lbl">Total</div><div class="kc-val" id="kpi-t">0</div><div class="kc-sub">pedidos</div></div>
    <div class="kc p"><div class="kc-lbl">Activos</div><div class="kc-val" id="kpi-p">0</div><div class="kc-sub">S/ <span id="kpi-ps">0</span></div></div>
    <div class="kc r"><div class="kc-lbl">Recibidos</div><div class="kc-val" id="kpi-r">0</div><div class="kc-sub">completados</div></div>
  </div>

  <div class="sec" style="animation-delay:0.15s">
    <div class="sec-hd">
      <div class="sec-title">Financiero<div class="sec-line"></div></div>
    </div>
    <div class="fin-card">
      <div class="fin-row"><span class="fin-lbl">Total en pedidos activos</span><span class="fin-val blue" id="fin-t">S/ 0.00</span></div>
      <div class="fin-row"><span class="fin-lbl">Ya pagado</span><span class="fin-val green" id="fin-p">S/ 0.00</span></div>
      <div class="fin-row"><span class="fin-lbl">Saldo por pagar</span><span class="fin-val amber" id="fin-s">S/ 0.00</span></div>
    </div>
  </div>

  <div class="sec" style="animation-delay:0.2s">
    <div class="sec-hd">
      <div class="sec-title">Pedidos<div class="sec-line"></div></div>
      <button class="btn-new" onclick="abrirNuevo()">+ Nuevo</button>
    </div>
    <div class="filtros">
      <button class="ftag active" onclick="filtrar('todos',this)">Todos</button>
      <button class="ftag" onclick="filtrar('pendiente',this)">⏳</button>
      <button class="ftag" onclick="filtrar('en-proceso',this)">⚙️</button>
      <button class="ftag" onclick="filtrar('en-transito',this)">🚚</button>
      <button class="ftag" onclick="filtrar('recibido',this)">✅</button>
    </div>
    <div id="lista-pedidos"></div>
  </div>

  <div class="firma">
    <div class="firma-name">ECOKAIZEN</div>
    <div class="firma-sub">Gestión de Pedidos · Proveedores Locales</div>
    <div class="firma-seal">🛡️ SISTEMA INTERNO</div>
  </div>
</div>

<!-- APP PROVEEDOR (modo cliente) -->
<div class="app" id="app-proveedor" style="display:none">
  <div class="topbar">
    <div class="brand">
      <div class="brand-box">EK</div>
      <div>
        <div class="brand-name">ECOKAIZEN</div>
        <div class="brand-sub">ORDEN DE COMPRA</div>
      </div>
    </div>
    <div class="topbar-badge secure"><div class="live-dot"></div>PROVEEDOR</div>
  </div>

  <div class="prov-hero">
    <div class="prov-eyebrow">Orden emitida por EcoKaizen</div>
    <div class="prov-nombre" id="pv-nombre">—</div>
    <div class="prov-fecha" id="pv-fecha">—</div>
  </div>

  <div class="sec" style="animation-delay:0.2s">
    <div class="sec-hd"><div class="sec-title">Detalle del Pedido<div class="sec-line"></div></div></div>
    <div class="pedido-vista">
      <div class="pv-section">
        <div class="pv-label">Producto / Descripción</div>
        <div class="pv-value" id="pv-prod">—</div>
      </div>
      <div class="pv-grid">
        <div>
          <div class="pv-label">Cantidad</div>
          <div class="pv-value" id="pv-cant">—</div>
        </div>
        <div>
          <div class="pv-label">Estado</div>
          <div class="pv-value" id="pv-est">—</div>
        </div>
        <div>
          <div class="pv-label">Fecha Pedido</div>
          <div class="pv-value" id="pv-fped">—</div>
        </div>
        <div>
          <div class="pv-label">Entrega Esperada</div>
          <div class="pv-value" id="pv-fent">—</div>
        </div>
      </div>
      <div class="pv-section">
        <div class="pv-label">Monto Total del Pedido</div>
        <div class="pv-value big" id="pv-monto">S/ 0.00</div>
      </div>
      <div class="pv-grid">
        <div>
          <div class="pv-label">Pagado</div>
          <div class="pv-value green" id="pv-pagado">S/ 0.00</div>
        </div>
        <div>
          <div class="pv-label">Saldo Pendiente</div>
          <div class="pv-value red" id="pv-saldo">S/ 0.00</div>
        </div>
      </div>
      <div class="pv-section" id="pv-notas-sec" style="display:none">
        <div class="pv-label">Notas / Condiciones</div>
        <div class="pv-value muted" id="pv-notas" style="color:var(--muted);font-size:13px;line-height:1.5"></div>
      </div>
    </div>
  </div>

  <div class="firma">
    <div class="firma-name">ECOKAIZEN</div>
    <div class="firma-sub">Tu Empaque Óptimo · Trujillo, Perú<br>Orden oficial emitida digitalmente</div>
    <div class="firma-seal">🛡️ ORDEN VERIFICADA · SOLO LECTURA</div>
  </div>
</div>

<script>
const SK   = 'ek_pedidos_v2';
const SALT = 'EK_PED_2026';
let pedidos = [];
let editando = null;
let filtroActivo = 'todos';

const fc  = n => 'S/ '+parseFloat(n||0).toLocaleString('es-PE',{minimumFractionDigits:2,maximumFractionDigits:2});
const uid = () => Date.now().toString(36)+Math.random().toString(36).slice(2,6);
const hoyISO = () => { const d=new Date(); return d.getFullYear()+'-'+String(d.getMonth()+1).padStart(2,'0')+'-'+String(d.getDate()).padStart(2,'0') };
const fmtF  = iso => { if(!iso) return '—'; const [y,m,d]=iso.split('-'); return d+'/'+m+'/'+y };
const isVenc = iso => iso && new Date(iso+'T23:59:59') < new Date();
const diasR  = iso => { if(!iso) return null; return Math.ceil((new Date(iso+'T23:59:59')-new Date())/(1000*60*60*24)) };

const EST = {
  'pendiente':   {label:'Pendiente',   ico:'⏳',cls:'st-pendiente',  cc:'pendiente',  bg:'rgba(255,204,0,0.1)'},
  'en-proceso':  {label:'En Proceso',  ico:'⚙️', cls:'st-en-proceso', cc:'en-proceso', bg:'rgba(74,144,255,0.1)'},
  'en-transito': {label:'En Tránsito', ico:'🚚',cls:'st-en-transito',cc:'en-transito',bg:'rgba(168,85,247,0.1)'},
  'recibido':    {label:'Recibido',    ico:'✅',cls:'st-recibido',   cc:'recibido',   bg:'rgba(0,255,179,0.1)'},
  'cancelado':   {label:'Cancelado',   ico:'❌',cls:'st-cancelado',  cc:'cancelado',  bg:'rgba(255,45,85,0.1)'},
};

// CRYPTO
const encrypt = obj => btoa(encodeURIComponent(JSON.stringify({...obj,s:SALT})));
const decrypt = tok => { try{ const d=JSON.parse(decodeURIComponent(atob(tok))); return d.s===SALT?d:null }catch(e){return null} };

// STORAGE
const save  = () => { try{ localStorage.setItem(SK,JSON.stringify(pedidos)) }catch(e){} };
const load  = () => { try{ const d=localStorage.getItem(SK); if(d) pedidos=JSON.parse(d) }catch(e){ pedidos=[] } };

// CANVAS
(function(){
  const c=document.getElementById('bg-canvas'),ctx=c.getContext('2d');let pts=[];
  const resize=()=>{c.width=window.innerWidth;c.height=window.innerHeight;pts=[];const n=Math.floor(c.width*c.height/22000);for(let i=0;i<n;i++)pts.push({x:Math.random()*c.width,y:Math.random()*c.height,vx:(Math.random()-.5)*.1,vy:(Math.random()-.5)*.1,r:Math.random()*1.2+.3,a:Math.random()*.25+.05})};
  const draw=()=>{ctx.clearRect(0,0,c.width,c.height);pts.forEach(p=>{ctx.beginPath();ctx.arc(p.x,p.y,p.r,0,Math.PI*2);ctx.fillStyle=`rgba(74,144,255,${p.a})`;ctx.fill();pts.forEach(q=>{const dx=p.x-q.x,dy=p.y-q.y,d=Math.sqrt(dx*dx+dy*dy);if(d<90){ctx.beginPath();ctx.moveTo(p.x,p.y);ctx.lineTo(q.x,q.y);ctx.strokeStyle=`rgba(74,144,255,${.025*(1-d/90)})`;ctx.lineWidth=.4;ctx.stroke()}});p.x+=p.vx;p.y+=p.vy;if(p.x<0||p.x>c.width)p.vx*=-1;if(p.y<0||p.y>c.height)p.vy*=-1});requestAnimationFrame(draw)};
  window.addEventListener('resize',resize);resize();draw();
})();

// WA LINK para proveedor
function buildWALink(p){
  const token = encrypt({
    id:p.id, prov:p.proveedor, tel:p.telefono,
    prod:p.producto, cant:p.cantidad, uni:p.unidad,
    monto:p.monto, pagado:p.pagado,
    fped:p.fechaPedido, fent:p.fechaEntrega,
    est:p.estado, notas:p.notas
  });
  const link = window.location.href.split('?')[0]+'?orden='+token;
  const est = EST[p.estado]||EST['pendiente'];
  const saldo = Math.max(0,(parseFloat(p.monto)||0)-(parseFloat(p.pagado)||0));
  const msg =
`Hola ${p.proveedor}, le enviamos la confirmación de su pedido desde EcoKaizen 🧾

📦 *Producto:* ${p.producto}
${p.cantidad?`📊 *Cantidad:* ${p.cantidad} ${p.unidad}\n`:''}💰 *Monto Total:* ${fc(p.monto)}
✅ *Pagado:* ${fc(p.pagado)}
${saldo>0?`⏳ *Saldo pendiente:* ${fc(saldo)}\n`:''}${est.ico} *Estado:* ${est.label}
${p.fechaEntrega?`📅 *Entrega esperada:* ${fmtF(p.fechaEntrega)}\n`:''}
🔗 Ver orden completa:
${link}

_EcoKaizen · Tu Empaque Óptimo_`;

  const tel = p.telefono ? p.telefono.replace(/\D/g,'') : '';
  return 'https://api.whatsapp.com/send?'+(tel?'phone='+tel+'&':'')+'text='+encodeURIComponent(msg);
}

// RENDER
function render(){
  const activos = pedidos.filter(p=>p.estado!=='cancelado'&&p.estado!=='recibido');
  const recibidos = pedidos.filter(p=>p.estado==='recibido');
  const pendientes = pedidos.filter(p=>['pendiente','en-proceso','en-transito'].includes(p.estado));

  document.getElementById('kpi-t').innerText = pedidos.length;
  document.getElementById('kpi-p').innerText = pendientes.length;
  const mp = pendientes.reduce((a,p)=>a+(parseFloat(p.monto)||0)-(parseFloat(p.pagado)||0),0);
  document.getElementById('kpi-ps').innerText = mp.toLocaleString('es-PE',{minimumFractionDigits:0});
  document.getElementById('kpi-r').innerText = recibidos.length;

  const tM=activos.reduce((a,p)=>a+(parseFloat(p.monto)||0),0);
  const tP=activos.reduce((a,p)=>a+(parseFloat(p.pagado)||0),0);
  document.getElementById('fin-t').innerText=fc(tM);
  document.getElementById('fin-p').innerText=fc(tP);
  document.getElementById('fin-s').innerText=fc(Math.max(0,tM-tP));

  const venc=pedidos.filter(p=>!['recibido','cancelado'].includes(p.estado)&&isVenc(p.fechaEntrega));
  const al=document.getElementById('alerta');
  if(venc.length>0){
    al.classList.add('show');
    document.getElementById('alerta-txt').innerHTML=`<strong>${venc.length} pedido(s)</strong> con entrega vencida — revisar con proveedor`;
  }else al.classList.remove('show');

  const filtrados = filtroActivo==='todos' ? pedidos : pedidos.filter(p=>p.estado===filtroActivo);
  const lista = document.getElementById('lista-pedidos');

  if(filtrados.length===0){
    lista.innerHTML=`<div class="empty-state"><div class="empty-ico">📦</div><div class="empty-txt">${filtroActivo==='todos'?'Sin pedidos. Toca "+ Nuevo" para agregar.':'Sin pedidos en este estado.'}</div></div>`;
    return;
  }

  lista.innerHTML = filtrados.map(p=>{
    const est=EST[p.estado]||EST['pendiente'];
    const monto=parseFloat(p.monto)||0;
    const pagado=parseFloat(p.pagado)||0;
    const saldo=Math.max(0,monto-pagado);
    const pct=monto>0?Math.min(100,Math.round(pagado/monto*100)):0;
    const dr=diasR(p.fechaEntrega);
    const venc=isVenc(p.fechaEntrega)&&!['recibido','cancelado'].includes(p.estado);

    return `<div class="pedido-card ${est.cc}" id="card-${p.id}">
      <div class="pedido-header" onclick="toggle('${p.id}')">
        <div class="pedido-ico" style="background:${est.bg}">${est.ico}</div>
        <div class="pedido-info">
          <div class="pedido-prov">${p.proveedor}</div>
          <div class="pedido-prod">${p.cantidad?p.cantidad+' '+p.unidad+' · ':''}${p.producto}</div>
          <div class="st-tag ${est.cls}">${est.ico} ${est.label}${venc?' · ⚠ VENCIDO':''}</div>
        </div>
        <div class="pedido-right">
          <div class="pedido-monto">${fc(monto)}</div>
          <div class="pedido-fecha">${fmtF(p.fechaPedido)}</div>
          ${saldo>0?`<div style="font-family:'Space Mono',monospace;font-size:9px;color:var(--amber);margin-top:2px">debe ${fc(saldo)}</div>`:''}
        </div>
      </div>
      <div class="pedido-detalle" id="det-${p.id}">
        <div class="det-grid">
          <div><div class="dg-lbl">Monto</div><div class="dg-val money">${fc(monto)}</div></div>
          <div><div class="dg-lbl">Pagado</div><div class="dg-val green">${fc(pagado)}</div></div>
          <div><div class="dg-lbl">Saldo</div><div class="dg-val ${saldo>0?'red':'green'}">${fc(saldo)}</div></div>
          <div><div class="dg-lbl">Entrega</div><div class="dg-val" style="${venc?'color:var(--red)':dr!==null&&dr<=3?'color:var(--amber)':''}">${p.fechaEntrega?fmtF(p.fechaEntrega)+(dr!==null?venc?' ⚠':' ('+dr+'d)':''):'—'}</div></div>
        </div>
        ${monto>0?`<div class="pago-prog"><div class="pago-prog-hd"><span>Pago completado</span><span>${pct}%</span></div><div class="pago-bar"><div class="pago-fill" style="width:${pct}%"></div></div></div>`:''}
        ${p.notas?`<div class="notas-box">📝 ${p.notas}</div>`:''}
        <!-- BTN WA -->
        <div class="btn-wa-pedido" style="margin-bottom:8px">
          <a href="${buildWALink(p)}" target="_blank">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="white"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
            ENVIAR ORDEN AL PROVEEDOR
          </a>
        </div>
        <div class="det-actions">
          <button class="btn-est" onclick="cambiarEst('${p.id}','pendiente')" title="Pendiente">⏳</button>
          <button class="btn-est" onclick="cambiarEst('${p.id}','en-proceso')" title="En Proceso">⚙️</button>
          <button class="btn-est" onclick="cambiarEst('${p.id}','en-transito')" title="En Tránsito">🚚</button>
          <button class="btn-est" onclick="cambiarEst('${p.id}','recibido')" title="Recibido">✅</button>
          <button class="btn-editar" onclick="editar('${p.id}')">✏️ Editar</button>
          <button class="btn-del" onclick="eliminar('${p.id}')">🗑</button>
        </div>
      </div>
    </div>`;
  }).join('');
}

function toggle(id){ document.getElementById('det-'+id)?.classList.toggle('open') }
function cambiarEst(id,est){ const p=pedidos.find(x=>x.id===id); if(p){p.estado=est;save();render()} }
function eliminar(id){ if(!confirm('¿Eliminar pedido?')) return; pedidos=pedidos.filter(x=>x.id!==id); save();render() }
function filtrar(f,btn){ filtroActivo=f; document.querySelectorAll('.ftag').forEach(b=>b.classList.remove('active')); btn.classList.add('active'); render() }

function abrirNuevo(){
  editando=null;
  document.getElementById('modal-tit').innerText='NUEVO PEDIDO';
  ['f-prov','f-tel','f-prod','f-cant','f-monto','f-notas'].forEach(id=>document.getElementById(id).value='');
  document.getElementById('f-pagado').value='0';
  document.getElementById('f-uni').value='Unid.';
  document.getElementById('f-est').value='pendiente';
  document.getElementById('f-fped').value=hoyISO();
  document.getElementById('f-fent').value='';
  document.getElementById('modal').classList.add('open');
  setTimeout(()=>document.getElementById('f-prov').focus(),300);
}

function editar(id){
  const p=pedidos.find(x=>x.id===id); if(!p) return;
  editando=id;
  document.getElementById('modal-tit').innerText='EDITAR PEDIDO';
  document.getElementById('f-prov').value=p.proveedor||'';
  document.getElementById('f-tel').value=p.telefono||'';
  document.getElementById('f-prod').value=p.producto||'';
  document.getElementById('f-cant').value=p.cantidad||'';
  document.getElementById('f-uni').value=p.unidad||'Unid.';
  document.getElementById('f-monto').value=p.monto||'';
  document.getElementById('f-pagado').value=p.pagado||'0';
  document.getElementById('f-est').value=p.estado||'pendiente';
  document.getElementById('f-notas').value=p.notas||'';
  document.getElementById('f-fped').value=p.fechaPedido||hoyISO();
  document.getElementById('f-fent').value=p.fechaEntrega||'';
  document.getElementById('modal').classList.add('open');
}

function cerrarModal(e){
  if(e&&e.target!==document.getElementById('modal')) return;
  document.getElementById('modal').classList.remove('open');
}

function guardar(){
  const prov=document.getElementById('f-prov').value.trim();
  const prod=document.getElementById('f-prod').value.trim();
  if(!prov||!prod){ alert('Proveedor y producto son obligatorios'); return; }
  const datos={
    proveedor:prov, telefono:document.getElementById('f-tel').value.trim(),
    producto:prod, cantidad:document.getElementById('f-cant').value,
    unidad:document.getElementById('f-uni').value,
    monto:document.getElementById('f-monto').value,
    pagado:document.getElementById('f-pagado').value||'0',
    estado:document.getElementById('f-est').value,
    notas:document.getElementById('f-notas').value.trim(),
    fechaPedido:document.getElementById('f-fped').value,
    fechaEntrega:document.getElementById('f-fent').value,
  };
  if(editando){ const i=pedidos.findIndex(x=>x.id===editando); if(i>=0) pedidos[i]={...pedidos[i],...datos} }
  else pedidos.unshift({id:uid(),...datos});
  save(); render();
  document.getElementById('modal').classList.remove('open');
}

// MODO PROVEEDOR
function mostrarPortalProveedor(data){
  document.getElementById('app-admin').style.display='none';
  document.getElementById('app-proveedor').style.display='block';

  const est=EST[data.est]||EST['pendiente'];
  const monto=parseFloat(data.monto)||0;
  const pagado=parseFloat(data.pagado)||0;
  const saldo=Math.max(0,monto-pagado);

  document.getElementById('pv-nombre').innerText=data.prov||'—';
  document.getElementById('pv-fecha').innerText='Pedido: '+fmtF(data.fped)+(data.fent?' · Entrega: '+fmtF(data.fent):'');
  document.getElementById('pv-prod').innerText=data.prod||'—';
  document.getElementById('pv-cant').innerText=data.cant?(data.cant+' '+data.uni):'—';
  document.getElementById('pv-est').innerHTML=`<span class="st-tag ${est.cls}">${est.ico} ${est.label}</span>`;
  document.getElementById('pv-fped').innerText=fmtF(data.fped);
  document.getElementById('pv-fent').innerText=data.fent?fmtF(data.fent)+(isVenc(data.fent)?' ⚠':''):'—';
  document.getElementById('pv-monto').innerText=fc(monto);
  document.getElementById('pv-pagado').innerText=fc(pagado);
  document.getElementById('pv-saldo').innerText=fc(saldo);
  if(data.notas){
    document.getElementById('pv-notas-sec').style.display='block';
    document.getElementById('pv-notas').innerText=data.notas;
  }
}

// INIT
window.onload=()=>{
  load();
  const params=new URLSearchParams(window.location.search);
  if(params.has('orden')){
    const data=decrypt(params.get('orden'));
    if(data) mostrarPortalProveedor(data);
    else{
      document.getElementById('app-admin').style.display='none';
      document.getElementById('app-proveedor').innerHTML='<div style="padding:40px 20px;text-align:center;color:var(--red);font-family:Bebas Neue,sans-serif;font-size:24px;letter-spacing:2px">🔐 ORDEN INVÁLIDA</div>';
      document.getElementById('app-proveedor').style.display='block';
    }
  } else {
    render();
  }
  setTimeout(()=>document.getElementById('splash').classList.add('out'),2000);
};
</script>
</body>
</html>
