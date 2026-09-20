[index.html](https://github.com/user-attachments/files/32427551/index.html)
<!doctype html>
<html lang="ko">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="color-scheme" content="light">
<title>빨대 팬플룻 연구소</title>
<!-- 2026-09-18 수정: 폰·패드 터치 소리 잠금·탭 반응 보강 / 폰에서도 세로 팬플룻 / 1단계 완성 연출 정리 -->
<!-- 2026-09-19: 다시수학 연구회 공통 디자인(design-miro.md) 적용 — 글꼴·알약 버튼·28px 파스텔 카드·팔레트 색, 연구회 로고를 왼쪽 상단 교구명 옆에 삽입, 전자칠판 전체 화면 버튼 -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@400;500;600&display=swap">
<style>
/* ---------- 디자인 토큰 : 다시수학 연구회 공통 디자인(design-miro.md)의 색·글꼴·모서리·그림자 ---------- */
:root{
  /* 팔레트 (design.md colors) */
  --canvas:#ffffff; --surface:#f7f8fa; --surface-soft:#fafbfc; --surface-yellow:#fff8e0;
  --hairline:#e0e2e8; --hairline-soft:#eef0f3; --hairline-strong:#c7cad5;
  --ink:#1c1c1e; --ink-deep:#050038; --charcoal:#2c2c34; --slate:#555a6a; --steel:#6b6f7e; --stone:#8e91a0; --muted:#a5a8b5;
  --brand-yellow:#ffd02f; --yellow-light:#fff4c4; --yellow-dark:#746019;
  --brand-blue:#4262ff; --blue-pressed:#2a41b6;
  --coral-light:#ffc6c6; --coral-dark:#600000; --rose-light:#fde0f0; --teal-light:#c3faf5; --moss-dark:#187574; --brand-teal:#0fbcb0; --orange-light:#ffe6cd;
  --success:#00b473;
  /* 프로그램 안에서 쓰는 이름 → 팔레트 */
  --paper:var(--canvas); --paper-2:var(--surface); --ink-2:var(--slate); --ink-3:var(--stone); --line:var(--hairline); --card:var(--canvas);
  --primary:var(--ink); --primary-2:var(--charcoal); --on-primary:#ffffff;
  --ok:var(--success); --ok-2:#008f5b; --bad:var(--coral-dark); --warn:#fcb900;
  /* 교구 자체의 색 (빨대·마개·테이프·받침) — 디자인 팔레트가 아닌 실물 색 */
  --tape:#F6CF3B;  --tape-2:#D9AE1C;
  --stopper:#D9453B; --stopper-2:#A32E27;
  --plastic-a:#FFFFFF; --plastic-b:#D9ECF6; --plastic-line:#8FBBD1;
  --wood:#EBDABC; --wood-2:#CFB283;
  /* 색깔 음계 (도=빨강 … 시=보라, 높은 도=밝은 빨강: 같은 음이름) — 학습 내용이라 유지 */
  --c-do:#E5533C; --c-re:#F08A24; --c-mi:#E9B92A; --c-fa:#5DB74A; --c-sol:#2FB0C6; --c-la:#3F73D8; --c-si:#8B5CD6; --c-do2:#F2857A;
  /* 모서리·그림자 (rounded.xl / rounded.xxxl / elevation 2·3·4) */
  --radius:16px; --radius-lg:28px; --pill:9999px;
  --shadow:rgba(5,0,56,.06) 0 4px 12px 0; --shadow-mockup:rgba(5,0,56,.08) 0 12px 32px -4px; --shadow-modal:rgba(5,0,56,.12) 0 16px 48px -8px;
  /* 글꼴: Roobert PRO, 없으면 Noto Sans KR (굵기 400·500·600만 사용) */
  --font:'Roobert PRO','Noto Sans KR','Noto Sans',-apple-system,BlinkMacSystemFont,system-ui,sans-serif;
  --font-display:var(--font); --font-body:var(--font); --font-hand:var(--font);
  --header-h:64px;
}
*{box-sizing:border-box}
html,body{height:100%}
body{
  margin:0;background:var(--canvas);color:var(--ink);
  font-family:var(--font);font-size:16px;line-height:1.5;font-weight:400;
  -webkit-text-size-adjust:100%;overscroll-behavior:none;
  -webkit-tap-highlight-color:transparent;-webkit-touch-callout:none;
  overflow:hidden;
}
button,input,select{font-family:inherit}
[hidden]{display:none!important}
/* 터치: 버튼류는 탭 지연·두 번 탭 확대 없이 바로 반응하고, 길게 눌러도 글자가 선택되지 않게 */
button,select,input,.btn,.tab,.card,.song-chip,.icon-btn,.brand{touch-action:manipulation}
button{-webkit-user-select:none;user-select:none}

#app{height:100vh;height:100dvh;display:flex;flex-direction:column;overflow:hidden;background:var(--canvas)}

/* ---------- 헤더 ---------- */
.hdr{height:var(--header-h);flex:0 0 auto;display:flex;align-items:center;gap:10px;padding:0 16px;
  background:var(--canvas);border-bottom:1px solid var(--hairline);}
.brand{display:flex;align-items:center;gap:10px;cursor:pointer;border:0;background:none;padding:6px 8px;border-radius:12px;color:var(--ink)}
.brand:hover{background:var(--surface)}
.brand .logo{width:38px;height:38px;object-fit:contain;display:block} /* 다시수학 연구회 로고 (교구명 왼쪽) */
.brand .name{font-family:var(--font);font-size:20px;font-weight:500;letter-spacing:-.2px;white-space:nowrap;color:var(--ink)}
/* 단계 탭 = pill-tab / pill-tab-active */
.tabs{margin-left:auto;margin-right:auto;display:flex;gap:6px;background:transparent;padding:0}
.tab{border:1px solid var(--hairline);background:var(--canvas);color:var(--steel);font-family:var(--font);font-size:14px;font-weight:500;padding:6px 14px 6px 6px;border-radius:var(--pill);cursor:pointer;display:flex;align-items:center;gap:8px;white-space:nowrap;line-height:1.3}
.tab .num{width:26px;height:26px;border-radius:50%;background:var(--surface);display:grid;place-items:center;font-size:13px;font-weight:600;color:var(--ink)}
.tab.on{background:var(--ink);color:#fff;border-color:var(--ink)}
.tab.on .num{background:#fff;color:var(--ink)}
.tab.done .num{background:var(--success);color:#fff}
.tab:focus-visible,.icon-btn:focus-visible,.brand:focus-visible{outline:2px solid var(--brand-blue);outline-offset:2px}
.hdr-right{display:flex;gap:8px;align-items:center}
/* 원형 아이콘 버튼 = button-icon-circular, 글자 있는 것은 button-secondary */
.icon-btn{border:1px solid var(--hairline);background:var(--canvas);color:var(--ink);font-size:14px;font-weight:500;font-family:var(--font);width:40px;height:40px;padding:0;border-radius:var(--pill);cursor:pointer;display:flex;align-items:center;justify-content:center;gap:6px;line-height:1.3}
.icon-btn:hover{background:var(--surface)}
.icon-btn:active{background:var(--hairline-soft)}
.icon-btn svg{width:20px;height:20px}
.icon-btn .label{display:none}
.icon-btn.pill{width:auto;padding:0 16px 0 12px;border-color:var(--hairline-strong)}
.icon-btn.pill .label{display:inline}

/* ---------- 공통 ---------- */
main#view{flex:1 1 auto;min-height:0;display:flex;flex-direction:column;position:relative}
.stage{flex:1 1 auto;min-height:0;display:flex;flex-direction:column}
.stage-bar{flex:0 0 auto;display:flex;align-items:center;flex-wrap:wrap;gap:10px 14px;padding:12px 20px;min-height:56px;margin:10px 12px 0;
  border-radius:20px;background:var(--surface);border:1px solid var(--hairline-soft)}
.stage.s1 .stage-bar{background:var(--yellow-light)} .stage.s2 .stage-bar{background:var(--teal-light)} .stage.s3 .stage-bar{background:var(--rose-light)}
/* 단계 이름 = badge (caption-bold, pill) */
.stage-bar h2{font-family:var(--font);font-size:14px;font-weight:600;line-height:1.4;margin:0;white-space:nowrap;padding:5px 12px;border-radius:var(--pill);background:var(--canvas);color:var(--ink);border:1px solid var(--hairline-soft)}
.stage-bar .msg{flex:1 1 260px;font-size:18px;font-weight:500;line-height:1.4;color:var(--ink);min-width:0}
.stage-bar .msg b{color:var(--ink-deep);font-weight:600}
.stage-body{flex:1 1 auto;min-height:0;display:flex;gap:12px;padding:10px 12px 12px}
/* 책상(보드) = whiteboard-mockup: 연한 회색 캔버스 위 점 격자, 28px 모서리, hairline 테두리, 목업 그림자 */
.desk{flex:1 1 auto;min-width:0;min-height:0;position:relative;border-radius:var(--radius-lg);overflow:hidden;
  background:var(--surface);box-shadow:var(--shadow-mockup);border:1px solid var(--hairline-soft)}
.desk svg.sheet{position:absolute;inset:0;width:100%;height:100%;display:block;touch-action:none;user-select:none;-webkit-user-select:none}

.btn{font-family:var(--font);font-size:16px;font-weight:500;line-height:1.3;padding:12px 24px;border-radius:var(--pill);border:1px solid transparent;
  background:var(--ink);color:#fff;cursor:pointer;box-shadow:none;
  display:inline-flex;align-items:center;gap:8px;white-space:nowrap;transition:background .15s,color .15s}
.btn:active{background:var(--charcoal)}
.btn.secondary{background:transparent;color:var(--ink);border-color:var(--hairline-strong)}   /* button-secondary */
.btn.secondary:active{background:var(--surface)}
.btn.tape{background:var(--brand-blue);color:#fff}                                          /* button-blue: 다음 단계·다시 도전 */
.btn.tape:active{background:var(--blue-pressed)}
.btn.rhythm{background:var(--brand-blue);color:#fff}
.btn.rhythm:active{background:var(--blue-pressed)}
.btn.ok{background:var(--success);color:#fff}
.btn.sm{font-size:15px;padding:10px 18px}
.btn.lg{font-size:18px;padding:14px 28px}
.btn:disabled{background:var(--hairline);color:var(--muted);border-color:transparent;cursor:not-allowed}
.btn.secondary:disabled{background:transparent;color:var(--muted);border-color:var(--hairline)}
.btn:focus-visible{outline:2px solid var(--brand-blue);outline-offset:2px}
.btn svg{width:20px;height:20px}

/* 진행 표시 = pill-tab */
.chip{display:inline-flex;align-items:center;gap:6px;padding:7px 14px;border-radius:var(--pill);background:var(--canvas);border:1px solid var(--hairline);font-size:14px;font-weight:500;color:var(--steel);line-height:1.3}
.chip b{color:var(--ink);font-weight:600}


/* 토스트 */
#toast{position:fixed;left:50%;bottom:22px;transform:translate(-50%,20px);opacity:0;pointer-events:none;
  background:var(--ink);color:#fff;font-family:var(--font);font-size:16px;font-weight:500;line-height:1.4;padding:12px 22px;border-radius:var(--pill);
  box-shadow:var(--shadow-modal);transition:opacity .2s,transform .25s;z-index:60;max-width:min(92vw,560px);text-align:center}
#toast.show{opacity:1;transform:translate(-50%,0)}
#toast.bad{background:var(--coral-light);color:var(--coral-dark)} #toast.ok{background:var(--success);color:#fff}

/* 다이얼로그 */
dialog{border:1px solid var(--hairline-soft);border-radius:24px;padding:0;background:var(--canvas);color:var(--ink);box-shadow:var(--shadow-modal);max-width:min(94vw,540px);width:100%;max-height:92vh;max-height:92dvh;overflow:auto}
dialog::backdrop{background:rgba(5,0,56,.35);backdrop-filter:blur(3px)}
.dlg{padding:28px 28px 24px;display:flex;flex-direction:column;gap:14px}
.dlg h2{font-family:var(--font);font-size:28px;font-weight:500;letter-spacing:-.5px;line-height:1.25;margin:0;text-align:center;text-wrap:balance}
.dlg p{margin:0;font-size:16px;color:var(--slate);text-align:center}
.dlg .row{display:flex;gap:10px;justify-content:center;flex-wrap:wrap}
.dlg .score{font-family:var(--font);font-weight:500;letter-spacing:-1.5px;font-size:64px;line-height:1.1;text-align:center;font-variant-numeric:tabular-nums}
.dlg .score small{font-size:22px;color:var(--slate);letter-spacing:0}
.stars{display:flex;justify-content:center;gap:8px;font-size:44px;line-height:1}
.stars span{color:var(--hairline);transition:transform .3s}
.stars span.lit{color:var(--brand-yellow);animation:pop .5s cubic-bezier(.2,1.6,.4,1) both}
@keyframes pop{from{transform:scale(.2)}to{transform:scale(1)}}
.settings-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:8px}
.settings-grid label{display:flex;flex-direction:column;gap:4px;font-size:14px;font-weight:600}
.settings-grid input{font-size:16px;padding:8px;height:44px;border:1px solid var(--hairline-strong);border-radius:8px;width:100%;text-align:center;font-variant-numeric:tabular-nums;color:var(--ink);background:var(--canvas)} /* text-input */
.settings-grid input:focus{outline:0;border:2px solid var(--brand-blue)}
.field{display:flex;align-items:center;justify-content:space-between;gap:10px;font-size:15px;font-weight:500}
.field select{font-size:15px;padding:8px 12px;height:40px;border-radius:8px;border:1px solid var(--hairline-strong);background:var(--canvas);color:var(--ink)}

/* ---------- 홈 ---------- */
.home{flex:1 1 auto;min-height:0;display:grid;grid-template-rows:auto 1fr auto;padding:8px 20px 16px;gap:8px;overflow:auto}
.home .hero{display:flex;align-items:center;justify-content:center;gap:24px;flex-wrap:wrap;text-align:center}
.home h1{font-family:var(--font);font-weight:500;font-size:clamp(30px,4vw,48px);line-height:1.15;margin:0;letter-spacing:-1px;text-wrap:balance}
.home h1 .u{background:linear-gradient(transparent 58%, var(--brand-yellow) 58%, var(--brand-yellow) 90%, transparent 90%)} /* 브랜드 노랑은 강조 표시에만 */
.home .sub{font-family:var(--font);font-weight:400;font-size:clamp(16px,1.6vw,18px);color:var(--slate);margin:4px 0 0}
.home .desk{max-height:100%;min-height:200px}
.home-flute{position:relative;flex:1 1 auto;min-height:0;display:flex;justify-content:center}
.home-flute .desk{width:min(100%,900px);height:100%}
.home-flute .hint{position:absolute;bottom:14px;right:16px;font-family:var(--font);font-size:15px;font-weight:500;color:var(--ink);pointer-events:none;
  background:var(--canvas);border:1px solid var(--hairline);border-radius:var(--pill);padding:8px 16px;box-shadow:var(--shadow);white-space:nowrap;max-width:calc(100% - 32px);overflow:hidden;text-overflow:ellipsis;
  animation:float 2.4s ease-in-out infinite}
@keyframes float{0%,100%{transform:translateY(0)}50%{transform:translateY(-5px)}}
/* 단계 카드 = card-feature (28px 모서리) 파스텔 변형: yellow / teal / rose */
.cards{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:16px;max-width:1100px;margin:0 auto;width:100%}
.card{position:relative;background:var(--canvas);border:1px solid var(--hairline-soft);border-radius:var(--radius-lg);padding:22px 24px;text-align:left;cursor:pointer;
  box-shadow:none;display:flex;flex-direction:column;gap:6px;color:var(--ink);transition:transform .15s,box-shadow .15s;min-height:128px;font-family:var(--font)}
.card.s1{background:var(--yellow-light)} .card.s2{background:var(--teal-light)} .card.s3{background:var(--rose-light)}
@media (hover:hover){.card:hover{transform:translateY(-2px);box-shadow:var(--shadow)}}
.card:focus-visible{outline:2px solid var(--brand-blue);outline-offset:3px}
.card .step{font-size:13px;font-weight:600;line-height:1.4;color:#fff;background:var(--ink);border-radius:var(--pill);padding:4px 10px;align-self:flex-start} /* badge */
.card h3{font-size:22px;font-weight:500;line-height:1.3;margin:4px 0 0}
.card p{margin:0;color:var(--slate);font-size:15px;line-height:1.5}
.card .badge{position:absolute;top:16px;right:16px;font-size:13px;font-weight:600;line-height:1.4;padding:4px 10px;border-radius:var(--pill);background:var(--canvas);color:var(--steel);border:1px solid var(--hairline-soft)}
.card .badge.done{background:var(--success);color:#fff;border-color:transparent}
.card .badge.best{background:var(--surface-yellow);color:var(--yellow-dark);border-color:transparent} /* badge-tag-yellow */

/* ---------- SVG 공통 ---------- */
svg.sheet text{font-family:var(--font);font-weight:500;fill:var(--ink);user-select:none;-webkit-user-select:none;pointer-events:none}
svg.sheet text.disp{font-weight:600}
svg.sheet text.hand{font-weight:500}
svg.sheet text.num{font-variant-numeric:tabular-nums;font-weight:600}
.pipe{cursor:pointer}
.pipe.dragging{cursor:grabbing}
.pipe .body{transition:filter .15s}
.pipe.lit .glow{opacity:1}
.pipe .glow{opacity:0;transition:opacity .15s}
.pipe.target .halo{opacity:1;animation:halo 1s ease-in-out infinite}
.pipe .halo{opacity:0;pointer-events:none}
.pipe .glow{pointer-events:none}
.song-row{padding-bottom:4px} .song-row .song-chips{flex-wrap:nowrap;gap:6px}
@media (orientation:landscape){ .phone .song-row .song-chip{font-size:12px;padding:4px 9px} }
@keyframes halo{0%,100%{stroke-opacity:.9;stroke-width:.35}50%{stroke-opacity:.35;stroke-width:.7}}
svg.sheet .slot,svg.sheet .tape,svg.sheet .ruler,svg.sheet .memo,svg.sheet .fnote,svg.sheet .tray{pointer-events:none}
.btn{pointer-events:auto}
.slot.hot rect{stroke:var(--brand-blue);stroke-dasharray:none;fill:rgba(66,98,255,.10)}
.slot.hot .hint{opacity:1}
.card-note{cursor:grab}
.card-note.dragging{cursor:grabbing}
.card-note.locked{cursor:default}
.tapzone{cursor:pointer}
.fade{transition:opacity .3s}
.arrow-bob{animation:bob .9s ease-in-out infinite}
@keyframes bob{0%,100%{transform:translateY(0)}50%{transform:translateY(-.35px)}}

/* ---------- 2단계 ---------- */
/* 초등 분수 표기: 가로줄 */
.frac{display:inline-flex;flex-direction:column;align-items:center;vertical-align:middle;line-height:1;font-variant-numeric:tabular-nums;font-weight:700;margin:0 3px;font-size:.8em}
.frac .fn{border-bottom:2px solid currentColor;padding:0 4px 2px}
.frac .fd{padding:2px 4px 0}
.ic .frac{font-size:13px;margin:0} .ic .frac .fn{border-bottom-width:1.5px}
.btn .frac{font-size:11px;margin-left:2px}

/* ---------- 3단계 ---------- */
/* 3단계 화면 = 안내 줄 · 팬플룻 책상(버튼 판·점수 판이 위에 떠 있음) · 음이름 띠. 세로로 넘치지 않아 화면을 내리지 않아도 음이름이 보임 */
.stage.s3 .desk-wrap{margin:0 12px}
.mode-float{position:absolute;top:12px;left:12px;z-index:3;display:grid;grid-template-columns:1fr 1fr;gap:8px;padding:10px;
  background:var(--canvas);border:1px solid var(--hairline-soft);border-radius:16px;box-shadow:var(--shadow)} /* card-base */
.mode-float.stack{grid-template-columns:1fr}
.mode-float .btn{justify-content:center;padding-left:14px;padding-right:14px}
.mode-float .btn.stop{grid-column:1 / -1}
.hud-float{position:absolute;top:12px;right:12px;z-index:3;display:flex;align-items:baseline;gap:10px;background:var(--canvas);border:1px solid var(--hairline-soft);border-radius:var(--pill);padding:8px 18px;box-shadow:var(--shadow);pointer-events:none;font-variant-numeric:tabular-nums}
.hud-float .score{font-family:var(--font);font-weight:500;font-size:22px;letter-spacing:-.5px}
.hud-float .prog{font-size:14px;color:var(--slate);font-weight:500}
.desk-wrap.lay-left .hud-float{top:auto;bottom:10px}
.melody{position:relative;display:flex;gap:6px 5px;padding:10px 12px;background:var(--canvas);border:1px solid var(--hairline-soft);border-radius:16px}
.melody.strip{flex:0 0 auto;flex-wrap:nowrap;align-items:center;overflow-x:auto;overflow-y:hidden;gap:5px;padding:7px 10px;margin:10px 12px 12px;border-radius:12px;scrollbar-width:none;-webkit-overflow-scrolling:touch}
.melody.strip::-webkit-scrollbar{display:none}
.melody.strip.center{justify-content:center}
.melody.strip.wrap{flex-wrap:wrap;justify-content:center;row-gap:0;overflow:hidden}
.melody.strip.wrap .mnote,.melody.strip.wrap .bar-sep{margin-top:3px;margin-bottom:3px}
.melody .row-break{display:none} .melody.strip.wrap .row-break{display:block;flex:1 0 100%;height:0}
.melody .bar-sep{width:2px;height:40px;background:var(--hairline);margin:0 4px;border-radius:2px;align-self:center;flex:0 0 auto}
.mnote{width:54px;height:54px;border-radius:50%;display:grid;place-items:center;font-family:var(--font);font-weight:600;font-size:22px;color:#fff;position:relative;border:3px solid transparent;transition:transform .15s,opacity .2s;flex:0 0 auto}
.mnote.long{width:70px;border-radius:27px}
.mnote.do2{font-size:15px}
.mnote.cur{border-color:var(--ink);transform:scale(1.18);box-shadow:0 0 0 4px rgba(5,0,56,.10)}
.mnote.done{opacity:.35}
.mnote.mi{color:var(--ink)}
.judge{position:absolute;left:0;top:0;pointer-events:none;font-family:var(--font);font-weight:600;font-size:26px;transform:translate(-50%,-50%);animation:judge .7s ease-out forwards;text-shadow:0 2px 0 rgba(255,255,255,.9),0 0 12px #fff;z-index:5}
@keyframes judge{0%{opacity:0;transform:translate(-50%,-30%) scale(.6)}25%{opacity:1;transform:translate(-50%,-60%) scale(1.15)}100%{opacity:0;transform:translate(-50%,-120%) scale(1)}}
.count{position:absolute;left:50%;top:38%;transform:translate(-50%,-50%);font-family:var(--font);font-weight:500;letter-spacing:-2px;font-size:120px;color:var(--ink);opacity:0;pointer-events:none;text-shadow:0 4px 0 #fff}
.count.go{animation:count .6s ease-out forwards}
@keyframes count{0%{opacity:0;transform:translate(-50%,-50%) scale(.5)}30%{opacity:1;transform:translate(-50%,-50%) scale(1.1)}100%{opacity:0;transform:translate(-50%,-50%) scale(1.3)}}
.song-chips{display:flex;gap:6px;flex-wrap:wrap}
/* 노래 고르기 = pill-tab / pill-tab-active */
.song-chip{border:1px solid var(--hairline);background:var(--canvas);border-radius:var(--pill);font-family:var(--font);font-weight:500;font-size:14px;line-height:1.3;padding:8px 14px;cursor:pointer;color:var(--steel)}
.song-chip.on{border-color:var(--ink);background:var(--ink);color:#fff}

#confetti{position:fixed;inset:0;pointer-events:none;z-index:50}
.desk-wrap{flex:1 1 auto;min-width:0;min-height:0;position:relative;display:flex}
.bar-btns{display:flex;gap:8px;align-items:center;flex-wrap:wrap}
.row-scroll{display:flex;gap:6px;overflow-x:auto;flex:0 0 auto;padding:2px 10px 8px;scrollbar-width:none;-webkit-overflow-scrolling:touch}
.row-scroll::-webkit-scrollbar{display:none}
.row-scroll>*{flex:0 0 auto}
/* 폰: 버튼 판·점수 판·음이름 띠를 작게 */
.phone .stage.s3 .desk-wrap{margin:0 8px}
.phone .mode-float{top:6px;left:6px;gap:6px;padding:6px;border-radius:14px}
.phone .mode-float .btn.sm{font-size:13px;padding:8px 10px}
.phone .hud-float{top:6px;right:6px;padding:5px 11px;gap:6px}
.phone .hud-float .score{font-size:17px} .phone .hud-float .prog{font-size:12px}
.phone .melody.strip{margin:8px 8px 8px}
.phone .melody.strip .mnote{width:46px;height:46px;font-size:21px} .phone .melody.strip .mnote.long{width:60px} .phone .melody.strip .mnote.do2{font-size:13px}
.phone .melody.strip .bar-sep{height:30px}
/* 원리 설명 그림 */
.fig-wrap{background:var(--surface);border:1px solid var(--hairline-soft);border-radius:16px;padding:10px 12px 4px}
svg.fig{width:100%;height:auto;display:block}
svg.fig text{font-family:var(--font);font-weight:600}
svg.fig text.disp{font-weight:500}
svg.fig text.hand{font-weight:600}
.dlg .rules{display:flex;flex-direction:column;gap:8px}
.dlg .rule{display:flex;align-items:center;gap:12px;background:var(--surface);border:1px solid var(--hairline-soft);border-radius:16px;padding:12px 16px;font-size:16px;line-height:1.5;color:var(--slate);text-align:left}
.dlg .rule b{color:var(--ink);font-weight:600}
.dlg .rule .ic{flex:0 0 40px;height:40px;border-radius:50%;display:grid;place-items:center;font-family:var(--font);font-weight:600;font-size:18px;color:#fff}
.dlg .who{font-family:var(--font);font-size:14px;font-weight:500;color:var(--steel);text-align:center}
.phone .dlg .rule{font-size:15px;padding:8px 10px;gap:10px}
.phone .dlg .rule .ic{flex-basis:34px;height:34px;font-size:16px}

/* ---------- 반응형 ---------- */
@media (max-width:900px){
  .brand .name{font-size:19px}
  .tab{font-size:15px;padding:8px 10px}
  .tab .label{display:none}
  .icon-btn .label{display:none}
}
@media (orientation:portrait){
  .stage-body{flex-direction:column}
  .stage-body .desk{flex:1 1 auto;min-height:46vh}
  .cards{grid-template-columns:1fr}
  .card{min-height:0}
  .home .hero{gap:6px}
  .home-flute .hint{font-size:17px}
}
/* ---------- 작은 폰 모드 (짧은 변 500px 미만) ---------- */
.phone .hdr{height:52px;padding:0 8px;gap:6px}
.phone .brand{padding:4px}
.phone .brand .logo{width:32px;height:32px}
.phone .brand .name{display:none}
.phone .tabs{margin:0 auto}
.phone .tab{font-size:13px;padding:4px 10px 4px 4px;gap:4px}
.phone .tab .num{width:24px;height:24px;font-size:12px}
.phone .tab .label{display:none}
.phone .icon-btn{width:36px;height:36px}
.phone .icon-btn.pill{width:36px;padding:0}
.phone .icon-btn .label{display:none}
.phone .stage-bar{padding:8px 12px;gap:6px 8px;min-height:0;margin:8px 8px 0;border-radius:16px}
.phone .stage-bar h2{font-size:12px;padding:3px 9px}
.phone .stage-bar .msg{font-size:14px;line-height:1.4;flex:1 1 100%}
.phone .btn.sm{font-size:14px;padding:8px 14px}
.phone .chip{font-size:13px;padding:5px 10px}
.phone .stage-body{flex-direction:column;gap:8px;padding:8px 8px 8px}
.phone .desk{flex:1 1 auto;min-height:0;border-radius:16px}
.phone .song-chip{font-size:13px;padding:6px 10px}
.phone .home{display:flex;flex-direction:column;gap:8px;padding:6px 10px 14px}
.phone .home h1{font-size:23px}
.phone .home .sub{font-size:14px;margin:0}
.phone .home-flute{flex:0 0 auto;height:46vh;min-height:280px}
.phone .home-flute .desk{min-height:0}
.phone .home-flute .hint{font-size:13px;top:8px;right:8px;bottom:auto;padding:5px 12px}
.phone .cards{grid-template-columns:1fr;gap:8px}
.phone .card{padding:14px 16px;min-height:0;gap:3px;border-radius:20px}
.phone .card h3{font-size:18px}
.phone .card p{font-size:13px}
.phone .card .badge{font-size:12px;top:10px;right:10px}
.phone dialog{max-width:96vw;border-radius:20px}
.phone .dlg{padding:16px 14px 14px;gap:10px}
.phone .dlg h2{font-size:21px}
.phone .dlg p{font-size:14px}
.phone .dlg p.lead,.phone .dlg ol.rules{font-size:14px}
.phone .dlg .score{font-size:50px}
.phone .stars{font-size:36px}
.phone .btn{font-size:15px;padding:11px 18px}
.phone .settings-grid{grid-template-columns:repeat(4,1fr);gap:6px}
.phone .settings-grid input{font-size:15px;padding:6px 4px}
.phone #toast{font-size:15px;padding:10px 14px;bottom:14px}
.phone .count{font-size:80px}
.phone .judge{font-size:20px}
/* 폰을 가로로 들었을 때: 세로 공간이 귀하니 안내 줄을 접음 */
@media (orientation:landscape){
  .phone .hdr{height:40px}
  .phone .stage.s3 .stage-bar{display:none}
  .phone .melody.strip{display:none}
  .phone .stage-bar .msg{display:none}
  .phone .home-flute{height:70vh}
}
/* ---------- 전자칠판·대형 화면 (1400px 이상): 멀리서도 읽히게 글자·버튼을 키움 ---------- */
@media (min-width:1400px) and (min-height:760px){
  :root{--header-h:70px}
  .brand .logo{width:44px;height:44px} .brand .name{font-size:24px}
  .tab{font-size:17px;padding:8px 18px 8px 8px} .tab .num{width:30px;height:30px;font-size:15px}
  .icon-btn{width:46px;height:46px;font-size:16px} .icon-btn.pill{padding:0 18px 0 14px} .icon-btn svg{width:24px;height:24px}
  .stage-bar{padding:14px 24px;gap:12px 16px;margin:12px 16px 0} .stage-bar h2{font-size:16px;padding:6px 14px} .stage-bar .msg{font-size:22px}
  .btn{font-size:21px;padding:15px 26px} .btn.sm{font-size:19px;padding:12px 20px} .btn.lg{font-size:25px}
  .chip{font-size:18px;padding:8px 14px}
  .song-chip{font-size:18px;padding:9px 15px}
  .home h1{font-size:clamp(34px,3.4vw,54px)} .home .sub{font-size:clamp(22px,1.8vw,30px)}
  .card{padding:20px 22px;min-height:150px} .card h3{font-size:26px} .card p{font-size:18px} .card .step{font-size:16px} .card .badge{font-size:16px}
  .home-flute .hint{font-size:24px}
  .mode-float{gap:10px;padding:12px} .hud-float{padding:10px 20px} .hud-float .score{font-size:30px} .hud-float .prog{font-size:19px}
  .mnote{width:66px;height:66px;font-size:27px} .mnote.long{width:86px;border-radius:33px} .mnote.do2{font-size:18px} .melody .bar-sep{height:48px}
  dialog{max-width:min(94vw,640px)} .dlg h2{font-size:34px} .dlg p{font-size:19px} .dlg .rule{font-size:20px} .dlg .rule .ic{flex-basis:46px;height:46px;font-size:22px} .dlg .who{font-size:22px} .dlg .score{font-size:76px}
  .settings-grid input{font-size:19px} .field{font-size:17px} .field select{font-size:17px}
  #toast{font-size:22px;padding:14px 26px}
  .judge{font-size:34px} .count{font-size:150px}
}
@media (prefers-reduced-motion:reduce){
  *{animation-duration:.01ms!important;animation-iteration-count:1!important;transition-duration:.01ms!important}
}
</style>
</head>
<body>
<div id="app">
  <header class="hdr">
    <button class="brand" id="brand" aria-label="홈으로">
      <img class="logo" alt="다시수학 교사 연구회 로고" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAKMAAACgCAYAAABg+NwuAACAx0lEQVR42u29d5xdV3Uv/l1rn3PLFDVLcsMdgxvVxqYEjOk9EBiFEAiBPCAxNQECoWQ8EHpJgAQSAgQCyQNNHpj6gGBsA6YYG4zBcsE2NrIl2bLKaNq995y91u+PXc+dkS0NJPDy+d1ksDSaueWctfde5VsIyzxUlTZNb+LpTdM2/P29H3vpvff0bz95rLv66L1ztx07sL2xktmIKhsyICISgIgMEQiqCiICFFAoAFLAkoKIRFUJxEykEKgSkZKq+zsRGaNqGRCAwBBiMCCqlL1LiAgRAUwGogC7F4OqKrFRhaqoVSZVIUChCst1YYq50dbojVy1f7J27fHff+mzprYBwOQkGJjE1NSU4CAfunnCkL9e/iLyFV//5PrxhasO1fmtq8BVm0kKUmarxFYqgsmfoQBsjfx71gKtstT0jRpWDBkmBQCL2v24ivsZY5pvygLKrFaECrg/A4CVigr3C1AWteKvq5AaQ6q2EgasilUBrPZlsXvI4btuPfMF2x989EMWAfdy6q8XreB6Lfeg4W9MbJ4wIQg3f/Xv737zbT991t7ebU+tpT4FXLVNYaBqfYABqu5pVBXM/jOJAgQYct9X90NwsckgAKrivpG9C1KCQkGg8MRwl4n862mIQ/dcKv7XGQqA3RPDavoekbrfJoCIwP5uKwRaMQBzO2txcYfW/vPkn338P4evwV0GoSoxkSqAf7lQO4/Y87zHduo7nqDVvrMM5FBSu1alahOAkhkKhRCBCVAREPnrAYABCARgTtdM/bUgAoH8Z2KoSrga7jKKvxbE8fsq/hq7//f3hUBE/jXDfVFACRJ/T/0vWKgqRNgaU84L8e2VllvRWn3xYOSoLx77lA/+CNClC/HXEYybN0+YTZum7b/+6wc33lL/4LyFet8fo6y6vaoHqS1ISEQFzEZVNfswFAMy/l3Vx47GFxEikLpXVXXXOf6sfw5/g92FVxuf20ewDyS/6+YXDhRj270PCt9278O/lroXVnWXnpmZWp0CVBtQ1f1Cmzb85V+f+4/XHkhAqk4y0ZQABW7d/LQ/advdrxor+ie1qIdKBFYUdSUQ8tdCASEoxSvir6D4d0thwabrqAowGKI2fpbw/fgpSWOwEfmAFHcYqQ9WIkBEQGT86SEgdu/E/ZumzQFKAIPA7v4xgyAoWVAwoTAldvXbatH94k7dMHnas//9Ct0MQ5tgfy3BGC7++z/56ofuqX758R5mju8t9EDEtSrYXRvyi8hfLn8Uq79A4WKk1YoYCSHoBAow+V2BQMRxx1NNfyb/M/G5EHZgv5KB+Lr+APabAGU3M+0wSPuIf59hByZVUgGEup02S9XeQ4P2n77t5dObw+Jc7sKFf7v6/FcfsWHws4+t5r2PrQc9LNYqAAkBrKTkF03IV+J781GXvTeK66b5PY4L3SVC/nNnP6v+JADULU4GmJE2BxAECva7ojut/LVSF8xQf49I3HOoC0BVAhmCQtwerVCQKlstxrol9lWdhV12wytOfO7n/1k3q6FNkMbHONhgnNRJnqIpedfHXvGIffLLL/bs7Eg90JoIxp2dbh8hQtjO3JHij4oQkPBHrKj4IxHp+yEw2O0AYl2gMadgTsEFiFgwE0QEzMYfyX6lhqPbv064IaoKY4y/CZqOs/j87jliSuG3Fw27r9i6KLkwaGGwl5733r/6yseX2yF1cpJpakp+8aWXn7x6/sovrTazx88sVLUyMfxTh0Xhdh2XaDAbd818MBEA8e9F80D1u7wqQMrZnfKfi31si79W/qSgsKmRuK887aEl6YUPf05PTwQRCwKD1O0lLugtKL4NH9gAKlHbMmza3RHcurD29Sc858tv/VWObJ6cnOQpmtJPfeldx8zWWzcvDPaO1H2xRFIQhMJhwgCY/K6jYYmkVexWokDi0eqXB7vgjTuUAhB3A4gQA6d5oRBzTw0XLttB3b+FS5UWgi9qfGAiFlEuINMu626+yyNdDqUgCLjgwlqVvg6EV9X//Odvf/IDpzdN28nJSR4OxKvPf/URqxau/PI4zxy/b7GuiKkgVYb/POJDS5T8MemunajGozh8GtE8F/ZhLOJ+j90pEQJIw2dElnb4jZeyV1al+DMpdUG8d8jzw7CYRV2uzT5XJ4WSO6bh81Ult+WIEowpTG2h/YV5e3h711t+/sknb6JN03bz5gmzomAEpsBk9IbtV3645rlDxEpNrIZCGKqCmeMFCZ9agLhLqaSf4yz5jrmdvxHMHHcEZLsgkXHHQfi7S+bATGC4PNMd2SktcMWSZoUTueeP+SPH44jZNHbv+P7E501EUPJBQcRqRalEwe3ev0xOnjsGTMEdTu6tX3bZZeXqfT/69BqePW52wdYAler/MbyXePT4/MH6oAufPV4nouY5FQKSuREk6rfTGNgirtjxBRqRwkLdkevzdMoCOG0Q2S6KLM0JvxsODNLsrSlEJQWyFUAV7HZpsmCSuq+r5Y5//On//uOjJiamRbMFfKCPYmoK8u5PvPhJM/amxyzM9ixzWUBtDA6OuWA4FtNR2dx9UnABMlTUKNgwxErKKTVmhwgHgiuwKctHEavkULVLzCNTwMWdJWZS4hLyvNpEvhOno91aBceboIBLC4ytpO6uKk6ar256+bv/Em/ZfKpb7TQ1ZbeftuXPDh1deOjuuX7NRVH4TMZtY1mwx/ek2rj5ogrWfMdLR6ALOk4piH9v+fVS8QHmAyhvSoQ6T5ecNnmxmWfQ6v9P/LHtC0F/8jH7HVbJFzwENeJPu3gveGC1Xj9q1y7O3jRFhOdv3ryFV7AzEvYu3PLSCj01RbE098xWbjoOEQsEZhOPYdcGsKna03Rspmo3VMe05EIhBGJY0dkNCz/vdj+K36JYZWv6nfjvKfcSkSzX1LiIYvWqLsFHCAAIV5XV2vRfdO7kxNimTdMWm6blwgv/pYP+zlcMeotqiBhWodbfSBVAfK4aFkt+PfNejCJ7j+l9UFh5xK4SCO+P89RF43FOIFhViN/Y3LFLyLMfynbqkPZAm7kks3H7KfndPL83SgBcFe5Pj7irhwWkIDPbG8ho0f/Da/7tuSdt2jRtD3Z35L/f/Nd3r6X/oLpviZRYIS6h93lDqGhVBca/OLLeoVsdeRWdVhcRxSM+PE84EtJqJrfqFCAVkFp/7GStmiz4XevMAPB/9r9rmNPza7rJQPN9hVzVvbdsdYe8y+dHAHFVV1qO0FFFd9eDwh533PYvPHicF+++ID7qGP4I05CQQlVCbQtmdrt5vkiyyAjXUUSGykoFq4LEd2Y1XDO/aOJqzFIegk87sr+DsoD390ZDF8MHQdZOCr0giiud4MpXm70336JrfhiySrKuK612fcsfA8BFuOjggnHfvpseRIUdF1FRFcqDAIKYU8WdSxWkiBeEsh0rBEIeEKHdoMPFiV+ZKfB0SQXjVncoYpo5X6yQw2Fjw1EYe0rZkanN3ZZCu4RSe4mGkn232qVoGS3L4uHhrZXUe+BIqwaUJHQMyWQ5HlLwIEtjiLJlFcrp+J4ITD6vFY1pDJrLN+bF6UBG1hkgQNlV2MpgYhCMG2BBY9pCSr6jQPF41nSxXfnj33vIJikeTC69UBXXnssWOhNBBTyoB9rRxcdMqvLDpy4+qKqau93R04hVw1WgPB6yC8bZSiLmJS2CeM9DkFF+81OAsuF4LRuVuabkfHinjaPFUAQ1KkSNzWPKdtDw+qmXmZ4b+cXNFlE+KQIBDCYVJSX6nbANFPXc74iI+4RDjfj8Bob3o5IKhjiNynaV+J78c6VjGoA/VYgIFDoCeRalWVAO5aoibkGJ36U5nk6pEOIw/dHUC6b8eBZ/f8TNh+KyJjetCR2V2BEl0ECUiOqTnvrxZx5NgLqR4QEG4x2z2+8pUFJiIk65HGVnJPstX8KOodIIAvF5CpNBYUpfvRYgMAyz/37hvg+G4RKGC5dTsdtVmCmuZibjPpyvzovCgDntaPBtJkbYUdgtEOK4whnueUVT0KbixeW26b9pB6LsyBYVcjlavREAqwor5DhryfWEoY0cN+VnYQfzzXvVeMPicZkdFRSqVQrtEx844hrQ7mTxv8eu38P+WhB8ZcsELji20oikcYy6jcD4gsi14sJ4IOxsCN0HsB8VCQwTTEGxCxAWHcdPmiJBSUmF0GbbbVe7DgOA6VMn6ICr6cGg1+GOxGYmyAWFteKayEiBSFnuFS6mMQaV9FH3e7BapVmxPwZMo3rTxuzUVepZbw0aU4OwU2ij80GNlUhhRk2hhVOgXZRx0uOaxmFXZd8DZf/aJpuvh2SeQg6ROgYQGMMFAMK2bW1mHrNqG6cHZfthKAr87pkKhTgGVd+vTQHMoTmfjeRC6qBhngcGYEF1BVtXELUQbkGLLhgKHvQg9cAt+qILNQXgG+zqW0xusxMQM6ymk0aH+pwqGV7A/4+wALUfDRL5z5cShrDDi6q0C3C7bcYAYOJgWjvkQDTuUvpxnsY8UV0vS6nRwglIBQVhfm4Ga0c34siNJ+OQNRvdB7UValvBSg0rNh5lId8RFVhb+0rbV9xiYSUdQ5pXvlm7KB/wc9wJAdEK+xb2Yue+rSjbLTD7oPI3nvJmhkrM/UNlG/LTPKcLx70oCgCY3f6lEUM8akWhykTkCxQr8eaJNvtzeaqR8uV0A0XEpXsePEExF3QRQVyAVaH9OfRhgDX3RHnY/dBefwpM9xBwZz2ICHVvD+p9t2Bw6/dR3X4Zyv7toNaoaxOJRUEMK2HASCnKsh1PU6kAZoL1OCtWA1hxY0F/v8LOL36LcG078k1yoFA7ctB9RoQGcrbzpXFaaoNwlru5Lr2g7g3w5LNeiN+5/1MxProOv+lHVfVxxbXfwuaL34tK+w41hDS94WxWHT+LZP00SXmbhj6aGqgbmhMVlpWUU1JPEagxPHILjWl1uVTKCfMWQZwPiy8I/fkgqVKmah6LaMMc8wSMnfg0dI44HVwsvc/t8IdTnonenpuwsOWTqK//LFroQU0XNVXu+K7dSJILVz5aWwcIlAdEEKwHUJRUwkJgLZqLN2/BxZl3nEQqgWCY2gcdjCraCMR8dYccyy2CdNyaAtg3u4g/OPtVOPsBvxdX8sFMx2l5BNuv9CjLNh5w2qNxy84b8PXL/wWjo+MROZTPfONOGDoE4gEBTNDaHfGU9TaVhHD66TTWMTKAaGwKa9bD8wEpKi7oPdoFsTJPRWBjQsWUFU+++PPVsV2cR73+dIyf8TKMHHlWVrhI4zM1G5mMztpj0XnIG7F47GMw9703wczegKI9hhoKFIyQKFmx7n4SuzzSGNi6drueug6G28bdpEdC94CGIB1ZgalQFK7wKgHgoqtuP/CckT0iVdTnd9r8kI1GMRSGDOYX5nHPI+6Hsx/we7BiXeHhK7Pf5MP6hvtxR5wC+jGnlgVR49hMQaCpa5BgP40eqMa7Aszt2sekyhGF1Jj5xiZJBIo4XIgPTG3Ol8MLhTFi7M6DQLZGr1KU934JNtz/f4FNxwdg2JnuokD1wdo98iyYx30Uey54OWj3FaDuGqhUvt2WgCXwp4O1LjhJPBSCNL5/9fjoZqIUPrdvzYWUCYrKykHPp9mK24NdIht7no05sIamLghkGLYWPPDUx6YRFBF+Gx7ki6/Rziq0zJif6aaxZQL6Nic0oZoMaVS+g4WaHccv0tjajhUiqxGckXbG8ByN3yUfmI1+IWLri4amIgqAbY1FaaH78Hdi3QNekgKRfLfgQJY8MUAGUIvW2GFY95gPYbDuvtDeXp//ufdbsIk7NwCo9ZW0ckC8pffMHsnj0TyiISUPuS7SAgNByRx8MCo4g3k2Qa6hHeIqO78mrKA0LRy+/vhmC+i36FHVA9i6ivmNAWWz8hzyRilYM9S6hAImyynOHtnAaB9ak2rdwAXG3TbNhCkbk8XdM+SMSFU1snaQO6UF82Iwds67sOqExwO+/XSXO+F+g9IAKii767D2ke/HYPwewGAeSgYiFiquGS6x2GcPWVMoScCVZ+geitNSjoAsSk1y/xmNm2EffDAGgGVsYObTj6GcgOPIiVGY1m9dEIYxZW8wD4tB7POJZhMIypvrzT/nTWOKx6hrq/UX+uSOICHQcKOYElwuQMIoz6UyNLvHIrJH5oT0xjCjqhUjD3oDxo45xwUim189ryYGVNAaOxRrz/lb1K31IOlHMEacxytBWaHskEyGTUwhOENrhfw3dg+s9ZO0tOg8omglweiH75pmomFem4/0Qi5kQKjrHm6944YlN/CAY8Y3eUXsr/fL52qzC3v8fSeItQ1AQkB65x2D4aM+YiBF4r/eglsyMLA2To5Gv1IT+sbl0pTaJqHNxKnPqKoQZlS9BZiTn4XVJz09C8S7yAvV+i85gIC0aK+7O7oPfiPqQe2GhH5xpP/z90Wl2T/VNKHSvNfsLogbN6rEHd5NjA5+O+c4eGnA9CmffjaArQKFKUtc8tMvxV7YwaLM3ejIIX5+nV+FKbG4OIcfXP1VlGXpTjmQx+CnPDgAOBzYIp8o+a6A5gArB5Fat3cdw/YdJdHPgWO+GJrx8ZhGgwvEAWASbrmk45moBA0WMDjk3lhz+sv8qOQACpSQF5JpTJ7u/Mi2GD3u0dB7PAO26rmJTJzrq79Ubmpm/SK2Iql3GtA7CeWRJl5h4iQRbHHQW3pBUAEx2GRzVM17ooljwn4VdNpdXHfr5bj4ss/i4Q94BqzUcEOKA3v0+z38fOuP0a8W/MxTh5oU2UiS0m1cbgYbG8Sq2De3C5de8zVsn7kBhlseC1lkIA/JdnOOAUmkkZ7gKA51dtEFIoK1a2rCiSdUdJmp/PzYxx01CrnUi21W1SGfYiJPcwBELRg1FtHC6rP+AqYc9bsc7/dM8XkSFnf9HPUdVwMQFOvuie6Gk5s/s9+GmmLV/c/FzNaLUMgMhAoH9Eidg3jNQUBhCt8vDa0xhRWBYQ+T0xxDmSCCvAKsdxF4Jcgbv1nVhwz2HyprIWB0ZBTnX/JBHLruaJx8wpmes2Lu9GgmEKqqwse+/Nf42U3farY3wurOmXyh7xaKAfa9PJFseKAOnaICS0BZtFEyAWQBYT/TbXYHKFa8kmEeKQNpuDxaMiDG6vE1BDyoFqCKwI8Ajoj8cA8V8x8jdCjIUyIlAh1cd5iphao3i+LkZ2P08AemHW+/gejaV3t/+Peor/s3FNUMiAnz1MXcPZ6FQ856BZiL/QdkzB8PR3mPp6P+yd+DR9YCWkE0jR8lXhcK0+8h+F+4NpQjg911NlAiRb2C1k4hqmQoZ+Ll8CSJA3rKQlQBGDCkHOBjX5nEi5/2Hhx7t1MaY6LljuawawwGPYCA8ZF1sFrFlSUSZqWSMLiaZr0c56bk29IOAsUOVhjJiKrWP1dChntIWIPANcynycG4RApjUkk93q/Jgfq4hqRpSrgx5NsfAfwa8scwfglo+TSBNFCpYMeOwrr7vOAudrQwp2fs+d47oNd8BO32aqA9DiWgU1tUP/swdvVnsP7sNw2dasvvjiOn/AFmrvscuN4DKkq3mRCDC0ZdW4TJnGbUE1C6R1C3Q7KfoWegAd8gP/jKi4VUVQLBI296a8qaPAeF4i4gsFAU3MZAF/HRL/w1du/ZnoCkdxb9RYFnPeY1WN09Egu9GRAcKEOEARI/zxY/r3aJsYqARD2jUB2HGLXjVatCxaKWGmotVGsoU6oAYTMWoWYo74DksRmu0PrPyQ7tHAIYBlgHGFMKqVoPIYpsvLRgUmss7OwQDSPySKJRJRgY1P1FtE58GsrRQ4ea88vniDNbNgPX/Sta3XV+Y7CA1FBitEbXANd/Bnuu+HCWQy7bjAVU0Ro9FMUJj4Ote/6zuHrB5YoaG90qOZ9GGnN2wya1qXIsKhG4MAdd2XIiwedgT42kJoBgDDfQNjEnEot22cGMvQ0f+txrsXffHS4g91PdhSp1w7oj8eLfeyfGWusxqBZ9e6FC4gc3Z+R5FZcHFWW4SErD0wiJ1wDGZnYNaU/YSpyYAPcyiUiVoYwIgREpNOhbsrYiSxrZUaEBHHq0kSwfWmGRIKax5RPBCPUi7MhRGDvpGXe+K/pAXNhxBQaXvRNl2fK5J2fYUcf5aXfHUV/xISzs+FE8ku+sp9E57glAMQJkx3LoAqgqalvHALSBPhLqFqYGqzHPV60qatGD3xmLIY5JU9UBy9BJE/qEmGC1QrsYwfa9P8eHP/tXmJvfGyFRywckQ8TiyI0n4MVPezdGzTr060WXbMS2B6VWci7H4REjac5MceHkwM+AG+Sc4pmxBpsgW47oobxVE7gn6qpJGnTrcPCNtgsQO3xarQxx+a5HCkjIax1fOj+t2EOAWAlaVSiOfxzKkY13siv6m2srzP3w3WjLHIRaECSkT4ScQSFkUKKP+R/9PVTs/gPcbzLt9afArj4JWi1GempYQMyc4zn89TR+tKkNLSViygoc96oF08HvjIFAFIoGQuKHBH5u6rBTFL2gDHUiYjEysga/3HMVPvQfr8HCwr5IoF/2RdlNAI487O74s6e/G6PlBlT1PApwaoX4iQR55QllB08Cp4BK3Gk01C3CKCuMORFHgQGypo31l3aFdLMCJlOEoMr18Xwon3ceqEb7SzODYm+lJa3utIoRIywEK2AI2XizKOyUvjZmEJSchpWQYtBahdG7P+nO2zEecLtww/8F3345tD0K+NSEhoDPbt5cg9pd6O2XYX77ZX4n2c/uqBZsSpRHPsQhd5B43aEP2+AR5ezC2KqCb3GlL0dtYBhayTHt70IsMDI+ctgdxL/JBEFHQ9AJBFgZYKQ7hht2/gT/dP7r0R8sDsmLLB+Qdzv0BJz7tHdgvLURPdtDaUp4ljEMl06QSHwjNjL7pNGIzRv0mrW/RHy+GObufmelSCzLisF8Pu9ZcOG4Nwya/9axs1NTJIc/65vn3nHHumP21p0zbp0v/nrOdn+xtmsMqRVVTxMwiQCaQ/EQugb1ArDx/mivu2e2Uy2zKxKjrnroX/VvKI0JIM9E5QU1p0ZMgDBK7WFw09cOKAA6hz8AajogseCckwVqAm8bp8lwbzl2pF1+rQqrKzimWaGOe2wbzd54rGRHXpyxhioS6hl6Tr1ObI1VI6tw3W2X4Z/PfwOqqp8dpfsPyKMOuwfOfeq7MFquRc/2YagAKafxEgTUAKtyVIZgTu/PWpuBHzhW6BqpEtTI61zOIw1eTLzQ7vghsZWaUjeMbLrlJf/yvyePfdP7nnX6+3prxk58/rd/dPRzv/fma3Dc6TvnO+/rlCUXqkJCaRohGpmBIfJJCfVA0Tn2UbEY3D/yhtC7+SJg95XQsg21td8JOVN3SIWzer4qmQL1jst8ccLL775+AZTrTwWNHAm1lWtvZSPTgGNt8GoaLbehTQkK0dq9oRUInLAQKODXwk1ywk4eRUIMtWnbzilQ5KmfIYcRYtRSY6wzip9t/RY+8cU3+SMAdxmQRx52d/zpk9+OFkYwkJ5rk8BDmvzMPRzPDQDC0Pw85+dQgLZ5nkyaioTiBFkuGhDMTTQPaUFChSlX2/des/uHW2aLPZd1R3Zf95d//7gL//rvnjLx0D/89z2H/tG3X7FzsOrPi06bVa1VyRXFMvAEMRQ91GNHoHu3s+9kV4SfHQO9G76AwtjsiERkTIYerTu1JGbaXLSBhW2odl+LJX2soRaPaY8D40eA1Do5Ew0dC7cgc+IVAjUicACcxpXvSDhhKvWB5BQzD/qYTmjdvDoPK0CsbfBwY34S+2XiJxjWj5TcsbpqdB0u+8UF+MzX353aHLjzgDzmyJPxJ49/E6hqodYqBmGutSMiQ9eXGu2knBba5E6T1wJKPcCsndk8TiNP2Os6KqGyVgZY7NboQ0sd5bY+XMeqza987yP/Vicn+ZjnfvPv9vTb7xnvGqMQG474ACkTx4iCVn0Uhz4A5ejGJgVzmV2xv/cGyM7LXcUbrnfGPVGxTV5SnJYxqL8P9czNGCp3l7wOASjWnQaR2uXKvhDLAz+yPpldoeTbbk6GJeSsEpUnoAQLPvhjGj63sgFoqkm6hJCDC/I8bWl+ltDBvgNW11g1uhrf2fJ5fPabHwQTZzIk+w/Ik44/A899/Hmo+7bRDkLG/UUWPMMXm0gT8AM5M1Di3DVvFeXom+bnSWpmSgKIsu8oQq3ooFfbxd6gHj2k/YpXjn/nPQTge+2Xvm7XoPPj0TYZF39N9Q1C7dRoj3hQxjbZ/7Sld8slMIO9ACdyVRqCOzA0MTXmI+FPhiwGd1y3DBp8mVcbOQx10I/0HYQwKVLJgchpgYU0JHVWuNH2M1hJNa0p8EB5DqDI/zcks835rjYgWImu4ISUrB1gpDuCr//oX/GVb3/CBeSdNMVDQN7nnr+DP3zEX6G/0Iey+vaLxvwwZEqhKOEAxYpAEs6KGk5Hd7aQYkJOtKStkrQmo6hYIJORL6KIWI1AzcJcr26PFa/4q3c99ombNm0aLNrOx8qi5bcdaoaBFdj2WrQOu++dB0no8916SUYh9ffF+M5CiEu/SeTaQwoCcRv1vhuH2nbLkz/M2OEganl+NbuxKyWBhfyaJggZNRTitCksvKIHN5vJLiAC9CkQvRtKWHF8lgeoNtQe2GfB6neb8dExfPH7/4ivf/eTzQrtTgLygfd9PJ7+sJeh6vVc09qYJnmPmgAFGp4EQDx3WJBTZMNRHZXUGmKj7BXRkJ0Aqf/oTgfxC8/VcSJKWkB7xv4lACyU7a/vXkDFxAVENSKpiCDSB606Hu1VR+0/SPxOPdi3DbL7ZzCtTpJg8VjIIJapGQhYMtm/IHPC/dshMrhLZFWx6mho2YFIHSqBuAByHctQM3AU//KDEXVVfDzRCbArqGCYmRIIQiRbhRkQgbLBP5L4UlgV+VSDh0Zl6i/U2NgIPnfJP+D7P/2qn+fexQ6pgnPOnMAJh90fC4O5WGgQ05KAdhzvHLktCbeYafzEoqShUpEa6JLJ7jnQR7PZHxdCKHocopbrqiIYecAfTp55t9uuOfNGUOv6tmEQkYaxGgGQaoDi0DNA/thdfmd073ew8wpQfxcUZSCXJjUKDSltSi04K8yCVrgs7IL09t7JduV3xnIEMJ0mRXlILUKRt/WkASMLcZPzKJhWckxnI8ugKJZPWobnjqFDn5rHzVwu9PdySoJLvA1a3Ta++O0Po9dbiESfOwMGAIozTn5M3JGSFk0TkU3DKhjIFMtMUw6lGYSaCYnmFXq+k1A+cs1SgXDMK6mFUoHu6pa55zlTUzWovKpdGihIE7UAEOqidfgZOJDDrHfbFWBrXaeCJcLOkKmWxcXFFNmN2XEBVD1If37/r+d/3JSj4M5acCZglS/adEyg0VEJ+SETeyEFink75OANEFiywz4UKWFsFbVcwgfOCO8c9WwQx265Hk7ILznA7JlgK8Hq7hiKwmQyvncej6XpgITB4IYAZv56NJzrZgEVkuyoMqaEnPhCmreGdGjen/QemXOBHDRaTWBSw4W2abwEQDWjEic6oFEIQCyks96W6+4pQ/vAEhCsSA3s+TmKouVZd03ktRdhixA2v21lbDoCGwORAWy9eKcwZwCg9hioswEaeEMYErmPkiyOrMXMGUWXmhIpcRq2gqY3ojZnZo8xxHnJmXVhZi2RU02N323Kr4WjpUC/XkSXR/CHj38diuIA+N3+Oa647qKkvBXQQ1HEVGIzL+wU8UJpLiyKRvAHZViJWuVNybjm5803Fj8NkqQdSSCwEld1BTX9OwBoGWFU1vfgCGxrYOTwudb4YdWdnwZAvbgX2Hs9UBhACKTGy7SgIRwVhQMoteISPt0BJdQO7pIEQsTQchQqdbMLqcMtvQSUSMtUk7B/0A9TgFcyDiT1Bg3kFcIynez8SMvh+oo8cPOqMOnwuN91Ik6V9mGkgz97+ttx5GEnNYThl3sEbN1Pf/4dXHXzdzDSHoVqHScrAajKATkSQLO+KmEv3JnLKudHlZu5a2M1C3JpkrS7N3qsyNA4cCL5AhUuWSF8u27be72qGgM60VYKKLE71hhSD0CrjhkloH3nwAig2nsjqJoHoYhCTfkOlOuT769StlAY7QP1/F2S2NwrF41uAiIySzKOTBj6+VrC+wXE/DKoazCvyIPDo+ApJaIN2Js2RYFiuNGQjHJIn5y4ZVKcdYLz0iO84MlvxvF3u59XtuU7CUTnbnDH7m349DfeAyo82yyAwL3AZ2q3+aqvQUwQP01IeS+xU+hyWtUUiVOJSJUkXEKSHlpGMVrDuCxHgatKURJJXz73vvf9ZO+tX37BvUh791+orLJ7QZBDX6Jce1xBB9BftPtuAukslEyjed/0zAluCFn2kNFG3RFuodXcAXCSnGgWcQbBUzSmPrk+e9DWTPN7V1GRSWPYFbV2xHplfTR1DB0O0CNk2CuU+W047EC5sGgDIe7lgEgJ/cUKz3/iJE4+/qy7pib4AFhYnMXHv/wm7B3sRsu0YIP/CQ3ZTAAwhhvsvCh/OVRopMo/7d45tyaqkzFlPjO+cIptDXe8B60dBtWtdln0Z7C7My/vAAAzu/Xc1a2KRUnI29E51l0BXn30AYQFYGdugnNhySTxwuQl18bMqA/DT+MAwgQZzB1QwQQqPEKp2UnRHByTq7BH8azAl1HQwXPzhvqMDI36hiGUPHk8IWQSaCIgZhqrcKjqDuoMc7MLeM6jXoP7nXyOk0G5i0AkYiwszuHDn30Dbtp1FUbabQRjuEQDbYggQIPMcAA/IGtz+GZ5AuRKhEotLYQQ20GuGRCKn5B/qhLVVmxtVbUmUN3qtou64lrn7QveMXXxTTd+4Xlnr+K5P963MBBmZpezMogEVLTQGjviLpvdAsDuugowRZz9BySE+NPLaTdqhPHlXYmoKKwEUoX09x5YJJgyLjrKxEQTOz/tmlH6r9HyysDQsjIrQUbm/ZcfFto8OTDcHNcsTWyoyTKBDWPvvj14xtkvwVn3eSJErIOo30Ug9noL+OfzX49rt1+KbmfUcZ6V3NhrqBUUoG5xYuKz6jCqouyThIAMrahwA9NcNWMZht8VBRlXw6syitJQq12azkjbdEeLotUtimrB/gy7Bo9/z+u/8dkrLvnXjWsWt34MslCKU2Wg6HVja9RmFczIoXc5nlMRcL0A40+YvLrNR3LIRoG5WpxoOhmYAakW77KAAQDurEm6P0gQutix8O+HG3rfSx29opjBCkQwCqZCA+oibLo0BE2KiT+l0jL3cwkFBzysa8+e3XjaQ16MRz3oWQd0NIdA/Mjn34hrtl+K8ZFVsFJ5EEZTNjFK20m6KamBThHckCnqeCCHP9LDyvbVNEX0i8c5ehaiqgnkKi0Kpf6c3WYH9Y2mVVSloV9obb99+Zcv/vTFF6N3zYX/tP7Q7f/+HyO69/j5vlgyZNzrWCgRjFiYkXUw3TX7j0VPL6jntsMu7gRzuezpysZEPKNoklIZ4otGSJmtewe2K41shA0iVUOCp0Qc7d6CdlC8Lxmbs5ltHHw0FirqYPPgIduKpksLZ6AC1zVw8HlklABjSszsuwNPfuAL8ISHPj8WI3cZiINF/PPnX4+rb/0exjouEMHswQrN6UlOeQDlKULeZkqza/IXJlm1SYYiygTawVHvJmnKkFJhYHv17MxueeQn3vbta5rvX822L/zR747s3PzWruw5Za5fWVMY0xSFMlCx4PHDwEX3LlmA9b5boQs7gW7HkdA8LTc2/EPlFgAMAdoV8bgUNR8VAqmrAwoE6q4LhoNR1i8OJiJgBM0UzefY4nGa6s2RWIGVWGQVLWMgOkAYFoSRm6iz6BVfwqdxm4AkgTvDUVgUBrv37cYj7/NMPOXhf+oD8U6OI19Q9Ac9fOTzf42rb/kuxrprUGsfoDKOJUMOI6IwJtM3jLqKGWXU5ypxB2wAJYZAvrkCb+aeEPz04q7IxINadx7b2nijKuiXn3/x4bqw44mo9z1w52ceedYaWjiVbA8LlsRQYRzBPVs0nocsnY3+JLnzto5KH6w1yHrJkDCPBjmOFZLWTYYDbsa4h6uBDCj2GekuyFAjCQmliZseG+3UtHFuHM6UKWuoeBWKg6eqFtZZj2cjH84uYlgN2dHsE+MwAnK5b4k9+3bjoSf/Lp752FdlgUj7yVLcxez3e/jI58/Dlq3fwWh3DSys1wKvY24SaQKco0SSydBwg91xd7SRcIedLm+CB3RRcwQIzwVuInuUiW+44dqS2Ax2fvrazevH5x5iezUqO8BiT1W4UOMkkxqWFKlXB6C16oCqWu3dkZ4jl4DOEEqAUw5zBZ0CS/ZbAVC6nmi9cEAVPJmW33Q0tpBCC1k1IEM8KII0c13WRh+aYIIXzsE3vZlUgnpq6CHpMrjBiOqhcMGDDVuBvXN7ceaJj8dznvS6pvLWneTMpITPfP09uPKXF2GsOw6rgyh5zNkkJM9Fguh9SieazXbiYX8UzpA2Gb0VTbXVvCmeA2zdUacwTOZTn7qyN/+9997NSP/+M3tm7b5eVS0MSEBMDOGQ2kQna0r9UBChverwAwqKwfYrwFr5WbRmGTqyMSuy0ZtrqpOS94BxBVf8zHJgO6PCQMlETUlkPKGQFkXPR58maK6mEWpDiYoTK9DaoUKk7nsQhHFHtNgMP8hhGA21LmkOuYQxJWbn9+LeRz0Iz3/KG7LR3J1MV3w+cunPvo4f3vBVrBlfA2trMJfZKBLIOdTRFsXkZcpS38KCihh87D9H2qGTWkXKP6UBsI1hHapU39BVKAOwe7Z+a8OI7XfFZUQm5KhBpNRKJg8XGIgsICpgxu92QEGB/kxj84zvJ6PQRjMmauC7G71SkDebR32A25JJ0ogqIDbNkWAcNGr2MTx+gTxVNpODWVHOCJAQU5ps+IBmww1XTlht6DkbYzC3MIMTNtwXL3zq34C5tWQnu7PHTbdei9n5GVR1jVpqGDDYOMg8U/OIDSNC8mR8kSSxy7l0GwnKso3CtD0yWhtiABgSDW1oJkeXheCclRkN+XxErYhAYIhjsyN04wMJK6Q4OfhUTQlujd/lLN49Ww1GgcxkCyEBy0lYHAKDNBYOgE2G5p4uq1LdlXCKf3kDjXhjE9t7IWV1bZ9kUMpIxU0+UQv+M1ZWkDOSBkUdqGQ3Lw3CE8YkgSsNFgcLWD96JF709Lei1RrLHFfvev4IAE962HNxwt1OwaDugU3h+4PcAG7mkxFksn05UT8Ekqhg5+5f4rtXfQk757ejZUymvCqp+MrfI2U3OooBUNa3dFMktW6bK8c3CGa2gWzt4WESHWyWSCVH9TRFrSVQdO6i10eQug8s3g4Y9mT/eBJDwhw4+x2OPPGQzyXBzri7e0Ic7mKToKIFDadTloRqmE9HVqB3y4rUDY7UhAgzg0JWMJ0uggiZZpOKoKYagAPk2R/hplmqQdbgjx//BoyPHnKXvcTlcqOR7iqcfuoj8et+nHna4/B3m1+GO+a2oijKJfhGkZQGNI/DTA0t5mcSbqwCwACjKIM6cFSpSAn/UuF5chhBboHL0buKRUhvD2R+m7OTGALL5EoeUIAMJ2BC7vGrCRzLYBg5sKCgcgRadABd9GPThEswHuyMDBkfbYcz59t8PMzFCsC1YlUcrJ/TruPm+8nEMlSd5FbAwuI87nf3s3H80fc7yEBsVtQrU6iV5b9UUNcDjI+tw++c9hRUg0W/mmUIFMspywpokyD7QEHWzo/dgp524BgXrC6vEl+kcDRsCkj5AEZlzypUEZBpoWiN3UnO6AES9QCQCgacwKm0XDeKombiEtpuTFvYwf/rQcbN1v1X060xwHShqJ1pVIDnIRnXh9cJpNgwn0aGF40kLeGV5IxRSQ65XDKQdsm4Kj36RS3h3nd/6IoklBsI7ZUoSt55swyqinWrD4fhVszndJmKGVn/LL/dHGJMUi9PggZu3SPy1FwKWoyU9dpCMz2iocn5/7U6oGAkRPtfnvXsLdC6BxQmyqPk4z7yfi1APjJORWNE2zBBYcFcQO0CpO45asGd3Q8uY38XQbRBUlqTu4CFVhMvmbqkfEqwAqR3URhNgFI0oUN5CyQiZQTtso1DVh++xNP5N/7wR1a71UFhWlBY5CKhzmwzGFnK0CTe4S/jlMNXxD4oLQBUdY9CfsbgZDAZrkymhY5oT8wwxbg7evfLX3YA3MGOH4F1AcqmwcxL/UVkpuU5fTTtmGzYm1ECBEFtF50S734l8vwCZQP4EWSupRm1JjPcJ2U1RcglRGzSUFaAdWVUVWnAYJCjXDKbWu+k7LSiBFXdz3z9frsela1Q2RpBKjmw/GIelOU5TZ8YiQl5juEMhG8tOhp2PclbHkqNfDEGEDGIARnsi4hviM2E4X0+xyX6czthf/EFFEXXI8Sbx36y520CROLx6LUgg+OZy2lLoL8P0p9NIlA69PperUxtH1TNAijBzqwkn+4nSF6WNxJ5VSRy9bX7A60YRsaxS5FZyDaJS5nSKzm7XmtrXH3TD/2ExP72RKEPqN5gETUqr5CW9UsbdpbUoFhE+JyDivv4ipLK4oAibN2fvaZNxEraiOHU3BKZarBpw8zfgn1X/qu7VlxkwvAG1lZY2HYp5i54GYr5WyBUwORo64wAhQxR05hmxbGSX0FRa7KFVrUPe3/wXvRntzVeN35x4ST3rt4M078NxCZiRnPQRPCfJmqKTxl1fOfYdhQip1anB31OF+JwSrE5kQRBfflOKeMiWFix6HQ7uORnn8fpJz0KRx5693RE6W92nwyg4O07fxGVynN4VVxwGYI9AYo5AjIaksd+3wAAU6yuCGwZxJq7QnFSHUuFrXs+C0VZlhj85IPYue0SFOtOAnPLo50GkD0/A+3aggIWKB1HOnma0xLiGqEJ+Rs2QArHtSsuKhRlG9j6Zey67QcoNzwAxfjdAGM83XUAlQHsrqtAu69C0ep6G2RqCDvE180mY/kIUgKmNBzxDg87OOhgJKDvxj9D/bYMt0WNY81pXQ9sH3//2Vfh9x72Etz3Hg9ziqq/6fRRgSuv+w4uueo/0Gl3fQLeDK6m5EgSLwXQEJiPeuIAxBtpd8fWLmCn9glauuFDwnYyGGI1Ju/k+34EhTWEFjN092XAzu+CFM65VICWaYGKLqzmamEUhfSDlnbIYYe1zoEkCB+mIUGihv3RbIouRuxe6C1f8j7cHk/km5dF0QFaxRBqq/lulJAZ3+fuDrnAfsrCDfHCQQdjpxybtVgEpA9w4eHu2rhRxM0LJaIoDGOx3otPfH0KX7v0OBx/+GlYNXaIo5Ry8lViyt0FmhoYmtsIOzPcBEkL3X7N9JEaLldJcVaI0B/M4+YdP8Mv77gGCkFRlFm6gQy3qJmMcpMV2dRSzCCUhgYAMNMam1tFOmtAY7UkEX7y04hmLZesf4ONMEzHtU/85AgSjlzrcz9OAgdMcSeSzIe70XnU4Xl6arZD/KKAV/ZACRQtGOPQPw5MYuD5I6BgDRf7y5w+BofBgvrpk298R+kb8twmAmCoFoKtsQ8AHn7qRj3wnbHo7KSalsjNNYns2vjgIg7dUhQljCmwc+4mbNvyc7cTMZrHxhKnVk2oHuJYCLjyyE8/rA2ZssfJOe5Lzv5wF1TcjuTzpHbRclW0mqa5UGMyFHYGjRedsiBNiB8fxIYB4n0AsHj6CxdXX/tvs0x0uIojA5FJ0wi3Zh38Durer1I2nYmTCjS9rTXtVmleLqnvKVnumClaUFrz0cclLyrTMRu+Y90viJ+7e/ym+n5WQ7WCgp65R8ojuB+kMWnYXDie4ApVobomsFncBwDTB7Mzzs7e8QspawDEKn5FLqsGq5mECUVlfPY+gu2i4/pT8Gpj1CQLOZSwX7KZbku0N0u9de9pF8ZbkkzLKXN6Dbk6E6x6xQVJ6JyUH6bFlAN0Y29wKCAij1gjDAeG+AoAOA2odsjgDi71Hm5eLRFxnoQzJV4jJ6wgDeh+mgAhM7fM7X4pwOejnEw8mrNKXfMJX0NaL01I4F0f1ANdRDjbUcmDYgK1V5viBJoXhUmbk0LljBw1FE471oKFFmpT7eivvR0AJq465YB3RiYprpKae8ZQ1OIIOMJE9WwiXXLTmtCjs1JBbIVaalh1VhjBz8/aGrWtva2G7/CrwIqFhaCGA0uIrQE/ZbHh5yGo1RVOtVhUtkYt1j2f1q6FowqyEslj1HA9zefPPscKoNysUszn3Mn5VIgsQav68gB/V6s3FcZ4F1uOFXXeoObMCJyY/YSH4tHb8AMjSr7YeeAxo/aa5TxEuwuqvUsDMVPf9YtZ/D0M+M/YBqKMwotm8ROEuwKULE2t0OzPKjf0vRWq7ZIAFNctnPjyGwkATU0deDC+9eWfuYqUf8olqyOg+ZmqV32FZiQnMjG5Vs1lReBbAoGPollHNMHjyZ8r4WeSLUW6eZKKtgYLTX2eyMRLBJusCGzo4yHpMca2FKdsPMixpIbuUDUeVCNUlZlNb75eUDWXhFfs69gPhApSlsZQoCHIToiiV5pRIEIOHW+/34EIDHBA3kg8UYogFgDrr4xTinUBp161QhtqEhH9jozFF/S/kUa87uesZ+SlkllzVEre/G5unjEeWX1/0ds1FVygr+U3zznnnFo2TxgcRNeRiUhLW0wXxpAqa9ifwy7IlJwNQrLapHg2UdYJJ4isBxmOdslACMMUBGoY3qQ5ssbnS301bXisJHH45rQlxw/krxPdTrMAjbmiT4BIVdptA1vLhe9/7Td++c0Lzy4AYJdZ95XdC+gXhtj1osVV0eJ0aBzAlb1ZkV88yCwYIolKo2x1bL6HANKkcjbMCVfPUUkLlzIngnye5J0ooFDDvjGd4SyJIrmLchmbsC1IKvzy3xlGPQk5W2AwlIzlPf2WzOphHwMATJxyUL0+56LBh3x8MFvfbowaFZZo8+rXqZB3PMgsGRJ/GktUvtIOlKroKLubtQ6SYWVzFQ4HZex56pJhUeOI4mXQIzGHzBaKZI4J+a6YgwmYCVVPUc/W7wSAD+7cqJs3T5jT/2j6+gXtfmpVt2QhWGYTTSoR1Rw8GSqwvrMWkGaNd/WC+FiCtxx679m1jO63SM3mcN2ClZqhTFPRO3jxcJoS1YjTGNPliqnwlJyvkwdqCNAw7XEqVHb1aJvnB61/P+1501dsnpgwRFMH1fjmzZsn+G0v/5edRla/ouQ2ga1AHbHfEdATpKppGM5RACn1JpuVdz7myft4DdUCzYOSh6SNkeEQm+AGZ6uhWQN7qdxz/rx5kztv7SBzTQh62ACqbrdlBjPykQ9OfftbE5snzPSmaXvVVdOqCrpdNr7htrn29pGSCxWxHM7e0NvLLSo8HcBZUjgvGFJ2f4cBsoMy8Vn8KRPeP2djuRj3bgd279f9N1cQdv8WVkAymEJotak2WumpBUaNzkm85+xBz2EBkACs4Xu2W6K4fc5smy+O/EtV0FWnnHLQExACgM2bJ8ymTdP2tf/w1HcXo/1Xzs/1a4ANkVBzqJKqwmbPDo3drKHDw17FPrPCHDZZbPb6hi8QRxeCRo4WCpOg/ZJrzWTKZHk/rrkDYkjPO/Y1q063KOdm6h/PbR87+6iR+81PnTcVNzSdnGSampKrP/KYcw7rznytoH45qMiSURNlBHkoGBUNgCsNQa9VFGSac/PhoipVrL4Nh+RNGJytFDbrkXKjyBS1DVS2BG2hOHsLaHmOollpN0wVftJ4r0GmgNRi220yA9tZ3DE47LGnPv/z3w7X6OCBEgA2bZqWic0T5h0v/sKrqr2t9490yoKNkrWoXf5Pjd6bNo621P9qwp0oajPmFaxmLZCmLniu050qeNVlRnqhuZBYnFn7iYNrZEavzfPgJhvQkZYAcQNm2+kW5fxMdeWuHfYpH3vXF2aBqXykDZqaEt08YU7+X1+/cNtgdFNlW4tjLTGwUmtDQZ8Sv1ldm4cjkkfjaRF3vpwPnu2CeSAmnaC0sDXsZlEqkJcwJl3ORw2dnrhLZrpDiGbtvhKXUMwmKRUEGUg2ApV6fLQ0lR2Zv3Uw/oxTn//5b+vmCbOSQBxG1xEmQZiCvPztj32RGdG3tUexdtCrIc7ClBRMpBrGuH5K4gEInmdr2MBKtsIDScmvOMm3hdBa8El5OE6pMQNNVhqRBx19nt2UgdEc9TkUtETkSa6oFnNVgpKKCowCZNptIghjYdb++9Zf6MvO/4cLdk1OTvLUfi6sbp4wtGnaXvmRxz7oiPbefz5kVE6dn6/Qr2Gd3zp5z6GGD5yrhtkz+VxXH7Hh6n5L8/ybhnYvDwGgZKUs+x/DavJJFFhdIs6ackLylbfGa5gvEPLft6HLLdwqDXdbBe5YaP9062D1C874k6/8IFyTXwEB2HxMKniKIC9981NPaI0t/qWY+g/aXTPORKgEgEdVk3d4DvJoNCRiHne0DM1CviAiDv7WAQIlPoCarqTQzMJ4GTkNDcSQLBCDfmRuy0YZFD/Y0oIEbAyMIdSLimqgl9Tzg3d94A0XfR4AJifBU1N3jhANF//8jzx//AHtm/6yTf0Xre30NxAJBrXAauHyN685rpy1nIZ3a8+0c4vNRsnqOJMODUjWdO0iW4pSMIecMYwiiZ1HT85/J44ToIDez7volCl5s9cbMobBJDDMmBsUmOvjugrlP27eeeyHX/3qT83/qoG4X9xxSNgB4Nw3P+EYUyw8iVv86Fr1lIJ5LbGOWCstPwcldyRyPLPJ/4Oqe/NBzYtYG6T8rBILvguN/mBUUnDbB6lmQ+RsXqleBJGje1RiBBpmVb/eiVjUCQMtqNi9YrG9LIrv1Av4ygde/42LXRBOcp4j3jVqbZJD1Xjhvzz3sLvTL57CBuewXbxPoTKuRF0COkpcgNiIqmHmIZ1PyirYMO9OkH/SUNQYP37TyMEh/zvJ+SvIjEg21yePvKasCPG/16iRAesRdExUi9iKWHpisWhB82LGrpfafm+xan3/q72nfPvlL395P8+jfw3Y6OUfk5OTvOXULTSdRfvEKWiteuwDx+xIOTq/MNcurFJRlFQb1n4fMGTZmpKAAQwZ5rrSyrAaQwq0YG3fv14LYntOBce4bF9sQe1xAAOgBUBs6XGtVtiQDgYDMAy32kmCmQ2pWCWCZf+0kEUhNqzW/07HkNam1nphoKOtESFT2nbbznW3bJ392+lbFve3CA8SRkmYnuC0MxBO/6cflp+oPtbm8dl2we1uWVRFbWxRVLaoaWDabAieL1aiBbJCaljLbikQVmAANaW0hHVQCbVK1oFlJl4kssRgocFgAGKnP6pSa6vo6KAWAgaorFKrBLRoOzKZ1FqqkzamylJZGkXR0UHdo9oucGWFilpEyIjWpRguqwHbakZ48ZbFu/V/vPUB/amp3x80Tr/NEwYT00L068FY75+RoUrYtIlpevjmJDNxB8UfEIACP9nRQsGEVRvdzxvvGHHzzw0Wb2WMH63AnvQ0xhBuu42xahVgraJ7hKA4vsZ9YJd07X+yo0B7L2PVKosjjqiH/r1p/hJoxUl7qC6LlkjmzoBlrON0YsKcd8q03tXRvL/HxObNZvPEhNB+LScIUOFTplGsAszCzT/hhbltRnpu0dneHK0JH6K7QLa/4BbjoEf7AKzCKnBroACwbx+wD8Ca1ohSa8S/3l4AwL7OqK7FWqz1z7XHX/P1nTG9ozdHyP5tZqFS0xmomV+tRXet7hzboNsxEOBYwXmoQSzLDVAIwDM2bzanXHWVTv0adsQ7DUadmDAhCL//5v913GG9bY8Qqh5iFhZPY1OMEps2iAp1aQ4DKAG01Q0yrWfHMYhJ1DKcBoj645qyAQml2CFhQi2qligLCHf0FgTDArXsiinRUAYKlIhIrIBIahCDWVmS7EOlqlbFWlZYC7Eg7ZmqmhuUo1fWqt+5SdZf9Jh3fXrb8Gc/kIcvciLJ8HFT730Ij3QfVlX1g9TSBjI6YphbBlQSUUth26QoGDC1KAcRYrKhMw0vvCVhvoRgM6GulwUGSJ0cta8mXYFBsThU9eAS1xL0xDdRUedC4JTRQgLA5FIZMhBRsuzgPZWy6anqoFaZr62dYcX1hTHfNfN7vvWVt7zx5rAIpzdtsv8lwagTMDQNe+nH3nzUxl9e9rpiYeYP15YyDlXAApUfRUVCvGjUOQzEbYfvo6iiRdm4i2MMeVh/LGI0mz8H7KLGzqZ4oi7lI78A+ZPQM0uioQ1UjjYBs25n9/wUUszWZtcidT57k+2+45HvPv8GnwPpXc1VJyY2m+npTZYA/N67P/QHcwP9C2v4jKI94iWQ3cZivQRyGOdBJCJmItAiV4UNQwIQRG2iMVj1DrFeti7v02hyAYtOFH44QJwXmI0q2b1P36kISKOAWiIAatzzsLrWEKmiXpybYcUXRmXwns/99St/EgfxKzAi2m8whl3hqvMmnnNIte/dq3Rx43xvgFphVRVkooBLQ1gpdqkyT+rcniGv0eCDODSqXS/St/Elc0HwXjTkN4bGkMxTKP0YTmVIpMTPZImZoX7oTMjfs2v4GWJVtVQaY0ZaBfbVtOcO4def+u4LP6STYExFNZFlAnHCTE9P299/5ztPmNXRf9Cy89hKFHbQVxDZsHeT/0DuMwviRD012Ycwo0ngCQ1fFYoomzA3FtUlQhGNLpKmQM3dzMLYMGl0ewU2zXy9HbMiiSS73qWKFWJjTNFuw/YX+52q9+Yvv+HP3+L7UfSrBGT8KBdOnl2cM3VxfePbnvWadfM73q4LixhIXddFyxhxkxhmB3zVzCUrh81SZlQENElduR1aDGLNxlPI6Q6eu+t31xBEUb1AEy8nqnJxFo6UT4so88d20yDrgavscZSiUFKxLeaiXbawXc177/GOC1+pk3+97A4Z+o9Pn/rbs+Zb3fNtu3NY1Zu37qO4QV4wmYSHlCXP5pxsnQItwvIyrxrJHBiSoylFcIVhj4AKihSiScEt1y1vNME9npS5YV7etN9LdiYOMM1x9Or7nkqqVoiLTncEdnb3/zni+iue/Yljjx1g6rzcg+GgHgYANk9MmCd98Cv2urc+59xDF7f/bW9u3vaJAeN0JoIhelxF2dFLtFziSUO4wkxiLevKRDiTbxcGAXkKYuWZuxZyLcIMEpUDI1SxZOSH1PoG5zYcyOwkADKGuRJRayt7WLd4yB+eftwRG97+8S/qxISZ2rJFhwPxOW/9wD32tMoL6sJslH6/Bpsi6HEhh5QBS/g3Yc4fph4cDaBoyKGKmhreQAMWpjkwV1xwJtoAZXo/GJ6NpusUNCQzI6qkVpveX8MzMmZTqraqarNqzWmznfFTbjjvdZu3bNnCW7ZsWRlVdfPEhNk0PW2vfftLzly1b8f7FubmRY3hIorPNyXEhRGnGzxkCLnEO8Y3bBVOkSCfqOT6NF73LZG/go6LzTS9w0gr66UNm0xShhRPO21iLYrPgZaMnijyO0gMm5mFXnVUd/DCn/z5Q19B09N288SEyU+SycnJ1h7Vf5Wyu14HtlZC4ZugHqSQAByaAVIp56jk7z4TUAh0A/Y6lTlLMf1Xh841t4qtlzxJDEjJZtrByD4zVQrvc4hlmCB4zW1GMnSLiMKlwloO5mcrs3b97z1x6l2vmJ6ethObN/OKjunJSfDDH6589Ncf97319d4zFurCMsNYtVHpKzHDmnZumRJxJCZR0HhuABHyGWsyYgy+MuEYCUdOFHoPSGxKs1ga8jQOCJ6UIujQjJxB4mkJ4Y1k4vRJkcFTwgiwqtpllj4Zu1XHz3rgu79yhUxO8qZTT6XpTZvsxNs/9Kq59si7er3F2llLZb4zw8jtIR7QMMNoODDdCFHijF1FsslIBlCJebg20pZhKJxkO3QDEpEhWhRhV801FpdqbS4BwwQuDEGYGBj0Fzozg9O+8p5X/xKTk4SDbPvw1BTkyG/9/u9u4MEZ87VaZWsEQ2JC4XjxO1qci0qyYgjBKTbtROy2hXjk5lhI67F0wZfaBs53GO9l0hrxvQStSKaUHoRiZhk8ZZyZxzvpV31+TLpy101rfIQYEPUVWNOi1iqZP08BTJ+6haY3bbLPnfzbNfukflW/7imRMsh6tYoEyw+vOay4IRkYU7M/R9RQQPAQD7mTaYSmERJRKgIdwlHP3FgADX3KBk+nmUdyHmSZXR8xL/HKUTTzc+/5wwSSYvWqsYVRvASATpx66gqMLEEoF+54IduBukot7U7wjlQRPSKJT5HORc0urGeKKdyRkPkIQrXhE81evF6ijUfmVxUK7EBIylArHN5jVgzEVQo0igBkiGfkjLq8xeKn7MHmzW1IDBXlud5AR6V69Ldf+JCjN/npyh0tfpS2u4dqbQWqnEzVE7QOeUcATbfaAAzJYWzB4kIzwftwlIZCw9o6+rwMk+mDx5+IpKM/qIEpeRROJtifAXUx5D+YiG7cQMiLphZeolMg1gKiwjqolYzZ9OhXPnvU9x4PKiD5sr976dFG6jN7AyF3DYrY/zNsEu2UcrRxGqxryOM08XzZCyNhSNEhui8xN1ZWrq8dV2j0fKGmrEZufxx2Zf9eGtrj2YoWfwVZBGRrkDgLNgk4A04AVVg4pBEp1aqyuksjG7r1g+LuRuXDYEoFc56OehWFlK9FjxlNir+hwo5Hsic65X3FXCI6BGYULg3IJ7FpJw1UjuAEMeQA0QA5B5yA73uG95iLTFGge8QcTBuFkNtYJFJXA1qcAbaiMGX36ArHnebbXweVO/LYnpvv3yWsqRo9B0T9vZyzIlnRkPfIgj8IR+UBL6VLCuVkf9nUEgy8GCzJ9XKgrOQSc4GPzCmX9RCKzCU+HOXcsL8FAcIMCUQzyugJFBYQfBM4BDdrAUJRtB8ZwJ+WcG8VS+S1lineaONzKN/op9RLdKoQFCFznOwWEsA1O2IDRVWD4JN/f5oBdQ0ZGCYYQy7f06Z1sUZzRGoYUCK3Yc525uEWTxL+4qEqP8A0NdafHFiPIsKtNorumhMA4PZTTjm4nXFkdPwerYLgN4pmzRaKjlpAWf6T+wznPnHqLG8jqT6seGO4WWnn3snIK7cEfg1C9gSKqz5MUzzM2x1fYcEEObtMno6GepHOnNNkpyTFajeIt8PfUM9xZqvAwOJMAPjol750WKcw96kHA0CUc8nhJZo4FEwv0ejRYVi5LeM+a74rhnTGGOTgZmfcSZgfVNg9v4A984uY6fVQq8D4nw3Hcs57Dl7def6qYXempbZvMcUZ8tsJC4kzjaIUyKpkCrCho1dSTRd2ds8JHBJuDKkVINnruoDQOHFhbz8bpjHGGBdATHFnzLkrnsuGpm4Ihv4ejhfjmIWChm2YmypofD4XeyY2KU1NoMJ45Lb4hm2mNhZQ56GlFxrOlJP8w2SHQOSwmy1QFwC+tuXmjTVoDXluUJ6nSnQ34JTLRnyEJDHR7Fpn/Ixkwr5MbhvE3I1hzMzPYbQgnH7koThi7SowG8wu9nDd9juwdWYOnU4HJTPq6EKQDEhjgRO6FV6Lh4YkU8JnSNhIahC/hpHzOW9JCahJN6woGLG4MKosjaMxSuOG6QhHmRs/G/XjO68o4UZJGpzcvLGQNmQ3hll4OaPNBaBmJkHSOIbDTmeiMppzZWBmoK5hFxadcEBRwvScyG+7aEPLMjkiBrOiDEPoDDZ5SZ6tmcK6iIIMCgKwd34edWc0jC6JsoLEGPYLoLkDhiY7oamKFh1Ls2vCmQmTIk1WlAESxfzCPJ52rxPxrIedhWM2bmy8530L8/jmlVfjY9++HLsHFp2CYSExkKnROE/wFEVKGcThP2PVT0MtKc4mMfCi91FwPnYuBATbWlEwEqRkJqilTE5NG+M+zvp8nAuJNhwJkvpE1GpRLwonBLABkTRHd026T9bySAl5oMuyJ2bBW2MwA7Y/j35rFcoHPQYj97g/yvH10HqAxW0/x+IPvoLO7m1Aq5XJrGjcKcQDfxO3x0+CuNkf9UUIBxwmKSWxL4eXSRYUvjWV70b5ERw9C0mzUyPNiTTvDmgc5qAgxtziAl72mLPwzIc8OKtw03tfNTKKpz7wDJx29N3w6n/7HHbXgsLPnzkEWN6Az+bfYeQXeC8R+TvUoF9KA0nuBuSlbRyFdWWz6UKISGD9to0odqnZJCTADwwlT7mUe9GS3aQxt5bm6K4xns0b2PEIoOjAZKEZdUChzBBYFFSimp9DdY8HY+Mz/xyjh53Y+FCr7/MILJ75ZNzxgT9DufdWaNEaGstJnOGCALIJLaOZYIFTA2NA3Ja9ZrTEXutsfkIhovkUKTbxgQZ8I/uMMfBi01384qNEBQgNZyYYMti3MIfHn3wMnvmQB0cwCRO5vmg2k6mtxd2POAwvf9zZeP1n/xNlt4vAgU/KHE0edE7ESnRWWjK3ziXwwvPRcOveyziDuV5JMLIT96dluMwNgQW3Ahv9MWkQ7t2qa+pfSLC1MmgIssefzW9VZvmk7MySmZycHIvCethUgQLV3G5U9z4bR537HowedqLD5on1puACtRW6hxyB8vh7Af0BkJlZRms3v0tZbyIejk3JBFcjyMNLUrXQipVjnuAHPk7MtygzdVo6tPTBplF2JL+GcRH771lRdIjwzIedlZzCiJZFvJQ+b3/YaSfj1MMPweJgAGMoVsyi2lyUvjfZGCpkvtW5nrvCjRuDxXI+0AqnmVULcX3N/sqCsdGuQeP4VHGGiZIn/pmrpiPxC4LJt2GOkhoRBOFzwUCdDkd5Sv45L2Ma5j5hIuNIBQYlA9XiDPonPQxHPf+tMC0vCMrGfwXrkAJVfxH9W64DytIpVFOqSmNLKbSX/A1jJWeM07jZEk8rNqJ5gx+qSyYpSU443XxuojgaIIWoJy6peg7BZdhgIBZHrRvH8Yce6iF3fBcUCNcu+p2TTkBVV/D9iAiuaEzUfPVNQxOWGJwZhiBOfjKGnDZ+z0vhuCvWW1EwGg72FEMilN7il3J5XP9ui2iZkUAQkcerKS+DeGMcNlH0qaFcJWliw65Pk7jUmhGjvQdgvbiI3lH3xlEveDtMa8R73PHQzXDH466vfgTmluuAdttpbmerPQd3aO5ChVzIPfKD4+i5FpMp4iSNpIYbQDadYkq5WVInw9B8KK/IJYnK+58dDAa425rVKEzR0PK+q8eh42OeFRn6mNRQBdFsFxZx49mQejBRLOwaO2fM8VOAptUXu/9gRr2ynFEUXDCYtIlnQ6iWEDX+wqqUOqE/wodoKqhqbOja3qLf3msUMDCtFoTLkIulRDjfNYI7lS+nDbeAQQ/za4/C3V7wDpQjqz1aemiXEAtig13fOR/Vf34c7ZGRKJ6Ua3YjqwgTd9j/16Tph4kCVe59dVaPKO+tgDofhTUDMo08M9u3XE0tVstZDuk3BApiVpIXXIg+2wdFEvPHaqp+h1UqssSdKOrzaLyUthG4UWOSk75ZEspMqYaIBYuuLBijXW/ow5F4OHo+J3WmdeEIUE81dX1FZNqHEtVZFYqqGqA487Fon/gg6MIM7PYb0L/xcmDnNhQQcNmBsoHAetsF3yoQm2SW2YDqAWbKMRz+v96GziF3S9XfUCCCDfZc+lXMfebN6JQFZAg/mQNuIdLECEZ97KT5I9YmdA+Ada0S2/0uanyR4p4mAUVCQ5mRIdQz+zsMYy05GwjnIqZ+Zy7LFm7ds8/JiXBxwDd2tl+5Xd3vzjLkpJUj6iMaKEPa524HyY+8qUcQC8AEkPML0FYrC0arCk6m4UrNfiADWYWo8ciyEpQMOFP6d9WUqPNitPUizGEn4JAHPSW+YLUwi4UbfoyF738Bg6suQTGYR9EdScKWoavv9CtgpMKMJax/wZswesxpbm487KwVAvEn38Lsv52HbtmCmCY6uYFCctLTUGnakC3FRwYSvB9v1jZgzBqi66k9QpkHCzVwjZShtwOXRJGEs0JREAPWL7iWYWzdtQ/bdu3BkevXQ/ZTwAz3cS/9+S9QsvGFlUbyPoamK8gXCOWAD/hcMwg9UbMdFYI19Cj9+3XDAFpZNR0KksCLCNVgzIGik6cbAUkQ1R8ybMzUSx1hCECrO4KFr/8rFrfd4KYytkY5Mo7V93oYDnvBu7HmxR+EnPJQDBYWoNb6OXZedwKz/b5d/Yevw5pTHrpsIDrpZ4OZ63+MfZ98HbqkIFMANmhRUwMHyE04T+wZBneAMPeO3B5NVqZVpHlkIvSU+omxCOGkd0PZ1CPnt2g26OVsV83ROgFnOGcV5//wioai8HKP2rqW1Y07bscVt+5Et1VmVTE3LUeAJtQtTFCy4i466+Yj3CjGaiMQBPG6ed8jlDKUyNPE5s3m7MnJYmLzZoP9GKMXQaE8HjnGM8wkW00ZiySuqHDM+XmxNqDWvilrDNq9OeyafheOePEHnCJCVkCMn3g/jJ54P+y+eBrzX/4gOr052LIAgVAQMLe4gPaTXjaz/qynrIEIL9kRfQGzcMctmPnEGzFS9SHtDqSune4PeaqBuC3exDGXN0NHpg8OZGVJKv01YzjOzQ1iS0q8FjgyO4xhr5l80oSsST7cOhquhpHt6KIWIyNtnH/F1TjjuGPwwJPvkWbL2ZnJRCgMY35xEe/72sXoVRbtdpm8ryU1yBug3/wdBC5OZHQF9mwmvSKZh2BclEnItHAFkJ2cnOQfrFtnJiY26zSRnUbT89dTXCWHFRVWLGBoqLqkxMFVja0QROwhvFWXP6KGmq8RxW0tqD0KXPtd3PGNT2Lj457fzPc8OHf92RPoHHMydn/0NWjt2wnudLG4bzfM2c/EEY97/rplc0QVgBj9md3Y9ZHXor13G2x7xO+eQwSvTPU2YP+akscB/YPm/NxrcYe0frY3Q6pmyCEhsPbyfqM2Rm8MNMhVjWKCkgpYHifh50QAtQriNt5w/n/i2Tt24OlnnYHxkZGh/FPx05u24kMX/gA/3roDo60y9S5j0dSUA9QM2oZsx8x9CQNii6PHIDUCMqKP2MBaAcgC0i88ub8PAM9730c3LEJO14qPa5fmmtFy4YoPbdq0x5OKOCDC6aY/P/vT61r17y8MrAWRkUZCitgsTtg4jx9UdbPPCBgY0rjiVG0ZEGZriw2v+CeMH3efJSbkap3W38wvrsTeD5wLs7AL1elPxjF/8lbXjB7eQXyAVYvzuO2Df47ihkthRldDpIZQkKBTCBPIepS5nyblzlmSweUSKskXD45pJ+2CeM9Atp74d98/+nff8nenLVD508oZTWoAEaXiJ5vnRhoCD7ECm5yibD3Eb1CDc0IxUAWE+YUFHLtmHGfd/Sgcs2EdGMDexT5+fPOt2LJ9J+atYrTV8uCSJk2BhlmKw+S1rBmeA2coA/zmCzngMxN7EGLabdb5vVd01b6waLWOGHBrk1XzKC1oIwoDqixY7a2w9cfHtu58+/QHp+YCxbWw3rNQMygTMWWq9tmEhHL4v582eG8+uEK8qZcIRwcVBrrSw67/eA9GXvFhmKLVZFSbAioWq4+7N3qPej7mr/4Ojv6j88BcLFHzD01QaxW3fWoK5vofgMZWoZbag3zTSAuqvuzNaR0ejMAU/WCa48qMcTeE8yrRivZ1aOAwCctoqrrmvkkIGM0ptqn+bEK2tCnfGaBL4d/GR7rY0e/hP664FlXtVJoMAQUZlGWJ0QIxEGNasKSKz4IvK1oaupWU2Xbku2VOUxgaJQLKdb+HojN2356tL+WyhJoCdTUA1bVoXTn6vSmOLEfGX7/3cDz+d//i9U/9PNHWyclJZvYyq43WhLWeMpojkoca0uFtM0WBG+tHeYJUQSoJYC3KzijMDVdg5wX/5sZz0kzCyeeTGx7/PBzzin9C0R5Z/iKqU1e9/fPvB1/xNZixVVDrVRc4DfiFmsddsqQATGFSsMRKM/fXzl7WAwAAgLuFNo5ShN5g3txIZ0RQDdNQXQ/Ha8YgDBLMuZ1JRH9T5pwKRYsMxjsdrB3tYu1IB6s6HXRbJRhuDs0ZMnuJUm9O6o+ofYpFaN7mkay3HNIb9u4Sw3muZrTWuq7VArDWSr24YNnNiRkCY0CsUmt/YX5Aq8buPz9+yPRLX/rSdujcZMiVNNIK81r2SWtYMwxqJjhDR0/kqlDivygb1Epoj46i97V/wfz2G1Nje2ilMhGMKZcNRBULMOP2//sxyDc/jnJ0PELoo3N97JsmrjSLAjbhJsU6aRBukI5yJmNQnFXfxlkyc2s0z50gQUKkSw5Ezlo/DeBthsCO0sQ5xyXkq+z6uuLhewqCBaPyXjq1AJV1M2ywAdj9jDK7Re9N5jXmjN4jxv+caNA058SN8adjLiCgGdInKYkMU2iD97qbG4oIE7FRJwbkU40IQmgNFuYqs2bNWVetOfx5U1NTUpBaCdYTIQkXNhBRGNImsEA1Ca1STuTPfVac6HjsOyEprAoZtPtz2PWFf8DIi95z5/ODZQKR2GDnt/4D9Zc/gHZ3DAOr4FxXB5SBaAPYkxJpKACDM7Q6B1RKnoZEmJx4KoV7MxUGMZ9Jx7MuoXIaTr6GyGF2pCiYMd/rw1Y1RssChmwGWG7q4KRX8MxFIlfMZKoRDV679SoZkokrDElR584SoU/Ys8BAgW6n7ZDkFg0if7SYQ/N5CM0cd5jvFOgJwWI5npbRts6wFVVTdP90cnLyIwVRASZZonHExkSV2nTMZfLEqpHoZIgyRdqcwZZNPdTxS8zYKgx+egH2/Og/se7+j15+moLlA3H3ld/C4mffhW67g8qTrihrWrN/fSXKzLt928FKpLimvhkv8dyLwA0CCF4zPuZELYCqLMH2r8LUAEzkNyPtLk4kf3ZuAacdvg5Pe8C9cdIRh6EsilyHY0hvPM1+KQPBIuvpxhHuMgtah9o2OToxwfcUu+cWceGW6/B/r7wG/UphCvL+lkPqGLkxaOBFDRVKTbXhhPIPaiFhhOzzTGOrGoZbp/1wHmcWtYjfQk08GTn4pSDZebl8gROwVJJzks3wbdENNVM1SKvcQZa6poWZL3wA4yefhbK7av8JduBFs8HszVdj9n9PYcQANRWA1MlIR5sVnw4FBQXBpAg9TD546YZmiyB/z2yA2h8ug4GjOXjlfzCnnmrgNqtmQlWJtGSYMb/Yx+NPPQave/qTUJgSvy2PozYA9znuaDzq1BPxV9NfxWytKE3YWJq5Ydjhc1cJzfI9J56f0foIjV0xXKd4vQBBp2V6vc79GOQAfTkmsemsmpsAZUJKlLGdfb6hUUcbjeMm2okpgaQGlW2Ut/0Cd3z9k80x3TK5GZgxv/0X2P2RV6GzMAMxbVAgxxAhd8IKxwIit1uTABIyDniWp2m+c1BKEbygpNO1plBNBxorR2H9UFHzEN+5MXVRoD+ocdTqNl791CegMCVqmxh5v+kvUUVlLU479hg876FnYDAYRIR9bD3lp11smaSia9hQioZriZwg1hAOcNAthZ7IhoolppSRC5tJ3OX6Nul58+CTFMABaKUJNcJkfFWqsGzRKluY/+lFsLZe5phOb76am8GuT7wB7b3boe0OUA+GiFySKs6saesq2WYLYqmDlg71VLMDU3ON8XRMk+fOJLgXIjAk7+NFhzB/N/tVhYeefAK6rbazRzbcKGR+k18BMiaqOP34o9Epk0oFhrWTkDEoh665NHJSuNZcjuJfbh7us3irMsb5TBWZHFvA5pFI0H7P/F5SUpoDbYP5pGYVZ1LzFz/nZhgB5q1izWOfB2OKRqXZyHiI0LvjVuiO68Htrj8aTSKaI2n0RNfQTOwp+KLkTd7ARQ4LLmZSOtyqcIWIevfvGiDTtakNPYRyT/7LWUYnkkHvBEetXbf/U+A3/Ajg2fFOG2tabudGNhakDJ0eRKRy7CbFkXJGjfX3QYfaWQBFIbAMOzvLUNE8qCia2iDTvGkW73leljjCfmVkbRIR7xmIIOBZwxQFenP7UD72+Vj/gCckL5gl/VjXLB475iTQvc6BLM7F2XiYnacgTk138r2wvNLU3LEv/lveIfC7P1NjZqwRfuVep1OMRAHNGORZmrG8MJb6ogqY7S0crOLHf+tDVbE4qLBQVakXyU1T9oag1pI4aIJsNFOtaNo9Jh9lIiVYC6t6NQdCcpOrmyX/3lO5eZxpQ78mrJDo+hRziWSq6KimBer5vajv8xgc+aQ/bc44l23wuA+9/kl/hvmRNWCtU+WrSZI55DHi2dnRgiKDhQ1b+UbUMjk/v6aUnyY1Bzgt/IC6DqieZHjJMU3InV1jv9YXgAWXuOKmHQm8/lu0QyqA2uf7V9+6AzN9i9Jw0ByK6a94CxVmykGs8TrRUMVOQMbAzHbKrNhjw2wHC/1iMP99FiQ9Q820r3OP5DD8zwWakIkt5QaSgYei4np04pUaiBmoeugffg8c+Zw3grhYFrUyvDuqCEYOPQajj3wuBguLMN4ylw27hjAyK7J8+pKtUFZkJuOhRskCMOghNkROfSNdFWLdPKfHNbm6iDJyPZpkKs2OttBrA2GkXeLSm2/FV354BYrALPRB+Zv8CmP00hjs3DuDj178fbRbba+/mOgkCSamQ2S65vQupHKa28Xls3hOqCYlsabsqO0PLrnw3W+7suCIa/Cd+VAv5/kQORK580f0GozWNiiYgQsnWX8qWLARGCw15ooRHPpHb0JrbO1++ov7AYuqYP0jnoVbr/gmZNvV0LLrF6ZdokeYdWeDIJGrvTWjHkQYSq76kPUoAnwL1KRbLFoSj9zWIBY5hMKhIbCBVYGAYGBQtDt459e+ja179uDJp98bRxyybokg52/isdDr4ce/2Ip/+sYl2LpvwYGTM/1zykarnI2GcwWMfMrksA3WuikQcQOs5m9TrbUaLhWDPlm7+FYFUDj4lGYa1Gj2CxPqM3JbSCkpnWZumxp9jSVqIKoSSlLM9npY9Sdvx+jRpy6P1h4W18z+rKIoWh2s/t2XYe8HX4LRcKxEf6x0IbjBxwk8GmqQzj3J2B+ZFEeInLd7/CQFlFb2AI2OUgOJQ55kLhnt1XEagyKsgIVBZYmPff8KnH/FNThx4yHYuGos8kmiPiJpjsRonB401NJmRlaMcVTfaEgBBikXIHOcdQuoV1e4cddubNu9ABSMbqvdJGFRmlVHFd5c7iRnCGb/LbtdQ0ywgxoQW3tcM4n7JSlgqN3pFPO33/LO77xt8oKJiQlTiK1VjfjOeIYeyfLI5GCgGbATUa0g3jBGpoPiuj3GKObm9qLzhJdg/f0fu/9AjI3xZXZH38NcffKZmH3A41F9///AjB4ClRphPtkcSSbQQwSG5bqIDXEniWJSminQRqAIcXP3Egf+iJLDIpm6L2LnIH/vaV7iUplV7S56VvHDrbdBZUc2acqI9Bxtbppe21iKBXDFhck3niY2ANocsSqieD8YaBUl2q3SgV4yjGaufx5QPKFIyaVtNKOyCgFc1SKLc5/Twqwn035oMTpS1FUFFUFBhtgYRj3AYNe2d1381je8JuikF2wMwAJbp4inRkD6SliS4WGcqvibwZSseeHhZywKLgwGs3tBZzwNhz3pT5dn9AWQ7B23Yvv0e3Do016C7mHHx+83j2vFhif9KbZd8z2MLO4DCpNJgwRZ8HyenjCBSS8RDUXcVHQkP73Y8FVFS3KKaAuEJB6Y918pOJgGY8gM7haoCjGevYzKaLtMfVlKLfjm9ReP6XRqGpTJqsaZOtJnVC8iBfYBKYGnnn1WRLxmtCOrxYKEG2L0kSKRdweguWp0Y7cWVdvqdk29sPMzF0y9+lkA8NjXvff+9UB+n4w8whg+xkp/Vvq9H6Ke/advvu3NF0KVpshlP4X1rpMOMs6NmWfDK0QVZB2RKRhrxya5z59M9CjxamALCxgcc18c/azXJh70Emwioeov4LaPvxHmZxfgNiYc86L3LMVK+KOis+5wjD/lpVj85OvQMWuccCakQSh3kyKN5PXYivEqpI1KOyrpZuzEUI171AzFWfQgGidF+gJFoFd8/iixE+H62vTD8Y1668edhnhIjydpY8Y/q3VKbwL0qgGqqnb3J+zkyigNo1UaGDBqayHRvsST6Gwac9owNZI0yl2iM55JLue8mXyCkrdtghVwWRaXTk4qf+mID5uvvehFPwLwIwLw7Le+9RCurp3/xJs/0XMg70kOgYiQM0akCbRhtq2aw6A8ey1OWzKUDLFfgf4IKAyo38Ps+KE48vlvRtEZW4LuDruissEd578ffOMP0Dn8OMxe8U3s+tHXsf7+j1lS5Dgwr2D9A5+EW7d8F/VlX4YZGY/ZUYCkESfbXKWmutcw/yTsnDbsjsFZgbO2kW1uA00AQmNeCgJH8G5Qu9ZM6ybfeSKQwqc70UlriEsTIFuziz2sbhvc74j1OPnIQ7F+fCyyOnfMzOLKm2/F9Xfsw6ICo+22E90KRxZnhKwc4pddN+RU24w4RjnF1TMbl8ESJ9AxdHxqiuTsyUmenJzkiwC+eGqq/uTrXrcr8F8wPY2pqSnbJGQFw/gAHw8tFU1AzWAOINQc/XAsYiV1lggwKphBgY3PezO6G45dtnIOueMd3/wM5KLPoBxdg7oWjLQLzHz5H7H65Aej7IwuBVH4o2n901+J7b+8BqMzt0LLluPbhCkIZ7T5IFQUG/ncVGalps64wtNYobGJHm7WYDCAFGVKBwhLBELdosuBBfkILGcKJuRQBFpw2iHjBIkNFqsKIww884yT8MT7nYYTDz+8kcJEdmBd4Sc334L/uPRyfPu6W1G2OiiNW2gNeZXhwqtBptOGhEqkxWZHdr4rDhczALBQVdH61nNhJCbzRNif1yCHpmRU+yJ4K4sAFvAAaj9JIL/1m0wGOOYQUqNgxtzcHNZseiVWnXh6RpBaisTZd/1PsPilD6AY6fhqvoK22mhtuwE7v/KRBg20cVxD0Vm9Hof80RTmqAVTV2mXNtxAdjeQ2aLefSHlxywaBeajU0OE6iuUkd34VjrMwlE+pLIWjtooJZLTQNEEJ3Cuu5MND8JFJxDmB30cf8go3vMHT8IrnvhYnHjEkQC5YtN6WRLrUdlFUeL0E47D2/7g6Xj1Ex4GgxoDj9qPnyFLTySjJORB2cBi0lKgg2RN7twcKfxOSUb306e7Uz9GFlVK9ODMBSsnevgbZ8Lq8GBQJUc1II9ENqbA4swsWo95PtY/+Bn7qZxd22dh5y3Y+/G/QkcqSKx0CbCCzsgo+hf9G2avv9z9/tDs2jXDLVYdf2+MP/P1mO8JClJQUUam33LEds5IT2GRgTM0D/uGuVcaEyeWE3e/VsQ7cjZWTPyrXGYYse/I8UaJlWQblxHb8uq49ioWDMZiVeGU9avwnj94Ku517DGwASsKOD1v5vgVAts1swm/+4D74S3PeBw6BNSiCeaSNeiZKWmMZxOnqP+dbQTDiy03W2pOujT6JR40iV9VIhhbXWYbXTzV9yCDVEecajChFuesYNQ3t02Bwdw85PRH4Yinvmz5prYPuHrQx65PTaG1dxu0LOOkI1AfLAhdsrj90+9AtTg7lJclzoyKxYYzH4+R505iriagWgQVhQtu3xRP4A/2Tq4x24WQV9yNQUax3RPLXovoTYMWGqjmKKE6NOKLVhW5Y1U2IhwexeW5WYCgVaLY0C3wpmc8ARtWr4EVgWG6UzWJcKwyOUL/WSeegNc96eHQuk7mREzZgtYh9QxquDMsVddoitM3T6u0kRomXlkwws2qs+wTNkP0KtQl9z5RFvF/97uuqoVBASzOo3+3k3DEs98QwRZLCerOqeq2z7wT5vpLwd3xbAdxhHjxiAdqjaBz69XY8YV/yPQVsUxACjae9SSs+7P3Y3b1kahndoPr2muOp9mqShK+V8USRLVm5HXK5D6chLTED9OAU2WoHxrmHmczcG0085vCARhyqgrz7Lrfw4vOORNHrN/gA/Hg7m9hXEH0sNNOxhPufXcs9Ppe7DWbGGVFaMhZ8x6jqjZpFpp2b82DEE0xMlJaEXKY2UOgA0EJTA0+SQh5yQbmcZBmFSADlR5mR9bisD95C8rRtUtUWx0/wxcsF/5v6Hf/A8XIeGSg5UUGYl/QojW6GvZb09j9owviTrjfhvg9z8Axr/4EzBPOxfyqjVhYmAf6VVZZS/K9blS/uR+hNERFo6BBxlsTry1JGSlN0UTqNP+MrFAIc/Qs+Kip9MBEWBzUOP3oQ/GY+97LeRryijaa+B6e9ZAzsLbbwSDzYiTPJddMezwn9nNuZxcpEQ7DyZkA/bCOETFBWVa2M5Kfn1hRSmgdRLg4ZTZhmskAs69MjQLzarDhj8/DyGEnJN+74crZGOz52SWY//zfoeyOuGON/MWhgBYnkPhUwVMWRlsGez79N5jfduOdBiRU0Bpbg8Oeci6Oes2nsPrc92Nw3GlAPWgqa0WCUMaKDFMSbRLdw1w8F6nmaI2Lhikk5ROkMJ5sjOCSrEp+HOcTnohIrwZ49L3u4XnjK585h6r3qPXr8YDjjvC7o89hs2KJlmMsZmP+Rt6dgWolL7oyG5OqlpUe00Ihj0h+K0tNgRyPg5LfH5wOda8/j9En/qkTZrJ2vy2c2V/8DDOfeD26VHtFq4R6CTWWaFgegBDDQiFFCyO9Gdz20degt+f2/QZkcGVVEZQjq7D21N/B2t99GfqVdcQtGc7VKP43qp+hmfs4rGM0LKfBYNCotjX3bsl5IhhSgs2lkYElhUSkcqjCKrCqW+JeRx+5HDdtRfgwBXDWCceg5Og5ssR+OLmsIk1xmtOVhv1cLn6qQ2ZHJpc3PphgBBccTmMrmXqBaFRbiEhoQQY4YNiqQrXxBKx/+IQPuhwN7Mj7xAYLO27Cno+9Fp3BHMCdgI51u2imiBrklTU7usQKqDOKkdtuwLa/fzEWd23zFbb1kle6pCJV6xTZFm78GRgCbWjjeEkOCXbCtAwvMexgAgmbxwTQNiZiruIsesi+F9mugaE8kjMj9GEyf9gta2tx6KoxHL52zVL5kRVCuAnACYdtQGkcCiey6vIiCkkeOt8pkQUpNfhDzd5ijnRXWhlYk0mVIS5fzB1Sw44Yc3mm3ELL7ZSeLgqvqQ3KrL2IAWMwd/PV2P0vr0Fr3w5QOeJABOSRNpRgMBrBC9Sci5NH2HRG0bn9Bux4/7nYe+0PHWG98XoUARAwBXZf8U30vvFRh82DuH5hJgmddiMbAa9KTU6N60kzhEC4EVybQtkT43N+dz4+QyaYlBcE4b829P0w7AKb/tstDFpF+WvZGMOjNCapzg4roWVC94Gcl3cCKDt9ZBkxglwmxVvWrehtF7BW2VD0WSHDQxVjpuaVXx5RqGG0dt2EbZ84D2sf/VyU6w5zarT1AIM7dmD2h1/F4NLz0R0sAGUbonUGYXLz1CCYyUxxhbLmrD1X0apUaLVHQHtvwZ5/egXmz3gCxs98AtqHHg0yTrtHevPob78Rc9/9IuSn30S3YCgbsMLZeIQn5FRVMpxch7MSSQq6jmgeDNmJcTxoMAC4SDA0yo7dnGiU6xYOO0JQcrNvShpnD2PMfwluMU44M7U1Hd5Cc2Zf+AxZwRJcbZWGZ9mhbcRQXdkxXQjcjRJKvbYAjIiqWNTArLrJi/+7KdvQH30Vd/z0YujoOtDIOKi/AOy7DUU1QLfVgS1aILHZJMOrPgTcXQbXjzdNkYwq1dnD1WqBoo0RKOpvfxp7vvc52PH10FYXDAEt7INZnEOhFVqdEdQeMMFKKNj42bvG/DggswNQAcSZ9k7QqPRvYhZUGatt9eADP3+OlsPZmCyf5+YwrFz0qQHKRdMla2axh4VBD6Od0aYO96/w2Ds/j8oKWkXZ2B1piE6q2tzxXVYicfE2CPsNhwR3T41rmK/omC6UtHIvIKreQjZMV5iHLCM08ZXjNm4IZmQVSgh0YRdo7nb3+2UJarWhtfUyx01nrcC6w9BRFXaNnBQOv7NFbWwAxfhqlFagi3uA3m5fxRug04KgjVqzaYJ3O0VmSgTlZRXEOKl8Z4w4VpwIFFwMtLY1VIvoNBtwfdqccCDDT2rmSpUXCzTEmAMBhTHYvm8OW+/YjZPuNrpfjOeBk6zcE2y5ZTv6taDdoqRPlFX6Ob881+II07gluXWuAZ7L+EFhCdXKChjihYB40SExH8ncNHM3A4nSucHjuIYVhRYlpGhDipYTK7I2qzwz4XSVIfHR3E8mzWmjGTjnK9dXn1YcFs8UUNNyX961y9ZVE3CbtaiQ+V3TkEEjezuQ6CZLFJAO9VUXQE9dv2a+LIvFpNajDfznsHIXlplTi28YR67QELjdEDA3qHH5L7Y253C/wtEMAFfecptH4tglY9IcCsa59HPWWB4W0ccQ8ayR1hHtWVkwtkfvUM8EC1zkPJMIR1muku9wdBSP0yjvFOVMkrWFc7uiRkM4Z5sF/ozx0CvxRC4KJHcNYyIM9QYTfhoiUUtQxKII9m6x4bz/XUORTNkV6lW/AqfHpxCk81Onwr7q1GP3FYb2inszimXaOZzN74cdBpDnXEMdgBy+1SpauOCq69Af9Bro7YN9hBHgDTtuw4+2bsNIu5XuZaiUfTsu12h0nOhsUQ6LJOiS4T+iR70CRum2FQVj1Vp9rRUDVqLk/xfco9KOogo0/CkyZrJSwsURk9slgxqYD7YAWm3KYSDKvdncR0aSY5QNLLahgXzQHA8uCbEhG0Xyk3RfLsqe+7oAyYQ9BmcuuUxQQ4Q+il3T07BHPehBvV5d3U7GNBS5xC9CNFhw3Eg9ho84GtqR8uZyp9XC1Tv24cuXXxmxmCuhn4aY+di3LsV838aEhDNsI2WC9rF/HPxo0LT1TUietFCDBbOf6hCqCtLr3woAG7ecelDriOd61RVzldbExKGyDXLDkilNMKcjDISEAg94yMwzJB+VBevYYNNGkqBoOT86gESDLDNxykXiDhlvcBOJE4I6NpgzFwNQ8+anwEsTkTBzj4VTzPVUCwZK5gsDkhkWV5uCVZ08W/QIzLfb+FrZSE2HdhIMTW0aPTsRtNttfORbl+Oarb+EYUZ9EAEZesaGCV+87Me46JpfYKzTiXa+krmFNVpSuUJERkERbVoEUwM+Fu+LMhuuFxcW6z0z1wDA9ClXHVww/uj3XvNja4qr2wZKCjH+BSWrajP5rkwaz1Wp3LRwTv7RvghSztQZsopcM8vZNFprAjkpGz+F3lcAhIjYHFPSaEPl+WXC6CR+N6HJD0fWeOfgfuIWpJnti+6b738pxknVvxgiROoEMFVzcIU2Gt65PPLSdlm6yWE0GMZrAkVpgDmreMN/fBXX3XoLCnb+OndG/ndBqN5Sj3HRVdfib//zErTLMmofNXwAh8+I2JSXpgB+9t6GRaOIgt0fhItCSe2PLvqnd9wMVQrC8QccjC8644yqh/KznbJNEBX1Ztu6RA4w7R4aioussAgckxBcoUiJ7eWQV3GmHuZ33OSmgIaNRchZ/CbkgjkGE2c9PgxdHGQNtTTZCaQrDWmAaEMMnoidE5XTyZGuMZirdMvMltal6r1LisXZr9rFuVk2xgmaR/hbJgCQ9xmRUhMZyhWX5F/Z90WBdlHgtkWLV/37l/C1H/8YTNrALQ6Daz18C4Dg09+9DG/6/Deh3sDTtZ+a40imZn0Qp28NQePUd+SsiAmsgMQrAlSE7MLcpwjQs88776CbpQYANj3+oTcUi/te0CVp1Y73S7nLafxfGtqJkFejHqLOQxzfsBsazmMty8uyxDgIfUaUeVK1itYRlKq+Zh9UGoUIGV4qTo8k2hQa3oHM3yhmXLjbTqcwt9XmrQ/8zLe+93BcVCxsPJO+8M8fnLnnIx5zHI2Mn47KWuVQ61ADkNEgMeXHXHZ050Dc/PfyXmRBjAULXHT1Dfj5jh1Y221j/fgoClPE8WIIkvleD5dcez3+9v9ehM/96BqYsmjgHylHe2dHbsQ3ZiPBxucYoiwk7Un1IgkqVJRsZ2du2bjrF+duufzywc0XXaSYmjrIPuPEhKE3fnzrT/7qiW9b37Jvqef6lTKVlHnDacZ3ifzj3DfGbxKaTR2yDcdNeEXAShBfqUbrMjRtJ+KMM+7GKfA4kqgE+QzB0X8p6TJyvqXnhuw+T7Pim97iGbHsdmfr0gDLascNih2LuO7awWkfVf0WgS6250xOEqA0svg3b5njYpMUnXGyVhTKGBr5sofdBbJVdDIY1jHMV67nJgeifICslYZRmhFceO1WXHL9Vhy3bjXufcwRWDc65ndFwa65Bfzk5m3YuncWQoyxbrvpohBaNEF6JN4r4zu3klDw4fXz+zlUcBEYxhtEGxYxREW/P/+66Q9/eGZi82YzTWQPeoyuAE1PTPCGU86lwxbfdsHRvPCwmUFVEXEJ5Na+GhvOOd0zWTwko6JYhHikeADnsr8QQXJEh2a7yPglcWfOiOchHRAP0m3q2CF7XjR6o432iiaSkQb1WQLIanBmkzZDB9SiW+zII878269evHliwmyanrYAMDGx2UxPb7JPPe9dz10cX/vxxaquCxGjnsugxn9OJHGBfOFhmfEhchmZsNg0eQ1yyCutoiZBvxbUdZ31/Nw4s1UUaBlnp2w9cMWxPJrVcL7zBvIdUXNClBeJ+SydoouWHw+wVu3uSFndtuNTF7z1tc8J12fF48qrTjlFz5k6p7710OOedbt2b1jdapUizshWguBnnpcpltjyhhYPZaBcUYmBmLdNLNAwMsptOPI+ZOCPwO8wjqOimXdhgtCTVzPI+4ZLCByhyPLjTxiOiBSwsxssCGiVLbN9oC8fDkQAmJ7eZCc2bzbnn/fqT+jMrneOdNoFCrbiNF4iCikeLEzLvg2VpG+oGeV1GNHOWfFmyQVPtzQY73awZqTrvkZHsarrmIDiXRBSHqwNwdRG5Z5TSZCJl2bo9Ri42aJmYlipVVnrdnes7O/eecH8zy9/4eTkJE9vnhCs8JHayJOTTFNT8u23/dnxR8/euHkDLZy+b7EWgSqDWKwl9hUde83CKKw+RJbKhYE0UpCDy6GbqCRCu2YxTYlfreKookQRTJGsDXLNaMqORRnKEXWZnYlScUXRdFxIVUZaZbEohO3SesX93/vN9+nmCUObppdd5WEHeMx573yLGVv3ul5dw6rUJdSAmHIR+zwLiSKalMRWk4yMZJjKZbrdUV5Ql0LRhsC9Qaw08Z+pOYbMZK/D71ux6T3nG0t2jVVVRdWS4aLT6mBxz87zd9+449lXfuo988HpaqXBGCueqYsvVp2c5GPe+O7dd//9Z//7hpkdh3QKfsB4yVzVloio1hBTHk7UQHxkR1ODSeYVuIf86Cj1GjMZudAHpMQTCZUbcbaXO4SPEznVZOrYMNMEIggiKIy5ytx9BAaEVESU0C0Nj3VavEvMtdts+9kPeO8F/6YTE4ampvd73GzZMo3JyUn+2NQbLjjpwQ+7Roge2B4ZWaNQElULVVH1bXrPMqLYXkmBxnFTlOy4ZnW2yg3Z+4b3TlP/EY05N2ULMSUn5N+KF0TxsjTJ3MP9m2vZshJIRdX9vKoQs4gIuCi4aLfZ9PvzMr/nzd9801++5LYrvzfA5CTjnHN+peHlUr8dv0MCwGWvf9oj1lazry6rxUev6xpDIqgEzhqNcnyXZkdN4CS7Lr4TCDKxoLDWokYwHRzG1Q0ZRiQPP68pJV7/WaVtwAR2s0Jl37NLCrWqBOMZgRGJHIoMJpSqKIxBjxhzA7lxkcuPXjTD//CiD39jRicmDE1PH1DeE3bIJ7/srw7V9ev+ouLus9HpHmFN8C30vVRp+vcFHZ0msTvpF4qtYUXjIaKN/oVXicsKs2HIH3lPbQSb48KkFCtrrXJuDsVJxyf2SolguABIIGJh52d3mcp+jvbNvPcb7/ubq6Nd76+wI+43GCNHcBJEU25Tu+SVTzxtNRafOAr7IJCezFqtZhBbq8RuOqLCwYcv7oZuFqIKVSJiYhK1ytoZLTDerxXGr8rc0Ht4fBZuHGfz1rJk9GqaFcWiQjn4kBNIVYXcMeZ85ILUnUJUyRn+Wi56QnQzwVwx3xr/zyv6qy76o/d8ah4AhnPEAwpIZ1drAeBZr33t2pn2IY/skTmb2Jxi1W4kMiMCbQk5lrJV6xi/GsCspKlN5aDobPgwFC2j4piOuS65BE2seLwjevDk40YLgTEFbL8StfV2nx+SNsT14wzMv4QqadhFUavaOVbdDsFVrPa79a6bLrn4gx/cMfy5fx2PO0UnbZ6YMBOnTGsISgB44QtfWP5B97bRNrd4vl0RZmcx2moqCOwDMNounVJIv6L5gaVqVcndXYtaHL5x5G6D2X9YZ2efNFdZcUMWalR3qYeVkNke+2g7JZvbK/7Gba01f9KjxXkAGO2717ftUk3fIeLm27bx2Ub7Rm271N7uvtxy+JH950058aF4OzZPGGyalhXjElRpYnqal7k5dPZzn9veuTBarBkfpX4xw2uxtvEDewCs9f8d6/eoMrN29PCTHyBjo58D0bhr9XBGfKUMUU5D4OfU8yIikNCA5u94+ra92y7u1uOmnc8VDwGwK/xlF8pORwFgz759Wo6M6Mwv2/b6r36gv9xpcMopV+nUQU5YfqVgzI/ui3ARPxwXSx6YK31sfd+5z1m/85p/3TM/67x9cwi7ZEc+kgGS7z3Y0a4xN9qRZ9z3HV//P78iT4kumjzbPHzLRsX0rxCE+wnK26+6ii4GBL/CDXvsWz/wDXTGHtnvLVrP8ogiUA2l3GxKBmIH3SOSstXiam7muovOe+U9f6XPNDnJZwO88dRTdXpiQn4dR/KKg3HJEb7Ct3L5h08vvrjtcvvcweNfdSjNv2PfYr8WQuF6h5pE8JE5oiEJVMKKHe22zK1V8WefHvnmh598xOnm9BdeXq/kE//agu+grrHe9auedx7hvPP0pe9/f+uGXuvyypSn1tVACMRNnUQ0hZsy5oAoYMVqWZZkFxe26e6bTr34fe+bweQkYeo8XUFY/LdcK17BlVXPnzror9O/cblMTUGswX2t2jh804yWoURIFIokQewlnrWAwgwW7j41BZndNnbw76NRy/63PDI2K/kq606+fDHw81t3b1isq+Ostalt2eA0a5wP565mmtkyu8LNrK51zaoUUNGV+06+MPyF38pg/JUep7gPVpAZjaLAxKCh1cj++8i9/Xx55CVA/3vf92/gUXS7HHCFSzyjh/ewTHZPh+fwDNPhfvH/wmf+b72pF+FsRxi1dgt7GFAyokwtHvFWIKHCNkWRCbpDF1Hu+h8bhVNTCgBPP/bQ21ug7RGMphKpGYkwZqNxZI5MiaBmY2CszHb6M3t8CqD/fzAOPebLkassFU7mJniNaJM47nQAEt/FNauJFwZC82S+BwA7t2zU/4HhqBObN5vnPe95Pa3qS03RUlHftMl3P0rCxxEEAc4bNUJMqlX/J1/+0If2TE5O8n9V4fH/ZDA+/LyLLQGYudtpX9lVm9tHDJESSRjWI+IVPeXJW4H4Jq0dLYlnBrTlB9e0L1EFbZqelv+Z2+M0AKBlF/6RqgE56WIvYhGQR4JM1UyjuEY8tg0L1TVxPfsBANhy6qn02/6p/1uDkQj6mYkJ8+AXTO2eK8df1+6OcMFQK2KJjJeA1NAkC0AGhZW6bZgXhbCrNn/x8q9+tT+9aYLx31uI/PeF4qZpOzk5yV+Y+qtvtfqz/9zpjhVCWiupRCN35AaaAccpEIUwqGqNdMv+zM5PfePtf/OFyclJ/nU2p/+rHua//UJv2aKbJybMI/7xs5f/wYNPKdYW8vDRgtlaS5aciCKJkxBgIrQJNNZhXrDG3lIVLzzz7y+a1slJPu2DH/wfuiu6x8UXXQQA/Ni1Y1/bNTtzQjGy7j4gQ6oViIwQIOrHzJ7TpiDmstOmwhizePvtn8Gt1/7JzU99qlzs89Df9sdvbOvWSTBNQS577VMfs072/XnLDh7SYhkvQN7cRlALoSdmV1/qi2/tdd/+8A9d8MOVjOv+H35EBNejXv+u50i79TI25v6m1WGw8WphNgJKtRqArfxY5mbed8Hb3/iJ4ef4/4PxAAISAC6b/L2Tunv33otZx4hMR1EtDsC7bx9ff8Wjp6Z/Caxsbvw/IiBdoqgK0JNf//aHVAUe3Bc+iYxZD1VoXe9RkutbVf+SwTumvnUxUMez+/+hVOb/A/a0xtpA7oo5AAAAAElFTkSuQmCC">
      <span class="name">빨대 팬플룻 연구소</span>
    </button>
    <nav class="tabs" aria-label="단계">
      <button class="tab" data-route="s1"><span class="num">1</span><span class="label">만들기</span></button>
      <button class="tab" data-route="s2"><span class="num">2</span><span class="label">연결하기</span></button>
      <button class="tab" data-route="s3"><span class="num">3</span><span class="label">연주하기</span></button>
    </nav>
    <div class="hdr-right">
      <button class="icon-btn" id="btn-sound" aria-label="소리 켜기/끄기">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M4 9v6h4l5 4V5L8 9H4z"/><path class="w1" d="M16 9a4 4 0 0 1 0 6"/><path class="w2" d="M18.5 6.5a8 8 0 0 1 0 11"/></svg>
        <span class="label">소리</span>
      </button>
      <button class="icon-btn" id="btn-full" aria-label="전체 화면" hidden>
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M4 9V4h5"/><path d="M20 9V4h-5"/><path d="M4 15v5h5"/><path d="M20 15v5h-5"/></svg>
        <span class="label">전체 화면</span>
      </button>
      <button class="icon-btn pill" id="btn-settings" aria-label="선생님 설정">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.7 1.7 0 0 0 .3 1.8l.1.1a2 2 0 1 1-2.8 2.8l-.1-.1a1.7 1.7 0 0 0-1.8-.3 1.7 1.7 0 0 0-1 1.5V21a2 2 0 1 1-4 0v-.1a1.7 1.7 0 0 0-1.1-1.5 1.7 1.7 0 0 0-1.8.3l-.1.1a2 2 0 1 1-2.8-2.8l.1-.1a1.7 1.7 0 0 0 .3-1.8 1.7 1.7 0 0 0-1.5-1H3a2 2 0 1 1 0-4h.1a1.7 1.7 0 0 0 1.5-1.1 1.7 1.7 0 0 0-.3-1.8l-.1-.1a2 2 0 1 1 2.8-2.8l.1.1a1.7 1.7 0 0 0 1.8.3H9a1.7 1.7 0 0 0 1-1.5V3a2 2 0 1 1 4 0v.1a1.7 1.7 0 0 0 1 1.5 1.7 1.7 0 0 0 1.8-.3l.1-.1a2 2 0 1 1 2.8 2.8l-.1.1a1.7 1.7 0 0 0-.3 1.8V9a1.7 1.7 0 0 0 1.5 1H21a2 2 0 1 1 0 4h-.1a1.7 1.7 0 0 0-1.5 1z"/></svg>
        <span class="label">선생님</span>
      </button>
    </div>
  </header>
  <main id="view"></main>
  <canvas id="confetti"></canvas>
  <div id="toast" role="status" aria-live="polite"></div>

  <dialog id="dlg-settings">
    <form method="dialog" class="dlg">
      <h2>선생님 설정</h2>
      <p>우리 반이 만든 관 길이에 맞게 고칠 수 있어요. (단위: cm)</p>
      <div class="settings-grid" id="len-grid"></div>
      <div class="row">
        <button type="button" class="btn secondary sm" id="set-video">영상 길이로</button>
        <button type="button" class="btn secondary sm" id="set-exact">정확한 비율로</button>
      </div>
      <label class="field">3단계 박자 빠르기
        <select id="set-tempo"><option value="slow">천천히</option><option value="normal" selected>보통</option><option value="fast">조금 빠르게</option></select>
      </label>
      <label class="field">천천히 도전에서 관 불빛 힌트
        <select id="set-hint"><option value="now" selected>바로 켜기</option><option value="late">3초 뒤에 켜기</option><option value="off">끄기</option></select>
      </label>
      <div class="row">
        <button type="button" class="btn secondary sm" id="set-reset">진도·점수 지우기</button>
        <button type="submit" class="btn sm" id="set-save">저장</button>
      </div>
    </form>
  </dialog>

  <dialog id="dlg-result">
    <div class="dlg" id="result-body"></div>
  </dialog>

  <dialog id="dlg-info">
    <div class="dlg" id="info-body"></div>
  </dialog>
</div>
<script>
(() => {
'use strict';

/* =====================================================================
   데이터 : 8개 관 (영상 '팬플룻 만드는 방법' 길이표 기준)
   ratio = 도를 1로 둔 진동수 비율 (순정률: 2:1, 3:2, 4:3 …)
   ===================================================================== */
const NOTES = [
  { id:'do',  name:'도',     cm:25.5, ratio:1,     hex:'#E5533C', darkText:false },
  { id:'re',  name:'레',     cm:22.7, ratio:9/8,   hex:'#F08A24', darkText:false },
  { id:'mi',  name:'미',     cm:20.4, ratio:5/4,   hex:'#E9B92A', darkText:true  },
  { id:'fa',  name:'파',     cm:19.2, ratio:4/3,   hex:'#5DB74A', darkText:false },
  { id:'sol', name:'솔',     cm:17.2, ratio:3/2,   hex:'#2FB0C6', darkText:false },
  { id:'la',  name:'라',     cm:15.3, ratio:5/3,   hex:'#3F73D8', darkText:false },
  { id:'si',  name:'시',     cm:13.6, ratio:15/8,  hex:'#8B5CD6', darkText:false },
  { id:'do2', name:'높은 도', cm:13,   ratio:2,     hex:'#F2857A', darkText:true  },
];
const NOTE_BY_ID = Object.fromEntries(NOTES.map(n => [n.id, n]));
const VIDEO_LENGTHS = NOTES.map(n => n.cm);
/* 관 그림 치수(cm). 화면 모드에 따라 바뀜: wide = 패드·노트북, phone = 작은 폰(같은 세로 관을 폰 폭에 맞춰 굵고 넓게, 글자도 크게) */
const GEOM = { wide: { w: 1.9, gap: 3.6, stop: 1.35 }, phone: { w: 2.5, gap: 4.7, stop: 1.5 } };
let PIPE_W = 1.9, PIPE_GAP = 3.6, STOP_H = 1.35, MODE = 'wide';
const app = document.getElementById('app');
function computeMode() { return Math.min(innerWidth, innerHeight) < 500 ? 'phone' : 'wide'; }
function applyMode() { MODE = computeMode(); const g = GEOM[MODE]; PIPE_W = g.w; PIPE_GAP = g.gap; STOP_H = g.stop; app.classList.toggle('phone', MODE === 'phone'); }
applyMode();
const isPhone = () => MODE === 'phone';
const RM = window.matchMedia && matchMedia('(prefers-reduced-motion: reduce)').matches;

/* =====================================================================
   저장 (진도 · 최고 점수 · 선생님 설정)
   ===================================================================== */
const KEY = 'panflute-lab-v1';
const DEFAULTS = () => ({
  lengths: VIDEO_LENGTHS.slice(),
  tempo: 'normal', hint: 'now', sound: true,
  s1: false, s2: false, best: {},
});
let S = DEFAULTS();
try { const raw = localStorage.getItem(KEY); if (raw) S = Object.assign(DEFAULTS(), JSON.parse(raw)); } catch (e) {}
if (!Array.isArray(S.lengths) || S.lengths.length !== 8) S.lengths = VIDEO_LENGTHS.slice();
function save() { try { localStorage.setItem(KEY, JSON.stringify(S)); } catch (e) {} }
const cmOf = note => S.lengths[NOTES.indexOf(note)];
const fmt = v => (Math.round(v * 100) / 100).toString();
/* 닫힌 관의 진동수 (끝 보정 포함): f = 34300 / (4 × (L + 0.24)) Hz  (L: cm) */
const freqOfCm = cm => 34300 / (4 * (cm + 0.24));
const freqOf = note => freqOfCm(cmOf(NOTES[0])) * note.ratio;
/* 선생님이 관을 기준(영상의 가장 긴 관 25.5cm)보다 길게 설정하면, 장면 높이를 그만큼 늘려 관이 잘리지 않게 함 */
const extraCm = () => Math.max(0, Math.max(...NOTES.map(cmOf)) - 25.5);

/* =====================================================================
   오디오 : 팬플룻 소리 합성 (숨소리 + 부드러운 음)
   ===================================================================== */
const Sound = (() => {
  let ctx = null, master = null, conv = null, noiseBuf = null;
  /* 폰·패드 소리 잠금 해제
     - 브라우저는 '손가락을 뗄 때'(pointerup·touchend·click)만 사용자 동작으로 인정한다. 관을 누르는 순간(pointerdown)에
       오디오를 켜면 크롬 계열은 첫 탭이 무음이 되고, 아이폰·아이패드(WebKit)는 아예 켜지지 않는다.
       → 누르는 순간 소리를 낼 수 없으면 그 음을 잠깐 기억해 두었다가(pending), 손가락을 떼며 오디오가 켜지는 즉시 낸다.
     - 아이폰·아이패드는 무음 스위치가 켜져 있으면 웹 오디오가 나오지 않는다. 무음 <audio>를 한 번 재생해 두면
       '재생 모드'로 바뀌어 스위치와 상관없이 소리가 난다(잘 알려진 우회법). 안드로이드에서는 쓰지 않는다(알림 표시 방지). */
  let pending = null, silentEl = null, silentOk = false;
  const IOS = /iP(hone|ad|od)/.test(navigator.userAgent) || (navigator.platform === 'MacIntel' && navigator.maxTouchPoints > 1);
  const SILENT_WAV = 'data:audio/wav;base64,UklGRkQDAABXQVZFZm10IBAAAAABAAEAQB8AAEAfAAABAAgAZGF0YSADAACAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgA==';
  function running() { return !!ctx && ctx.state === 'running'; }
  function flushPending() {
    if (!pending || !running()) return;
    const p = pending; pending = null;
    if (performance.now() - p.t < 2500) flute(p.freq, p.opt); /* 손가락을 뗀 직후라면 눌렀던 음을 냄 */
  }
  function tryResume() { /* 어느 이벤트가 '사용자 동작'으로 인정될지 브라우저마다 달라, 올 때마다 시도 (거듭 불러도 무해) */
    if (!ctx || ctx.state === 'running' || ctx.state === 'closed') return;
    try { const p = ctx.resume(); if (p && p.then) p.then(flushPending, () => {}); } catch (e) {}
  }
  function playSilent() {
    try {
      if (!silentEl) {
        silentEl = document.createElement('audio');
        silentEl.setAttribute('playsinline', ''); silentEl.setAttribute('webkit-playsinline', '');
        silentEl.preload = 'auto'; silentEl.loop = true; silentEl.src = SILENT_WAV; silentEl.load();
      }
      const p = silentEl.play(); if (p && p.then) p.then(() => { silentOk = true; }, () => {});
    } catch (e) {}
  }
  function ensure() {
    if (ctx) { tryResume(); return ctx; }
    const AC = window.AudioContext || window.webkitAudioContext; if (!AC) return null;
    ctx = new AC();
    ctx.addEventListener('statechange', () => { if (ctx.state === 'running') flushPending(); });
    master = ctx.createGain(); master.gain.value = 0.9;
    const comp = ctx.createDynamicsCompressor();
    comp.threshold.value = -16; comp.knee.value = 18; comp.ratio.value = 5; comp.attack.value = 0.004; comp.release.value = 0.22;
    master.connect(comp); comp.connect(ctx.destination);
    conv = ctx.createConvolver(); conv.buffer = impulse(1.5, 2.4);
    const wet = ctx.createGain(); wet.gain.value = 0.2; conv.connect(wet); wet.connect(master);
    noiseBuf = noise(2);
    return ctx;
  }
  function impulse(sec, decay) {
    const rate = ctx.sampleRate, len = Math.floor(rate * sec), buf = ctx.createBuffer(2, len, rate);
    for (let c = 0; c < 2; c++) { const d = buf.getChannelData(c); for (let i = 0; i < len; i++) d[i] = (Math.random() * 2 - 1) * Math.pow(1 - i / len, decay); }
    return buf;
  }
  function noise(sec) {
    const rate = ctx.sampleRate, len = Math.floor(rate * sec), buf = ctx.createBuffer(1, len, rate), d = buf.getChannelData(0);
    for (let i = 0; i < len; i++) d[i] = Math.random() * 2 - 1;
    return buf;
  }
  function on() { return S.sound; }
  /* release=true: 손가락을 뗀 순간(사용자 동작으로 인정되는 때) */
  function unlock(release) {
    if (!on()) return;
    if (IOS && release && !silentOk) playSilent();
    /* 아직 한 번도 사용자 동작이 없던 페이지에서 '누르는 순간'에 만들면 브라우저가 경고를 남기므로, 그때는 손가락을 뗄 때 만든다 */
    if (!ctx && !release && navigator.userActivation && !navigator.userActivation.hasBeenActive) return;
    const c = ensure(); if (!c) return;
    if (c.state !== 'running') {
      tryResume();
      if (release) { try { const b = c.createBuffer(1, 1, 22050), src = c.createBufferSource(); src.buffer = b; src.connect(c.destination); src.start(0); } catch (e) {} } /* 구형 iOS 잠금 해제용 빈 소리 */
    } else flushPending();
  }
  function visibility(visible) { if (!visible) { silentOk = false; try { silentEl && silentEl.pause(); } catch (e) {} } }
  function state() { return ctx ? ctx.state : 'none'; }

  /* 팬플룻 한 음 */
  function flute(freq, opt = {}) {
    if (!on()) return null; const c = ensure(); if (!c) return null;
    const dur = opt.dur ?? 0.8, vel = opt.vel ?? 1, t0 = c.currentTime + (opt.when ?? 0);
    const out = c.createGain(); out.gain.value = 0.0001; out.connect(master); out.connect(conv);
    const o1 = c.createOscillator(), o2 = c.createOscillator(), o3 = c.createOscillator();
    o1.type = 'sine'; o2.type = 'triangle'; o3.type = 'sine';
    const g1 = c.createGain(), g2 = c.createGain(), g3 = c.createGain();
    g1.gain.value = 0.55; g2.gain.value = 0.11; g3.gain.value = 0.05;
    const lp = c.createBiquadFilter(); lp.type = 'lowpass'; lp.frequency.value = Math.min(freq * 3.5, 7000);
    o1.connect(g1); o2.connect(lp); lp.connect(g2); o3.connect(g3);
    g1.connect(out); g2.connect(out); g3.connect(out);
    for (const [o, m] of [[o1, 1], [o2, 1], [o3, 3]]) {
      o.frequency.setValueAtTime(freq * m * 0.985, t0);
      o.frequency.exponentialRampToValueAtTime(freq * m, t0 + 0.06);
    }
    const lfo = c.createOscillator(); lfo.frequency.value = 5.2;
    const lfoG = c.createGain(); lfoG.gain.setValueAtTime(0, t0); lfoG.gain.linearRampToValueAtTime(freq * 0.0045, t0 + 0.4);
    lfo.connect(lfoG); lfoG.connect(o1.frequency); lfoG.connect(o2.frequency);
    const ns = c.createBufferSource(); ns.buffer = noiseBuf; ns.loop = true;
    const bp = c.createBiquadFilter(); bp.type = 'bandpass'; bp.frequency.value = freq; bp.Q.value = 6;
    const bp2 = c.createBiquadFilter(); bp2.type = 'bandpass'; bp2.frequency.value = freq * 2.9; bp2.Q.value = 2.2;
    const ng = c.createGain(), ng2 = c.createGain();
    ns.connect(bp); bp.connect(ng); ng.connect(out);
    ns.connect(bp2); bp2.connect(ng2); ng2.connect(out);
    ng.gain.setValueAtTime(0.0001, t0); ng.gain.exponentialRampToValueAtTime(0.7 * vel, t0 + 0.02); ng.gain.exponentialRampToValueAtTime(0.1, t0 + 0.2);
    ng2.gain.setValueAtTime(0.0001, t0); ng2.gain.exponentialRampToValueAtTime(0.12 * vel, t0 + 0.015); ng2.gain.exponentialRampToValueAtTime(0.012, t0 + 0.22);
    const peak = 0.6 * vel, tEnd = t0 + dur;
    out.gain.setValueAtTime(0.0001, t0);
    out.gain.exponentialRampToValueAtTime(peak, t0 + 0.04);
    out.gain.exponentialRampToValueAtTime(peak * 0.8, t0 + 0.25);
    out.gain.setValueAtTime(peak * 0.8, tEnd);
    out.gain.exponentialRampToValueAtTime(0.0001, tEnd + 0.24);
    const nodes = [o1, o2, o3, lfo, ns];
    nodes.forEach(n => n.start(t0)); nodes.forEach(n => n.stop(tEnd + 0.3));
    return {
      stop() {
        const now = c.currentTime;
        out.gain.cancelScheduledValues(now); out.gain.setValueAtTime(Math.max(out.gain.value, 0.0001), now);
        out.gain.exponentialRampToValueAtTime(0.0001, now + 0.15);
        nodes.forEach(n => { try { n.stop(now + 0.2); } catch (e) {} });
      }
    };
  }
  function note(n, opt) { return flute(freqOf(n), opt); }
  /* 관을 눌렀을 때: 오디오가 켜져 있으면 바로, 아직이면 기억해 두었다가 손가락을 뗄 때 냄 */
  function tapNote(n, opt) {
    if (!on()) return null;
    const c = ctx || ((!navigator.userActivation || navigator.userActivation.hasBeenActive) ? ensure() : null);
    if (c && c.state === 'running') return flute(freqOf(n), opt);
    pending = { freq: freqOf(n), opt, t: performance.now() }; return null;
  }

  /* 효과음 */
  function blip(freq, dur = 0.08, type = 'sine', vol = 0.25, when = 0) {
    if (!on()) return; const c = ensure(); if (!c) return; const t0 = c.currentTime + when;
    const o = c.createOscillator(), g = c.createGain(); o.type = type; o.frequency.value = freq;
    g.gain.setValueAtTime(0.0001, t0); g.gain.exponentialRampToValueAtTime(vol, t0 + 0.008); g.gain.exponentialRampToValueAtTime(0.0001, t0 + dur);
    o.connect(g); g.connect(master); o.start(t0); o.stop(t0 + dur + 0.02);
  }
  function click() {  /* 딸깍 */
    if (!on()) return; const c = ensure(); if (!c) return; const t0 = c.currentTime;
    const ns = c.createBufferSource(); ns.buffer = noiseBuf; const f = c.createBiquadFilter(); f.type = 'bandpass'; f.frequency.value = 2600; f.Q.value = 1.2;
    const g = c.createGain(); g.gain.setValueAtTime(0.5, t0); g.gain.exponentialRampToValueAtTime(0.0001, t0 + 0.06);
    ns.connect(f); f.connect(g); g.connect(master); ns.start(t0); ns.stop(t0 + 0.08);
    blip(180, 0.07, 'triangle', 0.25);
  }
  function good() { blip(660, 0.12, 'sine', 0.2); blip(990, 0.16, 'sine', 0.2, 0.07); }
  function bad() { blip(220, 0.18, 'sawtooth', 0.12); blip(160, 0.22, 'sawtooth', 0.12, 0.12); }
  function fanfare() { [0, 2, 4, 7].forEach((i, k) => { const n = NOTES[i]; flute(freqOf(n), { dur: k === 3 ? 0.9 : 0.25, when: k * 0.13, vel: 0.9 }); }); }
  function tick(accent) { blip(accent ? 1400 : 1000, 0.05, 'square', accent ? 0.12 : 0.07); }
  function gliss() { NOTES.forEach((n, i) => flute(freqOf(n), { dur: 0.32, when: i * 0.14, vel: 0.9 })); }
  return { unlock, visibility, state, running, tapNote, flute, note, click, good, bad, fanfare, tick, gliss, blip, get ctx() { return ctx; } };
})();
/* 소리 잠금 해제 연결: 누르는 순간에도 시도하고, 손가락을 뗄 때(브라우저가 인정하는 사용자 동작) 확실히 켠다.
   window 캡처 단계에 걸어 두어 관·카드 드래그처럼 전파를 멈추는 요소 위에서도 항상 실행됨 */
for (const t of ['pointerdown', 'touchstart', 'mousedown', 'keydown']) window.addEventListener(t, () => Sound.unlock(false), { capture: true, passive: true });
for (const t of ['pointerup', 'touchend', 'click']) window.addEventListener(t, () => Sound.unlock(true), { capture: true, passive: true });
document.addEventListener('visibilitychange', () => Sound.visibility(document.visibilityState === 'visible'));

/* 버튼 탭(터치): 손가락을 뗀 순간(pointerup)에 바로 눌러 주고, 뒤따라오는 브라우저 click은 잠깐 무시한다.
   - 크롬 계열은 빠른 드래그 직후 0.5초 안의 탭에 click 자체를 보내지 않는 일이 있어, click만 기다리면 버튼이 안 눌린다.
   - pointerup은 브라우저가 인정하는 '사용자 동작'이라 이 안에서 실행되는 소리 켜기도 정상 동작한다.
   - 눌린 직후 화면이 바뀌어 늦게 오는 click이 다른 버튼에 떨어지지 않도록, 짧은 시간 동안 모든 브라우저 click을 막는다. */
(() => {
  const down = new Map(); let quietUntil = 0;
  const btnOf = t => (t && t.closest) ? t.closest('button') : null;
  document.addEventListener('pointerdown', e => {
    if (e.pointerType !== 'touch') return;
    const b = btnOf(e.target); if (b) down.set(e.pointerId, { b, x: e.clientX, y: e.clientY });
  }, true);
  document.addEventListener('pointercancel', e => down.delete(e.pointerId), true);
  document.addEventListener('pointerup', e => {
    if (e.pointerType !== 'touch') return;
    const d = down.get(e.pointerId); down.delete(e.pointerId); if (!d) return;
    const b = d.b;
    if (btnOf(e.target) !== b || b.disabled || !b.isConnected || Math.hypot(e.clientX - d.x, e.clientY - d.y) > 12) return;
    quietUntil = performance.now() + 700;
    b._tapping = true; try { b.click(); } finally { b._tapping = false; }
  }, true);
  document.addEventListener('click', e => {
    if (!e.isTrusted) return;
    const b = btnOf(e.target); if (b && b._tapping) return;
    if (e.target.closest && e.target.closest('select,input,textarea,label,a')) return; /* 입력 요소는 브라우저 기본 동작 그대로 */
    if (performance.now() < quietUntil) { e.stopImmediatePropagation(); e.preventDefault(); }
  }, true);
})();
/* =====================================================================
   DOM / SVG 도우미
   ===================================================================== */
const SVGNS = 'http://www.w3.org/2000/svg';
function el(tag, attrs = {}, parent) {
  const e = document.createElementNS(SVGNS, tag);
  for (const k in attrs) if (attrs[k] != null) e.setAttribute(k, attrs[k]);
  if (parent) parent.appendChild(e);
  return e;
}
function h(tag, attrs = {}, ...children) {
  const e = document.createElement(tag);
  for (const k in attrs) {
    const v = attrs[k]; if (v == null) continue;
    if (k === 'class') e.className = v;
    else if (k === 'html') e.innerHTML = v;
    else if (k === 'style') e.style.cssText = v;
    else if (k.startsWith('on')) e.addEventListener(k.slice(2), v);
    else e.setAttribute(k, v);
  }
  for (const ch of children) if (ch != null) e.append(ch);
  return e;
}
/* 글자. 눕힌 시트(svg._rot)에서는 글자를 반대로 돌려 바로 읽히게 함. center:true면 (x,y)가 글자의 가운데 */
let CUR_SVG = null; /* 가장 최근에 만든 시트 (아직 붙지 않은 요소의 글자 방향 판단용) */
function text(parent, x, y, str, o = {}) {
  const svg = parent.ownerSVGElement || (parent.tagName === 'svg' ? parent : null) || CUR_SVG;
  const rot = o.rot != null ? !!o.rot : !!(svg && svg._rot), size = o.size || 0.9;
  let tx = x, ty = y;
  if (o.center) { if (rot) tx = x - 0.36 * size; else ty = y + 0.36 * size; }
  const t = el('text', { x: tx, y: ty, 'text-anchor': o.anchor || 'middle', 'font-size': size, class: o.cls, 'font-weight': o.weight }, parent);
  if (rot) t.setAttribute('transform', `rotate(90 ${tx} ${ty})`);
  if (o.fill) t.style.fill = o.fill; /* CSS 기본 fill보다 우선하도록 인라인 스타일로 */
  t.textContent = str; return t;
}
function setPos(g, x, y) { g._pos = { x, y }; g.setAttribute('transform', `translate(${x} ${y})`); }
function svgPt(svg, cx, cy) {
  const p = svg.createSVGPoint(); p.x = cx; p.y = cy; const m = (svg._root || svg).getScreenCTM();
  return m ? p.matrixTransform(m.inverse()) : { x: 0, y: 0 };
}
let uid = 0;
/* 모눈종이 시트 : viewBox 단위 = cm. 컨테이너 비율에 맞춰 viewBox를 넓혀 빈 띠가 생기지 않게 함 */
function makeSheet(desk, W, H, opts = {}) {
  const svg = el('svg', { class: 'sheet', viewBox: `0 0 ${W} ${H}`, preserveAspectRatio: 'xMidYMid meet' });
  const pfx = 'p' + (++uid) + '_';
  const defs = el('defs', {}, svg);
  const pg = el('linearGradient', { id: pfx + 'pipe', x1: 0, x2: 1, y1: 0, y2: 0 }, defs);
  [['0', '#DCEDF5'], ['0.22', '#FFFFFF'], ['0.5', '#E4F2F9'], ['0.8', '#CBE3EF'], ['1', '#BBD8E7']].forEach(([o, c]) => el('stop', { offset: o, 'stop-color': c }, pg));
  const sg = el('linearGradient', { id: pfx + 'stopper', x1: 0, x2: 1, y1: 0, y2: 0 }, defs);
  [['0', '#C33A31'], ['0.35', '#EE6A5F'], ['1', '#B8332B']].forEach(([o, c]) => el('stop', { offset: o, 'stop-color': c }, sg));
  const tg = el('linearGradient', { id: pfx + 'tape', x1: 0, x2: 0, y1: 0, y2: 1 }, defs);
  [['0', '#FFE27A'], ['0.5', '#F6CF3B'], ['1', '#E8BC2A']].forEach(([o, c]) => el('stop', { offset: o, 'stop-color': c }, tg));
  const wg = el('linearGradient', { id: pfx + 'wood', x1: 0, x2: 0, y1: 0, y2: 1 }, defs);
  [['0', '#F1E3C8'], ['1', '#D9BF95']].forEach(([o, c]) => el('stop', { offset: o, 'stop-color': c }, wg));
  /* 보드 위 점 격자 (1cm마다 작은 점, 5cm마다 조금 큰 점) — 길이를 재는 눈금 역할은 그대로 */
  const p1 = el('pattern', { id: pfx + 'g1', width: 1, height: 1, patternUnits: 'userSpaceOnUse' }, defs);
  el('circle', { cx: 0.5, cy: 0.5, r: 0.045, fill: '#c7cad5' }, p1);
  const p5 = el('pattern', { id: pfx + 'g5', width: 5, height: 5, patternUnits: 'userSpaceOnUse' }, defs);
  el('rect', { width: 5, height: 5, fill: `url(#${pfx}g1)` }, p5);
  el('circle', { cx: 0.5, cy: 0.5, r: 0.09, fill: '#a5a8b5' }, p5);
  const sh = el('filter', { id: pfx + 'shadow', x: '-20%', y: '-20%', width: '140%', height: '150%' }, defs);
  el('feDropShadow', { dx: 0, dy: 0.25, stdDeviation: 0.25, 'flood-color': '#1c1c1e', 'flood-opacity': 0.28 }, sh);
  const glow = el('filter', { id: pfx + 'glow', x: '-50%', y: '-50%', width: '200%', height: '200%' }, defs);
  el('feGaussianBlur', { stdDeviation: 0.45, result: 'b' }, glow);
  const mg = el('feMerge', {}, glow); el('feMergeNode', { in: 'b' }, mg); el('feMergeNode', { in: 'SourceGraphic' }, mg);
  if (opts.grid !== false) el('rect', { x: -200, y: -200, width: 400, height: 400, fill: `url(#${pfx}g5)` }, svg);
  const root = el('g', {}, svg);
  const rot = !!opts.rotated;
  if (rot) root.setAttribute('transform', `translate(0 ${W}) rotate(-90)`); /* 장면을 왼쪽으로 눕힘: 관 입구가 왼쪽, 마개가 오른쪽 */
  svg._pfx = pfx; svg._root = root; svg._rot = rot; svg._base = rot ? { W: H, H: W } : { W, H }; CUR_SVG = svg;
  svg.setAttribute('viewBox', `0 0 ${svg._base.W} ${svg._base.H}`);
  /* 크롬 계열은 관·카드를 빠르게 끌어다 놓으면 이를 화면 '튕김(fling)'으로 오인해, 0.5초 안에 이어지는 버튼 탭의 click을 보내지 않는다.
     시트 위의 터치는 앱이 직접 처리한다고 알려(preventDefault) 브라우저의 제스처 인식을 끈다 (touch-action:none과 별개) */
  svg.addEventListener('touchstart', e => { if (e.cancelable) e.preventDefault(); }, { passive: false });
  svg.addEventListener('touchmove', e => { if (e.cancelable) e.preventDefault(); }, { passive: false });
  desk.appendChild(svg);
  const fit = () => {
    const r = desk.getBoundingClientRect(); if (!r.width || !r.height) return;
    const { W, H } = svg._base;
    /* opts.reserve(): 책상 위에 떠 있는 요소(버튼 판)가 차지하는 왼쪽/위쪽 띠(px). 장면은 나머지 영역 가운데에 놓고, 모눈은 전체에 깔림 */
    const rv = (opts.reserve && opts.reserve()) || {};
    const L = Math.min(rv.left || 0, r.width * 0.6), T = Math.min(rv.top || 0, r.height * 0.6);
    const aw = r.width - L, ah = r.height - T, s = Math.min(aw / W, ah / H);
    svg.setAttribute('viewBox', `${-(L + (aw - W * s) / 2) / s} ${-(T + (ah - H * s) / 2) / s} ${r.width / s} ${r.height / s}`);
  };
  fit();
  if (window.ResizeObserver) { const ro = new ResizeObserver(fit); ro.observe(desk); svg._ro = ro; }
  svg._fit = fit;
  return svg;
}

/* ---- 관 그림 : 기준점 = 관 윗면 중앙 (0,0) ---- */
function pipeArt(svg, note, cm, o = {}) {
  const pfx = svg._pfx, W = PIPE_W, r = 0.3;
  const g = el('g', { class: 'pipe', 'data-note': note.id });
  el('rect', { class: 'halo', x: -W / 2 - 0.5, y: -0.7, width: W + 1, height: cm + STOP_H + 1.2, rx: 0.9, fill: 'none', stroke: note.hex, 'stroke-width': 0.4 }, g);
  el('rect', { class: 'body', x: -W / 2, y: 0, width: W, height: cm, rx: r, fill: `url(#${pfx}pipe)`, stroke: '#8FBBD1', 'stroke-width': 0.07 }, g);
  el('line', { x1: -W / 2 + 0.34, y1: 0.55, x2: -W / 2 + 0.34, y2: cm - 0.5, stroke: 'rgba(255,255,255,.95)', 'stroke-width': 0.16, 'stroke-linecap': 'round' }, g);
  el('rect', { class: 'glow', x: -W / 2, y: 0, width: W, height: cm, rx: r, fill: note.hex, 'fill-opacity': 0.55 }, g);
  el('ellipse', { cx: 0, cy: 0.02, rx: W / 2, ry: 0.24, fill: '#C4DDE9', stroke: '#8FBBD1', 'stroke-width': 0.06 }, g);
  el('ellipse', { cx: 0, cy: 0.04, rx: W / 2 - 0.3, ry: 0.11, fill: '#7FAABF' }, g);
  const SW = W + 0.55;
  if (o.flush) { /* 마개가 관 안에 끼워진 모습 (길이 비교용: 전체 높이 = 관 길이) */
    el('rect', { x: -W / 2 + 0.1, y: cm - 1.05, width: W - 0.2, height: 1.0, rx: 0.2, fill: `url(#${pfx}stopper)`, stroke: '#A32E27', 'stroke-width': 0.05 }, g);
  } else {
    el('rect', { x: -SW / 2, y: cm - 0.2, width: SW, height: STOP_H, rx: 0.32, fill: `url(#${pfx}stopper)`, stroke: '#A32E27', 'stroke-width': 0.06 }, g);
    el('line', { x1: -SW / 2 + 0.3, y1: cm + 0.15, x2: -SW / 2 + 0.3, y2: cm + STOP_H - 0.5, stroke: 'rgba(255,255,255,.45)', 'stroke-width': 0.12, 'stroke-linecap': 'round' }, g);
  }
  const rot = !!svg._rot, ph = isPhone();
  if (o.cmLabel) {
    const lb = el('g', { class: 'cml', opacity: o.cmLabelHidden ? 0 : 1 }, g);
    text(lb, 0, cm + STOP_H + (rot ? 2.0 : ph ? 0.8 : 0.55), fmt(cm) + 'cm', { size: rot ? 0.95 : ph ? 1.1 : 0.72, cls: 'num', center: true });
  }
  if (o.tag) { /* 관 입구 쪽에 붙은 길이 꼬리표 */
    const tg = el('g', { class: 'tag' }, g);
    if (!rot && ph) { /* 폰: 꼬리표를 크게 */
      el('rect', { x: -2.2, y: -2.5, width: 4.4, height: 1.9, rx: 0.5, fill: '#FFFDF3', stroke: '#C9B98A', 'stroke-width': 0.08 }, tg);
      el('line', { x1: 0, y1: -0.6, x2: 0, y2: -0.1, stroke: '#C9B98A', 'stroke-width': 0.08 }, tg);
      text(tg, 0, -1.55, fmt(cm) + 'cm', { size: 1.2, cls: 'num', fill: '#555a6a', center: true });
    } else if (rot) {
      el('rect', { x: -0.8, y: -4.1, width: 1.6, height: 3.3, rx: 0.35, fill: '#FFFDF3', stroke: '#C9B98A', 'stroke-width': 0.06 }, tg);
      el('line', { x1: 0, y1: -0.8, x2: 0, y2: -0.1, stroke: '#C9B98A', 'stroke-width': 0.06 }, tg);
      text(tg, 0, -2.45, fmt(cm) + 'cm', { size: 0.82, cls: 'num', fill: '#555a6a', center: true });
    } else {
      el('rect', { x: -1.55, y: -1.85, width: 3.1, height: 1.2, rx: 0.35, fill: '#FFFDF3', stroke: '#C9B98A', 'stroke-width': 0.06 }, tg);
      el('line', { x1: 0, y1: -0.65, x2: 0, y2: -0.1, stroke: '#C9B98A', 'stroke-width': 0.06 }, tg);
      text(tg, 0, -1.25, fmt(cm) + 'cm', { size: 0.72, cls: 'num', fill: '#555a6a', center: true });
    }
  }
  if (o.nameLabel) { /* 음이름 스티커 */
    const two = note.id === 'do2', fill = note.darkText ? '#1c1c1e' : '#fff';
    if (rot) {
      const bh = Math.min(3.6, PIPE_GAP * 0.72), bl = two ? bh * 2.4 : bh * 1.25, by = cm + STOP_H + 0.45;
      el('rect', { x: -bh / 2, y: by, width: bh, height: bl, rx: 0.8, fill: note.hex }, g);
      text(g, 0, by + bl / 2, note.name, { size: two ? bh * 0.46 : bh * 0.62, cls: 'disp', center: true, fill });
    } else {
      const bw = PIPE_GAP - 0.3, bh = 2.3, by = cm + STOP_H + 0.35;
      el('rect', { x: -bw / 2, y: by, width: bw, height: bh, rx: 0.6, fill: note.hex }, g);
      text(g, 0, by + bh / 2, two ? '높은도' : note.name, { size: two ? bw * 0.33 : bw * 0.5, cls: 'disp', center: true, fill });
    }
  }
  const hy0 = (ph && o.tag) ? -2.7 : -1.4; /* 꼬리표까지 잡을 수 있게 */
  el('rect', { class: 'hit', x: -PIPE_GAP / 2, y: hy0, width: PIPE_GAP, height: cm + STOP_H + (o.nameLabel ? (rot ? 9 : 4) : 2.6) + (-1.4 - hy0), fill: 'transparent' }, g);
  g._note = note; g._cm = cm;
  return g;
}
/* 관을 잠깐 빛나게 */
function lightPipe(g, ms = 500) {
  g.classList.add('lit'); clearTimeout(g._litT);
  g._litT = setTimeout(() => g.classList.remove('lit'), ms);
}
/* ---- 테이프 (끝이 살짝 찢어진 노란 테이프) ---- */
function tapeArt(svg, x, y, w, hgt) {
  const g = el('g', { class: 'tape' });
  const z = 0.22, d = [`M ${x} ${y}`];
  d.push(`L ${x + w} ${y}`);
  for (let yy = y, i = 0; yy < y + hgt - 0.01; yy += hgt / 4, i++) d.push(`L ${x + w + (i % 2 ? -z : 0)} ${yy + hgt / 8}`);
  d.push(`L ${x + w} ${y + hgt} L ${x} ${y + hgt}`);
  for (let yy = y + hgt, i = 0; yy > y + 0.01; yy -= hgt / 4, i++) d.push(`L ${x + (i % 2 ? z : 0)} ${yy - hgt / 8}`);
  d.push('Z');
  el('path', { d: d.join(' '), fill: `url(#${svg._pfx}tape)`, stroke: '#D9AE1C', 'stroke-width': 0.05, filter: `url(#${svg._pfx}shadow)` }, g);
  el('line', { x1: x + 0.3, y1: y + 0.32, x2: x + w - 0.3, y2: y + 0.32, stroke: 'rgba(255,255,255,.55)', 'stroke-width': 0.12 }, g);
  return g;
}
/* ---- 자 (세로, 위에서 아래로 cm) ---- */
function rulerArt(svg, x, y, len, up = false) {
  /* up=false: y가 0cm(위)이고 아래로 읽음 / up=true: y가 0cm(바닥)이고 위로 읽음 */
  const g = el('g', { class: 'ruler' });
  const y0 = up ? y - len : y;
  el('rect', { x: x - 0.9, y: y0 - 0.5, width: 1.4, height: len + 1.2, rx: 0.2, fill: '#FFFDF3', stroke: '#C9B98A', 'stroke-width': 0.06 }, g);
  for (let i = 0; i <= len; i++) {
    const big = i % 5 === 0, yy = up ? y - i : y + i;
    el('line', { x1: x + 0.5, y1: yy, x2: x + 0.5 - (big ? 0.75 : 0.4), y2: yy, stroke: '#555a6a', 'stroke-width': big ? 0.07 : 0.04 }, g);
    if (big) text(g, x - 0.55, yy, i, { size: 0.55, cls: 'num', anchor: 'middle', fill: '#555a6a', center: true });
  }
  text(g, x - 0.2, y0 - 1.05, 'cm', { size: 0.6, fill: '#8e91a0', cls: 'num', center: true });
  return g;
}
/* ---- 나무 받침 ---- */
function trayArt(svg, x, y, w, hgt, label) {
  const g = el('g', { class: 'tray' });
  el('rect', { x, y, width: w, height: hgt, rx: 0.8, fill: `url(#${svg._pfx}wood)`, stroke: '#CFB283', 'stroke-width': 0.08 }, g);
  el('rect', { x: x + 0.5, y: y + 0.4, width: w - 1, height: 0.25, rx: 0.12, fill: 'rgba(255,255,255,.55)' }, g);
  if (label) text(g, x + w / 2, y + hgt - 0.8, label, { size: 0.8, cls: 'hand', fill: '#555a6a', center: true });
  return g;
}
/* ---- 손글씨 메모 ---- */
function noteArt(svg, x, y, lines, o = {}) {
  const g = el('g', { class: 'memo' });
  if (svg._rot || isPhone()) return g; /* 작은 폰에서는 메모 생략 */
  const w = o.w || 9, lh = o.size ? o.size * 1.25 : 1.15, hgt = lines.length * lh + 1.1;
  el('rect', { x, y, width: w, height: hgt, rx: 0.5, fill: o.fill || '#fff4c4', stroke: 'rgba(5,0,56,.06)', 'stroke-width': 0.05, filter: `url(#${svg._pfx}shadow)`, transform: `rotate(${o.rot ?? -2} ${x + w / 2} ${y + hgt / 2})` }, g);
  lines.forEach((ln, i) => text(g, x + w / 2, y + 1.0 + i * lh, ln, { size: o.size || 0.95, cls: 'hand', fill: '#1c1c1e' }).setAttribute('transform', `rotate(${o.rot ?? -2} ${x + w / 2} ${y + hgt / 2})`));
  return g;
}

/* =====================================================================
   드래그 · 트윈
   ===================================================================== */
function draggable(g, svg, hs = {}) {
  /* 드래그 중 이벤트는 window에서 받는다 (요소를 맨 앞으로 옮기면 포인터 캡처가 풀릴 수 있으므로) */
  let active = false, pid = null, start = null, base = null, sx = 0, sy = 0;
  const move = e => {
    if (!active || e.pointerId !== pid) return;
    e.preventDefault();
    const p = svgPt(svg, e.clientX, e.clientY), nx = base.x + (p.x - start.x), ny = base.y + (p.y - start.y);
    setPos(g, nx, ny); hs.onMove && hs.onMove(p, nx, ny);
  };
  const end = e => {
    if (!active || e.pointerId !== pid) return;
    active = false; g.classList.remove('dragging');
    window.removeEventListener('pointermove', move); window.removeEventListener('pointerup', end); window.removeEventListener('pointercancel', end);
    const p = svgPt(svg, e.clientX, e.clientY);
    hs.onEnd && hs.onEnd(p, Math.hypot(p.x - start.x, p.y - start.y), Math.hypot(e.clientX - sx, e.clientY - sy));
  };
  g.addEventListener('pointerdown', e => {
    if (hs.canStart && !hs.canStart()) { hs.onBlocked && hs.onBlocked(e); return; }
    if (active) return;
    e.preventDefault(); e.stopPropagation();
    active = true; pid = e.pointerId; sx = e.clientX; sy = e.clientY;
    start = svgPt(svg, e.clientX, e.clientY); base = { ...g._pos };
    g.classList.add('dragging'); g.parentNode.appendChild(g);
    window.addEventListener('pointermove', move, { passive: false });
    window.addEventListener('pointerup', end); window.addEventListener('pointercancel', end);
    hs.onStart && hs.onStart(start);
  });
}
const easeOut = k => 1 - Math.pow(1 - k, 3);
const easeBack = k => { const c1 = 1.4, c3 = c1 + 1; return 1 + c3 * Math.pow(k - 1, 3) + c1 * Math.pow(k - 1, 2); };
const easeInOut = k => k < .5 ? 2 * k * k : 1 - Math.pow(-2 * k + 2, 2) / 2;
function tween(ms, fn, ease = easeOut) {
  if (RM) ms = 0;
  return new Promise(res => {
    const t0 = performance.now();
    const step = now => { const k = ms ? Math.min(1, (now - t0) / ms) : 1; fn(ease(k), k); if (k < 1) requestAnimationFrame(step); else res(); };
    requestAnimationFrame(step);
  });
}
function moveTo(g, x, y, ms = 320, ease) { const { x: x0, y: y0 } = g._pos; return tween(ms, e => setPos(g, x0 + (x - x0) * e, y0 + (y - y0) * e), ease); }
function shake(g, ms = 400) { const { x, y } = g._pos; return tween(ms, (e, k) => setPos(g, x + Math.sin(k * Math.PI * 7) * (1 - k) * 0.7, y), k => k); }
const wait = ms => new Promise(r => setTimeout(r, RM ? 0 : ms));

/* =====================================================================
   토스트 · 꽃가루 · 다이얼로그
   ===================================================================== */
const toastEl = document.getElementById('toast'); let toastT = null;
function toast(msg, kind = '', ms = 2200) {
  toastEl.textContent = msg; toastEl.className = 'show ' + kind; clearTimeout(toastT);
  toastT = setTimeout(() => toastEl.classList.remove('show'), ms);
}
const Confetti = (() => {
  const cv = document.getElementById('confetti'), cx = cv.getContext('2d'); let parts = [], running = false;
  function burst(n = 140) {
    if (RM) return;
    cv.width = innerWidth * devicePixelRatio; cv.height = innerHeight * devicePixelRatio; cx.setTransform(devicePixelRatio, 0, 0, devicePixelRatio, 0, 0);
    for (let i = 0; i < n; i++) parts.push({
      x: innerWidth / 2 + (Math.random() - .5) * innerWidth * .5, y: innerHeight * .35, vx: (Math.random() - .5) * 14, vy: -Math.random() * 14 - 4,
      r: 5 + Math.random() * 6, c: NOTES[i % 8].hex, a: Math.random() * Math.PI, va: (Math.random() - .5) * .3, life: 1,
    });
    if (!running) { running = true; requestAnimationFrame(loop); }
  }
  function loop() {
    cx.clearRect(0, 0, innerWidth, innerHeight);
    parts.forEach(p => { p.x += p.vx; p.vy += .42; p.y += p.vy; p.vx *= .985; p.a += p.va; p.life -= .011; cx.save(); cx.globalAlpha = Math.max(0, p.life); cx.translate(p.x, p.y); cx.rotate(p.a); cx.fillStyle = p.c; cx.fillRect(-p.r / 2, -p.r / 3, p.r, p.r / 1.5); cx.restore(); });
    parts = parts.filter(p => p.life > 0 && p.y < innerHeight + 40);
    if (parts.length) requestAnimationFrame(loop); else { running = false; cx.clearRect(0, 0, innerWidth, innerHeight); }
  }
  return { burst };
})();
const dlgInfo = document.getElementById('dlg-info'), infoBody = document.getElementById('info-body');
function showInfo(build) { infoBody.innerHTML = ''; build(infoBody, () => dlgInfo.close()); dlgInfo.showModal(); }
const dlgResult = document.getElementById('dlg-result'), resultBody = document.getElementById('result-body');
function starsFor(score) { return score >= 90 ? 3 : score >= 70 ? 2 : 1; }
function starsEl(n) { const w = h('div', { class: 'stars' }); for (let i = 0; i < 3; i++) { const s = h('span', {}, '★'); if (i < n) { s.style.animationDelay = (0.25 + i * 0.25) + 's'; setTimeout(() => s.classList.add('lit'), 250 + i * 250); } w.append(s); } return w; }

/* =====================================================================
   라우터
   ===================================================================== */
const view = document.getElementById('view');
let cleanup = null, route = null;
const Routes = {};
function go(r) {
  if (cleanup) { try { cleanup(); } catch (e) {} cleanup = null; }
  applyMode();
  view.innerHTML = ''; route = r;
  document.querySelectorAll('.tab').forEach(t => { t.classList.toggle('on', t.dataset.route === r); });
  cleanup = Routes[r](view) || null;
  refreshTabs();
}
function refreshTabs() {
  const t = document.querySelectorAll('.tab');
  t[0].classList.toggle('done', !!S.s1); t[1].classList.toggle('done', !!S.s2);
  t[2].classList.toggle('done', Object.keys(S.best || {}).length > 0);
}
document.querySelectorAll('.tab').forEach(t => t.addEventListener('click', () => go(t.dataset.route)));
let resizeT = null, lastLandscape = innerWidth > innerHeight;
/* 폰↔넓은 화면 모드가 바뀌거나, 폰을 돌려 가로·세로가 바뀌면(눕힌 장면의 줄 간격이 화면 비율에 묶여 있음) 장면을 다시 그림 */
window.addEventListener('resize', () => {
  clearTimeout(resizeT);
  resizeT = setTimeout(() => {
    const land = innerWidth > innerHeight;
    const flipped = computeMode() === 'phone' && land !== lastLandscape && !document.querySelector('dialog[open]'); /* 설정 창의 키보드로 화면이 줄어드는 경우는 제외 */
    if (route && (computeMode() !== MODE || flipped)) go(route);
    lastLandscape = land;
  }, 250);
});
let rotateHinted = false;
function phoneOrientationHint() { if (isPhone() && innerWidth > innerHeight && !rotateHinted) { rotateHinted = true; setTimeout(() => toast('폰을 세로로 돌리면 더 크게 보여요', '', 3200), 600); } }
document.getElementById('brand').addEventListener('click', () => go('home'));
const soundBtn = document.getElementById('btn-sound');
function paintSound() { soundBtn.classList.toggle('off', !S.sound); soundBtn.querySelector('.label').textContent = S.sound ? '소리' : '소리 꺼짐'; soundBtn.querySelectorAll('.w1,.w2').forEach(p => p.style.opacity = S.sound ? 1 : .25); }
soundBtn.addEventListener('click', () => { S.sound = !S.sound; save(); paintSound(); if (S.sound) { Sound.unlock(); Sound.good(); } });
paintSound();
/* 전체 화면 (전자칠판에서 시범할 때) — 지원되는 브라우저에서만 버튼을 보임 */
const fullBtn = document.getElementById('btn-full');
const fsOn = () => !!(document.fullscreenElement || document.webkitFullscreenElement);
const paintFull = () => { fullBtn.querySelector('.label').textContent = fsOn() ? '전체 화면 끄기' : '전체 화면'; fullBtn.setAttribute('aria-label', fsOn() ? '전체 화면 끄기' : '전체 화면'); };
if (document.fullscreenEnabled || document.webkitFullscreenEnabled) {
  fullBtn.hidden = false;
  fullBtn.addEventListener('click', () => {
    const de = document.documentElement;
    try {
      if (fsOn()) (document.exitFullscreen || document.webkitExitFullscreen).call(document);
      else (de.requestFullscreen || de.webkitRequestFullscreen).call(de);
    } catch (e) {}
  });
  document.addEventListener('fullscreenchange', paintFull); document.addEventListener('webkitfullscreenchange', paintFull);
}

/* ---- 선생님 설정 ---- */
const dlgSet = document.getElementById('dlg-settings'), lenGrid = document.getElementById('len-grid');
function fillSettings() {
  lenGrid.innerHTML = '';
  NOTES.forEach((n, i) => lenGrid.append(h('label', {}, h('span', { style: `color:${n.hex}` }, n.name), h('input', { type: 'number', step: '0.05', min: '5', max: '60', value: fmt(S.lengths[i]), 'data-i': i }))));
  document.getElementById('set-tempo').value = S.tempo; document.getElementById('set-hint').value = S.hint;
}
document.getElementById('btn-settings').addEventListener('click', () => { fillSettings(); dlgSet.showModal(); });
document.getElementById('set-video').addEventListener('click', () => { lenGrid.querySelectorAll('input').forEach((inp, i) => inp.value = VIDEO_LENGTHS[i]); });
document.getElementById('set-exact').addEventListener('click', () => { const base = parseFloat(lenGrid.querySelector('input').value) || 25.5; lenGrid.querySelectorAll('input').forEach((inp, i) => inp.value = fmt(Math.round(base / NOTES[i].ratio * 20) / 20)); });
const resetBtn = document.getElementById('set-reset'); let resetArmed = null;
resetBtn.addEventListener('click', () => {
  if (!resetArmed) { resetArmed = setTimeout(() => { resetArmed = null; resetBtn.textContent = '진도·점수 지우기'; }, 4000); resetBtn.textContent = '정말 지울까요? (한 번 더)'; return; }
  clearTimeout(resetArmed); resetArmed = null; resetBtn.textContent = '진도·점수 지우기';
  const L = S.lengths; S = DEFAULTS(); S.lengths = L; save(); refreshTabs(); toast('진도와 점수를 지웠어요', 'ok');
});
function saveSettings() {
  const L = [...lenGrid.querySelectorAll('input')].map(i => parseFloat(i.value));
  if (L.some(v => !(v > 3 && v < 80))) { toast('길이는 3~80cm 사이로 적어 주세요', 'bad'); return; }
  S.lengths = L; S.tempo = document.getElementById('set-tempo').value; S.hint = document.getElementById('set-hint').value; save();
  dlgSet.close(); toast('저장했어요. 화면을 새로 그려요'); go(route || 'home');
}
dlgSet.querySelector('form').addEventListener('submit', e => { e.preventDefault(); saveSettings(); });
/* 자동 점검용 손잡이 */
window.__panflute = { state: () => S, go: r => go(r), mode: () => MODE, audio: () => Sound.state() };

/* =====================================================================
   홈 : 바로 눌러 볼 수 있는 팬플룻 + 3단계 카드
   ===================================================================== */
Routes.home = root => {
  const phone = isPhone();
  const wrap = h('div', { class: 'home' });
  const hero = h('div', { class: 'hero' },
    h('div', {},
      h('h1', { html: '<span class="u">관의 길이</span>가 소리를 정해요' }),
      h('p', { class: 'sub' }, '빨대 팬플룻을 만들고, 소리의 비밀을 찾고, 연주해 봐요')));
  const desk = h('div', { class: 'desk' });
  const fluteWrap = h('div', { class: 'home-flute' }, desk, h('div', { class: 'hint' }, phone ? '관을 눌러 소리를 들어 보세요' : '관을 눌러 소리를 들어 보세요. 어느 관이 가장 낮은 소리일까요?'));
  const best3 = Object.values(S.best || {});
  const cards = h('div', { class: 'cards' },
    card('s1', '1단계', '팬플룻 만들기', '관의 길이를 보고 긴 관부터 차례대로 끼워 팬플룻을 완성해요.', S.s1 ? ['done', '완성'] : null),
    card('s2', '2단계', '길이와 소리 연결하기', '어느 관이 도일까? 음이름 카드를 알맞은 관에 붙여요.', S.s2 ? ['done', '완성'] : null),
    card('s3', '3단계', '학교종이 땡땡땡 연주', '내 팬플룻으로 노래를 연주하고 점수를 받아요.', best3.length ? ['best', '최고 ' + Math.max(...best3) + '점'] : null));
  wrap.append(hero, fluteWrap, cards);
  root.append(wrap);

  /* 홈 팬플룻 (폰도 세로) */
  let W, H, top, X0; const EX = extraCm();
  if (phone) { X0 = 2.5; top = 3.2; W = X0 + 7 * PIPE_GAP + 2.5; H = 32 + EX; } /* 폰: 자 없이 세로 관만 */
  else { W = 34; H = 32 + EX; top = 3.2; X0 = 4.6; }
  const svg = makeSheet(desk, W, H, {}); const R = svg._root;
  if (!phone) R.append(rulerArt(svg, 2.1, top, 27 + Math.ceil(EX)));
  const pipes = NOTES.map((n, i) => {
    const g = pipeArt(svg, n, cmOf(n), { cmLabel: true }); setPos(g, X0 + i * PIPE_GAP, top); R.append(g);
    g.addEventListener('pointerdown', e => { e.preventDefault(); Sound.tapNote(n, { dur: 0.7 }); lightPipe(g, 600); ripple(g); });
    return g;
  });
  R.append(tapeArt(svg, X0 - 1.6, top + 1.0, 7 * PIPE_GAP + 3.2, 1.6));
  R.append(tapeArt(svg, X0 - 1.4, top + 8.2, 7 * PIPE_GAP + 2.8, 1.1));
  /* 넓은 화면이면 양옆 빈 곳에 재료·원리 메모 */
  const memos = el('g', {}, R);
  const paintMemos = () => {
    memos.innerHTML = '';
    if (phone) return;
    const vb = svg.getAttribute('viewBox').split(' ').map(Number);
    if (vb[2] - W < 14) return;
    memos.append(noteArt(svg, vb[0] + 1.6, 10.5, ['만드는 재료', '긴 빨대 4개 → 8개로 자르기', '마개 8개 · 테이프 · 가위'], { w: 10.8, size: 0.85, rot: -3 }));
    memos.append(noteArt(svg, W + (vb[2] - W) / 2 - 12.2, 12, ['긴 관은 낮은 소리,', '짧은 관은 높은 소리!', '왜 그럴까요?'], { w: 10.4, size: 0.9, rot: 2, fill: '#c3faf5' }));
  };
  paintMemos();
  const roMemo = window.ResizeObserver ? new ResizeObserver(paintMemos) : null; roMemo && roMemo.observe(desk);
  function ripple(g) {
    const { x, y } = g._pos; const c = el('circle', { cx: x, cy: y, r: 0.6, fill: 'none', stroke: g._note.hex, 'stroke-width': 0.25 }, R);
    tween(600, e => { c.setAttribute('r', 0.6 + e * 3); c.setAttribute('stroke-opacity', 1 - e); }).then(() => c.remove());
  }
  function card(route, step, title, desc, badge) {
    const c = h('button', { class: 'card ' + route, onclick: () => go(route) },
      h('span', { class: 'step' }, step), h('h3', {}, title), h('p', {}, desc));
    if (badge) c.append(h('span', { class: 'badge ' + badge[0] }, badge[1]));
    return c;
  }
  phoneOrientationHint();
  return () => { svg._ro && svg._ro.disconnect(); roMemo && roMemo.disconnect(); };
};

/* =====================================================================
   1단계 : 관의 길이를 보고 팬플룻 완성하기
   ===================================================================== */
Routes.s1 = root => {
  const phone = isPhone();
  const msg = h('div', { class: 'msg' });
  const prog = h('span', { class: 'chip' }, h('b', {}, '0'), ' / 8');
  let hintOn = false;
  const hintBtn = h('button', { class: 'btn secondary sm', onclick: () => { hintOn = !hintOn; slots.forEach(s => s.hint.setAttribute('opacity', hintOn && !s.filled ? 1 : 0)); hintBtn.textContent = hintOn ? '힌트 끄기' : '힌트'; } }, '힌트');
  const resetBtn = h('button', { class: 'btn secondary sm', onclick: () => go('s1') }, '처음부터');
  const nextBtn = h('button', { class: 'btn tape sm', hidden: '', onclick: () => go('s2') }, '2단계로 →');
  const bar = h('div', { class: 'stage-bar' }, phone ? null : h('h2', {}, '1단계 · 팬플룻 만들기'), msg, h('div', { class: 'bar-btns' }, prog, hintBtn, resetBtn, nextBtn));
  const desk = h('div', { class: 'desk' });
  root.append(h('div', { class: 'stage s1' }, bar, h('div', { class: 'stage-body' }, desk)));
  msg.innerHTML = phone
    ? '<b>긴 관부터 짧은 관</b>까지 차례대로 위쪽 틀에 끌어다 끼워요.'
    : '관의 <b>길이</b>를 잘 보고, <b>긴 관부터 짧은 관</b>까지 차례대로 틀에 끼워요. 관을 끌어서 옮겨 보세요.';

  /* ---- 배치 ---- */
  const rc = desk.getBoundingClientRect();
  let L; const EX = extraCm(); /* 기준보다 긴 관이면 장면을 아래로 늘림 */
  if (phone) {
    /* 폰: 패드·PC와 같은 세로 배치(위 틀, 아래 받침). 자는 생략하고 그만큼 관을 크게 */
    const FX0 = 2.3, Wp = FX0 + 7 * PIPE_GAP + 2.3;
    L = { W: Wp, H: 64 + 2 * EX, rulerX: null, FX0, top: 2.2, trayX: 0.6, trayW: Wp - 1.2, trayTop: 61 + 2 * EX, TX0: FX0, g2: PIPE_GAP };
  } else {
    const landscape = rc.width / Math.max(1, rc.height) >= 1.15;
    L = landscape
      ? { W: 63, H: 32 + EX, rulerX: 3.4, FX0: 6.0, top: 2.2, trayX: 34.0, trayW: 28.4, trayTop: 28.6 + EX, TX0: 35.9, memoX: 37, memoY: 5, g2: PIPE_GAP }
      : { W: 36, H: 60 + 2 * EX, rulerX: 2.6, FX0: 5.4, top: 2.2, trayX: 3.6, trayW: 28.8, trayTop: 57.0 + 2 * EX, TX0: 5.7, memoX: 10, memoY: 37 + EX, g2: PIPE_GAP };
  }
  const svg = makeSheet(desk, L.W, L.H, {}); const R = svg._root;
  const Lslots = el('g', {}, R), Lpipes = el('g', {}, R), Ltape = el('g', {}, R), Lfx = el('g', {}, R);
  if (L.rulerX != null) R.insertBefore(rulerArt(svg, L.rulerX, L.top, 27 + Math.ceil(EX)), Lslots);
  if (!phone) R.insertBefore(noteArt(svg, L.FX0 + 4.55 * PIPE_GAP, L.top + 20.6, ['긴 관 → 짧은 관', '순서대로 끼워요'], { w: 7.6, size: 0.78, rot: -2 }), Lslots);

  /* 자리(슬롯) */
  const slots = NOTES.map((n, i) => {
    const cm = cmOf(n), x = L.FX0 + i * PIPE_GAP;
    const g = el('g', { class: 'slot' }, Lslots);
    const rect = el('rect', { x: x - PIPE_W / 2 - 0.22, y: L.top - 0.25, width: PIPE_W + 0.44, height: cm + STOP_H + 0.25, rx: 0.5, fill: 'rgba(255,255,255,.7)', stroke: '#8e91a0', 'stroke-width': 0.09, 'stroke-dasharray': '0.5 0.32' }, g);
    const hint = text(g, x, L.top + cm + STOP_H + (phone ? 1.2 : 0.8), fmt(cm) + 'cm', { size: phone ? 1.2 : 0.72, cls: 'num hint', fill: '#555a6a', center: true }); hint.setAttribute('opacity', 0);
    return { g, rect, note: n, x, cm, filled: false, hint };
  });
  /* 테이프 (윗부분) */
  const tapeX = L.FX0 - PIPE_GAP * 0.62, tapeW = 7 * PIPE_GAP + PIPE_GAP * 1.24;
  Ltape.append(tapeArt(svg, tapeX, L.top + 1.0, tapeW, 1.6));
  /* 받침과 뒤섞인 관 */
  Lslots.append(trayArt(svg, L.trayX, L.trayTop, L.trayW, 2.5, phone ? '' : '뒤섞인 관'));
  let order; do { order = NOTES.map((_, i) => i).sort(() => Math.random() - .5); } while (order.every((v, i) => v === i));
  let filled = 0, done = false;
  const pipes = order.map((ni, k) => {
    const n = NOTES[ni], cm = cmOf(n);
    const g = pipeArt(svg, n, cm, { tag: true, cmLabel: true, cmLabelHidden: true });
    const hx = L.TX0 + k * L.g2, hy = L.trayTop - (cm + STOP_H - 0.2);
    g._home = { x: hx, y: hy }; g._locked = false; setPos(g, hx, hy); Lpipes.append(g);
    draggable(g, svg, {
      canStart: () => !g._locked && !done,
      onBlocked: () => { Sound.tapNote(n, { dur: 0.7 }); lightPipe(g, 600); },
      onStart: () => { slots.forEach(s => s.g.classList.remove('hot')); },
      onMove: (p, nx, ny) => {
        const s = nearSlot(nx, ny);
        slots.forEach(sl => sl.g.classList.toggle('hot', sl === s && !sl.filled));
      },
      onEnd: async (p, moved, px) => {
        slots.forEach(s => s.g.classList.remove('hot'));
        if (px < 10) { Sound.tapNote(n, { dur: 0.7 }); lightPipe(g, 600); await moveTo(g, g._home.x, g._home.y, 200); return; } /* 살짝 누르기만 한 것 */
        const s = nearSlot(g._pos.x, g._pos.y);
        if (!s) { await moveTo(g, g._home.x, g._home.y, 360); return; }
        if (s.filled) { toast('이 자리에는 벌써 관이 있어요', 'bad'); await moveTo(g, g._home.x, g._home.y, 360); return; }
        if (s.note === n) await snap(g, s); else await wrong(g, s);
      },
    });
    return g;
  });
  function nearSlot(x, y) {
    if (y > L.top + 9 || y < L.top - 6) return null;
    let best = null, bd = PIPE_GAP * 0.52;
    for (const s of slots) { const d = Math.abs(s.x - x); if (d < bd) { bd = d; best = s; } }
    return best;
  }
  async function snap(g, s) {
    g._locked = true; s.filled = true; filled++;
    Sound.click();
    await moveTo(g, s.x, L.top, 260, easeBack);
    s.rect.setAttribute('opacity', 0); s.hint.setAttribute('opacity', 0);
    g.querySelector('.tag').setAttribute('opacity', 0); g.querySelector('.cml').setAttribute('opacity', 1);
    Sound.note(s.note, { dur: 0.6 }); lightPipe(g, 500);
    prog.querySelector('b').textContent = filled;
    if (filled === 4) msg.innerHTML = '<b>절반 완성!</b> 남은 관도 길이를 비교하며 끼워요.';
    else if (filled === 7) msg.innerHTML = '하나만 더! <b>마지막 관</b>을 끼워요.';
    if (filled === 8) await complete();
  }
  async function wrong(g, s) {
    Sound.bad();
    const longer = g._cm > s.cm;
    const dir = longer ? '더 왼쪽' : '더 오른쪽';
    toast(`${fmt(g._cm)}cm 관은 이 자리보다 ${longer ? '길어요' : '짧아요'}. ${dir} 자리를 찾아봐요!`, 'bad', 2600);
    await shake(g, 380);
    await moveTo(g, g._home.x, g._home.y, 420);
  }
  async function complete() { /* 여덟 관을 길이에 맞게 다 끼우면 바로 축하 (테이프 감기 연출 없음) */
    done = true;
    Sound.gliss();
    pipes.forEach((g, i) => setTimeout(() => lightPipe(g, 500), i * 90));
    await wait(500);
    Sound.fanfare(); Confetti.burst();
    S.s1 = true; save(); refreshTabs();
    msg.innerHTML = '<b>팬플룻 완성! 관을 길이에 맞게 모두 잘 연결했어요.</b> 관을 눌러 소리를 들어 보고, 다음 단계로 가요.';
    nextBtn.hidden = false;
    if (!phone) Lfx.append(noteArt(svg, L.memoX, L.memoY, ['팬플룻 완성!', '긴 관과 짧은 관,', '소리가 어떻게 다를까요?'], { w: 13, size: 1.0, rot: 2 }));
    toast('팬플룻 완성! 길이에 맞게 잘 연결했어요', 'ok', 3000);
  }
  return () => { svg._ro && svg._ro.disconnect(); };
};

/* =====================================================================
   분수 표시 (초등 표기: 가로줄 위 분자, 아래 분모)
   ===================================================================== */
function fracEl(a, b, cls) { return h('span', { class: 'frac' + (cls ? ' ' + cls : '') }, h('span', { class: 'fn' }, String(a)), h('span', { class: 'fd' }, String(b))); }

/* =====================================================================
   수학적 원리 설명 (2단계 완료 후) : 그림 + 두 줄
   ===================================================================== */
function principleFigure() {
  /* 도 관과 높은 도 관 두 개만: 길이 절반 = 같은 이름의 높은 소리 */
  const s = el('svg', { viewBox: '0 0 100 54', class: 'fig', 'aria-label': '도 관과 높은 도 관 길이 비교' });
  const d = el('defs', {}, s);
  const pg = el('linearGradient', { id: 'pf_pipe', x1: 0, x2: 1, y1: 0, y2: 0 }, d);
  [['0', '#DCEDF5'], ['0.25', '#FFFFFF'], ['0.8', '#CBE3EF'], ['1', '#BBD8E7']].forEach(([o, c]) => el('stop', { offset: o, 'stop-color': c }, pg));
  const doCm = cmOf(NOTES[0]), hiCm = cmOf(NOTES[7]), k = 32 / doCm, top = 5, w = 8;
  const T = (x, y, str, size, fill, anchor = 'middle', cls = 'disp') => { const t = el('text', { x, y, 'font-size': size, 'text-anchor': anchor, class: cls }, s); t.textContent = str; t.style.fill = fill; return t; };
  const pipe = (x, cm, note) => {
    const hh = cm * k;
    el('rect', { x: x - w / 2, y: top, width: w, height: hh, rx: 2, fill: 'url(#pf_pipe)', stroke: '#8FBBD1', 'stroke-width': 0.4 }, s);
    el('rect', { x: x - w / 2 - 0.8, y: top + hh - 0.8, width: w + 1.6, height: 3.6, rx: 1.1, fill: '#D9453B' }, s);
    T(x, top + hh + 8.2, note.name, 5.2, note.hex);
    T(x, top + hh + 12.6, fmt(cm) + 'cm', 3.4, '#555a6a', 'middle', 'num');
  };
  pipe(24, doCm, NOTES[0]);
  pipe(62, hiCm, NOTES[7]);
  /* 절반 점선과 괄호, 가로줄 분수 1/2 — 실제 관은 정확히 절반이 아니므로 '약 절반'이라고 씀 */
  const half = top + doCm * k / 2;
  el('line', { x1: 14, y1: half, x2: 72, y2: half, stroke: '#1c1c1e', 'stroke-width': 0.5, 'stroke-dasharray': '1.6 1.1' }, s);
  el('line', { x1: 36, y1: top, x2: 36, y2: half, stroke: '#1c1c1e', 'stroke-width': 0.6 }, s);
  el('line', { x1: 34.5, y1: top, x2: 37.5, y2: top, stroke: '#1c1c1e', 'stroke-width': 0.6 }, s);
  el('line', { x1: 34.5, y1: half, x2: 37.5, y2: half, stroke: '#1c1c1e', 'stroke-width': 0.6 }, s);
  const fy = (top + half) / 2;
  T(46, fy - 2.2, '약 절반', 4.2, '#1c1c1e', 'middle', 'hand');
  T(46, fy + 2.6, '1', 3.4, '#1c1c1e', 'middle', 'num');
  el('line', { x1: 44.2, y1: fy + 3.5, x2: 47.8, y2: fy + 3.5, stroke: '#1c1c1e', 'stroke-width': 0.5 }, s);
  T(46, fy + 7.2, '2', 3.4, '#1c1c1e', 'middle', 'num');
  /* 소리 높낮이 */
  T(24, top - 1.4, '낮은 소리', 3.6, '#4262ff');
  T(62, top - 1.4, '높은 소리', 3.6, '#E5533C');
  el('path', { d: 'M 76 22 L 94 22', stroke: '#1c1c1e', 'stroke-width': 0.6 }, s);
  el('path', { d: 'M 92 19.5 L 95.5 22 L 92 24.5 Z', fill: '#1c1c1e' }, s);
  T(85, 19.5, '길이 약 절반', 3.2, '#1c1c1e');
  T(85, 28, '같은 이름의', 3.1, '#555a6a');
  T(85, 32.2, '높은 소리', 3.1, '#555a6a');
  return s;
}
function showPrinciple(onNext) {
  showInfo((box, close) => {
    const ic = (node, bg) => h('span', { class: 'ic', style: `background:${bg}` }, node);
    box.append(...[
      h('h2', {}, '수학적 원리를 더 알아볼까요?'),
      h('div', { class: 'fig-wrap' }, principleFigure()),
      h('div', { class: 'rules' },
        h('div', { class: 'rule' }, ic('1', '#4262ff'), h('span', { html: '관이 <b>길면 낮은 소리</b>, <b>짧으면 높은 소리</b>가 나요.' })),
        /* 실제 길이(25.5cm·13cm)는 정확히 2배가 아니므로 반드시 '약'을 붙여 말함 */
        h('div', { class: 'rule' }, ic(fracEl(1, 2, 'ic-frac'), '#E5533C'),
          h('span', {}, h('b', {}, '도 관'), `(${fmt(cmOf(NOTES[0]))}cm)은 `, h('b', {}, '높은 도 관'), `(${fmt(cmOf(NOTES[7]))}cm)보다 `, h('b', {}, '약 2배'), ' 길어요. 관을 ', h('b', {}, '약 절반('), fracEl(1, 2), h('b', {}, ')'), '으로 자르면 ', h('b', {}, '같은 이름의 높은 소리'), '가 나요.'))),
      h('div', { class: 'who' }, '2500년 전 수학자 피타고라스가 찾아낸 규칙이에요'),
      h('div', { class: 'row' },
        h('button', { class: 'btn secondary', onclick: close }, '닫기'),
        onNext ? h('button', { class: 'btn tape', onclick: () => { close(); onNext(); } }, '3단계로 가기 →') : null)].filter(Boolean));
  });
}

/* =====================================================================
   2단계 : 관의 길이와 음이름 연결하기
   ===================================================================== */
Routes.s2 = root => {
  const phone = isPhone();
  const msg = h('div', { class: 'msg' });
  const actions = h('div', { class: 'bar-btns' });
  const bar = h('div', { class: 'stage-bar' }, phone ? null : h('h2', {}, '2단계 · 길이와 소리 연결하기'), msg, actions);
  const body = h('div', { class: 'stage-body' });
  root.append(h('div', { class: 'stage s2' }, bar, body));
  return matchView();

  /* ---------- 음이름 카드 붙이기 ---------- */
  function matchView() {
    msg.innerHTML = phone
      ? '관을 눌러 소리를 들어 보고, <b>음이름 카드</b>를 알맞은 관 아래에 끌어다 붙여요.'
      : '관을 눌러 소리를 들어 보고, <b>음이름 카드</b>를 알맞은 관에 끌어다 붙여요. 긴 관과 짧은 관, 어느 쪽이 낮은 소리일까요?';
    const checkBtn = h('button', { class: 'btn sm', disabled: '', onclick: check }, '확인하기');
    const hintBtn = h('button', { class: 'btn secondary sm', onclick: () => toast('가장 긴 관이 가장 낮은 소리 "도"예요. 그다음은 레, 미, 파… 순서대로!', '', 3200) }, '힌트');
    const whyBtn = h('button', { class: 'btn secondary sm', hidden: '', onclick: () => showPrinciple(() => go('s3')) }, '원리 다시 보기');
    const nextBtn = h('button', { class: 'btn tape sm', hidden: '', onclick: () => go('s3') }, '3단계로 →');
    actions.append(hintBtn, checkBtn, whyBtn, nextBtn);
    const desk = h('div', { class: 'desk' });
    body.append(desk);

    /* 카드 크기 (장면 cm). 눕힌 장면에서는 (가로=CH, 세로=CW)로 보임 */
    let W, H, top, X0, CW, CH, trayY; const EX = extraCm(); /* 기준보다 긴 관이면 받침을 아래로 내림 */
    if (phone) { /* 폰: 세로 관, 자 없이. 가장 긴 관(25.5cm)에 붙인 카드 끝(≈32.9)이 카드 받침(trayY)과 겹치지 않게 */
      X0 = 2.4; top = 2.4; CW = 3.9; CH = 3.0; trayY = 34.8 + EX; W = X0 + 7 * PIPE_GAP + 2.4; H = trayY + 2 * CH + 2.6 + 0.8;
    } else {
      W = 34; top = 2.4; X0 = 4.6; CW = 3.4; CH = 2.7; trayY = 32.6 + EX; H = trayY + 2 * CH + 2.6 + 0.8;
    }
    const svg = makeSheet(desk, W, H, {}); const R = svg._root;
    const Lback = el('g', {}, R), Lpipes = el('g', {}, R), Ltape = el('g', {}, R), Lcards = el('g', {}, R);
    if (!phone) Lback.append(rulerArt(svg, 2.1, top, 27 + Math.ceil(EX)));
    const pipes = NOTES.map((n, i) => {
      const g = pipeArt(svg, n, cmOf(n), {}); setPos(g, X0 + i * PIPE_GAP, top); Lpipes.append(g);
      g.addEventListener('pointerdown', e => { e.preventDefault(); tapPipe(g); });
      g._card = null; return g;
    });
    Ltape.append(tapeArt(svg, X0 - PIPE_GAP * 0.55, top + 1.0, 7 * PIPE_GAP + PIPE_GAP * 1.1, 1.6));
    Ltape.append(tapeArt(svg, X0 - PIPE_GAP * 0.48, top + 8.2, 7 * PIPE_GAP + PIPE_GAP * 0.96, 1.1));
    function tapPipe(g) { Sound.tapNote(g._note, { dur: 0.8 }); lightPipe(g, 700); }

    /* 카드 받침 : 4장씩 두 줄 */
    let order; do { order = NOTES.map((_, i) => i).sort(() => Math.random() - .5); } while (order.every((v, i) => v === i));
    let homeOf;
    {
      const gapX = phone ? 0.8 : 0.7, rowW = 4 * CW + 3 * gapX, x0 = (W - rowW) / 2 + CW / 2, plateH = 2 * CH + 2.6;
      Lback.append(trayArt(svg, 0.8, trayY, W - 1.6, plateH, ''));
      text(Lback, W / 2, trayY - 0.95, '음이름 카드를 알맞은 관 아래에 붙여요', { size: phone ? 1.15 : 0.95, cls: 'hand', fill: '#555a6a', center: true });
      homeOf = k => ({ x: x0 + (k % 4) * (CW + gapX), y: trayY + 0.9 + CH / 2 + Math.floor(k / 4) * (CH + 0.8) });
    }
    const cards = order.map((ni, k) => {
      const n = NOTES[ni], two = n.id === 'do2';
      const g = el('g', { class: 'card-note' }, Lcards);
      el('rect', { x: -CW / 2, y: -CH / 2, width: CW, height: CH, rx: 0.6, fill: n.hex, filter: `url(#${svg._pfx}shadow)` }, g);
      text(g, 0, 0, two ? '높은도' : n.name, { size: two ? CW * 0.32 : CW * 0.5, cls: 'disp', center: true, fill: n.darkText ? '#1c1c1e' : '#fff' });
      const chk = text(g, CW / 2 - 0.6, -CH / 2 + 0.6, '✓', { size: 0.75, cls: 'disp', center: true, fill: n.darkText ? '#1c1c1e' : '#fff' }); chk.setAttribute('opacity', 0);
      g._chk = chk; g._note = n; g._pipe = null; g._locked = false;
      const hm = homeOf(k); g._home = hm; setPos(g, hm.x, hm.y);
      draggable(g, svg, {
        canStart: () => !g._locked,
        onBlocked: () => { if (g._pipe) tapPipe(g._pipe); },
        onEnd: async (p, moved, px) => {
          if (px < 10) { await shake(g, 250); return; }
          const tgt = nearPipe(g._pos.x, g._pos.y);
          if (!tgt) { await returnHome(g); return; }
          if (tgt._card && tgt._card !== g) { const old = tgt._card; detach(old); returnHome(old); }
          attach(g, tgt);
          Sound.click();
          await moveTo(g, tgt._pos.x, top + tgt._cm + STOP_H + 0.5 + CH / 2, 240, easeBack);
          updateCheck();
        },
      });
      return g;
    });
    function nearPipe(x, y) {
      if (y < top - 3 || y > trayY - 0.5) return null;
      let best = null, bd = PIPE_GAP * 0.52;
      for (const g of pipes) { const d = Math.abs(g._pos.x - x); if (d < bd) { bd = d; best = g; } }
      return best;
    }
    function attach(card, pipe) { if (card._pipe) card._pipe._card = null; card._pipe = pipe; pipe._card = card; }
    function detach(card) { if (card._pipe) card._pipe._card = null; card._pipe = null; }
    async function returnHome(card) { detach(card); await moveTo(card, card._home.x, card._home.y, 360); updateCheck(); }
    function updateCheck() { const placed = cards.filter(c => c._pipe).length; checkBtn.disabled = placed < 8; if (placed === 8) msg.innerHTML = '카드를 모두 붙였어요! <b>확인하기</b>를 눌러요.'; }
    async function check() {
      const wrong = cards.filter(c => c._pipe && c._pipe._note !== c._note);
      cards.forEach(c => { if (c._pipe && c._pipe._note === c._note && !c._locked) { c._locked = true; c.classList.add('locked'); c._chk.setAttribute('opacity', 1); } });
      if (wrong.length) {
        Sound.bad();
        msg.innerHTML = `<b>${8 - wrong.length}개</b>는 맞았어요! 남은 ${wrong.length}개는 다시 생각해 봐요.`;
        toast(wrong.length >= 4 ? '긴 관은 낮은 소리, 짧은 관은 높은 소리라는 걸 떠올려 봐요' : '거의 다 맞았어요! 다시 한번', 'bad', 2600);
        await Promise.all(wrong.map(c => shake(c, 380)));
        await Promise.all(wrong.map(c => returnHome(c)));
        return;
      }
      Sound.fanfare(); Confetti.burst();
      pipes.forEach((g, i) => setTimeout(() => { lightPipe(g, 600); }, i * 90));
      S.s2 = true; save(); refreshTabs();
      checkBtn.hidden = true; hintBtn.hidden = true; whyBtn.hidden = false; nextBtn.hidden = false;
      msg.innerHTML = '<b>모두 맞았어요! 축하해요.</b> 가장 긴 관이 도, 가장 짧은 관이 높은 도예요. 이제 3단계에서 연주해 봐요!';
      setTimeout(() => showPrinciple(() => go('s3')), 900);
    }
    return () => { svg._ro && svg._ro.disconnect(); };
  }
};

/* =====================================================================
   3단계 : 팬플룻으로 노래 연주하기 (점수 · 재도전)
   ===================================================================== */
const SONGS = [
  { id: 'school', title: '학교종이 땡땡땡', bpm: { slow: 66, normal: 84, fast: 100 },
    notes: [['sol',1],['sol',1],['la',1],['la',1],['sol',1],['sol',1],['mi',2], ['sol',1],['sol',1],['mi',1],['mi',1],['re',4],
            ['sol',1],['sol',1],['la',1],['la',1],['sol',1],['sol',1],['mi',2], ['sol',1],['mi',1],['re',1],['mi',1],['do',4]] },
  { id: 'star', title: '작은 별', bpm: { slow: 72, normal: 92, fast: 110 },
    notes: [['do',1],['do',1],['sol',1],['sol',1],['la',1],['la',1],['sol',2], ['fa',1],['fa',1],['mi',1],['mi',1],['re',1],['re',1],['do',2],
            ['sol',1],['sol',1],['fa',1],['fa',1],['mi',1],['mi',1],['re',2], ['sol',1],['sol',1],['fa',1],['fa',1],['mi',1],['mi',1],['re',2],
            ['do',1],['do',1],['sol',1],['sol',1],['la',1],['la',1],['sol',2], ['fa',1],['fa',1],['mi',1],['mi',1],['re',1],['re',1],['do',2]] },
  { id: 'plane', title: '비행기', bpm: { slow: 72, normal: 92, fast: 110 },
    notes: [['mi',1],['re',1],['do',1],['re',1],['mi',1],['mi',1],['mi',2], ['re',1],['re',1],['re',2],['mi',1],['mi',1],['mi',2],
            ['mi',1],['re',1],['do',1],['re',1],['mi',1],['mi',1],['mi',2], ['re',1],['re',1],['mi',1],['re',1],['do',4]] },
];
const MODE_NAME = { slow: '천천히 도전', rhythm: '박자 도전' };

Routes.s3 = root => {
  const phone = isPhone();
  let song = SONGS[0], mode = 'idle';
  const idleMsg = s => phone ? `<b>${s.title}</b> · 연주 방법을 골라요.` : `<b>${s.title}</b> · 연주 방법을 골라요. 천천히 도전은 반짝이는 관을 차례대로, 박자 도전은 내려오는 음표가 관에 닿을 때 눌러요.`;
  const songChips = h('div', { class: 'song-chips' }, ...SONGS.map(s => h('button', { class: 'song-chip' + (s === song ? ' on' : ''), 'data-id': s.id, onclick: () => { if (mode !== 'idle') stopGame(); song = s; songChips.querySelectorAll('.song-chip').forEach(b => b.classList.toggle('on', b.dataset.id === s.id)); buildMelody(); msg.innerHTML = idleMsg(s); } }, s.title)));
  const msg = h('div', { class: 'msg' });
  const desk = h('div', { class: 'desk' });
  const countEl = h('div', { class: 'count' });
  const scoreEl = h('span', { class: 'score' }, '0점'); const progEl = h('span', { class: 'prog' }, '');
  const hud = { score: t => { scoreEl.textContent = t; }, prog: t => { progEl.textContent = t; } };
  /* 연주 방법 버튼 : 팬플룻 책상의 왼쪽 위에 떠 있는 판 (넓은 화면 2×2 / 좁은 세로 화면은 위쪽 띠 / 낮은 화면은 세로 한 줄) */
  const btnFree = h('button', { class: 'btn secondary sm', onclick: () => startFree() }, phone ? '연습' : '연습하기');
  const btnListen = h('button', { class: 'btn secondary sm', onclick: () => toggleListen() }, phone ? '듣기' : '노래 듣기');
  const btnSlow = h('button', { class: 'btn sm', onclick: () => startSlow() }, '천천히 도전');
  const btnRhythm = h('button', { class: 'btn sm rhythm', onclick: () => startRhythm() }, '박자 도전');
  const btnStop = h('button', { class: 'btn secondary sm stop', hidden: '', onclick: () => stopGame(true) }, '그만하기');
  const modeBox = h('div', { class: 'mode-float' }, btnFree, btnListen, btnSlow, btnRhythm, btnStop);
  const hudFloat = h('div', { class: 'hud-float', hidden: '' }, scoreEl, progEl);
  const melody = h('div', { class: 'melody strip' });
  const deskWrap = h('div', { class: 'desk-wrap' }, desk, modeBox, hudFloat, countEl);
  const stageEl = h('div', { class: 'stage s3' },
    phone ? h('div', { class: 'stage-bar' }, msg) : h('div', { class: 'stage-bar' }, h('h2', {}, '3단계 · 연주하기'), songChips, msg),
    phone ? h('div', { class: 'row-scroll song-row' }, songChips) : null,
    deskWrap, melody);
  root.append(stageEl);
  msg.innerHTML = idleMsg(song);

  /* ---- 버튼 판이 차지할 자리 정하기 : 팬플룻이 가장 크게 보이는 배치를 고름 ---- */
  const EX = extraCm(); /* 기준보다 긴 관이면 장면을 아래로 늘림 */
  /* 장면 크기 (폰도 세로 관: 자 없이 관만, 폰 폭에 맞춘 치수) */
  let W, H, top, X0;
  if (phone) { X0 = 2.8; top = 9.5; W = X0 + 7 * PIPE_GAP + 2.8; H = 41 + EX; } /* 양 끝 음이름 스티커(폭 4.4)가 잘리지 않게 여백 확보 */
  else { W = 34; H = 41 + EX; top = 9.5; X0 = 4.6; }
  const PAD = 16; /* 판과 장면 사이 여백(px) */
  const size = {}; /* 판 크기 측정 (2×2 / 세로 한 줄). 도전 중에는 2×2의 아랫줄이 '그만하기' 하나로 바뀌어 높이가 같음 */
  function measure() { /* 항상 '대기 상태'(버튼 4개) 기준으로 재서, 도전 중에 배치가 바뀌지 않게 */
    const st = modeBox.classList.contains('stack'), hid = [btnSlow.hidden, btnRhythm.hidden, btnStop.hidden];
    btnSlow.hidden = false; btnRhythm.hidden = false; btnStop.hidden = true;
    modeBox.classList.remove('stack'); size.gw = modeBox.offsetWidth; size.gh = modeBox.offsetHeight;
    modeBox.classList.add('stack'); size.sw = modeBox.offsetWidth; size.sh = modeBox.offsetHeight;
    modeBox.classList.toggle('stack', st); [btnSlow.hidden, btnRhythm.hidden, btnStop.hidden] = hid;
  }
  function pickLayout(r) {
    if (!size.gw) measure();
    const cands = phone
      ? [['grid-top', 0, size.gh + PAD], ['stack-left', size.sw + PAD, 0]]
      : [['grid-left', size.gw + PAD, 0], ['stack-left', size.sw + PAD, 0], ['grid-top', 0, size.gh + PAD]];
    const bw = W, bh = H;
    let best = null;
    for (const [name, L, T] of cands) {
      const s = Math.min(Math.max(1, r.width - L) / bw, Math.max(1, r.height - T) / bh);
      if (!best || s > best.s + 1e-6) best = { name, L, T, s };
    }
    modeBox.classList.toggle('stack', best.name === 'stack-left');
    modeBox.classList.toggle('top', best.name === 'grid-top');
    /* 판이 위쪽 띠면 점수 판도 그 띠의 오른쪽에, 판이 왼쪽이면 점수 판은 오른쪽 아래('다음 음' 표시와 겹치지 않게) */
    deskWrap.classList.toggle('lay-left', best.name !== 'grid-top');
    return best;
  }
  const reserve = () => { const b = pickLayout(desk.getBoundingClientRect()); return { left: b.L, top: b.T }; };

  /* ---- 팬플룻 ---- */
  const LEAD = 2.1;
  const svg = makeSheet(desk, W, H, { reserve }); const R = svg._root;
  let fontsT = 0; /* 글꼴이 늦게 실려 판 크기가 바뀌면 한 번 다시 재서 맞춤 */
  if (document.fonts && document.fonts.ready) document.fonts.ready.then(() => { fontsT = setTimeout(() => { if (!svg.isConnected) return; measure(); svg._fit && svg._fit(); }, 60); }).catch(() => {});
  const Lback = el('g', {}, R), Lnotes = el('g', {}, R), Lpipes = el('g', {}, R), Ltape = el('g', {}, R);
  /* 착지선 */
  el('line', { x1: X0 - PIPE_GAP * 0.8, y1: top, x2: X0 + 7 * PIPE_GAP + PIPE_GAP * 0.8, y2: top, stroke: '#1c1c1e', 'stroke-width': 0.1, 'stroke-dasharray': '0.5 0.35', opacity: 0.35 }, Lback);
  const pipes = NOTES.map((n, i) => {
    const g = pipeArt(svg, n, cmOf(n), { nameLabel: true }); setPos(g, X0 + i * PIPE_GAP, top); Lpipes.append(g);
    g.addEventListener('pointerdown', e => { e.preventDefault(); onTap(g); });
    return g;
  });
  const pipeOf = id => pipes.find(p => p._note.id === id);
  /* 천천히 도전용 '다음 음' 표시 */
  const marker = el('g', { class: 'fnote', opacity: 0 }, Lback);
  const markerIn = el('g', { class: 'arrow-bob' }, marker); /* 위치는 바깥 g, 통통 튀는 애니메이션은 안쪽 g */
  const mk = phone ? 1.25 : 1;
  el('path', { d: `M ${-0.9 * mk} ${-2.4 * mk} L ${0.9 * mk} ${-2.4 * mk} L 0 -0.9 Z`, fill: '#1c1c1e' }, markerIn);
  text(markerIn, 0, phone ? -4.1 : -3.3, '여기!', { size: 1.0 * mk, cls: 'hand', fill: '#1c1c1e', center: true });
  const nextLbl = el('g', { class: 'fnote', opacity: 0 }, Lback);
  let nextTxt;
  { /* 관 위쪽 가운데 '다음 음' 상자 */
    const cx = X0 + 3.5 * PIPE_GAP, bw = phone ? 15 : 14, bh = phone ? 3.3 : 3.0;
    el('rect', { x: cx - bw / 2, y: top - 8.9, width: bw, height: bh, rx: 1.5, fill: '#fff', stroke: '#1c1c1e', 'stroke-width': 0.1 }, nextLbl);
    nextTxt = text(nextLbl, cx, top - 8.9 + bh / 2, '', { size: phone ? 2.0 : 1.8, cls: 'disp', center: true });
  }
  function showNext(note, g) {
    if (!note) { marker.setAttribute('opacity', 0); nextLbl.setAttribute('opacity', 0); return; }
    marker.setAttribute('opacity', 1); marker.setAttribute('transform', `translate(${g._pos.x} ${top})`);
    nextLbl.setAttribute('opacity', 1); nextTxt.textContent = `다음 음 : ${note.name}`; nextTxt.style.fill = note.darkText ? '#B58A00' : note.hex;
  }
  Ltape.append(tapeArt(svg, X0 - PIPE_GAP * 0.55, top + 1.0, 7 * PIPE_GAP + PIPE_GAP * 1.1, 1.6));
  Ltape.append(tapeArt(svg, X0 - PIPE_GAP * 0.48, top + 8.2, 7 * PIPE_GAP + PIPE_GAP * 0.96, 1.1));

  /* ---- 음이름 순서 띠 (책상 바로 아래, 화면을 내리지 않아도 보임) ---- */
  let chips = [];
  function buildMelody() {
    melody.innerHTML = ''; chips = []; let beat = 0;
    song.notes.forEach(([id, b], i) => {
      const n = NOTE_BY_ID[id];
      const c = h('div', { class: 'mnote ' + id + (b >= 2 ? ' long' : ''), style: `background:${n.hex};${n.darkText ? 'color:#1c1c1e' : ''}` }, id === 'do2' ? '높은도' : n.name);
      melody.append(c); chips.push(c); beat += b;
      if (beat % 4 === 0 && i < song.notes.length - 1) melody.append(h('span', { class: 'bar-sep' }));
    });
    layoutMelody();
  }
  /* 넓은 화면: 노래 전체가 한 줄에 들어가면 가운데 정렬, 두 줄이면 줄바꿈해서 다 보이게, 그보다 길면 한 줄로 가로 스크롤(현재 음을 가운데로) */
  function layoutMelody() {
    const avail = melody.clientWidth - 22; if (avail <= 0) return;
    const firstChip = chips.find(c => !c.classList.contains('long'));
    const sz = (firstChip && firstChip.offsetWidth) || (phone ? 46 : 54); let total = 0, beat = 0;
    song.notes.forEach(([id, b], i) => { total += (b >= 2 ? sz * 1.3 : sz) + (i ? 5 : 0); beat += b; if (beat % 4 === 0 && i < song.notes.length - 1) total += 10; });
    const budget = deskWrap.offsetHeight + melody.offsetHeight; /* 책상 + 띠 높이 합 (줄 수와 무관하게 일정) */
    const twoRows = sz * 2 + 6 + 14;
    const wrap = !phone && total > avail && total <= avail * 2.1 && budget - twoRows - 8 >= 340;
    melody.classList.toggle('center', total <= avail);
    melody.querySelectorAll('.row-break').forEach(e => e.remove());
    if (wrap) { /* 두 줄로 나눌 때는 노래의 가운데에 가장 가까운 마디 끝에서 줄을 바꿈 */
      let acc = 0, bestSep = null, bestD = Infinity;
      for (const it of melody.children) {
        acc += (it.classList.contains('bar-sep') ? 10 : it.classList.contains('long') ? sz * 1.3 : sz) + 5;
        if (it.classList.contains('bar-sep')) { const d = Math.abs(acc - total / 2); if (d < bestD) { bestD = d; bestSep = it; } }
      }
      if (bestSep) bestSep.after(h('span', { class: 'row-break' }));
    }
    melody.classList.toggle('wrap', wrap);
    if (wrap && melody.scrollHeight > twoRows + 8) { melody.classList.remove('wrap'); melody.querySelectorAll('.row-break').forEach(e => e.remove()); } /* 실제로 세 줄이 되면 한 줄 스크롤로 */
    if (!melody.classList.contains('wrap')) { const cur = chips.findIndex(c => c.classList.contains('cur')); if (cur >= 0) focusChip(cur); }
  }
  buildMelody();
  const roMelody = window.ResizeObserver ? new ResizeObserver(layoutMelody) : null; roMelody && roMelody.observe(stageEl);
  function bestKey(m) { return `${song.id}:${m}`; }
  const beatDur = () => 60 / song.bpm[S.tempo || 'normal'];
  const nowS = () => performance.now() / 1000;

  /* ---- 공통 상태 ---- */
  let timers = [], raf = 0, game = null;
  function clearTimers() { timers.forEach(t => clearTimeout(t)); timers = []; if (raf) cancelAnimationFrame(raf); raf = 0; }
  function setMode(m) {
    mode = m; const playing = m !== 'idle', challenge = m === 'slow' || m === 'rhythm';
    /* 도전 중에는 두 도전 버튼 자리에 '그만하기'가 들어가 판 크기가 그대로 유지됨 */
    btnSlow.hidden = challenge; btnRhythm.hidden = challenge; btnStop.hidden = !challenge;
    [btnFree, btnListen, btnSlow, btnRhythm].forEach(b => b.disabled = playing && m !== 'free');
    if (m === 'free') btnFree.disabled = true;
    hudFloat.hidden = !challenge;
    pipes.forEach(p => p.classList.remove('target'));
    if (m !== 'slow') showNext(null);
    if (!playing) { chips.forEach(c => c.className = c.className.replace(/ (cur|done)/g, '')); Lnotes.innerHTML = ''; }
  }
  function stopGame(byUser) {
    clearTimers(); Lnotes.innerHTML = ''; game = null; setMode('idle');
    hud.score('0점'); hud.prog('');
    if (byUser) msg.innerHTML = `<b>${song.title}</b> · 다시 연주 방법을 골라요.`;
  }
  function playPipe(g, dur = 0.7, byTap = false) { (byTap ? Sound.tapNote : Sound.note)(g._note, { dur }); lightPipe(g, Math.min(900, dur * 1000 + 250)); }
  function judgeText(g, txt, color) {
    const r = g.querySelector('.body').getBoundingClientRect(), d = desk.getBoundingClientRect();
    const e = h('div', { class: 'judge', style: `left:${r.left + r.width / 2 - d.left}px;top:${r.top - d.top - 10}px;color:${color}` }, txt);
    desk.append(e); setTimeout(() => e.remove(), 800);
  }
  function setScore(pts, max) { const sc = max ? Math.round(pts / max * 100) : 0; hud.score(sc + '점'); return sc; }
  function focusChip(i) { /* 한 줄 스크롤 띠일 때 현재 음을 가운데로 (가로만 움직임) */
    const c = chips[i]; if (!c || melody.classList.contains('wrap') || melody.classList.contains('center')) return;
    const left = c.offsetLeft - melody.clientWidth / 2 + c.offsetWidth / 2;
    if (melody.scrollTo) melody.scrollTo({ left: Math.max(0, left), behavior: RM ? 'auto' : 'smooth' }); else melody.scrollLeft = Math.max(0, left);
  }

  /* ---- 연습하기 ---- */
  function startFree() { stopGame(); setMode('free'); msg.innerHTML = '<b>연습 시간!</b> 관을 마음껏 눌러 봐요.'; chips.forEach(c => c.classList.remove('done', 'cur')); }

  /* ---- 노래 듣기 ---- */
  let listening = false;
  function toggleListen() {
    if (listening) { stopGame(); listening = false; btnListen.textContent = phone ? '듣기' : '노래 듣기'; return; }
    stopGame(); setMode('listen'); listening = true; btnListen.disabled = false; btnListen.textContent = '멈추기';
    msg.innerHTML = `<b>${song.title}</b>를 들려 드릴게요. 어떤 관이 빛나는지 잘 봐요.`;
    let t = 0.4; const bd = beatDur();
    song.notes.forEach(([id, b], i) => {
      timers.push(setTimeout(() => { const g = pipeOf(id); playPipe(g, b * bd * 0.92); chips.forEach((c, k) => { c.classList.toggle('cur', k === i); c.classList.toggle('done', k < i); }); focusChip(i); }, t * 1000));
      t += b * bd;
    });
    timers.push(setTimeout(() => { listening = false; btnListen.textContent = phone ? '듣기' : '노래 듣기'; stopGame(); msg.innerHTML = '잘 들었나요? 이번엔 직접 연주해 봐요!'; }, (t + 0.6) * 1000));
  }

  /* ---- 천천히 도전 ---- */
  function startSlow() {
    stopGame(); setMode('slow');
    game = { kind: 'slow', k: 0, pts: 0, max: song.notes.length * 4, wrongHere: 0, mistakes: 0 };
    msg.innerHTML = '<b>천천히 도전!</b> \'다음 음\'을 보고 알맞은 관을 차례대로 눌러요. 박자는 신경 쓰지 않아도 돼요.';
    setScore(0, game.max); hud.prog(`0 / ${song.notes.length}`);
    nextSlow();
  }
  function nextSlow() {
    clearTimers();
    chips.forEach((c, i) => { c.classList.toggle('cur', i === game.k); c.classList.toggle('done', i < game.k); });
    pipes.forEach(p => p.classList.remove('target'));
    if (game.k >= song.notes.length) { showNext(null); finish(); return; }
    focusChip(game.k);
    const id = song.notes[game.k][0], g = pipeOf(id);
    showNext(NOTE_BY_ID[id], g);
    const hint = S.hint || 'now';
    if (hint === 'now') g.classList.add('target');
    else if (hint === 'late') timers.push(setTimeout(() => { if (game && game.kind === 'slow' && song.notes[game.k] && song.notes[game.k][0] === id) g.classList.add('target'); }, 3000));
  }

  /* ---- 박자 도전 ---- */
  function startRhythm() {
    stopGame(); setMode('rhythm');
    const bd = beatDur(); let t = 4 * bd + 0.3; const notes = [];
    song.notes.forEach(([id, b], i) => { notes.push({ id, b, t, i, judged: false, el: null }); t += b * bd; });
    game = { kind: 'rhythm', notes, pts: 0, max: notes.length * 4, done: 0, t0: nowS(), end: t + 1.0, beat: -5, bd };
    setScore(0, game.max); hud.prog(`0 / ${notes.length}`);
    msg.innerHTML = phone ? '<b>박자 도전!</b> 내려오는 음표가 점선에 닿는 순간 그 관을 눌러요. 준비…' : '<b>박자 도전!</b> 음표가 관 입구의 점선에 닿는 순간 그 관을 눌러요. 준비…';
    countEl.textContent = '';
    raf = requestAnimationFrame(loopRhythm);
  }
  function loopRhythm() {
    if (!game || game.kind !== 'rhythm') return;
    const t = nowS() - game.t0, bd = game.bd, speed = (top + 3.5) / LEAD;
    const beatIdx = Math.floor((t - 0.3) / bd) - 4;
    if (beatIdx > game.beat) {
      game.beat = beatIdx;
      if (beatIdx >= -4) {
        const inSong = beatIdx >= 0; Sound.tick(!inSong || beatIdx % 4 === 0);
        if (!inSong) { const label = ['하나', '둘', '셋', '넷'][beatIdx + 4]; if (label) { countEl.textContent = label; countEl.classList.remove('go'); void countEl.offsetWidth; countEl.classList.add('go'); } }
        if (beatIdx === 0) { countEl.textContent = '시작!'; countEl.classList.remove('go'); void countEl.offsetWidth; countEl.classList.add('go'); msg.innerHTML = '<b>박자 도전!</b> 점선에 닿을 때 눌러요!'; }
      }
    }
    const rr = phone ? Math.min(2.1, PIPE_GAP * 0.42) : 1.5;
    for (const n of game.notes) {
      const dt = n.t - t;
      if (!n.el && dt <= LEAD) {
        const note = NOTE_BY_ID[n.id], g = el('g', { class: 'fnote' }, Lnotes), x = pipeOf(n.id)._pos.x;
        const tail = (n.b - 1) * bd * speed * 0.8;
        if (tail > 0.3) el('rect', { x: x - rr * 0.4, y: -tail, width: rr * 0.8, height: tail, rx: rr * 0.4, fill: note.hex, 'fill-opacity': 0.35 }, g);
        el('circle', { cx: x, cy: 0, r: rr, fill: note.hex, stroke: '#fff', 'stroke-width': 0.14, filter: `url(#${svg._pfx}shadow)` }, g);
        text(g, x, 0, n.id === 'do2' ? '높은도' : note.name, { size: n.id === 'do2' ? rr * 0.55 : rr * 0.9, cls: 'disp', center: true, fill: note.darkText ? '#1c1c1e' : '#fff' });
        n.el = g;
      }
      if (n.el && !n.gone) {
        const y = top - dt * speed;
        n.el.setAttribute('transform', `translate(0 ${y})`);
        if (n.judged) { const k = Math.min(1, (t - n.judgedAt) / 0.3); n.el.setAttribute('opacity', 1 - k); n.el.querySelector('circle').setAttribute('r', rr + k * 1.2); if (k >= 1) { n.el.remove(); n.gone = true; } }
        else if (dt < -0.5) { n.judged = true; n.judgedAt = t; n.result = 'miss'; game.done++; judgeText(pipeOf(n.id), '놓쳤어요', '#8e91a0'); hud.prog(`${game.done} / ${game.notes.length}`); }
        else if (y > top + 3) { n.el.setAttribute('opacity', Math.max(0, 1 - (y - top - 3) / 3)); }
      }
    }
    if (t > game.end) { finish(); return; }
    raf = requestAnimationFrame(loopRhythm);
  }

  /* ---- 관을 눌렀을 때 ---- */
  function onTap(g) {
    if (mode === 'idle' || mode === 'free' || mode === 'listen') { playPipe(g, 0.7, true); return; }
    if (!game) return;
    if (game.kind === 'slow') {
      const want = song.notes[game.k]; if (!want) return;
      if (g._note.id === want[0]) {
        playPipe(g, Math.min(1.6, want[1] * beatDur() * 0.9), true);
        game.pts += Math.max(0, 4 - game.wrongHere); game.wrongHere = 0; game.k++;
        setScore(game.pts, game.max); hud.prog(`${game.k} / ${song.notes.length}`);
        if (game.k % 7 === 0 && game.k < song.notes.length) judgeText(g, '잘하고 있어요', '#00b473');
        nextSlow();
      } else {
        playPipe(g, 0.4, true); game.wrongHere++; game.mistakes++;
        judgeText(g, '다시!', '#600000'); Sound.bad();
        pipeOf(want[0]).classList.add('target');
      }
      return;
    }
    if (game.kind === 'rhythm') {
      const t = nowS() - game.t0; let best = null, bd_ = 0.5;
      for (const n of game.notes) { if (n.judged || n.id !== g._note.id) continue; const d = Math.abs(n.t - t); if (d < bd_) { bd_ = d; best = n; } }
      if (!best) { playPipe(g, 0.35, true); return; }
      best.judged = true; best.judgedAt = t; game.done++;
      const d = bd_; let pts, txt, col;
      if (d <= 0.17) { pts = 4; txt = '완벽!'; col = '#0fbcb0'; } else if (d <= 0.36) { pts = 2; txt = '좋아요'; col = '#4262ff'; } else { pts = 1; txt = '조금 늦었어요'; col = '#fcb900'; if (best.t > t) txt = '조금 빨랐어요'; }
      game.pts += pts; playPipe(g, Math.min(1.6, best.b * game.bd * 0.9), true); judgeText(g, txt, col);
      setScore(game.pts, game.max); hud.prog(`${game.done} / ${game.notes.length}`);
    }
  }

  /* ---- 끝 · 결과 ---- */
  function finish() {
    clearTimers(); const kind = game.kind, sc = setScore(game.pts, game.max); const key = bestKey(kind);
    const prevBest = S.best[key]; const isNew = prevBest == null || sc > prevBest;
    if (isNew) S.best[key] = sc; save(); refreshTabs();
    const stars = starsFor(sc);
    if (stars === 3) { Sound.fanfare(); Confetti.burst(160); } else Sound.good();
    pipes.forEach(p => p.classList.remove('target'));
    const msgs = { 3: '와, 정말 멋진 연주였어요!', 2: '좋아요! 조금만 더 연습하면 완벽해요.', 1: '끝까지 연주했어요! 다시 도전해 볼까요?' };
    resultBody.innerHTML = '';
    const again = h('button', { class: 'btn tape', onclick: () => { dlgResult.close(); kind === 'slow' ? startSlow() : startRhythm(); } }, '다시 도전');
    const other = h('button', { class: 'btn secondary', onclick: () => { dlgResult.close(); kind === 'slow' ? startRhythm() : startSlow(); } }, kind === 'slow' ? '박자 도전 해보기' : '천천히 도전 해보기');
    const closeB = h('button', { class: 'btn secondary', onclick: () => { dlgResult.close(); stopGame(); msg.innerHTML = `<b>${song.title}</b> · 다른 노래나 방법도 골라 봐요.`; } }, '그만하기');
    resultBody.append(...[
      h('h2', {}, `${song.title} · ${MODE_NAME[kind]}`),
      starsEl(stars),
      h('div', { class: 'score', html: `${sc}<small>점</small>` }),
      h('p', {}, msgs[stars] + (isNew && prevBest != null ? ' 새 기록이에요!' : isNew ? ' 첫 기록을 남겼어요!' : ` 최고 기록은 ${prevBest}점이에요.`)),
      kind === 'slow' && game.mistakes ? h('p', {}, `틀린 횟수 ${game.mistakes}번`) : null,
      h('div', { class: 'row' }, again, other, closeB)].filter(Boolean));
    dlgResult.showModal();
    game = null; setMode('idle');
  }

  return () => { clearTimers(); clearTimeout(fontsT); svg._ro && svg._ro.disconnect(); roMelody && roMelody.disconnect(); if (dlgResult.open) dlgResult.close(); };
};

/* =====================================================================
   시작
   ===================================================================== */
go('home');
window.addEventListener('keydown', e => {
  if (e.key === 'Escape' && route !== 'home' && !document.querySelector('dialog[open]')) go('home');
});
})();
</script>

</body>
</html>
