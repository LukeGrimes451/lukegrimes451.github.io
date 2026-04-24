<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>BasketCheck — Ireland's grocery price comparison</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;1,9..40,300&display=swap" rel="stylesheet">
<style>
:root{
  --teal-50:#E1F5EE;--teal-100:#9FE1CB;--teal-400:#1D9E75;--teal-600:#0F6E56;--teal-800:#085041;
  --blue-50:#E6F1FB;--blue-400:#378ADD;--blue-800:#0C447C;
  --amber-50:#FAEEDA;--amber-400:#BA7517;--amber-800:#633806;
  --purple-50:#EEEDFE;--purple-400:#7F77DD;--purple-800:#3C3489;
  --green-50:#EAF3DE;--green-400:#639922;--green-800:#27500A;
  --coral-50:#FAECE7;--coral-400:#D85A30;--coral-800:#712B13;
  --red-400:#E24B4A;--red-800:#791F1F;
  --gray-50:#F1EFE8;--gray-200:#B4B2A9;--gray-400:#888780;--gray-800:#444441;
  --bg:#F7F6F2;--surface:#FFFFFF;
  --border:rgba(0,0,0,0.1);
  --text:#1a1a18;--text-2:#5a5a56;--text-3:#8a8a84;
  --radius:14px;--radius-sm:8px;
}
*{box-sizing:border-box;margin:0;padding:0;}
body{font-family:'DM Sans',sans-serif;background:var(--bg);color:var(--text);min-height:100vh;display:flex;align-items:flex-start;justify-content:center;padding:24px 16px 48px;}
.app-shell{width:100%;max-width:420px;background:var(--surface);border-radius:24px;border:1px solid var(--border);overflow:hidden;min-height:700px;display:flex;flex-direction:column;position:relative;}
.screen{display:none;flex-direction:column;flex:1;}
.screen.active{display:flex;}
.status-bar{padding:10px 16px 6px;display:flex;align-items:center;justify-content:space-between;}
.status-time{font-size:13px;font-weight:500;}
.status-icons{display:flex;gap:5px;align-items:center;}
.status-dot{width:6px;height:6px;border-radius:50%;background:var(--teal-400);}
.notif-bar{background:var(--teal-400);padding:8px 14px;display:flex;align-items:center;gap:8px;cursor:pointer;}
.notif-dot{width:7px;height:7px;border-radius:50%;background:white;flex-shrink:0;}
.notif-text{font-size:12px;color:white;line-height:1.3;}
.notif-arrow{margin-left:auto;font-size:12px;color:rgba(255,255,255,0.7);}
.screen-hdr{padding:14px 16px 10px;border-bottom:1px solid var(--border);display:flex;align-items:center;gap:10px;}
.back-btn{width:30px;height:30px;border-radius:50%;background:var(--gray-50);border:none;cursor:pointer;display:flex;align-items:center;justify-content:center;flex-shrink:0;}
.hdr-title{font-size:16px;font-weight:500;}
.hdr-sub{font-size:11px;color:var(--text-3);margin-top:1px;}
.screen-body{padding:14px 16px;flex:1;display:flex;flex-direction:column;gap:10px;overflow-y:auto;}
.input-field{width:100%;padding:9px 12px;background:var(--gray-50);border:1px solid var(--border);border-radius:var(--radius-sm);font-size:13px;color:var(--text);font-family:'DM Sans',sans-serif;outline:none;}
.input-field:focus{border-color:var(--teal-400);}
.input-field::placeholder{color:var(--text-3);}
.btn-primary{width:100%;padding:11px;background:var(--teal-400);color:white;border:none;border-radius:var(--radius-sm);font-size:13px;font-weight:500;font-family:'DM Sans',sans-serif;cursor:pointer;transition:opacity .15s;}
.btn-primary:hover{opacity:.9;}
.btn-secondary{width:100%;padding:10px;background:var(--gray-50);color:var(--text-2);border:1px solid var(--border);border-radius:var(--radius-sm);font-size:13px;font-family:'DM Sans',sans-serif;cursor:pointer;transition:background .15s;}
.btn-secondary:hover{background:#ECEAE4;}
.screen-footer{padding:10px 16px 16px;border-top:1px solid var(--border);display:flex;flex-direction:column;gap:7px;}
.tab-bar{display:flex;border-top:1px solid var(--border);background:var(--surface);flex-shrink:0;}
.tab{flex:1;padding:8px 0 10px;display:flex;flex-direction:column;align-items:center;gap:3px;cursor:pointer;border:none;background:none;font-family:'DM Sans',sans-serif;}
.tab-lbl{font-size:9px;color:var(--text-3);}
.tab-lbl.on{color:var(--teal-400);}
.tab svg{width:18px;height:18px;}
.section-lbl{font-size:10px;text-transform:uppercase;letter-spacing:.06em;color:var(--text-3);margin-bottom:7px;}
.app-topbar{padding:12px 16px 10px;display:flex;align-items:center;justify-content:space-between;border-bottom:1px solid var(--border);}
.topbar-logo{font-family:'DM Serif Display',serif;font-size:20px;letter-spacing:-.3px;}
.topbar-logo span{color:var(--teal-400);}
.topbar-badge{background:var(--teal-50);color:var(--teal-800);font-size:10px;font-weight:500;padding:3px 8px;border-radius:10px;}
 
/* Onboarding */
.onboard-logo{text-align:center;padding:24px 16px 8px;}
.logo-mark{width:52px;height:52px;background:var(--teal-400);border-radius:14px;display:inline-flex;align-items:center;justify-content:center;margin-bottom:8px;}
.logo-name{font-family:'DM Serif Display',serif;font-size:28px;letter-spacing:-.5px;}
.logo-name span{color:var(--teal-400);}
.logo-tagline{font-size:12px;color:var(--text-3);margin-top:2px;letter-spacing:.05em;text-transform:uppercase;}
.how-steps{display:flex;flex-direction:column;}
.how-step{display:flex;align-items:flex-start;gap:12px;padding:8px 0;border-bottom:1px solid var(--border);}
.how-step:last-child{border-bottom:none;}
.step-num{width:26px;height:26px;border-radius:50%;background:var(--teal-50);color:var(--teal-800);font-size:12px;font-weight:500;display:flex;align-items:center;justify-content:center;flex-shrink:0;}
.step-num.active{background:var(--teal-400);color:white;}
.step-text-title{font-size:13px;font-weight:500;}
.step-text-sub{font-size:11px;color:var(--text-3);margin-top:1px;}
.location-section{background:var(--gray-50);border-radius:var(--radius-sm);padding:12px;border:1px solid var(--border);}
.radius-row{display:flex;align-items:center;gap:10px;margin-top:8px;}
.radius-lbl{font-size:12px;color:var(--text-2);white-space:nowrap;}
.radius-val{font-size:12px;font-weight:500;min-width:30px;text-align:right;}
input[type=range]{flex:1;accent-color:var(--teal-400);}
.store-btn-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:6px;}
.store-pick-btn{padding:8px 4px;border:1.5px solid var(--border);border-radius:var(--radius-sm);background:var(--surface);font-size:11px;font-weight:500;color:var(--text-2);cursor:pointer;text-align:center;transition:all .15s;font-family:'DM Sans',sans-serif;}
.store-pick-btn.selected{border-color:var(--teal-400);background:var(--teal-50);color:var(--teal-800);}
.store-pick-btn:hover:not(.selected){background:var(--gray-50);}
 
/* Basket */
.basket-item{display:flex;align-items:center;justify-content:space-between;padding:9px 0;border-bottom:1px solid var(--border);}
.basket-item:last-child{border-bottom:none;}
.item-left{display:flex;align-items:center;gap:9px;}
.item-cat-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0;}
.item-name{font-size:13px;}
.item-right{display:flex;align-items:center;gap:8px;}
.qty-ctrl{display:flex;align-items:center;gap:5px;}
.qty-btn{width:22px;height:22px;border-radius:50%;border:1px solid var(--border);background:var(--surface);font-size:14px;color:var(--text-2);cursor:pointer;display:flex;align-items:center;justify-content:center;font-family:'DM Sans',sans-serif;line-height:1;}
.qty-btn:hover{background:var(--gray-50);}
.qty-num{font-size:12px;font-weight:500;min-width:14px;text-align:center;}
.item-remove{background:none;border:none;color:var(--text-3);cursor:pointer;font-size:16px;padding:0 2px;}
.basket-total-row{display:flex;justify-content:space-between;align-items:center;padding:10px 0;margin-top:4px;border-top:1px solid var(--border);}
.basket-total-lbl{font-size:12px;color:var(--text-3);}
.basket-total-num{font-size:15px;font-weight:500;}
 
/* ── SEARCH DROP-DOWN (Problem 1 + Feature 1) ── */
.search-dropdown{display:none;background:white;border:1px solid var(--border);border-radius:var(--radius-sm);margin-top:2px;overflow:hidden;position:absolute;width:100%;z-index:10;box-shadow:0 4px 14px rgba(0,0,0,0.10);max-height:320px;overflow-y:auto;}
.search-dropdown.open{display:block;}
 
/* Recent searches section */
.drop-section-hdr{display:flex;align-items:center;justify-content:space-between;padding:7px 12px 5px;background:var(--gray-50);border-bottom:1px solid var(--border);}
.drop-section-lbl{font-size:9px;text-transform:uppercase;letter-spacing:.07em;color:var(--text-3);font-weight:500;}
.drop-clear-btn{font-size:10px;color:var(--teal-600);background:none;border:none;cursor:pointer;font-family:'DM Sans',sans-serif;padding:0;}
 
/* Recent item row */
.recent-item{display:flex;align-items:center;gap:9px;padding:9px 12px;border-bottom:1px solid var(--border);cursor:pointer;font-size:13px;color:var(--text-2);}
.recent-item:last-child{border-bottom:none;}
.recent-item:hover{background:var(--gray-50);}
.recent-clock{width:14px;height:14px;flex-shrink:0;opacity:.45;}
.recent-name{flex:1;}
.recent-remove{background:none;border:none;font-size:14px;color:var(--text-3);cursor:pointer;padding:0 2px;line-height:1;}
 
/* Category group header */
.cat-group-hdr{padding:6px 12px 3px;background:var(--gray-50);border-bottom:1px solid var(--border);display:flex;align-items:center;gap:6px;}
.cat-group-dot{width:7px;height:7px;border-radius:50%;flex-shrink:0;}
.cat-group-name{font-size:9px;text-transform:uppercase;letter-spacing:.07em;color:var(--text-3);font-weight:500;flex:1;}
.cat-group-count{font-size:9px;color:var(--text-3);}
 
/* Suggestion item inside group */
.suggestion-item{padding:8px 12px 8px 28px;font-size:13px;border-bottom:1px solid var(--border);cursor:pointer;display:flex;align-items:center;gap:8px;}
.suggestion-item:last-child{border-bottom:none;}
.suggestion-item:hover{background:var(--gray-50);}
.suggest-match{font-weight:500;color:var(--teal-800);}
 
/* Empty state */
.search-empty{padding:20px 12px;text-align:center;}
.search-empty-icon{font-size:22px;margin-bottom:6px;}
.search-empty-title{font-size:13px;font-weight:500;color:var(--text);margin-bottom:3px;}
.search-empty-sub{font-size:11px;color:var(--text-3);}
 
/* Ranking */
.baseline-banner{background:var(--gray-50);border:1px solid var(--border);border-radius:var(--radius-sm);padding:7px 10px;display:flex;align-items:center;gap:6px;}
.baseline-text{font-size:11px;color:var(--text-2);}
.baseline-store{font-weight:500;color:var(--text);}
.store-rank-row{display:flex;align-items:center;gap:10px;padding:10px 4px;border-bottom:1px solid var(--border);cursor:pointer;border-radius:4px;margin:0 -4px;}
.store-rank-row:last-child{border-bottom:none;}
.store-rank-row:hover{background:var(--gray-50);}
.rank-num{font-size:11px;font-weight:500;color:var(--text-3);width:16px;flex-shrink:0;text-align:center;}
.store-abbr{width:32px;height:32px;border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:9px;font-weight:500;flex-shrink:0;}
.abbr-lidl{background:var(--blue-50);color:var(--blue-800);}
.abbr-aldi{background:var(--green-50);color:var(--green-800);}
.abbr-dunnes{background:var(--coral-50);color:var(--coral-800);}
.abbr-sv{background:var(--amber-50);color:var(--amber-800);}
.abbr-tesco{background:var(--purple-50);color:var(--purple-800);}
.store-info{flex:1;min-width:0;}
.store-nm{font-size:13px;font-weight:500;}
.store-dist{font-size:11px;color:var(--text-3);}
.store-price-col{text-align:right;flex-shrink:0;}
.store-total{font-size:14px;font-weight:500;}
.store-delta{font-size:11px;}
.delta-saving{color:var(--teal-600);}
.delta-usual{color:var(--text-3);font-style:italic;}
.delta-more{color:var(--red-400);}
.store-chevron{color:var(--text-3);font-size:14px;flex-shrink:0;}
.saving-hero{background:var(--teal-50);border-radius:var(--radius-sm);padding:12px;text-align:center;}
.saving-big{font-family:'DM Serif Display',serif;font-size:28px;color:var(--teal-800);line-height:1;}
.saving-sub{font-size:11px;color:var(--teal-600);margin-top:3px;}
 
/* Breakdown */
.col-hdr-row{display:flex;justify-content:space-between;padding:4px 0 6px;border-bottom:1px solid var(--border);}
.col-h{font-size:10px;text-transform:uppercase;letter-spacing:.06em;color:var(--text-3);}
.breakdown-row{display:flex;justify-content:space-between;align-items:center;padding:8px 0;border-bottom:1px solid var(--border);}
.breakdown-row:last-child{border-bottom:none;}
.br-item{font-size:12px;flex:1;min-width:0;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;margin-right:10px;}
.br-prices{display:flex;gap:14px;flex-shrink:0;align-items:center;}
.br-cheap{font-size:12px;font-weight:500;color:var(--teal-800);}
.br-dear{font-size:12px;color:var(--text-3);text-decoration:line-through;}
.br-equiv{font-size:10px;color:var(--teal-600);margin-top:1px;}
.br-item-col{display:flex;flex-direction:column;flex:1;min-width:0;margin-right:10px;}
.saving-summary-row{display:flex;justify-content:space-between;align-items:center;padding:9px 10px;background:var(--gray-50);border-radius:var(--radius-sm);border:1px solid var(--border);}
.ss-label{font-size:12px;color:var(--text-2);}
.ss-val{font-size:14px;font-weight:500;color:var(--teal-800);}
.disclaimer{background:var(--gray-50);border-radius:var(--radius-sm);padding:8px 10px;font-size:11px;color:var(--text-3);line-height:1.4;}
 
/* Savings */
.metric-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px;}
.metric-card{background:var(--gray-50);border-radius:var(--radius-sm);padding:12px;}
.metric-card.full{grid-column:1/-1;}
.mc-label{font-size:10px;color:var(--text-3);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em;}
.mc-value{font-family:'DM Serif Display',serif;font-size:26px;line-height:1;}
.mc-value.small{font-size:20px;}
.mc-sub{font-size:11px;color:var(--text-3);margin-top:3px;}
.progress-bg{height:5px;background:var(--border);border-radius:3px;overflow:hidden;}
.progress-fill{height:5px;background:var(--teal-400);border-radius:3px;}
.progress-lbl{font-size:10px;color:var(--text-3);margin-top:3px;}
.history-entry{border-bottom:1px solid var(--border);}
.history-entry:last-child{border-bottom:none;}
.history-row{display:flex;justify-content:space-between;align-items:center;padding:10px 0;cursor:pointer;}
.hr-store{font-size:13px;font-weight:500;}
.hr-date{font-size:11px;color:var(--text-3);}
.hr-right{display:flex;align-items:center;gap:6px;}
.hr-saving{font-size:13px;font-weight:500;color:var(--teal-600);}
.hr-chevron{font-size:13px;color:var(--text-3);transition:transform .2s;display:inline-block;}
.hr-chevron.open{transform:rotate(90deg);}
.hr-items-panel{display:none;padding:0 0 10px;}
.hr-items-panel.open{display:block;}
.hr-item-row{display:flex;justify-content:space-between;padding:3px 0;}
.hr-item-name{font-size:11px;color:var(--text-2);}
.hr-item-price{font-size:11px;color:var(--text-3);}
 
/* Settings */
.settings-section{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);overflow:hidden;margin-bottom:4px;}
.settings-row{display:flex;align-items:center;justify-content:space-between;padding:13px 14px;border-bottom:1px solid var(--border);cursor:pointer;}
.settings-row:last-child{border-bottom:none;}
.settings-icon{width:30px;height:30px;border-radius:8px;display:flex;align-items:center;justify-content:center;flex-shrink:0;}
.si-teal{background:var(--teal-50);}
.si-blue{background:var(--blue-50);}
.si-amber{background:var(--amber-50);}
.si-purple{background:var(--purple-50);}
.settings-label{font-size:13px;font-weight:500;}
.settings-value{font-size:12px;color:var(--text-3);}
.settings-arrow{font-size:14px;color:var(--text-3);transition:transform .2s;}
.settings-arrow.open{transform:rotate(90deg);}
.settings-edit-panel{background:var(--gray-50);padding:14px;display:none;border-top:1px solid var(--border);}
.settings-edit-panel.open{display:block;}
 
/* Location autocomplete (Problem 2) */
.loc-suggestions{display:none;margin-top:4px;border:1px solid var(--border);border-radius:var(--radius-sm);overflow:hidden;background:white;}
.loc-suggestions.open{display:block;}
.loc-suggestion-item{padding:9px 12px;font-size:12px;color:var(--text);cursor:pointer;border-bottom:1px solid var(--border);display:flex;align-items:center;gap:8px;}
.loc-suggestion-item:last-child{border-bottom:none;}
.loc-suggestion-item:hover{background:var(--gray-50);}
.loc-pin-icon{flex-shrink:0;opacity:.5;}
.loc-sub{font-size:10px;color:var(--text-3);}
 
/* Map screen */
.map-container{flex:1;position:relative;overflow:hidden;background:#e8f0e8;min-height:260px;}
@keyframes dash-move{to{stroke-dashoffset:-48;}}
.route-animated{animation:dash-move 1.2s linear infinite;}
.map-info-card{padding:14px 16px 4px;}
.map-store-name{font-size:15px;font-weight:500;}
.map-eta-row{display:flex;gap:16px;margin-top:8px;}
.map-eta-item{display:flex;align-items:center;gap:6px;}
.map-eta-label{font-size:12px;color:var(--text-3);}
.map-eta-val{font-size:13px;font-weight:500;}
.map-step{display:flex;align-items:flex-start;gap:10px;padding:7px 0;border-bottom:1px solid var(--border);}
.map-step:last-child{border-bottom:none;}
.map-step-icon{width:26px;height:26px;border-radius:50%;background:var(--teal-50);display:flex;align-items:center;justify-content:center;flex-shrink:0;}
.map-step-text{font-size:12px;color:var(--text-2);line-height:1.4;}
.map-step-dist{font-size:11px;color:var(--text-3);}
 
/* Map app picker modal (Problem 3) */
.map-picker-backdrop{display:none;position:absolute;inset:0;background:rgba(0,0,0,0.45);z-index:200;align-items:flex-end;}
.map-picker-backdrop.open{display:flex;}
.map-picker-sheet{background:white;border-radius:20px 20px 0 0;padding:20px 16px 28px;width:100%;position:relative;}
.map-picker-title{font-size:15px;font-weight:500;margin-bottom:4px;}
.map-picker-sub{font-size:12px;color:var(--text-3);margin-bottom:16px;}
.map-app-grid{display:flex;flex-direction:column;gap:8px;}
.map-app-row{display:flex;align-items:center;gap:12px;padding:11px 14px;border:1px solid var(--border);border-radius:var(--radius-sm);cursor:pointer;transition:background .12s;}
.map-app-row:hover{background:var(--gray-50);}
.map-app-icon{width:38px;height:38px;border-radius:10px;display:flex;align-items:center;justify-content:center;flex-shrink:0;font-size:20px;}
.map-app-name{font-size:13px;font-weight:500;color:var(--text);}
.map-app-desc{font-size:11px;color:var(--text-3);}
.map-picker-cancel{margin-top:10px;width:100%;padding:11px;background:var(--gray-50);border:1px solid var(--border);border-radius:var(--radius-sm);font-size:13px;font-family:'DM Sans',sans-serif;cursor:pointer;}
 
/* Share modal */
.modal-backdrop{display:none;position:absolute;inset:0;background:rgba(0,0,0,0.45);z-index:200;align-items:flex-end;}
.modal-backdrop.open{display:flex;}
.share-modal{background:white;border-radius:20px 20px 0 0;padding:20px 16px 24px;width:100%;position:relative;}
.share-title{font-size:15px;font-weight:500;margin-bottom:4px;}
.share-msg{font-size:11px;color:var(--text-3);line-height:1.5;background:var(--gray-50);border-radius:var(--radius-sm);padding:10px 12px;margin:10px 0;}
.share-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-bottom:14px;}
.share-btn-item{display:flex;flex-direction:column;align-items:center;gap:5px;cursor:pointer;border:none;background:none;font-family:'DM Sans',sans-serif;}
.share-icon-circle{width:44px;height:44px;border-radius:14px;display:flex;align-items:center;justify-content:center;}
.share-icon-label{font-size:10px;color:var(--text-2);}
.share-copy-row{display:flex;gap:8px;}
.share-copy-input{flex:1;padding:8px 10px;background:var(--gray-50);border:1px solid var(--border);border-radius:var(--radius-sm);font-size:11px;color:var(--text-2);outline:none;font-family:'DM Sans',sans-serif;}
.share-copy-btn{padding:8px 14px;background:var(--teal-400);color:white;border:none;border-radius:var(--radius-sm);font-size:12px;font-weight:500;cursor:pointer;white-space:nowrap;font-family:'DM Sans',sans-serif;}
.modal-close-btn{position:absolute;top:14px;right:16px;background:none;border:none;font-size:20px;color:var(--text-3);cursor:pointer;line-height:1;}
</style>
</head>
<body>
<div class="app-shell">
 
<!-- SCREEN 1: ONBOARDING -->
<div class="screen active" id="screen-1">
  <div class="status-bar"><div class="status-time">9:41</div><div class="status-icons"><div class="status-dot"></div><div class="status-dot" style="opacity:.4"></div><div class="status-dot" style="opacity:.2"></div></div></div>
  <div class="onboard-logo">
    <div class="logo-mark"><svg width="28" height="28" viewBox="0 0 28 28" fill="none"><path d="M5 9h18l-3 12H8L5 9z" stroke="white" stroke-width="1.8" stroke-linejoin="round" fill="none"/><circle cx="11" cy="24" r="1.8" fill="white"/><circle cx="19" cy="24" r="1.8" fill="white"/><path d="M10 14h8M10 17.5h5.5" stroke="white" stroke-width="1.5" stroke-linecap="round"/></svg></div>
    <div class="logo-name">Basket<span>Check</span></div>
    <div class="logo-tagline">Know before you go</div>
  </div>
  <div class="screen-body" style="gap:12px">
    <div>
      <div class="section-lbl">How it works</div>
      <div class="how-steps">
        <div class="how-step"><div class="step-num active">1</div><div><div class="step-text-title">Build your basket once</div><div class="step-text-sub">Add your regular weekly items — takes 3 minutes</div></div></div>
        <div class="how-step"><div class="step-num">2</div><div><div class="step-text-title">We compare all 5 stores</div><div class="step-text-sub">Live prices across Lidl, Aldi, Tesco, Dunnes, SuperValu</div></div></div>
        <div class="how-step"><div class="step-num">3</div><div><div class="step-text-title">Shop smart, save weekly</div><div class="step-text-sub">Average saving: €5–€18 per shop</div></div></div>
      </div>
    </div>
    <div class="location-section">
      <div class="section-lbl">Your location</div>
      <input class="input-field" id="loc-input" type="text" value="Rathmines, Dublin 6" oninput="onboardLocInput(this.value)" autocomplete="off">
      <div class="loc-suggestions" id="onboard-loc-suggestions"></div>
      <div class="radius-row">
        <span class="radius-lbl">Search radius</span>
        <input type="range" id="radius-slider" min="1" max="5" value="2" step="1">
        <span class="radius-val" id="radius-val">2 km</span>
      </div>
    </div>
    <div>
      <div class="section-lbl">Which store do you usually shop at?</div>
      <div class="store-btn-grid" id="store-pick-grid">
        <button class="store-pick-btn" onclick="selectUsualStore(this,'Tesco')">Tesco</button>
        <button class="store-pick-btn selected" onclick="selectUsualStore(this,'Dunnes')">Dunnes</button>
        <button class="store-pick-btn" onclick="selectUsualStore(this,'SuperValu')">SuperValu</button>
        <button class="store-pick-btn" onclick="selectUsualStore(this,'Lidl')">Lidl</button>
        <button class="store-pick-btn" onclick="selectUsualStore(this,'Aldi')">Aldi</button>
        <button class="store-pick-btn" onclick="selectUsualStore(this,'None')">No usual</button>
      </div>
    </div>
  </div>
  <div class="screen-footer"><button class="btn-primary" onclick="goTo(2)">Get started →</button></div>
</div>
 
<!-- SCREEN 2: BASKET -->
<div class="screen" id="screen-2">
  <div class="status-bar"><div class="status-time">9:42</div><div class="status-icons"><div class="status-dot"></div></div></div>
  <div class="app-topbar"><div class="topbar-logo">Basket<span>Check</span></div><div class="topbar-badge" id="basket-count-badge">12 items</div></div>
  <div class="screen-body">
    <div style="position:relative">
      <input class="input-field" type="text" id="item-search" placeholder="Search items to add (e.g. milk, free range eggs)..." autocomplete="off"
        oninput="onSearchInput(this.value)"
        onfocus="onSearchFocus()"
        onblur="setTimeout(closeDropdown,200)">
      <div class="search-dropdown" id="search-dropdown"></div>
    </div>
    <div class="section-lbl" style="margin-top:2px">My basket</div>
    <div id="basket-list"></div>
    <div class="basket-total-row"><div class="basket-total-lbl" id="basket-count-lbl">12 items</div><div class="basket-total-num" id="basket-total">~€32.40</div></div>
  </div>
  <div class="screen-footer"><button class="btn-primary" onclick="goToCompare()">Compare all stores →</button></div>
  <div class="tab-bar">
    <button class="tab" onclick="goTo(2)"><svg viewBox="0 0 18 18" fill="none"><rect x="1" y="4" width="16" height="12" rx="2" stroke="#1D9E75" stroke-width="1.4"/><path d="M5 8h8M5 11h5" stroke="#1D9E75" stroke-width="1.2" stroke-linecap="round"/></svg><span class="tab-lbl on">Basket</span></button>
    <button class="tab" onclick="goToCompare()"><svg viewBox="0 0 18 18" fill="none"><circle cx="9" cy="9" r="7" stroke="#888780" stroke-width="1.4"/><path d="M6 9h6M9 6v6" stroke="#888780" stroke-width="1.2" stroke-linecap="round"/></svg><span class="tab-lbl">Compare</span></button>
    <button class="tab" onclick="goTo(5)"><svg viewBox="0 0 18 18" fill="none"><path d="M2 13L5.5 7.5l3 3.5L12 5l4 8H2z" stroke="#888780" stroke-width="1.4" stroke-linejoin="round" fill="none"/></svg><span class="tab-lbl">Savings</span></button>
    <button class="tab" onclick="goTo(6)"><svg viewBox="0 0 18 18" fill="none"><circle cx="9" cy="9" r="6.5" stroke="#888780" stroke-width="1.4" fill="none"/><path d="M9 6.5v2.5l1.5 1.5" stroke="#888780" stroke-width="1.2" stroke-linecap="round"/></svg><span class="tab-lbl">Settings</span></button>
  </div>
</div>
 
<!-- SCREEN 3: RANKING -->
<div class="screen" id="screen-3">
  <div class="status-bar"><div class="status-time">9:43</div><div class="status-icons"><div class="status-dot"></div></div></div>
  <div class="notif-bar" onclick="goTo(3)"><div class="notif-dot"></div><div class="notif-text">Lidl is cheapest for your basket this week</div><div class="notif-arrow">›</div></div>
  <div class="screen-hdr">
    <button class="back-btn" onclick="goTo(2)"><svg width="14" height="14" viewBox="0 0 14 14" fill="none"><path d="M9 2L4 7l5 5" stroke="#444" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/></svg></button>
    <div><div class="hdr-title">Compare stores</div><div class="hdr-sub" id="ranking-sub">12 items · within 2km · updated now</div></div>
  </div>
  <div class="screen-body">
    <div class="baseline-banner"><svg width="16" height="16" viewBox="0 0 16 16" fill="none" style="flex-shrink:0"><circle cx="8" cy="8" r="6.5" stroke="#888780" stroke-width="1"/><path d="M8 5v3.5l2 1.5" stroke="#888780" stroke-width="1.2" stroke-linecap="round"/></svg><div class="baseline-text">All prices vs your usual store: <span class="baseline-store" id="usual-store-label">Dunnes</span></div></div>
    <div id="store-list"></div>
    <div class="saving-hero"><div class="saving-big" id="saving-big">€5.70</div><div class="saving-sub" id="saving-sub">less at Lidl than your usual Dunnes</div></div>
  </div>
  <div class="screen-footer">
    <button class="btn-primary" id="breakdown-btn" onclick="goToBreakdown()">See item breakdown →</button>
    <button class="btn-secondary" id="directions-btn" onclick="openMapPicker()">Get directions to Lidl</button>
  </div>
</div>
 
<!-- SCREEN 4: BREAKDOWN -->
<div class="screen" id="screen-4">
  <div class="status-bar"><div class="status-time">9:44</div><div class="status-icons"><div class="status-dot"></div></div></div>
  <div class="screen-hdr">
    <button class="back-btn" onclick="goTo(3)"><svg width="14" height="14" viewBox="0 0 14 14" fill="none"><path d="M9 2L4 7l5 5" stroke="#444" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/></svg></button>
    <div><div class="hdr-title" id="breakdown-title">Lidl vs Dunnes</div><div class="hdr-sub">Item-by-item comparison</div></div>
  </div>
  <div class="screen-body">
    <div class="col-hdr-row"><div class="col-h">Item</div><div style="display:flex;gap:24px"><div class="col-h" id="col-winner">Lidl</div><div class="col-h" id="col-usual">Dunnes</div></div></div>
    <div id="breakdown-list"></div>
    <div class="saving-summary-row"><div class="ss-label" id="bd-saving-label">Total saving at Lidl</div><div class="ss-val" id="bd-saving-val">€5.70 less</div></div>
    <div class="disclaimer">Prices updated daily and may vary by ±5% in-store.</div>
  </div>
  <div class="screen-footer">
    <button class="btn-primary" onclick="openMapPicker()">Get directions →</button>
    <button class="btn-secondary" onclick="openShareModal()">Share my savings</button>
  </div>
</div>
 
<!-- SCREEN 5: SAVINGS -->
<div class="screen" id="screen-5">
  <div class="status-bar"><div class="status-time">9:45</div><div class="status-icons"><div class="status-dot"></div></div></div>
  <div class="app-topbar"><div class="topbar-logo">Basket<span>Check</span></div><div class="topbar-badge">16 weeks</div></div>
  <div class="screen-body">
    <div class="metric-grid">
      <div class="metric-card full"><div class="mc-label">This week</div><div class="mc-value">€5.70</div><div class="mc-sub">vs shopping at <span id="usual-in-tracker">Dunnes</span></div></div>
      <div class="metric-card"><div class="mc-label">This month</div><div class="mc-value small">€22.80</div></div>
      <div class="metric-card"><div class="mc-label">All time</div><div class="mc-value small">€91.20</div></div>
    </div>
    <div style="background:var(--gray-50);border-radius:var(--radius-sm);padding:10px 12px;border:1px solid var(--border)">
      <div style="font-size:11px;color:var(--text-3);margin-bottom:4px">Monthly target: €40</div>
      <div class="progress-bg"><div class="progress-fill" style="width:57%"></div></div>
      <div class="progress-lbl">€22.80 saved · 57% of goal</div>
    </div>
    <div class="section-lbl">Recent shops — tap to see what you bought</div>
    <div id="history-list"></div>
  </div>
  <div class="screen-footer"><button class="btn-primary" onclick="openShareModal()">Share my savings</button></div>
  <div class="tab-bar">
    <button class="tab" onclick="goTo(2)"><svg viewBox="0 0 18 18" fill="none"><rect x="1" y="4" width="16" height="12" rx="2" stroke="#888780" stroke-width="1.4"/><path d="M5 8h8M5 11h5" stroke="#888780" stroke-width="1.2" stroke-linecap="round"/></svg><span class="tab-lbl">Basket</span></button>
    <button class="tab" onclick="goToCompare()"><svg viewBox="0 0 18 18" fill="none"><circle cx="9" cy="9" r="7" stroke="#888780" stroke-width="1.4"/><path d="M6 9h6M9 6v6" stroke="#888780" stroke-width="1.2" stroke-linecap="round"/></svg><span class="tab-lbl">Compare</span></button>
    <button class="tab" onclick="goTo(5)"><svg viewBox="0 0 18 18" fill="none"><path d="M2 13L5.5 7.5l3 3.5L12 5l4 8H2z" stroke="#1D9E75" stroke-width="1.4" stroke-linejoin="round" fill="none"/></svg><span class="tab-lbl on">Savings</span></button>
    <button class="tab" onclick="goTo(6)"><svg viewBox="0 0 18 18" fill="none"><circle cx="9" cy="9" r="6.5" stroke="#888780" stroke-width="1.4" fill="none"/><path d="M9 6.5v2.5l1.5 1.5" stroke="#888780" stroke-width="1.2" stroke-linecap="round"/></svg><span class="tab-lbl">Settings</span></button>
  </div>
</div>
 
<!-- SCREEN 6: SETTINGS -->
<div class="screen" id="screen-6">
  <div class="status-bar"><div class="status-time">9:46</div><div class="status-icons"><div class="status-dot"></div></div></div>
  <div class="app-topbar"><div class="topbar-logo">Basket<span>Check</span></div><div style="font-size:12px;color:var(--text-3)">Settings</div></div>
  <div class="screen-body" style="gap:8px">
    <div class="section-lbl" style="margin-top:4px">Your preferences</div>
    <div class="settings-section">
      <div class="settings-row" onclick="toggleSettingsPanel('panel-loc','arrow-loc')">
        <div style="display:flex;align-items:center;gap:10px">
          <div class="settings-icon si-teal"><svg width="16" height="16" viewBox="0 0 16 16" fill="none"><circle cx="8" cy="6.5" r="2.5" stroke="#085041" stroke-width="1.2"/><path d="M8 2C5.24 2 3 4.24 3 6.5c0 3 5 8 5 8s5-5 5-8C13 4.24 10.76 2 8 2z" stroke="#085041" stroke-width="1.2" fill="none"/></svg></div>
          <div><div class="settings-label">Location</div><div class="settings-value" id="settings-loc-display">Rathmines, Dublin 6</div></div>
        </div>
        <div class="settings-arrow" id="arrow-loc">›</div>
      </div>
      <div class="settings-edit-panel" id="panel-loc">
        <div class="section-lbl">Edit location</div>
        <div style="position:relative">
          <input class="input-field" id="settings-loc-input" type="text" value="Rathmines, Dublin 6" oninput="settingsLocInput(this.value)" autocomplete="off">
          <div class="loc-suggestions" id="settings-loc-suggestions"></div>
        </div>
        <div class="radius-row" style="margin-top:8px">
          <span class="radius-lbl">Radius</span>
          <input type="range" id="settings-radius" min="1" max="5" value="2" step="1" oninput="document.getElementById('settings-radius-val').textContent=this.value+' km'">
          <span class="radius-val" id="settings-radius-val">2 km</span>
        </div>
        <button class="btn-primary" style="margin-top:10px" onclick="saveLocation()">Save</button>
      </div>
    </div>
    <div class="settings-section">
      <div class="settings-row" onclick="toggleSettingsPanel('panel-store','arrow-store')">
        <div style="display:flex;align-items:center;gap:10px">
          <div class="settings-icon si-blue"><svg width="16" height="16" viewBox="0 0 16 16" fill="none"><rect x="1" y="5" width="14" height="10" rx="2" stroke="#0C447C" stroke-width="1.2" fill="none"/><path d="M5 5V4a3 3 0 016 0v1" stroke="#0C447C" stroke-width="1.2"/></svg></div>
          <div><div class="settings-label">Usual store</div><div class="settings-value" id="settings-store-display">Dunnes</div></div>
        </div>
        <div class="settings-arrow" id="arrow-store">›</div>
      </div>
      <div class="settings-edit-panel" id="panel-store">
        <div class="section-lbl">Change usual store</div>
        <div class="store-btn-grid" id="settings-store-grid">
          <button class="store-pick-btn" onclick="selectSettingsStore(this,'Tesco')">Tesco</button>
          <button class="store-pick-btn selected" onclick="selectSettingsStore(this,'Dunnes')">Dunnes</button>
          <button class="store-pick-btn" onclick="selectSettingsStore(this,'SuperValu')">SuperValu</button>
          <button class="store-pick-btn" onclick="selectSettingsStore(this,'Lidl')">Lidl</button>
          <button class="store-pick-btn" onclick="selectSettingsStore(this,'Aldi')">Aldi</button>
          <button class="store-pick-btn" onclick="selectSettingsStore(this,'None')">No usual</button>
        </div>
      </div>
    </div>
    <div class="settings-section">
      <div class="settings-row" onclick="toggleSettingsPanel('panel-notif','arrow-notif')">
        <div style="display:flex;align-items:center;gap:10px">
          <div class="settings-icon si-amber"><svg width="16" height="16" viewBox="0 0 16 16" fill="none"><path d="M8 2a5 5 0 015 5v3l1.5 2H1.5L3 10V7a5 5 0 015-5z" stroke="#633806" stroke-width="1.2" fill="none"/><path d="M6.5 13.5a1.5 1.5 0 003 0" stroke="#633806" stroke-width="1.2"/></svg></div>
          <div><div class="settings-label">Weekly notification</div><div class="settings-value">Thursday 7:00 PM</div></div>
        </div>
        <div class="settings-arrow" id="arrow-notif">›</div>
      </div>
      <div class="settings-edit-panel" id="panel-notif">
        <div class="section-lbl">Notification time</div>
        <div style="display:flex;gap:6px;flex-wrap:wrap;margin-bottom:8px">
          <button class="store-pick-btn selected" style="padding:5px 12px;font-size:11px">Thursday</button>
          <button class="store-pick-btn" style="padding:5px 12px;font-size:11px">Wednesday</button>
          <button class="store-pick-btn" style="padding:5px 12px;font-size:11px">Friday</button>
        </div>
        <div style="display:flex;align-items:center;gap:8px"><span style="font-size:12px;color:var(--text-2)">At</span><input class="input-field" type="time" value="19:00" style="width:110px"></div>
        <button class="btn-primary" style="margin-top:10px" onclick="toggleSettingsPanel('panel-notif','arrow-notif')">Save</button>
      </div>
    </div>
    <div class="settings-section">
      <div class="settings-row" onclick="toggleSettingsPanel('panel-goal','arrow-goal')">
        <div style="display:flex;align-items:center;gap:10px">
          <div class="settings-icon si-purple"><svg width="16" height="16" viewBox="0 0 16 16" fill="none"><path d="M2 11.5L5.5 6.5l3 3.5L12 3.5l2 8H2z" stroke="#3C3489" stroke-width="1.2" stroke-linejoin="round" fill="none"/></svg></div>
          <div><div class="settings-label">Monthly savings goal</div><div class="settings-value" id="settings-goal-display">€40 / month</div></div>
        </div>
        <div class="settings-arrow" id="arrow-goal">›</div>
      </div>
      <div class="settings-edit-panel" id="panel-goal">
        <div class="section-lbl">Set your target</div>
        <div style="display:flex;align-items:center;gap:8px"><span style="font-size:16px;color:var(--text-2)">€</span><input class="input-field" id="goal-input" type="number" min="10" max="300" value="40" style="width:80px"><span style="font-size:13px;color:var(--text-3)">per month</span></div>
        <button class="btn-primary" style="margin-top:10px" onclick="saveGoal()">Save goal</button>
      </div>
    </div>
    <div style="padding:8px 0;text-align:center"><div style="font-size:11px;color:var(--text-3);line-height:1.5">BasketCheck v1.0 · Made in Ireland<br>Data updated daily · GDPR compliant</div></div>
  </div>
  <div class="tab-bar">
    <button class="tab" onclick="goTo(2)"><svg viewBox="0 0 18 18" fill="none"><rect x="1" y="4" width="16" height="12" rx="2" stroke="#888780" stroke-width="1.4"/><path d="M5 8h8M5 11h5" stroke="#888780" stroke-width="1.2" stroke-linecap="round"/></svg><span class="tab-lbl">Basket</span></button>
    <button class="tab" onclick="goToCompare()"><svg viewBox="0 0 18 18" fill="none"><circle cx="9" cy="9" r="7" stroke="#888780" stroke-width="1.4"/><path d="M6 9h6M9 6v6" stroke="#888780" stroke-width="1.2" stroke-linecap="round"/></svg><span class="tab-lbl">Compare</span></button>
    <button class="tab" onclick="goTo(5)"><svg viewBox="0 0 18 18" fill="none"><path d="M2 13L5.5 7.5l3 3.5L12 5l4 8H2z" stroke="#888780" stroke-width="1.4" stroke-linejoin="round" fill="none"/></svg><span class="tab-lbl">Savings</span></button>
    <button class="tab" onclick="goTo(6)"><svg viewBox="0 0 18 18" fill="none"><circle cx="9" cy="9" r="6.5" stroke="#1D9E75" stroke-width="1.4" fill="none"/><path d="M9 6.5v2.5l1.5 1.5" stroke="#1D9E75" stroke-width="1.2" stroke-linecap="round"/></svg><span class="tab-lbl on">Settings</span></button>
  </div>
</div>
 
<!-- SCREEN 7: MAP -->
<div class="screen" id="screen-7">
  <div class="status-bar" style="background:var(--teal-400)"><div class="status-time" style="color:white">9:47</div><div class="status-icons"><div class="status-dot" style="background:rgba(255,255,255,.7)"></div></div></div>
  <div class="screen-hdr" style="background:var(--teal-400);border-bottom:none;padding:8px 16px 12px">
    <button class="back-btn" style="background:rgba(255,255,255,.2)" onclick="goTo(3)"><svg width="14" height="14" viewBox="0 0 14 14" fill="none"><path d="M9 2L4 7l5 5" stroke="white" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/></svg></button>
    <div><div class="hdr-title" style="color:white" id="map-header-title">Lidl Rathmines</div><div class="hdr-sub" style="color:rgba(255,255,255,.75)">0.8 km away · 10 min walk</div></div>
  </div>
  <div class="map-container">
    <svg width="100%" height="100%" viewBox="0 0 420 280" preserveAspectRatio="xMidYMid slice" style="display:block">
      <rect width="420" height="280" fill="#e5ede5"/>
      <rect x="0" y="240" width="420" height="18" fill="#b8d8e8" opacity=".8"/>
      <text x="160" y="252" font-size="9" fill="#6aa0b8" font-family="sans-serif">Grand Canal</text>
      <rect x="290" y="30" width="100" height="80" rx="6" fill="#b8d4b0"/>
      <text x="340" y="74" text-anchor="middle" font-size="9" fill="#4a7a3a" font-family="sans-serif">Palmerston Park</text>
      <rect x="10" y="20" width="65" height="50" rx="2" fill="#ccc8be"/><rect x="90" y="20" width="80" height="45" rx="2" fill="#ccc8be"/>
      <rect x="10" y="100" width="70" height="55" rx="2" fill="#ccc8be"/><rect x="100" y="100" width="65" height="55" rx="2" fill="#ccc8be"/>
      <rect x="185" y="100" width="75" height="55" rx="2" fill="#ccc8be"/>
      <rect x="10" y="175" width="80" height="55" rx="2" fill="#ccc8be"/><rect x="110" y="175" width="70" height="55" rx="2" fill="#ccc8be"/>
      <rect x="200" y="175" width="75" height="55" rx="2" fill="#ccc8be"/>
      <rect x="290" y="125" width="80" height="55" rx="2" fill="#ccc8be"/><rect x="300" y="195" width="75" height="55" rx="2" fill="#ccc8be"/>
      <line x1="185" y1="0" x2="185" y2="280" stroke="white" stroke-width="8" stroke-linecap="round"/>
      <line x1="185" y1="0" x2="185" y2="280" stroke="#f0ede8" stroke-width="6" stroke-linecap="round"/>
      <text x="188" y="14" font-size="8" fill="#999" font-family="sans-serif">Rathmines Rd</text>
      <line x1="0" y1="80" x2="420" y2="80" stroke="white" stroke-width="6"/><line x1="0" y1="80" x2="420" y2="80" stroke="#f0ede8" stroke-width="4"/>
      <line x1="0" y1="160" x2="420" y2="160" stroke="white" stroke-width="6"/><line x1="0" y1="160" x2="420" y2="160" stroke="#f0ede8" stroke-width="4"/>
      <line x1="92" y1="0" x2="92" y2="240" stroke="white" stroke-width="4"/><line x1="92" y1="0" x2="92" y2="240" stroke="#f0ede8" stroke-width="2.5"/>
      <line x1="270" y1="0" x2="270" y2="240" stroke="white" stroke-width="4"/><line x1="270" y1="0" x2="270" y2="240" stroke="#f0ede8" stroke-width="2.5"/>
      <text x="20" y="78" font-size="8" fill="#bbb" font-family="sans-serif">Leinster Rd</text>
      <text x="20" y="158" font-size="8" fill="#bbb" font-family="sans-serif">Charleston Rd</text>
      <polyline points="210,205 210,160 210,80 150,80 125,80" stroke="#1D9E75" stroke-width="5" fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-dasharray="8 4" class="route-animated"/>
      <circle cx="210" cy="205" r="14" fill="#378ADD" opacity=".2"/>
      <circle cx="210" cy="205" r="8" fill="#378ADD"/>
      <circle cx="210" cy="205" r="4" fill="white"/>
      <text x="224" y="209" font-size="9" fill="#0C447C" font-weight="bold" font-family="sans-serif">You</text>
      <ellipse cx="125" cy="88" rx="20" ry="11" fill="rgba(29,158,117,.2)"/>
      <circle cx="125" cy="77" r="12" fill="#1D9E75"/>
      <path d="M125 71h0M121 75h8l-1 4h-6l-1-4z" stroke="white" stroke-width="1.4" fill="none" stroke-linecap="round"/>
      <text x="103" y="63" font-size="9" fill="#085041" font-weight="bold" font-family="sans-serif">Lidl</text>
    </svg>
  </div>
  <div class="map-info-card">
    <div class="map-store-name" id="map-store-name">Lidl Rathmines</div>
    <div style="font-size:11px;color:var(--text-3);margin-top:1px" id="map-store-addr">1 Rathmines Road Lower, Dublin 6</div>
    <div class="map-eta-row">
      <div class="map-eta-item"><svg width="14" height="14" viewBox="0 0 14 14" fill="none"><circle cx="7" cy="7" r="5.5" stroke="#1D9E75" stroke-width="1.2"/><path d="M7 4v3l2 1.5" stroke="#1D9E75" stroke-width="1.2" stroke-linecap="round"/></svg><span class="map-eta-label">Walk</span><span class="map-eta-val">10 min</span></div>
      <div class="map-eta-item"><svg width="14" height="14" viewBox="0 0 14 14" fill="none"><circle cx="7" cy="6" r="2.5" stroke="#888780" stroke-width="1.2"/><path d="M3 12c0-2.21 1.79-4 4-4s4 1.79 4 4" stroke="#888780" stroke-width="1.2" stroke-linecap="round" fill="none"/></svg><span class="map-eta-label">Distance</span><span class="map-eta-val">0.8 km</span></div>
    </div>
    <div style="margin-top:10px">
      <div class="map-step"><div class="map-step-icon"><svg width="14" height="14" viewBox="0 0 14 14" fill="none"><path d="M7 2v6M4 5l3-3 3 3" stroke="#085041" stroke-width="1.4" stroke-linecap="round" stroke-linejoin="round"/></svg></div><div><div class="map-step-text">Head north on Rathmines Road Lower</div><div class="map-step-dist">240 m · 3 min</div></div></div>
      <div class="map-step"><div class="map-step-icon"><svg width="14" height="14" viewBox="0 0 14 14" fill="none"><path d="M7 3l-4 4 4 4M3 7h8" stroke="#085041" stroke-width="1.4" stroke-linecap="round" stroke-linejoin="round"/></svg></div><div><div class="map-step-text">Turn left onto Leinster Road West</div><div class="map-step-dist">380 m · 5 min</div></div></div>
      <div class="map-step"><div class="map-step-icon"><svg width="14" height="14" viewBox="0 0 14 14" fill="none"><circle cx="7" cy="7" r="3" fill="#1D9E75"/></svg></div><div><div class="map-step-text" style="color:var(--teal-800);font-weight:500">Arrive at Lidl — on your right</div><div class="map-step-dist">0.8 km total</div></div></div>
    </div>
  </div>
  <div class="screen-footer"><button class="btn-primary" onclick="goTo(3)">← Back to comparison</button></div>
</div>
 
<!-- MAP APP PICKER (Problem 3) -->
<div class="map-picker-backdrop" id="map-picker-modal">
  <div class="map-picker-sheet">
    <button class="modal-close-btn" onclick="closeMapPicker()">×</button>
    <div class="map-picker-title">Open in Maps</div>
    <div class="map-picker-sub" id="map-picker-sub">Get directions to Lidl Rathmines</div>
    <div class="map-app-grid">
      <div class="map-app-row" onclick="openInMapApp('google')">
        <div class="map-app-icon" style="background:#fff;border:1px solid #eee">
          <svg width="22" height="22" viewBox="0 0 24 24"><path d="M12 2C8.13 2 5 5.13 5 9c0 5.25 7 13 7 13s7-7.75 7-13c0-3.87-3.13-7-7-7z" fill="#EA4335"/><circle cx="12" cy="9" r="2.5" fill="#fff"/></svg>
        </div>
        <div><div class="map-app-name">Google Maps</div><div class="map-app-desc">Opens in Google Maps</div></div>
        <svg style="margin-left:auto;flex-shrink:0" width="14" height="14" viewBox="0 0 14 14" fill="none"><path d="M5 2l5 5-5 5" stroke="#888780" stroke-width="1.4" stroke-linecap="round" stroke-linejoin="round"/></svg>
      </div>
      <div class="map-app-row" onclick="openInMapApp('apple')">
        <div class="map-app-icon" style="background:linear-gradient(135deg,#4fc3f7,#1976d2)">
          <svg width="20" height="20" viewBox="0 0 24 24" fill="white"><path d="M18.71 19.5c-.83 1.24-1.71 2.45-3.05 2.47-1.34.03-1.77-.79-3.29-.79-1.53 0-2 .77-3.27.82-1.31.05-2.3-1.32-3.14-2.53C4.25 17 2.94 12.45 4.7 9.39c.87-1.52 2.43-2.48 4.12-2.51 1.28-.02 2.5.87 3.29.87.78 0 2.26-1.07 3.8-.91.65.03 2.47.26 3.64 1.98-.09.06-2.17 1.28-2.15 3.81.03 3.02 2.65 4.03 2.68 4.04-.03.07-.42 1.44-1.38 2.83M13 3.5c.73-.83 1.94-1.46 2.94-1.5.13 1.17-.34 2.35-1.04 3.19-.69.85-1.83 1.51-2.95 1.42-.15-1.15.41-2.35 1.05-3.11z"/></svg>
        </div>
        <div><div class="map-app-name">Apple Maps</div><div class="map-app-desc">Opens in Apple Maps</div></div>
        <svg style="margin-left:auto;flex-shrink:0" width="14" height="14" viewBox="0 0 14 14" fill="none"><path d="M5 2l5 5-5 5" stroke="#888780" stroke-width="1.4" stroke-linecap="round" stroke-linejoin="round"/></svg>
      </div>
      <div class="map-app-row" onclick="openInMapApp('waze')">
        <div class="map-app-icon" style="background:#33CCFF">
          <svg width="22" height="22" viewBox="0 0 24 24" fill="white"><path d="M12 2a9 9 0 019 9c0 3.5-1.5 5.5-3 7l-1 3H7l-1-3C4.5 16.5 3 14.5 3 11a9 9 0 019-9zm0 2a7 7 0 00-7 7c0 2.8 1.2 4.5 2.5 6l.8 2.5h7.4L16.5 17C17.8 15.5 19 13.8 19 11a7 7 0 00-7-7zm-2 7a1 1 0 110-2 1 1 0 010 2zm4 0a1 1 0 110-2 1 1 0 010 2zm-2 3c-1.5 0-2.8-.8-3.5-2h7c-.7 1.2-2 2-3.5 2z"/></svg>
        </div>
        <div><div class="map-app-name">Waze</div><div class="map-app-desc">Opens in Waze</div></div>
        <svg style="margin-left:auto;flex-shrink:0" width="14" height="14" viewBox="0 0 14 14" fill="none"><path d="M5 2l5 5-5 5" stroke="#888780" stroke-width="1.4" stroke-linecap="round" stroke-linejoin="round"/></svg>
      </div>
    </div>
    <button class="map-picker-cancel" onclick="closeMapPicker()">Cancel</button>
  </div>
</div>
 
<!-- SHARE MODAL -->
<div class="modal-backdrop" id="share-modal">
  <div class="share-modal">
    <button class="modal-close-btn" onclick="closeShareModal()">×</button>
    <div class="share-title">Share your savings</div>
    <div class="share-msg" id="share-msg-text"></div>
    <div class="share-grid">
      <button class="share-btn-item" onclick="shareToSocial('whatsapp')">
        <div class="share-icon-circle" style="background:#25D366"><svg width="24" height="24" viewBox="0 0 24 24" fill="none"><path d="M12 4a8 8 0 018 8 8 8 0 01-8 8 7.9 7.9 0 01-4.3-1.27L4 20l1.27-3.7A7.9 7.9 0 014 12a8 8 0 018-8z" fill="white"/><path d="M9.5 9s.5 1.2 1.8 2.5 2.5 1.8 2.5 1.8l1.1-1.1c.3-.3.8-.1.9.1l1.5 1.5c.3.3.1.8-.1 1-.6.6-1.7 1.1-2.7.5-1.2-.7-3.9-3.4-4.6-4.6-.6-1-.1-2.1.5-2.7.2-.2.7-.4 1-.1l1.5 1.5c.2.2 0 .7 0 .7l-1.1 1.1z" fill="#25D366"/></svg></div>
        <span class="share-icon-label">WhatsApp</span>
      </button>
      <button class="share-btn-item" onclick="shareToSocial('twitter')">
        <div class="share-icon-circle" style="background:#000"><svg width="22" height="22" viewBox="0 0 22 22" fill="none"><path d="M4 4l5.5 7.5L4 18h2l4.5-5.5L15 18h3l-5.8-7.8L17.5 4h-2L11 9l-4-5H4z" fill="white"/></svg></div>
        <span class="share-icon-label">X / Twitter</span>
      </button>
      <button class="share-btn-item" onclick="shareToSocial('instagram')">
        <div class="share-icon-circle" style="background:radial-gradient(circle at 30% 107%,#fdf497 0%,#fd5949 45%,#d6249f 60%,#285AEB 90%)"><svg width="22" height="22" viewBox="0 0 22 22" fill="none"><rect x="3.5" y="3.5" width="15" height="15" rx="4.5" stroke="white" stroke-width="1.5" fill="none"/><circle cx="11" cy="11" r="3.5" stroke="white" stroke-width="1.5" fill="none"/><circle cx="16" cy="6.5" r="1.2" fill="white"/></svg></div>
        <span class="share-icon-label">Instagram</span>
      </button>
      <button class="share-btn-item" onclick="shareToSocial('tiktok')">
        <div class="share-icon-circle" style="background:#010101"><svg width="22" height="22" viewBox="0 0 22 22" fill="none"><path d="M15 4c.5 2.3 2.2 3.5 4 3.5v3c-1.5 0-3-.5-4-1.5V15a5 5 0 11-5-5v3a2 2 0 102 2V4h3z" fill="white"/></svg></div>
        <span class="share-icon-label">TikTok</span>
      </button>
    </div>
    <div class="share-copy-row">
      <input class="share-copy-input" id="share-copy-input" readonly>
      <button class="share-copy-btn" id="copy-btn" onclick="copyShareText()">Copy</button>
    </div>
  </div>
</div>
 
<script>
// ══════════════════════════════════════════════════════
// STATE
// ══════════════════════════════════════════════════════
let usualStore='Dunnes', selectedStore='Lidl', searchRadius=2;
let recentSearches=[]; // Feature 1: recent searches
 
const BASKET_ITEMS=[
  {id:1,name:'Sliced bread 800g',qty:1,cat:'grain',prices:{Lidl:.99,Aldi:1.09,Dunnes:1.89,SuperValu:1.95,Tesco:1.85}},
  {id:2,name:'Whole milk 2L',qty:2,cat:'dairy',prices:{Lidl:1.09,Aldi:1.12,Dunnes:1.20,SuperValu:1.25,Tesco:1.19}},
  {id:3,name:'Free range eggs 6pk',qty:1,cat:'protein',prices:{Lidl:2.29,Aldi:2.19,Dunnes:2.69,SuperValu:2.79,Tesco:2.65}},
  {id:4,name:'Chicken fillets 500g',qty:1,cat:'protein',prices:{Lidl:4.49,Aldi:4.29,Dunnes:5.50,SuperValu:5.69,Tesco:5.45}},
  {id:5,name:'Pasta penne 500g',qty:2,cat:'grain',prices:{Lidl:.59,Aldi:.65,Dunnes:.80,SuperValu:.85,Tesco:.79}},
  {id:6,name:'Heinz Baked Beans',qty:2,cat:'tin',prices:{Lidl:null,Aldi:null,Dunnes:1.09,SuperValu:1.15,Tesco:1.05},equiv:{Lidl:{name:'Simply Beans (own brand)',price:.49},Aldi:{name:'Harvest Morn Beans',price:.45}}},
  {id:7,name:'Cheddar cheese 400g',qty:1,cat:'dairy',prices:{Lidl:2.89,Aldi:2.79,Dunnes:3.29,SuperValu:3.45,Tesco:3.19}},
  {id:8,name:'Mixed veg bag 1kg',qty:1,cat:'veg',prices:{Lidl:.99,Aldi:.99,Dunnes:1.49,SuperValu:1.59,Tesco:1.45}},
  {id:9,name:'Natural yoghurt 500g',qty:1,cat:'dairy',prices:{Lidl:1.29,Aldi:1.19,Dunnes:1.79,SuperValu:1.89,Tesco:1.69}},
  {id:10,name:'Porridge oats 1kg',qty:1,cat:'grain',prices:{Lidl:1.29,Aldi:1.19,Dunnes:1.99,SuperValu:2.09,Tesco:1.89}},
  {id:11,name:'Tomatoes 6pk',qty:1,cat:'veg',prices:{Lidl:.89,Aldi:.89,Dunnes:1.29,SuperValu:1.35,Tesco:1.19}},
  {id:12,name:'Orange juice 1L',qty:1,cat:'drink',prices:{Lidl:1.49,Aldi:1.59,Dunnes:1.99,SuperValu:2.09,Tesco:1.95}},
];
 
const SHOP_HISTORY=[
  {id:1,store:'Lidl Rathmines',date:'This week',saving:5.70,items:[{name:'Sliced bread',price:.99},{name:'Whole milk ×2',price:2.18},{name:'Eggs 6pk',price:2.29},{name:'Chicken fillets',price:4.49},{name:'Pasta ×2',price:1.18},{name:'Simply Beans ×2',price:.98},{name:'Cheddar cheese',price:2.89},{name:'Mixed veg',price:.99},{name:'Yoghurt',price:1.29},{name:'Oats',price:1.29},{name:'Tomatoes',price:.89},{name:'Orange juice',price:1.49}]},
  {id:2,store:"Aldi Harold's Cross",date:'Last week',saving:4.80,items:[{name:'Sliced bread',price:1.09},{name:'Whole milk ×2',price:2.24},{name:'Eggs 6pk',price:2.19},{name:'Chicken fillets',price:4.29},{name:'Pasta ×2',price:1.30},{name:'Harvest Morn Beans ×2',price:.90},{name:'Cheddar',price:2.79},{name:'Mixed veg',price:.99}]},
  {id:3,store:'Lidl Rathmines',date:'2 weeks ago',saving:6.20,items:[{name:'Sliced bread',price:.99},{name:'Whole milk ×2',price:2.18},{name:'Eggs 6pk',price:2.29},{name:'Chicken fillets',price:4.49},{name:'Cheddar',price:2.89},{name:'Orange juice',price:1.49}]},
  {id:4,store:'Dunnes Rathmines',date:'3 weeks ago',saving:5.80,items:[{name:'Sliced bread',price:1.89},{name:'Whole milk ×2',price:2.40},{name:'Heinz Beans ×2',price:2.18},{name:'Cheddar',price:3.29},{name:'Mixed veg',price:1.49}]},
];
 
const CAT_COLORS={grain:'#BA7517',dairy:'#378ADD',protein:'#D4537E',tin:'#888780',veg:'#639922',drink:'#7F77DD',snack:'#D85A30',household:'#888780',frozen:'#378ADD',bakery:'#BA7517',condiment:'#1D9E75',sweet:'#D4537E',alcohol:'#7F77DD',hygiene:'#888780',cleaning:'#888780',baby:'#D4537E',pet:'#888780',health:'#1D9E75'};
 
const STORE_META={Lidl:{abbr:'LDL',cls:'abbr-lidl'},Aldi:{abbr:'ALD',cls:'abbr-aldi'},Dunnes:{abbr:'DUN',cls:'abbr-dunnes'},SuperValu:{abbr:'SV',cls:'abbr-sv'},Tesco:{abbr:'TSC',cls:'abbr-tesco'}};
 
// ══════════════════════════════════════════════════════
// PROBLEM 1: COMPREHENSIVE GROCERY CATALOG
// Covers all major supermarket categories across Ireland
// ══════════════════════════════════════════════════════
const CATALOG=[
  // ── DAIRY & EGGS ──
  {name:'Whole milk 2L',cat:'dairy'},{name:'Semi-skimmed milk 2L',cat:'dairy'},{name:'Skimmed milk 2L',cat:'dairy'},{name:'Oat milk 1L',cat:'dairy'},{name:'Almond milk 1L',cat:'dairy'},{name:'Soy milk 1L',cat:'dairy'},{name:'Lactose free milk 1L',cat:'dairy'},
  {name:'Free range eggs 6pk',cat:'dairy'},{name:'Free range eggs 12pk',cat:'dairy'},{name:'Organic eggs 6pk',cat:'dairy'},{name:'Large eggs 6pk',cat:'dairy'},
  {name:'Butter 500g',cat:'dairy'},{name:'Unsalted butter 250g',cat:'dairy'},{name:'Low fat spread 500g',cat:'dairy'},
  {name:'Cheddar cheese 400g',cat:'dairy'},{name:'Mature cheddar 400g',cat:'dairy'},{name:'Mild cheddar 400g',cat:'dairy'},{name:'Red cheddar 400g',cat:'dairy'},{name:'Mozzarella 125g',cat:'dairy'},{name:'Brie 200g',cat:'dairy'},{name:'Gouda 400g',cat:'dairy'},{name:'Parmesan 100g',cat:'dairy'},{name:'Feta cheese 200g',cat:'dairy'},{name:'Cottage cheese 300g',cat:'dairy'},{name:'Cream cheese 200g',cat:'dairy'},{name:'Processed cheese slices 200g',cat:'dairy'},
  {name:'Natural yoghurt 500g',cat:'dairy'},{name:'Greek yoghurt 500g',cat:'dairy'},{name:'Low fat yoghurt 500g',cat:'dairy'},{name:'Strawberry yoghurt 4pk',cat:'dairy'},{name:'Vanilla yoghurt 4pk',cat:'dairy'},{name:'Kids yoghurt 6pk',cat:'dairy'},
  {name:'Fresh cream 200ml',cat:'dairy'},{name:'Sour cream 200ml',cat:'dairy'},{name:'Crème fraîche 200ml',cat:'dairy'},{name:'Double cream 300ml',cat:'dairy'},{name:'Whipping cream 300ml',cat:'dairy'},
 
  // ── MEAT & FISH (PROTEIN) ──
  {name:'Chicken fillets 500g',cat:'protein'},{name:'Chicken breasts 600g',cat:'protein'},{name:'Chicken thighs 1kg',cat:'protein'},{name:'Chicken drumsticks 1kg',cat:'protein'},{name:'Whole chicken 1.5kg',cat:'protein'},{name:'Chicken mince 500g',cat:'protein'},
  {name:'Beef mince 500g',cat:'protein'},{name:'Lean beef mince 500g',cat:'protein'},{name:'Steak 300g',cat:'protein'},{name:'Sirloin steak 300g',cat:'protein'},{name:'Ribeye steak 250g',cat:'protein'},{name:'Beef burgers 4pk',cat:'protein'},{name:'Diced beef 500g',cat:'protein'},{name:'Beef stir fry strips 400g',cat:'protein'},
  {name:'Pork chops 500g',cat:'protein'},{name:'Pork sausages 8pk',cat:'protein'},{name:'Pork belly 600g',cat:'protein'},{name:'Bacon rashers 400g',cat:'protein'},{name:'Back bacon 400g',cat:'protein'},{name:'Streaky bacon 200g',cat:'protein'},{name:'Ham slices 200g',cat:'protein'},{name:'Cooked ham 200g',cat:'protein'},
  {name:'Lamb chops 500g',cat:'protein'},{name:'Lamb mince 500g',cat:'protein'},
  {name:'Salmon fillets 300g',cat:'protein'},{name:'Smoked salmon 200g',cat:'protein'},{name:'Cod fillets 400g',cat:'protein'},{name:'Haddock fillets 400g',cat:'protein'},{name:'Tuna steaks 2pk',cat:'protein'},{name:'Prawns 250g',cat:'protein'},{name:'Battered fish fillets 4pk',cat:'protein'},
  {name:'Tuna tin 4pk',cat:'tin'},{name:'Tuna in brine 185g',cat:'tin'},{name:'Sardines tin',cat:'tin'},{name:'Mackerel tin',cat:'tin'},
  {name:'Turkey mince 500g',cat:'protein'},{name:'Turkey rashers 200g',cat:'protein'},
 
  // ── BAKERY & BREAD ──
  {name:'Sliced white bread 800g',cat:'bakery'},{name:'Sliced brown bread 800g',cat:'bakery'},{name:'Wholemeal bread 800g',cat:'bakery'},{name:'Seeded loaf 800g',cat:'bakery'},{name:'Sourdough loaf',cat:'bakery'},{name:'Tiger bread loaf',cat:'bakery'},
  {name:'Rolls 6pk',cat:'bakery'},{name:'Burger buns 4pk',cat:'bakery'},{name:'Hot dog rolls 6pk',cat:'bakery'},{name:'Bagels 5pk',cat:'bakery'},{name:'Pitta bread 6pk',cat:'bakery'},{name:'Tortilla wraps 8pk',cat:'bakery'},{name:'Naan bread 2pk',cat:'bakery'},{name:'Ciabatta rolls 2pk',cat:'bakery'},
  {name:'Plain flour 1.5kg',cat:'bakery'},{name:'Self raising flour 1.5kg',cat:'bakery'},{name:'Bread flour 1.5kg',cat:'bakery'},{name:'Baking powder 200g',cat:'bakery'},{name:'Bicarbonate of soda 200g',cat:'bakery'},{name:'Yeast sachets 7g',cat:'bakery'},
  {name:'Croissants 4pk',cat:'bakery'},{name:'Brioche rolls 4pk',cat:'bakery'},{name:'Scones 4pk',cat:'bakery'},
 
  // ── FRUIT & VEG ──
  {name:'Bananas bunch',cat:'veg'},{name:'Apples 6pk',cat:'veg'},{name:'Granny smith apples 4pk',cat:'veg'},{name:'Oranges 4pk',cat:'veg'},{name:'Clementines 600g',cat:'veg'},{name:'Grapes 500g',cat:'veg'},{name:'Strawberries 400g',cat:'veg'},{name:'Blueberries 150g',cat:'veg'},{name:'Raspberries 150g',cat:'veg'},{name:'Mango 1 each',cat:'veg'},{name:'Pineapple 1 each',cat:'veg'},{name:'Lemon 4pk',cat:'veg'},{name:'Lime 4pk',cat:'veg'},{name:'Kiwi 4pk',cat:'veg'},{name:'Peaches 4pk',cat:'veg'},{name:'Melon half',cat:'veg'},{name:'Avocado 2pk',cat:'veg'},
  {name:'Potatoes 2kg',cat:'veg'},{name:'Baby potatoes 750g',cat:'veg'},{name:'Sweet potatoes 1kg',cat:'veg'},{name:'Carrots 1kg',cat:'veg'},{name:'Baby carrots 400g',cat:'veg'},{name:'Onions 1kg',cat:'veg'},{name:'Red onions 500g',cat:'veg'},{name:'Spring onions bunch',cat:'veg'},{name:'Garlic bulb',cat:'veg'},{name:'Garlic cloves 3pk',cat:'veg'},
  {name:'Tomatoes 6pk',cat:'veg'},{name:'Cherry tomatoes 250g',cat:'veg'},{name:'Plum tomatoes 400g',cat:'veg'},{name:'Cucumber 1 each',cat:'veg'},{name:'Iceberg lettuce',cat:'veg'},{name:'Mixed salad leaves 100g',cat:'veg'},{name:'Baby spinach 200g',cat:'veg'},{name:'Kale 200g',cat:'veg'},{name:'Broccoli 1 head',cat:'veg'},{name:'Cauliflower 1 head',cat:'veg'},{name:'Cabbage 1 head',cat:'veg'},{name:'Red cabbage',cat:'veg'},{name:'Brussels sprouts 500g',cat:'veg'},{name:'Courgette 2pk',cat:'veg'},{name:'Aubergine 1 each',cat:'veg'},{name:'Red pepper 3pk',cat:'veg'},{name:'Yellow pepper 3pk',cat:'veg'},{name:'Mixed peppers 3pk',cat:'veg'},{name:'Celery bunch',cat:'veg'},{name:'Leeks 500g',cat:'veg'},{name:'Mushrooms 400g',cat:'veg'},{name:'Chestnut mushrooms 400g',cat:'veg'},{name:'Sweetcorn 2 ears',cat:'veg'},{name:'Peas fresh 500g',cat:'veg'},{name:'Mixed veg bag 1kg',cat:'veg'},{name:'Beansprouts 300g',cat:'veg'},{name:'Parsnips 500g',cat:'veg'},{name:'Turnip 1 each',cat:'veg'},{name:'Beetroot 3pk',cat:'veg'},
  {name:'Fresh herbs mixed',cat:'veg'},{name:'Fresh basil pot',cat:'veg'},{name:'Fresh coriander bunch',cat:'veg'},{name:'Fresh parsley bunch',cat:'veg'},{name:'Fresh chillies 3pk',cat:'veg'},
 
  // ── CEREALS & BREAKFAST ──
  {name:'Porridge oats 1kg',cat:'grain'},{name:'Rolled oats 1kg',cat:'grain'},{name:'Ready brek 750g',cat:'grain'},{name:'Weetabix 24pk',cat:'grain'},{name:'Corn flakes 500g',cat:'grain'},{name:'Bran flakes 750g',cat:'grain'},{name:'Rice crispies 500g',cat:'grain'},{name:'Granola 500g',cat:'grain'},{name:'Muesli 750g',cat:'grain'},{name:'Crunchy nut cornflakes 500g',cat:'grain'},{name:'Frosties 500g',cat:'grain'},
 
  // ── PASTA, RICE & GRAINS ──
  {name:'Pasta penne 500g',cat:'grain'},{name:'Spaghetti 500g',cat:'grain'},{name:'Fusilli 500g',cat:'grain'},{name:'Tagliatelle 500g',cat:'grain'},{name:'Linguine 500g',cat:'grain'},{name:'Macaroni 500g',cat:'grain'},{name:'Lasagne sheets 500g',cat:'grain'},{name:'Noodles 500g',cat:'grain'},{name:'Egg noodles 500g',cat:'grain'},{name:'Rice noodles 250g',cat:'grain'},{name:'Udon noodles 3pk',cat:'grain'},
  {name:'Long grain rice 1kg',cat:'grain'},{name:'Basmati rice 1kg',cat:'grain'},{name:'Brown rice 1kg',cat:'grain'},{name:'Jasmine rice 1kg',cat:'grain'},{name:'Microwave rice pouches 3pk',cat:'grain'},{name:'Arborio rice 500g',cat:'grain'},
  {name:'Couscous 500g',cat:'grain'},{name:'Quinoa 500g',cat:'grain'},{name:'Bulgur wheat 500g',cat:'grain'},{name:'Lentils 500g',cat:'grain'},{name:'Red lentils 500g',cat:'grain'},{name:'Chickpeas tin 400g',cat:'tin'},{name:'Kidney beans tin 400g',cat:'tin'},{name:'Baked beans tin 4pk',cat:'tin'},{name:'Heinz Baked Beans 4pk',cat:'tin'},{name:'Sweetcorn tin 340g',cat:'tin'},{name:'Chopped tomatoes tin 400g',cat:'tin'},{name:'Whole tomatoes tin 400g',cat:'tin'},{name:'Lentil soup tin',cat:'tin'},{name:'Coconut milk tin 400ml',cat:'tin'},
 
  // ── DRINKS ──
  {name:'Orange juice 1L',cat:'drink'},{name:'Pressed apple juice 1L',cat:'drink'},{name:'Smooth orange juice 1.75L',cat:'drink'},{name:'Cranberry juice 1L',cat:'drink'},{name:'Pineapple juice 1L',cat:'drink'},{name:'Squash no added sugar 1L',cat:'drink'},{name:'Ribena 1L',cat:'drink'},
  {name:'Sparkling water 6pk',cat:'drink'},{name:'Still water 6pk',cat:'drink'},{name:'Sparkling water 1.5L',cat:'drink'},{name:'Tap water filter jug',cat:'drink'},
  {name:'Tea bags 80pk',cat:'drink'},{name:'Tea bags 240pk',cat:'drink'},{name:'Green tea bags 40pk',cat:'drink'},{name:'Herbal tea bags 20pk',cat:'drink'},{name:'Instant coffee 200g',cat:'drink'},{name:'Coffee granules 200g',cat:'drink'},{name:'Ground coffee 250g',cat:'drink'},{name:'Coffee pods 10pk',cat:'drink'},{name:'Hot chocolate 400g',cat:'drink'},
  {name:'Coca cola 6pk cans',cat:'drink'},{name:'Diet coke 6pk cans',cat:'drink'},{name:'7up 6pk cans',cat:'drink'},{name:'Fanta 6pk cans',cat:'drink'},{name:'Lucozade sport 6pk',cat:'drink'},{name:'Red bull 4pk',cat:'drink'},
  {name:'Beer 6pk',cat:'alcohol'},{name:'Lager 12pk',cat:'alcohol'},{name:'Wine red 750ml',cat:'alcohol'},{name:'Wine white 750ml',cat:'alcohol'},{name:'Prosecco 750ml',cat:'alcohol'},
 
  // ── FROZEN FOODS ──
  {name:'Frozen peas 1kg',cat:'frozen'},{name:'Frozen mixed veg 1kg',cat:'frozen'},{name:'Frozen sweetcorn 1kg',cat:'frozen'},{name:'Frozen broccoli 900g',cat:'frozen'},{name:'Frozen spinach 900g',cat:'frozen'},
  {name:'Frozen chips 1kg',cat:'frozen'},{name:'Oven chips 1kg',cat:'frozen'},{name:'Frozen waffles 10pk',cat:'frozen'},{name:'Frozen hash browns 1kg',cat:'frozen'},
  {name:'Frozen fish fingers 10pk',cat:'frozen'},{name:'Frozen battered cod 4pk',cat:'frozen'},{name:'Frozen prawns 400g',cat:'frozen'},{name:'Frozen salmon fillets 4pk',cat:'frozen'},
  {name:'Frozen chicken nuggets 500g',cat:'frozen'},{name:'Frozen beef burgers 4pk',cat:'frozen'},{name:'Frozen lasagne 400g',cat:'frozen'},{name:'Frozen pizza 350g',cat:'frozen'},{name:'Frozen dumplings 300g',cat:'frozen'},
  {name:'Ice cream 1L',cat:'frozen'},{name:'Chocolate ice cream 1L',cat:'frozen'},{name:'Vanilla ice cream 1L',cat:'frozen'},{name:'Ice cream cones 4pk',cat:'frozen'},{name:'Magnum ice cream 4pk',cat:'frozen'},
 
  // ── CONDIMENTS & SAUCES ──
  {name:'Ketchup 700ml',cat:'condiment'},{name:'Heinz ketchup 700ml',cat:'condiment'},{name:'Brown sauce 400ml',cat:'condiment'},{name:'Mayonnaise 800ml',cat:'condiment'},{name:'Hellmanns mayonnaise 800ml',cat:'condiment'},{name:'Mustard 185g',cat:'condiment'},{name:'Dijon mustard 185g',cat:'condiment'},{name:'Barbecue sauce 300ml',cat:'condiment'},{name:'Soy sauce 150ml',cat:'condiment'},{name:'Sweet chilli sauce 220ml',cat:'condiment'},{name:'Hot sauce 200ml',cat:'condiment'},{name:'Worcestershire sauce 150ml',cat:'condiment'},{name:'Vinegar 568ml',cat:'condiment'},{name:'Balsamic vinegar 250ml',cat:'condiment'},
  {name:'Olive oil 500ml',cat:'condiment'},{name:'Sunflower oil 1L',cat:'condiment'},{name:'Vegetable oil 1L',cat:'condiment'},{name:'Coconut oil 500ml',cat:'condiment'},{name:'Rapeseed oil 500ml',cat:'condiment'},
  {name:'Pasta sauce jar 500g',cat:'condiment'},{name:'Bolognese sauce jar 500g',cat:'condiment'},{name:'Pesto green 190g',cat:'condiment'},{name:'Red pesto 190g',cat:'condiment'},{name:'Curry paste 290g',cat:'condiment'},{name:'Tikka masala sauce jar',cat:'condiment'},{name:'Korma sauce jar',cat:'condiment'},{name:'Stir fry sauce sachet',cat:'condiment'},
  {name:'Jam strawberry 340g',cat:'condiment'},{name:'Raspberry jam 340g',cat:'condiment'},{name:'Marmalade 340g',cat:'condiment'},{name:'Honey 340g',cat:'condiment'},{name:'Peanut butter 340g',cat:'condiment'},{name:'Nutella 400g',cat:'condiment'},{name:'Marmite 250g',cat:'condiment'},
  {name:'Salt 750g',cat:'condiment'},{name:'Black pepper ground 38g',cat:'condiment'},{name:'Mixed herbs jar 25g',cat:'condiment'},{name:'Paprika jar 38g',cat:'condiment'},{name:'Curry powder jar 38g',cat:'condiment'},{name:'Garlic powder jar 38g',cat:'condiment'},{name:'Cumin jar 38g',cat:'condiment'},{name:'Stock cubes 12pk',cat:'condiment'},{name:'Chicken stock cubes 12pk',cat:'condiment'},{name:'Beef stock cubes 12pk',cat:'condiment'},
  {name:'Sugar 1kg',cat:'condiment'},{name:'Icing sugar 500g',cat:'condiment'},{name:'Brown sugar 500g',cat:'condiment'},
 
  // ── SNACKS & CRISPS ──
  {name:'Crisps multipack 6pk',cat:'snack'},{name:'Tayto cheese and onion 12pk',cat:'snack'},{name:'Pringles 200g',cat:'snack'},{name:'Doritos 150g',cat:'snack'},{name:'Kettle chips 150g',cat:'snack'},{name:'Rice cakes 130g',cat:'snack'},{name:'Popcorn 100g',cat:'snack'},{name:'Pretzels 150g',cat:'snack'},{name:'Crackers 200g',cat:'snack'},{name:'Cream crackers 200g',cat:'snack'},{name:'Digestive biscuits 400g',cat:'snack'},{name:'Hobnobs 300g',cat:'snack'},{name:'Custard creams 300g',cat:'snack'},{name:'Jaffa cakes 12pk',cat:'snack'},{name:'Rich tea biscuits 300g',cat:'snack'},
 
  // ── SWEETS & CHOCOLATE ──
  {name:'Chocolate bar 100g',cat:'sweet'},{name:'Milk chocolate bar 100g',cat:'sweet'},{name:'Dark chocolate bar 100g',cat:'sweet'},{name:'Cadbury dairy milk 200g',cat:'sweet'},{name:'Roses chocolate box 400g',cat:'sweet'},{name:'Kitkat 4pk',cat:'sweet'},{name:'Maltesers 120g',cat:'sweet'},{name:'Haribo sweets 200g',cat:'sweet'},{name:'Wine gums 200g',cat:'sweet'},{name:'Jelly beans 200g',cat:'sweet'},
 
  // ── HOUSEHOLD & CLEANING ──
  {name:'Toilet roll 9pk',cat:'household'},{name:'Toilet roll 18pk',cat:'household'},{name:'Kitchen roll 4pk',cat:'household'},{name:'Tissues box',cat:'household'},{name:'Napkins 50pk',cat:'household'},{name:'Bin bags 30pk',cat:'household'},{name:'Sandwich bags 50pk',cat:'household'},{name:'Cling film roll',cat:'household'},{name:'Tin foil roll',cat:'household'},{name:'Baking paper roll',cat:'household'},
  {name:'Washing up liquid 500ml',cat:'cleaning'},{name:'Fairy washing up liquid 500ml',cat:'cleaning'},{name:'Dishwasher tablets 30pk',cat:'cleaning'},{name:'Dishwasher tablets 60pk',cat:'cleaning'},{name:'Dishwasher salt 2kg',cat:'cleaning'},{name:'Dishwasher rinse aid 400ml',cat:'cleaning'},
  {name:'Washing powder 1kg',cat:'cleaning'},{name:'Persil washing powder 2kg',cat:'cleaning'},{name:'Ariel washing powder 2kg',cat:'cleaning'},{name:'Washing liquid 1L',cat:'cleaning'},{name:'Fabric softener 1L',cat:'cleaning'},{name:'Comfort fabric softener 1L',cat:'cleaning'},
  {name:'Bleach 1L',cat:'cleaning'},{name:'Flash spray 500ml',cat:'cleaning'},{name:'Dettol spray 500ml',cat:'cleaning'},{name:'Bathroom cleaner 500ml',cat:'cleaning'},{name:'Kitchen cleaner 500ml',cat:'cleaning'},{name:'Floor cleaner 1L',cat:'cleaning'},{name:'Glass cleaner 500ml',cat:'cleaning'},{name:'Mop refill',cat:'cleaning'},{name:'Sponges 3pk',cat:'cleaning'},{name:'Rubber gloves',cat:'cleaning'},
  {name:'Air freshener spray',cat:'cleaning'},{name:'Plug in air freshener',cat:'cleaning'},{name:'Candle',cat:'cleaning'},
 
  // ── HYGIENE & PERSONAL CARE ──
  {name:'Shampoo 400ml',cat:'hygiene'},{name:'Conditioner 400ml',cat:'hygiene'},{name:'Body wash 500ml',cat:'hygiene'},{name:'Bar soap 4pk',cat:'hygiene'},{name:'Hand soap 500ml',cat:'hygiene'},{name:'Shower gel 500ml',cat:'hygiene'},{name:'Deodorant roll on',cat:'hygiene'},{name:'Deodorant spray 150ml',cat:'hygiene'},{name:'Toothpaste 125ml',cat:'hygiene'},{name:'Toothbrush',cat:'hygiene'},{name:'Toothbrush electric replacement',cat:'hygiene'},{name:'Mouthwash 500ml',cat:'hygiene'},{name:'Dental floss',cat:'hygiene'},{name:'Razor 4pk',cat:'hygiene'},{name:'Shaving foam 200ml',cat:'hygiene'},{name:'Face wash 150ml',cat:'hygiene'},{name:'Moisturiser 200ml',cat:'hygiene'},{name:'Sunscreen SPF50 200ml',cat:'hygiene'},{name:'Lip balm',cat:'hygiene'},
  {name:'Sanitary towels 14pk',cat:'hygiene'},{name:'Tampons 20pk',cat:'hygiene'},{name:'Pantyliner 24pk',cat:'hygiene'},
 
  // ── HEALTH ──
  {name:'Paracetamol 500mg 24pk',cat:'health'},{name:'Ibuprofen 400mg 24pk',cat:'health'},{name:'Vitamin C 1000mg 30pk',cat:'health'},{name:'Vitamin D 30pk',cat:'health'},{name:'Multivitamins 30pk',cat:'health'},{name:'Iron tablets 30pk',cat:'health'},{name:'Omega 3 fish oil 30pk',cat:'health'},{name:'Protein bar 60g',cat:'health'},{name:'Protein powder 1kg',cat:'health'},
 
  // ── BABY & KIDS ──
  {name:'Nappies size 3 44pk',cat:'baby'},{name:'Nappies size 4 40pk',cat:'baby'},{name:'Nappies size 5 36pk',cat:'baby'},{name:'Baby wipes 64pk',cat:'baby'},{name:'Baby formula 800g',cat:'baby'},{name:'Baby food pouches 4pk',cat:'baby'},{name:'Baby shampoo 200ml',cat:'baby'},
 
  // ── PET FOOD ──
  {name:'Dog food dry 3kg',cat:'pet'},{name:'Cat food tins 4pk',cat:'pet'},{name:'Cat food pouches 12pk',cat:'pet'},{name:'Dog treats 200g',cat:'pet'},{name:'Cat treats 60g',cat:'pet'},{name:'Cat litter 10L',cat:'pet'},
 
  // ── READY MEALS & CONVENIENCE ──
  {name:'Ready meal pasta 400g',cat:'frozen'},{name:'Ready meal curry 400g',cat:'frozen'},{name:'Soup carton 1L',cat:'tin'},{name:'Tomato soup tin 400g',cat:'tin'},{name:'Vegetable soup tin 400g',cat:'tin'},{name:'Instant noodles 3pk',cat:'grain'},{name:'Pot noodle 90g',cat:'grain'},{name:'Cup a soup 4pk',cat:'tin'},{name:'Microwave macaroni cheese',cat:'grain'},
];
 
// Category display names and order
const CAT_META={
  dairy:{label:'Dairy & eggs',order:1},protein:{label:'Meat & fish',order:2},bakery:{label:'Bakery',order:3},
  grain:{label:'Cereals, pasta & rice',order:4},veg:{label:'Fruit & veg',order:5},frozen:{label:'Frozen foods',order:6},
  drink:{label:'Drinks',order:7},tin:{label:'Tinned goods',order:8},condiment:{label:'Condiments & sauces',order:9},
  snack:{label:'Snacks & biscuits',order:10},sweet:{label:'Sweets & chocolate',order:11},alcohol:{label:'Alcohol',order:12},
  household:{label:'Household',order:13},cleaning:{label:'Cleaning',order:14},hygiene:{label:'Personal care',order:15},
  health:{label:'Health & pharmacy',order:16},baby:{label:'Baby & kids',order:17},pet:{label:'Pet food',order:18},
};
 
// ══════════════════════════════════════════════════════
// PROBLEM 2: LOCATION SUGGESTIONS FOR ALL 32 COUNTIES
// ══════════════════════════════════════════════════════
const IRELAND_LOCATIONS=[
  // Dublin
  {name:'Dublin City Centre',county:'Dublin',stores:[{name:'Tesco Metro Henry St',dist:.3},{name:'Lidl Parnell St',dist:.5},{name:'Aldi Abbey St',dist:.6},{name:'Dunnes St Stephens Green',dist:.4}]},
  {name:'Rathmines, Dublin 6',county:'Dublin',stores:[{name:'Lidl Rathmines',dist:.8},{name:"Aldi Harold's Cross",dist:1.3},{name:'Dunnes Rathmines',dist:.4},{name:'SuperValu Rathgar',dist:1.9},{name:'Tesco Terenure',dist:2.1}]},
  {name:'Malahide, Dublin',county:'Dublin',stores:[{name:'Tesco Malahide',dist:.4},{name:'Lidl Malahide Rd',dist:1.2},{name:'SuperValu Malahide',dist:.6},{name:'Dunnes Malahide',dist:.8}]},
  {name:'Tallaght, Dublin',county:'Dublin',stores:[{name:'Lidl Tallaght',dist:.3},{name:'Aldi Tallaght',dist:.5},{name:'Tesco Tallaght',dist:.2},{name:'Dunnes Tallaght',dist:.4}]},
  {name:'Swords, Dublin',county:'Dublin',stores:[{name:'Tesco Swords',dist:.5},{name:'Lidl Swords',dist:.7},{name:'Aldi Swords',dist:.9},{name:'SuperValu Swords',dist:.6}]},
  {name:'Blanchardstown, Dublin',county:'Dublin',stores:[{name:'Dunnes Blanchardstown',dist:.4},{name:'Tesco Blanchardstown',dist:.3},{name:'Lidl Blanchardstown',dist:.6},{name:'Aldi Blanchardstown',dist:.8}]},
  {name:'Dundrum, Dublin',county:'Dublin',stores:[{name:'Lidl Dundrum',dist:.4},{name:'Tesco Dundrum',dist:.5},{name:'SuperValu Dundrum',dist:.3},{name:'Dunnes Dundrum',dist:.6}]},
  {name:'Dún Laoghaire, Dublin',county:'Dublin',stores:[{name:'SuperValu Dún Laoghaire',dist:.5},{name:'Tesco Dún Laoghaire',dist:.3},{name:'Lidl Dún Laoghaire',dist:.7},{name:'Aldi Dún Laoghaire',dist:.9}]},
  // Cork
  {name:'Cork City Centre',county:'Cork',stores:[{name:'Tesco Cork Patrick St',dist:.2},{name:'Lidl Cork City',dist:.6},{name:'Aldi Cork City',dist:.5},{name:'Dunnes Patrick St',dist:.3}]},
  {name:'Douglas, Cork',county:'Cork',stores:[{name:'SuperValu Douglas',dist:.4},{name:'Lidl Douglas',dist:.6},{name:'Tesco Douglas',dist:.5},{name:'Dunnes Douglas',dist:.8}]},
  {name:'Ballincollig, Cork',county:'Cork',stores:[{name:'Lidl Ballincollig',dist:.4},{name:'SuperValu Ballincollig',dist:.3},{name:'Tesco Ballincollig',dist:.7}]},
  {name:'Togher, Cork',county:'Cork',stores:[{name:'Aldi Togher',dist:.3},{name:'Lidl Togher',dist:.4},{name:'Tesco Wilton',dist:.6}]},
  // Galway
  {name:'Eyre Square, Galway',county:'Galway',stores:[{name:'Tesco Eyre Square',dist:.2},{name:'Lidl Eyre Square',dist:.5},{name:'Dunnes Galway Shopping Centre',dist:.3},{name:'Aldi Galway',dist:.6}]},
  {name:'Salthill, Galway',county:'Galway',stores:[{name:'SuperValu Salthill',dist:.3},{name:'Tesco Salthill',dist:.5},{name:'Lidl Galway West',dist:.8}]},
  {name:'Tuam, Galway',county:'Galway',stores:[{name:'Lidl Tuam',dist:.4},{name:'SuperValu Tuam',dist:.5}]},
  // Limerick
  {name:'Limerick City Centre',county:'Limerick',stores:[{name:'Tesco Limerick',dist:.3},{name:'Lidl Limerick City',dist:.5},{name:'Aldi Limerick',dist:.4},{name:'Dunnes Limerick',dist:.3}]},
  {name:'Dooradoyle, Limerick',county:'Limerick',stores:[{name:'Tesco Dooradoyle',dist:.3},{name:'Lidl Dooradoyle',dist:.5},{name:'SuperValu Dooradoyle',dist:.4}]},
  // Waterford
  {name:'Waterford City Centre',county:'Waterford',stores:[{name:'Tesco Waterford',dist:.2},{name:'Lidl Waterford',dist:.5},{name:'Aldi Waterford',dist:.4},{name:'Dunnes Waterford',dist:.3}]},
  // Kilkenny
  {name:'Kilkenny City Centre',county:'Kilkenny',stores:[{name:'SuperValu Kilkenny',dist:.4},{name:'Tesco Kilkenny',dist:.3},{name:'Lidl Kilkenny',dist:.6}]},
  // Wexford
  {name:'Wexford Town',county:'Wexford',stores:[{name:'Lidl Wexford',dist:.4},{name:'Tesco Wexford',dist:.3},{name:'Aldi Wexford',dist:.5}]},
  // Wicklow
  {name:'Bray, Wicklow',county:'Wicklow',stores:[{name:'Tesco Bray',dist:.3},{name:'Lidl Bray',dist:.5},{name:'Aldi Bray',dist:.4},{name:'SuperValu Bray',dist:.6}]},
  {name:'Wicklow Town',county:'Wicklow',stores:[{name:'SuperValu Wicklow',dist:.4},{name:'Tesco Wicklow',dist:.3}]},
  // Kildare
  {name:'Naas, Kildare',county:'Kildare',stores:[{name:'Lidl Naas',dist:.5},{name:'Tesco Naas',dist:.3},{name:'Dunnes Naas',dist:.4}]},
  {name:'Newbridge, Kildare',county:'Kildare',stores:[{name:'Tesco Newbridge',dist:.3},{name:'Lidl Newbridge',dist:.5}]},
  // Meath
  {name:'Navan, Meath',county:'Meath',stores:[{name:'Tesco Navan',dist:.3},{name:'Lidl Navan',dist:.5},{name:'Aldi Navan',dist:.4},{name:'SuperValu Navan',dist:.6}]},
  {name:'Drogheda, Meath',county:'Meath',stores:[{name:'Tesco Drogheda',dist:.4},{name:'Lidl Drogheda',dist:.6},{name:'Aldi Drogheda',dist:.5},{name:'Dunnes Drogheda',dist:.3}]},
  // Louth
  {name:'Dundalk, Louth',county:'Louth',stores:[{name:'Tesco Dundalk',dist:.3},{name:'Lidl Dundalk',dist:.5},{name:'Aldi Dundalk',dist:.4},{name:'SuperValu Dundalk',dist:.6}]},
  // Westmeath
  {name:'Athlone, Westmeath',county:'Westmeath',stores:[{name:'Tesco Athlone',dist:.4},{name:'Lidl Athlone',dist:.5},{name:'Aldi Athlone',dist:.6}]},
  {name:'Mullingar, Westmeath',county:'Westmeath',stores:[{name:'Tesco Mullingar',dist:.3},{name:'Lidl Mullingar',dist:.5}]},
  // Tipperary
  {name:'Clonmel, Tipperary',county:'Tipperary',stores:[{name:'Tesco Clonmel',dist:.3},{name:'Lidl Clonmel',dist:.5},{name:'Aldi Clonmel',dist:.4}]},
  {name:'Thurles, Tipperary',county:'Tipperary',stores:[{name:'SuperValu Thurles',dist:.4},{name:'Lidl Thurles',dist:.5}]},
  // Clare
  {name:'Ennis, Clare',county:'Clare',stores:[{name:'Tesco Ennis',dist:.3},{name:'Lidl Ennis',dist:.5},{name:'Aldi Ennis',dist:.4}]},
  // Mayo
  {name:'Castlebar, Mayo',county:'Mayo',stores:[{name:'Tesco Castlebar',dist:.4},{name:'Lidl Castlebar',dist:.5},{name:'Aldi Castlebar',dist:.6}]},
  {name:'Westport, Mayo',county:'Mayo',stores:[{name:'SuperValu Westport',dist:.4},{name:'Tesco Westport',dist:.5}]},
  // Sligo
  {name:'Sligo Town',county:'Sligo',stores:[{name:'Tesco Sligo',dist:.3},{name:'Lidl Sligo',dist:.5},{name:'Aldi Sligo',dist:.4},{name:'Dunnes Sligo',dist:.3}]},
  // Donegal
  {name:'Letterkenny, Donegal',county:'Donegal',stores:[{name:'Tesco Letterkenny',dist:.4},{name:'Lidl Letterkenny',dist:.5},{name:'Aldi Letterkenny',dist:.6}]},
  // Cavan
  {name:'Cavan Town',county:'Cavan',stores:[{name:'Tesco Cavan',dist:.3},{name:'Lidl Cavan',dist:.5}]},
  // Monaghan
  {name:'Monaghan Town',county:'Monaghan',stores:[{name:'Tesco Monaghan',dist:.3},{name:'Lidl Monaghan',dist:.5}]},
  // Roscommon
  {name:'Roscommon Town',county:'Roscommon',stores:[{name:'SuperValu Roscommon',dist:.4},{name:'Lidl Roscommon',dist:.5}]},
  // Leitrim
  {name:'Carrick-on-Shannon, Leitrim',county:'Leitrim',stores:[{name:'SuperValu Carrick-on-Shannon',dist:.4},{name:'Tesco Carrick-on-Shannon',dist:.5}]},
  // Kerry
  {name:'Tralee, Kerry',county:'Kerry',stores:[{name:'Tesco Tralee',dist:.3},{name:'Lidl Tralee',dist:.5},{name:'Aldi Tralee',dist:.4}]},
  {name:'Killarney, Kerry',county:'Kerry',stores:[{name:'Tesco Killarney',dist:.4},{name:'SuperValu Killarney',dist:.3},{name:'Lidl Killarney',dist:.6}]},
  // Offaly
  {name:'Tullamore, Offaly',county:'Offaly',stores:[{name:'Tesco Tullamore',dist:.3},{name:'Lidl Tullamore',dist:.5}]},
  // Laois
  {name:'Portlaoise, Laois',county:'Laois',stores:[{name:'Tesco Portlaoise',dist:.3},{name:'Lidl Portlaoise',dist:.5},{name:'Aldi Portlaoise',dist:.4}]},
  // Longford
  {name:'Longford Town',county:'Longford',stores:[{name:'Tesco Longford',dist:.3},{name:'Lidl Longford',dist:.5}]},
  // Carlow
  {name:'Carlow Town',county:'Carlow',stores:[{name:'Tesco Carlow',dist:.3},{name:'Lidl Carlow',dist:.5},{name:'Aldi Carlow',dist:.4}]},
  // Northern Ireland
  {name:'Belfast City Centre',county:'Belfast',stores:[{name:'Tesco Belfast',dist:.3},{name:'Lidl Belfast City',dist:.5},{name:'Sainsbury\'s Belfast',dist:.4},{name:'Asda Belfast',dist:.6}]},
  {name:'Derry/Londonderry',county:'Derry',stores:[{name:'Tesco Derry',dist:.4},{name:'Lidl Derry',dist:.5},{name:'Asda Derry',dist:.6}]},
  {name:'Newry, Down',county:'Down',stores:[{name:'Tesco Newry',dist:.3},{name:'Lidl Newry',dist:.5}]},
  {name:'Armagh City',county:'Armagh',stores:[{name:'Tesco Armagh',dist:.4},{name:'Lidl Armagh',dist:.5}]},
  {name:'Enniskillen, Fermanagh',county:'Fermanagh',stores:[{name:'Tesco Enniskillen',dist:.4},{name:'Lidl Enniskillen',dist:.5}]},
  {name:'Omagh, Tyrone',county:'Tyrone',stores:[{name:'Tesco Omagh',dist:.4},{name:'Lidl Omagh',dist:.5}]},
  {name:'Antrim Town',county:'Antrim',stores:[{name:'Tesco Antrim',dist:.4},{name:'Lidl Antrim',dist:.5}]},
  {name:'Ballymena, Antrim',county:'Antrim',stores:[{name:'Tesco Ballymena',dist:.3},{name:'Lidl Ballymena',dist:.5}]},
];
 
// Current location data (updated when user changes location)
let currentLocationData=IRELAND_LOCATIONS.find(l=>l.name==='Rathmines, Dublin 6');
 
function getLocSuggestions(val){
  if(!val||val.length<2)return[];
  const q=val.toLowerCase();
  return IRELAND_LOCATIONS.filter(l=>
    l.name.toLowerCase().includes(q)||
    l.county.toLowerCase().includes(q)
  ).slice(0,6);
}
 
function renderLocSuggestions(inputId, suggestId, val){
  const box=document.getElementById(suggestId);
  const suggestions=getLocSuggestions(val);
  if(!suggestions.length){box.classList.remove('open');return;}
  box.innerHTML=suggestions.map(s=>`
    <div class="loc-suggestion-item" onmousedown="selectLocation('${s.name}','${inputId}','${suggestId}')">
      <svg class="loc-pin-icon" width="12" height="12" viewBox="0 0 12 12" fill="none"><circle cx="6" cy="5" r="2" stroke="#1D9E75" stroke-width="1.2"/><path d="M6 2C4.34 2 3 3.34 3 5c0 2.5 3 6 3 6s3-3.5 3-6c0-1.66-1.34-3-3-3z" stroke="#1D9E75" stroke-width="1.2" fill="none"/></svg>
      <div><div>${s.name}</div><div class="loc-sub">Co. ${s.county} · ${s.stores.length} stores nearby</div></div>
    </div>`).join('');
  box.classList.add('open');
}
 
function selectLocation(name, inputId, suggestId){
  document.getElementById(inputId).value=name;
  document.getElementById(suggestId).classList.remove('open');
  currentLocationData=IRELAND_LOCATIONS.find(l=>l.name===name)||null;
  if(inputId==='settings-loc-input'){
    document.getElementById('settings-loc-display').textContent=name;
  }
}
 
function onboardLocInput(val){renderLocSuggestions('loc-input','onboard-loc-suggestions',val);}
function settingsLocInput(val){renderLocSuggestions('settings-loc-input','settings-loc-suggestions',val);}
 
// ══════════════════════════════════════════════════════
// NAVIGATION
// ══════════════════════════════════════════════════════
function goTo(n){
  document.querySelectorAll('.screen').forEach(s=>s.classList.remove('active'));
  document.getElementById('screen-'+n).classList.add('active');
  if(n===2)renderBasket();
  if(n===3)renderRanking();
  if(n===5){document.getElementById('usual-in-tracker').textContent=usualStore||'usual store';renderHistory();}
}
function goToCompare(){renderRanking();goTo(3);}
function goToBreakdown(){renderBreakdown(selectedStore);goTo(4);}
function goToMap(){
  const nm=selectedStore+(selectedStore==='Lidl'?' Rathmines':selectedStore==='Aldi'?" Harold's Cross":' Nearby');
  document.getElementById('map-header-title').textContent=nm;
  document.getElementById('map-store-name').textContent=nm;
  goTo(7);
}
 
// ══════════════════════════════════════════════════════
// ONBOARDING / SETTINGS
// ══════════════════════════════════════════════════════
function selectUsualStore(btn,store){
  document.querySelectorAll('#store-pick-grid .store-pick-btn').forEach(b=>b.classList.remove('selected'));
  btn.classList.add('selected');
  usualStore=store==='None'?null:store;
  document.getElementById('settings-store-display').textContent=usualStore||'None';
  document.querySelectorAll('#settings-store-grid .store-pick-btn').forEach(b=>b.classList.toggle('selected',b.textContent===(usualStore||'None')));
}
document.getElementById('radius-slider').addEventListener('input',function(){
  document.getElementById('radius-val').textContent=this.value+' km';
  searchRadius=parseInt(this.value);
});
function toggleSettingsPanel(panelId,arrowId){
  const panel=document.getElementById(panelId);const arrow=document.getElementById(arrowId);
  const wasOpen=panel.classList.contains('open');
  document.querySelectorAll('.settings-edit-panel').forEach(p=>p.classList.remove('open'));
  document.querySelectorAll('.settings-arrow').forEach(a=>a.classList.remove('open'));
  if(!wasOpen){panel.classList.add('open');if(arrow)arrow.classList.add('open');}
}
function saveLocation(){
  const val=document.getElementById('settings-loc-input').value;
  document.getElementById('settings-loc-display').textContent=val;
  currentLocationData=IRELAND_LOCATIONS.find(l=>l.name===val)||null;
  toggleSettingsPanel('panel-loc','arrow-loc');
}
function selectSettingsStore(btn,store){
  document.querySelectorAll('#settings-store-grid .store-pick-btn').forEach(b=>b.classList.remove('selected'));
  btn.classList.add('selected');
  usualStore=store==='None'?null:store;
  document.getElementById('settings-store-display').textContent=store;
  document.querySelectorAll('#store-pick-grid .store-pick-btn').forEach(b=>b.classList.toggle('selected',b.textContent===(usualStore||'No usual')));
}
function saveGoal(){
  const val=document.getElementById('goal-input').value;
  document.getElementById('settings-goal-display').textContent='€'+val+' / month';
  toggleSettingsPanel('panel-goal','arrow-goal');
}
 
// ══════════════════════════════════════════════════════
// BASKET
// ══════════════════════════════════════════════════════
function renderBasket(){
  const list=document.getElementById('basket-list');list.innerHTML='';let total=0;
  BASKET_ITEMS.forEach(item=>{
    const price=item.prices['Tesco']||item.prices['Dunnes']||1.5;
    total+=(price||1.5)*item.qty;
    const el=document.createElement('div');el.className='basket-item';
    el.innerHTML=`<div class="item-left"><div class="item-cat-dot" style="background:${CAT_COLORS[item.cat]||'#888'}"></div><div class="item-name">${item.name}</div></div><div class="item-right"><div class="qty-ctrl"><button class="qty-btn" onclick="changeQty(${item.id},-1)">−</button><span class="qty-num" id="qty-${item.id}">${item.qty}</span><button class="qty-btn" onclick="changeQty(${item.id},1)">+</button></div><button class="item-remove" onclick="removeItem(${item.id})">×</button></div>`;
    list.appendChild(el);
  });
  const count=BASKET_ITEMS.reduce((s,i)=>s+i.qty,0);
  document.getElementById('basket-total').textContent='~€'+total.toFixed(2);
  document.getElementById('basket-count-lbl').textContent=count+' items';
  document.getElementById('basket-count-badge').textContent=count+' items';
}
function changeQty(id,delta){
  const item=BASKET_ITEMS.find(i=>i.id===id);if(!item)return;
  item.qty=Math.max(1,item.qty+delta);
  document.getElementById('qty-'+id).textContent=item.qty;
  const total=BASKET_ITEMS.reduce((s,i)=>{const p=i.prices['Tesco']||i.prices['Dunnes']||1.5;return s+p*i.qty;},0);
  const count=BASKET_ITEMS.reduce((s,i)=>s+i.qty,0);
  document.getElementById('basket-total').textContent='~€'+total.toFixed(2);
  document.getElementById('basket-count-lbl').textContent=count+' items';
  document.getElementById('basket-count-badge').textContent=count+' items';
}
function removeItem(id){
  const idx=BASKET_ITEMS.findIndex(i=>i.id===id);
  if(idx>-1)BASKET_ITEMS.splice(idx,1);
  renderBasket();
}
 
// ══════════════════════════════════════════════════════
// PROBLEM 1 + FEATURE 1: COMPREHENSIVE SEARCH ENGINE
// ══════════════════════════════════════════════════════
 
// Relevance scoring: exact word match > prefix match > word prefix > contains > category name match
function scoreItem(item, queryTerms){
  const nameLower=item.name.toLowerCase();
  const catLower=(CAT_META[item.cat]?.label||item.cat).toLowerCase();
  let score=0;
  for(const term of queryTerms){
    if(!term)continue;
    const words=nameLower.split(/\s+/);
    if(words.includes(term))score+=100;                              // exact word match
    else if(nameLower.startsWith(term))score+=80;                   // name prefix
    else if(words.some(w=>w.startsWith(term)))score+=60;            // word prefix
    else if(nameLower.includes(term))score+=40;                     // contains
    else if(catLower.includes(term))score+=10;                      // category match
  }
  return score;
}
 
// Highlight all matched query terms in a string
function highlightTerms(text, queryTerms){
  let result=text;
  for(const term of queryTerms){
    if(!term)continue;
    const regex=new RegExp('('+term.replace(/[.*+?^${}()|[\]\\]/g,'\\$&')+')','gi');
    result=result.replace(regex,'<span class="suggest-match">$1</span>');
  }
  return result;
}
 
function closeDropdown(){document.getElementById('search-dropdown').classList.remove('open');}
 
// Feature 1: show recent searches when field is focused with no query
function onSearchFocus(){
  const val=document.getElementById('item-search').value.trim();
  if(!val)showRecentSearches();
}
 
function showRecentSearches(){
  const dd=document.getElementById('search-dropdown');
  if(!recentSearches.length){dd.classList.remove('open');return;}
  let html=`<div class="drop-section-hdr"><span class="drop-section-lbl">Recent searches</span><button class="drop-clear-btn" onmousedown="clearRecentSearches()">Clear all</button></div>`;
  html+=recentSearches.map(r=>
    `<div class="recent-item" onmousedown="addItem('${r.name.replace(/'/g,"\\'")}','${r.cat}')">
      <svg class="recent-clock" width="14" height="14" viewBox="0 0 14 14" fill="none"><circle cx="7" cy="7" r="5.5" stroke="#888780" stroke-width="1.2"/><path d="M7 4.5v3l2 1.5" stroke="#888780" stroke-width="1.2" stroke-linecap="round"/></svg>
      <span class="recent-name">${r.name}</span>
      <span style="font-size:9px;color:var(--text-3)">${CAT_META[r.cat]?.label||r.cat}</span>
      <button class="recent-remove" onmousedown="removeRecentSearch('${r.name.replace(/'/g,"\\'")}')" onclick="event.stopPropagation()">×</button>
    </div>`
  ).join('');
  dd.innerHTML=html;
  dd.classList.add('open');
}
 
function clearRecentSearches(){recentSearches=[];closeDropdown();}
function removeRecentSearch(name){
  recentSearches=recentSearches.filter(r=>r.name!==name);
  if(!recentSearches.length)closeDropdown();
  else showRecentSearches();
}
 
function onSearchInput(val){
  const dd=document.getElementById('search-dropdown');
  const trimmed=val.trim();
 
  // Feature 1: If input is empty, show recent searches; if no recent match, hide recents and show catalog
  if(!trimmed){
    showRecentSearches();
    return;
  }
 
  // Feature 1: If typed value doesn't match any recent search, hide recents and show catalog only
  const queryTerms=trimmed.toLowerCase().split(/\s+/);
 
  // Score and sort catalog
  const scored=CATALOG
    .map(item=>({item,score:scoreItem(item,queryTerms)}))
    .filter(x=>x.score>0)
    .sort((a,b)=>b.score-a.score);
 
  if(!scored.length){
    dd.innerHTML=`<div class="search-empty"><div class="search-empty-icon">🔍</div><div class="search-empty-title">No results for "${trimmed}"</div><div class="search-empty-sub">Try a different spelling, or add it as a custom item</div><div style="margin-top:10px"><button style="padding:7px 16px;background:var(--teal-50);color:var(--teal-800);border:1px solid var(--teal-100);border-radius:var(--radius-sm);font-size:12px;cursor:pointer;font-family:inherit" onmousedown="addItem('${trimmed}','grain')">Add "${trimmed}" anyway</button></div></div>`;
    dd.classList.add('open');
    return;
  }
 
  // Group by category
  const groups={};
  scored.forEach(({item})=>{
    if(!groups[item.cat])groups[item.cat]=[];
    if(groups[item.cat].length<4)groups[item.cat].push(item);
  });
 
  // Sort groups by their first item's score descending
  const sortedCats=Object.keys(groups).sort((a,b)=>{
    const scoreA=scoreItem(groups[a][0],queryTerms);
    const scoreB=scoreItem(groups[b][0],queryTerms);
    return scoreB-scoreA;
  });
 
  let html='';
  sortedCats.forEach(cat=>{
    const meta=CAT_META[cat]||{label:cat};
    const dot=CAT_COLORS[cat]||'#888';
    html+=`<div class="cat-group-hdr"><div class="cat-group-dot" style="background:${dot}"></div><div class="cat-group-name">${meta.label}</div><div class="cat-group-count">${groups[cat].length}</div></div>`;
    groups[cat].forEach(item=>{
      const highlighted=highlightTerms(item.name,queryTerms);
      html+=`<div class="suggestion-item" onmousedown="addItem('${item.name.replace(/'/g,"\\'")}','${item.cat}')">${highlighted}</div>`;
    });
  });
 
  dd.innerHTML=html;
  dd.classList.add('open');
}
 
function addItem(name,cat){
  const newItem={id:Date.now(),name,qty:1,cat:cat||'grain',prices:{Lidl:1.29,Aldi:1.19,Dunnes:1.79,SuperValu:1.89,Tesco:1.69}};
  BASKET_ITEMS.push(newItem);
  // Feature 1: Save to recent searches (deduplicated, max 8)
  recentSearches=recentSearches.filter(r=>r.name!==name);
  recentSearches.unshift({name,cat});
  if(recentSearches.length>8)recentSearches.pop();
  document.getElementById('item-search').value='';
  closeDropdown();
  renderBasket();
}
 
// ══════════════════════════════════════════════════════
// RANKING — uses currentLocationData for real store names
// ══════════════════════════════════════════════════════
function getBasketTotal(store){
  return BASKET_ITEMS.reduce((sum,item)=>{
    let price=item.prices[store];
    if(price===null||price===undefined)price=item.equiv&&item.equiv[store]?item.equiv[store].price:null;
    if(price===null)price=(item.prices['Dunnes']||item.prices['Tesco']||1.5)*.75;
    return sum+price*item.qty;
  },0);
}
 
function getStoreName(store){
  if(!currentLocationData)return store+' Nearby';
  // Match store name in currentLocationData
  const match=currentLocationData.stores.find(s=>s.name.toLowerCase().includes(store.toLowerCase()));
  return match?match.name:store+' Nearby';
}
 
function getStoreDist(store){
  if(!currentLocationData)return '—';
  const match=currentLocationData.stores.find(s=>s.name.toLowerCase().includes(store.toLowerCase()));
  return match?match.dist.toFixed(1)+'km':'—';
}
 
function renderRanking(){
  const baseline=usualStore||'Tesco';
  document.getElementById('usual-store-label').textContent=baseline;
  const loc=currentLocationData?currentLocationData.name:'your area';
  document.getElementById('ranking-sub').textContent=BASKET_ITEMS.length+' items · '+loc+' · '+searchRadius+'km radius';
  const stores=['Lidl','Aldi','Dunnes','SuperValu','Tesco'];
  const totals=stores.map(s=>({store:s,total:getBasketTotal(s)}));
  totals.sort((a,b)=>a.total-b.total);
  const baselineTotal=getBasketTotal(baseline);
  const cheapest=totals[0];selectedStore=cheapest.store;
  const list=document.getElementById('store-list');list.innerHTML='';
  totals.forEach((s,idx)=>{
    const diff=baselineTotal-s.total;
    const isBaseline=s.store===baseline;
    let dHtml;
    if(isBaseline)dHtml=`<span class="delta-usual">your usual store</span>`;
    else if(diff>0)dHtml=`<span class="delta-saving">€${diff.toFixed(2)} less than ${baseline}</span>`;
    else dHtml=`<span class="delta-more">€${Math.abs(diff).toFixed(2)} more than ${baseline}</span>`;
    const meta=STORE_META[s.store];
    const storeFullName=getStoreName(s.store);
    const storeDist=getStoreDist(s.store);
    const row=document.createElement('div');row.className='store-rank-row';
    row.innerHTML=`<div class="rank-num">${idx+1}</div><div class="store-abbr ${meta.cls}">${meta.abbr}</div><div class="store-info"><div class="store-nm">${storeFullName}</div><div class="store-dist">${storeDist} away</div></div><div class="store-price-col"><div class="store-total">€${s.total.toFixed(2)}</div><div class="store-delta">${dHtml}</div></div><div class="store-chevron">›</div>`;
    row.onclick=()=>{selectedStore=s.store;goToBreakdown();};
    list.appendChild(row);
  });
  const saving=baselineTotal-cheapest.total;
  document.getElementById('saving-big').textContent=saving>0?`€${saving.toFixed(2)}`:'€0.00';
  document.getElementById('saving-sub').textContent=saving>0?`less at ${cheapest.store} than your usual ${baseline}`:`${cheapest.store} is already cheapest`;
  document.getElementById('breakdown-btn').textContent='See item breakdown →';
  document.getElementById('directions-btn').textContent=`Get directions to ${getStoreName(cheapest.store)}`;
}
 
// ══════════════════════════════════════════════════════
// BREAKDOWN
// ══════════════════════════════════════════════════════
function renderBreakdown(winnerStore){
  const baseline=usualStore||'Tesco';
  document.getElementById('breakdown-title').textContent=`${getStoreName(winnerStore)} vs ${baseline}`;
  document.getElementById('col-winner').textContent=winnerStore;
  document.getElementById('col-usual').textContent=baseline;
  const list=document.getElementById('breakdown-list');list.innerHTML='';let totalSaving=0;
  BASKET_ITEMS.forEach(item=>{
    const wp=item.prices[winnerStore];const up=item.prices[baseline]||item.prices['Tesco']||1.5;
    const isUnavail=wp===null||wp===undefined;const hasEquiv=isUnavail&&item.equiv&&item.equiv[winnerStore];
    const row=document.createElement('div');
    if(isUnavail){
      row.className='breakdown-row';
      const ep=hasEquiv?item.equiv[winnerStore].price:null;
      totalSaving+=ep!==null?(up-ep)*item.qty:0;
      row.innerHTML=`<div class="br-item-col"><div class="br-item" style="color:var(--text-3);text-decoration:line-through">${item.name}</div>${hasEquiv?`<div class="br-equiv">Own-brand: ${item.equiv[winnerStore].name}</div>`:'<div class="br-equiv">Not stocked</div>'}</div><div class="br-prices"><div class="br-cheap">${hasEquiv?'€'+ep.toFixed(2):'—'}</div><div class="br-dear">€${up.toFixed(2)}</div></div>`;
    }else{
      row.className='breakdown-row';totalSaving+=(up-wp)*item.qty;
      row.innerHTML=`<div class="br-item">${item.name}${item.qty>1?' ×'+item.qty:''}</div><div class="br-prices"><div class="${wp<up?'br-cheap':'br-dear'}" style="${wp>=up?'text-decoration:none;color:var(--text-2)':''}">€${(wp*item.qty).toFixed(2)}</div><div class="${wp<up?'br-dear':'br-cheap'}" style="${wp<up?'':'text-decoration:none;color:var(--text-2)'}">€${(up*item.qty).toFixed(2)}</div></div>`;
    }
    list.appendChild(row);
  });
  document.getElementById('bd-saving-label').textContent=`Total saving at ${winnerStore}`;
  document.getElementById('bd-saving-val').textContent=totalSaving>0?`€${totalSaving.toFixed(2)} less`:`€${Math.abs(totalSaving).toFixed(2)} more`;
}
 
// ══════════════════════════════════════════════════════
// SAVINGS HISTORY
// ══════════════════════════════════════════════════════
function renderHistory(){
  const list=document.getElementById('history-list');list.innerHTML='';
  SHOP_HISTORY.forEach(shop=>{
    const el=document.createElement('div');el.className='history-entry';
    const rowTotal=shop.items.reduce((s,i)=>s+i.price,0);
    el.innerHTML=`
      <div class="history-row" onclick="toggleHistory(${shop.id})">
        <div><div class="hr-store">${shop.store}</div><div class="hr-date">${shop.date}</div></div>
        <div class="hr-right"><div class="hr-saving">−€${shop.saving.toFixed(2)}</div><span class="hr-chevron" id="hc-${shop.id}">›</span></div>
      </div>
      <div class="hr-items-panel" id="hi-${shop.id}">
        <div style="background:var(--gray-50);border-radius:var(--radius-sm);padding:8px 10px;margin-bottom:8px">
          ${shop.items.map(i=>`<div class="hr-item-row"><div class="hr-item-name">${i.name}</div><div class="hr-item-price">€${i.price.toFixed(2)}</div></div>`).join('')}
          <div class="hr-item-row" style="border-top:1px solid var(--border);margin-top:5px;padding-top:5px"><div class="hr-item-name" style="font-weight:500;color:var(--text)">Total paid</div><div class="hr-item-price" style="font-weight:500;color:var(--text)">€${rowTotal.toFixed(2)}</div></div>
          <div class="hr-item-row"><div class="hr-item-name" style="color:var(--teal-600)">Saved vs ${usualStore||'usual store'}</div><div class="hr-item-price" style="color:var(--teal-600);font-weight:500">€${shop.saving.toFixed(2)}</div></div>
        </div>
      </div>`;
    list.appendChild(el);
  });
}
function toggleHistory(id){
  const panel=document.getElementById('hi-'+id);const chevron=document.getElementById('hc-'+id);
  const open=panel.classList.contains('open');
  panel.classList.toggle('open',!open);chevron.classList.toggle('open',!open);
}
 
// ══════════════════════════════════════════════════════
// PROBLEM 3: MAP APP PICKER — real-world directions
// ══════════════════════════════════════════════════════
function openMapPicker(){
  const storeName=getStoreName(selectedStore);
  document.getElementById('map-picker-sub').textContent='Get directions to '+storeName;
  document.getElementById('map-picker-modal').classList.add('open');
}
function closeMapPicker(){document.getElementById('map-picker-modal').classList.remove('open');}
 
function openInMapApp(app){
  const storeName=encodeURIComponent(getStoreName(selectedStore)+' Ireland');
  const loc=currentLocationData?currentLocationData.name:'Ireland';
  const q=encodeURIComponent(getStoreName(selectedStore)+', '+loc);
  let url='';
  if(app==='google') url=`https://www.google.com/maps/search/?api=1&query=${q}`;
  else if(app==='apple') url=`http://maps.apple.com/?q=${q}`;
  else if(app==='waze') url=`https://waze.com/ul?q=${q}&navigate=yes`;
  closeMapPicker();
  window.open(url,'_blank');
}
 
// ══════════════════════════════════════════════════════
// SHARE MODAL
// ══════════════════════════════════════════════════════
function openShareModal(){
  const baseline=usualStore||'Tesco';
  const w=(getBasketTotal(baseline)-getBasketTotal(selectedStore)).toFixed(2);
  const full=`I saved €${w} this week (€91.20 all time!) with BasketCheck — Ireland's free grocery price comparison app. Download at basketcheck.ie 🛒`;
  const short=`Saved €${w} this week with BasketCheck 🛒 basketcheck.ie`;
  document.getElementById('share-msg-text').textContent=full;
  document.getElementById('share-copy-input').value=short;
  document.getElementById('share-modal').classList.add('open');
}
function closeShareModal(){document.getElementById('share-modal').classList.remove('open');}
function shareToSocial(platform){
  const txt=encodeURIComponent(document.getElementById('share-copy-input').value);
  if(platform==='whatsapp')window.open(`https://wa.me/?text=${txt}`,'_blank');
  else if(platform==='twitter')window.open(`https://twitter.com/intent/tweet?text=${txt}`,'_blank');
  else{copyShareText();alert(`Text copied!\nOpen ${platform==='instagram'?'Instagram':'TikTok'} and paste to your story or post.`);}
}
function copyShareText(){
  const input=document.getElementById('share-copy-input');
  input.select();input.setSelectionRange(0,999);
  try{document.execCommand('copy');}catch(e){}
  const btn=document.getElementById('copy-btn');
  btn.textContent='Copied!';btn.style.background='#085041';
  setTimeout(()=>{btn.textContent='Copy';btn.style.background='var(--teal-400)';},2200);
}
 
// ── INIT ──────────────────────────────────────────────
renderBasket();
</script>
</body>
</html>
