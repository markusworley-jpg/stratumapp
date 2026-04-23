<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0,viewport-fit=cover,user-scalable=no">
<meta name="theme-color" content="#0a0a0a">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="STRATUM">
<link rel="manifest" href="manifest.json">
<link rel="apple-touch-icon" href="icon-192.png">
<title>STRATUM</title>
<style>
:root{--font:'Inter',-apple-system,BlinkMacSystemFont,sans-serif;--mono:'SF Mono','JetBrains Mono',Menlo,monospace;--accent:#3b82f6;--accent-b:#60a5fa;--accent-g:rgba(59,130,246,0.15);--ok:#10b981;--ok-bg:rgba(16,185,129,0.12);--bad:#ef4444;--bad-bg:rgba(239,68,68,0.12);--warn:#f59e0b;--warn-bg:rgba(245,158,11,0.12);--sw:240px;--r4:4px;--r6:6px;--r10:10px;--r14:14px;--r20:20px;--ease:cubic-bezier(.16,1,.3,1);--fast:150ms;--med:260ms;--slow:400ms;}
[data-theme="charcoal"]{--bg:#0a0a0a;--bg1:#141414;--bg2:#1c1c1c;--bgh:#242424;--bga:#2c2c2c;--br:rgba(255,255,255,.06);--brS:rgba(255,255,255,.1);--t1:#f5f5f5;--t2:#a8a8a8;--t3:#6e6e6e;--t4:#4a4a4a;--sh:0 8px 32px rgba(0,0,0,.4);}
[data-theme="navy"]{--bg:#0d1117;--bg1:#161b22;--bg2:#1c232e;--bgh:#242c3a;--bga:#2d3644;--br:rgba(255,255,255,.07);--brS:rgba(255,255,255,.12);--t1:#f0f6fc;--t2:#9ba7b8;--t3:#6a7383;--t4:#444d5c;--sh:0 8px 32px rgba(0,0,0,.5);}
[data-theme="oled"]{--bg:#000;--bg1:#0a0a0a;--bg2:#121212;--bgh:#1a1a1a;--bga:#222;--br:rgba(255,255,255,.08);--brS:rgba(255,255,255,.14);--t1:#fff;--t2:#b0b0b0;--t3:#707070;--t4:#424242;--sh:0 8px 32px rgba(0,0,0,.8);}
[data-theme="warm"]{--bg:#12100e;--bg1:#1c1814;--bg2:#25201b;--bgh:#2f2924;--bga:#39322c;--br:rgba(255,220,180,.06);--brS:rgba(255,220,180,.1);--t1:#f5ede0;--t2:#a89d8b;--t3:#6e6558;--t4:#4a4238;--sh:0 8px 32px rgba(0,0,0,.5);}
[data-theme="light-gray"]{--bg:#f2f2f0;--bg1:#fff;--bg2:#e8e8e6;--bgh:#ebebea;--bga:#dedede;--br:rgba(0,0,0,.08);--brS:rgba(0,0,0,.14);--t1:#1a1a1a;--t2:#555;--t3:#888;--t4:#bbb;--sh:0 4px 24px rgba(0,0,0,.08);}
[data-theme="light-warm"]{--bg:#f5f0e8;--bg1:#fdfaf4;--bg2:#ede8df;--bgh:#e8e2d8;--bga:#ddd7cc;--br:rgba(120,90,40,.1);--brS:rgba(120,90,40,.18);--t1:#1e1a14;--t2:#5a5040;--t3:#8a7a65;--t4:#c0b090;--sh:0 4px 24px rgba(80,60,20,.1);}
[data-theme="light-white"]{--bg:#f8f8f8;--bg1:#fff;--bg2:#f0f0f0;--bgh:#f4f4f4;--bga:#e8e8e8;--br:rgba(0,0,0,.1);--brS:rgba(0,0,0,.18);--t1:#000;--t2:#444;--t3:#888;--t4:#ccc;--sh:0 2px 16px rgba(0,0,0,.06);}
[data-theme="light-sky"]{--bg:#edf1f7;--bg1:#f8fafd;--bg2:#e2e8f2;--bgh:#dce4f0;--bga:#d0daec;--br:rgba(60,90,140,.1);--brS:rgba(60,90,140,.18);--t1:#111827;--t2:#374151;--t3:#6b7280;--t4:#9ca3af;--sh:0 4px 24px rgba(60,90,140,.1);}
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;}
html,body{height:100%;overflow-x:hidden;}
body{font-family:var(--font);font-size:15px;line-height:1.5;color:var(--t1);background:var(--bg);-webkit-font-smoothing:antialiased;letter-spacing:-.01em;transition:background var(--med) var(--ease),color var(--med) var(--ease);padding-top:env(safe-area-inset-top);}
button{font-family:inherit;font-size:inherit;background:none;border:none;color:inherit;cursor:pointer;}
input,textarea,select{font-family:inherit;font-size:inherit;color:inherit;}
::-webkit-scrollbar{width:6px;height:6px;}
::-webkit-scrollbar-thumb{background:var(--brS);border-radius:3px;}
/* BRAND */
.brand{display:inline-flex;align-items:center;gap:10px;user-select:none;}
.brand-mark{width:28px;height:28px;}
.brand-wm{font-weight:800;font-size:18px;letter-spacing:.14em;}
/* AUTH */
.auth-screen{position:fixed;inset:0;display:flex;align-items:center;justify-content:center;background:var(--bg);z-index:100;opacity:0;pointer-events:none;transition:opacity var(--slow) var(--ease);overflow:hidden;}
.auth-screen.active{opacity:1;pointer-events:auto;}
.auth-bg{position:absolute;inset:0;overflow:hidden;pointer-events:none;}
.auth-grid{position:absolute;inset:-50%;background-image:linear-gradient(var(--brS) 1px,transparent 1px),linear-gradient(90deg,var(--brS) 1px,transparent 1px);background-size:80px 80px;opacity:.4;mask-image:radial-gradient(ellipse at center,black 0%,transparent 70%);-webkit-mask-image:radial-gradient(ellipse at center,black 0%,transparent 70%);}
.auth-glow{position:absolute;width:800px;height:800px;top:50%;left:50%;transform:translate(-50%,-50%);background:radial-gradient(circle,var(--accent-g) 0%,transparent 60%);filter:blur(40px);animation:apulse 8s ease-in-out infinite;}
@keyframes apulse{0%,100%{opacity:.4;transform:translate(-50%,-50%) scale(1);}50%{opacity:.7;transform:translate(-50%,-50%) scale(1.1);}}
.auth-panel{position:relative;width:100%;max-width:440px;padding:48px 40px;margin:0 20px;background:var(--bg1);border:1px solid var(--br);border-radius:var(--r20);box-shadow:var(--sh);z-index:1;animation:arise 600ms var(--ease) both;}
@keyframes arise{from{opacity:0;transform:translateY(16px);}to{opacity:1;transform:translateY(0);}}
/* FIELDS */
.field{display:flex;flex-direction:column;gap:6px;}
.lbl{font-size:11px;font-weight:600;color:var(--t3);letter-spacing:.08em;text-transform:uppercase;}
.inp,.sel,.ta{width:100%;padding:13px 14px;background:var(--bg);border:1px solid var(--br);border-radius:var(--r10);color:var(--t1);font-size:15px;transition:all var(--fast) var(--ease);}
.inp:focus,.sel:focus,.ta:focus{outline:none;border-color:var(--accent);background:var(--bg2);box-shadow:0 0 0 3px var(--accent-g);}
.inp::placeholder,.ta::placeholder{color:var(--t4);}
.sel{appearance:none;cursor:pointer;background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' fill='none' stroke='%236e6e6e' stroke-width='2' viewBox='0 0 24 24'%3E%3Cpath d='M6 9l6 6 6-6'/%3E%3C/svg%3E");background-repeat:no-repeat;background-position:right 14px center;}
.ta{font-size:14px;line-height:1.6;resize:vertical;min-height:90px;}
/* BUTTONS */
.btn{display:inline-flex;align-items:center;justify-content:center;gap:8px;padding:13px 18px;border-radius:var(--r10);font-size:14px;font-weight:600;cursor:pointer;transition:all var(--fast) var(--ease);border:1px solid transparent;white-space:nowrap;}
.btn-p{background:var(--accent);color:#fff;}.btn-p:hover{background:var(--accent-b);transform:translateY(-1px);box-shadow:0 4px 12px var(--accent-g);}
.btn-g{background:transparent;color:var(--t2);border:1px solid var(--br);}.btn-g:hover{background:var(--bgh);color:var(--t1);}
.btn-s{background:var(--ok);color:#fff;}.btn-s:hover{background:#0e9e6e;transform:translateY(-1px);}
.btn-d{background:var(--bad-bg);color:var(--bad);}.btn-d:hover{background:var(--bad);color:#fff;}
.btn-bl{width:100%;}.btn-sm{padding:8px 14px;font-size:13px;}.btn-xs{padding:6px 10px;font-size:12px;}
.auth-msg{font-size:12px;text-align:center;padding:10px;border-radius:var(--r6);margin-top:8px;display:none;}
.auth-msg.show{display:block;}.auth-msg.err{background:var(--bad-bg);color:var(--bad);}.auth-msg.inf{background:var(--accent-g);color:var(--accent-b);}
/* APP SHELL */
.app{display:none;min-height:100dvh;}
.app.on{display:flex;}
.sidebar{width:var(--sw);background:var(--bg1);border-right:1px solid var(--br);display:flex;flex-direction:column;position:sticky;top:0;height:100dvh;flex-shrink:0;padding-top:env(safe-area-inset-top);}
.sb-hd{padding:24px 20px 20px;border-bottom:1px solid var(--br);}
.sb-nav{flex:1;padding:16px 12px;overflow-y:auto;display:flex;flex-direction:column;gap:2px;}
.nav-sec{font-size:10px;font-weight:600;color:var(--t4);letter-spacing:.12em;text-transform:uppercase;padding:16px 12px 8px;}
.nav-it{display:flex;align-items:center;gap:12px;padding:10px 12px;border-radius:var(--r10);color:var(--t2);font-size:14px;font-weight:500;cursor:pointer;transition:all var(--fast) var(--ease);position:relative;border:1px solid transparent;}
.nav-it:hover{background:var(--bgh);color:var(--t1);}
.nav-it.on{background:var(--bg2);color:var(--t1);border-color:var(--br);}
.nav-it.on::before{content:'';position:absolute;left:-12px;top:50%;transform:translateY(-50%);width:3px;height:20px;background:var(--accent);border-radius:0 2px 2px 0;}
.nav-ic{width:18px;height:18px;display:flex;align-items:center;justify-content:center;flex-shrink:0;}
.nav-ic svg{width:18px;height:18px;}
.sb-ft{padding:16px 12px;border-top:1px solid var(--br);}
.prof-chip{display:flex;align-items:center;gap:10px;padding:10px;border-radius:var(--r10);cursor:pointer;transition:background var(--fast) var(--ease);}
.prof-chip:hover{background:var(--bgh);}
.prof-av{width:32px;height:32px;border-radius:50%;background:var(--accent);display:flex;align-items:center;justify-content:center;font-size:13px;font-weight:700;color:#fff;flex-shrink:0;}
.prof-nm{font-size:13px;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.prof-sub{font-size:11px;color:var(--t3);}
/* MAIN */
.main{flex:1;min-width:0;overflow-x:hidden;}
.main-hd{position:sticky;top:0;padding-top:env(safe-area-inset-top);background:color-mix(in oklab,var(--bg) 80%,transparent);backdrop-filter:blur(24px);-webkit-backdrop-filter:blur(24px);border-bottom:1px solid var(--br);z-index:20;}
.main-hd-in{padding:18px 32px;display:flex;align-items:center;justify-content:space-between;gap:16px;}
.pg-sub{font-size:11px;color:var(--t3);letter-spacing:.1em;text-transform:uppercase;font-weight:600;}
.pg-ttl{font-size:20px;font-weight:700;letter-spacing:-.02em;}
.icon-btn{width:36px;height:36px;border-radius:var(--r10);display:flex;align-items:center;justify-content:center;background:var(--bg1);border:1px solid var(--br);color:var(--t2);transition:all var(--fast) var(--ease);}
.icon-btn:hover{background:var(--bgh);color:var(--t1);}
.icon-btn svg{width:16px;height:16px;}
.main-body{padding:32px;max-width:1280px;margin:0 auto;}
/* BOTTOM TABS */
.btabs{display:none;position:fixed;bottom:0;left:0;right:0;background:color-mix(in oklab,var(--bg1) 92%,transparent);backdrop-filter:blur(24px);-webkit-backdrop-filter:blur(24px);border-top:1px solid var(--br);padding:8px 0 calc(8px + env(safe-area-inset-bottom));z-index:50;}
.btabs-in{display:grid;grid-template-columns:repeat(6,1fr);padding:0 4px;gap:2px;}
.tab-it{display:flex;flex-direction:column;align-items:center;gap:4px;padding:8px 4px;border-radius:var(--r10);color:var(--t3);transition:color var(--fast) var(--ease);}
.tab-it.on{color:var(--accent);}
.tab-it svg{width:22px;height:22px;}
.tab-lbl{font-size:10px;font-weight:600;}
/* SECTIONS */
.sec{display:none;}
.sec.on{display:block;animation:fadeup var(--med) var(--ease) both;}
@keyframes fadeup{from{opacity:0;transform:translateY(4px);}to{opacity:1;transform:translateY(0);}}
/* HERO */
.hero{background:linear-gradient(135deg,var(--bg1),var(--bg2));border:1px solid var(--br);border-radius:var(--r20);padding:32px;margin-bottom:24px;position:relative;overflow:hidden;}
.hero::before{content:'';position:absolute;top:0;right:0;width:200px;height:200px;background:radial-gradient(circle,var(--accent-g) 0%,transparent 70%);pointer-events:none;}
.hero-lbl{font-size:11px;color:var(--accent-b);letter-spacing:.12em;text-transform:uppercase;font-weight:700;margin-bottom:12px;}
.hero-ttl{font-size:28px;font-weight:700;letter-spacing:-.02em;margin-bottom:6px;}
.hero-sub{color:var(--t2);font-size:14px;max-width:560px;}
.hero-cta{margin-top:20px;display:flex;gap:10px;flex-wrap:wrap;}
.hero-row{margin-bottom:12px;display:flex;align-items:center;gap:8px;flex-wrap:wrap;}
.h-badge{display:inline-flex;align-items:center;font-size:12px;font-weight:600;padding:4px 12px;border-radius:20px;}
.h-badge.cut{background:var(--bad-bg);color:var(--bad);}
.h-badge.bulk{background:var(--ok-bg);color:var(--ok);}
.h-badge.maintain{background:var(--accent-g);color:var(--accent-b);}
.h-trend{display:inline-flex;align-items:center;font-size:11px;font-weight:600;padding:3px 8px;border-radius:10px;}
.h-trend.ok{background:var(--ok-bg);color:var(--ok);}
.h-trend.drift{background:var(--warn-bg);color:var(--warn);}
.h-trend.off{background:var(--bad-bg);color:var(--bad);}
.goal-bar-wrap{margin-top:16px;}
.goal-bar-hd{display:flex;justify-content:space-between;font-size:12px;color:var(--t2);margin-bottom:6px;}
.goal-bar-tr{height:6px;background:var(--bga);border-radius:3px;overflow:hidden;}
.goal-bar{height:100%;border-radius:3px;background:var(--accent);transition:width .6s var(--ease);}
.hero-stats{display:flex;gap:28px;margin-top:20px;flex-wrap:wrap;}
.hs-val{font-size:22px;font-weight:700;letter-spacing:-.02em;font-variant-numeric:tabular-nums;}
.hs-lbl{font-size:11px;color:var(--t3);margin-top:2px;}
/* STAT CARDS */
.stat-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:12px;margin-bottom:24px;}
.stat-c{background:var(--bg1);border:1px solid var(--br);border-radius:var(--r14);padding:18px 20px;}
.stat-lbl{font-size:11px;color:var(--t3);letter-spacing:.08em;text-transform:uppercase;font-weight:600;margin-bottom:6px;}
.stat-val{font-size:28px;font-weight:700;letter-spacing:-.03em;font-variant-numeric:tabular-nums;line-height:1.1;}
.stat-sub{font-size:12px;color:var(--t3);margin-top:4px;}
.c-ok{color:var(--ok);}.c-bad{color:var(--bad);}
/* CARDS */
.card{background:var(--bg1);border:1px solid var(--br);border-radius:var(--r14);padding:24px;margin-bottom:16px;}
.card-hd{display:flex;align-items:center;justify-content:space-between;margin-bottom:20px;gap:12px;flex-wrap:wrap;}
.card-ttl{font-size:16px;font-weight:600;letter-spacing:-.01em;}
.card-sub{font-size:12px;color:var(--t3);margin-top:2px;}
/* GRID / ROW */
.fg{display:grid;grid-template-columns:1fr 1fr;gap:16px;}
.fg .ff{grid-column:1/-1;}
.fr{display:flex;gap:12px;align-items:flex-end;flex-wrap:wrap;}
.fr .field{flex:1;min-width:140px;}
/* DATE STEPPER */
.dstep{display:flex;align-items:center;gap:4px;}
.stbtn{width:38px;height:46px;border-radius:var(--r10);display:flex;align-items:center;justify-content:center;background:var(--bg);border:1px solid var(--br);color:var(--t2);flex-shrink:0;font-size:16px;font-weight:600;transition:all var(--fast) var(--ease);}
.stbtn:hover:not(:disabled){background:var(--bgh);color:var(--t1);}
.stbtn:disabled{opacity:.3;cursor:not-allowed;}
.stbtn.today{width:auto;padding:0 10px;font-size:11px;font-weight:700;letter-spacing:.05em;}
.stbtn.today.is-today{background:var(--accent);color:#fff;border-color:var(--accent);}
.dstep .inp{flex:1;text-align:center;}
/* MONTH GROUPS */
.mg{margin-bottom:8px;}
.mg-hd{display:flex;align-items:center;justify-content:space-between;padding:8px 14px;background:var(--bg2);border-radius:var(--r6);cursor:pointer;user-select:none;transition:background var(--fast) var(--ease);}
.mg-hd:hover{background:var(--bgh);}
.mg-ttl{font-size:12px;font-weight:700;color:var(--t2);letter-spacing:.04em;}
.mg-meta{font-size:11px;color:var(--t4);}
.mg-chev{font-size:10px;color:var(--t4);transition:transform var(--fast) var(--ease);margin-left:8px;}
.mg-chev.open{transform:rotate(180deg);}
.mg-body{display:none;border:1px solid var(--br);border-radius:var(--r6);overflow:hidden;margin-top:2px;}
.mg-body.open{display:block;}
/* WI ROWS */
.wi-row{display:flex;align-items:center;justify-content:space-between;padding:12px 16px;border-top:1px solid var(--br);transition:background var(--fast) var(--ease);}
.wi-row:first-child{border-top:none;}
.wi-row:hover{background:var(--bgh);}
.wi-date{font-size:14px;font-weight:500;}
.wi-day{font-size:11px;color:var(--t3);margin-left:8px;}
.wi-val{font-size:16px;font-weight:600;font-variant-numeric:tabular-nums;}
.wi-del{width:28px;height:28px;border-radius:var(--r4);display:flex;align-items:center;justify-content:center;color:var(--t4);transition:all var(--fast) var(--ease);margin-left:8px;font-size:18px;line-height:1;}
.wi-del:hover{color:var(--bad);background:var(--bad-bg);}
.bulk-tag{display:inline-block;font-size:9px;font-weight:700;color:var(--warn);background:var(--warn-bg);padding:1px 5px;border-radius:6px;margin-left:6px;letter-spacing:.04em;vertical-align:middle;}
/* MACRO */
.mac-tog{display:flex;background:var(--bg);border:1px solid var(--br);border-radius:var(--r4);padding:3px;width:fit-content;}
.mac-btn{padding:6px 14px;font-size:12px;font-weight:600;border-radius:4px;transition:background var(--fast) var(--ease);color:var(--t2);}
.mac-btn.on{background:var(--bg2);color:var(--t1);}
.mac-bar{display:flex;height:8px;border-radius:4px;overflow:hidden;background:var(--bg);margin-top:10px;}
.mac-seg{transition:width var(--med) var(--ease);}
.mac-p{background:var(--accent);}.mac-c{background:var(--ok);}.mac-f{background:var(--warn);}
.mac-leg{display:flex;gap:16px;margin-top:8px;font-size:11px;color:var(--t2);flex-wrap:wrap;}
.mac-dot{width:8px;height:8px;border-radius:2px;display:inline-block;margin-right:4px;vertical-align:middle;}
/* LOG TABS */
.ltabs{display:flex;gap:8px;margin-bottom:20px;flex-wrap:wrap;}
.ltab{padding:10px 20px;font-size:13px;font-weight:600;color:var(--t3);border:1px solid var(--br);border-radius:var(--r10);transition:all var(--fast) var(--ease);}
.ltab.on{background:var(--bg2);color:var(--t1);border-color:var(--accent);}
.ltab:hover:not(.on){background:var(--bgh);}
.lpanel{display:none;}
.lpanel.on{display:block;}
/* SCORE */
.spill{display:inline-flex;align-items:center;font-size:12px;font-weight:700;padding:2px 8px;border-radius:20px;}
.sg{background:var(--ok-bg);color:var(--ok);}
.sb2{background:var(--accent-g);color:var(--accent-b);}
.so{background:var(--warn-bg);color:var(--warn);}
.sl{background:var(--bad-bg);color:var(--bad);}
/* CALENDAR */
.cal-hd{display:flex;align-items:center;justify-content:space-between;margin-bottom:16px;}
.cal-ttl{font-size:16px;font-weight:600;}
.cal-nav{display:flex;gap:4px;}
.cal-nb{width:32px;height:32px;border-radius:var(--r4);display:flex;align-items:center;justify-content:center;border:1px solid var(--br);color:var(--t2);transition:all var(--fast) var(--ease);}
.cal-nb:hover{background:var(--bgh);}
.cal-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:4px;}
.cal-dl{text-align:center;font-size:10px;font-weight:600;color:var(--t4);letter-spacing:.08em;text-transform:uppercase;padding:8px 0;}
.cal-cell{aspect-ratio:1;border-radius:var(--r4);display:flex;flex-direction:column;align-items:center;justify-content:center;font-size:13px;font-weight:500;color:var(--t3);position:relative;border:1px solid transparent;}
.cal-cell.click{cursor:pointer;transition:all var(--fast) var(--ease);}
.cal-cell.click:hover{background:var(--bgh);}
.cal-cell.today{border-color:var(--accent);color:var(--t1);}
.cal-cell.has{color:var(--t1);background:var(--bg2);}
.cal-cell.has::after{content:'';width:4px;height:4px;border-radius:50%;background:var(--accent);position:absolute;bottom:4px;}
.cal-cell.other{opacity:.3;}
.cal-cell.fut{opacity:.25;cursor:not-allowed;}
.cal-wt{font-size:9px;color:var(--t3);font-variant-numeric:tabular-nums;margin-top:1px;}
/* PHASES */
.ph-list{display:flex;flex-direction:column;gap:8px;}
.ph-item{display:flex;align-items:center;justify-content:space-between;padding:16px 20px;background:var(--bg1);border:1px solid var(--br);border-radius:var(--r14);gap:16px;}
.ph-item.cur{border-color:var(--accent);box-shadow:0 0 0 3px var(--accent-g);}
.ph-item.done{opacity:.6;}
.ph-main{flex:1;min-width:0;}
.ph-name{font-size:15px;font-weight:600;margin-bottom:4px;display:flex;align-items:center;gap:8px;flex-wrap:wrap;}
.ph-meta{font-size:12px;color:var(--t3);}
.ph-goal{font-size:12px;color:var(--t2);margin-top:2px;}
.ph-cal{font-size:18px;font-weight:700;color:var(--accent-b);white-space:nowrap;font-variant-numeric:tabular-nums;}
.ph-cal span{font-size:11px;font-weight:500;color:var(--t4);margin-left:2px;}
.ph-acts{display:flex;gap:4px;flex-wrap:wrap;}
.badge{display:inline-block;padding:2px 8px;font-size:10px;font-weight:700;letter-spacing:.08em;text-transform:uppercase;border-radius:4px;}
.bc-cut{background:var(--bad-bg);color:var(--bad);}
.bc-bulk{background:var(--ok-bg);color:var(--ok);}
.bc-maintain{background:var(--accent-g);color:var(--accent-b);}
.bc-active{background:var(--accent);color:#fff;}
.bc-done{background:var(--ok-bg);color:var(--ok);}
/* HISTORY */
.hfbar{display:flex;gap:8px;margin-bottom:16px;flex-wrap:wrap;}
.hpreset{font-size:12px;font-weight:600;padding:6px 14px;border-radius:20px;border:1px solid var(--br);color:var(--t2);transition:all var(--fast) var(--ease);}
.hpreset.on{background:var(--accent);color:#fff;border-color:var(--accent);}
.hpreset:hover:not(.on){background:var(--bgh);color:var(--t1);}
.hcust{display:none;gap:8px;align-items:flex-end;flex-wrap:wrap;padding:8px 0;}
.psec{margin-bottom:12px;border:1px solid var(--br);border-radius:var(--r14);overflow:hidden;}
.psec-hd{display:flex;align-items:center;justify-content:space-between;padding:14px 20px;background:var(--bg2);cursor:pointer;transition:background var(--fast) var(--ease);}
.psec-hd:hover{background:var(--bgh);}
.psec-ttl{font-size:15px;font-weight:600;}
.psec-meta{font-size:12px;color:var(--t3);margin-top:2px;}
.pchev{font-size:11px;color:var(--t4);transition:transform var(--fast) var(--ease);}
.pchev.open{transform:rotate(180deg);}
.psec-body{display:none;border-top:1px solid var(--br);}
.psec-body.open{display:block;}
.tl-item{display:flex;gap:16px;padding:13px 20px;border-bottom:1px solid var(--br);cursor:pointer;transition:background var(--fast) var(--ease);align-items:center;}
.tl-item:hover{background:var(--bgh);}
.tl-item:last-child{border-bottom:none;}
.tl-wk{font-size:12px;font-weight:700;color:var(--accent-b);width:48px;flex-shrink:0;}
.tl-lbl{font-size:13px;font-weight:500;}
.tl-dt{font-size:11px;color:var(--t3);}
.tl-r{display:flex;align-items:center;gap:10px;flex-shrink:0;}
.tl-wv{font-size:14px;font-weight:600;font-variant-numeric:tabular-nums;}
.tl-d{font-size:12px;font-weight:600;font-variant-numeric:tabular-nums;min-width:42px;text-align:right;}
/* ACHIEVEMENTS */
.ach-grid{display:flex;flex-direction:column;gap:6px;}
.ach-item{display:flex;align-items:center;gap:14px;padding:14px 18px;border:1px solid var(--br);border-radius:var(--r14);}
.ach-item.earn{border-color:var(--ok);}
.ach-item.earn.maj{border-color:var(--warn);}
.ach-ic{width:36px;height:36px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:16px;flex-shrink:0;background:var(--bg2);color:var(--t4);}
.ach-ic.earn{background:var(--ok-bg);color:var(--ok);}
.ach-ic.maj{background:var(--warn-bg);color:var(--warn);}
.ach-meta{flex:1;min-width:0;}
.ach-nm{font-size:14px;font-weight:600;}
.ach-desc{font-size:12px;color:var(--t3);margin-top:2px;}
.ach-r{margin-left:auto;text-align:right;flex-shrink:0;}
.ach-date{font-size:12px;color:var(--ok);font-weight:600;}
.ach-prog{font-size:12px;color:var(--t3);}
.ach-pbar{height:3px;background:var(--bga);border-radius:2px;overflow:hidden;margin-top:4px;width:80px;}
.ach-pfill{height:100%;border-radius:2px;background:var(--accent);}
/* TREND INTERPRETATION */
.trend-card{background:var(--bg1);border:1px solid var(--br);border-radius:var(--r14);padding:20px 24px;margin-bottom:16px;}
.trend-card-lbl{font-size:10px;font-weight:700;color:var(--t3);letter-spacing:.15em;text-transform:uppercase;margin-bottom:10px;}
.trend-read{font-size:14px;color:var(--t2);line-height:1.75;}
.trend-read strong{color:var(--t1);font-weight:600;}
.trend-conf{display:inline-block;font-size:10px;font-weight:600;letter-spacing:.06em;text-transform:uppercase;padding:2px 8px;border-radius:10px;margin-left:8px;vertical-align:middle;}
.trend-conf.high{background:var(--ok-bg);color:var(--ok);}
.trend-conf.med{background:var(--accent-g);color:var(--accent-b);}
.trend-conf.low{background:var(--warn-bg);color:var(--warn);}
.trend-conf.none{background:var(--bga);color:var(--t4);}
/* MEASUREMENTS */
.meas-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(160px,1fr));gap:10px;margin-bottom:20px;}
.meas-field{display:flex;flex-direction:column;gap:6px;}
.meas-row{display:flex;align-items:center;justify-content:space-between;padding:13px 16px;border-top:1px solid var(--br);transition:background var(--fast) var(--ease);}
.meas-row:first-child{border-top:none;}
.meas-row:hover{background:var(--bgh);}
.meas-lbl{font-size:12px;color:var(--t3);font-weight:500;}
.meas-val{font-size:14px;font-weight:600;font-variant-numeric:tabular-nums;}
.meas-delta{font-size:11px;font-weight:600;padding:2px 7px;border-radius:10px;margin-left:8px;}
.meas-delta.pos{background:var(--ok-bg);color:var(--ok);}
.meas-delta.neg{background:var(--bad-bg);color:var(--bad);}
.meas-delta.neu{background:var(--bga);color:var(--t3);}
.meas-entry{background:var(--bg1);border:1px solid var(--br);border-radius:var(--r14);overflow:hidden;margin-bottom:8px;}
.meas-entry-hd{display:flex;align-items:center;justify-content:space-between;padding:12px 16px;background:var(--bg2);}
.meas-entry-date{font-size:13px;font-weight:600;}
.meas-entry-body{padding:4px 0;}
/* PHASE COMPARISON */
.cmp-grid{display:grid;grid-template-columns:1fr 1fr;gap:0;border:1px solid var(--br);border-radius:var(--r14);overflow:hidden;margin-bottom:16px;}
.cmp-hd{padding:14px 18px;background:var(--bg2);font-size:13px;font-weight:600;}
.cmp-hd.a{border-right:1px solid var(--br);}
.cmp-cell{padding:12px 18px;border-top:1px solid var(--br);font-size:13px;font-variant-numeric:tabular-nums;}
.cmp-cell.a{border-right:1px solid var(--br);}
.cmp-lbl{font-size:11px;color:var(--t3);font-weight:600;letter-spacing:.06em;text-transform:uppercase;padding:10px 18px 4px;border-top:1px solid var(--br);grid-column:1/-1;background:var(--bg2);}
.cmp-win{color:var(--ok);font-weight:700;}
.cmp-neu{color:var(--t3);}
/* PROGRESS PHOTOS */
.photo-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(140px,1fr));gap:10px;padding:4px 0;}
.photo-thumb{position:relative;aspect-ratio:3/4;border-radius:var(--r10);overflow:hidden;cursor:pointer;border:2px solid transparent;transition:border-color var(--fast) var(--ease);}
.photo-thumb:hover{border-color:var(--accent);}
.photo-thumb.sel{border-color:var(--accent);box-shadow:0 0 0 3px var(--accent-g);}
.photo-thumb img{width:100%;height:100%;object-fit:cover;display:block;}
.photo-thumb-meta{position:absolute;bottom:0;left:0;right:0;padding:6px 8px;background:linear-gradient(transparent,rgba(0,0,0,.7));font-size:10px;color:#fff;font-weight:600;}
.photo-del{position:absolute;top:5px;right:5px;width:22px;height:22px;border-radius:50%;background:rgba(0,0,0,.6);color:#fff;display:flex;align-items:center;justify-content:center;font-size:14px;opacity:0;transition:opacity var(--fast) var(--ease);cursor:pointer;border:none;}
.photo-thumb:hover .photo-del{opacity:1;}
.photo-compare{display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-top:16px;}
.photo-compare img{width:100%;border-radius:var(--r10);object-fit:cover;max-height:420px;}
.photo-compare-lbl{font-size:12px;color:var(--t3);text-align:center;margin-top:6px;}
.cel-ov{position:fixed;inset:0;z-index:300;display:flex;align-items:center;justify-content:center;background:rgba(0,0,0,.7);opacity:0;pointer-events:none;transition:opacity var(--med) var(--ease);}
.cel-ov.on{opacity:1;pointer-events:auto;}
.cel-c{background:var(--bg1);border:2px solid var(--warn);border-radius:var(--r20);padding:40px;text-align:center;max-width:380px;width:90%;transform:scale(.9);transition:transform var(--slow) var(--ease);}
.cel-ov.on .cel-c{transform:scale(1);}
.cel-ic{font-size:48px;margin-bottom:16px;}
.cel-ttl{font-size:24px;font-weight:800;letter-spacing:-.02em;margin-bottom:8px;}
.cel-sub{font-size:14px;color:var(--t2);}
/* TEMPLATE TOGGLES */
.tpl-row{display:flex;align-items:center;justify-content:space-between;padding:14px 20px;border-bottom:1px solid var(--br);gap:16px;}
.tpl-row:last-child{border-bottom:none;}
.tpl-ttl{font-size:14px;font-weight:500;}
.tpl-sub{font-size:12px;color:var(--t3);margin-top:2px;}
.tpl-lock{font-size:11px;color:var(--t4);}
.tog{width:42px;height:24px;background:var(--bga);border-radius:12px;position:relative;cursor:pointer;transition:background var(--fast) var(--ease);flex-shrink:0;}
.tog::after{content:'';position:absolute;top:3px;left:3px;width:18px;height:18px;background:var(--t1);border-radius:50%;transition:all var(--fast) var(--ease);}
.tog.on{background:var(--accent);}
.tog.on::after{left:21px;background:#fff;}
/* MODAL */
.m-ov{position:fixed;inset:0;background:rgba(0,0,0,.6);backdrop-filter:blur(8px);-webkit-backdrop-filter:blur(8px);z-index:100;display:flex;align-items:center;justify-content:center;padding:20px;opacity:0;pointer-events:none;transition:opacity var(--med) var(--ease);}
.m-ov.open{opacity:1;pointer-events:auto;}
.modal{background:var(--bg1);border:1px solid var(--br);border-radius:var(--r20);padding:28px;max-width:560px;width:100%;max-height:88vh;overflow-y:auto;transform:translateY(12px);transition:transform var(--med) var(--ease);}
.m-ov.open .modal{transform:translateY(0);}
.m-hd{display:flex;align-items:center;justify-content:space-between;margin-bottom:20px;}
.m-ttl{font-size:18px;font-weight:600;letter-spacing:-.02em;}
.m-close{width:32px;height:32px;border-radius:var(--r4);display:flex;align-items:center;justify-content:center;color:var(--t3);font-size:22px;line-height:1;transition:all var(--fast) var(--ease);}
.m-close:hover{background:var(--bgh);color:var(--t1);}
.m-ft{display:flex;gap:8px;justify-content:flex-end;margin-top:24px;flex-wrap:wrap;}
/* SETTINGS */
.sg-wrap{margin-bottom:32px;}
.sg-ttl{font-size:11px;color:var(--t3);letter-spacing:.12em;text-transform:uppercase;font-weight:700;margin-bottom:12px;padding:0 4px;}
.s-card{background:var(--bg1);border:1px solid var(--br);border-radius:var(--r14);overflow:hidden;}
.s-row{display:flex;align-items:center;justify-content:space-between;padding:16px 20px;border-bottom:1px solid var(--br);gap:16px;}
.s-row:last-child{border-bottom:none;}
.s-ttl{font-size:14px;font-weight:500;}
.s-sub{font-size:12px;color:var(--t3);margin-top:2px;}
.th-pick{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;padding:16px 20px;}
.th-sw{display:flex;flex-direction:column;align-items:center;gap:8px;cursor:pointer;}
.th-col{width:100%;height:44px;border-radius:var(--r10);border:2px solid transparent;transition:all var(--fast) var(--ease);}
.th-sw.on .th-col{border-color:var(--accent);box-shadow:0 0 0 3px var(--accent-g);}
.th-nm{font-size:11px;color:var(--t2);text-align:center;}
.th-sw.on .th-nm{color:var(--t1);font-weight:600;}
.seg{display:flex;background:var(--bg);border:1px solid var(--br);border-radius:var(--r4);padding:3px;}
.seg-btn{padding:6px 14px;font-size:12px;font-weight:600;border-radius:4px;color:var(--t2);transition:all var(--fast) var(--ease);}
.seg-btn.on{background:var(--bg2);color:var(--t1);}
/* BULK */
.subtabs{display:flex;gap:4px;background:var(--bg);border:1px solid var(--br);border-radius:var(--r10);padding:4px;margin-bottom:20px;max-width:fit-content;}
.stab{padding:8px 16px;font-size:13px;font-weight:600;color:var(--t2);border-radius:var(--r6);transition:all var(--fast) var(--ease);}
.stab.on{background:var(--bg2);color:var(--t1);}
.spanel{display:none;}
.spanel.on{display:block;}
.bt-wrap{overflow-x:auto;border:1px solid var(--br);border-radius:var(--r10);margin-bottom:12px;}
.bt{width:100%;border-collapse:separate;border-spacing:0;font-size:13px;}
.bt th{text-align:left;padding:8px 10px;background:var(--bg);font-size:10px;font-weight:700;color:var(--t3);letter-spacing:.08em;text-transform:uppercase;border-bottom:1px solid var(--br);white-space:nowrap;}
.bt td{padding:3px 4px;border-bottom:1px solid var(--br);}
.bt td input,.bt td select{width:100%;padding:7px 9px;background:transparent;border:1px solid transparent;border-radius:var(--r6);font-size:13px;color:var(--t1);transition:all var(--fast) var(--ease);}
.bt td input:focus,.bt td select:focus{background:var(--bg);border-color:var(--accent);outline:none;}
.bt-warn td input{background:var(--warn-bg)!important;}
/* MISC */
.empty{text-align:center;padding:40px 24px;color:var(--t3);}
.empty-ttl{font-size:16px;font-weight:600;color:var(--t2);margin-bottom:6px;}
.empty-sub{font-size:13px;max-width:300px;margin:0 auto;line-height:1.5;}
/* WALKTHROUGH */
.wt-ov{position:fixed;inset:0;background:rgba(0,0,0,.75);backdrop-filter:blur(6px);z-index:200;opacity:0;pointer-events:none;transition:opacity var(--med) var(--ease);}
.wt-ov.on{opacity:1;pointer-events:auto;}
.wt-c{position:fixed;top:50%;left:50%;transform:translate(-50%,-52%);background:var(--bg1);border:1px solid var(--accent);border-radius:var(--r20);padding:32px;max-width:480px;width:90%;box-shadow:0 20px 60px rgba(0,0,0,.5),0 0 0 8px rgba(59,130,246,.1);z-index:201;opacity:0;pointer-events:none;transition:opacity var(--med) var(--ease),transform var(--med) var(--ease);}
.wt-c.on{opacity:1;pointer-events:auto;transform:translate(-50%,-50%);}
.wt-step{font-size:10px;color:var(--accent-b);letter-spacing:.12em;text-transform:uppercase;font-weight:700;margin-bottom:10px;}
.wt-ttl{font-size:22px;font-weight:700;letter-spacing:-.02em;margin-bottom:8px;}
.wt-txt{color:var(--t2);font-size:14px;line-height:1.6;margin-bottom:20px;}
.wt-nav{display:flex;justify-content:space-between;align-items:center;}
.wt-dots{display:flex;gap:6px;}
.wt-dot{width:6px;height:6px;border-radius:50%;background:var(--t4);transition:all var(--fast) var(--ease);}
.wt-dot.on{background:var(--accent);width:20px;border-radius:3px;}
/* HELP */
.h-toc{display:grid;grid-template-columns:repeat(auto-fit,minmax(160px,1fr));gap:10px;margin-bottom:24px;}
.h-ti{padding:12px 16px;background:var(--bg1);border:1px solid var(--br);border-radius:var(--r10);cursor:pointer;transition:all var(--fast) var(--ease);font-size:13px;color:var(--t2);}
.h-ti:hover{border-color:var(--accent);color:var(--t1);}
.h-sec{margin-bottom:32px;}
.h-sec h3{font-size:18px;font-weight:700;letter-spacing:-.02em;margin-bottom:12px;}
.h-sec p,.h-sec li{color:var(--t2);font-size:14px;line-height:1.7;margin-bottom:6px;}
.h-sec ul{list-style:none;padding:0;}
.h-sec li{padding-left:16px;position:relative;}
.h-sec li::before{content:'';width:4px;height:4px;border-radius:50%;background:var(--accent);position:absolute;left:0;top:10px;}
/* LOADER */
.intel-card{background:linear-gradient(135deg,var(--bg1),var(--bg2));border:1px solid var(--accent);box-shadow:0 0 0 1px var(--accent-g);border-radius:var(--r14);padding:24px;margin-bottom:16px;position:relative;overflow:hidden;}
.intel-card::before{content:'';position:absolute;top:0;right:0;width:160px;height:160px;background:radial-gradient(circle,var(--accent-g) 0%,transparent 70%);pointer-events:none;}
.intel-lbl{font-size:10px;font-weight:700;color:var(--accent-b);letter-spacing:.15em;text-transform:uppercase;margin-bottom:12px;}
.intel-row{display:flex;justify-content:space-between;align-items:center;padding:10px 0;border-bottom:1px solid var(--br);font-size:13px;gap:12px;}
.intel-row:last-of-type{border-bottom:none;}
.intel-row-lbl{color:var(--t2);flex:1;}
.intel-row-val{font-weight:700;font-variant-numeric:tabular-nums;font-size:15px;flex-shrink:0;}
.intel-note{font-size:11px;color:var(--t3);margin-top:12px;line-height:1.6;padding:10px 12px;background:var(--bg);border-radius:var(--r6);}
.intel-warn{font-size:11px;color:var(--warn);margin-top:10px;padding:8px 12px;background:var(--warn-bg);border-radius:var(--r6);line-height:1.5;}
.intel-setup{text-align:center;padding:20px;color:var(--t3);}
.intel-setup p{font-size:13px;margin-bottom:12px;line-height:1.6;}
.conf-low{color:var(--warn)!important;}
.conf-med{color:var(--accent-b)!important;}
.conf-high{color:var(--ok)!important;}
.loader{width:16px;height:16px;border:2px solid var(--bgh);border-top-color:var(--t1);border-radius:50%;animation:spin 600ms linear infinite;display:inline-block;}
@keyframes spin{to{transform:rotate(360deg);}}
.hidden{display:none!important;}
/* PROGRESS / CHARTS */
.chart-wrap{background:var(--bg1);border:1px solid var(--br);border-radius:var(--r14);padding:24px;margin-bottom:16px;}
.chart-hd{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:20px;gap:12px;flex-wrap:wrap;}
.chart-ttl{font-size:16px;font-weight:600;letter-spacing:-.01em;}
.chart-sub{font-size:12px;color:var(--t3);margin-top:2px;}
.chart-legend{display:flex;gap:16px;flex-wrap:wrap;align-items:center;}
.chart-leg-item{display:flex;align-items:center;gap:6px;font-size:11px;color:var(--t2);}
.chart-leg-line{width:20px;height:2px;border-radius:1px;flex-shrink:0;}
.chart-leg-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0;}
.chart-svg-wrap{width:100%;overflow:hidden;position:relative;}
.chart-svg-wrap svg{display:block;width:100%;overflow:visible;}
.chart-empty{text-align:center;padding:40px 0;color:var(--t3);font-size:13px;}
.prog-filter-bar{display:flex;gap:8px;margin-bottom:20px;flex-wrap:wrap;}
.prog-preset{font-size:12px;font-weight:600;padding:6px 14px;border-radius:20px;border:1px solid var(--br);color:var(--t2);transition:all var(--fast) var(--ease);}
.prog-preset.on{background:var(--accent);color:#fff;border-color:var(--accent);}
.prog-preset:hover:not(.on):not(:disabled){background:var(--bgh);color:var(--t1);}
.prog-preset:disabled{opacity:.3;cursor:not-allowed;}
.chart-tooltip{position:absolute;background:var(--bg2);border:1px solid var(--brS);border-radius:var(--r6);padding:8px 12px;font-size:12px;pointer-events:none;z-index:10;white-space:nowrap;box-shadow:var(--sh);opacity:0;transition:opacity var(--fast) var(--ease);}
.chart-tooltip.show{opacity:1;}
.chart-tooltip strong{display:block;font-weight:700;margin-bottom:2px;}
.chart-tog{display:flex;align-items:center;gap:5px;font-size:11px;color:var(--t2);background:none;border:none;cursor:pointer;padding:3px 6px;border-radius:var(--r4);transition:all var(--fast) var(--ease);opacity:1;}
.chart-tog:not(.on){opacity:.35;}
.chart-tog span{white-space:nowrap;}
@media(max-width:820px){
  .sidebar{display:none;}.btabs{display:block;}
  .main-hd-in{padding:14px 16px;}.pg-ttl{font-size:18px;}
  .main-body{padding:20px 16px 96px;}
  .hero{padding:24px 20px;border-radius:var(--r14);}.hero-ttl{font-size:22px;}
  .auth-panel{padding:36px 24px;margin:0 16px;}
  .stat-grid{grid-template-columns:repeat(2,1fr);}
  .ph-item{flex-direction:column;align-items:flex-start;}
  .th-pick{grid-template-columns:repeat(2,1fr);}
  .fg{grid-template-columns:1fr;}
}
@media(max-width:400px){.main-body{padding:16px 12px 96px;}}
</style></head>
<body data-theme="charcoal">
<svg width="0" height="0" style="position:absolute" aria-hidden="true">
  <defs><symbol id="lm" viewBox="0 0 32 32"><rect x="4" y="22" width="24" height="4" rx="1" fill="currentColor" opacity=".35"/><rect x="6" y="14" width="20" height="4" rx="1" fill="currentColor" opacity=".65"/><rect x="8" y="6" width="16" height="4" rx="1" fill="currentColor"/><circle cx="26" cy="8" r="2" fill="#3b82f6"/></symbol></defs>
</svg>

<!-- AUTH -->

<div class="auth-screen active" id="authScreen">
  <div class="auth-bg"><div class="auth-grid"></div><div class="auth-glow"></div></div>
  <div class="auth-panel">
    <div style="display:flex;flex-direction:column;align-items:center;gap:16px;margin-bottom:36px;">
      <svg style="width:48px;height:48px;color:var(--t1);"><use href="#lm"/></svg>
      <span style="font-weight:800;font-size:24px;letter-spacing:.2em;">STRATUM<span style="color:var(--accent);">.</span></span>
      <span style="font-size:13px;color:var(--t3);font-weight:700;letter-spacing:.05em;">BRICK. BY. BRICK.</span>
    </div>
    <div style="margin-bottom:20px;">
      <div id="authModeTitle" style="font-size:20px;font-weight:700;letter-spacing:-.02em;margin-bottom:4px;">Welcome back</div>
      <div id="authModeSub" style="font-size:13px;color:var(--t3);">Sign in to your STRATUM account.</div>
    </div>
    <div style="display:flex;flex-direction:column;gap:14px;">
      <div class="field" id="nameField" style="display:none;"><label class="lbl" for="authName">Display name</label><input class="inp" type="text" id="authName" placeholder="What should we call you" maxlength="40" autocomplete="name"></div>
      <div class="field"><label class="lbl" for="authEmail">Email</label><input class="inp" type="email" id="authEmail" placeholder="you@example.com" autocomplete="email"></div>
      <div class="field"><label class="lbl" for="authPw">Password</label><input class="inp" type="password" id="authPw" placeholder="••••••••" autocomplete="current-password"></div>
      <button class="btn btn-p btn-bl" id="authBtn" onclick="handleAuth()"><span id="authBtnLbl">Sign in</span></button>
      <div class="auth-msg" id="authMsg"></div>
      <div style="display:flex;align-items:center;gap:12px;"><div style="flex:1;height:1px;background:var(--br);"></div><span style="font-size:11px;color:var(--t4);">OR</span><div style="flex:1;height:1px;background:var(--br);"></div></div>
      <button class="btn btn-g btn-bl" onclick="toggleAuth()"><span id="authTogLbl">Create a new account</span></button>
      <button type="button" id="forgotBtn" onclick="handleForgotPw()" style="background:none;border:none;color:var(--t3);font-size:12px;text-decoration:underline;cursor:pointer;align-self:center;margin-top:-4px;">Forgot password?</button>
    </div>
    <div style="margin-top:20px;font-size:11px;color:var(--t4);text-align:center;line-height:1.6;">Your data is yours. Private, secure, never shared.</div>
  </div>
</div>

<!-- APP -->

<div class="app" id="app">
  <aside class="sidebar">
    <div class="sb-hd"><div class="brand"><svg class="brand-mark" style="color:var(--t1);"><use href="#lm"/></svg><span class="brand-wm">STRATUM<span style="color:var(--accent);">.</span></span></div></div>
    <nav class="sb-nav">
      <div class="nav-sec">Workspace</div>
      <div class="nav-it on" data-route="dashboard"><span class="nav-ic"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="7" height="9" rx="1"/><rect x="14" y="3" width="7" height="5" rx="1"/><rect x="14" y="12" width="7" height="9" rx="1"/><rect x="3" y="16" width="7" height="5" rx="1"/></svg></span>Dashboard</div>
      <div class="nav-it" data-route="log"><span class="nav-ic"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 20h9"/><path d="M16.5 3.5a2.121 2.121 0 013 3L7 19l-4 1 1-4z"/></svg></span>Log</div>
      <div class="nav-it" data-route="calendar"><span class="nav-ic"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="4" width="18" height="18" rx="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/></svg></span>Calendar</div>
      <div class="nav-it" data-route="phases"><span class="nav-ic"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 16V8a2 2 0 00-1-1.73l-7-4a2 2 0 00-2 0l-7 4A2 2 0 003 8v8a2 2 0 001 1.73l7 4a2 2 0 002 0l7-4A2 2 0 0021 16z"/></svg></span>Phases</div>
      <div class="nav-it" data-route="measurements"><span class="nav-ic"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M3 12h4l3-9 4 18 3-9h4"/></svg></span>Measurements</div>
      <div class="nav-it" data-route="history"><span class="nav-ic"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg></span>History</div>
      <div class="nav-it" data-route="progress"><span class="nav-ic"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="22 12 18 12 15 21 9 3 6 12 2 12"/></svg></span>Progress</div>
      <div class="nav-it" data-route="compare"><span class="nav-ic"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="8" height="18" rx="1"/><rect x="13" y="3" width="8" height="18" rx="1"/></svg></span>Compare</div>
      <div class="nav-it" data-route="photos"><span class="nav-ic"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="18" height="18" rx="2"/><circle cx="8.5" cy="8.5" r="1.5"/><polyline points="21 15 16 10 5 21"/></svg></span>Photos</div>
      <div class="nav-sec">Setup</div>
      <div class="nav-it" data-route="help"><span class="nav-ic"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><path d="M9.09 9a3 3 0 015.83 1c0 2-3 3-3 3"/><line x1="12" y1="17" x2="12.01" y2="17"/></svg></span>Help &amp; Guide</div>
      <div class="nav-it" data-route="settings"><span class="nav-ic"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 00.33 1.82l.06.06a2 2 0 01-2.83 2.83l-.06-.06a1.65 1.65 0 00-1.82-.33 1.65 1.65 0 00-1 1.51V21a2 2 0 01-4 0v-.09A1.65 1.65 0 009 19.4a1.65 1.65 0 00-1.82.33l-.06.06a2 2 0 01-2.83-2.83l.06-.06A1.65 1.65 0 004.6 9a1.65 1.65 0 00-1.51-1H3a2 2 0 010-4h.09A1.65 1.65 0 004.6 9"/></svg></span>Settings</div>
    </nav>
    <div class="sb-ft"><div class="prof-chip"><div class="prof-av" id="profAv">?</div><div style="flex:1;min-width:0;"><div class="prof-nm" id="profNm">—</div><div class="prof-sub" id="profSub">—</div></div></div></div>
  </aside>

  <main class="main">
    <header class="main-hd">
      <div class="main-hd-in">
        <div><div class="pg-sub" id="pgSub">Overview</div><h1 class="pg-ttl" id="pgTtl">Dashboard</h1></div>
        <div style="display:flex;gap:8px;"><button class="icon-btn" id="signOutBtn" title="Sign out"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M9 21H5a2 2 0 01-2-2V5a2 2 0 012-2h4"/><polyline points="16 17 21 12 16 7"/><line x1="21" y1="12" x2="9" y2="12"/></svg></button></div>
      </div>
    </header>
    <div class="main-body">

<!-- DASHBOARD -->

<section class="sec on" data-sec="dashboard">
  <div class="hero">
    <div class="hero-lbl" id="heroLbl">— Getting started</div>
    <div class="hero-row" id="heroRow"></div>
    <div class="hero-ttl" id="heroTtl">Welcome to STRATUM.</div>
    <div class="hero-sub" id="heroSub">Log your first weigh-in to start tracking.</div>
    <div id="goalBarWrap" class="goal-bar-wrap" style="display:none;">
      <div class="goal-bar-hd"><span id="goalBarLbl">Target</span><span id="goalBarPct"></span></div>
      <div class="goal-bar-tr"><div class="goal-bar" id="goalBar" style="width:0%"></div></div>
    </div>
    <div class="hero-stats" id="heroStats" style="display:none;">
      <div><div class="hs-val" id="hsScore">—</div><div class="hs-lbl">Last score</div></div>
      <div><div class="hs-val" id="hsChange">—</div><div class="hs-lbl">Toward goal</div></div>
      <div><div class="hs-val" id="hsProj">—</div><div class="hs-lbl">Projected finish</div></div>
    </div>
    <div class="hero-cta" id="heroCta"><button class="btn btn-p" onclick="nav('log')">Log a weigh-in</button><button class="btn btn-g" onclick="nav('phases')">Create a phase</button></div>
  </div>
  <div class="stat-grid">
    <div class="stat-c"><div class="stat-lbl">Current weight</div><div class="stat-val" id="dWeight">—</div><div class="stat-sub" id="dWeightSub">No weigh-ins yet</div></div>
    <div class="stat-c"><div class="stat-lbl">Weekly avg</div><div class="stat-val" id="dAvg">—</div><div class="stat-sub" id="dAvgSub">This week</div></div>
    <div class="stat-c"><div class="stat-lbl">Rate of change</div><div class="stat-val" id="dRate">—</div><div class="stat-sub" id="dRateSub">vs last check-in</div></div>
    <div class="stat-c"><div class="stat-lbl">Current phase</div><div class="stat-val" id="dPhase" style="font-size:18px;">—</div><div class="stat-sub" id="dPhaseSub">No active phase</div></div>
  </div>
  <!-- TREND INTERPRETATION -->
  <div class="trend-card" id="trendCard">
    <div class="trend-card-lbl">Weekly read</div>
    <div class="trend-read" id="trendRead"><span style="color:var(--t4);font-size:13px;">Log 2+ check-ins to generate a trend read.</span></div>
  </div>

  <!-- MACRO INSIGHT -->

  <div class="trend-card" id="macroCard" style="display:none;">
    <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:10px;">
      <div class="trend-card-lbl" style="margin-bottom:0;">Macro read</div>
      <span id="macroConfBadge"></span>
    </div>
    <div id="macroInsightBody"></div>
  </div>

  <div class="intel-card" id="intelCard">
    <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:12px;">
      <div class="intel-lbl">Trend Analysis</div>
      <button onclick="togIntelExp()" style="background:none;border:none;color:var(--t3);font-size:11px;cursor:pointer;padding:0;text-decoration:underline;" id="intelExpBtn">How this is calculated</button>
    </div>
    <div id="intelExpPanel" style="display:none;padding:10px 14px;background:var(--bg);border-radius:var(--r6);margin-bottom:12px;font-size:12px;color:var(--t2);line-height:1.7;"></div>
    <div id="intelBody"><div class="intel-setup"><p>Setting up...</p></div></div>
  </div>

  <div class="card">
    <div class="card-hd"><div class="card-ttl">Quick weigh-in</div></div>
    <div class="fr">
      <div class="field" style="flex:2;min-width:220px;"><label class="lbl">Date</label>
        <div class="dstep">
          <button class="stbtn" id="dPrevBtn" onclick="stepDate('d',-1)">&#8592;</button>
          <input class="inp" type="date" id="dDate" onchange="onDateChange('d')">
          <button class="stbtn" id="dNextBtn" onclick="stepDate('d',1)">&#8594;</button>
          <button class="stbtn today" id="dTodayBtn" onclick="setToday('d')">Today</button>
        </div>
      </div>
      <div class="field"><label class="lbl" id="dWtLbl">Weight (lbs)</label><input class="inp" type="number" id="dWt" step="0.1" placeholder="185.0"></div>
      <div class="field"><label class="lbl">Calories (optional)</label><input class="inp" type="number" id="dCal" placeholder="2200"></div>
      <button class="btn btn-p" style="height:48px;align-self:flex-end;" onclick="quickLog()">Log</button>
    </div>
  </div>
  <div class="card">
    <div class="card-hd"><div class="card-ttl">Recent weigh-ins</div><button class="btn btn-g btn-xs" onclick="nav('log')">View all</button></div>
    <div id="dRecent"><div class="empty" style="padding:24px;"><div class="empty-sub">No weigh-ins yet.</div></div></div>
  </div>
</section>

<!-- LOG -->

<section class="sec" data-sec="log">
  <div class="ltabs">
    <button class="ltab on" data-lt="wi" onclick="switchLTab('wi')">Daily weigh-in</button>
    <button class="ltab" data-lt="ci" onclick="switchLTab('ci')">Weekly check-in</button>
  </div>
  <div class="lpanel on" id="lpWi">
    <div class="card">
      <div class="card-hd"><div class="card-ttl">Log morning weight</div></div>
      <div class="fr">
        <div class="field" style="flex:2;min-width:220px;"><label class="lbl">Date</label>
          <div class="dstep">
            <button class="stbtn" id="lPrevBtn" onclick="stepDate('l',-1)">&#8592;</button>
            <input class="inp" type="date" id="lDate" onchange="onDateChange('l')">
            <button class="stbtn" id="lNextBtn" onclick="stepDate('l',1)">&#8594;</button>
            <button class="stbtn today" id="lTodayBtn" onclick="setToday('l')">Today</button>
          </div>
        </div>
        <div class="field"><label class="lbl" id="lWtLbl">Weight (lbs)</label><input class="inp" type="number" id="lWt" step="0.1" placeholder="185.0"></div>
        <div class="field"><label class="lbl">Calories (optional)</label><input class="inp" type="number" id="lCal" placeholder="2200"></div>
        <button class="btn btn-p" style="height:48px;align-self:flex-end;" onclick="saveWI()">Save</button>
      </div>
    </div>
    <div class="card">
      <div class="card-hd"><div class="card-ttl">This week</div><div style="display:flex;align-items:center;gap:10px;"><div style="font-size:12px;color:var(--t3);" id="lWeekAvg">Avg: —</div><button onclick="togSection('lWeekList','lWeekChev')" style="background:none;border:none;color:var(--t3);font-size:12px;cursor:pointer;display:flex;align-items:center;gap:3px;padding:0;"><span id="lWeekChev" style="display:inline-block;transition:transform var(--fast) var(--ease);transform:rotate(0deg);">&#9660;</span></button></div></div>
      <div id="lWeekList" style="overflow:hidden;"><div class="empty" style="padding:24px;"><div class="empty-sub">No weigh-ins this week.</div></div></div>
    </div>
    <div class="card">
      <div class="card-hd"><div class="card-ttl">All weigh-ins</div><div style="display:flex;align-items:center;gap:10px;"><div style="font-size:12px;color:var(--t3);">Grouped by month</div><button onclick="togSection('lAllWI','lAllChev')" style="background:none;border:none;color:var(--t3);font-size:12px;cursor:pointer;display:flex;align-items:center;gap:3px;padding:0;"><span id="lAllChev" style="display:inline-block;transition:transform var(--fast) var(--ease);">&#9660;</span></button></div></div>
      <div id="lAllWI" style="overflow:hidden;"><div class="empty" style="padding:24px;"><div class="empty-sub">Your complete history appears here.</div></div></div>
    </div>
  </div>
  <div class="lpanel" id="lpCi">
    <div class="card">
      <div class="card-hd">
        <div><div class="card-ttl">Weekly check-in</div><div class="card-sub">Toggle fields in Settings → Check-in template</div></div>
        <button class="btn btn-g btn-xs" onclick="clearCIForm()">Clear</button>
      </div>
      <div class="fg">
        <div class="ff" style="margin-bottom:4px;">
          <label class="lbl" id="ciSLbl" style="margin-bottom:8px;display:block;">Week</label>
          <div style="display:flex;align-items:center;gap:6px;flex-wrap:wrap;">
            <button type="button" onclick="ciStepWeek(-1)" style="width:36px;height:40px;border-radius:var(--r6);background:var(--bg);border:1px solid var(--br);color:var(--t2);font-size:16px;display:flex;align-items:center;justify-content:center;flex-shrink:0;transition:all var(--fast) var(--ease);" onmouseover="this.style.background='var(--bgh)'" onmouseout="this.style.background='var(--bg)'">&#8592;</button>
            <div style="flex:1;min-width:180px;display:flex;gap:6px;align-items:center;">
              <input class="inp" type="date" id="ciS" onchange="ciStartChanged()" style="flex:1;">
              <span style="color:var(--t3);font-size:13px;flex-shrink:0;">→</span>
              <input class="inp" type="date" id="ciE" onchange="autoFillWt()" style="flex:1;">
            </div>
            <button type="button" onclick="ciStepWeek(1)" id="ciNextWkBtn" style="width:36px;height:40px;border-radius:var(--r6);background:var(--bg);border:1px solid var(--br);color:var(--t2);font-size:16px;display:flex;align-items:center;justify-content:center;flex-shrink:0;transition:all var(--fast) var(--ease);" onmouseover="this.style.background='var(--bgh)'" onmouseout="this.style.background='var(--bg)'">&#8594;</button>
            <button type="button" onclick="ciSetThisWeek()" style="height:40px;padding:0 12px;border-radius:var(--r6);background:var(--bg);border:1px solid var(--br);color:var(--t2);font-size:11px;font-weight:700;letter-spacing:.05em;white-space:nowrap;flex-shrink:0;transition:all var(--fast) var(--ease);" onmouseover="this.style.background='var(--bgh)'" onmouseout="this.style.background='var(--bg)'">This week</button>
          </div>
          <div id="ciWeekPreview" style="font-size:11px;color:var(--t3);margin-top:6px;padding:4px 2px;"></div>
        </div>
        <div class="field"><label class="lbl">Phase</label><select class="sel" id="ciPh"><option value="">— No phase —</option></select></div>
        <div class="field"><label class="lbl">Avg weight (<span class="ulbl">lbs</span>) <span id="ciAutoLbl" style="color:var(--t4);font-size:10px;font-weight:400;text-transform:none;letter-spacing:0;"></span></label><input class="inp" type="number" id="ciWt" step="0.1" placeholder="Auto-calculated"></div>
        <div class="field ci-cal"><label class="lbl">Avg daily calories</label><input class="inp" type="number" id="ciCal" placeholder="2200"></div>
        <div class="field ci-cal"><label class="lbl">Target calories <span style="color:var(--t4);font-size:10px;font-weight:400;text-transform:none;letter-spacing:0;">(this week's goal)</span></label><input class="inp" type="number" id="ciTargetCal" placeholder="2000"></div>
        <div class="field ci-train"><label class="lbl">Training sessions</label><input class="inp" type="number" id="ciTrain" placeholder="4" min="0"></div>
        <div class="field ci-sleep"><label class="lbl">Avg sleep (hrs)</label><input class="inp" type="number" id="ciSleep" step="0.5" placeholder="7.5"></div>
        <div class="field ff ci-mood"><label class="lbl">Mood / energy (1–5)</label>
          <div style="display:flex;gap:8px;">
            <button type="button" class="mbtn" data-v="1" onclick="setMood(1)" style="flex:1;padding:10px;border:1px solid var(--br);border-radius:var(--r10);font-size:14px;background:transparent;color:var(--t2);transition:all var(--fast) var(--ease);">1</button>
            <button type="button" class="mbtn" data-v="2" onclick="setMood(2)" style="flex:1;padding:10px;border:1px solid var(--br);border-radius:var(--r10);font-size:14px;background:transparent;color:var(--t2);transition:all var(--fast) var(--ease);">2</button>
            <button type="button" class="mbtn" data-v="3" onclick="setMood(3)" style="flex:1;padding:10px;border:1px solid var(--br);border-radius:var(--r10);font-size:14px;background:transparent;color:var(--t2);transition:all var(--fast) var(--ease);">3</button>
            <button type="button" class="mbtn" data-v="4" onclick="setMood(4)" style="flex:1;padding:10px;border:1px solid var(--br);border-radius:var(--r10);font-size:14px;background:transparent;color:var(--t2);transition:all var(--fast) var(--ease);">4</button>
            <button type="button" class="mbtn" data-v="5" onclick="setMood(5)" style="flex:1;padding:10px;border:1px solid var(--br);border-radius:var(--r10);font-size:14px;background:transparent;color:var(--t2);transition:all var(--fast) var(--ease);">5</button>
          </div>
        </div>
        <div class="ff ci-mac">
          <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:8px;"><label class="lbl" style="margin:0;">Macros</label><div class="mac-tog"><button class="mac-btn on" id="macPBtn" onclick="setMacMode('pct')">%</button><button class="mac-btn" id="macGBtn" onclick="setMacMode('g')">g</button></div></div>
          <div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;">
            <div class="field"><label class="lbl" style="font-size:10px;">Protein</label><input class="inp" type="number" id="ciProt" step="0.1" placeholder="40" oninput="updMacBar()"></div>
            <div class="field"><label class="lbl" style="font-size:10px;">Carbs</label><input class="inp" type="number" id="ciCarb" step="0.1" placeholder="35" oninput="updMacBar()"></div>
            <div class="field"><label class="lbl" style="font-size:10px;">Fats</label><input class="inp" type="number" id="ciFat" step="0.1" placeholder="25" oninput="updMacBar()"></div>
          </div>
          <div class="mac-bar" id="macBar"><div class="mac-seg mac-p" style="width:40%"></div><div class="mac-seg mac-c" style="width:35%"></div><div class="mac-seg mac-f" style="width:25%"></div></div>
          <div class="mac-leg"><span><span class="mac-dot" style="background:var(--accent)"></span>Protein <span id="macPv">40%</span></span><span><span class="mac-dot" style="background:var(--ok)"></span>Carbs <span id="macCv">35%</span></span><span><span class="mac-dot" style="background:var(--warn)"></span>Fats <span id="macFv">25%</span></span></div>
          <div id="macWarn" style="display:none;font-size:11px;color:var(--bad);margin-top:6px;padding:6px 10px;background:var(--bad-bg);border-radius:var(--r4);"></div>
        </div>
        <div class="ff ci-notes"><label class="lbl">Notes</label><textarea class="ta" id="ciNotes" placeholder="Diet quality, training, energy, anything worth noting."></textarea></div>
      </div>
      <div style="display:flex;gap:8px;justify-content:flex-end;margin-top:20px;flex-wrap:wrap;">
        <button class="btn btn-g" onclick="clearCIForm()">Clear</button>
        <button class="btn btn-p" onclick="saveCI()">Save check-in</button>
      </div>
    </div>
    <div class="card">
      <div class="card-hd"><div class="card-ttl">Previous check-ins</div><div style="font-size:12px;color:var(--t3);">Grouped by month</div></div>
      <div id="lCIList"><div class="empty" style="padding:24px;"><div class="empty-sub">No check-ins yet.</div></div></div>
    </div>
  </div>
</section>

<!-- CALENDAR -->

<section class="sec" data-sec="calendar">
  <div class="card">
    <div class="cal-hd">
      <div class="cal-nav"><button class="cal-nb" onclick="calNav(-1)"><svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="15 18 9 12 15 6"/></svg></button></div>
      <div class="cal-ttl" id="calTtl">—</div>
      <div class="cal-nav"><button class="cal-nb" onclick="calNav(0)" style="font-size:11px;width:auto;padding:0 10px;">Today</button><button class="cal-nb" onclick="calNav(1)"><svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="9 18 15 12 9 6"/></svg></button></div>
    </div>
    <div class="cal-grid" id="calGrid"></div>
  </div>
  <div class="card" id="calDet" style="display:none;">
    <div class="card-hd"><div class="card-ttl" id="calDetTtl">—</div><button class="btn btn-g btn-xs" id="calDetBtn">Log</button></div>
    <div id="calDetBody"></div>
  </div>
</section>

<!-- PHASES -->

<section class="sec" data-sec="phases">
  <div class="card">
    <div class="card-hd"><div class="card-ttl">Your phases</div><button class="btn btn-p btn-sm" onclick="openPhaseModal()">New phase</button></div>
    <div id="phaseList"><div class="empty"><div class="empty-ttl">No phases yet</div><div class="empty-sub">Phases organize your journey — Cut, Bulk, or Maintain.</div></div></div>
  </div>
</section>

<!-- HISTORY -->

<section class="sec" data-sec="progress">
  <div class="prog-filter-bar">
    <button class="prog-preset on" data-pr="phase" onclick="setProgRange('phase')">This phase</button>
    <button class="prog-preset" data-pr="4w" onclick="setProgRange('4w')">Last 4 wks</button>
    <button class="prog-preset" data-pr="3m" onclick="setProgRange('3m')">Last 3 months</button>
    <button class="prog-preset" data-pr="all" onclick="setProgRange('all')">All time</button>
  </div>

  <!-- WEIGHT TREND -->

  <div class="chart-wrap">
    <div class="chart-hd">
      <div><div class="chart-ttl">Weight trend</div><div class="chart-sub">Daily logs · rolling average · check-in averages</div></div>
      <div class="chart-legend" style="gap:10px;">
        <button class="chart-tog on" data-chart="wt" data-series="dots" onclick="togChartSeries('wt','dots',this)" title="Toggle daily logs"><div class="chart-leg-dot" style="background:var(--accent);opacity:.5;"></div><span>Daily logs</span></button>
        <button class="chart-tog on" data-chart="wt" data-series="roll" onclick="togChartSeries('wt','roll',this)" title="Toggle rolling average"><div class="chart-leg-line" style="background:var(--accent);"></div><span>Rolling avg</span></button>
        <button class="chart-tog on" data-chart="wt" data-series="ci" onclick="togChartSeries('wt','ci',this)" title="Toggle check-in averages"><div class="chart-leg-line" style="background:var(--ok);border-top:2px dashed var(--ok);"></div><span>Check-in avg</span></button>
        <button class="chart-tog on" data-chart="wt" data-series="target" onclick="togChartSeries('wt','target',this)" id="goalLineLegendBtn" style="display:none;"><div class="chart-leg-line" style="background:var(--warn);border-top:2px dashed var(--warn);"></div><span>Target</span></button>
      </div>
    </div>
    <div class="chart-svg-wrap" id="weightChartWrap">
      <div class="chart-empty" id="weightChartEmpty">No weigh-in data yet.</div>
    </div>
    <div class="chart-tooltip" id="weightTooltip"></div>
  </div>

  <!-- CUMULATIVE PROGRESS -->

  <div class="chart-wrap">
    <div class="chart-hd">
      <div><div class="chart-ttl">Cumulative progress</div><div class="chart-sub">Total weight change from start of selected range</div></div>
      <div class="chart-legend" style="gap:10px;">
        <button class="chart-tog on" data-chart="rate" data-series="line" onclick="togChartSeries('rate','line',this)" title="Toggle progress line"><div class="chart-leg-line" style="background:var(--accent);"></div><span>Progress</span></button>
        <button class="chart-tog on" data-chart="rate" data-series="pace" onclick="togChartSeries('rate','pace',this)" id="rateLineLegendBtn" style="display:none;"><div class="chart-leg-line" style="background:var(--warn);border-top:2px dashed var(--warn);"></div><span>Goal pace</span></button>
      </div>
    </div>
    <div class="chart-svg-wrap" id="rateChartWrap">
      <div class="chart-empty" id="rateChartEmpty">Need 2+ check-ins to show cumulative progress.</div>
    </div>
    <div class="chart-tooltip" id="rateTooltip"></div>
  </div>

  <!-- CALORIES -->

  <div class="chart-wrap">
    <div class="chart-hd">
      <div><div class="chart-ttl">Calorie intake</div><div class="chart-sub">Weekly average calories logged</div></div>
      <div class="chart-legend" style="gap:10px;">
        <button class="chart-tog on" data-chart="cal" data-series="line" onclick="togChartSeries('cal','line',this)" title="Toggle calorie line"><div class="chart-leg-line" style="background:var(--ok);"></div><span>Avg calories</span></button>
        <div class="chart-leg-item" id="calTargetLegend" style="display:none;"><div class="chart-leg-line" style="background:var(--warn);"></div>Phase target</div>
      </div>
    </div>
    <div class="chart-svg-wrap" id="calChartWrap">
      <div class="chart-empty" id="calChartEmpty">No calorie data logged yet.</div>
    </div>
    <div class="chart-tooltip" id="calTooltip"></div>
  </div>
</section>

<section class="sec" data-sec="history">
  <div class="stat-grid">
    <div class="stat-c"><div class="stat-lbl">Weeks tracked</div><div class="stat-val" id="hWks">0</div></div>
    <div class="stat-c"><div class="stat-lbl">Total change <span id="hRangeTag" style="font-size:10px;color:var(--t4);font-weight:400;"></span></div><div class="stat-val" id="hChange">—</div><div class="stat-sub" id="hChangeSub">—</div></div>
    <div class="stat-c"><div class="stat-lbl">Avg weekly rate</div><div class="stat-val" id="hAvgRate">—</div></div>
    <div class="stat-c" id="hBestCard" style="display:none;"><div class="stat-lbl" id="hBestLbl">Best week</div><div class="stat-val" id="hBest">—</div><div class="stat-sub" id="hBestSub">—</div></div>
  </div>
  <div class="card">
    <div class="card-hd"><div class="card-ttl">Check-in timeline</div></div>
    <div class="hfbar">
      <button class="hpreset on" data-hr="phase" onclick="setHRange('phase')">This phase</button>
      <button class="hpreset" data-hr="4w" onclick="setHRange('4w')">Last 4 wks</button>
      <button class="hpreset" data-hr="3m" onclick="setHRange('3m')">Last 3 months</button>
      <button class="hpreset" data-hr="all" onclick="setHRange('all')">All time</button>
      <button class="hpreset" data-hr="custom" onclick="setHRange('custom')">Custom</button>
    </div>
    <div style="display:flex;align-items:center;gap:10px;margin-bottom:12px;flex-wrap:wrap;">
      <label style="font-size:11px;font-weight:600;color:var(--t3);letter-spacing:.08em;text-transform:uppercase;white-space:nowrap;">View phase</label>
      <select class="sel" id="hPhaseFilter" onchange="renderHistory()" style="flex:1;max-width:260px;font-size:13px;padding:8px 12px;">
        <option value="">— All / current filter —</option>
      </select>
    </div>
    <div class="hcust" id="hCust">
      <div class="field" style="flex:1;min-width:140px;"><label class="lbl">From</label><input class="inp" type="date" id="hFrom" onchange="renderHistory()"></div>
      <div class="field" style="flex:1;min-width:140px;"><label class="lbl">To</label><input class="inp" type="date" id="hTo" onchange="renderHistory()"></div>
    </div>
    <div id="histTl"><div class="empty"><div class="empty-ttl">No history yet</div><div class="empty-sub">Complete your first weekly check-in to begin.</div></div></div>
  </div>
</section>

<!-- HELP -->

<section class="sec" data-sec="help">
  <div class="card">
    <div class="card-hd"><div><div class="card-ttl">User guide</div><div class="card-sub">Everything STRATUM does and how to use it.</div></div><button class="btn btn-p btn-sm" onclick="startWT()">Start walkthrough</button></div>
    <div class="h-toc">
      <div class="h-ti" onclick="scrollHelp('dash')">Dashboard</div>
      <div class="h-ti" onclick="scrollHelp('log')">Logging</div>
      <div class="h-ti" onclick="scrollHelp('phases')">Phases &amp; goals</div>
      <div class="h-ti" onclick="scrollHelp('score')">Consistency score</div>
      <div class="h-ti" onclick="scrollHelp('intel')">Trend Analysis</div>
      <div class="h-ti" onclick="scrollHelp('cal')">Calendar</div>
      <div class="h-ti" onclick="scrollHelp('hist')">History</div>
      <div class="h-ti" onclick="scrollHelp('progress')">Progress charts</div>
      <div class="h-ti" onclick="scrollHelp('bulk')">Bulk entry</div>
      <div class="h-ti" onclick="scrollHelp('sett')">Settings</div>
    </div>
    <div class="h-sec" id="help-dash"><h3>Dashboard</h3><p>Your command center. The hero card adapts as you log data. Once you have a phase with a target weight it shows a progress bar and projected finish date based on your rolling rate.</p><ul><li><strong>Current weight</strong> — your most recent daily weigh-in.</li><li><strong>Weekly avg</strong> — average of all weigh-ins Mon–Sun (or Sun–Sat if configured).</li><li><strong>Rate of change</strong> — difference between your two most recent check-in averages.</li><li><strong>Current phase</strong> — the phase active today.</li></ul></div>
    <div class="h-sec" id="help-log"><h3>Logging data</h3><p>Two tabs: Daily weigh-in and Weekly check-in.</p><ul><li><strong>Daily weigh-in</strong> — use the arrow buttons to step days, or the date picker to jump. Future dates are blocked.</li><li><strong>Weekly check-in</strong> — avg weight auto-fills from your daily logs the moment you pick a start or end date. Toggle optional fields in Settings → Check-in template.</li></ul></div>
    <div class="h-sec" id="help-phases"><h3>Phases &amp; goals</h3><p>Phases organize your journey into named, goal-driven blocks. Set Cut, Bulk, or Maintain. Add a starting weight, target weight, target date, and weekly rate — STRATUM cross-checks the math and warns if they don't align.</p><p>When you're done, tap <strong>Complete</strong> on the active phase for a full summary, then start a new one.</p></div>
    <div class="h-sec" id="help-score"><h3>Consistency score (0–100)</h3><p>Every check-in earns a score based on effort, not outcome.</p><ul><li><strong>Submit check-in — 35 pts</strong> — showing up is the biggest thing.</li><li><strong>Any weigh-in this week — 25 pts</strong> — even one daily log earns full points.</li><li><strong>Calories logged — 20 pts</strong> — any value in the calories field.</li><li><strong>Weight trending right direction — 20 pts</strong> — cut = lower avg than last week, bulk = higher, maintain = within ±0.5 lbs.</li></ul><p>Bulk imports are excluded. They don't count toward achievements or goal progress.</p></div>
    <div class="h-sec" id="help-intel"><h3>Trend Analysis</h3><p>The Trend Analysis card on the dashboard provides a maintenance calorie estimate and tracks how results compare to the active phase plan.</p><ul><li><strong>Adaptive estimate</strong> — once 2+ weekly check-ins with calories are logged, STRATUM derives maintenance from actual weight changes and logged calories, weighted toward recent weeks. This replaces the formula estimate and updates with each check-in.</li><li><strong>Formula fallback</strong> — when adaptive data is insufficient, the estimate uses Mifflin-St Jeor based on the profile set in Settings → Maintenance estimate setup. Shown as low confidence until real data is available.</li><li><strong>This week's balance</strong> — the implied daily surplus or deficit: most recent check-in calories minus the maintenance estimate.</li><li><strong>Signal check</strong> — flags when logged calories and actual weight change diverge significantly, which may indicate water retention, water loss, or a logging gap.</li><li><strong>Projected finish</strong> — extrapolates current rate of change against phase target weight. Based on the rolling trend across the last 1–4 check-ins. Confidence label reflects data quantity.</li><li><strong>How this is calculated</strong> — tap the link on the card to view transparent reasoning based on actual data sources and the calculation method in use.</li></ul></div>
<div class="h-sec" id="help-cal"><h3>Calendar</h3><p>Month view of daily weigh-ins. Future dates are blocked. Tap any past day to view or log.</p></div>
    <div class="h-sec" id="help-progress"><h3>Progress charts</h3><p>The Progress tab has three charts, all scoped to the same filter. Each chart has per-series toggles in its header — click any legend item to show or hide that data series.</p><ul><li><strong>Weight trend</strong> — daily weigh-ins as dots, with a 7-day rolling average line overlay and a separate weekly check-in average line. The rolling average smooths out day-to-day fluctuation. If you have a phase target weight set, a dashed line shows it.</li><li><strong>Cumulative progress</strong> — total weight change from the start of the selected range, plotted as a continuous line starting at zero. The slope shows your pace — steeper means faster change, flat means stalled. If your phase has a weekly rate set, a dashed goal pace line shows what the slope should look like. Hovering a point shows the total change and that week's average weight.</li><li><strong>Calorie intake</strong> — weekly average calories from check-ins. If you set a target calorie goal on a check-in, a reference line shows it.</li></ul></div>
<div class="h-sec" id="help-hist"><h3>History</h3><p>Your complete record organized by phase in collapsible sections. Week numbers count from the start of each phase. Use the filter bar to scope stats: This phase, Last 4 wks, Last 3 months, All time, or Custom.</p></div>
    <div class="h-sec" id="help-bulk"><h3>Bulk entry</h3><p>Found in Settings → Bulk Entry. Add past weeks row by row — set the date range, weight, calories, and notes for each week. Assign all rows to a specific phase or let STRATUM match them by date automatically. All imported data is tagged BULK so you can tell it apart from your live tracking.</p></div>
    <div class="h-sec" id="help-sett"><h3>Settings</h3><ul><li><strong>Theme</strong> — 8 options (4 dark, 4 light).</li><li><strong>Weight unit</strong> — lbs or kg. Display-only conversion; stored values unchanged.</li><li><strong>Week start</strong> — any day of the week.</li><li><strong>Check-in template</strong> — toggle optional fields.</li><li><strong>Bulk entry</strong> — dedicated import page.</li><li><strong>Achievements</strong> — all badges plus progress toward locked ones.</li></ul></div>
  </div>
</section>

<!-- SETTINGS -->

<section class="sec" data-sec="settings">
  <div class="sg-wrap"><div class="sg-ttl">Appearance</div>
    <div class="s-card">
      <div class="s-row" onclick="togThemePicker()" style="cursor:pointer;"><div><div class="s-ttl">Theme</div><div class="s-sub" id="themeSubLbl">4 dark + 4 light</div></div><span id="themeChev" style="font-size:11px;color:var(--t3);transition:transform var(--fast) var(--ease);transform:rotate(-90deg);">&#9660;</span></div>
      <div id="themePickerWrap" style="display:none;"><div class="th-pick">
        <div class="th-sw on" data-tc="charcoal"><div class="th-col" style="background:#0a0a0a;border:1px solid rgba(255,255,255,.1);"></div><div class="th-nm">Charcoal</div></div>
        <div class="th-sw" data-tc="navy"><div class="th-col" style="background:#0d1117;border:1px solid rgba(255,255,255,.1);"></div><div class="th-nm">Navy</div></div>
        <div class="th-sw" data-tc="oled"><div class="th-col" style="background:#000;border:1px solid rgba(255,255,255,.1);"></div><div class="th-nm">OLED</div></div>
        <div class="th-sw" data-tc="warm"><div class="th-col" style="background:#12100e;border:1px solid rgba(255,220,180,.1);"></div><div class="th-nm">Warm Dark</div></div>
        <div class="th-sw" data-tc="light-gray"><div class="th-col" style="background:#f2f2f0;border:1px solid rgba(0,0,0,.1);"></div><div class="th-nm">Light Gray</div></div>
        <div class="th-sw" data-tc="light-warm"><div class="th-col" style="background:#f5f0e8;border:1px solid rgba(120,90,40,.1);"></div><div class="th-nm">Warm Paper</div></div>
        <div class="th-sw" data-tc="light-white"><div class="th-col" style="background:#fff;border:1px solid rgba(0,0,0,.12);"></div><div class="th-nm">True White</div></div>
        <div class="th-sw" data-tc="light-sky"><div class="th-col" style="background:#edf1f7;border:1px solid rgba(60,90,140,.1);"></div><div class="th-nm">Sky</div></div>
      </div></div>
    </div>
  </div>
  <div class="sg-wrap"><div class="sg-ttl">Units &amp; Time</div>
    <div class="s-card">
      <div class="s-row"><div><div class="s-ttl">Weight unit</div><div class="s-sub">Display-only — stored values unchanged</div></div><div class="seg"><button class="seg-btn on" id="uLbs">lbs</button><button class="seg-btn" id="uKg">kg</button></div></div>
      <div class="s-row"><div><div class="s-ttl">Week start day</div><div class="s-sub">Affects check-ins, calendar, averages</div></div><select class="sel" id="wkStartSel" style="width:auto;min-width:160px;"><option value="1">Monday</option><option value="2">Tuesday</option><option value="3">Wednesday</option><option value="4">Thursday</option><option value="5">Friday</option><option value="6">Saturday</option><option value="0">Sunday</option></select></div>
    </div>
  </div>
  <div class="sg-wrap"><div class="sg-ttl">Trend Analysis Profile</div>
    <div class="s-card">
      <div class="s-row" onclick="openIntelModal()" style="cursor:pointer;">
        <div><div class="s-ttl">Maintenance estimate setup</div><div class="s-sub" id="intelProfileSub">Set age, sex, height, activity level</div></div>
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" style="color:var(--t3);flex-shrink:0;"><polyline points="9 18 15 12 9 6"/></svg>
      </div>
    </div>
  </div>
  <div class="sg-wrap"><div class="sg-ttl">Bulk Entry</div>
    <div class="s-card">
      <div class="s-row" onclick="nav('bulk')" style="cursor:pointer;"><div><div class="s-ttl">Open bulk entry</div><div class="s-sub">Enter historical weeks manually, one at a time</div></div><svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" style="color:var(--t3);flex-shrink:0;"><polyline points="9 18 15 12 9 6"/></svg></div>
      <div class="s-row" onclick="openReassignModal()" style="cursor:pointer;"><div><div class="s-ttl">Reassign bulk data to phases</div><div class="s-sub" id="reassignSub">Assign existing bulk check-ins to a phase</div></div><svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" style="color:var(--t3);flex-shrink:0;"><polyline points="9 18 15 12 9 6"/></svg></div>
    </div>
  </div>
  <div class="sg-wrap"><div class="sg-ttl">Check-in Template</div>
    <div class="s-card">
      <div class="tpl-row"><div><div class="tpl-ttl">Week dates</div><div class="tpl-sub">Always shown</div></div><div class="tpl-lock">Always on</div></div>
      <div class="tpl-row"><div><div class="tpl-ttl">Average weight</div><div class="tpl-sub">Auto-fills from daily logs</div></div><div class="tpl-lock">Always on</div></div>
      <div class="tpl-row"><div><div class="tpl-ttl">Calories</div><div class="tpl-sub">Avg daily intake</div></div><div class="tog on" data-tpl="cal"></div></div>
      <div class="tpl-row"><div><div class="tpl-ttl">Macros</div><div class="tpl-sub">Protein / Carbs / Fats</div></div><div class="tog on" data-tpl="mac"></div></div>
      <div class="tpl-row"><div><div class="tpl-ttl">Mood / energy</div><div class="tpl-sub">1–5 scale</div></div><div class="tog" data-tpl="mood"></div></div>
      <div class="tpl-row"><div><div class="tpl-ttl">Sleep average</div><div class="tpl-sub">Hours per night</div></div><div class="tog" data-tpl="sleep"></div></div>
      <div class="tpl-row"><div><div class="tpl-ttl">Training sessions</div><div class="tpl-sub">Sessions this week</div></div><div class="tog" data-tpl="train"></div></div>
      <div class="tpl-row"><div><div class="tpl-ttl">Notes</div><div class="tpl-sub">Free text</div></div><div class="tog on" data-tpl="notes"></div></div>
    </div>
  </div>
  <div class="sg-wrap"><div class="sg-ttl">Achievements</div><div class="s-card" id="settAch"><div style="padding:16px 20px;font-size:13px;color:var(--t3);">Loading...</div></div></div>
  <div class="sg-wrap"><div class="sg-ttl">Help</div>
    <div class="s-card">
      <div class="s-row" onclick="startWT()" style="cursor:pointer;"><div><div class="s-ttl">Replay walkthrough</div></div><svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" style="color:var(--t3);flex-shrink:0;"><polyline points="9 18 15 12 9 6"/></svg></div>
      <div class="s-row" onclick="nav('help')" style="cursor:pointer;"><div><div class="s-ttl">Open user guide</div></div><svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" style="color:var(--t3);flex-shrink:0;"><polyline points="9 18 15 12 9 6"/></svg></div>
    </div>
  </div>
  <div class="sg-wrap"><div class="sg-ttl">Account</div>
    <div class="s-card"><div class="s-row"><div><div class="s-ttl" id="settNm">—</div><div class="s-sub" id="settEm">—</div></div><button class="btn btn-g btn-sm" id="settSOBtn">Sign out</button></div></div>
  </div>
</section>

<!-- MEASUREMENTS -->

<section class="sec" data-sec="measurements">
  <div class="card">
    <div class="card-hd">
      <div><div class="card-ttl">Log measurements</div><div class="card-sub">All fields optional — log what you track</div></div>
      <button class="btn btn-g btn-xs" onclick="clearMeasForm()">Clear</button>
    </div>
    <div class="field" style="margin-bottom:16px;">
      <label class="lbl">Date</label>
      <div class="dstep">
        <button class="stbtn" onclick="stepMeasDate(-1)">&#8592;</button>
        <input class="inp" type="date" id="measDate" onchange="onMeasDateChange()">
        <button class="stbtn" onclick="stepMeasDate(1)" id="measNextBtn">&#8594;</button>
        <button class="stbtn today" id="measTodayBtn" onclick="setMeasToday()">Today</button>
      </div>
    </div>
    <div class="meas-grid">
      <div class="meas-field"><label class="lbl">Waist (<span class="ulbl-meas">in</span>)</label><input class="inp" type="number" id="mWaist" step="0.1" placeholder="32.0"></div>
      <div class="meas-field"><label class="lbl">Chest (<span class="ulbl-meas">in</span>)</label><input class="inp" type="number" id="mChest" step="0.1" placeholder="40.0"></div>
      <div class="meas-field"><label class="lbl">Hips (<span class="ulbl-meas">in</span>)</label><input class="inp" type="number" id="mHips" step="0.1" placeholder="38.0"></div>
      <div class="meas-field"><label class="lbl">Left arm (<span class="ulbl-meas">in</span>)</label><input class="inp" type="number" id="mArmL" step="0.1" placeholder="14.0"></div>
      <div class="meas-field"><label class="lbl">Right arm (<span class="ulbl-meas">in</span>)</label><input class="inp" type="number" id="mArmR" step="0.1" placeholder="14.0"></div>
      <div class="meas-field"><label class="lbl">Left thigh (<span class="ulbl-meas">in</span>)</label><input class="inp" type="number" id="mThighL" step="0.1" placeholder="22.0"></div>
      <div class="meas-field"><label class="lbl">Right thigh (<span class="ulbl-meas">in</span>)</label><input class="inp" type="number" id="mThighR" step="0.1" placeholder="22.0"></div>
      <div class="meas-field"><label class="lbl">Body fat %</label><input class="inp" type="number" id="mBf" step="0.1" placeholder="18.0" min="1" max="60"></div>
    </div>
    <div class="field" style="margin-bottom:16px;">
      <label class="lbl">Notes (optional)</label>
      <textarea class="ta" id="mNotes" placeholder="Method used, conditions, anything worth recording." style="min-height:70px;"></textarea>
    </div>
    <div style="display:flex;gap:8px;justify-content:flex-end;">
      <button class="btn btn-g" onclick="clearMeasForm()">Clear</button>
      <button class="btn btn-p" onclick="saveMeas()">Save measurement</button>
    </div>
  </div>

  <div class="card">
    <div class="card-hd"><div class="card-ttl">Measurement history</div><div style="font-size:12px;color:var(--t3);">Grouped by month</div></div>
    <div id="measList"><div class="empty" style="padding:24px;"><div class="empty-sub">No measurements logged yet.</div></div></div>
  </div>
</section>

<!-- PHASE COMPARISON -->

<section class="sec" data-sec="compare">
  <div class="card">
    <div class="card-hd"><div><div class="card-ttl">Compare phases</div><div class="card-sub">Select any two phases to compare side by side</div></div></div>
    <div class="fg" style="margin-bottom:16px;">
      <div class="field">
        <label class="lbl">Phase A</label>
        <select class="sel" id="cmpPhaseA" onchange="renderComparison()"><option value="">— Select phase —</option></select>
      </div>
      <div class="field">
        <label class="lbl">Phase B</label>
        <select class="sel" id="cmpPhaseB" onchange="renderComparison()"><option value="">— Select phase —</option></select>
      </div>
    </div>
    <div id="cmpResult"><div class="empty" style="padding:32px;"><div class="empty-sub">Select two phases above to see the comparison.</div></div></div>
  </div>
</section>

<!-- PROGRESS PHOTOS -->

<section class="sec" data-sec="photos">
  <div class="card">
    <div class="card-hd"><div><div class="card-ttl">Add photo</div><div class="card-sub">Stored locally on this device</div></div></div>
    <div style="display:flex;flex-direction:column;gap:14px;">
      <div class="fg">
        <div class="field">
          <label class="lbl">Date</label>
          <input class="inp" type="date" id="photoDate" max="">
        </div>
        <div class="field">
          <label class="lbl">Phase (optional)</label>
          <select class="sel" id="photoPhase"><option value="">— No phase —</option></select>
        </div>
      </div>
      <div class="field">
        <label class="lbl">Note (optional)</label>
        <input class="inp" type="text" id="photoNote" placeholder="Front, side, back, condition note...">
      </div>
      <div class="field">
        <label class="lbl">Photo</label>
        <input type="file" id="photoFile" accept="image/*" style="display:none;" onchange="onPhotoSelected()">
        <div id="photoPreviewWrap" style="display:none;margin-bottom:8px;">
          <img id="photoPreview" style="max-height:200px;border-radius:var(--r10);object-fit:cover;">
        </div>
        <button class="btn btn-g" onclick="q('photoFile').click()" type="button">Choose image</button>
      </div>
      <div style="display:flex;gap:8px;justify-content:flex-end;">
        <button class="btn btn-g" onclick="clearPhotoForm()">Clear</button>
        <button class="btn btn-p" onclick="savePhoto()">Save photo</button>
      </div>
    </div>
  </div>

  <div class="card" id="photoCompareCard" style="display:none;">
    <div class="card-hd"><div class="card-ttl">Compare photos</div><button class="btn btn-g btn-xs" onclick="clearPhotoCompare()">Clear</button></div>
    <div class="photo-compare" id="photoCompareGrid"></div>
  </div>

  <div class="card">
    <div class="card-hd"><div class="card-ttl">Photo history</div><div style="font-size:12px;color:var(--t3);">Tap any photo to compare</div></div>
    <div id="photoList"><div class="empty" style="padding:32px;"><div class="empty-sub">No photos yet. Add your first above.</div></div></div>
  </div>
</section>

<!-- BULK ENTRY PAGE -->

<section class="sec" data-sec="bulk">
  <div style="margin-bottom:20px;"><button class="btn btn-g btn-xs" onclick="nav('settings')">&larr; Back to Settings</button></div>
  <div class="card">
    <div class="card-hd"><div><div class="card-ttl">Bulk Historical Entry</div><div class="card-sub">Bulk data is flagged BULK and excluded from achievements and goal progress.</div></div></div>
    <div style="padding:14px 16px;background:var(--bg);border-radius:var(--r10);margin-bottom:16px;font-size:13px;color:var(--t2);line-height:1.6;">Add rows one at a time. All saved as bulk — excluded from achievements and goals.</div>
      <div class="fg" style="margin-bottom:16px;">
        <div class="field"><label class="lbl">Assign all rows to phase</label><select class="sel" id="bmPhase"><option value="">— No phase —</option></select></div>
        <div class="field" style="justify-content:flex-end;"><label class="lbl">&nbsp;</label><button class="btn btn-g btn-sm" style="align-self:flex-end;" onclick="bmAddRow()">+ Add row</button></div>
      </div>
      <div id="bmTable"></div>
      <div style="display:flex;gap:8px;justify-content:flex-end;margin-top:12px;flex-wrap:wrap;" id="bmActs" class="hidden">
        <button class="btn btn-g" onclick="bmClear()">Discard all</button>
        <button class="btn btn-p" onclick="saveManual()">Save all as bulk</button>
      </div>
  </div>
</section>

```
</div><!-- /main-body -->
```

  </main>

  <nav class="btabs">
    <div class="btabs-in">
      <button class="tab-it on" data-route="dashboard"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="7" height="9" rx="1"/><rect x="14" y="3" width="7" height="5" rx="1"/><rect x="14" y="12" width="7" height="9" rx="1"/><rect x="3" y="16" width="7" height="5" rx="1"/></svg><span class="tab-lbl">Home</span></button>
      <button class="tab-it" data-route="log"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 5v14M5 12h14"/></svg><span class="tab-lbl">Log</span></button>
      <button class="tab-it" data-route="measurements"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M3 12h4l3-9 4 18 3-9h4"/></svg><span class="tab-lbl">Measure</span></button>
      <button class="tab-it" data-route="phases"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 16V8a2 2 0 00-1-1.73l-7-4a2 2 0 00-2 0l-7 4A2 2 0 003 8v8a2 2 0 001 1.73l7 4a2 2 0 002 0l7-4A2 2 0 0021 16z"/></svg><span class="tab-lbl">Phases</span></button>
      <button class="tab-it" data-route="history"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg><span class="tab-lbl">History</span></button>
      <button class="tab-it" data-route="settings"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="3"/><path d="M12 1v6m0 6v6m11-7h-6m-6 0H1"/></svg><span class="tab-lbl">Settings</span></button>
    </div>
  </nav>
</div>

<!-- REASSIGN BULK DATA MODAL -->

<div class="m-ov" id="mReassign">
  <div class="modal">
    <div class="m-hd"><div class="m-ttl">Reassign bulk data</div><button class="m-close" onclick="closeM('mReassign')">&times;</button></div>
    <p style="font-size:13px;color:var(--t2);margin-bottom:16px;line-height:1.6;">Assign existing bulk check-ins to a phase. You can batch-assign all unphased entries, or change the phase for individual entries below.</p>
    <div style="padding:14px 16px;background:var(--bg);border-radius:var(--r10);margin-bottom:16px;">
      <div style="font-size:11px;font-weight:700;color:var(--t2);letter-spacing:.08em;text-transform:uppercase;margin-bottom:12px;">Batch assign all unphased bulk entries</div>
      <div style="display:flex;gap:8px;align-items:flex-end;flex-wrap:wrap;">
        <div class="field" style="flex:1;min-width:180px;"><label class="lbl">Assign to phase</label><select class="sel" id="raBatchPhase"><option value="">— Select a phase —</option></select></div>
        <button class="btn btn-p btn-sm" onclick="raBatchAssign()" style="flex-shrink:0;">Assign all unphased</button>
      </div>
      <div style="font-size:11px;color:var(--t4);margin-top:8px;" id="raUnphasedCount"></div>
    </div>
    <div style="font-size:11px;font-weight:700;color:var(--t2);letter-spacing:.08em;text-transform:uppercase;margin-bottom:10px;">All bulk check-ins</div>
    <div id="raList" style="max-height:320px;overflow-y:auto;border:1px solid var(--br);border-radius:var(--r10);"></div>
    <div class="m-ft"><button class="btn btn-g" onclick="closeM('mReassign')">Done</button></div>
  </div>
</div>

<!-- INTELLIGENCE PROFILE MODAL -->

<div class="m-ov" id="mIntel">
  <div class="modal">
    <div class="m-hd"><div class="m-ttl">Trend Analysis Profile</div><button class="m-close" onclick="closeM('mIntel')">&times;</button></div>
    <p style="font-size:13px;color:var(--t2);margin-bottom:20px;line-height:1.6;">Used for the formula estimate when you have limited data. Once you have 2+ check-ins with calories logged, the adaptive estimate takes over and uses your actual results instead.</p>
    <div style="display:flex;flex-direction:column;gap:14px;">
      <div class="fg">
        <div class="field"><label class="lbl">Age</label><input class="inp" type="number" id="ipAge" placeholder="30" min="13" max="100"></div>
        <div class="field"><label class="lbl">Biological sex</label><select class="sel" id="ipSex"><option value="">— Select —</option><option value="male">Male</option><option value="female">Female</option></select></div>
      </div>
      <div class="fg">
        <div class="field"><label class="lbl">Height</label>
          <div style="display:flex;gap:6px;">
            <input class="inp" type="number" id="ipHeightFt" placeholder="5" min="3" max="8" style="flex:1;">
            <span style="align-self:center;color:var(--t3);font-size:13px;">ft</span>
            <input class="inp" type="number" id="ipHeightIn" placeholder="10" min="0" max="11" style="flex:1;">
            <span style="align-self:center;color:var(--t3);font-size:13px;">in</span>
          </div>
        </div>
        <div class="field"><label class="lbl">Activity level</label>
          <select class="sel" id="ipActivity">
            <option value="">— Select —</option>
            <option value="1.2">Sedentary (desk job, little exercise)</option>
            <option value="1.375">Light (1-3 days/wk)</option>
            <option value="1.55">Moderate (3-5 days/wk)</option>
            <option value="1.725">Active (6-7 days/wk)</option>
            <option value="1.9">Very active (physical job + training)</option>
          </select>
        </div>
      </div>
      <div id="ipPreview" style="padding:12px 16px;background:var(--bg);border-radius:var(--r10);font-size:13px;color:var(--t2);display:none;"></div>
    </div>
    <div class="m-ft"><button class="btn btn-g" onclick="closeM('mIntel')">Cancel</button><button class="btn btn-p" onclick="saveIntelProfile()">Save profile</button></div>
  </div>
</div>

<!-- PHASE MODAL -->

<div class="m-ov" id="mPhase">
  <div class="modal">
    <div class="m-hd"><div class="m-ttl" id="mPhaseTtl">New phase</div><button class="m-close" onclick="closeM('mPhase')">&times;</button></div>
    <div style="display:flex;flex-direction:column;gap:16px;">
      <div class="field"><label class="lbl">Phase name</label><input class="inp" type="text" id="pmNm" placeholder='"Cut Phase 1", "Winter Bulk"'></div>
      <div class="fg">
        <div class="field"><label class="lbl">Goal type</label><select class="sel" id="pmGoal"><option value="cut">Cut — losing weight</option><option value="bulk">Bulk — gaining weight</option><option value="maintain">Maintain — recomp / hold</option></select></div>
      </div>
      <div style="padding:14px 16px;background:var(--bg);border-radius:var(--r10);">
        <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:12px;">
          <div style="font-size:11px;font-weight:700;color:var(--t2);letter-spacing:.08em;text-transform:uppercase;">Calorie targets</div>
          <button type="button" class="btn btn-g btn-xs" onclick="pmAddCalStage()">+ Add stage</button>
        </div>
        <div style="font-size:11px;color:var(--t3);margin-bottom:10px;line-height:1.5;">Set one target or multiple — each stage applies from its date until the next. The first stage uses the phase start date.</div>
        <div id="pmCalStages" style="display:flex;flex-direction:column;gap:8px;"></div>
      </div>
      <div style="padding:14px 16px;background:var(--bg);border-radius:var(--r10);">
        <div style="font-size:11px;font-weight:700;color:var(--t2);letter-spacing:.08em;text-transform:uppercase;margin-bottom:12px;">Phase goal (optional)</div>
        <div class="fg">
          <div class="field"><label class="lbl">Starting weight (<span class="ulbl">lbs</span>)</label><input class="inp" type="number" id="pmSW" step="0.1" placeholder="Auto from latest log"></div>
          <div class="field"><label class="lbl">Target weight (<span class="ulbl">lbs</span>)</label><input class="inp" type="number" id="pmTW" step="0.1" placeholder="175.0"></div>
          <div class="field"><label class="lbl">Target date</label><input class="inp" type="date" id="pmTD"></div>
          <div class="field"><label class="lbl">Weekly rate (<span class="ulbl">lbs</span>/wk)</label><input class="inp" type="number" id="pmRate" step="0.1" placeholder="-0.5"></div>
        </div>
        <div id="pmWarn" style="display:none;font-size:11px;color:var(--warn);padding:8px 10px;background:var(--warn-bg);border-radius:var(--r4);margin-top:10px;line-height:1.5;"></div>
      </div>
      <div class="fg">
        <div class="field"><label class="lbl">Start date</label><input class="inp" type="date" id="pmStart" onchange="pmSyncStageDate()"></div>
        <div class="field"><label class="lbl">End date (optional)</label><input class="inp" type="date" id="pmEnd"></div>
      </div>
    </div>
    <div class="m-ft"><button class="btn btn-g" onclick="closeM('mPhase')">Cancel</button><button class="btn btn-p" onclick="savePhase()">Save phase</button></div>
  </div>
</div>

<!-- WEEK DETAIL MODAL -->

<div class="m-ov" id="mWeek"><div class="modal"><div class="m-hd"><div class="m-ttl" id="mWeekTtl">Week summary</div><button class="m-close" onclick="closeM('mWeek')">&times;</button></div><div id="mWeekBody"></div></div></div>

<!-- COMPLETE PHASE MODAL -->

<div class="m-ov" id="mComplete">
  <div class="modal"><div class="m-hd"><div class="m-ttl" id="mCompTtl">Phase complete</div><button class="m-close" onclick="closeM('mComplete')">&times;</button></div><div id="mCompBody"></div><div class="m-ft" id="mCompFt"></div></div>
</div>

<!-- WALKTHROUGH -->

<div class="wt-ov" id="wtOv"></div>
<div class="wt-c" id="wtCard">
  <div class="wt-step" id="wtStep">Step 1 of 7</div>
  <div class="wt-ttl" id="wtTtl">—</div>
  <div class="wt-txt" id="wtTxt">—</div>
  <div class="wt-nav"><button class="btn btn-g btn-sm" onclick="skipWT()">Skip</button><div class="wt-dots" id="wtDots"></div><button class="btn btn-p btn-sm" id="wtNextBtn" onclick="wtNext()">Next</button></div>
</div>

<!-- CELEBRATION -->

<div class="cel-ov" id="celOv" onclick="closeCel()">
  <div class="cel-c"><div class="cel-ic" id="celIc">★</div><div class="cel-ttl" id="celTtl">Achievement unlocked</div><div class="cel-sub" id="celSub">—</div><button class="btn btn-p" style="margin-top:24px;width:100%;" onclick="closeCel()">Nice.</button></div>
</div>
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2" onerror="window.__sbFailed=true"></script>
<script>
/* ============================================================ CONFIG */
var SUPABASE_URL='', SUPABASE_ANON_KEY='';

/* ============================================================ STORAGE */
var STR_KEY=‘stratum:v3’, STR_GL=‘stratum:global’;
var Local={
_rg:function(){try{return JSON.parse(localStorage.getItem(STR_GL))||{};}catch(e){return{};}},
getG:function(k,fb){var d=Local._rg();return d[k]!==undefined?d[k]:fb;},
setG:function(k,v){var d=Local._rg();d[k]=v;localStorage.setItem(STR_GL,JSON.stringify(d));},
_uid:function(){return appState.user?appState.user.id:’**guest**’;},
_k:function(){return STR_KEY+’:’+Local._uid();},
_r:function(){try{return JSON.parse(localStorage.getItem(Local._k()))||{};}catch(e){return{};}},
get:function(k,fb){var d=Local._r();return d[k]!==undefined?d[k]:fb;},
set:function(k,v){var d=Local._r();d[k]=v;localStorage.setItem(Local._k(),JSON.stringify(d));}
};

/* ============================================================ SUPABASE */
var DEMO=!SUPABASE_URL||!SUPABASE_ANON_KEY, sbc=null;
if(!DEMO){try{if(window.supabase&&window.supabase.createClient)sbc=window.supabase.createClient(SUPABASE_URL,SUPABASE_ANON_KEY);}catch(e){DEMO=true;}}

/* ============================================================ STATE */
var appState={user:null,profile:null,theme:Local.getG(‘theme’,‘charcoal’),unit:‘lbs’,weekStart:1,tpl:{cal:true,mac:true,mood:false,sleep:false,train:false,notes:true},hRange:‘phase’};
var weighIns=[], checkins=[], phases=[], measurements=[], photos=[];
var macMode=‘pct’, selMood=0, calMonth=new Date().getMonth(), calYear=new Date().getFullYear();
var editPhaseId=null, bmRows=[], wtStep=0;

/* ============================================================ UNIT HELPERS */
var L2K=0.453592, K2L=2.20462;
function toDisp(lbs){return appState.unit===‘kg’?Math.round(lbs*L2K*100)/100:lbs;}
function fromDisp(v){return appState.unit===‘kg’?Math.round(v*K2L*100)/100:v;}
function fmtW(lbs,d){if(lbs==null||isNaN(lbs))return’—’;return toDisp(lbs).toFixed(d!=null?d:1)+’ ‘+appState.unit;}
function dispVal(lbs){return lbs!=null?toDisp(lbs).toFixed(1):’’;}

/* ============================================================ DATE HELPERS */
function toDate(s){if(!s)return new Date();var d=new Date(s+‘T00:00:00’);return isNaN(d)?new Date():d;}
function dateStr(d){var dt=typeof d===‘string’?toDate(d):d;return dt.getFullYear()+’-’+String(dt.getMonth()+1).padStart(2,‘0’)+’-’+String(dt.getDate()).padStart(2,‘0’);}
function todayStr(){return dateStr(new Date());}
function addDays(d,n){var dt=new Date(typeof d===‘string’?toDate(d):d);dt.setDate(dt.getDate()+n);return dt;}
function fmtD(d){if(!d)return’—’;var dt=typeof d===‘string’?toDate(d):d;if(isNaN(dt))return’—’;return dt.toLocaleDateString(‘en-US’,{month:‘short’,day:‘numeric’});}
function fmtDF(d){if(!d)return’—’;var dt=typeof d===‘string’?toDate(d):d;return dt.toLocaleDateString(‘en-US’,{weekday:‘short’,month:‘short’,day:‘numeric’,year:‘numeric’});}
function ordSuffix(n){var s=[‘th’,‘st’,‘nd’,‘rd’],v=n%100;return n+(s[(v-20)%10]||s[v]||s[0]);}
function fmtFull(d){if(!d)return’—’;var dt=typeof d===‘string’?toDate(d):d;if(isNaN(dt))return’—’;var days=[‘Sunday’,‘Monday’,‘Tuesday’,‘Wednesday’,‘Thursday’,‘Friday’,‘Saturday’];var months=[‘January’,‘February’,‘March’,‘April’,‘May’,‘June’,‘July’,‘August’,‘September’,‘October’,‘November’,‘December’];return days[dt.getDay()]+’, ‘+months[dt.getMonth()]+’ ‘+ordSuffix(dt.getDate())+’, ‘+dt.getFullYear();}
function fmtMY(d){var dt=typeof d===‘string’?toDate(d):d;return dt.toLocaleDateString(‘en-US’,{month:‘long’,year:‘numeric’});}
function mkKey(ds){return ds?ds.substring(0,7):’’;}
function wkStart(d){var dt=new Date(typeof d===‘string’?toDate(d):d);dt.setHours(0,0,0,0);var day=dt.getDay(),ws=appState.weekStart,diff=((day-ws)+7)%7;dt.setDate(dt.getDate()-diff);return dt;}
function wkEnd(d){var s=wkStart(d);s.setDate(s.getDate()+6);return s;}
function div(a,b){return b===0?0:a/b;}
function esc(s){return(s||’’).toString().replace(/&/g,’&’).replace(/</g,’<’).replace(/>/g,’>’).replace(/”/g,’"’);}
function q(id){return document.getElementById(id);}
function qa(sel){return document.querySelectorAll(sel);}

/* ============================================================ NATURAL DATE PARSER */
var MO={jan:0,feb:1,mar:2,apr:3,may:4,jun:5,jul:6,aug:7,sep:8,oct:9,nov:10,dec:11,january:0,february:1,march:2,april:3,june:5,july:6,august:7,september:8,october:9,november:10,december:11};
function parseDate(s){
if(!s)return null;
s=s.trim().replace(/\s+/g,’ ’);
// Strip day-of-week prefix: “Monday, Sep 25, 2025” → “Sep 25, 2025”
s=s.replace(/^(Monday|Tuesday|Wednesday|Thursday|Friday|Saturday|Sunday),?\s*/i,’’);
var m;
// ISO 2025-09-25
m=s.match(/^(\d{4})-(\d{2})-(\d{2})$/);if(m)return new Date(+m[1],+m[2]-1,+m[3]);
// US slash 9/25/25 or 9/25/2025
m=s.match(/^(\d{1,2})/(\d{1,2})/(\d{2,4})$/);if(m){var y=+m[3];if(y<100)y+=2000;return new Date(y,+m[1]-1,+m[2]);}
// “Sep 25, 2025” or “Sep 25”
m=s.match(/^([A-Za-z]+).?\s+(\d{1,2}),?\s*(\d{4})?$/);if(m){var mo=MO[m[1].toLowerCase()];if(mo!=null){var yr=m[3]?+m[3]:new Date().getFullYear();return new Date(yr,mo,+m[2]);}}
// “25 Sep 2025”
m=s.match(/^(\d{1,2})\s+([A-Za-z]+).?\s*(\d{4})?$/);if(m){var mo2=MO[m[2].toLowerCase()];if(mo2!=null){var yr2=m[3]?+m[3]:new Date().getFullYear();return new Date(yr2,mo2,+m[1]);}}
var d=new Date(s);return isNaN(d)?null:d;
}
function parseDRange(s){
if(!s)return null;
var p=s.split(/\s*[-–—]\s*/);
if(p.length>=2){var d1=parseDate(p[0].trim()),d2=parseDate(p[1].trim());if(d1&&d2&&!isNaN(d1)&&!isNaN(d2))return{start:d1,end:d2};}
return null;
}

/* ============================================================ THEME */
function applyTheme(name){
document.body.setAttribute(‘data-theme’,name);appState.theme=name;
Local.setG(‘theme’,name);if(appState.user)Local.set(‘theme’,name);
var tc={charcoal:’#0a0a0a’,navy:’#0d1117’,oled:’#000’,warm:’#12100e’,‘light-gray’:’#f2f2f0’,‘light-warm’:’#f5f0e8’,‘light-white’:’#f8f8f8’,‘light-sky’:’#edf1f7’};
var mc=document.querySelector(‘meta[name=“theme-color”]’);if(mc)mc.setAttribute(‘content’,tc[name]||’#0a0a0a’);
qa(’.th-sw’).forEach(function(s){s.classList.toggle(‘on’,s.dataset.tc===name);});
updateThemeLabel();
}
qa(’.th-sw’).forEach(function(sw){sw.addEventListener(‘click’,function(){applyTheme(sw.dataset.tc);});});

/* ============================================================ AUTH */
var authIsSignup=false;
function toggleAuth(){
authIsSignup=!authIsSignup;
q(‘nameField’).style.display=authIsSignup?‘flex’:‘none’;
q(‘authModeTitle’).textContent=authIsSignup?‘Create account’:‘Welcome back’;
q(‘authModeSub’).textContent=authIsSignup?‘Set up your STRATUM account.’:‘Sign in to your STRATUM account.’;
q(‘authBtnLbl’).textContent=authIsSignup?‘Create account’:‘Sign in’;
q(‘authTogLbl’).textContent=authIsSignup?‘Already have an account? Sign in’:‘Create a new account’;
q(‘authMsg’).className=‘auth-msg’;
}
function showMsg(txt,k){var e=q(‘authMsg’);e.textContent=txt;e.className=‘auth-msg show ‘+k;}
function handleAuth(){
var email=q(‘authEmail’).value.trim(),pw=q(‘authPw’).value,nm=q(‘authName’).value.trim();
if(!email){showMsg(‘Enter your email.’,‘err’);return;}
if(!pw||pw.length<6){showMsg(‘Password must be at least 6 characters.’,‘err’);return;}
if(authIsSignup&&!nm){showMsg(‘Enter a display name.’,‘err’);return;}
var btn=q(‘authBtn’);btn.disabled=true;btn.innerHTML=’<span class="loader"></span>’;
if(DEMO){
setTimeout(function(){
try{
var us=Local.getG(‘demoUsers’,{});
if(authIsSignup){
if(us[email.toLowerCase()])throw new Error(‘Account already exists. Sign in instead.’);
var id=‘demo-’+Date.now();us[email.toLowerCase()]={id,name:nm,email,pw};
Local.setG(‘demoUsers’,us);Local.setG(‘demoSess’,{email});
appState.user={id,email};appState.profile={display_name:nm,email};enterApp(true);
}else{
var hit=us[email.toLowerCase()];
if(!hit)throw new Error(‘No account found. Create one above.’);
if(hit.pw!==pw)throw new Error(‘Incorrect password.’);
appState.user={id:hit.id,email:hit.email};appState.profile={display_name:hit.name,email:hit.email};
Local.setG(‘demoSess’,{email});enterApp(false);
}
}catch(err){showMsg(err.message,‘err’);btn.disabled=false;btn.innerHTML=’<span id="authBtnLbl">’+(authIsSignup?‘Create account’:‘Sign in’)+’</span>’;}
},350);return;
}
if(authIsSignup){
sbc.auth.signUp({email,password:pw,options:{data:{display_name:nm}}}).then(function(res){
if(res.error)throw res.error;
if(!res.data.session){showMsg(‘Check email to confirm then sign in.’,‘inf’);btn.disabled=false;btn.innerHTML=’<span>Create account</span>’;return;}
appState.user=res.data.user;
sbc.from(‘profiles’).upsert({id:res.data.user.id,display_name:nm,email}).then(function(){loadProf().then(function(){enterApp(true);});});
}).catch(function(e){showMsg(e.message||‘Signup failed.’,‘err’);btn.disabled=false;btn.innerHTML=’<span>Create account</span>’;});
}else{
sbc.auth.signInWithPassword({email,password:pw}).then(function(res){
if(res.error)throw res.error;appState.user=res.data.user;loadProf().then(function(){enterApp(false);});
}).catch(function(e){showMsg(e.message||‘Sign in failed.’,‘err’);btn.disabled=false;btn.innerHTML=’<span>Sign in</span>’;});
}
}
function signOut(){
if(DEMO)Local.setG(‘demoSess’,null);else if(sbc)sbc.auth.signOut();
appState.user=null;appState.profile=null;weighIns=[];checkins=[];phases=[];location.reload();
}
function loadProf(){
return new Promise(function(res){
if(!appState.user||DEMO||!sbc){res();return;}
sbc.from(‘profiles’).select(’*’).eq(‘id’,appState.user.id).single().then(function(r){appState.profile=r.data||{display_name:appState.user.email.split(’@’)[0],email:appState.user.email};res();}).catch(function(){res();});
});
}
q(‘authPw’).addEventListener(‘keydown’,function(e){if(e.key===‘Enter’)handleAuth();});
q(‘signOutBtn’).addEventListener(‘click’,signOut);
q(‘settSOBtn’).addEventListener(‘click’,signOut);

/* ============================================================ ENTER APP */
function enterApp(isNew){
appState.theme=Local.get(‘theme’,Local.getG(‘theme’,‘charcoal’));
appState.unit=Local.get(‘unit’,‘lbs’);
appState.weekStart=Local.get(‘weekStart’,1);
appState.tpl=Local.get(‘tpl’,{cal:true,mac:true,mood:false,sleep:false,train:false,notes:true});
weighIns=Local.get(‘weighIns’,[]);checkins=Local.get(‘checkins’,[]);phases=Local.get(‘phases’,[]);measurements=Local.get(‘measurements’,[]);photos=Local.get(‘photos’,[]);
applyTheme(appState.theme);applyUnitUI();applyTpl();
qa(’[data-tpl]’).forEach(function(t){t.classList.toggle(‘on’,!!appState.tpl[t.dataset.tpl]);});
q(‘wkStartSel’).value=appState.weekStart;
var nm=(appState.profile&&appState.profile.display_name)||‘Friend’;
var em=(appState.profile&&appState.profile.email)||’’;
q(‘profAv’).textContent=nm.charAt(0).toUpperCase();q(‘profNm’).textContent=nm;q(‘profSub’).textContent=em;
q(‘settNm’).textContent=nm;q(‘settEm’).textContent=em;
initDates();ciUpdateNextBtn();ciUpdatePreview();refreshAll();renderCal();checkAch(false);renderAch();fillPhasePickers();renderIntel();
q(‘authScreen’).classList.remove(‘active’);q(‘app’).classList.add(‘on’);
if(isNew||!Local.get(‘wtSeen’,false))setTimeout(startWT,700);
}

/* ============================================================ NAVIGATION */
var PAGE_INFO={dashboard:[‘Overview’,‘Dashboard’],log:[‘Input’,‘Log’],calendar:[‘Review’,‘Calendar’],phases:[‘Organize’,‘Phases’],measurements:[‘Record’,‘Measurements’],history:[‘Archive’,‘History’],progress:[‘Charts’,‘Progress’],compare:[‘Analysis’,‘Compare Phases’],photos:[‘Record’,‘Progress Photos’],help:[‘Learn’,‘Help & Guide’],settings:[‘Configure’,‘Settings’],bulk:[‘Import’,‘Bulk Entry’]};
function nav(route){
appState.route=route;
qa(’[data-route]’).forEach(function(el){el.classList.toggle(‘on’,el.dataset.route===route);});
qa(’[data-sec]’).forEach(function(s){s.classList.toggle(‘on’,s.dataset.sec===route);});
var p=PAGE_INFO[route]||[’’,’’];q(‘pgSub’).textContent=p[0];q(‘pgTtl’).textContent=p[1];
if(route!==‘calendar’){var cd=q(‘calDet’);if(cd)cd.style.display=‘none’;}
if(route===‘progress’){setTimeout(renderAllCharts,50);}
if(route===‘measurements’){setTimeout(function(){initMeasDate();renderMeasurements();},50);}
if(route===‘compare’){setTimeout(function(){fillComparePickers();renderComparison();},50);}
if(route===‘photos’){setTimeout(function(){initPhotoForm();renderPhotos();},50);}
window.scrollTo({top:0,behavior:‘instant’});
}
qa(’[data-route]’).forEach(function(el){el.addEventListener(‘click’,function(){nav(el.dataset.route);});});

/* ============================================================ UNIT DISPLAY */
function applyUnitUI(){
q(‘uLbs’).classList.toggle(‘on’,appState.unit===‘lbs’);q(‘uKg’).classList.toggle(‘on’,appState.unit===‘kg’);
qa(’.ulbl’).forEach(function(el){el.textContent=appState.unit;});
if(q(‘dWtLbl’))q(‘dWtLbl’).textContent=‘Weight (’+appState.unit+’)’;
if(q(‘lWtLbl’))q(‘lWtLbl’).textContent=‘Weight (’+appState.unit+’)’;
}
function setUnit(u){appState.unit=u;if(appState.user)Local.set(‘unit’,u);applyUnitUI();refreshAll();}
q(‘uLbs’).addEventListener(‘click’,function(){setUnit(‘lbs’);});
q(‘uKg’).addEventListener(‘click’,function(){setUnit(‘kg’);});
q(‘wkStartSel’).addEventListener(‘change’,function(){appState.weekStart=parseInt(q(‘wkStartSel’).value);Local.set(‘weekStart’,appState.weekStart);initDates();refreshAll();renderCal();});

/* ============================================================ TEMPLATE */
var TPL_MAP={cal:’.ci-cal’,mac:’.ci-mac’,mood:’.ci-mood’,sleep:’.ci-sleep’,train:’.ci-train’,notes:’.ci-notes’};
function applyTpl(){Object.keys(TPL_MAP).forEach(function(k){document.querySelectorAll(TPL_MAP[k]).forEach(function(el){el.style.display=appState.tpl[k]?’’:‘none’;});});}
qa(’[data-tpl]’).forEach(function(t){t.addEventListener(‘click’,function(){t.classList.toggle(‘on’);appState.tpl[t.dataset.tpl]=t.classList.contains(‘on’);Local.set(‘tpl’,appState.tpl);applyTpl();});});

/* ============================================================ DATE STEPPERS */
function initDates(){
var td=todayStr();
setDF(‘d’,td);setDF(‘l’,td);
var cS=q(‘ciS’),cE=q(‘ciE’);
if(cS&&!cS.value){cS.value=dateStr(wkStart(new Date()));cE.value=dateStr(wkEnd(new Date()));}
var DAY_SHORT=[‘Sun’,‘Mon’,‘Tue’,‘Wed’,‘Thu’,‘Fri’,‘Sat’];
if(q(‘ciSLbl’))q(‘ciSLbl’).textContent=‘Week start (’+DAY_SHORT[appState.weekStart]+’)’;
if(q(‘ciELbl’))q(‘ciELbl’).textContent=‘Week end (’+DAY_SHORT[(appState.weekStart+6)%7]+’)’;
if(q(‘pmStart’)&&!q(‘pmStart’).value)q(‘pmStart’).value=td;
}
function setDF(ctx,ds){
var td=todayStr();
var fId=ctx===‘d’?‘dDate’:‘lDate’;
var nId=ctx===‘d’?‘dNextBtn’:‘lNextBtn’;
var tId=ctx===‘d’?‘dTodayBtn’:‘lTodayBtn’;
var el=q(fId);if(!el)return;
el.value=ds;el.max=td;
var nb=q(nId);if(nb)nb.disabled=ds>=td;
var tb=q(tId);if(tb)tb.classList.toggle(‘is-today’,ds===td);
// Pre-fill weight and calories if an entry exists for this date
var wi=weighIns.find(function(w){return w.date===ds;});
var wInput=ctx===‘d’?q(‘dWt’):q(‘lWt’);
var cInput=ctx===‘d’?q(‘dCal’):q(‘lCal’);
if(wInput&&wi)wInput.value=dispVal(wi.weight);
else if(wInput)wInput.value=’’;
if(cInput&&wi&&wi.calories)cInput.value=wi.calories;
else if(cInput)cInput.value=’’;
}
function stepDate(ctx,dir){
var el=q(ctx===‘d’?‘dDate’:‘lDate’);if(!el)return;
var cur=el.value||todayStr();
var nxt=dateStr(addDays(toDate(cur),dir));
if(nxt>todayStr())return;
setDF(ctx,nxt);
}
function setToday(ctx){setDF(ctx,todayStr());}
function onDateChange(ctx){
var el=q(ctx===‘d’?‘dDate’:‘lDate’);if(!el)return;
var v=el.value;if(v>todayStr()){el.value=todayStr();v=todayStr();}
setDF(ctx,v);
}

/* ============================================================ CHECK-IN AUTO-FILL */
function ciSetThisWeek(){
q(‘ciS’).value=dateStr(wkStart(new Date()));
q(‘ciE’).value=dateStr(wkEnd(new Date()));
ciStartChanged();
}
function ciStepWeek(dir){
var s=q(‘ciS’).value;if(!s)s=dateStr(wkStart(new Date()));
var next=wkStart(addDays(toDate(s),dir*7));
// Block future weeks
if(dateStr(next)>todayStr())return;
q(‘ciS’).value=dateStr(next);
q(‘ciE’).value=dateStr(wkEnd(next));
ciUpdateNextBtn();
ciStartChanged();
}
function ciUpdateNextBtn(){
var btn=q(‘ciNextWkBtn’);if(!btn)return;
var s=q(‘ciS’).value;
var nextStart=dateStr(wkStart(addDays(toDate(s||todayStr()),7)));
btn.disabled=nextStart>todayStr();
btn.style.opacity=nextStart>todayStr()?‘0.3’:‘1’;
btn.style.cursor=nextStart>todayStr()?‘not-allowed’:‘pointer’;
}
function ciUpdatePreview(){
var s=q(‘ciS’).value,e=q(‘ciE’).value,el=q(‘ciWeekPreview’);if(!el)return;
if(!s||!e){el.textContent=’’;return;}
var wi=weighIns.filter(function(w){return !w.isBulk&&w.date>=s&&w.date<=e;});
var txt=wi.length?wi.length+’ weigh-in’+(wi.length!==1?‘s’:’’)+’ in range’:‘No weigh-ins in this range — avg weight will need manual entry’;
el.textContent=txt;
}
function ciStartChanged(){
var s=q(‘ciS’).value;if(!s)return;
q(‘ciE’).value=dateStr(addDays(toDate(s),6));
ciUpdateNextBtn();ciUpdatePreview();autoFillWt();
}
function autoFillWt(){
var s=q(‘ciS’).value,e=q(‘ciE’).value;
var al=q(‘ciAutoLbl’),wEl=q(‘ciWt’);
if(!s||!e){if(al)al.textContent=’’;return;}
var wi=weighIns.filter(function(w){return !w.isBulk&&w.date>=s&&w.date<=e;});
if(!wi.length){if(al)al.textContent=’— no logs in range’;return;}
var avg=Math.round(div(wi.reduce(function(a,w){return a+w.weight;},0),wi.length)*100)/100;
if(al)al.textContent=’— auto: ’+dispVal(avg);
if(wEl&&!wEl.value)wEl.value=dispVal(avg);
ciUpdatePreview();
}

/* ============================================================ WEIGH-IN */
function quickLog(){
var dt=q(‘dDate’).value,raw=parseFloat(q(‘dWt’).value);
if(!dt||isNaN(raw)||raw<=0){toast(‘Enter a valid date and weight’,‘err’);return;}
if(dt>todayStr()){toast(‘Cannot log future dates’,‘err’);return;}
var cal=parseInt(q(‘dCal’).value)||null;
addWI(dt,fromDisp(raw),false,cal);q(‘dWt’).value=’’;if(q(‘dCal’))q(‘dCal’).value=’’;toast(‘Logged ‘+fmtW(fromDisp(raw)));
}
function saveWI(){
var dt=q(‘lDate’).value,raw=parseFloat(q(‘lWt’).value);
if(!dt||isNaN(raw)||raw<=0){toast(‘Enter a valid date and weight’,‘err’);return;}
if(dt>todayStr()){toast(‘Cannot log future dates’,‘err’);return;}
var cal=parseInt(q(‘lCal’).value)||null;
addWI(dt,fromDisp(raw),false,cal);q(‘lWt’).value=’’;if(q(‘lCal’))q(‘lCal’).value=’’;toast(‘Weigh-in saved’);
}
function addWI(date,lbs,isBulk,calories){
var idx=weighIns.findIndex(function(w){return w.date===date;});
var id=idx>=0?weighIns[idx].id:‘w-’+Date.now()+’-’+Math.floor(Math.random()*9999);
var en={id:id,date:date,weight:lbs,isBulk:!!isBulk,calories:calories||null};
if(idx>=0)weighIns[idx]=en;else weighIns.push(en);
weighIns.sort(function(a,b){return b.date.localeCompare(a.date);});
Local.set(‘weighIns’,weighIns);refreshAll();renderCal();checkAch(true);
}
function addWISilent(date,lbs,isBulk,calories){
var idx=weighIns.findIndex(function(w){return w.date===date;});
var id=idx>=0?weighIns[idx].id:‘w-’+Date.now()+’-’+Math.floor(Math.random()*9999);
var en={id:id,date:date,weight:lbs,isBulk:!!isBulk,calories:calories||null};
if(idx>=0)weighIns[idx]=en;else weighIns.push(en);
weighIns.sort(function(a,b){return b.date.localeCompare(a.date);});
}
function delWI(id){weighIns=weighIns.filter(function(w){return w.id!==id;});Local.set(‘weighIns’,weighIns);refreshAll();renderCal();}

/* ============================================================ MONTH GROUPING */
function renderByMonth(containerId,items){
var el=q(containerId);if(!el)return;
if(!items||!items.length){el.innerHTML=’<div class="empty" style="padding:24px;"><div class="empty-sub">Nothing here yet.</div></div>’;return;}
var groups={},order=[];
items.forEach(function(w){var mk=mkKey(w.date);if(!groups[mk]){groups[mk]=[];order.push(mk);}groups[mk].push(w);});
order.sort(function(a,b){return b.localeCompare(a);});
var html=’’;
order.forEach(function(mk){
var g=groups[mk];
var avg=div(g.reduce(function(a,w){return a+w.weight;},0),g.length);
var sid=‘wm-’+mk.replace(’-’,’’);
var isOpen=mk===mkKey(todayStr());
html+=’<div class="mg"><div class="mg-hd" onclick="togMG(\''+sid+'\')">’;
html+=’<span class="mg-ttl">’+fmtMY(g[0].date)+’</span>’;
html+=’<span style="display:flex;align-items:center;gap:8px;"><span class="mg-meta">’+g.length+’ log’+(g.length!==1?‘s’:’’)+’ · avg ‘+fmtW(avg)+’</span><span class="mg-chev'+(isOpen?' open':'')+'">▼</span></span>’;
html+=’</div><div class="mg-body'+(isOpen?' open':'')+'" id="'+sid+'">’;
g.forEach(function(w){
var calStr=w.calories?’<span style="font-size:11px;color:var(--t3);margin-left:8px;">’+w.calories.toLocaleString()+’ cal</span>’:’’;
html+=’<div class="wi-row"><div><span class="wi-date">’+fmtFull(w.date)+’</span>’+(w.isBulk?’<span class="bulk-tag">BULK</span>’:’’)+’</div>’;
html+=’<div style="display:flex;align-items:center;">’+calStr+’<span class="wi-val" style="margin-left:8px;">’+fmtW(w.weight)+’</span><button class="wi-del" onclick="delWI(\''+w.id+'\')">×</button></div></div>’;
});
html+=’</div></div>’;
});
el.innerHTML=html;
}
function renderCIByMonth(containerId,items){
var el=q(containerId);if(!el)return;
if(!items||!items.length){el.innerHTML=’<div class="empty" style="padding:24px;"><div class="empty-sub">No check-ins yet.</div></div>’;return;}
var groups={},order=[];
items.forEach(function(c){var mk=mkKey(c.startDate);if(!groups[mk]){groups[mk]=[];order.push(mk);}groups[mk].push(c);});
order.sort(function(a,b){return b.localeCompare(a);});
var html=’’;
order.forEach(function(mk){
var g=groups[mk];
var sid=‘cm-’+mk.replace(’-’,’’);
var isOpen=mk===mkKey(todayStr());
html+=’<div class="mg"><div class="mg-hd" onclick="togMG(\''+sid+'\')">’;
html+=’<span class="mg-ttl">’+fmtMY(g[0].startDate)+’</span>’;
html+=’<span style="display:flex;align-items:center;gap:8px;"><span class="mg-meta">’+g.length+’ check-in’+(g.length!==1?‘s’:’’)+’</span><span class="mg-chev'+(isOpen?' open':'')+'">▼</span></span>’;
html+=’</div><div class="mg-body'+(isOpen?' open':'')+'" id="'+sid+'">’;
g.forEach(function(c){
var wStr=c.avgWeight?fmtW(c.avgWeight):’—’;
var cStr=c.calories?c.calories.toLocaleString()+’ cal’:’—’;
var pill=c.score!=null?’<span class="spill '+sCls(c.score)+'">’+c.score+’</span>’:’’;
html+=’<div class="wi-row" onclick="openWeekM(\''+c.id+'\')" style="cursor:pointer;flex-wrap:wrap;gap:4px;">’;
html+=’<div><span class="wi-date">’+(c.label||fmtFull(c.startDate))+’</span><span class="wi-day">’+fmtD(c.startDate)+’ — ‘+fmtD(c.endDate)+’</span>’+(c.isBulk?’<span class="bulk-tag">BULK</span>’:’’)+’</div>’;
html+=’<div style="display:flex;align-items:center;gap:8px;">’+pill+’<span style="font-size:12px;color:var(--t3);">’+cStr+’</span><span class="wi-val">’+wStr+’</span>’;
html+=’<button class="wi-del" onclick="event.stopPropagation();delCI(\''+c.id+'\')">×</button></div></div>’;
});
html+=’</div></div>’;
});
el.innerHTML=html;
}
function togSection(bodyId,chevId){
var body=q(bodyId),chev=q(chevId);if(!body)return;
var collapsed=body.dataset.collapsed===‘1’;
if(collapsed){body.style.display=’’;body.dataset.collapsed=‘0’;if(chev)chev.style.transform=‘rotate(0deg)’;}
else{body.style.display=‘none’;body.dataset.collapsed=‘1’;if(chev)chev.style.transform=‘rotate(-90deg)’;}
}
function togMG(id){
var el=q(id);if(!el)return;
var open=el.classList.contains(‘open’);el.classList.toggle(‘open’,!open);
var hdr=el.previousElementSibling;
if(hdr){var ch=hdr.querySelector(’.mg-chev’);if(ch)ch.classList.toggle(‘open’,!open);}
}

/* ============================================================ MOOD */
function setMood(v){
selMood=v;
qa(’.mbtn’).forEach(function(b){var bv=parseInt(b.dataset.v);b.style.background=bv<=v?‘var(–accent)’:‘transparent’;b.style.color=bv<=v?’#fff’:‘var(–t2)’;b.style.borderColor=bv<=v?‘var(–accent)’:‘var(–br)’;});
}

/* ============================================================ MACRO BAR */
function setMacMode(m){macMode=m;q(‘macPBtn’).classList.toggle(‘on’,m===‘pct’);q(‘macGBtn’).classList.toggle(‘on’,m===‘g’);updMacBar();}
function updMacBar(){
var p=parseFloat(q(‘ciProt’).value)||0,c=parseFloat(q(‘ciCarb’).value)||0,f=parseFloat(q(‘ciFat’).value)||0;
var w=q(‘macWarn’);
if(macMode===‘pct’&&p+c+f>100){w.style.display=‘block’;w.textContent=‘Macros total ‘+(p+c+f)+’% — should add up to 100%.’;}
else w.style.display=‘none’;
var pp,cp,fp;
if(macMode===‘g’){var kcal=p*4+c*4+f*9;if(!kcal){pp=33;cp=33;fp=34;}else{pp=Math.round(p*4/kcal*100);cp=Math.round(c*4/kcal*100);fp=Math.max(0,100-pp-cp);}}
else{var tot=p+c+f;if(!tot){pp=33;cp=33;fp=34;}else{pp=Math.round(p/tot*100);cp=Math.round(c/tot*100);fp=Math.max(0,100-pp-cp);}}
q(‘macBar’).children[0].style.width=pp+’%’;q(‘macBar’).children[1].style.width=cp+’%’;q(‘macBar’).children[2].style.width=fp+’%’;
q(‘macPv’).textContent=pp+’%’;q(‘macCv’).textContent=cp+’%’;q(‘macFv’).textContent=fp+’%’;
}

/* ============================================================ SCORE SYSTEM
35 = check-in submitted
25 = any non-bulk weigh-in this week
20 = calories logged
20 = weight trending correct direction
*/
function calcScore(ci){
if(ci.isBulk)return null;
var score=35;// submitted
var wi=weighIns.filter(function(w){return !w.isBulk&&ci.startDate&&ci.endDate&&w.date>=ci.startDate&&w.date<=ci.endDate;});
if(wi.length>0)score+=25;
if(ci.calories&&ci.calories>0)score+=20;
var ph=ci.phaseId?phases.find(function(p){return p.id===ci.phaseId;}):null;
var goal=ph?(ph.goal||‘cut’):‘cut’;
var prev=checkins.filter(function(c){return !c.isBulk&&c.avgWeight&&c.startDate<(ci.startDate||‘z’);}).sort(function(a,b){return b.startDate.localeCompare(a.startDate);});
if(prev.length>0&&ci.avgWeight){
var diff=ci.avgWeight-prev[0].avgWeight;
var ok=(goal===‘cut’&&diff<0)||(goal===‘bulk’&&diff>0)||(goal===‘maintain’&&Math.abs(diff)<=0.5);
if(ok)score+=20;
}
return Math.min(score,100);
}
function sCls(s){if(s>=80)return’sg’;if(s>=60)return’sb2’;if(s>=40)return’so’;return’sl’;}

/* ============================================================ CHECK-IN SAVE */
function saveCI(){
var sd=q(‘ciS’).value,ed=q(‘ciE’).value;
if(!sd||!ed){toast(‘Set the week start and end dates’,‘err’);return;}
var p=parseFloat(q(‘ciProt’).value)||0,c=parseFloat(q(‘ciCarb’).value)||0,f=parseFloat(q(‘ciFat’).value)||0;
if(macMode===‘pct’&&p+c+f>100){toast(‘Macros exceed 100%’,‘err’);return;}
var rawWt=parseFloat(q(‘ciWt’).value)||null;
var avgLbs=rawWt?fromDisp(rawWt):null;
if(!avgLbs){
var wi=weighIns.filter(function(w){return !w.isBulk&&w.date>=sd&&w.date<=ed;});
if(wi.length)avgLbs=Math.round(div(wi.reduce(function(a,w){return a+w.weight;},0),wi.length)*100)/100;
}
var phId=q(‘ciPh’).value||null;
if(!phId){var auto=phases.find(function(ph){return ph.startDate<=sd&&(!ph.endDate||ph.endDate>=sd);});if(auto)phId=auto.id;}
var existing=checkins.findIndex(function(c){return c.startDate===sd;});
var id=existing>=0?checkins[existing].id:‘ci-’+Date.now()+’-’+Math.floor(Math.random()*9999);
var en={id:id,label:’’,startDate:sd,endDate:ed,calories:parseInt(q(‘ciCal’).value)||null,targetCal:parseInt(q(‘ciTargetCal’).value)||null,avgWeight:avgLbs,macroMode:macMode,protein:p||null,carbs:c||null,fats:f||null,notes:q(‘ciNotes’).value.trim(),phaseId:phId,sleep:parseFloat(q(‘ciSleep’).value)||null,training:parseInt(q(‘ciTrain’).value)||null,mood:selMood||null,isBulk:false};
en.score=calcScore(en);
if(existing>=0)checkins[existing]=en;else checkins.push(en);
checkins.sort(function(a,b){return b.startDate.localeCompare(a.startDate);});
Local.set(‘checkins’,checkins);
var cp=getCurPhase();
if(cp&&cp.targetWeight&&avgLbs){var hit=(cp.goal===‘cut’&&avgLbs<=cp.targetWeight)||(cp.goal===‘bulk’&&avgLbs>=cp.targetWeight)||(cp.goal===‘maintain’&&Math.abs(avgLbs-cp.targetWeight)<=0.5);if(hit)setTimeout(function(){toast(‘Target weight reached! Consider completing this phase.’,‘info’,5000);},400);}
clearCIForm();refreshAll();checkAch(true);toast(‘Check-in saved’);
}
function clearCIForm(){
[‘ciCal’,‘ciTargetCal’,‘ciWt’,‘ciProt’,‘ciCarb’,‘ciFat’,‘ciNotes’,‘ciSleep’,‘ciTrain’].forEach(function(id){if(q(id))q(id).value=’’;});
if(q(‘ciPh’))q(‘ciPh’).selectedIndex=0;if(q(‘ciAutoLbl’))q(‘ciAutoLbl’).textContent=’’;
selMood=0;qa(’.mbtn’).forEach(function(b){b.style.background=‘transparent’;b.style.color=‘var(–t2)’;b.style.borderColor=‘var(–br)’;});
initDates();updMacBar();
}
function delCI(id){if(!confirm(‘Delete this check-in?’))return;checkins=checkins.filter(function(c){return c.id!==id;});Local.set(‘checkins’,checkins);refreshAll();}

/* ============================================================ PHASES */
function getCurPhase(){var td=todayStr();return phases.find(function(p){return p.startDate<=td&&(!p.endDate||p.endDate>td);})||null;}
function fillPhasePickers(){
[‘ciPh’,‘bpPhase’,‘bmPhase’].forEach(function(pid){
var sel=q(pid);if(!sel)return;
var prev=sel.value;
sel.innerHTML=’<option value="">— ‘+(pid===‘ciPh’?‘No phase’:‘Auto-match by date’)+’ —</option>’;
phases.forEach(function(ph){sel.innerHTML+=’<option value="'+ph.id+'">’+esc(ph.name)+’</option>’;});
if(phases.find(function(p){return p.id===prev;}))sel.value=prev;else sel.selectedIndex=0;
});
// Populate history phase filter separately (different label)
var hSel=q(‘hPhaseFilter’);if(hSel){
var hPrev=hSel.value;
hSel.innerHTML=’<option value="">— All / current filter —</option>’;
phases.slice().sort(function(a,b){return b.startDate.localeCompare(a.startDate);}).forEach(function(ph){
hSel.innerHTML+=’<option value="'+ph.id+'">’+esc(ph.name)+(ph.goal?’ (’+ph.goal+’)’:’’)+’</option>’;
});
if(phases.find(function(p){return p.id===hPrev;}))hSel.value=hPrev;else hSel.selectedIndex=0;
}
}
/* ============================================================ ADAPTIVE CALORIE TARGET */
// Returns the active calorie target for a phase on a given date string.
// Looks through calStages (sorted by date) for the most recent stage on or before the date.
// Falls back to ph.calories for backward compatibility with phases that have no stages.
function getPhaseCalTarget(ph, ds){
if(!ph)return null;
// New system: calStages array
if(ph.calStages&&ph.calStages.length){
var sorted=ph.calStages.slice().sort(function(a,b){return a.date.localeCompare(b.date);});
var active=null;
for(var i=0;i<sorted.length;i++){
if(sorted[i].date<=ds)active=sorted[i].calories;
else break;
}
return active||ph.calories||null;
}
// Legacy: single calories field
return ph.calories||null;
}

// Phase modal calorie stage state
var pmCalStageRows=[];

function pmRenderCalStages(){
var el=q(‘pmCalStages’);if(!el)return;
if(!pmCalStageRows.length){el.innerHTML=’<div style="font-size:12px;color:var(--t4);padding:4px 0;">No calorie target set.</div>’;return;}
var html=’’;
pmCalStageRows.forEach(function(r,i){
var isFirst=i===0;
html+=’<div style="display:flex;gap:8px;align-items:center;">’;
html+=’<div style="flex:1;min-width:120px;"><label class="lbl" style="font-size:9px;">From date</label>’;
if(isFirst){
html+=’<div style="padding:10px 14px;background:var(--bg2);border:1px solid var(--br);border-radius:var(--r10);font-size:13px;color:var(--t3);" id="pmStageDate0">’+(r.date?fmtD(r.date):‘Phase start’)+’</div>’;
}else{
html+=’<input class="inp" type="date" value="'+esc(r.date||'')+'" onchange="pmStageE('+i+',\'date\',this.value)" style="width:100%;">’;
}
html+=’</div>’;
html+=’<div style="flex:1;min-width:100px;"><label class="lbl" style="font-size:9px;">Daily calories</label>’;
html+=’<input class="inp" type="number" value="'+esc(r.calories||'')+'" placeholder="2200" onchange="pmStageE('+i+',\'calories\',this.value)">’;
html+=’</div>’;
if(!isFirst){
html+=’<button type="button" class="wi-del" onclick="pmStageD('+i+')" style="margin-top:18px;flex-shrink:0;">×</button>’;
}else{
html+=’<div style="width:28px;flex-shrink:0;"></div>’;
}
html+=’</div>’;
});
el.innerHTML=html;
}

function pmAddCalStage(){
// Default new stage date: 4 weeks after phase start or after last stage
var sd=q(‘pmStart’)?q(‘pmStart’).value:’’;
var lastDate=pmCalStageRows.length?pmCalStageRows[pmCalStageRows.length-1].date:sd;
var nextDate=lastDate?dateStr(addDays(toDate(lastDate),28)):sd;
pmCalStageRows.push({date:nextDate,calories:’’});
pmRenderCalStages();
}

function pmStageE(i,f,v){
if(pmCalStageRows[i])pmCalStageRows[i][f]=v;
// Keep first stage date synced with phase start
if(i===0&&f===‘date’){var el=q(‘pmStageDate0’);if(el)el.textContent=v?fmtD(v):‘Phase start’;}
}

function pmStageD(i){
pmCalStageRows.splice(i,1);
pmRenderCalStages();
}

// Called when phase start date changes — update first stage date to match
function pmSyncStageDate(){
var sd=q(‘pmStart’)?q(‘pmStart’).value:’’;
if(pmCalStageRows.length){pmCalStageRows[0].date=sd;pmRenderCalStages();}
}

function openPhaseModal(id){
editPhaseId=id||null;q(‘mPhaseTtl’).textContent=id?‘Edit phase’:‘New phase’;
var latest=weighIns.filter(function(w){return !w.isBulk;})[0];
var latestDisp=latest?dispVal(latest.weight):’’;
pmCalStageRows=[];
if(id){
var ph=phases.find(function(p){return p.id===id;});if(!ph)return;
q(‘pmNm’).value=ph.name;q(‘pmGoal’).value=ph.goal||‘cut’;
q(‘pmSW’).value=ph.startWeight?dispVal(ph.startWeight):’’;
q(‘pmTW’).value=ph.targetWeight?dispVal(ph.targetWeight):’’;
q(‘pmTD’).value=ph.targetDate||’’;
q(‘pmRate’).value=ph.weeklyRate?toDisp(ph.weeklyRate).toFixed(2):’’;
q(‘pmStart’).value=ph.startDate;q(‘pmEnd’).value=ph.endDate||’’;
// Populate calorie stages — migrate legacy single calories if needed
if(ph.calStages&&ph.calStages.length){
pmCalStageRows=ph.calStages.map(function(s){return{date:s.date,calories:s.calories};});
}else if(ph.calories){
pmCalStageRows=[{date:ph.startDate,calories:ph.calories}];
}else{
pmCalStageRows=[{date:ph.startDate,calories:’’}];
}
}else{
[‘pmNm’,‘pmTW’,‘pmTD’,‘pmRate’,‘pmEnd’].forEach(function(fid){if(q(fid))q(fid).value=’’;});
q(‘pmGoal’).value=‘cut’;q(‘pmStart’).value=todayStr();q(‘pmSW’).value=latestDisp;
pmCalStageRows=[{date:todayStr(),calories:’’}];
}
pmRenderCalStages();
q(‘pmWarn’).style.display=‘none’;openM(‘mPhase’);
}
function savePhase(){
var nm=q(‘pmNm’).value.trim();if(!nm){toast(‘Enter a phase name’,‘err’);return;}
var sd=q(‘pmStart’).value;if(!sd){toast(‘Set a start date’,‘err’);return;}
var rawSW=parseFloat(q(‘pmSW’).value)||null,rawTW=parseFloat(q(‘pmTW’).value)||null,rawRate=parseFloat(q(‘pmRate’).value)||null;
var sw=rawSW?fromDisp(rawSW):null,tw=rawTW?fromDisp(rawTW):null,rate=rawRate?fromDisp(Math.abs(rawRate)):null;
var td2=q(‘pmTD’).value||null;
// Build calorie stages from pmCalStageRows — keep first stage date locked to phase start
var calStages=[];
pmCalStageRows.forEach(function(r,i){
var cal=parseInt(r.calories)||null;
var stageDate=i===0?sd:(r.date||’’);
if(cal&&stageDate)calStages.push({date:stageDate,calories:cal});
});
// Legacy calories field = first stage value for backward compat with display code
var legacyCal=calStages.length?calStages[0].calories:null;
var warn=’’;
if(sw&&tw&&rate&&td2){
var wLeft=Math.max(1,Math.round((toDate(td2)-new Date())/(7*24*3600*1000)));
var implied=Math.round((sw+(q(‘pmGoal’).value===‘cut’?-1:1)*rate*wLeft)*10)/10;
if(Math.abs(implied-tw)>2)warn=‘At ‘+fmtW(rate,2)+’/wk for ‘+wLeft+’ wks from ‘+fmtW(sw)+’, you'd reach ~‘+fmtW(implied)+’ — but target is ‘+fmtW(tw)+’. Adjust rate or date.’;
}
q(‘pmWarn’).textContent=warn;q(‘pmWarn’).style.display=warn?‘block’:‘none’;
var en={id:editPhaseId||(‘p-’+Date.now()+’-’+Math.floor(Math.random()*9999)),name:nm,goal:q(‘pmGoal’).value,calories:legacyCal,calStages:calStages,startWeight:sw,targetWeight:tw,targetDate:td2,weeklyRate:rate,startDate:sd,endDate:q(‘pmEnd’).value||null};
if(editPhaseId){var idx=phases.findIndex(function(p){return p.id===editPhaseId;});if(idx>=0)phases[idx]=en;}
else phases.push(en);
phases.sort(function(a,b){return b.startDate.localeCompare(a.startDate);});
Local.set(‘phases’,phases);closeM(‘mPhase’);refreshAll();checkAch(true);
}
function delPhase(id){
if(!confirm(‘Delete this phase?’))return;phases=phases.filter(function(p){return p.id!==id;});
checkins.forEach(function(c){if(c.phaseId===id)c.phaseId=null;});
Local.set(‘phases’,phases);Local.set(‘checkins’,checkins);refreshAll();
}
function showPhaseSum(id){
var ph=phases.find(function(p){return p.id===id;});if(!ph)return;
// Live CIs only for scoring/behavioral metrics
var liveCI=checkins.filter(function(c){return c.phaseId===id&&!c.isBulk;}).sort(function(a,b){return a.startDate.localeCompare(b.startDate);});
// All CIs (including bulk) for physique/trend data
var allCI=checkins.filter(function(c){return c.phaseId===id;}).sort(function(a,b){return a.startDate.localeCompare(b.startDate);});
var dur=’–’;
if(ph.startDate){var days=Math.round((toDate(ph.endDate||todayStr())-toDate(ph.startDate))/(24*3600*1000));dur=Math.round(days/7)+’ weeks’;}
// Weight trend uses all CI data (bulk included)
var withW=allCI.filter(function(c){return c.avgWeight;});
var totalChg=withW.length>=2?withW[withW.length-1].avgWeight-withW[0].avgWeight:null;
// Calorie avg from live CIs only
var calCI=liveCI.filter(function(c){return c.calories;});
var avgCal=calCI.length?Math.round(div(calCI.reduce(function(a,c){return a+c.calories;},0),calCI.length)):null;
// Consistency score from live CIs only
var scores=liveCI.filter(function(c){return c.score!=null;});
var avgScore=scores.length?Math.round(div(scores.reduce(function(a,c){return a+c.score;},0),scores.length)):null;
// Best week from all CI data for trend context
var bestStr=’–’;
if(withW.length>=2){
var dels=[];
for(var i=1;i<withW.length;i++)dels.push({w:withW[i],d:withW[i].avgWeight-withW[i-1].avgWeight});
var best=ph.goal===‘cut’?dels.reduce(function(a,b){return b.d<a.d?b:a;}):ph.goal===‘bulk’?dels.reduce(function(a,b){return b.d>a.d?b:a;}):dels.reduce(function(a,b){return Math.abs(b.d)<Math.abs(a.d)?b:a;});
bestStr=(best.d>0?’+’:’’)+fmtW(best.d)+’ (’+fmtD(best.w.startDate)+’)’;
}
var SI=function(v,l){return ‘<div style="background:var(--bg);border-radius:var(--r10);padding:14px;"><div style="font-size:22px;font-weight:700;font-variant-numeric:tabular-nums;">’+v+’</div><div style="font-size:11px;color:var(--t3);text-transform:uppercase;letter-spacing:.06em;font-weight:600;margin-top:4px;">’+l+’</div></div>’;};
var startW=withW.length?withW[0].avgWeight:ph.startWeight;
var endW=withW.length?withW[withW.length-1].avgWeight:null;
var html=’<div style="display:flex;align-items:center;gap:8px;margin-bottom:16px;flex-wrap:wrap;">’;
if(ph.goal)html+=’<span class="badge bc-'+ph.goal+'">’+ph.goal+’</span>’;
html+=’<span class="badge bc-done">✓ Completed ‘+fmtD(ph.endDate)+’</span></div>’;
if(startW&&endW){
var chgStr=totalChg!=null?(’ <strong style="color:'+(totalChg<0?'var(--ok)':'var(--bad)')+';">(’+( totalChg>0?’+’:’’)+fmtW(totalChg)+’)</strong>’):’’;
html+=’<div style="padding:10px 14px;background:var(--bg);border-radius:var(--r10);font-size:13px;color:var(--t2);margin-bottom:12px;">’+fmtW(startW)+’ → ‘+fmtW(endW)+chgStr+’</div>’;
}
html+=’<div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:16px;">’;
html+=SI(dur,‘Duration’);
html+=SI(avgCal?avgCal.toLocaleString()+’ cal’:’–’,‘Avg daily calories’);
html+=SI(avgScore!=null?avgScore+’ / 100’:’–’,‘Avg consistency’);
html+=SI(liveCI.length+’ week’+(liveCI.length!==1?‘s’:’’)+(allCI.length>liveCI.length?’ + ‘+(allCI.length-liveCI.length)+’ bulk’:’’),‘Check-ins’);
html+=’</div>’;
html+=’<div style="padding:12px 16px;background:var(--bg);border-radius:var(--r10);font-size:13px;color:var(--t2);">Best week: ‘+bestStr+’</div>’;
// Measurement delta for this phase
var measDelta=getMeasDeltaForPhase(id,ph.startDate,ph.endDate);
if(measDelta){
html+=’<div style="margin-top:12px;border:1px solid var(--br);border-radius:var(--r10);overflow:hidden;">’;
html+=’<div style="padding:10px 14px;background:var(--bg2);font-size:11px;font-weight:700;color:var(--t3);letter-spacing:.08em;text-transform:uppercase;">Measurement changes</div>’;
Object.values(measDelta).forEach(function(d){
var unit=d.isBf?’%’:’ in’;
var dSign=d.delta>0?’+’:’’;
var dColor=d.delta===0?‘var(–t3)’:(d.label===‘Waist’||d.label===‘Body fat %’)?(d.delta<0?‘var(–ok)’:‘var(–bad)’):(d.delta>0?‘var(–ok)’:‘var(–bad)’);
html+=’<div class="meas-row"><span class="meas-lbl">’+d.label+’</span>’;
html+=’<span style="display:flex;align-items:center;gap:8px;"><span style="font-size:11px;color:var(--t3);">’+d.from+unit+’ → ‘+d.to+unit+’</span><span style="font-size:12px;font-weight:700;color:'+dColor+';">’+dSign+d.delta+unit+’</span></span></div>’;
});
html+=’</div>’;
}
q(‘mCompTtl’).textContent=esc(ph.name);
q(‘mCompBody’).innerHTML=html;
q(‘mCompFt’).innerHTML=’<button class="btn btn-g" onclick="closeM(\'mComplete\')">Close</button><button class="btn btn-p btn-sm" onclick="closeM(\'mComplete\');openPhaseModal(\''+id+'\')" >Edit phase</button>’;
openM(‘mComplete’);
}
function completePhase(id){
var ph=phases.find(function(p){return p.id===id;});if(!ph)return;
// Live CIs for scoring/behavioral metrics only
var liveCI=checkins.filter(function(c){return c.phaseId===id&&!c.isBulk;}).sort(function(a,b){return a.startDate.localeCompare(b.startDate);});
// All CIs including bulk for physique/trend data
var allCI=checkins.filter(function(c){return c.phaseId===id;}).sort(function(a,b){return a.startDate.localeCompare(b.startDate);});
var dur=’—’;
if(ph.startDate){var ed=ph.endDate||todayStr();var days=Math.round((toDate(ed)-toDate(ph.startDate))/(24*3600*1000));dur=Math.round(days/7)+’ weeks’;}
var withW=allCI.filter(function(c){return c.avgWeight;});
var totalChg=withW.length>=2?withW[withW.length-1].avgWeight-withW[0].avgWeight:null;
var calCI=liveCI.filter(function(c){return c.calories;});
var avgCal=calCI.length?Math.round(div(calCI.reduce(function(a,c){return a+c.calories;},0),calCI.length)):null;
var scores=liveCI.filter(function(c){return c.score!=null;});
var avgScore=scores.length?Math.round(div(scores.reduce(function(a,c){return a+c.score;},0),scores.length)):null;
var bestStr=’—’;
if(withW.length>=2){
var dels=[];for(var i=1;i<withW.length;i++)dels.push({w:withW[i],d:withW[i].avgWeight-withW[i-1].avgWeight});
var best=ph.goal===‘cut’?dels.reduce(function(a,b){return b.d<a.d?b:a;}):ph.goal===‘bulk’?dels.reduce(function(a,b){return b.d>a.d?b:a;}):dels.reduce(function(a,b){return Math.abs(b.d)<Math.abs(a.d)?b:a;});
bestStr=(best.d>0?’+’:’’)+fmtW(best.d)+’ (’+fmtD(best.w.startDate)+’)’;
}
q(‘mCompTtl’).textContent=ph.name+’ — Summary’;
var SI=function(v,l){return’<div style="background:var(--bg);border-radius:var(--r10);padding:14px;"><div style="font-size:22px;font-weight:700;font-variant-numeric:tabular-nums;">’+v+’</div><div style="font-size:11px;color:var(--t3);text-transform:uppercase;letter-spacing:.06em;font-weight:600;margin-top:4px;">’+l+’</div></div>’;};
var startW=withW.length?withW[0].avgWeight:ph.startWeight;
var endW=withW.length?withW[withW.length-1].avgWeight:null;
var html=’’;
if(startW&&endW){
var chgStr=totalChg!=null?(’ <strong style="color:'+(totalChg<0?'var(--ok)':'var(--bad)')+';">(’+( totalChg>0?’+’:’’)+fmtW(totalChg)+’)</strong>’):’’;
html+=’<div style="padding:10px 14px;background:var(--bg);border-radius:var(--r10);font-size:13px;color:var(--t2);margin-bottom:12px;">’+fmtW(startW)+’ → ‘+fmtW(endW)+chgStr+’</div>’;
}
html+=’<div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:16px;">’;
html+=SI(dur,‘Duration’);
html+=SI(totalChg!=null?(totalChg>0?’+’:’’)+fmtW(totalChg):’—’,‘Total change’);
html+=SI(avgCal?avgCal.toLocaleString()+’ cal’:’—’,‘Avg daily calories’);
html+=SI(avgScore!=null?avgScore:’—’,‘Avg consistency’);
html+=’</div>’;
html+=’<div style="padding:12px 16px;background:var(--bg);border-radius:var(--r10);font-size:13px;color:var(--t2);margin-bottom:16px;"><span style="color:var(--t1);font-weight:600;">Best week: </span>’+bestStr+’</div>’;
if(allCI.length>liveCI.length)html+=’<div style="font-size:11px;color:var(--t3);margin-bottom:12px;">Weight data includes ‘+(allCI.length-liveCI.length)+’ bulk-imported week’+(allCI.length-liveCI.length!==1?‘s’:’’)+’. Consistency score reflects live check-ins only.</div>’;
html+=’<div style="font-size:13px;color:var(--t2);">Ready to close it out? This will set the end date to today.</div>’;
q(‘mCompBody’).innerHTML=html;
var phId=id;
q(‘mCompFt’).innerHTML=’<button class="btn btn-g" onclick="closeM(\'mComplete\')">Not yet</button><button class="btn btn-s" onclick="finishPhase(\''+phId+'\')">Mark complete & close</button>’;
openM(‘mComplete’);
}
function finishPhase(id){
var ph=phases.find(function(p){return p.id===id;});if(!ph)return;
ph.endDate=todayStr();Local.set(‘phases’,phases);
closeM(‘mComplete’);refreshAll();
toast(‘Phase completed. Start a new one when ready.’);
setTimeout(function(){openPhaseModal();},800);
}
function reopenPhase(id){
var ph=phases.find(function(p){return p.id===id;});if(!ph)return;
// Block if another phase is currently active (would overlap)
var td=todayStr();
var otherActive=phases.find(function(p){return p.id!==id&&p.startDate<=td&&(!p.endDate||p.endDate>td);});
if(otherActive){toast(‘Complete or end “’+esc(otherActive.name)+’” before reopening this phase.’,‘err’,4000);return;}
ph.endDate=null;
Local.set(‘phases’,phases);refreshAll();
toast(esc(ph.name)+’ reopened as active phase.’);
}
function renderPhases(){
var el=q(‘phaseList’);if(!el)return;fillPhasePickers();
if(!phases.length){el.innerHTML=’<div class="empty"><div class="empty-ttl">No phases yet</div><div class="empty-sub">Create your first phase to organize your journey.</div></div>’;return;}
var td=todayStr(),html=’<div class="ph-list">’;
phases.forEach(function(ph){
var isCur=ph.startDate<=td&&(!ph.endDate||ph.endDate>td);
var isDone=ph.endDate&&ph.endDate<=td;
var range=fmtD(ph.startDate)+(ph.endDate?’ — ‘+fmtD(ph.endDate):’ — Present’);
var gBadge=ph.goal?’<span class="badge bc-'+ph.goal+'">’+ph.goal+’</span>’:’’;
var aBadge=isCur?’<span class="badge bc-active">Active</span>’:’’;
var dBadge=isDone?’<span class="badge bc-done">Done</span>’:’’;
var gMeta=’’;
if(ph.startWeight)gMeta+=‘Start: ‘+fmtW(ph.startWeight);
if(ph.targetWeight)gMeta+=(gMeta?’ · ‘:’’)+‘Target: ‘+fmtW(ph.targetWeight);
if(ph.targetDate)gMeta+=(gMeta?’ · ‘:’’)+‘By ‘+fmtD(ph.targetDate);
if(ph.weeklyRate)gMeta+=(gMeta?’ · ‘:’’)+((ph.goal===‘cut’?’-’:’+’)+toDisp(ph.weeklyRate).toFixed(1))+’ ‘+appState.unit+’/wk’;
html+=’<div class="ph-item'+(isCur?' cur':(isDone?' done':''))+'">’;
html+=’<div class=“ph-main” style=“cursor:’+(isDone?‘pointer’:‘default’)+’;”’+(isDone?’ onclick=“showPhaseSum('’+ph.id+’')”’:’’)+’>’;
html+=’<div class="ph-name">’+esc(ph.name)+gBadge+aBadge+dBadge+’</div>’;
html+=’<div class="ph-meta">’+range+’</div>’;
if(gMeta)html+=’<div class="ph-goal">’+gMeta+’</div>’;
html+=’</div>’;
if(ph.calStages&&ph.calStages.length>1){
html+=’<div class="ph-cal"><span style="font-size:11px;font-weight:500;color:var(--t4);">’+ph.calStages.length+’ cal stages</span></div>’;
}else if(ph.calories){
html+=’<div class="ph-cal">’+ph.calories.toLocaleString()+’<span>cal</span></div>’;
}
html+=’<div class="ph-acts">’;
if(isCur)html+=’<button class="btn btn-s btn-xs" onclick="completePhase(\''+ph.id+'\')">Complete</button>’;
else if(isDone)html+=’<button class="btn btn-g btn-xs" onclick="reopenPhase(\''+ph.id+'\')">Reopen</button>’;
html+=’<button class="icon-btn" onclick="openPhaseModal(\''+ph.id+'\')" title="Edit"><svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 20h9"/><path d="M16.5 3.5a2.1 2.1 0 013 3L7 19l-4 1 1-4z"/></svg></button>’;
html+=’<button class="icon-btn" onclick="delPhase(\''+ph.id+'\')" title="Delete"><svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="3 6 5 6 21 6"/><path d="M19 6l-1 14a2 2 0 01-2 2H8a2 2 0 01-2-2L5 6"/></svg></button>’;
html+=’</div></div>’;
});
html+=’</div>’;el.innerHTML=html;
}

/* ============================================================ CALENDAR */
function renderCal(){
var grid=q(‘calGrid’);if(!grid)return;
var MONTHS=[‘January’,‘February’,‘March’,‘April’,‘May’,‘June’,‘July’,‘August’,‘September’,‘October’,‘November’,‘December’];
var ALL_DAYS=[‘Sun’,‘Mon’,‘Tue’,‘Wed’,‘Thu’,‘Fri’,‘Sat’];var dls=[];for(var _di=0;_di<7;_di++)dls.push(ALL_DAYS[(appState.weekStart+_di)%7]);
q(‘calTtl’).textContent=MONTHS[calMonth]+’ ‘+calYear;grid.innerHTML=’’;
dls.forEach(function(l){grid.innerHTML+=’<div class="cal-dl">’+l+’</div>’;});
var first=new Date(calYear,calMonth,1),last=new Date(calYear,calMonth+1,0),td=todayStr();
var sdow=((first.getDay()-appState.weekStart)+7)%7;
for(var i=0;i<sdow;i++)addCC(grid,new Date(calYear,calMonth,-(sdow-1-i)),true,td);
for(var d=1;d<=last.getDate();d++)addCC(grid,new Date(calYear,calMonth,d),false,td);
var edow=((last.getDay()-appState.weekStart)+7)%7;
for(var t=1;t<=6-edow;t++)addCC(grid,new Date(calYear,calMonth+1,t),true,td);
}
function addCC(grid,d,other,td){
var ds=dateStr(d),isFut=ds>td,wi=weighIns.find(function(w){return w.date===ds;});
var cls=‘cal-cell’+(other?’ other’:’’)+(ds===td?’ today’:’’)+(wi?’ has’:’’)+(isFut?’ fut’:’ click’);
var oc=isFut?’’:’ onclick=“selCalDay('’+ds+’')”’;
grid.innerHTML+=’<div class=”’+cls+’”’+oc+’>’+d.getDate()+(wi&&!isFut?’<div class="cal-wt">’+toDisp(wi.weight).toFixed(1)+’</div>’:’’)+’</div>’;
}
function calNav(dir){if(dir===0){calMonth=new Date().getMonth();calYear=new Date().getFullYear();}else{calMonth+=dir;if(calMonth>11){calMonth=0;calYear++;}if(calMonth<0){calMonth=11;calYear–;}}renderCal();}
function selCalDay(ds){
if(ds>todayStr())return;
var det=q(‘calDet’),dtt=q(‘calDetTtl’),body=q(‘calDetBody’),btn=q(‘calDetBtn’);
det.style.display=‘block’;dtt.textContent=fmtDF(ds);
var wi=weighIns.find(function(w){return w.date===ds;});
if(wi){
body.innerHTML=’<div style="font-size:24px;font-weight:700;margin-bottom:4px;">’+fmtW(wi.weight)+’</div><div style="font-size:12px;color:var(--t3);">Morning weigh-in’+(wi.isBulk?’ <span class="bulk-tag">BULK</span>’:’’)+’</div>’;
btn.textContent=‘Edit’;btn.onclick=function(){nav(‘log’);switchLTab(‘wi’);setDF(‘l’,ds);q(‘lWt’).value=dispVal(wi.weight);};
}else{
body.innerHTML=’<div style="color:var(--t3);font-size:13px;">No weigh-in for this day.</div>’;
btn.textContent=‘Log’;btn.onclick=function(){nav(‘log’);switchLTab(‘wi’);setDF(‘l’,ds);};
}
}

/* ============================================================ HISTORY */
function setHRange(r){
appState.hRange=r;
qa(’.hpreset’).forEach(function(b){b.classList.toggle(‘on’,b.dataset.hr===r);});
q(‘hCust’).style.display=r===‘custom’?‘flex’:‘none’;renderHistory();
}
function getFilteredCI(){
var td=todayStr(),from=null,to=null;
// Phase selector takes priority when a specific phase is chosen
var hPhSel=q(‘hPhaseFilter’);
var selPhaseId=hPhSel?hPhSel.value:’’;
if(selPhaseId){
var selPh=phases.find(function(p){return p.id===selPhaseId;});
if(selPh){from=selPh.startDate;to=selPh.endDate||td;}
return checkins.filter(function(c){if(from&&c.startDate<from)return false;if(to&&c.startDate>to)return false;return true;});
}
if(appState.hRange===‘phase’){var cp=getCurPhase();if(cp){from=cp.startDate;to=cp.endDate||td;}else return checkins.slice();}
else if(appState.hRange===‘4w’){var d4=new Date();d4.setDate(d4.getDate()-28);from=dateStr(d4);}
else if(appState.hRange===‘3m’){var d3=new Date();d3.setMonth(d3.getMonth()-3);from=dateStr(d3);}
else if(appState.hRange===‘custom’){from=q(‘hFrom’)?q(‘hFrom’).value:null;to=q(‘hTo’)?q(‘hTo’).value:null;}
return checkins.filter(function(c){if(from&&c.startDate<from)return false;if(to&&c.startDate>to)return false;return true;});
}
function renderHistory(){
var el=q(‘histTl’);if(!el)return;
// Determine if a specific phase is explicitly selected via the phase selector
var hPhSel=q(‘hPhaseFilter’);
var selPhaseId=hPhSel?hPhSel.value:’’;
var selPh=selPhaseId?phases.find(function(p){return p.id===selPhaseId;}):null;
var filt=getFilteredCI();
q(‘hWks’).textContent=filt.length;
var tag={phase:’(this phase)’,‘4w’:’(last 4 wks)’,‘3m’:’(last 3 mo)’,all:’(all time)’,custom:’(custom)’}[appState.hRange]||’’;
if(selPh)tag=’(’+esc(selPh.name)+’)’;
q(‘hRangeTag’).textContent=tag;
var withW=filt.filter(function(c){return c.avgWeight;});
if(withW.length>=2){
var srt=withW.slice().sort(function(a,b){return a.startDate.localeCompare(b.startDate);});
var diff=srt[srt.length-1].avgWeight-srt[0].avgWeight;
q(‘hChange’).textContent=(diff>0?’+’:’’)+fmtW(diff);q(‘hChange’).className=‘stat-val ‘+(diff>0?‘c-ok’:diff<0?‘c-bad’:’’);
q(‘hChangeSub’).textContent=fmtD(srt[0].startDate)+’ → ‘+fmtD(srt[srt.length-1].startDate);
q(‘hAvgRate’).textContent=(div(diff,srt.length-1)>0?’+’:’’)+fmtW(div(diff,srt.length-1))+’/wk’;
}else{q(‘hChange’).textContent=’—’;q(‘hAvgRate’).textContent=’—’;q(‘hChangeSub’).textContent=’—’;}
// Best Week: ONLY visible when a specific phase is explicitly selected via the phase selector
var bestCard=q(‘hBestCard’);
if(selPh&&withW.length>=2){
var phGoal=selPh.goal||‘cut’;
var srt2=withW.slice().sort(function(a,b){return a.startDate.localeCompare(b.startDate);});
var dels=[];for(var i=1;i<srt2.length;i++)dels.push({w:srt2[i],d:srt2[i].avgWeight-srt2[i-1].avgWeight});
var best=phGoal===‘cut’?dels.reduce(function(a,b){return b.d<a.d?b:a;}):phGoal===‘bulk’?dels.reduce(function(a,b){return b.d>a.d?b:a;}):dels.reduce(function(a,b){return Math.abs(b.d)<Math.abs(a.d)?b:a;});
q(‘hBestLbl’).textContent=phGoal===‘cut’?‘Best week (loss)’:phGoal===‘bulk’?‘Best week (gain)’:‘Best week (stable)’;
q(‘hBest’).textContent=(best.d>0?’+’:’’)+fmtW(best.d);q(‘hBestSub’).textContent=fmtD(best.w.startDate);
if(bestCard)bestCard.style.display=’’;
}else{
if(bestCard)bestCard.style.display=‘none’;
}
if(!filt.length){el.innerHTML=’<div class="empty"><div class="empty-ttl">No data in this range</div><div class="empty-sub">Try a wider filter or add more check-ins.</div></div>’;return;}
var secs={},secOrd=[];
filt.forEach(function(c){var k=c.phaseId||’**none**’;if(!secs[k]){secs[k]=[];secOrd.push(k);}secs[k].push(c);});
secOrd=secOrd.filter(function(v,i){return secOrd.indexOf(v)===i;});
var cp=getCurPhase();
var html=’’;
secOrd.forEach(function(key){
var items=secs[key].slice().sort(function(a,b){return a.startDate.localeCompare(b.startDate);});
var phase=key!==’**none**’?phases.find(function(p){return p.id===key;}):null;
var pNm=phase?phase.name:‘Unphased’;
var withW2=items.filter(function(c){return c.avgWeight;});
var pDiff=withW2.length>=2?withW2[withW2.length-1].avgWeight-withW2[0].avgWeight:null;
var pDS=pDiff!=null?(pDiff>0?’+’:’’)+fmtW(pDiff):’’;
var sid=‘ps-’+key.replace(/[^a-z0-9]/gi,’-’);
var isOpen=key===(cp?cp.id:null)||secOrd.length===1||key===selPhaseId;
html+=’<div class="psec"><div class="psec-hd" onclick="togPS(\''+sid+'\')">’;
html+=’<div><div class="psec-ttl">’+esc(pNm)+’</div><div class="psec-meta">’+items.length+’ week’+(items.length!==1?‘s’:’’)+(pDS?’ · ‘+pDS:’’)+’</div></div>’;
html+=’<div style="display:flex;align-items:center;gap:8px;">’+(phase&&phase.goal?’<span class="badge bc-'+phase.goal+'">’+phase.goal+’</span>’:’’)+’ <span class="pchev'+(isOpen?' open':'')+'">▼</span></div></div>’;
html+=’<div class="psec-body'+(isOpen?' open':'')+'" id="'+sid+'">’;
items.forEach(function(c,idx){
var delta=idx>0&&c.avgWeight&&items[idx-1].avgWeight?c.avgWeight-items[idx-1].avgWeight:null;
var dStr=delta!=null?(delta>0?’+’:’’)+fmtW(delta):’—’;
var dCls=delta===null?’’:‘stat-val ‘+(delta>0?‘c-ok’:‘c-bad’);
var pill=c.score!=null?’<span class="spill '+sCls(c.score)+'" style="font-size:10px;">’+c.score+’</span>’:’’;
html+=’<div class="tl-item" onclick="openWeekM(\''+c.id+'\')">’;
html+=’<div class="tl-wk">Wk ‘+(idx+1)+’</div>’;
html+=’<div style="flex:1;min-width:0;"><div class="tl-lbl">’+esc(c.label||fmtFull(c.startDate)+’ — ‘+fmtFull(c.endDate))+(c.isBulk?’<span class="bulk-tag" style="margin-left:6px;">BULK</span>’:’’)+’</div><div class="tl-dt">’+fmtD(c.startDate)+’ — ‘+fmtD(c.endDate)+’</div></div>’;
html+=’<div class="tl-r">’+pill+(c.avgWeight?’<span class="tl-wv">’+fmtW(c.avgWeight)+’</span>’:’’)+’<span class="tl-d '+dCls+'">’+dStr+’</span></div></div>’;
});
html+=’</div></div>’;
});
el.innerHTML=html;
}
function togPS(id){var el=q(id);if(!el)return;var op=el.classList.contains(‘open’);el.classList.toggle(‘open’,!op);var hdr=el.previousElementSibling;if(hdr){var ch=hdr.querySelector(’.pchev’);if(ch)ch.classList.toggle(‘open’,!op);}}

/* ============================================================ WEEK DETAIL */
function openWeekM(id){
var c=checkins.find(function(ci){return ci.id===id;});if(!c)return;
q(‘mWeekTtl’).textContent=c.label||fmtFull(c.startDate)+’ — ‘+fmtFull(c.endDate);
var ph=c.phaseId?phases.find(function(p){return p.id===c.phaseId;}):null;
var html=’<div class="stat-grid" style="margin-bottom:16px;">’;
html+=’<div class="stat-c"><div class="stat-lbl">Avg weight</div><div class="stat-val">’+(c.avgWeight?fmtW(c.avgWeight):’—’)+’</div></div>’;
html+=’<div class="stat-c"><div class="stat-lbl">Avg calories</div><div class="stat-val">’+(c.calories?c.calories.toLocaleString():’—’)+’</div></div>’;
if(c.targetCal)html+=’<div class="stat-c"><div class="stat-lbl">Target calories</div><div class="stat-val">’+c.targetCal.toLocaleString()+’</div></div>’;
if(c.score!=null)html+=’<div class="stat-c"><div class="stat-lbl">Score</div><div class="stat-val"><span class="spill '+sCls(c.score)+'">’+c.score+’</span></div></div>’;
html+=’</div>’;
var ex=[];if(c.mood)ex.push(‘Mood: ‘+c.mood+’/5’);if(c.sleep)ex.push(‘Sleep: ‘+c.sleep+‘h’);if(c.training)ex.push(‘Sessions: ‘+c.training);
if(ex.length)html+=’<div style="display:flex;gap:16px;font-size:13px;color:var(--t2);margin-bottom:12px;flex-wrap:wrap;">’+ex.map(function(e){return’<span>’+e+’</span>’;}).join(’’)+’</div>’;
if(c.protein||c.carbs||c.fats)html+=’<div style="margin-bottom:12px;"><div class="stat-lbl" style="margin-bottom:6px;">Macros (’+(c.macroMode===‘g’?‘g’:’%’)+’)</div><div style="display:flex;gap:16px;font-size:13px;"><span style="color:var(--accent)">P: ‘+(c.protein||’—’)+’</span><span style="color:var(--ok)">C: ‘+(c.carbs||’—’)+’</span><span style="color:var(--warn)">F: ‘+(c.fats||’—’)+’</span></div></div>’;
if(ph)html+=’<div style="font-size:12px;color:var(--t3);margin-bottom:10px;">Phase: <span style="color:var(--accent-b);">’+esc(ph.name)+’</span></div>’;
if(c.isBulk)html+=’<div style="font-size:12px;color:var(--warn);margin-bottom:10px;">Bulk import — not counted toward achievements or goals</div>’;
if(c.notes)html+=’<div style="padding:14px 16px;background:var(--bg);border-radius:var(--r10);font-size:13px;line-height:1.6;color:var(--t2);white-space:pre-wrap;">’+esc(c.notes)+’</div>’;
html+=’<div style="font-size:11px;color:var(--t4);margin-top:14px;">’+fmtFull(c.startDate)+’ — ‘+fmtFull(c.endDate)+’</div>’;
q(‘mWeekBody’).innerHTML=html;openM(‘mWeek’);
}

/* ============================================================ LOG TAB */
function switchLTab(t){qa(’.ltab’).forEach(function(b){b.classList.toggle(‘on’,b.dataset.lt===t);});qa(’.lpanel’).forEach(function(p){p.classList.toggle(‘on’,p.id===‘lp’+t.charAt(0).toUpperCase()+t.slice(1));});}

/* ============================================================ BULK */
function bmAddRow(){
var last=bmRows.length&&bmRows[bmRows.length-1].endDate?toDate(bmRows[bmRows.length-1].endDate):wkEnd(new Date());
var start=addDays(last,1),end=addDays(start,6);
bmRows.push({startDate:dateStr(start),endDate:dateStr(end),weight:’’,calories:’’,notes:’’,phaseId:’’});
renderBMTable();
}
function renderBMTable(){
var tbl=q(‘bmTable’),acts=q(‘bmActs’);
if(!bmRows.length){tbl.innerHTML=’<div style="font-size:13px;color:var(--t3);padding:16px 0;">Click “+ Add row” to start.</div>’;acts.classList.add(‘hidden’);return;}
var phaseOpts=’<option value="">— Auto / global —</option>’;
phases.slice().sort(function(a,b){return b.startDate.localeCompare(a.startDate);}).forEach(function(ph){
phaseOpts+=’<option value="'+ph.id+'">’+esc(ph.name)+’</option>’;
});
var html=’<div class="bt-wrap"><table class="bt"><thead><tr><th>Start date</th><th>End date</th><th>Weight (’+appState.unit+’)</th><th>Calories</th><th>Phase</th><th>Notes</th><th></th></tr></thead><tbody>’;
bmRows.forEach(function(r,i){
html+=’<tr><td><input type="date" value="'+r.startDate+'" max="'+todayStr()+'" onchange="bmE('+i+',\'startDate\',this.value)" style="min-width:130px;"></td>’;
html+=’<td><input type="date" value="'+r.endDate+'" max="'+todayStr()+'" onchange="bmE('+i+',\'endDate\',this.value)" style="min-width:130px;"></td>’;
html+=’<td><input type="number" step="0.1" value="'+r.weight+'" onchange="bmE('+i+',\'weight\',this.value)" style="width:80px;"></td>’;
html+=’<td><input type="number" value="'+r.calories+'" onchange="bmE('+i+',\'calories\',this.value)" style="width:90px;"></td>’;
html+=’<td><select onchange="bmE('+i+',\'phaseId\',this.value)" style="min-width:130px;padding:7px 9px;background:transparent;border:1px solid transparent;border-radius:var(--r6);font-size:13px;color:var(--t1);">’+phaseOpts.replace(‘value=”’+esc(r.phaseId||’’)+’”’,‘value=”’+esc(r.phaseId||’’)+’” selected’)+’</select></td>’;
html+=’<td><input type="text" value="'+esc(r.notes)+'" onchange="bmE('+i+',\'notes\',this.value)" style="min-width:140px;"></td>’;
html+=’<td><button class="wi-del" onclick="bmD('+i+')">×</button></td></tr>’;
});
html+=’</tbody></table></div>’;tbl.innerHTML=html;acts.classList.remove(‘hidden’);
}
function bmE(i,f,v){if(bmRows[i])bmRows[i][f]=v;}
function bmD(i){bmRows.splice(i,1);renderBMTable();}
function bmClear(){bmRows=[];renderBMTable();}
function saveManual(){
if(!bmRows.length)return;
var overPh=q(‘bmPhase’).value||null,saved=0;
bmRows.forEach(function(r,i){
if(!r.startDate)return;
var rawW=parseFloat(r.weight)||null,wLbs=rawW?fromDisp(rawW):null;
if(wLbs&&r.startDate)addWISilent(r.startDate,wLbs,true);
// Priority: per-row phase > global override > auto-match by date
var phId=r.phaseId||overPh||null;
if(!phId){var auto=phases.find(function(p){return p.startDate<=r.startDate&&(!p.endDate||p.endDate>=r.startDate);});if(auto)phId=auto.id;}
var en={id:‘ci-’+Date.now()+’-’+i+’-’+Math.floor(Math.random()*9999),label:’’,startDate:r.startDate,endDate:r.endDate||dateStr(addDays(toDate(r.startDate),6)),calories:parseInt(r.calories)||null,avgWeight:wLbs,macroMode:‘pct’,protein:null,carbs:null,fats:null,notes:r.notes||’’,phaseId:phId,isBulk:true,score:null};
var ex=checkins.findIndex(function(c){return c.startDate===en.startDate&&c.isBulk;});
if(ex>=0)checkins[ex]=en;else checkins.push(en);saved++;
});
checkins.sort(function(a,b){return b.startDate.localeCompare(a.startDate);});
Local.set(‘checkins’,checkins);Local.set(‘weighIns’,weighIns);
bmClear();refreshAll();toast(saved+’ week’+(saved!==1?‘s’:’’)+’ imported as bulk’);
}

/* ============================================================ MEASUREMENTS */
var MEAS_FIELDS=[
{id:‘mWaist’,key:‘waist’,label:‘Waist’},
{id:‘mChest’,key:‘chest’,label:‘Chest’},
{id:‘mHips’,key:‘hips’,label:‘Hips’},
{id:‘mArmL’,key:‘armL’,label:‘Left arm’},
{id:‘mArmR’,key:‘armR’,label:‘Right arm’},
{id:‘mThighL’,key:‘thighL’,label:‘Left thigh’},
{id:‘mThighR’,key:‘thighR’,label:‘Right thigh’},
{id:‘mBf’,key:‘bf’,label:‘Body fat %’}
];

function initMeasDate(){
var el=q(‘measDate’);if(!el)return;
if(!el.value)el.value=todayStr();
el.max=todayStr();
updateMeasNavBtns();
onMeasDateChange();
}

function updateMeasNavBtns(){
var el=q(‘measDate’);if(!el)return;
var nb=q(‘measNextBtn’),tb=q(‘measTodayBtn’);
if(nb)nb.disabled=el.value>=todayStr();
if(tb)tb.classList.toggle(‘is-today’,el.value===todayStr());
}

function stepMeasDate(dir){
var el=q(‘measDate’);if(!el)return;
var cur=el.value||todayStr();
var nxt=dateStr(addDays(toDate(cur),dir));
if(nxt>todayStr())return;
el.value=nxt;
updateMeasNavBtns();
onMeasDateChange();
}

function setMeasToday(){
var el=q(‘measDate’);if(!el)return;
el.value=todayStr();
updateMeasNavBtns();
onMeasDateChange();
}

function onMeasDateChange(){
// Pre-fill fields if an entry exists for this date
var el=q(‘measDate’);if(!el)return;
var existing=measurements.find(function(m){return m.date===el.value;});
MEAS_FIELDS.forEach(function(f){
var inp=q(f.id);if(!inp)return;
inp.value=existing&&existing[f.key]!=null?existing[f.key]:’’;
});
var notesEl=q(‘mNotes’);
if(notesEl)notesEl.value=existing&&existing.notes?existing.notes:’’;
updateMeasNavBtns();
}

function clearMeasForm(){
MEAS_FIELDS.forEach(function(f){var inp=q(f.id);if(inp)inp.value=’’;});
var notesEl=q(‘mNotes’);if(notesEl)notesEl.value=’’;
var el=q(‘measDate’);if(el){el.value=todayStr();updateMeasNavBtns();}
}

function saveMeas(){
var el=q(‘measDate’);
var ds=el?el.value:todayStr();
if(!ds||ds>todayStr()){toast(‘Date cannot be in the future’,‘err’);return;}
// Require at least one field filled
var hasData=MEAS_FIELDS.some(function(f){var v=parseFloat(q(f.id).value);return !isNaN(v)&&v>0;});
if(!hasData){toast(‘Enter at least one measurement’,‘err’);return;}
var en={id:‘ms-’+Date.now()+’-’+Math.floor(Math.random()*9999),date:ds};
MEAS_FIELDS.forEach(function(f){
var v=parseFloat(q(f.id).value);
en[f.key]=(!isNaN(v)&&v>0)?v:null;
});
en.notes=q(‘mNotes’)?q(‘mNotes’).value.trim():’’;
// Upsert — replace existing entry for same date
var idx=measurements.findIndex(function(m){return m.date===ds;});
if(idx>=0)measurements[idx]=en;else measurements.push(en);
measurements.sort(function(a,b){return b.date.localeCompare(a.date);});
Local.set(‘measurements’,measurements);
renderMeasurements();
toast(‘Measurement saved’);
}

function delMeas(id){
if(!confirm(‘Delete this measurement entry?’))return;
measurements=measurements.filter(function(m){return m.id!==id;});
Local.set(‘measurements’,measurements);
renderMeasurements();
}

function renderMeasurements(){
var el=q(‘measList’);if(!el)return;
if(!measurements.length){
el.innerHTML=’<div class="empty" style="padding:24px;"><div class="empty-sub">No measurements logged yet. Log your first entry above.</div></div>’;
return;
}
// Group by month
var groups={},order=[];
measurements.forEach(function(m){
var mk=mkKey(m.date);
if(!groups[mk]){groups[mk]=[];order.push(mk);}
groups[mk].push(m);
});
order.sort(function(a,b){return b.localeCompare(a);});
var html=’’;
order.forEach(function(mk){
var g=groups[mk];
var sid=‘mm-’+mk.replace(’-’,’’);
var isOpen=mk===mkKey(todayStr());
html+=’<div class="mg"><div class="mg-hd" onclick="togMG(\''+sid+'\')">’;
html+=’<span class="mg-ttl">’+fmtMY(g[0].date)+’</span>’;
html+=’<span style="display:flex;align-items:center;gap:8px;"><span class="mg-meta">’+g.length+’ entr’+(g.length!==1?‘ies’:‘y’)+’</span><span class="mg-chev'+(isOpen?' open':'')+'">▼</span></span>’;
html+=’</div><div class="mg-body'+(isOpen?' open':'')+'" id="'+sid+'">’;
g.forEach(function(m){
// Find previous entry to show delta
var prev=measurements.find(function(p){return p.date<m.date;});
html+=’<div class="meas-entry">’;
html+=’<div class="meas-entry-hd">’;
html+=’<span class="meas-entry-date">’+fmtFull(m.date)+’</span>’;
html+=’<button class="wi-del" onclick="delMeas(\''+m.id+'\')" title="Delete">×</button>’;
html+=’</div>’;
html+=’<div class="meas-entry-body">’;
var hasAny=false;
MEAS_FIELDS.forEach(function(f){
if(m[f.key]==null)return;
hasAny=true;
var unit=f.key===‘bf’?’%’:’ in’;
var deltaHtml=’’;
if(prev&&prev[f.key]!=null){
var d=Math.round((m[f.key]-prev[f.key])*10)/10;
var cls=d===0?‘neu’:(f.key===‘waist’||f.key===‘hips’||f.key===‘thighL’||f.key===‘thighR’||f.key===‘bf’)
?(d<0?‘pos’:‘neg’):(d>0?‘pos’:‘neg’);
if(d!==0)deltaHtml=’<span class="meas-delta '+cls+'">’+(d>0?’+’:’’)+d+unit+’</span>’;
}
html+=’<div class="meas-row"><span class="meas-lbl">’+f.label+’</span>’;
html+=’<span style="display:flex;align-items:center;"><span class="meas-val">’+m[f.key]+unit+’</span>’+deltaHtml+’</span></div>’;
});
if(!hasAny)html+=’<div style="padding:12px 16px;font-size:12px;color:var(--t3);">No fields recorded.</div>’;
if(m.notes)html+=’<div style="padding:8px 16px 12px;font-size:12px;color:var(--t3);line-height:1.5;border-top:1px solid var(--br);margin-top:4px;">’+esc(m.notes)+’</div>’;
html+=’</div></div>’;
});
html+=’</div></div>’;
});
el.innerHTML=html;
}

/* ============================================================ MEASUREMENT PHASE SUMMARY HELPER */
function getMeasDeltaForPhase(phaseId,startDate,endDate){
// Find earliest and latest measurement entries within a phase date range
var ph=phases.find(function(p){return p.id===phaseId;});
var from=startDate||(ph?ph.startDate:null);
var to=endDate||(ph?ph.endDate||todayStr():todayStr());
if(!from)return null;
var inRange=measurements.filter(function(m){return m.date>=from&&m.date<=to;})
.sort(function(a,b){return a.date.localeCompare(b.date);});
if(inRange.length<2)return null;
var first=inRange[0],last=inRange[inRange.length-1];
var deltas={};
MEAS_FIELDS.forEach(function(f){
if(first[f.key]!=null&&last[f.key]!=null){
deltas[f.key]={from:first[f.key],to:last[f.key],delta:Math.round((last[f.key]-first[f.key])*10)/10,label:f.label,isBf:f.key===‘bf’};
}
});
return Object.keys(deltas).length?deltas:null;
}
function openM(id){q(id).classList.add(‘open’);}
function closeM(id){q(id).classList.remove(‘open’);}
q(‘mPhase’).addEventListener(‘click’,function(e){if(e.target===q(‘mPhase’))closeM(‘mPhase’);});
q(‘mIntel’).addEventListener(‘click’,function(e){if(e.target===q(‘mIntel’))closeM(‘mIntel’);});
q(‘mWeek’).addEventListener(‘click’,function(e){if(e.target===q(‘mWeek’))closeM(‘mWeek’);});
q(‘mComplete’).addEventListener(‘click’,function(e){if(e.target===q(‘mComplete’))closeM(‘mComplete’);});
q(‘mReassign’).addEventListener(‘click’,function(e){if(e.target===q(‘mReassign’))closeM(‘mReassign’);});

/* ============================================================ REASSIGN BULK DATA */
function openReassignModal(){
var sel=q(‘raBatchPhase’);
if(sel){
sel.innerHTML=’<option value="">— Select a phase —</option>’;
phases.slice().sort(function(a,b){return b.startDate.localeCompare(a.startDate);}).forEach(function(ph){
sel.innerHTML+=’<option value="'+ph.id+'">’+esc(ph.name)+(ph.goal?’ (’+ph.goal+’)’:’’)+’</option>’;
});
}
var unphased=checkins.filter(function(c){return c.isBulk&&!c.phaseId;});
var sub=q(‘raUnphasedCount’);
if(sub)sub.textContent=unphased.length+’ unphased bulk check-in’+(unphased.length!==1?‘s’:’’)+’ found.’;
var rsub=q(‘reassignSub’);
var bulkTotal=checkins.filter(function(c){return c.isBulk;}).length;
if(rsub)rsub.textContent=bulkTotal+’ bulk check-in’+(bulkTotal!==1?‘s’:’’)+’ · ‘+unphased.length+’ unphased’;
renderReassignList();
openM(‘mReassign’);
}
function renderReassignList(){
var el=q(‘raList’);if(!el)return;
var bulk=checkins.filter(function(c){return c.isBulk;})
.slice().sort(function(a,b){return b.startDate.localeCompare(a.startDate);});
if(!bulk.length){
el.innerHTML=’<div style="padding:20px;text-align:center;font-size:13px;color:var(--t3);">No bulk check-ins found.</div>’;
return;
}
var phaseOpts=’<option value="">— No phase —</option>’;
phases.slice().sort(function(a,b){return b.startDate.localeCompare(a.startDate);}).forEach(function(ph){
phaseOpts+=’<option value="'+ph.id+'">’+esc(ph.name)+’</option>’;
});
var html=’’;
bulk.forEach(function(c){
var ph=c.phaseId?phases.find(function(p){return p.id===c.phaseId;}):null;
var wStr=c.avgWeight?fmtW(c.avgWeight):’—’;
// Build select with correct option selected
var selHtml=’<select onchange="raSetPhase(\''+c.id+'\',this.value)" style="font-size:12px;padding:5px 8px;background:var(--bg);border:1px solid var(--br);border-radius:var(--r6);color:var(--t1);min-width:140px;">’;
selHtml+=’<option value=””’+(c.phaseId?’’:’ selected’)+’>— No phase —</option>’;
phases.slice().sort(function(a,b){return b.startDate.localeCompare(a.startDate);}).forEach(function(p){
selHtml+=’<option value=”’+p.id+’”’+(c.phaseId===p.id?’ selected’:’’)+’>’+esc(p.name)+’</option>’;
});
selHtml+=’</select>’;
html+=’<div style="display:flex;align-items:center;justify-content:space-between;padding:10px 14px;border-bottom:1px solid var(--br);gap:10px;flex-wrap:wrap;">’;
html+=’<div><div style="font-size:13px;font-weight:500;">’+fmtD(c.startDate)+’ — ‘+fmtD(c.endDate)+’</div>’;
html+=’<div style="font-size:11px;color:var(--t3);margin-top:2px;">’+wStr+(c.calories?’ · ‘+c.calories.toLocaleString()+’ cal’:’’)+(ph?’ · <span style="color:var(--accent-b);">’+esc(ph.name)+’</span>’:’ · <span style="color:var(--t4);">Unphased</span>’)+’</div></div>’;
html+=selHtml+’</div>’;
});
el.innerHTML=html;
}
function raSetPhase(id,phaseId){
var ci=checkins.find(function(c){return c.id===id;});
if(!ci)return;
ci.phaseId=phaseId||null;
Local.set(‘checkins’,checkins);
var unphased=checkins.filter(function(c){return c.isBulk&&!c.phaseId;});
var sub=q(‘raUnphasedCount’);
if(sub)sub.textContent=unphased.length+’ unphased bulk check-in’+(unphased.length!==1?‘s’:’’)+’ found.’;
var rsub=q(‘reassignSub’);
var bulkTotal=checkins.filter(function(c){return c.isBulk;}).length;
if(rsub)rsub.textContent=bulkTotal+’ bulk check-in’+(bulkTotal!==1?‘s’:’’)+’ · ‘+unphased.length+’ unphased’;
refreshAll();
toast(‘Phase updated’);
}
function raBatchAssign(){
var sel=q(‘raBatchPhase’);
var phId=sel?sel.value:’’;
if(!phId){toast(‘Select a phase first’,‘err’);return;}
var unphased=checkins.filter(function(c){return c.isBulk&&!c.phaseId;});
if(!unphased.length){toast(‘No unphased bulk check-ins to assign’,‘err’);return;}
unphased.forEach(function(c){c.phaseId=phId;});
Local.set(‘checkins’,checkins);
renderReassignList();
var remaining=checkins.filter(function(c){return c.isBulk&&!c.phaseId;});
var sub=q(‘raUnphasedCount’);
if(sub)sub.textContent=remaining.length+’ unphased bulk check-in’+(remaining.length!==1?‘s’:’’)+’ found.’;
var rsub=q(‘reassignSub’);
var bulkTotal=checkins.filter(function(c){return c.isBulk;}).length;
if(rsub)rsub.textContent=bulkTotal+’ bulk check-in’+(bulkTotal!==1?‘s’:’’)+’ · ‘+remaining.length+’ unphased’;
refreshAll();
toast(unphased.length+’ check-in’+(unphased.length!==1?‘s’:’’)+’ assigned’,‘ok’);
}

/* ============================================================ ACHIEVEMENTS */
var ADEFS=[
{id:‘first_log’,name:‘First log’,desc:‘Logged your first weigh-in’,maj:false,icon:‘✓’,chk:function(){return weighIns.filter(function(w){return !w.isBulk;}).length>=1;}},
{id:‘first_ci’,name:‘First check-in’,desc:‘Submitted your first weekly check-in’,maj:false,icon:‘✓’,chk:function(){return checkins.filter(function(c){return !c.isBulk;}).length>=1;}},
{id:‘streak_2’,name:‘2-week streak’,desc:‘2 consecutive check-ins’,maj:false,icon:‘✓’,chk:function(){return ciStreak()>=2;}},
{id:‘streak_4’,name:‘4-week streak’,desc:‘4 consecutive check-ins’,maj:true,icon:‘★’,chk:function(){return ciStreak()>=4;}},
{id:‘streak_8’,name:‘8-week streak’,desc:‘8 consecutive check-ins’,maj:true,icon:‘★’,chk:function(){return ciStreak()>=8;}},
{id:‘first_phase’,name:‘Phase created’,desc:‘Created your first training phase’,maj:false,icon:‘✓’,chk:function(){return phases.length>=1;}},
{id:‘goal_5’,name:‘First 5 lbs’,desc:‘5 lbs of progress toward goal’,maj:true,icon:‘★’,chk:function(){return goalProg()>=5;}},
{id:‘goal_10’,name:‘10 lbs milestone’,desc:‘10 lbs of progress toward goal’,maj:true,icon:‘★’,chk:function(){return goalProg()>=10;}},
{id:‘score_80_3’,name:‘Consistent’,desc:‘Scored 80+ three weeks running’,maj:false,icon:‘✓’,chk:function(){return hiScoreStr(80,3);}},
{id:‘cis_10’,name:‘10 check-ins’,desc:‘10 weekly check-ins submitted’,maj:false,icon:‘✓’,chk:function(){return checkins.filter(function(c){return !c.isBulk;}).length>=10;}},
{id:‘cis_52’,name:‘Full year’,desc:‘52 weekly check-ins logged’,maj:true,icon:‘★’,chk:function(){return checkins.filter(function(c){return !c.isBulk;}).length>=52;}}
];
function ciStreak(){var live=checkins.filter(function(c){return !c.isBulk;}).sort(function(a,b){return b.startDate.localeCompare(a.startDate);});if(!live.length)return 0;var s=1;for(var i=1;i<live.length;i++){var df=Math.round((toDate(live[i-1].startDate)-toDate(live[i].startDate))/(7*24*3600*1000));if(df<=1)s++;else break;}return s;}
function goalProg(){var cp=getCurPhase();if(!cp||!cp.targetWeight)return 0;var liveWI=weighIns.filter(function(w){return !w.isBulk;});if(!liveWI.length)return 0;var pCI=checkins.filter(function(c){return c.phaseId===cp.id&&c.avgWeight&&!c.isBulk;}).sort(function(a,b){return a.startDate.localeCompare(b.startDate);});var sw=pCI.length?pCI[0].avgWeight:(cp.startWeight||liveWI[liveWI.length-1].weight);return Math.abs(liveWI[0].weight-sw);}
function hiScoreStr(min,n){var live=checkins.filter(function(c){return !c.isBulk;}).sort(function(a,b){return b.startDate.localeCompare(a.startDate);});var s=0;for(var i=0;i<live.length;i++){if((live[i].score||0)>=min)s++;else break;}return s>=n;}
function checkAch(celebrate){
var earned=Local.get(‘earnedAch’,{});var newU=[];
ADEFS.forEach(function(def){if(!earned[def.id]&&def.chk()){earned[def.id]=todayStr();newU.push(def);}});
if(newU.length){Local.set(‘earnedAch’,earned);if(celebrate){var maj=newU.filter(function(a){return a.maj;});if(maj.length)setTimeout(function(){showCel(maj[0]);},500);else toast(‘Achievement: ‘+newU[0].name,‘ok’);}}
renderAch();
}
function showCel(def){q(‘celIc’).textContent=def.icon;q(‘celTtl’).textContent=def.name;q(‘celSub’).textContent=def.desc;q(‘celOv’).classList.add(‘on’);}
function closeCel(){q(‘celOv’).classList.remove(‘on’);}
function renderAch(){
var el=q(‘settAch’);if(!el)return;
var earned=Local.get(‘earnedAch’,{}),streak=ciStreak();
var liveCI=checkins.filter(function(c){return !c.isBulk;});
var html=’<div class="ach-grid" style="padding:12px 16px;">’;
ADEFS.forEach(function(def){
var isE=!!earned[def.id];
html+=’<div class="ach-item'+(isE?' earn'+(def.maj?' maj':''):'')+'"><div class="ach-ic'+(isE?' '+(def.maj?'maj':'earn'):'')+'">’+(isE?def.icon:‘○’)+’</div>’;
html+=’<div class="ach-meta"><div class="ach-nm">’+def.name+’</div><div class="ach-desc">’+def.desc+’</div></div>’;
html+=’<div class="ach-r">’;
if(isE){html+=’<div class="ach-date">’+fmtD(earned[def.id])+’</div>’;}
else if(def.id===‘streak_2’||def.id===‘streak_4’||def.id===‘streak_8’){var n=def.id===‘streak_2’?2:def.id===‘streak_4’?4:8;html+=’<div class="ach-prog">’+streak+’ / ‘+n+’</div><div class="ach-pbar"><div class="ach-pfill" style="width:'+Math.min(100,Math.round(streak/n*100))+'%"></div></div>’;}
else if(def.id===‘cis_10’||def.id===‘cis_52’){var n2=def.id===‘cis_10’?10:52;html+=’<div class="ach-prog">’+liveCI.length+’ / ‘+n2+’</div><div class="ach-pbar"><div class="ach-pfill" style="width:'+Math.min(100,Math.round(liveCI.length/n2*100))+'%"></div></div>’;}
else{html+=’<div class="ach-prog">Locked</div>’;}
html+=’</div></div>’;
});
html+=’</div>’;el.innerHTML=html;
}

/* ============================================================ WALKTHROUGH */
var WT_STEPS=[
{title:‘Welcome to STRATUM’,text:‘Your personal physique record system. STRATUM stores, structures, and interprets your bodyweight and calorie data over time — so you can understand your trend, not just today's number. Brick by brick.’},
{title:‘Log your daily weight’,text:‘Each morning, log your weight using the Log tab or the quick entry on the dashboard. You can also log optional daily calories alongside each entry. STRATUM uses these daily logs to calculate your weekly average automatically — no manual math needed.’},
{title:‘Weekly check-ins’,text:‘Once a week, complete a check-in. Your average weight auto-fills from your daily logs for that week. Add calories, macros, notes, and a weekly target calorie goal. Check-ins are the primary data source for trend analysis and the TDEE engine.’},
{title:‘Phases & goals’,text:‘Create a phase to give your training a name and direction — Cut, Bulk, or Maintain. Set a target weight, rate, and date. STRATUM will cross-check the math and track your progress automatically. Complete a phase when done for a full summary.’},
{title:‘Trend Analysis’,text:‘The Trend Analysis card on your dashboard estimates your maintenance calories from your actual results — not just a formula. Once you have 2+ check-ins with calories logged, it switches from a formula estimate to an adaptive estimate built from your real data.’},
{title:‘Achievements’,text:‘Hit milestones and earn permanent badges. Eleven to unlock, from your first log to a full year of check-ins. Bulk-imported data does not count toward achievements.’},
{title:“You’re ready”,text:‘The Help page has the full guide. Progress charts, history by phase, and trend analysis all improve the more data you log. Now build something. Brick by brick.’}
];
function startWT(){wtStep=0;renderWTStep();q(‘wtOv’).classList.add(‘on’);q(‘wtCard’).classList.add(‘on’);}
function renderWTStep(){var s=WT_STEPS[wtStep];q(‘wtStep’).textContent=‘Step ‘+(wtStep+1)+’ of ‘+WT_STEPS.length;q(‘wtTtl’).innerHTML=s.title;q(‘wtTxt’).innerHTML=s.text;q(‘wtNextBtn’).textContent=wtStep===WT_STEPS.length-1?‘Finish’:‘Next’;var dots=’’;for(var i=0;i<WT_STEPS.length;i++)dots+=’<div class="wt-dot'+(i===wtStep?' on':'')+'"></div>’;q(‘wtDots’).innerHTML=dots;}
function wtNext(){if(wtStep<WT_STEPS.length-1){wtStep++;renderWTStep();}else skipWT();}
function skipWT(){q(‘wtOv’).classList.remove(‘on’);q(‘wtCard’).classList.remove(‘on’);Local.set(‘wtSeen’,true);}
q(‘wtOv’).addEventListener(‘click’,skipWT);

/* ============================================================ HELP */
function scrollHelp(id){var el=q(‘help-’+id);nav(‘help’);if(el)setTimeout(function(){el.scrollIntoView({behavior:‘smooth’,block:‘start’});},100);}

/* ============================================================ DASHBOARD */
function refreshDash(){
var u=appState.unit;
if(q(‘dWtLbl’))q(‘dWtLbl’).textContent=‘Weight (’+u+’)’;
if(q(‘lWtLbl’))q(‘lWtLbl’).textContent=‘Weight (’+u+’)’;
qa(’.ulbl’).forEach(function(el){el.textContent=u;});
var liveWI=weighIns.filter(function(w){return !w.isBulk;});
if(liveWI.length){q(‘dWeight’).textContent=toDisp(liveWI[0].weight).toFixed(1);q(‘dWeightSub’).textContent=fmtD(liveWI[0].date);}
else{q(‘dWeight’).textContent=’—’;q(‘dWeightSub’).textContent=‘No weigh-ins yet’;}
var ws=dateStr(wkStart(new Date())),we=dateStr(wkEnd(new Date()));
var wWI=liveWI.filter(function(w){return w.date>=ws&&w.date<=we;});
if(wWI.length){var avg=Math.round(div(wWI.reduce(function(a,w){return a+w.weight;},0),wWI.length)*100)/100;q(‘dAvg’).textContent=toDisp(avg).toFixed(1);q(‘dAvgSub’).textContent=wWI.length+’ log’+(wWI.length!==1?‘s’:’’)+’ this week’;if(q(‘lWeekAvg’))q(‘lWeekAvg’).textContent=‘Avg: ‘+toDisp(avg).toFixed(1)+’ ‘+u;}
else{q(‘dAvg’).textContent=’—’;q(‘dAvgSub’).textContent=‘This week’;if(q(‘lWeekAvg’))q(‘lWeekAvg’).textContent=‘Avg: —’;}
var sCI=checkins.filter(function(c){return c.avgWeight&&!c.isBulk;}).sort(function(a,b){return b.startDate.localeCompare(a.startDate);});
if(sCI.length>=2){var rate=sCI[0].avgWeight-sCI[1].avgWeight;q(‘dRate’).textContent=(rate>0?’+’:’’)+fmtW(rate);q(‘dRate’).className=‘stat-val ‘+(rate>0?‘c-ok’:rate<0?‘c-bad’:’’);}
else{q(‘dRate’).textContent=’—’;q(‘dRateSub’).textContent=‘vs last check-in’;q(‘dRate’).className=‘stat-val’;}
var cp=getCurPhase();
if(cp){var cpCal=getPhaseCalTarget(cp,todayStr());q(‘dPhase’).textContent=cp.name;q(‘dPhaseSub’).textContent=cpCal?cpCal.toLocaleString()+’ cal target’:(cp.goal||‘Active’);}
else{q(‘dPhase’).textContent=’—’;q(‘dPhaseSub’).textContent=‘No active phase’;}
var nm=(appState.profile&&appState.profile.display_name)||‘Friend’;
var hr=new Date().getHours();var greet=hr<5?‘Up late’:hr<12?‘Good morning’:hr<17?‘Good afternoon’:‘Good evening’;
q(‘heroTtl’).textContent=greet+’, ‘+nm+’.’;
if(!liveWI.length&&!checkins.filter(function(c){return !c.isBulk;}).length){
q(‘heroLbl’).textContent=’— Getting started’;q(‘heroSub’).textContent=‘Log your first weigh-in to start tracking.’;
q(‘heroCta’).style.display=‘flex’;q(‘goalBarWrap’).style.display=‘none’;q(‘heroStats’).style.display=‘none’;q(‘heroRow’).innerHTML=’’;
}else{
q(‘heroLbl’).textContent=’— This week’;q(‘heroCta’).style.display=‘none’;
var phRow=’’;
if(cp){
var tCls=‘h-trend ok’,tTxt=‘On track’;
if(sCI.length>=2){var n=Math.min(3,sCI.length),tRate=div(sCI[0].avgWeight-sCI[n-1].avgWeight,n-1);var onDir=(cp.goal===‘cut’&&tRate<-0.05)||(cp.goal===‘bulk’&&tRate>0.05)||(cp.goal===‘maintain’&&Math.abs(tRate)<0.3);var drift=!onDir&&Math.abs(tRate)<0.8;if(!onDir){tCls=drift?‘h-trend drift’:‘h-trend off’;tTxt=drift?‘Drifting’:‘Off course’;}}
phRow=’<span class="h-badge '+cp.goal+'">’+esc(cp.name)+’</span><span class="'+tCls+'">’+tTxt+’</span>’;
}
q(‘heroRow’).innerHTML=phRow;
if(cp&&cp.targetWeight&&liveWI.length){
q(‘goalBarWrap’).style.display=‘block’;
var pCI=checkins.filter(function(c){return c.phaseId===cp.id&&c.avgWeight&&!c.isBulk;}).sort(function(a,b){return a.startDate.localeCompare(b.startDate);});
var sw2=pCI.length?pCI[0].avgWeight:(cp.startWeight||liveWI[liveWI.length-1].weight);
var cur=liveWI[0].weight,tot=Math.abs(cp.targetWeight-sw2),done2=Math.abs(cur-sw2);
var pct=tot>0?Math.min(100,Math.round(div(done2,tot)*100)):0;
q(‘goalBarLbl’).textContent=‘Target: ‘+fmtW(cp.targetWeight)+’ — ‘+pct+’% there’;q(‘goalBar’).style.width=pct+’%’;
q(‘heroStats’).style.display=‘flex’;
q(‘hsScore’).textContent=sCI.length&&sCI[0].score!=null?sCI[0].score:’—’;
var moved=Math.round((cur-sw2)*10)/10;q(‘hsChange’).textContent=(moved>0?’+’:’’)+fmtW(moved);
q(‘hsChange’).style.color=cp.goal===‘cut’?(moved<0?‘var(–ok)’:‘var(–bad)’):cp.goal===‘bulk’?(moved>0?‘var(–ok)’:‘var(–bad)’):‘var(–t1)’;
if(sCI.length>=2){var wkR=div(sCI[0].avgWeight-sCI[Math.min(2,sCI.length-1)].avgWeight,Math.min(2,sCI.length-1));var wLeft=wkR!==0?Math.ceil(div(cp.targetWeight-cur,wkR)):null;if(wLeft&&wLeft>0&&wLeft<200)q(‘hsProj’).textContent=fmtD(addDays(new Date(),wLeft*7));else q(‘hsProj’).textContent=’—’;}
else q(‘hsProj’).textContent=’—’;
}else{q(‘goalBarWrap’).style.display=‘none’;q(‘heroStats’).style.display=‘none’;}
var sub=cp?‘Phase: ‘+esc(cp.name)+(cp.goal?’ (’+cp.goal+’)’:’’):’’;var cpCalT=cp?getPhaseCalTarget(cp,todayStr()):null;if(cpCalT)sub+=’ · Target: ‘+cpCalT.toLocaleString()+’ cal/day’;
q(‘heroSub’).textContent=sub;
}
renderByMonth(‘dRecent’,liveWI.slice(0,30));
setDF(‘d’,q(‘dDate’).value||todayStr());setDF(‘l’,q(‘lDate’).value||todayStr());
}

/* ============================================================ REFRESH ALL */
function refreshAll(){
refreshDash();
renderIntel();
buildTrendRead();
buildMacroRead();
if(appState.route===‘progress’)renderAllCharts();
if(appState.route===‘measurements’)renderMeasurements();
var ws=dateStr(wkStart(new Date())),we=dateStr(wkEnd(new Date()));
var liveWI=weighIns.filter(function(w){return !w.isBulk;});
renderByMonth(‘lWeekList’,liveWI.filter(function(w){return w.date>=ws&&w.date<=we;}));
renderByMonth(‘lAllWI’,weighIns);
renderCIByMonth(‘lCIList’,checkins);
renderHistory();renderPhases();fillPhasePickers();renderCal();
}

/* ============================================================ TOAST */
function toast(txt,type,dur){
var bg={err:‘var(–bad)’,ok:‘var(–ok)’,info:‘var(–accent)’}[type]||‘var(–accent)’;
var el=document.createElement(‘div’);el.textContent=txt;
el.style.cssText=‘position:fixed;bottom:24px;left:50%;transform:translateX(-50%);background:’+bg+’;color:#fff;padding:12px 20px;border-radius:var(–r10);font-size:13px;font-weight:600;z-index:500;box-shadow:0 8px 24px rgba(0,0,0,.3);white-space:nowrap;max-width:90vw;text-align:center;pointer-events:none;’;
document.body.appendChild(el);
setTimeout(function(){el.style.transition=‘opacity .3s’;el.style.opacity=‘0’;setTimeout(function(){el.remove();},300);},dur||2200);
}

/* ============================================================ THEME PICKER TOGGLE */
function togThemePicker(){
var wrap=q(‘themePickerWrap’),chev=q(‘themeChev’);
if(!wrap)return;
var open=wrap.style.display!==‘none’;
wrap.style.display=open?‘none’:‘block’;
if(chev)chev.style.transform=open?‘rotate(-90deg)’:‘rotate(0deg)’;
}
function updateThemeLabel(){
var lbl=q(‘themeSubLbl’);if(!lbl)return;
var names={charcoal:‘Charcoal’,navy:‘Navy’,oled:‘OLED’,warm:‘Warm Dark’,‘light-gray’:‘Light Gray’,‘light-warm’:‘Warm Paper’,‘light-white’:‘True White’,‘light-sky’:‘Sky’};
lbl.textContent=’Active: ’+(names[appState.theme]||appState.theme);
}

/* ============================================================ PROGRESS / CHARTS */
var progRange = ‘phase’;

// Track per-chart, per-series visibility
var chartSeriesState = {
wt: { dots: true, roll: true, ci: true, target: true },
rate: { line: true, pace: true },
cal: { line: true }
};

function togChartSeries(chart, series, btn) {
chartSeriesState[chart] = chartSeriesState[chart] || {};
chartSeriesState[chart][series] = !chartSeriesState[chart][series];
btn.classList.toggle(‘on’, !!chartSeriesState[chart][series]);
if (chart === ‘wt’) renderWeightChart();
else if (chart === ‘rate’) renderRateChart();
else if (chart === ‘cal’) renderCalChart();
}

function hasDataForRange(r) {
var td = todayStr(), from = null, to = null;
if (r === ‘phase’) {
var cp = getChartPhase();
if (!cp) return false;
from = cp.startDate; to = cp.endDate || td;
} else if (r === ‘4w’) {
var d4 = new Date(); d4.setDate(d4.getDate() - 28); from = dateStr(d4);
} else if (r === ‘3m’) {
var d3 = new Date(); d3.setMonth(d3.getMonth() - 3); from = dateStr(d3);
} else { return true; }
return weighIns.some(function(w) {
return (!from || w.date >= from) && (!to || w.date <= to);
}) || checkins.some(function(c) {
return (!from || c.startDate >= from) && (!to || c.startDate <= to);
});
}

function setProgRange(r) {
progRange = r;
document.querySelectorAll(’.prog-preset’).forEach(function(b) {
b.classList.toggle(‘on’, b.dataset.pr === r);
});
// Update disabled state for all preset buttons based on data availability
document.querySelectorAll(’.prog-preset’).forEach(function(b) {
var pr = b.dataset.pr;
if (pr && pr !== r) {
b.disabled = !hasDataForRange(pr);
} else {
b.disabled = false;
}
});
renderAllCharts();
}

// Returns the phase to use for chart scoping:
// 1. Active phase (current date falls within it)
// 2. Most recently started phase if none active
function getChartPhase(){
var cp=getCurPhase();
if(cp)return cp;
// Fall back to most recently started phase
if(!phases.length)return null;
return phases.slice().sort(function(a,b){return b.startDate.localeCompare(a.startDate);})[0];
}

function getProgData() {
var td = todayStr(), from = null, to = null;
if (progRange === ‘phase’) {
var cp = getChartPhase();
if (cp) { from = cp.startDate; to = cp.endDate || td; }
} else if (progRange === ‘4w’) {
var d4 = new Date(); d4.setDate(d4.getDate() - 28); from = dateStr(d4);
} else if (progRange === ‘3m’) {
var d3 = new Date(); d3.setMonth(d3.getMonth() - 3); from = dateStr(d3);
}
var wi = weighIns.filter(function(w) {
if (from && w.date < from) return false;
if (to && w.date > to) return false;
return true;
}).slice().sort(function(a,b) { return a.date.localeCompare(b.date); });
var ci = checkins.filter(function(c) {
if (from && c.startDate < from) return false;
if (to && c.startDate > to) return false;
return true;
}).slice().sort(function(a,b) { return a.startDate.localeCompare(b.startDate); });
return { wi: wi, ci: ci };
}

// Rolling average helper
function rollingAvg(arr, window) {
return arr.map(function(_, i) {
var start = Math.max(0, i - window + 1);
var slice = arr.slice(start, i + 1);
return slice.reduce(function(a,b){ return a+b; }, 0) / slice.length;
});
}

// SVG builder helpers
function svgEl(tag, attrs) {
var el = document.createElementNS(‘http://www.w3.org/2000/svg’, tag);
Object.keys(attrs).forEach(function(k) { el.setAttribute(k, attrs[k]); });
return el;
}

function showTooltip(tooltipEl, wrapEl, x, y, html) {
tooltipEl.innerHTML = html;
tooltipEl.classList.add(‘show’);
var tw = tooltipEl.offsetWidth || 120;
var ww = wrapEl.offsetWidth || 300;
var left = Math.min(x + 12, ww - tw - 8);
tooltipEl.style.left = Math.max(4, left) + ‘px’;
tooltipEl.style.top = (y - 40) + ‘px’;
}
function hideTooltip(tooltipEl) { tooltipEl.classList.remove(‘show’); }

// ── CHART 1: Weight Trend ──────────────────────────────────────
function renderWeightChart() {
var wrap = document.getElementById(‘weightChartWrap’);
var empty = document.getElementById(‘weightChartEmpty’);
var tooltip = document.getElementById(‘weightTooltip’);
if (!wrap) return;
// Clear previous SVG before any early return
var prev = wrap.querySelector(‘svg’); if (prev) prev.remove();
var data = getProgData();
var wi = data.wi;
var ciData = data.ci.filter(function(c) { return c.avgWeight; });
// Need at least 2 daily weigh-ins OR 2 check-ins to render
if (wi.length < 2 && ciData.length < 2) { if(empty) empty.style.display=‘block’; return; }
if (empty) empty.style.display = ‘none’;

var showDots   = chartSeriesState.wt.dots   !== false;
var showRoll   = chartSeriesState.wt.roll   !== false;
var showCI     = chartSeriesState.wt.ci     !== false;
var showTarget = chartSeriesState.wt.target !== false;

var cp = getCurPhase();
var H = 220, PAD = { top: 16, right: 24, bottom: 36, left: 52 };
var W = wrap.offsetWidth || 320;
if (W < 50) W = 320;
var IW = W - PAD.left - PAD.right;
var IH = H - PAD.top - PAD.bottom;

var vals   = wi.map(function(w) { return toDisp(w.weight); });
var rolling = wi.length >= 2 ? rollingAvg(vals, 7) : [];
var targetW = cp && cp.targetWeight ? toDisp(cp.targetWeight) : null;

// Build unified date domain across both daily and check-in series
var allDates = wi.map(function(w) { return w.date; });
ciData.forEach(function(c) { if (allDates.indexOf(c.startDate) < 0) allDates.push(c.startDate); });
allDates.sort();
var domainMin = allDates[0], domainMax = allDates[allDates.length-1];
function dateToX(ds) {
var total = toDate(domainMax) - toDate(domainMin);
if (!total) return PAD.left + IW / 2;
return PAD.left + ((toDate(ds) - toDate(domainMin)) / total) * IW;
}

// Value range — include all active series
var allVals = [];
if (showDots || showRoll) allVals = allVals.concat(vals);
if (showRoll && rolling.length) allVals = allVals.concat(rolling);
if (showCI) ciData.forEach(function(c) { allVals.push(toDisp(c.avgWeight)); });
if (targetW) allVals.push(targetW);
if (!allVals.length) { if(empty) empty.style.display=‘block’; return; }
var minV = Math.min.apply(null, allVals), maxV = Math.max.apply(null, allVals);
var pad = Math.max((maxV - minV) * 0.12, 0.5);
minV -= pad; maxV += pad;
var range = maxV - minV || 1;

function yp(v) { return PAD.top + (1 - (v - minV) / range) * IH; }

var svg = svgEl(‘svg’, { viewBox: ’0 0 ’ + W + ’ ’ + H, xmlns: ‘http://www.w3.org/2000/svg’ });

// Grid lines + Y labels
var ticks = 5;
for (var t = 0; t <= ticks; t++) {
var v = minV + (range / ticks) * t;
var y = yp(v);
svg.appendChild(svgEl(‘line’, { x1: PAD.left, y1: y, x2: W - PAD.right, y2: y, stroke: ‘rgba(128,128,128,0.12)’, ‘stroke-width’: ‘1’ }));
var lbl = svgEl(‘text’, { x: PAD.left - 6, y: y + 4, ‘text-anchor’: ‘end’, ‘font-size’: ‘10’, fill: ‘var(–t3)’, ‘font-family’: ‘var(–font)’ });
lbl.textContent = v.toFixed(1);
svg.appendChild(lbl);
}

// Target weight dashed line
var goalLineLegBtn = document.getElementById(‘goalLineLegendBtn’);
if (targetW) {
if (goalLineLegBtn) goalLineLegBtn.style.display = ‘flex’;
if (showTarget && targetW >= minV && targetW <= maxV) {
svg.appendChild(svgEl(‘line’, { x1: PAD.left, y1: yp(targetW), x2: W - PAD.right, y2: yp(targetW), stroke: ‘var(–warn)’, ‘stroke-width’: ‘1.5’, ‘stroke-dasharray’: ‘6,4’, opacity: ‘0.8’ }));
}
} else { if (goalLineLegBtn) goalLineLegBtn.style.display = ‘none’; }

// X axis date labels (~5 evenly spaced from domain)
var labelEvery = Math.max(1, Math.floor(allDates.length / 5));
allDates.forEach(function(ds, i) {
if (i % labelEvery !== 0 && i !== allDates.length - 1) return;
var lbl = svgEl(‘text’, { x: dateToX(ds), y: H - 6, ‘text-anchor’: ‘middle’, ‘font-size’: ‘10’, fill: ‘var(–t3)’, ‘font-family’: ‘var(–font)’ });
lbl.textContent = fmtD(ds);
svg.appendChild(lbl);
});

// Raw daily dots (faint)
if (showDots && wi.length) {
wi.forEach(function(w) {
svg.appendChild(svgEl(‘circle’, { cx: dateToX(w.date), cy: yp(toDisp(w.weight)), r: ‘3’, fill: ‘var(–accent)’, opacity: ‘0.35’ }));
});
}

// 7-day rolling average line (accent)
if (showRoll && rolling.length >= 2) {
var pts = wi.map(function(w, i) { return dateToX(w.date) + ‘,’ + yp(rolling[i]); }).join(’ ’);
svg.appendChild(svgEl(‘polyline’, { points: pts, fill: ‘none’, stroke: ‘var(–accent)’, ‘stroke-width’: ‘2.5’, ‘stroke-linejoin’: ‘round’, ‘stroke-linecap’: ‘round’ }));
}

// Weekly check-in average line (green)
if (showCI && ciData.length >= 2) {
var ciPts = ciData.map(function(c) { return dateToX(c.startDate) + ‘,’ + yp(toDisp(c.avgWeight)); }).join(’ ’);
svg.appendChild(svgEl(‘polyline’, { points: ciPts, fill: ‘none’, stroke: ‘var(–ok)’, ‘stroke-width’: ‘2’, ‘stroke-linejoin’: ‘round’, ‘stroke-linecap’: ‘round’, ‘stroke-dasharray’: ‘4,2’ }));
// CI dots
ciData.forEach(function(c) {
svg.appendChild(svgEl(‘circle’, { cx: dateToX(c.startDate), cy: yp(toDisp(c.avgWeight)), r: ‘4’, fill: ‘var(–ok)’, opacity: ‘0.9’ }));
});
}

// Invisible hit targets for daily tooltip (placed last so on top)
if (wi.length) {
wi.forEach(function(w) {
var hitbox = svgEl(‘circle’, { cx: dateToX(w.date), cy: yp(toDisp(w.weight)), r: ‘14’, fill: ‘transparent’, style: ‘cursor:pointer;’ });
hitbox.addEventListener(‘mouseenter’, function() {
showTooltip(tooltip, wrap, dateToX(w.date), yp(toDisp(w.weight)),
‘<strong>’ + fmtD(w.date) + ‘</strong>’ + fmtW(w.weight) + (w.isBulk ? ’ <span style="color:var(--warn);font-size:10px;">BULK</span>’ : ‘’));
});
hitbox.addEventListener(‘mouseleave’, function() { hideTooltip(tooltip); });
svg.appendChild(hitbox);
});
}

// CI hit targets
if (showCI) {
ciData.forEach(function(c) {
var hitbox = svgEl(‘circle’, { cx: dateToX(c.startDate), cy: yp(toDisp(c.avgWeight)), r: ‘10’, fill: ‘transparent’, style: ‘cursor:pointer;’ });
hitbox.addEventListener(‘mouseenter’, function() {
showTooltip(tooltip, wrap, dateToX(c.startDate), yp(toDisp(c.avgWeight)),
’<strong>Wk avg ’ + fmtD(c.startDate) + ‘</strong>’ + fmtW(c.avgWeight));
});
hitbox.addEventListener(‘mouseleave’, function() { hideTooltip(tooltip); });
svg.appendChild(hitbox);
});
}

wrap.appendChild(svg);
}

// ── CHART 2: Cumulative Progress ───────────────────────────────
function renderRateChart() {
var wrap = document.getElementById(‘rateChartWrap’);
var empty = document.getElementById(‘rateChartEmpty’);
var tooltip = document.getElementById(‘rateTooltip’);
if (!wrap) return;
// Always clear previous SVG first
var prev = wrap.querySelector(‘svg’); if (prev) prev.remove();
var data = getProgData();
var ci = data.ci.filter(function(c) { return c.avgWeight; });
if (ci.length < 2) { if(empty) empty.style.display=‘block’; return; }
if (empty) empty.style.display = ‘none’;

var showLine = chartSeriesState.rate.line !== false;
var showPace = chartSeriesState.rate.pace !== false;
var cp = getCurPhase();

// Build cumulative change from the first check-in in range
var baseline = toDisp(ci[0].avgWeight);
var points = ci.map(function(c, i) {
return { date: c.startDate, cumulative: toDisp(c.avgWeight) - baseline, ci: c, i: i };
});

// Goal pace line
var goalRate = null;
var rateLegBtn = document.getElementById(‘rateLineLegendBtn’);
if (cp && cp.weeklyRate) {
goalRate = cp.goal === ‘cut’ ? -toDisp(cp.weeklyRate) : toDisp(cp.weeklyRate);
if (rateLegBtn) rateLegBtn.style.display = ‘flex’;
} else {
if (rateLegBtn) rateLegBtn.style.display = ‘none’;
}

// Value range
var cumVals = points.map(function(p) { return p.cumulative; });
var goalVals = [];
if (goalRate) {
for (var gi = 0; gi < points.length; gi++) goalVals.push(goalRate * gi);
}
var allVals = cumVals.concat(goalVals).concat([0]);
var minV = Math.min.apply(null, allVals);
var maxV = Math.max.apply(null, allVals);
var pad = Math.max((maxV - minV) * 0.15, 0.3);
minV -= pad; maxV += pad;
var range = maxV - minV || 1;

var H = 200, PAD = { top: 16, right: 24, bottom: 36, left: 52 };
var W = wrap.offsetWidth || 320;
if (W < 50) W = 320;
var IW = W - PAD.left - PAD.right;
var IH = H - PAD.top - PAD.bottom;
var n = points.length;

function xp(i) { return PAD.left + (i / (n - 1)) * IW; }
function yp(v) { return PAD.top + (1 - (v - minV) / range) * IH; }

var svg = svgEl(‘svg’, { viewBox: ’0 0 ’ + W + ’ ’ + H, xmlns: ‘http://www.w3.org/2000/svg’ });

// Zero line (baseline reference)
var zeroY = yp(0);
svg.appendChild(svgEl(‘line’, { x1: PAD.left, y1: zeroY, x2: W - PAD.right, y2: zeroY, stroke: ‘rgba(128,128,128,0.2)’, ‘stroke-width’: ‘1.5’ }));

// Grid lines — a few above and below zero
var gridStep = Math.max(0.5, Math.round((maxV - minV) / 5 * 10) / 10);
var gridStart = Math.ceil(minV / gridStep) * gridStep;
for (var gv = gridStart; gv <= maxV; gv = Math.round((gv + gridStep) * 100) / 100) {
if (Math.abs(gv) < 0.05) continue; // skip zero — already drawn
var gy2 = yp(gv);
if (gy2 < PAD.top || gy2 > H - PAD.bottom) continue;
svg.appendChild(svgEl(‘line’, { x1: PAD.left, y1: gy2, x2: W - PAD.right, y2: gy2, stroke: ‘rgba(128,128,128,0.07)’, ‘stroke-width’: ‘1’ }));
var gl = svgEl(‘text’, { x: PAD.left - 6, y: gy2 + 4, ‘text-anchor’: ‘end’, ‘font-size’: ‘10’, fill: ‘var(–t3)’, ‘font-family’: ‘var(–font)’ });
gl.textContent = (gv > 0 ? ‘+’ : ‘’) + gv.toFixed(1);
svg.appendChild(gl);
}

// Y label at zero
var zl = svgEl(‘text’, { x: PAD.left - 6, y: zeroY + 4, ‘text-anchor’: ‘end’, ‘font-size’: ‘10’, fill: ‘var(–t3)’, ‘font-family’: ‘var(–font)’ });
zl.textContent = ‘0’;
svg.appendChild(zl);

// Goal pace dashed line
if (goalRate && showPace && n >= 2) {
var gpPts = points.map(function(p, i) { return xp(i) + ‘,’ + yp(goalRate * i); }).join(’ ’);
svg.appendChild(svgEl(‘polyline’, { points: gpPts, fill: ‘none’, stroke: ‘var(–warn)’, ‘stroke-width’: ‘1.5’, ‘stroke-dasharray’: ‘5,4’, opacity: ‘0.85’ }));
}

if (showLine && n >= 2) {
// Filled area between line and zero
var fillPts = xp(0) + ‘,’ + zeroY;
points.forEach(function(p, i) { fillPts += ’ ’ + xp(i) + ‘,’ + yp(p.cumulative); });
fillPts += ’ ’ + xp(n - 1) + ‘,’ + zeroY;
// Color the fill based on phase goal direction
var fillColor = ‘var(–accent)’;
if (cp && cp.goal === ‘cut’) fillColor = points[n-1].cumulative < 0 ? ‘var(–ok)’ : ‘var(–bad)’;
if (cp && cp.goal === ‘bulk’) fillColor = points[n-1].cumulative > 0 ? ‘var(–ok)’ : ‘var(–bad)’;
svg.appendChild(svgEl(‘polygon’, { points: fillPts, fill: fillColor, opacity: ‘0.07’ }));

```
// Progress line
var linePts = points.map(function(p, i) { return xp(i) + ',' + yp(p.cumulative); }).join(' ');
svg.appendChild(svgEl('polyline', { points: linePts, fill: 'none', stroke: 'var(--accent)', 'stroke-width': '2.5', 'stroke-linejoin': 'round', 'stroke-linecap': 'round' }));

// Dots + tooltips
points.forEach(function(p, i) {
  var dot = svgEl('circle', { cx: xp(i), cy: yp(p.cumulative), r: '4', fill: 'var(--accent)', style: 'cursor:pointer;' });
  var cumDisp = (p.cumulative >= 0 ? '+' : '') + p.cumulative.toFixed(1) + ' ' + appState.unit;
  dot.addEventListener('mouseenter', function() {
    showTooltip(tooltip, wrap, xp(i), yp(p.cumulative),
      '<strong>' + fmtD(p.date) + '</strong>' + cumDisp + '<br><span style="color:var(--t3);font-size:11px;">' + fmtW(p.ci.avgWeight) + ' avg</span>');
  });
  dot.addEventListener('mouseleave', function() { hideTooltip(tooltip); });
  svg.appendChild(dot);
});
```

}

// X labels
var every = Math.max(1, Math.floor(n / 5));
points.forEach(function(p, i) {
if (i % every !== 0 && i !== n - 1) return;
var lbl = svgEl(‘text’, { x: xp(i), y: H - 6, ‘text-anchor’: ‘middle’, ‘font-size’: ‘10’, fill: ‘var(–t3)’, ‘font-family’: ‘var(–font)’ });
lbl.textContent = fmtD(p.date);
svg.appendChild(lbl);
});

wrap.appendChild(svg);
}

// ── CHART 4: Calorie Intake (line) ─────────────────────────────
function renderCalChart() {
var wrap = document.getElementById(‘calChartWrap’);
var empty = document.getElementById(‘calChartEmpty’);
var tooltip = document.getElementById(‘calTooltip’);
if (!wrap) return;
// Always clear previous SVG first
var prev = wrap.querySelector(‘svg’); if (prev) prev.remove();
var data = getProgData();
var ci = data.ci.filter(function(c) { return c.calories; });
if (ci.length < 2) { if(empty) empty.style.display=‘block’; return; }
if (empty) empty.style.display = ‘none’;

var showLine = chartSeriesState.cal.line !== false;

var cp = getCurPhase()||getChartPhase();
// Build per-CI target array using adaptive stage lookup
var ciTargets = ci.map(function(c) {
return c.targetCal || getPhaseCalTarget(cp, c.startDate) || null;
});

var H = 200, PAD = { top: 16, right: 24, bottom: 36, left: 56 };
var W = wrap.offsetWidth || 320;
if (W < 50) W = 320;
var IW = W - PAD.left - PAD.right;
var IH = H - PAD.top - PAD.bottom;

var calVals = ci.map(function(c) { return c.calories; });
var minV = Math.min.apply(null, calVals);
var maxV = Math.max.apply(null, calVals);
// Include all per-CI targets in the value range so reference lines are always visible
ciTargets.forEach(function(t) { if(t){minV=Math.min(minV,t);maxV=Math.max(maxV,t);} });
var pad2 = (maxV - minV) * 0.12 || 100;
minV -= pad2; maxV += pad2;
var range = maxV - minV || 1;

function xp(i) { return PAD.left + (i / (ci.length - 1)) * IW; }
function yp(v) { return PAD.top + (1 - (v - minV) / range) * IH; }

var svg = svgEl(‘svg’, { viewBox: ’0 0 ’ + W + ’ ’ + H, xmlns: ‘http://www.w3.org/2000/svg’ });

// Grid lines
var ticks = 4;
for (var t = 0; t <= ticks; t++) {
var v = minV + (range / ticks) * t;
var y = yp(v);
svg.appendChild(svgEl(‘line’, { x1: PAD.left, y1: y, x2: W - PAD.right, y2: y, stroke: ‘rgba(128,128,128,0.1)’, ‘stroke-width’: ‘1’ }));
var lbl = svgEl(‘text’, { x: PAD.left - 6, y: y + 4, ‘text-anchor’: ‘end’, ‘font-size’: ‘10’, fill: ‘var(–t3)’, ‘font-family’: ‘var(–font)’ });
lbl.textContent = Math.round(v).toLocaleString();
svg.appendChild(lbl);
}

// Per-CI adaptive target reference lines — draw as step segments between check-in points
// Group consecutive CIs that share the same target and draw one line segment per group
var calLeg = document.getElementById(‘calTargetLegend’);
var hasAnyTarget = ciTargets.some(function(t){return t!=null;});
if (hasAnyTarget) {
if (calLeg) calLeg.style.display = ‘flex’;
// Build step-function polyline for the adaptive target
var targetPts = ‘’;
var lastTarget = null;
ci.forEach(function(c, i) {
var tgt = ciTargets[i];
if (tgt == null) return;
if (targetPts === ‘’) {
// Start from left edge at this target level if it’s the first
targetPts = (i === 0 ? PAD.left : xp(i)) + ‘,’ + yp(tgt);
} else if (tgt !== lastTarget) {
// Step: vertical then horizontal
targetPts += ’ ’ + xp(i) + ‘,’ + yp(lastTarget);
targetPts += ’ ’ + xp(i) + ‘,’ + yp(tgt);
}
lastTarget = tgt;
});
// Extend to right edge at last known target
if (lastTarget !== null) {
targetPts += ’ ’ + (PAD.left + IW) + ‘,’ + yp(lastTarget);
}
if (targetPts) {
svg.appendChild(svgEl(‘polyline’, { points: targetPts, fill: ‘none’, stroke: ‘var(–warn)’, ‘stroke-width’: ‘1.5’, ‘stroke-dasharray’: ‘6,4’, opacity: ‘0.85’ }));
}
} else {
if (calLeg) calLeg.style.display = ‘none’;
}

if (showLine) {
// Filled area under line
var ptsFill = PAD.left + ‘,’ + (PAD.top + IH);
ci.forEach(function(c, i) { ptsFill += ’ ’ + xp(i) + ‘,’ + yp(c.calories); });
ptsFill += ’ ’ + (PAD.left + IW) + ‘,’ + (PAD.top + IH);
svg.appendChild(svgEl(‘polygon’, { points: ptsFill, fill: ‘var(–ok)’, opacity: ‘0.08’ }));

```
// Line
var pts = ci.map(function(c, i) { return xp(i) + ',' + yp(c.calories); }).join(' ');
svg.appendChild(svgEl('polyline', { points: pts, fill: 'none', stroke: 'var(--ok)', 'stroke-width': '2', 'stroke-linejoin': 'round', 'stroke-linecap': 'round' }));

// Dots + tooltips — show per-CI adaptive target in tooltip
ci.forEach(function(c, i) {
  var tgt = ciTargets[i];
  var dot = svgEl('circle', { cx: xp(i), cy: yp(c.calories), r: '4', fill: 'var(--ok)', style: 'cursor:pointer;' });
  dot.addEventListener('mouseenter', function() {
    showTooltip(tooltip, wrap, xp(i), yp(c.calories),
      '<strong>' + fmtD(c.startDate) + '</strong>' + c.calories.toLocaleString() + ' cal'
      + (tgt ? '<br><span style="color:var(--t3);">Target: ' + tgt.toLocaleString() + '</span>' : ''));
  });
  dot.addEventListener('mouseleave', function() { hideTooltip(tooltip); });
  svg.appendChild(dot);
});
```

}

// X labels
var every = Math.max(1, Math.floor(ci.length / 5));
ci.forEach(function(c, i) {
if (i % every !== 0 && i !== ci.length - 1) return;
var lbl = svgEl(‘text’, { x: xp(i), y: H - 6, ‘text-anchor’: ‘middle’, ‘font-size’: ‘10’, fill: ‘var(–t3)’, ‘font-family’: ‘var(–font)’ });
lbl.textContent = fmtD(c.startDate);
svg.appendChild(lbl);
});

wrap.appendChild(svg);
}

function renderAllCharts() {
renderWeightChart();
renderRateChart();
renderCalChart();
}

/* ============================================================ INTELLIGENCE ENGINE */
function mifflinTDEE(weightKg,heightCm,age,sex,activity){
var bmr=sex===‘male’?(10*weightKg+6.25*heightCm-5*age+5):(10*weightKg+6.25*heightCm-5*age-161);
return Math.round(bmr*activity);
}
function getRollingData(weeks){
return checkins.filter(function(c){return !c.isBulk&&c.avgWeight&&c.calories;})
.sort(function(a,b){return a.startDate.localeCompare(b.startDate);}).slice(-weeks);
}
function adaptiveTDEE(pts){
if(pts.length<2)return null;
var ests=[];
for(var i=1;i<pts.length;i++){
var wtDiff=pts[i].avgWeight-pts[i-1].avgWeight;
var impliedMaint=pts[i].calories-(wtDiff*3500/7);
ests.push({val:impliedMaint,idx:i});
}
var tw=0,ws=0;
ests.forEach(function(e){tw+=e.idx;ws+=e.val*e.idx;});
return tw>0?Math.round(ws/tw):null;
}
function tdeeConf(pts){return pts.length>=4?‘high’:pts.length>=2?‘med’:‘low’;}
function thisWeekBal(tdee){
if(!tdee)return null;
var r=checkins.filter(function(c){return !c.isBulk&&c.calories;}).sort(function(a,b){return b.startDate.localeCompare(a.startDate);});
return r.length?r[0].calories-tdee:null;
}
function realisticChk(tdee){
if(!tdee)return null;
var r=checkins.filter(function(c){return !c.isBulk&&c.avgWeight&&c.calories;}).sort(function(a,b){return b.startDate.localeCompare(a.startDate);});
if(r.length<2)return null;
var loggedDef=tdee-r[0].calories;
var actualChg=r[0].avgWeight-r[1].avgWeight;
var impliedFromWt=-actualChg*500;
if(Math.abs(loggedDef-impliedFromWt)>400){
if(loggedDef>0&&actualChg>0.2)return’A deficit of ~‘+Math.round(loggedDef)+’ cal/day was logged, but weight increased ‘+fmtW(actualChg)+’. This may indicate water retention or a logging gap — the trend may clarify over subsequent weeks.’;
if(loggedDef<-200&&actualChg<-0.2)return’Weight decreased ‘+fmtW(Math.abs(actualChg))+’ despite a logged surplus. This may reflect water loss rather than tissue change — monitoring over the next few weeks may clarify.’;
}
return null;
}
function projFromRate(cp){
if(!cp||!cp.targetWeight)return null;
var liveWI=weighIns.filter(function(w){return !w.isBulk;});
if(!liveWI.length)return null;
var curW=liveWI[0].weight;
var sCI=checkins.filter(function(c){return c.avgWeight&&!c.isBulk;}).sort(function(a,b){return b.startDate.localeCompare(a.startDate);});
if(sCI.length<2)return null;
var n=Math.min(4,sCI.length);
var wkRate=div(sCI[0].avgWeight-sCI[n-1].avgWeight,n-1);
if(Math.abs(wkRate)<0.01)return null;
var wksLeft=Math.ceil(div(cp.targetWeight-curW,wkRate));
if(wksLeft<=0||wksLeft>260)return null;
return addDays(new Date(),wksLeft*7);
}
function openIntelModal(){
var p=Local.get(‘intelProfile’,{});
if(p.age)q(‘ipAge’).value=p.age;
if(p.sex)q(‘ipSex’).value=p.sex;
if(p.heightFt)q(‘ipHeightFt’).value=p.heightFt;
if(p.heightIn!==undefined)q(‘ipHeightIn’).value=p.heightIn;
if(p.activity)q(‘ipActivity’).value=p.activity;
updIPPreview();openM(‘mIntel’);
}
function updIPPreview(){
var age=parseInt(q(‘ipAge’).value),sex=q(‘ipSex’).value;
var ft=parseInt(q(‘ipHeightFt’).value)||0,inch=parseInt(q(‘ipHeightIn’).value)||0;
var act=parseFloat(q(‘ipActivity’).value);
var prev=q(‘ipPreview’);if(!age||!sex||!ft||!act){prev.style.display=‘none’;return;}
var heightCm=(ft*12+inch)*2.54;
var liveWI=weighIns.filter(function(w){return !w.isBulk;});
var wtKg=liveWI.length?liveWI[0].weight*0.453592:70;
var tdee=mifflinTDEE(wtKg,heightCm,age,sex,act);
prev.style.display=‘block’;
prev.innerHTML=‘Estimated maintenance: <strong>’+tdee.toLocaleString()+’ cal/day</strong>’;
}
[‘ipAge’,‘ipSex’,‘ipHeightFt’,‘ipHeightIn’,‘ipActivity’].forEach(function(id){
var el=document.getElementById(id);
if(el){el.addEventListener(‘input’,updIPPreview);el.addEventListener(‘change’,updIPPreview);}
});
function saveIntelProfile(){
var p={age:parseInt(q(‘ipAge’).value)||null,sex:q(‘ipSex’).value||null,heightFt:parseInt(q(‘ipHeightFt’).value)||null,heightIn:parseInt(q(‘ipHeightIn’).value)||0,activity:parseFloat(q(‘ipActivity’).value)||null};
Local.set(‘intelProfile’,p);closeM(‘mIntel’);
var sub=q(‘intelProfileSub’);
if(sub&&p.age&&p.sex)sub.textContent=‘Profile set \u2014 ‘+(p.sex===‘male’?‘Male’:‘Female’)+’, age ‘+p.age;
renderIntel();toast(‘Profile saved’);
}
function togIntelExp(){
var panel=q(‘intelExpPanel’),btn=q(‘intelExpBtn’);
if(!panel)return;
var open=panel.style.display!==‘none’;
panel.style.display=open?‘none’:‘block’;
if(btn)btn.textContent=open?‘How this is calculated’:‘Hide explanation’;
if(!open)buildIntelExp(panel);
}
function buildIntelExp(el){
var rolling=getRollingData(4);
var conf=tdeeConf(rolling);
var adaptTDEE=adaptiveTDEE(rolling);
var profile=Local.get(‘intelProfile’,{});
var hasProfile=profile.age&&profile.sex&&profile.heightFt&&profile.activity;
var lines=[];
if(adaptTDEE&&rolling.length>=2){
lines.push(’<strong>Maintenance estimate source:</strong> Adaptive — derived from your actual weight changes and logged calories across ‘+rolling.length+’ check-in’+(rolling.length!==1?‘s’:’’)+’.’);
lines.push(’<strong>Method:</strong> For each consecutive check-in pair, STRATUM calculates the implied maintenance as: calories logged minus the calorie equivalent of weight change (3,500 cal/lb). These estimates are then averaged, weighted toward more recent weeks.’);
lines.push(’<strong>Confidence:</strong> ‘+(conf===‘high’?‘High — 4+ weeks of check-in data with calories logged.’:conf===‘med’?‘Moderate — ‘+rolling.length+’ weeks of data. More check-ins will improve accuracy.’:‘Low — fewer than 2 usable check-ins.’));
lines.push(’<strong>Limitation:</strong> Estimate accuracy depends on consistent calorie logging. Gaps or inaccurate logging reduce reliability. Short-term weight changes may include water retention which is not metabolically meaningful.’);
}else if(hasProfile){
lines.push(’<strong>Maintenance estimate source:</strong> Formula (Mifflin-St Jeor) — based on your profile data, not your actual logged results.’);
lines.push(’<strong>Inputs used:</strong> Current weight, height (’+profile.heightFt+‘ft ‘+(profile.heightIn||0)+‘in), age (’+profile.age+’), biological sex (’+profile.sex+’), activity multiplier (’+profile.activity+’).’);
lines.push(’<strong>Limitation:</strong> Formula estimates can differ from real-world maintenance by 10–20%. Log calories on 2+ weekly check-ins to unlock the adaptive estimate, which uses your actual data.’);
}else{
lines.push(‘No profile or check-in data available yet. Set up your profile in Settings or log 2+ check-ins with calories to generate an estimate.’);
}
lines.push(’<strong>This week balance:</strong> Calculated as your most recent check-in calories minus the maintenance estimate. Positive = surplus, negative = deficit.’);
lines.push(’<strong>Projected finish:</strong> Extrapolated from your rolling rate of change across the last 1–4 check-ins relative to your phase target weight. Not a guarantee — based on sustained current trend.’);
el.innerHTML=lines.map(function(l){return’<div style="margin-bottom:8px;">’+l+’</div>’;}).join(’’);
}
function renderIntel(){
var el=q(‘intelBody’);if(!el)return;
var cp=getCurPhase();
var rolling=getRollingData(4);
var conf=tdeeConf(rolling);
var adaptTDEE=adaptiveTDEE(rolling);
var profile=Local.get(‘intelProfile’,{});
var hasProfile=profile.age&&profile.sex&&profile.heightFt&&profile.activity;
var sub=q(‘intelProfileSub’);
if(sub&&hasProfile)sub.textContent=‘Profile set \u2014 ‘+(profile.sex===‘male’?‘Male’:‘Female’)+’, age ‘+profile.age;
var tdee=null,source=’’,confClass=’’;
if(adaptTDEE&&rolling.length>=2){
tdee=adaptTDEE;source=‘adaptive’;
confClass=conf===‘high’?‘conf-high’:‘conf-med’;
}else if(hasProfile){
var liveWI=weighIns.filter(function(w){return !w.isBulk;});
var wtLbs=liveWI.length?liveWI[0].weight:null;
if(wtLbs){
var wtKg=wtLbs*0.453592;
var heightCm=(profile.heightFt*12+(profile.heightIn||0))*2.54;
tdee=mifflinTDEE(wtKg,heightCm,profile.age,profile.sex,profile.activity);
source=‘formula’;confClass=‘conf-low’;
}
}
// Refresh explanation panel if currently open
var expPanel=q(‘intelExpPanel’);
if(expPanel&&expPanel.style.display!==‘none’)buildIntelExp(expPanel);
if(!tdee){
el.innerHTML=’<div class="intel-setup"><p>Set up your profile to get a maintenance calorie estimate. Once you have 2+ check-ins with calories logged, the estimate will be based on your actual data instead.</p><button class="btn btn-p btn-sm" onclick="openIntelModal()">Set up profile</button></div>’;
return;
}
var balance=thisWeekBal(tdee);
var warning=realisticChk(tdee);
var proj=projFromRate(cp);
var html=’’;
html+=’<div class="intel-row"><span class="intel-row-lbl">Est. maintenance</span><span class="intel-row-val '+confClass+'">’+tdee.toLocaleString()+’ cal/day</span></div>’;
if(balance!==null){
var bSign=balance>=0?’+’:’’;
var bColor=balance<-50?‘var(–ok)’:balance>50?‘var(–bad)’:‘var(–t2)’;
var bLabel=balance<-50?‘deficit’:balance>50?‘surplus’:‘at maintenance’;
html+=’<div class="intel-row"><span class="intel-row-lbl">This week</span><span class="intel-row-val" style="color:'+bColor+';">’+bSign+Math.round(balance)+’ cal/day <span style="font-size:11px;font-weight:500;color:var(--t3);">(’+bLabel+’)</span></span></div>’;
}
if(proj&&cp&&cp.targetDate){
var projStr=fmtD(proj);
var diff=Math.round((toDate(dateStr(proj)).getTime()-toDate(cp.targetDate).getTime())/(7*24*3600*1000));
var diffStr=diff===0?‘on target’:diff>0?diff+’ wks late’:Math.abs(diff)+’ wks early’;
var diffColor=diff<=0?‘var(–ok)’:diff<=2?‘var(–warn)’:‘var(–bad)’;
html+=’<div class="intel-row"><span class="intel-row-lbl">Projected finish</span><span class="intel-row-val">’+projStr+’ <span style="font-size:11px;font-weight:600;color:'+diffColor+';">(’+diffStr+’)</span></span></div>’;
}else if(proj){
html+=’<div class="intel-row"><span class="intel-row-lbl">Projected finish</span><span class="intel-row-val">’+fmtD(proj)+’</span></div>’;
}
var editBtn=’<button onclick="openIntelModal()" style="background:none;border:none;color:var(--accent-b);font-size:11px;cursor:pointer;padding:0;text-decoration:underline;">Edit profile</button>’;
if(source===‘adaptive’){
var cLbls={high:‘High confidence \u2014 4 weeks of data’,med:‘Moderate confidence \u2014 ‘+rolling.length+’ weeks of data’};
html+=’<div class="intel-note">Adaptive estimate — derived from your actual results. ‘+(cLbls[conf]||rolling.length+’ weeks of data’)+’. Updates with each check-in. ‘+editBtn+’</div>’;
}else{
var wksNeeded=Math.max(0,2-rolling.length);
html+=’<div class="intel-note" style="color:var(--warn);">Formula estimate — based on your profile, not your actual data. Log calories on ‘+wksNeeded+’ more check-in’+(wksNeeded!==1?‘s’:’’)+’ to unlock the adaptive estimate. ‘+editBtn+’</div>’;
}
if(warning)html+=’<div class="intel-warn">’+warning+’</div>’;
el.innerHTML=html;
}

/* ============================================================ TREND INTERPRETATION ENGINE */
function buildTrendRead(){
var el=q(‘trendRead’);if(!el)return;

// Gather data sources
var liveCI=checkins.filter(function(c){return !c.isBulk&&c.avgWeight;})
.sort(function(a,b){return b.startDate.localeCompare(a.startDate);});
var cp=getCurPhase();

// Not enough data
if(liveCI.length<2){
el.innerHTML=’<span style="color:var(--t4);font-size:13px;">Log 2+ weekly check-ins to generate a trend read.</span>’;
return;
}

// Core calculations
var n=Math.min(4,liveCI.length);
var recent=liveCI.slice(0,n);

// Rate of change: avg weekly delta across last n check-ins
var totalDelta=recent[0].avgWeight-recent[n-1].avgWeight;
var weekSpan=n-1;
var weeklyRate=weekSpan>0?totalDelta/weekSpan:0; // lbs/week
var absRate=Math.abs(weeklyRate);

// Direction consistency: how many of the last deltas agree on direction
var deltas=[];
for(var i=0;i<recent.length-1;i++)deltas.push(recent[i].avgWeight-recent[i+1].avgWeight);
var posCount=deltas.filter(function(d){return d>0;}).length;
var negCount=deltas.filter(function(d){return d<0;}).length;
var consistent=posCount===deltas.length||negCount===deltas.length;
var mixed=!consistent;

// Calorie signal from most recent check-in
var calCI=liveCI.filter(function(c){return c.calories;});
var hasCal=calCI.length>0;
var lastCal=hasCal?calCI[0].calories:null;

// Confidence level: based on data quantity and consistency
var conf=liveCI.length>=4&&consistent?‘high’:liveCI.length>=3?‘med’:liveCI.length>=2?‘low’:‘none’;
var confLabels={high:‘High confidence’,med:‘Moderate confidence’,low:‘Low confidence’,none:‘Insufficient data’};

// Phase context
var goal=cp?cp.goal:null;
var phaseName=cp?cp.name:null;

// — Build the sentence —
var sentences=[];

// Sentence 1: What is happening (direction + magnitude)
var dirWord=’’;
var rateWord=’’;
if(absRate<0.1){
dirWord=‘stable’;
rateWord=’’;
}else if(weeklyRate<0){
dirWord=‘declining’;
rateWord=fmtW(absRate)+’/week’;
}else{
dirWord=‘increasing’;
rateWord=fmtW(absRate)+’/week’;
}

var s1=’’;
if(absRate<0.1){
s1=‘Weight has been <strong>stable</strong> over the last ‘+n+’ check-in’+(n!==1?‘s’:’’)+’, averaging no meaningful change week to week.’;
}else{
s1=‘Weight has been <strong>’+dirWord+’</strong> at approximately <strong>’+rateWord+’</strong> averaged across the last ‘+n+’ check-in’+(n!==1?‘s’:’’)+’.’;
}
if(mixed&&absRate>=0.1){
s1+=’ The direction has not been consistent week to week, which may reduce the reliability of the rate estimate.’;
}
sentences.push(s1);

// Sentence 2: Why / phase alignment
var s2=’’;
if(goal){
if(goal===‘cut’){
if(weeklyRate<-0.1&&absRate<=1.5){
s2=‘This aligns with a cut goal. The rate is within a range generally associated with primarily fat loss rather than muscle loss, though individual variation applies.’;
}else if(weeklyRate<-1.5){
s2=‘The rate of decline is above what is typically associated with a cut goal. Rates above 1–1.5 lbs/week sustained over multiple weeks may indicate a larger deficit than intended.’;
}else if(weeklyRate>0.1){
s2=‘This is inconsistent with the current cut goal. Weight is trending upward despite the phase objective.’;
}else{
s2=‘Weight is stable. For a cut goal, this may indicate intake is near maintenance.’;
}
}else if(goal===‘bulk’){
if(weeklyRate>0.1&&absRate<=0.75){
s2=‘This aligns with a bulk goal. The rate is within a range often associated with controlled surplus, though individual response varies.’;
}else if(weeklyRate>0.75){
s2=‘The rate of increase is above what is typically targeted in a controlled bulk. A faster rate may include a higher proportion of fat gain.’;
}else if(weeklyRate<-0.1){
s2=‘This is inconsistent with the current bulk goal. Weight is trending downward despite the phase objective.’;
}else{
s2=‘Weight is stable. For a bulk goal, this may indicate intake is near maintenance rather than in a surplus.’;
}
}else if(goal===‘maintain’){
if(absRate<0.3){
s2=‘This is consistent with a maintain goal. Weight is within a range that suggests near-maintenance intake.’;
}else if(weeklyRate<-0.3){
s2=‘The downward trend may indicate intake is below maintenance. For a maintain goal this may require review.’;
}else{
s2=‘The upward trend may indicate intake is above maintenance. For a maintain goal this may require review.’;
}
}
}else if(hasCal&&lastCal){
s2=‘No active phase is set, so the trend is reported without goal context.’;
}
if(s2)sentences.push(s2);

// Sentence 3: Calorie signal / what it may indicate
var s3=’’;
if(hasCal&&lastCal){
if(absRate>=0.1){
var impliedDef=weeklyRate*-3500/7; // negative = deficit
var calDir=impliedDef<0?‘surplus’:‘deficit’;
var calAbs=Math.abs(Math.round(impliedDef));
s3=‘Based on the rate of change alone, the data may suggest an implied <strong>’+calDir+’ of approximately ‘+calAbs+’ cal/day</strong> relative to maintenance. Logged calories this check-in: ‘+lastCal.toLocaleString()+’.’;
}else{
s3=‘Logged calories this check-in: ‘+lastCal.toLocaleString()+’. The stable weight trend is consistent with near-maintenance intake if logging is accurate.’;
}
}else if(!hasCal){
s3=‘Calorie data has not been logged on recent check-ins. Adding calorie data enables the adaptive maintenance estimate and calorie alignment signals.’;
}
if(s3)sentences.push(s3);

// Render
var confBadge=’<span class="trend-conf '+conf+'">’+confLabels[conf]+’</span>’;
el.innerHTML=sentences.join(’ ‘)+’<br><small style="color:var(--t4);font-size:11px;margin-top:10px;display:block;">Based on ‘+n+’ check-in’+(n!==1?‘s’:’’+(phaseName?’ · ‘+esc(phaseName):’’))+’. ‘+confLabels[conf]+’. Probabilistic — not a medical or clinical assessment.</small>’;
}

/* ============================================================ MACRO INSIGHT ENGINE */
function buildMacroRead(){
var card=q(‘macroCard’);
var body=q(‘macroInsightBody’);
var badge=q(‘macroConfBadge’);
if(!card||!body)return;

// Gather live check-ins that have macro data logged
var macCI=checkins.filter(function(c){
return !c.isBulk&&(c.protein||c.carbs||c.fats)&&c.macroMode;
}).sort(function(a,b){return b.startDate.localeCompare(a.startDate);});

// Need at least 3 check-ins with macro data before producing output
if(macCI.length<3){
card.style.display=‘none’;
return;
}
card.style.display=’’;

var cp=getCurPhase();
var goal=cp?cp.goal:null;
var n=Math.min(4,macCI.length);
var recent=macCI.slice(0,n);
var latest=recent[0];

// ── Helper: normalise a check-in to percentage split regardless of mode ──
function toPct(ci){
if(!ci.protein&&!ci.carbs&&!ci.fats)return null;
if(ci.macroMode===‘g’){
var p=ci.protein||0,c=ci.carbs||0,f=ci.fats||0;
var kcal=p*4+c*4+f*9;
if(!kcal)return null;
return{p:Math.round(p*4/kcal*100),c:Math.round(c*4/kcal*100),f:Math.max(0,100-Math.round(p*4/kcal*100)-Math.round(c*4/kcal*100)),mode:‘g’,pG:p,cG:c,fG:f,kcal:kcal};
}else{
var tot=(ci.protein||0)+(ci.carbs||0)+(ci.fats||0);
if(!tot)return null;
return{p:Math.round((ci.protein||0)/tot*100),c:Math.round((ci.carbs||0)/tot*100),f:Math.max(0,100-Math.round((ci.protein||0)/tot*100)-Math.round((ci.carbs||0)/tot*100)),mode:‘pct’};
}
}

var latestPct=toPct(latest);
var liveWI=weighIns.filter(function(w){return !w.isBulk;});
var currentWeight=liveWI.length?liveWI[0].weight:null; // stored in lbs

var insights=[];
var flags=[];

// ── Signal 1: Protein per lb of bodyweight (only when grams logged) ──
if(latest.macroMode===‘g’&&latest.protein&&currentWeight){
var protPerLb=Math.round(latest.protein/currentWeight*10)/10;
var protLine=‘Most recent check-in logged <strong>’+latest.protein+‘g protein</strong>, equivalent to approximately <strong>’+protPerLb+‘g per lb</strong> of current bodyweight (’+fmtW(currentWeight)+’).’;
// Contextual note based on phase goal
if(goal===‘cut’){
if(protPerLb<0.7){
protLine+=’ For a cut phase, intakes below approximately 0.7–0.8g/lb are often associated with greater lean mass loss relative to higher intakes. This may be worth monitoring if lean mass retention is a priority.’;
}else if(protPerLb>=0.7&&protPerLb<=1.2){
protLine+=’ This falls within a range commonly associated with lean mass retention during a caloric deficit.’;
}else{
protLine+=’ This is on the higher end of typical ranges. Intakes above approximately 1.0–1.2g/lb show diminishing returns in most research contexts.’;
}
}else if(goal===‘bulk’){
if(protPerLb<0.6){
protLine+=’ For a bulk phase focused on muscle gain, intakes below approximately 0.6–0.7g/lb may be insufficient to maximise muscle protein synthesis.’;
}else{
protLine+=’ This is consistent with ranges generally associated with adequate protein for a bulk phase.’;
}
}else if(goal===‘maintain’){
protLine+=’ For a maintenance phase, this provides context on protein adequacy relative to bodyweight.’;
}else{
protLine+=’ No active phase is set, so no goal-specific context is applied.’;
}
insights.push(protLine);
}

// ── Signal 2: Macro split alignment with phase goal ──
if(latestPct){
var alignLine=’’;
if(goal===‘cut’){
if(latestPct.p<25){
alignLine=‘The macro split shows protein at <strong>’+latestPct.p+’%</strong> of calories — relatively low for a cut phase. Higher protein allocation during a deficit is generally associated with greater lean mass preservation.’;
}else if(latestPct.f>40){
alignLine=‘Fat is at <strong>’+latestPct.f+’%</strong> of calories. A high fat allocation during a cut reduces the proportion of calories available from protein and carbohydrates, which may affect training performance and satiety differently than a higher-carb or higher-protein split.’;
}else{
alignLine=‘The macro split — protein <strong>’+latestPct.p+’%</strong>, carbs <strong>’+latestPct.c+’%</strong>, fat <strong>’+latestPct.f+’%</strong> — is structurally consistent with a cut phase.’;
}
}else if(goal===‘bulk’){
if(latestPct.p<20){
alignLine=‘Protein is at <strong>’+latestPct.p+’%</strong> of calories. For a bulk phase, insufficient protein may limit muscle protein synthesis even when total calories are in a surplus.’;
}else if(latestPct.c<35){
alignLine=‘Carbohydrates are at <strong>’+latestPct.c+’%</strong> of calories. For a bulk phase, higher carbohydrate allocation is often associated with better training performance and glycogen replenishment.’;
}else{
alignLine=‘The macro split — protein <strong>’+latestPct.p+’%</strong>, carbs <strong>’+latestPct.c+’%</strong>, fat <strong>’+latestPct.f+’%</strong> — is structurally consistent with a bulk phase.’;
}
}else if(goal===‘maintain’){
alignLine=‘Macro split this check-in: protein <strong>’+latestPct.p+’%</strong>, carbs <strong>’+latestPct.c+’%</strong>, fat <strong>’+latestPct.f+’%</strong>. No specific alignment concern relative to a maintain goal.’;
}
if(alignLine)insights.push(alignLine);
}

// ── Signal 3: Calorie-macro consistency check ──
if(latest.macroMode===‘g’&&latest.calories&&(latest.protein||latest.carbs||latest.fats)){
var p2=latest.protein||0,c2=latest.carbs||0,f2=latest.fats||0;
var impliedKcal=p2*4+c2*4+f2*9;
var calDiff=Math.abs(impliedKcal-latest.calories);
var calDiffPct=latest.calories>0?calDiff/latest.calories:0;
if(calDiffPct>0.15&&calDiff>150){
flags.push(‘Macro-calorie inconsistency: logged macros imply approximately <strong>’+Math.round(impliedKcal)+’ calories</strong>, but logged calories are <strong>’+latest.calories.toLocaleString()+’</strong> — a difference of ~‘+Math.round(calDiff)+’ cal. This may indicate a logging error in either field.’);
}
}

// ── Signal 4: Protein trend across recent check-ins ──
var protTrendCI=recent.filter(function(c){return c.macroMode===‘g’&&c.protein;});
if(protTrendCI.length>=3){
var protVals=protTrendCI.map(function(c){return c.protein;}).reverse(); // oldest first
var firstHalf=protVals.slice(0,Math.floor(protVals.length/2));
var secondHalf=protVals.slice(Math.floor(protVals.length/2));
var avgFirst=firstHalf.reduce(function(a,b){return a+b;},0)/firstHalf.length;
var avgSecond=secondHalf.reduce(function(a,b){return a+b;},0)/secondHalf.length;
var protShift=avgSecond-avgFirst;
if(Math.abs(protShift)>10){
var dir=protShift>0?‘increased’:‘decreased’;
insights.push(‘Protein intake has <strong>’+dir+’</strong> by approximately ’+Math.round(Math.abs(protShift))+‘g/day on average across the last ‘+protTrendCI.length+’ check-ins with gram data. This is a sustained directional shift, not a single-week variation.’);
}
}

// ── Signal 5: Fat floor check (only when grams, only sustained low) ──
var fatGramCI=recent.filter(function(c){return c.macroMode===‘g’&&c.fats!=null&&c.calories;});
if(fatGramCI.length>=3){
var allLowFat=fatGramCI.every(function(c){
var fatPct=(c.fats*9)/c.calories*100;
return fatPct<18;
});
if(allLowFat){
var avgFatPct=Math.round(fatGramCI.reduce(function(a,c){return a+(c.fats*9/c.calories*100);},0)/fatGramCI.length);
flags.push(‘Fat intake has been consistently low — averaging approximately <strong>’+avgFatPct+’%</strong> of calories across the last ‘+fatGramCI.length+’ check-ins. Chronically low dietary fat (below ~15–20% of calories) may affect hormone function. This is noted as a contextual signal, not a recommendation.’);
}
}

// ── Confidence ──
var conf=macCI.length>=4?‘high’:macCI.length>=3?‘med’:‘low’;
var confLabels={high:‘High confidence’,med:‘Moderate confidence’,low:‘Low confidence’};
if(badge)badge.innerHTML=’<span class="trend-conf '+conf+'">’+confLabels[conf]+’</span>’;

// ── Render ──
if(!insights.length&&!flags.length){
body.innerHTML=’<div style="font-size:13px;color:var(--t3);">Macro pattern over the last ‘+n+’ check-in’+(n!==1?‘s’:’’)+’ shows no signals requiring attention at this time.</div>’;
return;
}
var html=’’;
insights.forEach(function(s,i){
html+=’<div class="trend-read" style="margin-bottom:'+(i<insights.length-1||flags.length?'14px':'0')+';">’+s+’</div>’;
});
flags.forEach(function(f,i){
html+=’<div style="margin-top:'+(insights.length?'10px':'0')+';padding:10px 14px;background:var(--warn-bg);border-radius:var(--r6);font-size:13px;color:var(--t2);line-height:1.65;">’+f+’</div>’;
});
html+=’<small style="color:var(--t4);font-size:11px;margin-top:12px;display:block;">Based on ‘+n+’ check-in’+(n!==1?‘s’:’’)+’ with macro data. ‘+confLabels[conf]+’. Contextual signals only — not medical or nutritional advice.</small>’;
body.innerHTML=html;
}

/* ============================================================ PHASE COMPARISON */
function fillComparePickers(){
[‘cmpPhaseA’,‘cmpPhaseB’].forEach(function(pid){
var sel=q(pid);if(!sel)return;
var prev=sel.value;
sel.innerHTML=’<option value="">— Select phase —</option>’;
phases.slice().sort(function(a,b){return b.startDate.localeCompare(a.startDate);}).forEach(function(ph){
sel.innerHTML+=’<option value="'+ph.id+'">’+esc(ph.name)+(ph.goal?’ (’+ph.goal+’)’:’’)+’</option>’;
});
if(phases.find(function(p){return p.id===prev;}))sel.value=prev;
});
}

function getPhaseStats(id){
var ph=phases.find(function(p){return p.id===id;});
if(!ph)return null;
var liveCI=checkins.filter(function(c){return c.phaseId===id&&!c.isBulk;}).sort(function(a,b){return a.startDate.localeCompare(b.startDate);});
var allCI=checkins.filter(function(c){return c.phaseId===id;}).sort(function(a,b){return a.startDate.localeCompare(b.startDate);});
var dur=null;
if(ph.startDate){var days=Math.round((toDate(ph.endDate||todayStr())-toDate(ph.startDate))/(24*3600*1000));dur=Math.round(days/7);}
var withW=allCI.filter(function(c){return c.avgWeight;});
var totalChg=withW.length>=2?Math.round((withW[withW.length-1].avgWeight-withW[0].avgWeight)*10)/10:null;
var startW=withW.length?withW[0].avgWeight:(ph.startWeight||null);
var endW=withW.length?withW[withW.length-1].avgWeight:null;
// Weekly rate = total change / weeks
var weeklyRate=totalChg!=null&&dur&&dur>0?Math.round(totalChg/dur*100)/100:null;
var calCI=liveCI.filter(function(c){return c.calories;});
var avgCal=calCI.length?Math.round(div(calCI.reduce(function(a,c){return a+c.calories;},0),calCI.length)):null;
var scores=liveCI.filter(function(c){return c.score!=null;});
var avgScore=scores.length?Math.round(div(scores.reduce(function(a,c){return a+c.score;},0),scores.length)):null;
// Protein avg from live CIs with gram data
var protCI=liveCI.filter(function(c){return c.macroMode===‘g’&&c.protein;});
var avgProt=protCI.length?Math.round(div(protCI.reduce(function(a,c){return a+c.protein;},0),protCI.length)):null;
return{ph:ph,dur:dur,totalChg:totalChg,startW:startW,endW:endW,weeklyRate:weeklyRate,avgCal:avgCal,avgScore:avgScore,avgProt:avgProt,checkIns:liveCI.length,allCheckIns:allCI.length};
}

function renderComparison(){
var el=q(‘cmpResult’);if(!el)return;
var idA=q(‘cmpPhaseA’)?q(‘cmpPhaseA’).value:’’;
var idB=q(‘cmpPhaseB’)?q(‘cmpPhaseB’).value:’’;
if(!idA||!idB){
el.innerHTML=’<div class="empty" style="padding:32px;"><div class="empty-sub">Select two phases above to see the comparison.</div></div>’;
return;
}
if(idA===idB){
el.innerHTML=’<div class="empty" style="padding:24px;"><div class="empty-sub">Select two different phases to compare.</div></div>’;
return;
}
var a=getPhaseStats(idA),b=getPhaseStats(idB);
if(!a||!b){el.innerHTML=’<div class="empty" style="padding:24px;"><div class="empty-sub">Could not load phase data.</div></div>’;return;}

// Helper: render a comparison cell pair with winner highlight
// winFn(aVal,bVal) returns ‘a’,‘b’, or ‘tie’
function row(label,aStr,bStr,winner){
var aCls=winner===‘a’?‘cmp-win’:winner===‘tie’?‘cmp-neu’:’’;
var bCls=winner===‘b’?‘cmp-win’:winner===‘tie’?‘cmp-neu’:’’;
return ‘<div class="cmp-lbl">’+label+’</div>’+
‘<div class="cmp-cell a'+(aCls?' '+aCls:'')+'">’+aStr+’</div>’+
‘<div class="cmp-cell b'+(bCls?' '+bCls:'')+'">’+bStr+’</div>’;
}

var html=’<div class="cmp-grid">’;
// Headers
html+=’<div class="cmp-hd a"><span class="badge bc-'+(a.ph.goal||'cut')+'" style="margin-right:6px;">’+(a.ph.goal||’—’)+’</span>’+esc(a.ph.name)+’</div>’;
html+=’<div class="cmp-hd"><span class="badge bc-'+(b.ph.goal||'cut')+'" style="margin-right:6px;">’+(b.ph.goal||’—’)+’</span>’+esc(b.ph.name)+’</div>’;

// Duration
var durWin=a.dur!=null&&b.dur!=null?(a.dur>b.dur?‘a’:b.dur>a.dur?‘b’:‘tie’):‘tie’;
html+=row(‘Duration’,a.dur!=null?a.dur+’ wks’:’—’,b.dur!=null?b.dur+’ wks’:’—’,‘tie’);

// Date range
html+=’<div class="cmp-lbl">Date range</div>’;
html+=’<div class="cmp-cell a" style="font-size:12px;">’+fmtD(a.ph.startDate)+’ — ‘+(a.ph.endDate?fmtD(a.ph.endDate):‘Present’)+’</div>’;
html+=’<div class="cmp-cell b" style="font-size:12px;">’+fmtD(b.ph.startDate)+’ — ‘+(b.ph.endDate?fmtD(b.ph.endDate):‘Present’)+’</div>’;

// Weight change — winner depends on goal of each phase independently
var aChgStr=a.totalChg!=null?(a.totalChg>0?’+’:’’)+fmtW(a.totalChg):’—’;
var bChgStr=b.totalChg!=null?(b.totalChg>0?’+’:’’)+fmtW(b.totalChg):’—’;
html+=row(‘Total weight change’,aChgStr,bChgStr,‘tie’);

// Start → End weight
html+=’<div class="cmp-lbl">Start → End weight</div>’;
html+=’<div class="cmp-cell a">’+(a.startW?fmtW(a.startW):’—’)+’ → ‘+(a.endW?fmtW(a.endW):’—’)+’</div>’;
html+=’<div class="cmp-cell b">’+(b.startW?fmtW(b.startW):’—’)+’ → ‘+(b.endW?fmtW(b.endW):’—’)+’</div>’;

// Weekly rate — for cuts, more negative is better; for bulks, more positive is better
var aRateStr=a.weeklyRate!=null?(a.weeklyRate>0?’+’:’’)+fmtW(a.weeklyRate)+’/wk’:’—’;
var bRateStr=b.weeklyRate!=null?(b.weeklyRate>0?’+’:’’)+fmtW(b.weeklyRate)+’/wk’:’—’;
html+=row(‘Avg weekly rate’,aRateStr,bRateStr,‘tie’);

// Avg daily calories — lower is better on cut, higher on bulk, tie on maintain
var calWin=‘tie’;
if(a.avgCal!=null&&b.avgCal!=null){
if(a.ph.goal===‘cut’&&b.ph.goal===‘cut’)calWin=a.avgCal<b.avgCal?‘a’:b.avgCal<a.avgCal?‘b’:‘tie’;
else if(a.ph.goal===‘bulk’&&b.ph.goal===‘bulk’)calWin=a.avgCal>b.avgCal?‘a’:b.avgCal>a.avgCal?‘b’:‘tie’;
}
html+=row(‘Avg daily calories’,a.avgCal?a.avgCal.toLocaleString()+’ cal’:’—’,b.avgCal?b.avgCal.toLocaleString()+’ cal’:’—’,calWin);

// Avg protein
html+=row(‘Avg daily protein (g)’,a.avgProt?a.avgProt+‘g’:’—’,b.avgProt?b.avgProt+‘g’:’—’,
a.avgProt!=null&&b.avgProt!=null?(a.avgProt>b.avgProt?‘a’:b.avgProt>a.avgProt?‘b’:‘tie’):‘tie’);

// Consistency score — higher is always better
var scoreWin=‘tie’;
if(a.avgScore!=null&&b.avgScore!=null)scoreWin=a.avgScore>b.avgScore?‘a’:b.avgScore>a.avgScore?‘b’:‘tie’;
html+=row(‘Avg consistency’,a.avgScore!=null?a.avgScore+’ / 100’:’—’,b.avgScore!=null?b.avgScore+’ / 100’:’—’,scoreWin);

// Check-ins
html+=row(‘Check-ins logged’,
a.checkIns+(a.allCheckIns>a.checkIns?’ + ‘+(a.allCheckIns-a.checkIns)+’ bulk’:’’),
b.checkIns+(b.allCheckIns>b.checkIns?’ + ‘+(b.allCheckIns-b.checkIns)+’ bulk’:’’),
a.checkIns>b.checkIns?‘a’:b.checkIns>a.checkIns?‘b’:‘tie’);

html+=’</div>’;

// Measurement delta comparison
var measA=getMeasDeltaForPhase(idA,a.ph.startDate,a.ph.endDate);
var measB=getMeasDeltaForPhase(idB,b.ph.startDate,b.ph.endDate);
if(measA||measB){
html+=’<div style="margin-top:4px;border:1px solid var(--br);border-radius:var(--r14);overflow:hidden;">’;
html+=’<div style="display:grid;grid-template-columns:1fr 1fr;border-bottom:1px solid var(--br);">’;
html+=’<div class="cmp-hd a" style="font-size:12px;">’+esc(a.ph.name)+’ — measurements</div>’;
html+=’<div class="cmp-hd" style="font-size:12px;">’+esc(b.ph.name)+’ — measurements</div>’;
html+=’</div>’;
// Collect all keys present in either
var allKeys={};
if(measA)Object.keys(measA).forEach(function(k){allKeys[k]=1;});
if(measB)Object.keys(measB).forEach(function(k){allKeys[k]=1;});
html+=’<div style="display:grid;grid-template-columns:1fr 1fr;">’;
Object.keys(allKeys).forEach(function(k){
var dA=measA?measA[k]:null;
var dB=measB?measB[k]:null;
var unit=dA?(dA.isBf?’%’:’ in’):(dB?(dB.isBf?’%’:’ in’):’ in’);
var label=dA?dA.label:(dB?dB.label:k);
var aStr=dA?(dA.delta>0?’+’:’’)+dA.delta+unit:’—’;
var bStr=dB?(dB.delta>0?’+’:’’)+dB.delta+unit:’—’;
html+=’<div class="cmp-cell a" style="font-size:12px;"><span style="color:var(--t3);margin-right:6px;">’+label+’</span>’+aStr+’</div>’;
html+=’<div class="cmp-cell b" style="font-size:12px;"><span style="color:var(--t3);margin-right:6px;">’+label+’</span>’+bStr+’</div>’;
});
html+=’</div></div>’;
}

html+=’<p style="font-size:11px;color:var(--t4);margin-top:12px;line-height:1.6;">Green highlights indicate a stronger result in that metric. Goal context is applied where relevant (e.g. lower calories on a cut, higher on a bulk). Metrics without a universal better/worse direction show no highlight.</p>’;
el.innerHTML=html;
}

/* ============================================================ PROGRESS PHOTOS */
var photoCompareSelection=[];

function initPhotoForm(){
var dateEl=q(‘photoDate’);
if(dateEl){dateEl.value=todayStr();dateEl.max=todayStr();}
// Populate phase picker
var sel=q(‘photoPhase’);
if(sel){
var prev=sel.value;
sel.innerHTML=’<option value="">— No phase —</option>’;
phases.slice().sort(function(a,b){return b.startDate.localeCompare(a.startDate);}).forEach(function(ph){
sel.innerHTML+=’<option value="'+ph.id+'">’+esc(ph.name)+’</option>’;
});
if(prev&&phases.find(function(p){return p.id===prev;}))sel.value=prev;
}
}

function onPhotoSelected(){
var file=q(‘photoFile’).files[0];
if(!file)return;
if(file.size>8*1024*1024){toast(‘Image too large — keep it under 8MB’,‘err’);return;}
var reader=new FileReader();
reader.onload=function(e){
var preview=q(‘photoPreview’),wrap=q(‘photoPreviewWrap’);
if(preview){preview.src=e.target.result;}
if(wrap)wrap.style.display=‘block’;
};
reader.readAsDataURL(file);
}

function savePhoto(){
var file=q(‘photoFile’).files[0];
var dateEl=q(‘photoDate’);
var ds=dateEl?dateEl.value:todayStr();
if(!ds||ds>todayStr()){toast(‘Select a valid date’,‘err’);return;}
if(!file){toast(‘Select an image first’,‘err’);return;}
var reader=new FileReader();
reader.onload=function(e){
var dataUrl=e.target.result;
var en={
id:‘ph-’+Date.now()+’-’+Math.floor(Math.random()*9999),
date:ds,
phaseId:q(‘photoPhase’)?q(‘photoPhase’).value||null:null,
note:q(‘photoNote’)?q(‘photoNote’).value.trim():’’,
dataUrl:dataUrl
};
photos.push(en);
photos.sort(function(a,b){return b.date.localeCompare(a.date);});
Local.set(‘photos’,photos);
clearPhotoForm();
renderPhotos();
toast(‘Photo saved’);
};
reader.readAsDataURL(file);
}

function clearPhotoForm(){
var fi=q(‘photoFile’);if(fi)fi.value=’’;
var prev=q(‘photoPreview’),wrap=q(‘photoPreviewWrap’);
if(prev)prev.src=’’;if(wrap)wrap.style.display=‘none’;
var note=q(‘photoNote’);if(note)note.value=’’;
var dateEl=q(‘photoDate’);if(dateEl){dateEl.value=todayStr();dateEl.max=todayStr();}
if(q(‘photoPhase’))q(‘photoPhase’).selectedIndex=0;
}

function delPhoto(id){
if(!confirm(‘Delete this photo? This cannot be undone.’))return;
photos=photos.filter(function(p){return p.id!==id;});
photoCompareSelection=photoCompareSelection.filter(function(sid){return sid!==id;});
Local.set(‘photos’,photos);
renderPhotos();
renderPhotoCompare();
}

function togglePhotoSelect(id){
var idx=photoCompareSelection.indexOf(id);
if(idx>=0){
photoCompareSelection.splice(idx,1);
}else{
if(photoCompareSelection.length>=2)photoCompareSelection.shift();
photoCompareSelection.push(id);
}
renderPhotos();
renderPhotoCompare();
}

function clearPhotoCompare(){
photoCompareSelection=[];
renderPhotos();
renderPhotoCompare();
}

function renderPhotoCompare(){
var card=q(‘photoCompareCard’);
var grid=q(‘photoCompareGrid’);
if(!card||!grid)return;
if(photoCompareSelection.length===0){card.style.display=‘none’;grid.innerHTML=’’;return;}
card.style.display=’’;
var html=’’;
photoCompareSelection.forEach(function(id){
var ph=photos.find(function(p){return p.id===id;});
if(!ph)return;
var phase=ph.phaseId?phases.find(function(p){return p.id===ph.phaseId;}):null;
html+=’<div>’;
html+=’<img src="'+ph.dataUrl+'" alt="Progress photo '+fmtD(ph.date)+'">’;
html+=’<div class="photo-compare-lbl">’+fmtFull(ph.date)+(phase?’ · ‘+esc(phase.name):’’)+(ph.note?’ · ‘+esc(ph.note):’’)+’</div>’;
html+=’</div>’;
});
grid.innerHTML=html;
}

function renderPhotos(){
var el=q(‘photoList’);if(!el)return;
if(!photos.length){
el.innerHTML=’<div class="empty" style="padding:32px;"><div class="empty-sub">No photos yet. Add your first above.</div></div>’;
return;
}
// Group by phase, then ungrouped
var groups={},order=[];
photos.forEach(function(ph){
var key=ph.phaseId||’**none**’;
if(!groups[key]){groups[key]=[];order.push(key);}
groups[key].push(ph);
});
order=order.filter(function(v,i){return order.indexOf(v)===i;});
var html=’’;
order.forEach(function(key){
var items=groups[key];
var phase=key!==’**none**’?phases.find(function(p){return p.id===key;}):null;
var grpName=phase?phase.name:‘Unphased’;
var sid=‘pg-’+key.replace(/[^a-z0-9]/gi,’-’);
var isOpen=key===(getCurPhase()?getCurPhase().id:null)||order.length===1||key===’**none**’;
html+=’<div class="mg"><div class="mg-hd" onclick="togMG(\''+sid+'\')">’;
html+=’<span class="mg-ttl">’+esc(grpName)+’</span>’;
html+=’<span style="display:flex;align-items:center;gap:8px;"><span class="mg-meta">’+items.length+’ photo’+(items.length!==1?‘s’:’’)+’</span><span class="mg-chev'+(isOpen?' open':'')+'">▼</span></span>’;
html+=’</div><div class="mg-body'+(isOpen?' open':'')+'" id="'+sid+'" style="padding:12px;">’;
html+=’<div class="photo-grid">’;
items.forEach(function(ph){
var isSel=photoCompareSelection.indexOf(ph.id)>=0;
var selNum=photoCompareSelection.indexOf(ph.id)+1;
html+=’<div class=“photo-thumb’+(isSel?’ sel’:’’)+’” onclick=“togglePhotoSelect('’+ph.id+’')” title=”’+fmtFull(ph.date)+(ph.note?’ — ‘+esc(ph.note):’'’)+’'>’;
html+=’<img src="'+ph.dataUrl+'" alt="Progress '+fmtD(ph.date)+'" loading="lazy">’;
html+=’<div class="photo-thumb-meta">’+fmtD(ph.date)+(ph.note?’<br>’+esc(ph.note):’’)+’</div>’;
if(isSel)html+=’<div style="position:absolute;top:5px;left:5px;width:20px;height:20px;border-radius:50%;background:var(--accent);color:#fff;font-size:11px;font-weight:700;display:flex;align-items:center;justify-content:center;">’+selNum+’</div>’;
html+=’<button class="photo-del" onclick="event.stopPropagation();delPhoto(\''+ph.id+'\')">×</button>’;
html+=’</div>’;
});
html+=’</div></div></div>’;
});
el.innerHTML=html;
}

/* ============================================================ FORGOT PASSWORD */
function handleForgotPw(){
var email=q(‘authEmail’).value.trim();
if(!email){showMsg(‘Enter your email address first, then click Forgot password.’,‘err’);return;}
if(DEMO){showMsg(‘Password reset is not available in demo mode. Sign in with your password.’,‘inf’);return;}
if(!sbc){showMsg(‘Not connected. Check your Supabase config.’,‘err’);return;}
var btn=q(‘forgotBtn’);btn.textContent=‘Sending…’;btn.disabled=true;
sbc.auth.resetPasswordForEmail(email,{redirectTo:window.location.href}).then(function(res){
if(res.error){showMsg(res.error.message||‘Could not send reset email.’,‘err’);}
else{showMsg(‘Reset link sent — check your email (including spam folder).’,‘inf’);}
btn.textContent=‘Forgot password?’;btn.disabled=false;
}).catch(function(e){showMsg(e.message||‘Error sending reset email.’,‘err’);btn.textContent=‘Forgot password?’;btn.disabled=false;});
}

/* ============================================================ BOOT */
function boot(){
applyTheme(appState.theme);
if(DEMO){var sess=Local.getG(‘demoSess’,null);if(sess&&sess.email){var us=Local.getG(‘demoUsers’,{});var hit=us[sess.email.toLowerCase()];if(hit){appState.user={id:hit.id,email:hit.email};appState.profile={display_name:hit.name,email:hit.email};enterApp(false);}}}
else if(sbc){sbc.auth.getSession().then(function(res){if(res.data&&res.data.session){appState.user=res.data.session.user;loadProf().then(function(){enterApp(false);});}});}
}
boot();
if(‘serviceWorker’ in navigator){window.addEventListener(‘load’,function(){navigator.serviceWorker.register(‘sw.js’).catch(function(){});});}
</script>

</body>
</html>
