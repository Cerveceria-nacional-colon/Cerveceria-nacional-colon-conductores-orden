<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Cervecería Nacional — Portal RR.HH.</title>
<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700;800&family=Open+Sans:wght@300;400;600&family=DM+Sans:wght@400;500;600;700&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
/* =====================================================
   SHARED VARIABLES & RESET
   ===================================================== */
:root{
  /* Asistencia palette */
  --bg:#f0f4ff;--white:#fff;--ink:#1a1a2e;--ink2:#666;
  --border:#e0e4f0;--accent:#2563eb;--accent-light:#eff6ff;
  --green:#16a34a;--green-light:#f0fdf4;
  --red:#dc2626;--red-light:#fef2f2;
  --yellow:#d97706;--yellow-light:#fffbeb;
  --orange:#ea580c;--orange-light:#fff7ed;
  --purple:#7c3aed;--purple-light:#f5f3ff;
  --shadow:0 2px 12px rgba(37,99,235,0.08);
  --shadow-lg:0 8px 40px rgba(37,99,235,0.12);
  /* CV scanner palette */
  --cv-bg:#f4f6f9;--cv-surface:#fff;--cv-surface2:#eef1f7;
  --cv-border:#d0d8e8;--cv-accent:#003087;--cv-accent2:#0052cc;
  --cv-gold:#F5A623;--cv-gold2:#e8950f;--cv-danger:#d0021b;
  --cv-muted:#5a6a8a;--cv-card-shadow:0 2px 16px rgba(0,48,135,0.08);
}
*{box-sizing:border-box;margin:0;padding:0;}
body{font-family:'DM Sans',sans-serif;background:var(--bg);color:var(--ink);min-height:100vh;overflow-x:hidden;}

/* =====================================================
   PORTAL NAV — selecciona qué sistema mostrar
   ===================================================== */
#portalNav{
  background:var(--cv-accent);
  display:flex;align-items:center;justify-content:space-between;
  padding:0 24px;height:58px;position:sticky;top:0;z-index:200;
  box-shadow:0 2px 12px rgba(0,0,0,0.25);
}
.portal-brand{display:flex;align-items:center;gap:12px;}
.portal-logo{width:34px;height:34px;background:var(--cv-gold);border-radius:8px;
  display:flex;align-items:center;justify-content:center;font-size:18px;}
.portal-name{font-family:'Montserrat',sans-serif;font-size:1rem;font-weight:800;
  color:#fff;letter-spacing:0.04em;text-transform:uppercase;}
.portal-name span{font-weight:400;opacity:0.65;font-size:0.75rem;display:block;margin-top:-2px;}
.nav-tabs{display:flex;gap:4px;}
.nav-tab{padding:8px 18px;border:1.5px solid rgba(255,255,255,0.25);border-radius:8px;
  background:none;color:rgba(255,255,255,0.7);font-family:'Montserrat',sans-serif;
  font-size:0.8rem;font-weight:600;cursor:pointer;transition:all 0.2s;text-transform:uppercase;letter-spacing:0.05em;}
.nav-tab:hover{background:rgba(255,255,255,0.1);color:#fff;}
.nav-tab.active{background:var(--cv-gold);border-color:var(--cv-gold);color:var(--cv-accent);font-weight:700;}
@media(max-width:520px){
  .portal-name span{display:none;}
  .nav-tab{padding:7px 12px;font-size:0.72rem;}
}

/* =====================================================
   SECCION WRAPPERS
   ===================================================== */
.seccion{display:none;}
.seccion.activa{display:block;}


/* =====================================================
   ESCANER DE HOJAS DE VIDA (tu código original)
   ===================================================== */
#secCV{background:var(--cv-bg);min-height:calc(100vh - 58px);}
#secCV body::before{display:none;}
.cv-pattern{
  position:fixed;inset:58px 0 0 0;
  background-image:linear-gradient(rgba(0,48,135,0.025)1px,transparent 1px),linear-gradient(90deg,rgba(0,48,135,0.025)1px,transparent 1px);
  background-size:48px 48px;pointer-events:none;z-index:0;
}
.cv-container{position:relative;z-index:1;max-width:1100px;margin:0 auto;padding:0 24px;}

/* CV header band */
.cv-sub-header{
  background:var(--cv-accent2);padding:10px 24px;text-align:center;
  font-family:'Montserrat',sans-serif;font-size:0.72rem;font-weight:600;
  color:rgba(255,255,255,0.8);letter-spacing:0.12em;text-transform:uppercase;
  margin-bottom:36px;
}

/* Layout */
.cv-layout{display:grid;grid-template-columns:1fr 1fr;gap:24px;align-items:start;}
@media(max-width:768px){.cv-layout{grid-template-columns:1fr;}}

/* Cards */
.cv-card{background:var(--cv-surface);border:1px solid var(--cv-border);border-radius:12px;
  padding:28px;box-shadow:var(--cv-card-shadow);border-top:3px solid var(--cv-accent);}
.cv-card-title{font-family:'Montserrat',sans-serif;font-size:0.9rem;font-weight:700;
  color:var(--cv-accent);text-transform:uppercase;letter-spacing:0.08em;
  margin-bottom:20px;display:flex;align-items:center;gap:10px;}

/* Form */
.cv-label{display:block;font-size:0.75rem;font-weight:600;color:var(--cv-muted);
  margin-bottom:7px;text-transform:uppercase;letter-spacing:0.08em;font-family:'Montserrat',sans-serif;}
.cv-textarea,.cv-input{width:100%;background:var(--cv-surface2);border:1.5px solid var(--cv-border);
  border-radius:8px;color:var(--ink);font-family:'Open Sans',sans-serif;font-size:0.88rem;
  padding:11px 14px;resize:vertical;transition:border-color 0.2s;outline:none;}
.cv-textarea{min-height:120px;}
.cv-textarea:focus,.cv-input:focus{border-color:var(--cv-accent);box-shadow:0 0 0 3px rgba(0,48,135,0.08);}
.cv-form-group{margin-bottom:18px;}

/* Dropzone */
.cv-dropzone{border:2px dashed var(--cv-border);border-radius:10px;padding:28px 20px;
  text-align:center;cursor:pointer;transition:all 0.25s;background:var(--cv-surface2);margin-bottom:14px;}
.cv-dropzone:hover,.cv-dropzone.drag-over{border-color:var(--cv-accent);background:rgba(0,48,135,0.04);}
.cv-dropzone-icon{font-size:2.2rem;margin-bottom:10px;}
.cv-dropzone p{color:var(--cv-muted);font-size:0.83rem;line-height:1.5;}
.cv-dropzone strong{color:var(--cv-accent);}
#cvFileInput{display:none;}

/* File list */
.cv-file-list{display:flex;flex-direction:column;gap:7px;margin-bottom:14px;}
.cv-file-item{background:var(--cv-surface2);border:1px solid var(--cv-border);border-radius:7px;
  padding:9px 13px;display:flex;align-items:center;gap:10px;font-size:0.83rem;}
.cv-file-item .fn{flex:1;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;}
.cv-file-item .fs{color:var(--cv-muted);font-size:0.73rem;}
.cv-file-item .rm{background:none;border:none;color:var(--cv-muted);cursor:pointer;
  font-size:1rem;padding:2px 6px;border-radius:4px;transition:color 0.2s;}
.cv-file-item .rm:hover{color:var(--cv-danger);}

/* CV Button */
.cv-btn-primary{display:inline-flex;align-items:center;gap:8px;padding:14px 24px;border-radius:8px;
  font-family:'Montserrat',sans-serif;font-size:0.85rem;font-weight:700;cursor:pointer;border:none;
  transition:all 0.2s;text-transform:uppercase;letter-spacing:0.06em;width:100%;justify-content:center;
  background:linear-gradient(135deg,var(--cv-gold),var(--cv-gold2));color:var(--cv-accent);
  box-shadow:0 3px 12px rgba(245,166,35,0.3);}
.cv-btn-primary:hover{transform:translateY(-1px);box-shadow:0 6px 20px rgba(245,166,35,0.45);}
.cv-btn-primary:disabled{opacity:0.45;cursor:not-allowed;transform:none;box-shadow:none;}

/* Results */
#cvResults{margin-top:36px;}
.cv-section-div{display:flex;align-items:center;gap:12px;margin:32px 0 20px;}
.cv-section-div span{font-size:0.72rem;color:var(--cv-accent);white-space:nowrap;text-transform:uppercase;
  letter-spacing:0.12em;font-family:'Montserrat',sans-serif;font-weight:700;}
.cv-section-div::before,.cv-section-div::after{content:'';flex:1;height:2px;background:linear-gradient(90deg,var(--cv-border),transparent);}
.cv-section-div::before{background:linear-gradient(90deg,transparent,var(--cv-border));}
.cv-results-header{display:flex;align-items:baseline;justify-content:space-between;margin-bottom:20px;}
.cv-results-header h2{font-family:'Montserrat',sans-serif;font-size:1.1rem;font-weight:800;
  color:var(--cv-accent);text-transform:uppercase;letter-spacing:0.05em;}
.cv-results-count{font-size:0.78rem;color:var(--cv-muted);font-weight:600;}
.cv-candidates-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(300px,1fr));gap:18px;}

/* Candidate card */
.cv-cand-card{background:var(--cv-surface);border:1px solid var(--cv-border);border-radius:12px;
  padding:22px;transition:transform 0.2s,box-shadow 0.2s;animation:fadeUp 0.4s ease forwards;
  opacity:0;border-left:4px solid var(--cv-border);}
.cv-cand-card.card-eligible{border-left-color:#1a9e5c;}
.cv-cand-card.card-review{border-left-color:var(--cv-gold);}
.cv-cand-card.card-not{border-left-color:var(--cv-danger);}
.cv-cand-card:hover{transform:translateY(-3px);box-shadow:0 8px 28px rgba(0,48,135,0.12);}
@keyframes fadeUp{from{opacity:0;transform:translateY(14px);}to{opacity:1;transform:translateY(0);}}
.cv-cand-top{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:14px;}
.cv-cand-name{font-family:'Montserrat',sans-serif;font-size:1rem;font-weight:700;color:var(--cv-accent);}
.cv-cand-file{font-size:0.73rem;color:var(--cv-muted);margin-top:2px;}

/* Badges */
.cv-badge{display:inline-flex;align-items:center;gap:5px;padding:4px 11px;border-radius:100px;
  font-size:0.72rem;font-weight:700;white-space:nowrap;font-family:'Montserrat',sans-serif;
  text-transform:uppercase;letter-spacing:0.04em;}
.badge-eligible{background:rgba(26,158,92,0.1);color:#1a9e5c;border:1px solid rgba(26,158,92,0.3);}
.badge-not-eligible{background:rgba(208,2,27,0.08);color:var(--cv-danger);border:1px solid rgba(208,2,27,0.25);}
.badge-review{background:rgba(245,166,35,0.12);color:#b87800;border:1px solid rgba(245,166,35,0.4);}

/* Score */
.cv-score-section{margin:12px 0;}
.cv-score-label{display:flex;justify-content:space-between;font-size:0.77rem;color:var(--cv-muted);margin-bottom:6px;}
.cv-score-label strong{color:var(--cv-accent);font-size:0.9rem;font-family:'Montserrat',sans-serif;font-weight:700;}
.cv-score-bar{height:6px;background:var(--cv-surface2);border-radius:100px;overflow:hidden;border:1px solid var(--cv-border);}
.cv-score-fill{height:100%;border-radius:100px;transition:width 1s ease;}
.score-high{background:linear-gradient(90deg,#1a9e5c,#2dd17a);}
.score-mid{background:linear-gradient(90deg,var(--cv-gold),#ffd700);}
.score-low{background:linear-gradient(90deg,var(--cv-danger),#ff6b6b);}

/* Skills */
.cv-skills-section{margin-top:12px;}
.cv-skills-section p{font-size:0.7rem;color:var(--cv-muted);margin-bottom:7px;text-transform:uppercase;
  letter-spacing:0.1em;font-family:'Montserrat',sans-serif;font-weight:600;}
.cv-skills-tags{display:flex;flex-wrap:wrap;gap:5px;}
.cv-skill-tag{font-size:0.7rem;padding:3px 9px;border-radius:5px;font-weight:600;}
.skill-match{background:rgba(0,48,135,0.08);color:var(--cv-accent);border:1px solid rgba(0,48,135,0.18);}
.skill-miss{background:rgba(208,2,27,0.06);color:var(--cv-danger);border:1px solid rgba(208,2,27,0.15);text-decoration:line-through;opacity:0.65;}
.cv-summary-text{font-size:0.81rem;color:var(--cv-muted);line-height:1.6;
  border-top:1px solid var(--cv-border);margin-top:12px;padding-top:12px;}
.cv-contact-btn{margin-top:14px;width:100%;background:var(--cv-surface2);border:1.5px solid var(--cv-border);
  color:var(--cv-muted);border-radius:7px;padding:9px;font-family:'Open Sans',sans-serif;
  font-size:0.78rem;font-weight:600;cursor:pointer;transition:all 0.2s;
  display:flex;align-items:center;justify-content:center;gap:6px;}
.cv-contact-btn:hover{border-color:var(--cv-accent2);color:var(--cv-accent2);background:rgba(0,82,204,0.04);}
.cv-contact-btn.eligible-contact{border-color:rgba(26,158,92,0.4);color:#1a9e5c;background:rgba(26,158,92,0.05);}
.cv-contact-btn.eligible-contact:hover{background:rgba(26,158,92,0.1);}

/* Scan progress */
.cv-scan-progress{background:var(--cv-surface);border:1px solid var(--cv-border);border-radius:10px;
  padding:18px 22px;margin-bottom:22px;display:none;box-shadow:var(--cv-card-shadow);}
.cv-scan-progress.active{display:block;}
.cv-progress-label{font-size:0.82rem;color:var(--cv-muted);margin-bottom:10px;font-weight:600;}
.cv-progress-bar{height:5px;background:var(--cv-surface2);border-radius:100px;overflow:hidden;}
.cv-progress-fill{height:100%;background:linear-gradient(90deg,var(--cv-accent),var(--cv-accent2),var(--cv-gold));
  border-radius:100px;transition:width 0.4s ease;animation:progressShimmer 1.5s ease infinite;}
@keyframes progressShimmer{0%,100%{opacity:1;}50%{opacity:0.7;}}
.cv-empty-state{text-align:center;padding:56px 20px;color:var(--cv-muted);}
.cv-empty-state .icon{font-size:2.8rem;margin-bottom:14px;opacity:0.35;}
.cv-empty-state p{font-size:0.88rem;line-height:1.6;}
.cv-spinner{display:inline-block;width:15px;height:15px;border:2px solid rgba(0,48,135,0.2);
  border-top-color:var(--cv-accent);border-radius:50%;animation:spin 0.7s linear infinite;}
@keyframes spin{to{transform:rotate(360deg);}}

/* Sync indicator for CV */
.cv-sync-note{font-size:0.72rem;color:var(--cv-muted);text-align:center;margin-top:10px;font-style:italic;}
.cv-sync-note.ok{color:#1a9e5c;}
.cv-sync-note.err{color:var(--cv-danger);}


/* =====================================================
   ASISTENCIA (tu código original)
   ===================================================== */
#secAsistencia{min-height:calc(100vh - 58px);}

/* Colaborador view */
#vistaColaborador{min-height:calc(100vh - 58px);display:flex;flex-direction:column;align-items:center;justify-content:center;padding:24px 16px;background:linear-gradient(160deg,#eff6ff 0%,#f0fdf4 100%);}
.register-card{background:var(--white);border-radius:24px;padding:32px 26px;width:100%;max-width:400px;box-shadow:var(--shadow-lg);border:1px solid var(--border);}
.brand{display:flex;flex-direction:column;align-items:center;gap:8px;margin-bottom:22px;}
.brand-icon{width:52px;height:52px;background:var(--accent);border-radius:14px;display:flex;align-items:center;justify-content:center;box-shadow:0 4px 14px rgba(37,99,235,0.3);}
.brand-name{font-size:1.1rem;font-weight:700;}
.brand-sub{font-size:0.78rem;color:var(--ink2);margin-top:-4px;}
.hora-badge{display:flex;flex-direction:column;align-items:center;background:var(--accent-light);border:1px solid #bfdbfe;border-radius:12px;padding:10px 16px;margin-bottom:20px;}
.hora-badge .time{font-family:'DM Mono',monospace;font-size:1.5rem;font-weight:500;color:var(--accent);}
.hora-badge .date{font-size:0.76rem;color:var(--ink2);}
.status-banner{border-radius:10px;padding:10px 14px;margin-bottom:16px;font-size:0.82rem;font-weight:600;text-align:center;display:none;}
.banner-orange{background:var(--orange-light);border:1px solid #fed7aa;color:var(--orange);}
.banner-purple{background:var(--purple-light);border:1px solid #ddd6fe;color:var(--purple);}
.field{margin-bottom:14px;}
.field label{display:block;font-size:0.78rem;font-weight:700;color:var(--ink2);margin-bottom:5px;letter-spacing:0.04em;text-transform:uppercase;}
.field input{width:100%;border:2px solid var(--border);border-radius:12px;padding:12px 15px;font-family:'DM Sans',sans-serif;font-size:1rem;color:var(--ink);transition:all 0.2s;}
.field input:focus{outline:none;border-color:var(--accent);box-shadow:0 0 0 3px rgba(37,99,235,0.1);}
.field input::placeholder{color:#bbb;}
.btn-register{width:100%;padding:14px;border:none;border-radius:12px;background:var(--accent);color:#fff;font-family:'DM Sans',sans-serif;font-size:1rem;font-weight:700;cursor:pointer;transition:all 0.2s;box-shadow:0 4px 14px rgba(37,99,235,0.3);}
.btn-register:hover{background:#1d4ed8;transform:translateY(-1px);}
.horario-note{background:var(--yellow-light);border:1px solid #fde68a;border-radius:10px;padding:10px 14px;font-size:0.8rem;color:var(--yellow);margin-top:14px;font-weight:500;text-align:center;}
.result-box{border-radius:12px;padding:14px;margin-top:14px;text-align:center;display:none;}
.result-box.ok{background:var(--green-light);border:1px solid #bbf7d0;color:var(--green);}
.result-box.warn{background:var(--yellow-light);border:1px solid #fde68a;color:var(--yellow);}
.result-box.err{background:var(--red-light);border:1px solid #fecaca;color:var(--red);}
.result-msg{font-size:0.95rem;font-weight:700;}
.result-sub{font-size:0.8rem;margin-top:3px;opacity:0.85;}
.sv-link{margin-top:16px;text-align:center;font-size:0.75rem;}
.sv-link a{color:#aaa;text-decoration:none;}
.sv-link a:hover{color:var(--accent);}

/* Supervisor */
#vistaSupervisor{display:none;min-height:calc(100vh - 58px);background:var(--bg);}
.sv-header{background:var(--white);border-bottom:1px solid var(--border);padding:0 20px;display:flex;align-items:center;justify-content:space-between;height:58px;position:sticky;top:58px;z-index:100;}
.sv-logo{display:flex;align-items:center;gap:8px;font-weight:700;font-size:0.95rem;}
.sv-logo-icon{width:28px;height:28px;background:var(--accent);border-radius:7px;display:flex;align-items:center;justify-content:center;}
#svClock{font-family:'DM Mono',monospace;font-size:0.75rem;color:var(--ink2);}
.btn-out{background:none;border:1px solid var(--border);border-radius:8px;padding:5px 12px;font-family:'DM Sans',sans-serif;font-size:0.78rem;font-weight:600;cursor:pointer;color:var(--ink2);}
.btn-out:hover{border-color:var(--red);color:var(--red);}
.sv-main{max-width:1020px;margin:0 auto;padding:20px 16px;}
.sv-tabs{display:flex;gap:4px;margin-bottom:20px;background:var(--white);border:1px solid var(--border);border-radius:12px;padding:4px;}
.sv-tab{flex:1;padding:9px;border:none;border-radius:9px;font-family:'DM Sans',sans-serif;font-size:0.85rem;font-weight:600;cursor:pointer;color:var(--ink2);background:none;transition:all 0.15s;}
.sv-tab.active{background:var(--accent);color:#fff;}
.sv-panel{display:none;}
.sv-panel.active{display:block;}
/* cronómetro */
.cron-card{background:var(--white);border:1px solid var(--border);border-radius:16px;padding:20px;box-shadow:var(--shadow);margin-bottom:16px;}
.cron-title{font-size:0.68rem;font-weight:700;letter-spacing:0.1em;text-transform:uppercase;color:var(--ink2);margin-bottom:14px;}
.cron-display{text-align:center;padding:10px 0 16px;}
.cron-big{font-family:'DM Mono',monospace;font-size:2.8rem;font-weight:700;color:var(--orange);}
.cron-big.stopped{color:var(--green);}
.cron-label{font-size:0.75rem;color:var(--ink2);margin-top:4px;}
.cron-milestones{display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px;margin-bottom:16px;}
@media(max-width:480px){.cron-milestones{grid-template-columns:1fr;}}
.milestone{border-radius:10px;padding:12px;text-align:center;border:1px solid var(--border);}
.milestone.done{border-color:#bbf7d0;background:var(--green-light);}
.milestone.active{border-color:#fed7aa;background:var(--orange-light);}
.milestone.pending{background:#f9fafb;}
.milestone-icon{font-size:1.3rem;margin-bottom:4px;}
.milestone-label{font-size:0.72rem;font-weight:700;color:var(--ink2);text-transform:uppercase;letter-spacing:0.05em;}
.milestone.done .milestone-label{color:var(--green);}
.milestone.active .milestone-label{color:var(--orange);}
.milestone-time{font-family:'DM Mono',monospace;font-size:0.85rem;font-weight:600;margin-top:3px;color:var(--ink);}
.cron-btns{display:flex;gap:10px;flex-wrap:wrap;}
.btn-cron{flex:1;min-width:140px;padding:12px;border:none;border-radius:10px;font-family:'DM Sans',sans-serif;font-size:0.88rem;font-weight:700;cursor:pointer;transition:all 0.15s;}
.btn-cron:disabled{opacity:0.4;cursor:not-allowed;}
.btn-orange{background:var(--orange);color:#fff;}
.btn-orange:not(:disabled):hover{background:#c2410c;}
.btn-red{background:var(--red);color:#fff;}
.btn-red:not(:disabled):hover{background:#b91c1c;}
.btn-gray{background:var(--white);color:var(--ink2);border:1px solid var(--border);}
.btn-gray:hover{border-color:var(--red);color:var(--red);}
/* conductores */
.control-card{background:var(--white);border:1px solid var(--border);border-radius:16px;padding:20px;box-shadow:var(--shadow);margin-bottom:16px;}
.control-title{font-size:0.68rem;font-weight:700;letter-spacing:0.1em;text-transform:uppercase;color:var(--ink2);margin-bottom:14px;}
.conductores-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(280px,1fr));gap:12px;}
.conductor-card{background:var(--white);border:2px solid var(--border);border-radius:14px;padding:16px;box-shadow:var(--shadow);transition:all 0.2s;}
.conductor-card.verificado{border-color:#bbf7d0;background:var(--green-light);}
.conductor-card.pendiente{border-color:#fed7aa;}
.conductor-header{display:flex;align-items:center;gap:10px;margin-bottom:12px;}
.conductor-avatar{width:38px;height:38px;border-radius:50%;background:var(--accent-light);color:var(--accent);display:flex;align-items:center;justify-content:center;font-weight:700;font-size:0.95rem;flex-shrink:0;}
.conductor-card.verificado .conductor-avatar{background:var(--green-light);color:var(--green);}
.conductor-nombre{font-weight:700;font-size:0.9rem;}
.conductor-status{font-size:0.72rem;color:var(--ink2);margin-top:1px;}
.conductor-card.verificado .conductor-status{color:var(--green);}
.verif-fields{display:flex;gap:8px;margin-bottom:10px;}
.verif-fields input{flex:1;border:1px solid var(--border);border-radius:8px;padding:7px 10px;font-family:'DM Sans',sans-serif;font-size:0.82rem;color:var(--ink);}
.verif-fields input:focus{outline:none;border-color:var(--accent);}
.btn-verif{width:100%;padding:9px;border:none;border-radius:9px;font-family:'DM Sans',sans-serif;font-size:0.85rem;font-weight:700;cursor:pointer;transition:all 0.15s;}
.btn-verif.pendiente{background:var(--orange);color:#fff;}
.btn-verif.pendiente:hover{background:#c2410c;}
.btn-verif.verificado{background:var(--green-light);color:var(--green);border:1px solid #bbf7d0;cursor:default;}
.verif-info{font-size:0.78rem;color:var(--green);margin-top:6px;font-family:'DM Mono',monospace;}
/* stats */
.stats-row{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-bottom:16px;}
@media(max-width:500px){.stats-row{grid-template-columns:1fr 1fr;}}
.stat{background:var(--white);border:1px solid var(--border);border-radius:12px;padding:14px;box-shadow:var(--shadow);}
.stat-n{font-size:0.63rem;font-weight:700;letter-spacing:0.08em;text-transform:uppercase;color:var(--ink2);}
.stat-v{font-size:1.7rem;font-weight:700;margin-top:2px;}
.c-blue{color:var(--accent);}.c-green{color:var(--green);}.c-yellow{color:var(--yellow);}.c-purple{color:var(--purple);}
/* tabla */
.sv-card{background:var(--white);border:1px solid var(--border);border-radius:14px;padding:20px;box-shadow:var(--shadow);}
.sv-card-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:14px;flex-wrap:wrap;gap:8px;}
.sv-card-title{font-size:0.68rem;font-weight:700;letter-spacing:0.1em;text-transform:uppercase;color:var(--ink2);}
.filters{display:flex;gap:8px;margin-bottom:14px;flex-wrap:wrap;}
.filters input,.filters select{flex:1;min-width:110px;border:1px solid var(--border);border-radius:9px;padding:8px 11px;font-family:'DM Sans',sans-serif;font-size:0.83rem;background:var(--white);color:var(--ink);}
.filters input:focus,.filters select:focus{outline:none;border-color:var(--accent);}
.tbl-wrap{overflow-x:auto;}
table{width:100%;border-collapse:collapse;font-size:0.82rem;}
thead th{text-align:left;padding:9px 11px;font-size:0.63rem;font-weight:700;letter-spacing:0.08em;text-transform:uppercase;color:var(--ink2);border-bottom:2px solid var(--border);white-space:nowrap;}
tbody tr{border-bottom:1px solid var(--border);transition:background 0.1s;}
tbody tr:hover{background:var(--bg);}
tbody td{padding:11px 11px;white-space:nowrap;}
.empty{text-align:center;padding:40px;color:var(--ink2);font-size:0.875rem;white-space:normal;}
.pill{display:inline-flex;align-items:center;gap:3px;padding:3px 9px;border-radius:20px;font-size:0.7rem;font-weight:700;}
.pill-green{background:var(--green-light);color:var(--green);border:1px solid #bbf7d0;}
.pill-yellow{background:var(--yellow-light);color:var(--yellow);border:1px solid #fde68a;}
.pill-purple{background:var(--purple-light);color:var(--purple);border:1px solid #ddd6fe;}
.pill-gray{background:#f3f4f6;color:#6b7280;border:1px solid #e5e7eb;}
.pill-orange{background:var(--orange-light);color:var(--orange);border:1px solid #fed7aa;}
.btn-sm{background:none;border:1px solid var(--border);border-radius:8px;padding:6px 13px;font-family:'DM Sans',sans-serif;font-size:0.78rem;font-weight:600;cursor:pointer;color:var(--ink2);transition:all 0.15s;}
.btn-sm:hover{border-color:var(--accent);color:var(--accent);}
.btn-sm.green{background:var(--green);color:#fff;border-color:var(--green);}
.btn-sm.danger{color:var(--red);border-color:#fca5a5;}
/* modal */
.modal-bg{position:fixed;inset:0;background:rgba(0,0,0,0.5);display:flex;align-items:center;justify-content:center;z-index:300;padding:20px;backdrop-filter:blur(6px);}
.modal-bg.hidden{display:none;}
.modal{background:var(--white);border-radius:20px;padding:30px;width:100%;max-width:340px;box-shadow:var(--shadow-lg);animation:popIn 0.2s ease;text-align:center;}
@keyframes popIn{from{transform:scale(0.9);opacity:0;}to{transform:scale(1);opacity:1;}}
.modal-icon{font-size:2.2rem;margin-bottom:10px;}
.modal h3{font-size:1.05rem;font-weight:700;margin-bottom:5px;}
.modal p{font-size:0.82rem;color:var(--ink2);margin-bottom:16px;}
.modal input{width:100%;border:2px solid var(--border);border-radius:10px;padding:11px 14px;font-family:'DM Mono',monospace;font-size:1rem;text-align:center;letter-spacing:0.2em;margin-bottom:6px;}
.modal input:focus{outline:none;border-color:var(--accent);}
.modal-err{color:var(--red);font-size:0.78rem;margin-bottom:10px;display:none;}
.modal-btns{display:flex;gap:8px;}
.modal-btns button{flex:1;padding:11px;border:none;border-radius:10px;font-family:'DM Sans',sans-serif;font-size:0.88rem;font-weight:600;cursor:pointer;}
.mbtn-primary{background:var(--accent);color:#fff;}
.mbtn-cancel{background:var(--border);color:var(--ink2);}
/* toast */
#toast{position:fixed;bottom:20px;right:20px;padding:12px 18px;border-radius:10px;font-size:0.84rem;font-weight:600;box-shadow:var(--shadow-lg);transform:translateY(60px);opacity:0;transition:all 0.25s;z-index:999;color:#fff;max-width:280px;}
#toast.show{transform:translateY(0);opacity:1;}
#toast.ok{background:var(--green);}
#toast.fail{background:var(--red);}
#toast.warn{background:var(--yellow);}
#toast.info{background:var(--accent);}
</style>
</head>
<body>

<!-- ==================== PORTAL NAV ==================== -->
<nav id="portalNav">
  <div class="portal-brand">
    <div class="portal-logo">🍺</div>
    <div class="portal-name">
      Cervecería Nacional
      <span>Portal de Recursos Humanos</span>
    </div>
  </div>
  <div class="nav-tabs">
    <button class="nav-tab active" onclick="mostrarSeccion('secAsistencia',this)">⏱ Asistencia</button>
    <button class="nav-tab" onclick="mostrarSeccion('secCV',this)">📄 Escáner CV</button>
  </div>
</nav>


<!-- ==================== SECCIÓN ASISTENCIA ==================== -->
<div id="secAsistencia" class="seccion activa">

  <!-- COLABORADOR -->
  <div id="vistaColaborador">
    <div class="register-card">
      <div class="brand">
        <div class="brand-icon">
          <svg width="26" height="26" viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="2.2">
            <path d="M17 21v-2a4 4 0 00-4-4H5a4 4 0 00-4 4v2"/>
            <circle cx="9" cy="7" r="4"/>
            <path d="M23 21v-2a4 4 0 00-3-3.87M16 3.13a4 4 0 010 7.75"/>
          </svg>
        </div>
        <div>
          <div class="brand-name">Cervecería Nacional</div>
          <div class="brand-sub">Registro de asistencia</div>
        </div>
      </div>
      <div class="hora-badge">
        <div class="time" id="horaActual">00:00:00</div>
        <div class="date" id="fechaActual">—</div>
      </div>
      <div class="status-banner banner-orange" id="bannerMatinal">🚛 Verificación de camiones en curso</div>
      <div class="status-banner banner-purple" id="bannerVerif">✅ Jornada finalizada</div>
      <div class="field">
        <label>Nombre completo</label>
        <input type="text" id="inputNombre" placeholder="Ej: María González" autocomplete="off">
      </div>
      <div class="field">
        <label>Número OP</label>
        <input type="text" id="inputOP" placeholder="Ej: OP-001" autocomplete="off"
          onkeydown="if(event.key==='Enter') registrar()">
      </div>
      <button class="btn-register" onclick="registrar()">✅ Registrar entrada</button>
      <div class="horario-note">🕖 Entrada: <strong>7:00 AM</strong> · Tolerancia: <strong>5 min</strong></div>
      <div class="result-box" id="resultBox">
        <div class="result-msg" id="resultMsg"></div>
        <div class="result-sub" id="resultSub"></div>
      </div>
      <div class="sv-link"><a href="#" onclick="abrirLogin();return false;">Acceso supervisor / coordinador →</a></div>
    </div>
  </div>

  <!-- SUPERVISOR -->
  <div id="vistaSupervisor">
    <div class="sv-header">
      <div class="sv-logo">
        <div class="sv-logo-icon">
          <svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="2.5">
            <path d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2"/>
            <rect x="9" y="3" width="6" height="4" rx="1"/>
          </svg>
        </div>
        Panel Supervisor
      </div>
      <div id="svClock">—</div>
      <button class="btn-out" onclick="cerrarSesion()">Salir</button>
    </div>
    <div class="sv-main">
      <div class="sv-tabs">
        <button class="sv-tab active" onclick="goSvTab('tiempo',this)">⏱ Tiempo</button>
        <button class="sv-tab" onclick="goSvTab('asistencia',this)">👷 Asistencia</button>
      </div>

      <!-- TAB TIEMPO -->
      <div id="svPanel-tiempo" class="sv-panel active">
        <div class="cron-card">
          <div class="cron-title">⏱ Cronómetro de Jornada</div>
          <div class="cron-display">
            <div class="cron-big" id="cronBig">00:00:00</div>
            <div class="cron-label" id="cronLabel">El cronómetro inicia automáticamente a las 7:00 AM</div>
          </div>
          <div class="cron-milestones">
            <div class="milestone pending" id="ms1">
              <div class="milestone-icon">🕖</div>
              <div class="milestone-label">Inicio (7:00 AM)</div>
              <div class="milestone-time" id="ms1time">—</div>
            </div>
            <div class="milestone pending" id="ms2">
              <div class="milestone-icon">🔔</div>
              <div class="milestone-label">Matinal Finalizada</div>
              <div class="milestone-time" id="ms2time">—</div>
            </div>
            <div class="milestone pending" id="ms3">
              <div class="milestone-icon">🏁</div>
              <div class="milestone-label">Cierre de Jornada</div>
              <div class="milestone-time" id="ms3time">—</div>
            </div>
          </div>
          <div class="cron-btns">
            <button class="btn-cron btn-orange" id="btnMatinal" onclick="finMatinal()" disabled>✅ Matinal Finalizada</button>
            <button class="btn-cron btn-red"    id="btnCierre"  onclick="cerrarJornada()" disabled>🏁 Cerrar Jornada</button>
            <button class="btn-cron btn-gray"   onclick="resetTodo()">🔄 Reiniciar</button>
          </div>
        </div>
        <div class="control-card">
          <div class="control-title">🚛 Verificación de Camiones</div>
          <div class="conductores-grid" id="conductoresGrid"></div>
        </div>
      </div>

      <!-- TAB ASISTENCIA -->
      <div id="svPanel-asistencia" class="sv-panel">
        <div class="stats-row">
          <div class="stat"><div class="stat-n">Total hoy</div><div class="stat-v c-blue"   id="sTotal">0</div></div>
          <div class="stat"><div class="stat-n">A tiempo</div> <div class="stat-v c-green"  id="sTiempo">0</div></div>
          <div class="stat"><div class="stat-n">Tarde</div>    <div class="stat-v c-yellow" id="sTarde">0</div></div>
          <div class="stat"><div class="stat-n">Verificados</div><div class="stat-v c-purple" id="sVerif">0</div></div>
        </div>
        <div class="sv-card">
          <div class="sv-card-header">
            <span class="sv-card-title">Registros de entrada</span>
            <div style="display:flex;gap:8px;flex-wrap:wrap;">
              <button class="btn-sm green"  onclick="exportExcel()">⬇ Exportar Excel</button>
              <button class="btn-sm danger" onclick="clearRecs()">🗑 Limpiar</button>
            </div>
          </div>
          <div class="filters">
            <input type="text" id="fText" placeholder="🔎 Nombre o OP..." oninput="renderTable()">
            <input type="date" id="fDate" oninput="renderTable()">
            <select id="fStatus" onchange="renderTable()">
              <option value="">Todos</option>
              <option value="A tiempo">A tiempo</option>
              <option value="Tarde">Tarde</option>
            </select>
          </div>
          <div class="tbl-wrap">
            <table>
              <thead><tr>
                <th>#</th><th>Nombre</th><th>N° OP</th><th>Entrada</th><th>Estado</th>
                <th>Fin Matinal</th><th>Camión</th><th>Ruta</th><th>Hora Verif.</th><th>Tiempo desde 7AM</th><th>Fecha</th>
              </tr></thead>
              <tbody id="tBody"></tbody>
            </table>
          </div>
        </div>
        <div class="sv-card" style="margin-top:16px;">
          <div class="sv-card-header"><span class="sv-card-title">🚛 Resumen por Conductor</span></div>
          <div class="tbl-wrap">
            <table>
              <thead><tr>
                <th>Conductor</th><th>Camión</th><th>Ruta</th><th>Hora Verificación</th><th>Tiempo desde 7AM</th><th>Estado</th>
              </tr></thead>
              <tbody id="tBodyConductores"></tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</div><!-- fin secAsistencia -->


<!-- ==================== SECCIÓN ESCÁNER CV ==================== -->
<div id="secCV" class="seccion">
  <div class="cv-pattern"></div>
  <div class="cv-sub-header">Gestión del Talento · Selección de Personal</div>
  <div class="cv-container">
    <div class="cv-layout">
      <!-- Vacante -->
      <div class="cv-card">
        <div class="cv-card-title"><span>💼</span> Descripción de la Vacante</div>
        <div class="cv-form-group">
          <label class="cv-label">Nombre del cargo</label>
          <input type="text" class="cv-input" id="jobTitle" placeholder="Ej: Desarrollador Backend Senior">
        </div>
        <div class="cv-form-group">
          <label class="cv-label">Requisitos y descripción del cargo</label>
          <textarea class="cv-textarea" id="jobDesc" rows="8" placeholder="Describe los requisitos del cargo, habilidades técnicas, experiencia mínima, formación académica, responsabilidades, etc.

Ejemplo:
- 3+ años de experiencia en Python o Node.js
- Conocimientos en bases de datos SQL y NoSQL
- Experiencia con AWS o GCP
- Trabajo en equipo y metodologías ágiles
- Título en Ingeniería de Sistemas o afines"></textarea>
        </div>
      </div>
      <!-- Hojas de vida -->
      <div class="cv-card">
        <div class="cv-card-title"><span>📄</span> Hojas de Vida</div>
        <div class="cv-dropzone" id="cvDropzone" onclick="document.getElementById('cvFileInput').click()">
          <div class="cv-dropzone-icon">📂</div>
          <p>Arrastra archivos aquí o <strong>haz clic para seleccionar</strong></p>
          <p style="margin-top:6px;font-size:0.75rem;">Soporta .txt, .pdf (texto), .docx · Máx. 10 archivos</p>
        </div>
        <input type="file" id="cvFileInput" multiple accept=".txt,.pdf,.docx,.doc">
        <div class="cv-file-list" id="cvFileList"></div>
        <button class="cv-btn-primary" id="cvScanBtn" onclick="startScan()" disabled>
          <span class="cv-btn-text">🚀 Iniciar Escaneo</span>
        </button>
        <div class="cv-sync-note" id="cvSyncNote"></div>
      </div>
    </div>

    <!-- Resultados -->
    <div id="cvResults">
      <div class="cv-section-div"><span>Resultados del Análisis</span></div>
      <div class="cv-scan-progress" id="cvScanProgress">
        <div class="cv-progress-label" id="cvProgressLabel">Analizando hoja de vida...</div>
        <div class="cv-progress-bar"><div class="cv-progress-fill" id="cvProgressFill" style="width:0%"></div></div>
      </div>
      <div class="cv-empty-state" id="cvEmptyState">
        <div class="icon">🎯</div>
        <p>Configura la vacante, sube las hojas de vida<br>y haz clic en <strong>Iniciar Escaneo</strong></p>
      </div>
      <div class="cv-results-header" id="cvResultsHeader" style="display:none">
        <h2>Candidatos Evaluados</h2>
        <div class="cv-results-count" id="cvResultsCount"></div>
      </div>
      <div class="cv-candidates-grid" id="cvCandidatesGrid"></div>
    </div>
    <br><br>
  </div>
</div><!-- fin secCV -->


<!-- Modal Login -->
<div id="modalLogin" class="modal-bg hidden">
  <div class="modal">
    <div class="modal-icon">🔐</div>
    <h3>Acceso Supervisor</h3>
    <p>Ingresa la clave para continuar</p>
    <input type="password" id="claveInput" placeholder="••••••" maxlength="20"
      onkeydown="if(event.key==='Enter') verificarClave()">
    <div id="claveError" class="modal-err">Clave incorrecta</div>
    <div class="modal-btns">
      <button class="mbtn-cancel" onclick="cerrarModal()">Cancelar</button>
      <button class="mbtn-primary" onclick="verificarClave()">Entrar</button>
    </div>
  </div>
</div>

<div id="toast"></div>

<script>
// ╔══════════════════════════════════════════════════════════════╗
// ║  REEMPLAZA ESTA URL CON LA URL DE TU APPS SCRIPT DESPLEGADO ║
// ╚══════════════════════════════════════════════════════════════╝
const APPS_SCRIPT_URL = 'https://script.google.com/macros/s/AKfycbzaQy-jm1-1j0gbFK4otrU_SK3XdXuuN9tu0OmrV3t6z_HGr1vVUGpo-HNzsWNjg25hAA/exec';

// ============================================================
//  PORTAL NAV
// ============================================================
function mostrarSeccion(id, btn) {
  document.querySelectorAll('.seccion').forEach(s => s.classList.remove('activa'));
  document.querySelectorAll('.nav-tab').forEach(b => b.classList.remove('active'));
  document.getElementById(id).classList.add('activa');
  btn.classList.add('active');
}


// ============================================================
//  ASISTENCIA — CONFIG
// ============================================================
const HORA_ENTRADA   = 7;
const TOLERANCIA_MIN = 5;
const CLAVE          = '1234';
const CONDUCTORES    = [
  'Jonathan Perea','Pedro Ulloa','Martín Clark',
  'Humberto Vásquez','William De Gracia','Jaime Hernández',
  'Juan Ruiz','Fredy Campos','Ernesto Escobar'
];

// Reset diario
(function checkDailyReset(){
  const hoy = new Date().toDateString();
  const ult  = localStorage.getItem('att_ultimo_dia');
  if(ult && ult !== hoy){ localStorage.removeItem('att_jornada'); localStorage.removeItem('att_verifs'); }
  localStorage.setItem('att_ultimo_dia', hoy);
})();

let records = JSON.parse(localStorage.getItem('att_recs')    || '[]');
let jornada = JSON.parse(localStorage.getItem('att_jornada') || 'null');
let verifs  = JSON.parse(localStorage.getItem('att_verifs')  || '{}');

function saveRecs()    { localStorage.setItem('att_recs',    JSON.stringify(records)); }
function saveJornada() { localStorage.setItem('att_jornada', JSON.stringify(jornada)); }
function saveVerifs()  { localStorage.setItem('att_verifs',  JSON.stringify(verifs)); }

// Relojes
setInterval(tickAll, 1000); tickAll();
function tickAll(){
  const n = new Date();
  const h = n.toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit',second:'2-digit'});
  const d = n.toLocaleDateString('es-MX',{weekday:'long',day:'numeric',month:'long'});
  document.getElementById('horaActual').textContent = h;
  document.getElementById('fechaActual').textContent = d.charAt(0).toUpperCase()+d.slice(1);
  document.getElementById('svClock').textContent =
    n.toLocaleDateString('es',{weekday:'short',day:'2-digit',month:'short'})+' · '+h;
  if(!jornada && n.getHours()===HORA_ENTRADA && n.getMinutes()===0){
    const inicio=new Date(n); inicio.setSeconds(0,0);
    jornada={inicioTs:inicio.toISOString(),matinalTs:null,cierreTs:null,tiempoTotal:null};
    saveJornada(); syncCronUI();
  }
  if(jornada){
    const inicio=new Date(jornada.inicioTs);
    const fin=jornada.cierreTs?new Date(jornada.cierreTs):n;
    const diff=Math.floor((fin-inicio)/1000);
    const el=document.getElementById('cronBig');
    el.textContent=formatSeg(diff);
    el.className='cron-big'+(jornada.cierreTs?' stopped':'');
  }
}
function formatSeg(s){
  return [Math.floor(s/3600),Math.floor((s%3600)/60),s%60].map(v=>v.toString().padStart(2,'0')).join(':');
}
function getEstado(d){ return d.getHours()*60+d.getMinutes()<=HORA_ENTRADA*60+TOLERANCIA_MIN?'A tiempo':'Tarde'; }
function getRetraso(d){ return Math.max(0,d.getHours()*60+d.getMinutes()-(HORA_ENTRADA*60+TOLERANCIA_MIN)); }

// Login
function abrirLogin(){
  document.getElementById('claveInput').value='';
  document.getElementById('claveError').style.display='none';
  document.getElementById('modalLogin').classList.remove('hidden');
  setTimeout(()=>document.getElementById('claveInput').focus(),200);
}
function cerrarModal(){ document.getElementById('modalLogin').classList.add('hidden'); }
function verificarClave(){
  if(document.getElementById('claveInput').value===CLAVE){ cerrarModal(); abrirSupervisor(); }
  else{ document.getElementById('claveError').style.display='block'; document.getElementById('claveInput').value=''; }
}
function abrirSupervisor(){
  document.getElementById('vistaColaborador').style.display='none';
  document.getElementById('vistaSupervisor').style.display='block';
  syncCronUI(); renderConductores(); renderTable(); renderConductoresTable(); updateStats();
}
function cerrarSesion(){
  document.getElementById('vistaSupervisor').style.display='none';
  document.getElementById('vistaColaborador').style.display='flex';
}
function goSvTab(id,btn){
  document.querySelectorAll('.sv-panel').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.sv-tab').forEach(b=>b.classList.remove('active'));
  document.getElementById('svPanel-'+id).classList.add('active');
  btn.classList.add('active');
  if(id==='asistencia'){ renderTable(); renderConductoresTable(); updateStats(); }
  if(id==='tiempo'){ syncCronUI(); renderConductores(); }
}

// ── REGISTRAR — ahora envía a Google Sheets ──────────────────
async function registrar(){
  const nombre=document.getElementById('inputNombre').value.trim();
  const op=document.getElementById('inputOP').value.trim();
  if(!nombre){ mostrarRes('err','⚠️ Falta tu nombre','Escribe tu nombre completo'); return; }
  if(!op)    { mostrarRes('err','⚠️ Falta el N° OP','Escribe tu número OP'); return; }
  const now=new Date(), hoy=now.toDateString();
  const yaMarcó=records.find(r=>r.op.toLowerCase()===op.toLowerCase()&&new Date(r.ts).toDateString()===hoy);
  if(yaMarcó){ mostrarRes('warn','⚠️ Ya registraste hoy','Entrada a las '+yaMarcó.time); return; }
  if(!jornada&&now.getHours()===HORA_ENTRADA){
    const inicio=new Date(now); inicio.setMinutes(0); inicio.setSeconds(0,0);
    jornada={inicioTs:inicio.toISOString(),matinalTs:null,cierreTs:null,tiempoTotal:null};
    saveJornada(); syncCronUI();
  }
  const estado=getEstado(now), retraso=getRetraso(now);
  const time=now.toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit',second:'2-digit'});
  const date=now.toLocaleDateString('es-MX');
  const rec={id:Date.now(),nombre,op:op.toUpperCase(),estado,retraso,date,time,ts:now.toISOString()};
  records.unshift(rec); saveRecs();
  if(estado==='A tiempo') mostrarRes('ok','✅ ¡Entrada registrada!',`Bienvenido/a ${nombre} · ${time}`);
  else mostrarRes('warn',`⚠️ Tarde ${retraso} min`,`${nombre} · ${time}`);
  document.getElementById('inputNombre').value='';
  document.getElementById('inputOP').value='';
  // Enviar a Google Sheets (sin bloquear UI)
  try {
    const p=new URLSearchParams({action:'add',nombre,op:op.toUpperCase(),estado,retraso,time,date});
    await fetch(APPS_SCRIPT_URL+'?'+p.toString());
  } catch(e){ console.warn('No se pudo enviar a Sheets:',e); }
}

function mostrarRes(tipo,msg,sub){
  const b=document.getElementById('resultBox');
  b.className='result-box '+tipo; b.style.display='block';
  document.getElementById('resultMsg').textContent=msg;
  document.getElementById('resultSub').textContent=sub;
  clearTimeout(window._rt);
  window._rt=setTimeout(()=>b.style.display='none',5000);
}

// Cronómetro
function finMatinal(){
  if(!jornada){ toast('El cronómetro aún no ha iniciado (7:00 AM)','warn'); return; }
  if(jornada.matinalTs){ toast('Matinal ya fue registrada','warn'); return; }
  if(!confirm('¿Confirmas que la matinal ha finalizado?')) return;
  jornada.matinalTs=new Date().toISOString();
  saveJornada(); syncCronUI(); toast('✅ Matinal finalizada · Cronómetro sigue corriendo','ok');
}
function cerrarJornada(){
  if(!jornada){ toast('El cronómetro aún no ha iniciado','warn'); return; }
  if(jornada.cierreTs){ toast('La jornada ya fue cerrada','warn'); return; }
  if(!confirm('¿Confirmas el cierre de jornada? El cronómetro se detendrá.')) return;
  const now=new Date(), inicio=new Date(jornada.inicioTs);
  jornada.cierreTs=now.toISOString();
  jornada.tiempoTotal=formatSeg(Math.floor((now-inicio)/1000));
  saveJornada(); syncCronUI();
  document.getElementById('bannerMatinal').style.display='none';
  document.getElementById('bannerVerif').style.display='block';
  toast('🏁 Jornada cerrada · Tiempo total: '+jornada.tiempoTotal,'ok');
  renderConductoresTable(); renderTable();
}
function syncCronUI(){
  const btnM=document.getElementById('btnMatinal'),btnC=document.getElementById('btnCierre');
  const label=document.getElementById('cronLabel');
  const ms1=document.getElementById('ms1'),ms2=document.getElementById('ms2'),ms3=document.getElementById('ms3');
  if(!jornada){
    label.textContent='El cronómetro inicia automáticamente a las 7:00 AM';
    btnM.disabled=true; btnC.disabled=true;
    [ms1,ms2,ms3].forEach(m=>{m.className='milestone pending';});
    document.getElementById('ms1time').textContent='—';
    document.getElementById('ms2time').textContent='—';
    document.getElementById('ms3time').textContent='—';
    document.getElementById('bannerMatinal').style.display='none';
    document.getElementById('bannerVerif').style.display='none';
    return;
  }
  ms1.className='milestone done';
  document.getElementById('ms1time').textContent=new Date(jornada.inicioTs).toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit',second:'2-digit'});
  if(jornada.matinalTs){
    ms2.className='milestone done';
    document.getElementById('ms2time').textContent=new Date(jornada.matinalTs).toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit',second:'2-digit'});
    btnM.disabled=true;
  } else { ms2.className='milestone active'; document.getElementById('ms2time').textContent='En curso...'; btnM.disabled=false; }
  if(jornada.cierreTs){
    ms3.className='milestone done';
    document.getElementById('ms3time').textContent=new Date(jornada.cierreTs).toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit',second:'2-digit'});
    btnC.disabled=true;
    label.textContent='✅ Jornada cerrada · Tiempo total: '+jornada.tiempoTotal;
  } else {
    ms3.className='milestone active'; document.getElementById('ms3time').textContent='Pendiente';
    btnC.disabled=false;
    label.textContent=jornada.matinalTs?'🚛 Verificando camiones — cronómetro corriendo':'⏳ Esperando fin de matinal — cronómetro corriendo';
  }
  document.getElementById('bannerMatinal').style.display=(!jornada.cierreTs)?'block':'none';
  document.getElementById('bannerVerif').style.display=jornada.cierreTs?'block':'none';
}
function resetTodo(){
  if(!confirm('¿Reiniciar cronómetro y verificaciones? Los registros de asistencia NO se borran.')) return;
  jornada=null; verifs={}; saveJornada(); saveVerifs();
  syncCronUI(); renderConductores(); updateStats(); renderConductoresTable();
  toast('🔄 Reiniciado','info');
}

// Conductores
function renderConductores(){
  const grid=document.getElementById('conductoresGrid');
  const hab=jornada&&!jornada.cierreTs;
  grid.innerHTML=CONDUCTORES.map(nombre=>{
    const v=verifs[nombre];
    const ini=nombre.split(' ').map(p=>p[0]).join('').slice(0,2).toUpperCase();
    if(v) return `<div class="conductor-card verificado"><div class="conductor-header"><div class="conductor-avatar">${ini}</div><div><div class="conductor-nombre">${nombre}</div><div class="conductor-status">✅ Verificado</div></div></div><div class="verif-info">🚛 ${v.camion} &nbsp;·&nbsp; 📍 ${v.ruta}<br>⏰ ${v.horaVerif} &nbsp;·&nbsp; ⏱ Tiempo: ${v.tiempoDesde7}</div></div>`;
    const dis=!hab?'disabled':'';
    return `<div class="conductor-card pendiente"><div class="conductor-header"><div class="conductor-avatar">${ini}</div><div><div class="conductor-nombre">${nombre}</div><div class="conductor-status" style="color:var(--orange);">⏳ Pendiente</div></div></div><div class="verif-fields"><input type="text" placeholder="N° Camión" id="camion-${san(nombre)}" ${dis}><input type="text" placeholder="Ruta" id="ruta-${san(nombre)}" ${dis}></div><button class="btn-verif pendiente" ${dis} onclick="verificarConductor('${nombre}')">✅ Marcar verificado</button>${!hab?'<div style="font-size:0.72rem;color:#aaa;margin-top:6px;text-align:center;">Disponible cuando inicie la jornada</div>':''}</div>`;
  }).join('');
}
function san(n){ return n.replace(/\s+/g,'-').replace(/[^a-zA-Z0-9-]/g,''); }
function verificarConductor(nombre){
  if(!jornada){ toast('El cronómetro no ha iniciado','fail'); return; }
  const camion=document.getElementById('camion-'+san(nombre))?.value.trim();
  const ruta=document.getElementById('ruta-'+san(nombre))?.value.trim();
  if(!camion){ toast('Ingresa el número de camión','fail'); return; }
  if(!ruta)  { toast('Ingresa la ruta','fail'); return; }
  const now=new Date(), inicio=new Date(jornada.inicioTs);
  verifs[nombre]={camion,ruta,horaVerif:now.toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit',second:'2-digit'}),tiempoDesde7:formatSeg(Math.floor((now-inicio)/1000)),ts:now.toISOString()};
  saveVerifs(); renderConductores(); updateStats(); renderConductoresTable();
  toast('✅ '+nombre+' verificado','ok');
}

// Tablas
function renderTable(){
  const ft=document.getElementById('fText').value.toLowerCase();
  const fd=document.getElementById('fDate').value;
  const fs=document.getElementById('fStatus').value;
  const filtered=records.filter(r=>{
    return (!ft||r.nombre.toLowerCase().includes(ft)||r.op.toLowerCase().includes(ft))&&
           (!fd||r.ts.startsWith(fd))&&(!fs||r.estado===fs);
  });
  const body=document.getElementById('tBody');
  if(!filtered.length){ body.innerHTML=`<tr><td colspan="11" class="empty">Sin registros</td></tr>`; return; }
  body.innerHTML=filtered.map((r,i)=>{
    const pill=r.estado==='A tiempo'?`<span class="pill pill-green">✅ A tiempo</span>`:`<span class="pill pill-yellow">⚠️ Tarde ${r.retraso}m</span>`;
    const fm=jornada?.matinalTs?new Date(jornada.matinalTs).toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit'}):'—';
    const esC=CONDUCTORES.find(c=>c.toLowerCase()===r.nombre.toLowerCase());
    const v=esC?verifs[esC]:null;
    return `<tr><td style="color:var(--ink2);font-family:'DM Mono',monospace;font-size:0.73rem;">${i+1}</td><td><strong>${r.nombre}</strong></td><td style="font-family:'DM Mono',monospace;font-size:0.78rem;color:var(--accent);">${r.op}</td><td style="font-family:'DM Mono',monospace;font-size:0.82rem;font-weight:600;color:var(--green);">${r.time}</td><td>${pill}</td><td style="font-family:'DM Mono',monospace;font-size:0.78rem;">${fm}</td><td style="font-size:0.8rem;">${v?v.camion:'—'}</td><td style="font-size:0.8rem;">${v?v.ruta:'—'}</td><td style="font-family:'DM Mono',monospace;font-size:0.78rem;">${v?v.horaVerif:'—'}</td><td>${v?`<span class="pill pill-purple">⏱ ${v.tiempoDesde7}</span>`:'—'}</td><td style="font-family:'DM Mono',monospace;font-size:0.75rem;color:var(--ink2);">${r.date}</td></tr>`;
  }).join('');
}
function renderConductoresTable(){
  const body=document.getElementById('tBodyConductores');
  body.innerHTML=CONDUCTORES.map(nombre=>{
    const v=verifs[nombre];
    return v?`<tr><td><strong>${nombre}</strong></td><td style="font-family:'DM Mono',monospace;">${v.camion}</td><td>${v.ruta}</td><td style="font-family:'DM Mono',monospace;">${v.horaVerif}</td><td><span class="pill pill-purple">⏱ ${v.tiempoDesde7}</span></td><td><span class="pill pill-green">✅ Verificado</span></td></tr>`:`<tr><td><strong>${nombre}</strong></td><td>—</td><td>—</td><td>—</td><td>—</td><td><span class="pill pill-orange">⏳ Pendiente</span></td></tr>`;
  }).join('');
}
function updateStats(){
  const hoy=new Date().toDateString();
  const hoyR=records.filter(r=>new Date(r.ts).toDateString()===hoy);
  document.getElementById('sTotal').textContent=hoyR.length;
  document.getElementById('sTiempo').textContent=hoyR.filter(r=>r.estado==='A tiempo').length;
  document.getElementById('sTarde').textContent=hoyR.filter(r=>r.estado==='Tarde').length;
  document.getElementById('sVerif').textContent=Object.keys(verifs).length;
}
function clearRecs(){
  if(!confirm('¿Borrar TODOS los registros?')) return;
  records=[]; saveRecs(); renderTable(); updateStats(); toast('Registros eliminados','fail');
}
function exportExcel(){
  if(!records.length){ toast('No hay registros','fail'); return; }
  const BOM='\uFEFF';
  let csv=BOM+'REGISTRO DE ASISTENCIA · CERVECERÍA NACIONAL\n';
  if(jornada){
    csv+=`Inicio jornada:,${new Date(jornada.inicioTs).toLocaleTimeString('es-MX')},`;
    csv+=`Fin matinal:,${jornada.matinalTs?new Date(jornada.matinalTs).toLocaleTimeString('es-MX'):'—'},`;
    csv+=`Cierre:,${jornada.cierreTs?new Date(jornada.cierreTs).toLocaleTimeString('es-MX'):'—'},`;
    csv+=`Tiempo total:,${jornada.tiempoTotal||'—'}\n\n`;
  }
  csv+=['#','Nombre','N° OP','Hora Entrada','Estado','Min Retraso','Fin Matinal','Camión','Ruta','Hora Verificación','Tiempo desde 7AM','Fecha'].join(',')+'\n';
  records.forEach((r,i)=>{
    const fm=jornada?.matinalTs?new Date(jornada.matinalTs).toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit'}):'';
    const esC=CONDUCTORES.find(c=>c.toLowerCase()===r.nombre.toLowerCase());
    const v=esC?verifs[esC]:null;
    csv+=[i+1,`"${r.nombre}"`,r.op,r.time,r.estado,r.retraso||0,fm,v?v.camion:'',v?v.ruta:'',v?v.horaVerif:'',v?v.tiempoDesde7:'',r.date].join(',')+'\n';
  });
  const blob=new Blob([csv],{type:'text/csv;charset=utf-8;'});
  const a=document.createElement('a'); a.download=`Asistencia_${new Date().toLocaleDateString('es-MX').replace(/\//g,'-')}.csv`; a.href=URL.createObjectURL(blob); a.click();
  toast('✅ Excel exportado','ok');
}

// ============================================================
//  ESCÁNER CV — tu código original + envío a Google Sheets
// ============================================================
let uploadedFiles = [];

document.getElementById('cvDropzone').addEventListener('dragover', e=>{e.preventDefault();document.getElementById('cvDropzone').classList.add('drag-over');});
document.getElementById('cvDropzone').addEventListener('dragleave', ()=>document.getElementById('cvDropzone').classList.remove('drag-over'));
document.getElementById('cvDropzone').addEventListener('drop', e=>{
  e.preventDefault(); document.getElementById('cvDropzone').classList.remove('drag-over');
  handleFiles(Array.from(e.dataTransfer.files));
});
document.getElementById('cvFileInput').addEventListener('change', e=>{
  handleFiles(Array.from(e.target.files)); e.target.value='';
});

function handleFiles(files){
  const allowed=files.filter(f=>/\.(txt|pdf|docx|doc)$/i.test(f.name));
  if(allowed.length<files.length) toast('⚠️ Solo se permiten archivos .txt, .pdf y .docx','warn');
  allowed.forEach(f=>{
    if(uploadedFiles.find(u=>u.file.name===f.name)) return;
    if(uploadedFiles.length>=10){ toast('Máximo 10 hojas de vida','warn'); return; }
    uploadedFiles.push({file:f,id:Date.now()+Math.random()});
  });
  renderCVFileList();
}
function renderCVFileList(){
  const list=document.getElementById('cvFileList');
  list.innerHTML=uploadedFiles.map(u=>`<div class="cv-file-item"><span>📄</span><span class="fn">${u.file.name}</span><span class="fs">${(u.file.size/1024).toFixed(1)} KB</span><button class="rm" onclick="removeCVFile('${u.id}')">✕</button></div>`).join('');
  document.getElementById('cvScanBtn').disabled=uploadedFiles.length===0;
}
function removeCVFile(id){ uploadedFiles=uploadedFiles.filter(u=>String(u.id)!==String(id)); renderCVFileList(); }

async function readFile(file){
  return new Promise(resolve=>{
    if(file.type==='application/pdf'){
      const r=new FileReader();
      r.onload=()=>{
        const text=r.result;
        const extracted=text.replace(/[^\x20-\x7E\n\r\t áéíóúñÁÉÍÓÚÑüÜ]/g,' ').replace(/\s{3,}/g,'\n').trim();
        resolve(extracted.length>100?extracted:`[Archivo PDF: ${file.name}]`);
      };
      r.readAsBinaryString(file);
    } else {
      const r=new FileReader();
      r.onload=()=>resolve(r.result);
      r.readAsText(file,'UTF-8');
    }
  });
}

async function startScan(){
  const jobTitle=document.getElementById('jobTitle').value.trim();
  const jobDesc=document.getElementById('jobDesc').value.trim();
  if(!jobDesc){ toast('⚠️ Por favor describe la vacante','warn'); return; }
  if(uploadedFiles.length===0){ toast('⚠️ Sube al menos una hoja de vida','warn'); return; }
  document.getElementById('cvEmptyState').style.display='none';
  document.getElementById('cvResultsHeader').style.display='none';
  document.getElementById('cvCandidatesGrid').innerHTML='';
  document.getElementById('cvScanProgress').classList.add('active');
  document.getElementById('cvScanBtn').disabled=true;
  document.getElementById('cvScanBtn').innerHTML='<span class="cv-spinner"></span> &nbsp;Analizando...';
  document.getElementById('cvSyncNote').textContent='';
  const results=[];
  for(let i=0;i<uploadedFiles.length;i++){
    const{file}=uploadedFiles[i];
    document.getElementById('cvProgressFill').style.width=Math.round((i/uploadedFiles.length)*100)+'%';
    document.getElementById('cvProgressLabel').textContent=`Analizando: ${file.name} (${i+1} de ${uploadedFiles.length})...`;
    const cvText=await readFile(file);
    const result=await analyzeCV(file.name,cvText,jobTitle,jobDesc);
    results.push(result);
    renderCVCard(result,i);
    // ── Guardar en Google Sheets ──────────────────────────────
    await guardarCandidatoEnSheets(result, jobTitle);
  }
  document.getElementById('cvProgressFill').style.width='100%';
  setTimeout(()=>document.getElementById('cvScanProgress').classList.remove('active'),600);
  const eligible=results.filter(r=>r.status==='eligible').length;
  const review=results.filter(r=>r.status==='review').length;
  document.getElementById('cvResultsHeader').style.display='flex';
  document.getElementById('cvResultsCount').textContent=`${eligible} elegible(s) · ${review} en revisión · ${results.length-eligible-review} no elegible(s)`;
  document.getElementById('cvScanBtn').disabled=false;
  document.getElementById('cvScanBtn').innerHTML='<span class="cv-btn-text">🔄 Escanear de Nuevo</span>';
  toast(`✅ Análisis completo: ${results.length} candidato(s) evaluado(s)`,'ok');
}

// ── Guardar candidato en Google Sheets ─────────────────────
async function guardarCandidatoEnSheets(r, puesto) {
  const note = document.getElementById('cvSyncNote');
  try {
    const params = new URLSearchParams({
      action:           'addCV',
      nombre:           r.name           || '',
      email:            r.contact_email  || '',
      puesto:           puesto            || '',
      score:            r.score          || 0,
      estado:           r.status         || '',
      habilidades_match:(r.matched_skills||[]).join(', '),
      habilidades_falta:(r.missing_skills||[]).join(', '),
      resumen:          r.summary        || '',
      contacto_email:   r.contact_email  || '',
      contacto_tel:     r.contact_phone  || '',
      archivo:          r.filename       || ''
    });
    await fetch(APPS_SCRIPT_URL + '?' + params.toString());
    note.textContent = '✅ Candidatos guardados en Google Sheets';
    note.className = 'cv-sync-note ok';
  } catch(e) {
    note.textContent = '⚠️ No se pudo sincronizar con Sheets (revisa la URL del script)';
    note.className = 'cv-sync-note err';
  }
}

async function analyzeCV(filename,cvText,jobTitle,jobDesc){
  const prompt=`Eres un experto en Recursos Humanos. Analiza la siguiente hoja de vida para la vacante indicada y responde SOLO con JSON, sin texto adicional ni backticks.

VACANTE: ${jobTitle||'No especificado'}
DESCRIPCIÓN DE LA VACANTE:
${jobDesc}

CONTENIDO DE LA HOJA DE VIDA (archivo: ${filename}):
${cvText.substring(0,3000)}

Responde ÚNICAMENTE con este JSON (sin markdown, sin backticks):
{
  "name": "Nombre completo del candidato (si no se encuentra, usa el nombre del archivo sin extensión)",
  "status": "eligible" | "review" | "not_eligible",
  "score": número del 0 al 100,
  "matched_skills": ["skill1", "skill2"],
  "missing_skills": ["skill3", "skill4"],
  "summary": "Resumen breve de 2-3 oraciones sobre el candidato y su idoneidad para el cargo.",
  "contact_email": "email si aparece en la hoja de vida, sino null",
  "contact_phone": "teléfono si aparece, sino null"
}

Criterios:
- "eligible": score >= 70
- "review": score entre 45-69
- "not_eligible": score < 45`;

  try {
    const response=await fetch("https://api.anthropic.com/v1/messages",{
      method:"POST",
      headers:{"Content-Type":"application/json"},
      body:JSON.stringify({model:"claude-sonnet-4-20250514",max_tokens:1000,messages:[{role:"user",content:prompt}]})
    });
    const data=await response.json();
    const raw=data.content.map(b=>b.text||'').join('').trim();
    const parsed=JSON.parse(raw.replace(/```json|```/g,'').trim());
    parsed.filename=filename;
    return parsed;
  } catch(err) {
    return {name:filename.replace(/\.(pdf|docx?|txt)$/i,'').replace(/[-_]/g,' '),filename,status:'review',score:50,matched_skills:[],missing_skills:[],summary:'No se pudo analizar este archivo. Revísalo manualmente.',contact_email:null,contact_phone:null};
  }
}

function renderCVCard(r,idx){
  const grid=document.getElementById('cvCandidatesGrid');
  const delay=idx*120;
  const badgeClass=r.status==='eligible'?'badge-eligible':r.status==='review'?'badge-review':'badge-not-eligible';
  const badgeLabel=r.status==='eligible'?'✅ Elegible':r.status==='review'?'⚠️ Revisar':'❌ No Elegible';
  const scoreClass=r.score>=70?'score-high':r.score>=45?'score-mid':'score-low';
  const matchedTags=(r.matched_skills||[]).slice(0,6).map(s=>`<span class="cv-skill-tag skill-match">${s}</span>`).join('');
  const missingTags=(r.missing_skills||[]).slice(0,4).map(s=>`<span class="cv-skill-tag skill-miss">${s}</span>`).join('');
  const contactInfo=r.contact_email||r.contact_phone?`📧 ${r.contact_email||''} ${r.contact_phone?'· 📞 '+r.contact_phone:''}`:'📋 Ver hoja de vida para contacto';
  const card=document.createElement('div');
  card.className='cv-cand-card '+(r.status==='eligible'?'card-eligible':r.status==='review'?'card-review':'card-not');
  card.style.animationDelay=delay+'ms';
  card.innerHTML=`<div class="cv-cand-top"><div><div class="cv-cand-name">${r.name||'Candidato'}</div><div class="cv-cand-file">${r.filename}</div></div><span class="cv-badge ${badgeClass}">${badgeLabel}</span></div><div class="cv-score-section"><div class="cv-score-label"><span>Compatibilidad</span><strong>${r.score}%</strong></div><div class="cv-score-bar"><div class="cv-score-fill ${scoreClass}" style="width:0%" data-target="${r.score}"></div></div></div>${matchedTags||missingTags?`<div class="cv-skills-section"><p>Habilidades</p><div class="cv-skills-tags">${matchedTags}${missingTags}</div></div>`:''}<p class="cv-summary-text">${r.summary}</p><button class="cv-contact-btn ${r.status==='eligible'?'eligible-contact':''}" onclick="copyCVContact('${r.contact_email||''}','${r.contact_phone||''}','${r.name}')">${contactInfo}</button>`;
  grid.appendChild(card);
  setTimeout(()=>{const fill=card.querySelector('.cv-score-fill');if(fill)fill.style.width=fill.dataset.target+'%';},delay+200);
}
function copyCVContact(email,phone,name){
  const info=[name,email,phone].filter(Boolean).join(' · ');
  if(info) navigator.clipboard.writeText(info).then(()=>toast('📋 Info copiada al portapapeles','ok'));
  else toast('ℹ️ No hay datos de contacto en la hoja de vida','info');
}

// ============================================================
//  TOAST UNIFICADO
// ============================================================
function toast(msg,type='ok'){
  const t=document.getElementById('toast');
  t.textContent=msg; t.className='show '+type;
  clearTimeout(t._t); t._t=setTimeout(()=>t.className='',3500);
}

// Init
syncCronUI();
</script>
</body>
</html>
