<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>유닛 RANK 분석 — 데모 & 화면 설계서</title>
<style>
:root{
  --color-bg:#ffffff;
  --color-bg-secondary:#f8f8f7;
  --color-bg-tertiary:#f7f9f3;
  --color-text-primary:#1a1a18;
  --color-text-secondary:#6b6b66;
  --color-text-muted:#9a9a94;
  --color-border:rgba(0,0,0,0.08);
  --color-border-strong:rgba(0,0,0,0.14);
  --color-accent:#7bb932;
  --color-accent-dark:#5d9422;
  --color-accent-deep:#436c16;
  --color-accent-bg:#f3f9ea;
  --color-accent-bg-strong:#e4f2cf;
}
*{box-sizing:border-box;}
body{font-family:-apple-system,BlinkMacSystemFont,"Malgun Gothic","맑은 고딕",sans-serif;background:var(--color-bg-tertiary);color:var(--color-text-primary);margin:0;padding:32px;}
.tabs{max-width:1280px;margin:0 auto 20px;display:flex;gap:4px;background:var(--color-accent-bg);border:1px solid var(--color-accent-bg-strong);border-radius:10px;padding:6px;}
.tab{padding:8px 18px;border:none;background:transparent;cursor:pointer;font-size:14px;color:var(--color-text-secondary);border-radius:7px;transition:all .15s;}
.tab:not(.tab--active):hover{color:var(--color-accent-dark);font-weight:600;}
.tab--active:hover{color:var(--color-accent-dark);}
.tab--active{color:var(--color-accent-dark);font-weight:600;background:var(--color-bg);box-shadow:0 1px 3px rgba(0,0,0,0.08);}
.panel{display:none;}
.panel--active{display:block;}
.spec{display:flex;flex-direction:row-reverse;gap:28px;align-items:flex-start;max-width:1280px;margin:0 auto;}
.spec__legend{width:340px;flex-shrink:0;background:#fff;border:1px solid #e5e7eb;border-radius:12px;padding:20px;position:sticky;top:20px;max-height:calc(100vh - 40px);overflow-y:auto;}
.spec__legend h2{font-size:15px;font-weight:600;margin:0 0 14px;}
.spec-table{width:100%;border-collapse:collapse;}
.spec-table th,.spec-table td{border:1px solid #e5e7eb;padding:8px 10px;font-size:13px;vertical-align:top;text-align:left;}
.spec-table th{background:#f3f4f6;font-weight:600;}
.spec-table td:first-child,.spec-table th:first-child{width:44px;text-align:center;}
.num-cell{display:inline-flex;align-items:center;justify-content:center;min-width:22px;height:22px;padding:0 5px;border-radius:11px;background:var(--color-accent-dark);color:#fff;font-size:11px;font-weight:700;white-space:nowrap;}
.sub-row{display:flex;gap:8px;align-items:flex-start;margin-top:8px;padding:8px 10px;background:var(--color-bg-secondary);border-left:2px solid var(--color-accent-bg-strong);font-size:12px;color:#4b5563;}
.spec__screen{flex:1;min-width:0;overflow:visible;}
.spec-num{position:absolute;min-width:22px;height:22px;padding:0 5px;border-radius:11px;background:var(--color-accent-dark);color:#fff;font-size:11px;font-weight:700;display:flex;align-items:center;justify-content:center;box-shadow:0 0 0 2px #fff;white-space:nowrap;pointer-events:none;}
.spec-num-alt{position:absolute;min-width:22px;height:22px;padding:0 5px;border-radius:11px;background:#2563eb;color:#fff;font-size:11px;font-weight:700;display:flex;align-items:center;justify-content:center;box-shadow:0 0 0 2px #fff;white-space:nowrap;pointer-events:none;}
.marker-host{position:relative;overflow:visible;}
*{box-sizing:border-box;}
body{font-family:-apple-system,BlinkMacSystemFont,"Malgun Gothic","맑은 고딕",sans-serif;background:#f5f6f8;color:#111827;margin:0;padding:32px;}
.dash{background:var(--color-bg-tertiary);border-radius:12px;padding:20px;border:.5px solid rgba(0,0,0,0.12);max-width:1280px;margin:0 auto;}
.dash-hd{display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:10px;margin-bottom:14px;}
.dash-title{font-size:15px;font-weight:600;color:var(--color-text-primary);margin:0 0 2px;}
.dash-sub{font-size:11px;color:var(--color-text-muted);margin:0;}
.dash-r{display:flex;gap:8px;align-items:center;}
.kpi-sel{height:28px;padding:0 10px;border:.5px solid var(--color-border-strong);border-radius:7px;font-size:11px;font-weight:500;color:var(--color-text-primary);background:var(--color-bg);cursor:pointer;outline:none;}
.kpi-sel:focus{border-color:var(--color-accent);}

/* 기본 단가 버튼 */
.base-wrap{position:relative;}
.base-btn{font-size:11px;padding:7px 12px;border-radius:20px;background:#fffbeb;color:#92400e;border:.5px solid #fde68a;cursor:pointer;display:inline-flex;align-items:center;gap:5px;white-space:nowrap;position:relative;}
.base-btn:hover{background:#fef3c7;}
.base-ic{display:none;font-size:12px;color:#92400e;}
.base-btn:hover .base-ic{display:inline;}
.base-btn.active .base-ic{display:inline;}
.base-btn.active{background:#fef3c7;}
.bep{display:none;position:absolute;top:calc(100% + 8px);left:0;z-index:20;background:var(--color-bg);border:.5px solid var(--color-border-strong);border-radius:10px;padding:14px 16px;width:230px;box-shadow:0 4px 16px rgba(0,0,0,.1);}
.bep.open{display:block;}
.bep-title{font-size:12px;font-weight:600;color:var(--color-text-primary);margin:0 0 10px;}
.bep-row{display:flex;align-items:center;gap:8px;margin-bottom:8px;overflow:hidden;}
.bep-lbl{font-size:11px;color:var(--color-text-secondary);width:72px;flex-shrink:0;}
.bep-inp{width:80px;flex-shrink:1;min-width:0;height:30px;padding:0 8px;border:.5px solid rgba(0,0,0,.14);border-radius:6px;font-size:12px;color:var(--color-text-primary);}
.bep-inp::-webkit-outer-spin-button,.bep-inp::-webkit-inner-spin-button{-webkit-appearance:auto;opacity:1;}
.bep-inp:focus{outline:none;border-color:#7bb932;}
.bep-unit{font-size:11px;color:var(--color-text-muted);flex-shrink:0;}
.bep-foot{display:flex;gap:6px;justify-content:flex-end;margin-top:10px;border-top:.5px solid rgba(0,0,0,.08);padding-top:10px;}
.ttip-mock{background:#fff;border:1px solid rgba(0,0,0,.1);border-radius:8px;padding:10px;width:220px;box-shadow:0 4px 16px rgba(0,0,0,.08);}
.ttip-mock-title{font-size:11px;font-weight:600;color:var(--color-text-primary);margin:0 0 6px;}
.ttip-mock-row{display:flex;align-items:center;justify-content:space-between;padding:2px 0;}
.ttip-mock-l{display:flex;align-items:center;gap:5px;font-size:13px;font-weight:600;color:var(--color-text-secondary);}
.ttip-dot{width:7px;height:7px;border-radius:50%;flex-shrink:0;}
.ttip-mock-v{font-size:13px;font-weight:600;}
.bep-cancel{padding:4px 12px;font-size:11px;border:.5px solid rgba(0,0,0,.14);border-radius:6px;background:transparent;color:var(--color-text-secondary);cursor:pointer;}
.bep-save{padding:4px 12px;font-size:11px;font-weight:500;border:none;border-radius:6px;background:#1a1a18;color:#fff;cursor:pointer;}

/* 구간 버튼 */
.seg-btns{display:flex;gap:3px;background:var(--color-bg);border:.5px solid var(--color-border-strong);border-radius:8px;padding:3px;}
.seg-btn{padding:4px 12px;font-size:11px;font-weight:500;border:none;border-radius:5px;cursor:pointer;background:transparent;color:var(--color-text-secondary);transition:all .12s;}
.seg-btn:hover{background:#f3f4f6;}
.seg-btn.on{background:#1a1a18;color:#fff;}

/* 차트 */
.charts-g{display:grid;grid-template-columns:1fr 1fr;gap:14px;}
.chart-card{background:var(--color-bg);border:.5px solid var(--color-border-strong);border-radius:12px 12px 0 0;padding:14px 18px;}
.chart-hd{display:flex;align-items:center;justify-content:space-between;margin-bottom:8px;}
.chart-title{font-size:12px;font-weight:600;color:var(--color-text-primary);}
.lgnd{display:flex;flex-wrap:wrap;gap:7px;font-size:10px;color:var(--color-text-secondary);}
.lgnd-item{display:flex;align-items:center;gap:3px;}
.lbar{width:8px;height:8px;border-radius:2px;}
.lline{width:12px;height:2px;}
.ldash{width:12px;height:0;}
.chart-area{position:relative;width:100%;height:185px;}
.chart-area canvas{cursor:pointer;}

/* 구간 넘버 */
.sn{flex:1;min-width:0;padding:3px 1px;border-radius:3px;text-align:center;font-size:9px;font-weight:500;color:#185FA5;background:#eff6ff;border:.5px solid #bfdbfe;cursor:pointer;transition:all .12s;}
.sn:hover{background:#dbeafe;}
.sn.on{background:#1a1a18;color:#fff;border-color:var(--color-text-primary);}

/* 요약 바 */
.sum-bar{background:var(--color-bg);border:.5px solid var(--color-border-strong);border-top:none;border-radius:0 0 12px 12px;overflow:hidden;}
.bar-empty{padding:14px 18px;display:flex;align-items:center;justify-content:center;gap:8px;min-height:56px;}
.bar-empty p{font-size:12px;color:var(--color-text-secondary);margin:0;}
.bar-sel{display:none;padding:12px 18px;}
.sum-top{display:flex;align-items:center;justify-content:space-between;margin-bottom:10px;}
.sum-tl{display:flex;align-items:center;gap:6px;}
.sbadge{font-size:10px;font-weight:700;padding:1px 7px;border-radius:20px;background:var(--color-accent-bg);color:var(--color-accent-deep);border:.5px solid #e4f2cf;}
.srange{font-size:11px;font-weight:500;color:var(--color-text-primary);}
.sunits{font-size:11px;color:var(--color-text-secondary);}
.cx{background:none;border:.5px solid rgba(0,0,0,.14);border-radius:8px;cursor:pointer;font-size:12px;font-weight:500;color:var(--color-text-secondary);line-height:1;padding:6px 20px;}
.cx:hover{background:#f3f4f6;}
.cpc-row{display:grid;grid-template-columns:1fr 1fr auto;gap:8px;align-items:center;margin-bottom:10px;}
.cbox{background:var(--color-bg-tertiary);border-radius:8px;padding:7px 12px;}
.clbl{font-size:9px;color:var(--color-text-muted);margin:0 0 2px;}
.cval{font-size:15px;font-weight:500;color:var(--color-text-primary);margin:0;}
.cval.bl{color:#185FA5;}
.rc{display:flex;align-items:center;gap:8px;background:var(--color-bg-tertiary);border-radius:8px;padding:8px 10px;}
.rb{width:36px;height:36px;border:.5px solid rgba(0,0,0,.14);border-radius:6px;background:#fff;font-size:18px;cursor:pointer;display:flex;align-items:center;justify-content:center;flex-shrink:0;color:var(--color-text-primary);}
.rw{position:relative;}
.ri{width:84px;height:36px;font-size:14px;padding:0 22px 0 10px;border:.5px solid rgba(0,0,0,.14);border-radius:6px;text-align:center;background:#fff;color:var(--color-text-primary);}
.ri:focus{outline:none;border-color:#7bb932;}
.rp{position:absolute;right:8px;top:50%;transform:translateY(-50%);font-size:11px;color:var(--color-text-muted);}
.stbl{width:100%;border-collapse:collapse;border:.5px solid rgba(0,0,0,.14);border-radius:6px;overflow:hidden;table-layout:fixed;}
.stbl th:first-child,.stbl td:first-child{width:26%;}
.stbl th:not(:first-child),.stbl td:not(:first-child){width:24.66%;}
.stbl thead tr{background:var(--color-bg-tertiary);}
.stbl th{padding:5px 10px;font-size:10px;font-weight:500;color:var(--color-text-muted);letter-spacing:.03em;text-transform:uppercase;border-bottom:.5px solid rgba(0,0,0,.08);}
.stbl th:first-child{text-align:left;}
.stbl th:not(:first-child){text-align:right;}
.stbl td{padding:7px 10px;border-bottom:.5px solid rgba(0,0,0,.08);}
.stbl tr:last-child td{border-bottom:none;}
.stbl .itm{font-size:11px;color:var(--color-text-secondary);}
.stbl .vl{text-align:right;font-size:13px;font-weight:500;color:var(--color-text-primary);}
.stbl .df{text-align:right;font-size:11px;}
.ar{display:flex;justify-content:flex-end;align-items:center;gap:8px;margin-top:8px;}
.ab{padding:6px 20px;font-size:12px;font-weight:500;border:none;border-radius:8px;background:#1a1a18;color:#fff;cursor:pointer;transition:all .15s;}
.ab:hover:not(:disabled){background:#333;}
.ab:disabled{background:#d1d5db;color:#9ca3af;cursor:not-allowed;}
.sum-bar{background:var(--color-bg);border:.5px solid var(--color-border-strong);border-top:none;border-radius:0 0 12px 12px;overflow:visible;}
.bar-sel{display:none;padding:12px 18px;overflow:visible;}
.doc-header{max-width:1280px;margin:0 auto 20px;}
.doc-title{font-size:20px;font-weight:700;color:var(--color-text-primary);margin:0 0 4px;}
.doc-sub{font-size:12px;color:var(--color-text-secondary);margin:0 0 16px;}
.history-table{width:100%;border-collapse:collapse;background:var(--color-bg);border:1px solid var(--color-border-strong);border-radius:10px;overflow:hidden;font-size:12.5px;}
.history-table th{background:var(--color-accent-bg);text-align:left;padding:8px 14px;font-weight:600;color:var(--color-accent-deep);border-bottom:1px solid var(--color-accent-bg-strong);}
.history-table td{padding:8px 14px;border-bottom:1px solid var(--color-border);color:var(--color-text-primary);}
.history-table tr:last-child td{border-bottom:none;}
</style>
</head>
<body>

<div class="doc-header">
  <h1 class="doc-title">스마트 유닛 관리 대시보드 고도화</h1>
  <p class="doc-sub">유닛 RANK 분석 · CPC 수정 · 예측 데이터 대시보드 기획안</p>
  <table class="history-table">
    <thead>
      <tr>
        <th style="width:80px;">버전</th>
        <th style="width:120px;">작성일</th>
        <th style="width:100px;">작성자</th>
        <th style="display:flex;align-items:center;justify-content:space-between;">변경 내용<button id="history-toggle" onclick="(function(){var rows=document.querySelectorAll('.history-old');var btn=document.getElementById('history-toggle');var open=rows[0].style.display!=='none';rows.forEach(function(r){r.style.display=open?'none':'table-row';});btn.textContent=open?'▾':'▴';})()" style="background:#fff;border:1px solid var(--color-accent-bg-strong);border-radius:5px;cursor:pointer;font-size:11px;color:var(--color-accent-deep);padding:2px 8px;line-height:1;">▾</button></th>
      </tr>
    </thead>
    <tbody>
      <!-- 최신 행 (항상 노출) -->
      <tr id="history-latest">
        <td>v1.2</td><td>2026.07.02</td><td>전태호</td>
        <td>차트 클릭으로만 구간 선택 가능하도록 정책 변경 (구간 넘버링 바 제거) / 목표 ROAS 수평선 및 범례 추가 / 전환율·예상 전환율 보라 계열 컬러 통일</td>
      </tr>
      <!-- 이전 행 (접힘 기본) -->
      <tr class="history-old" style="display:none;"><td>v1.1</td><td>2026.07.01</td><td>전태호</td><td>ROAS 막대 그래프 겹쳐 그리기 방식 적용</td></tr>
      <tr class="history-old" style="display:none;"><td>v1.0</td><td>2026.06.30</td><td>전태호</td><td>최초 작성</td></tr>
    </tbody>
  </table>
</div>

<div class="tabs" role="tablist">
  <button type="button" class="tab tab--active" data-tab="demo">데모</button>
  <button type="button" class="tab" data-tab="spec">화면 설계서</button>
</div>

<div class="panel panel--active" id="panel-demo">
  <div style="max-width:1280px;margin:0 auto;">
<div style="display:flex;align-items:center;gap:10px;margin-bottom:12px;">
  <span style="font-size:12px;font-weight:500;color:var(--color-text-secondary);">KPI 유형</span>
  <select class="kpi-sel" id="kpi-sel" onchange="setKPI(this.value)">
    <option value="ROAS">ROAS</option>
    <option value="CPA">CPA</option>
    <option value="CPC">CPC</option>
    <option value="CPI">CPI</option>
  </select>
</div>
<div class="dash">
  <div class="dash-hd">
    <div>
      <p class="dash-title">유닛 RANK 분석</p>
      <p class="dash-sub">배너 · PC · 쇼핑 &nbsp;·&nbsp; 왼쪽 = 상위 RANK</p>
    </div>
    <div class="dash-r">
      <div class="base-wrap">
        <button class="base-btn" id="base-btn">
          <span class="base-txt" id="base-txt">기본 단가 320원</span>
          <svg class="base-ic" width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"/><path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"/></svg>
        </button>
        <div class="bep" id="bep">
          <p class="bep-title">기본 단가 수정</p>
          <div class="bep-row"><span class="bep-lbl">현재 단가</span><span style="font-size:13px;font-weight:500;color:var(--color-text-primary);" id="cur-base">320원</span></div>
          <div class="bep-row"><span class="bep-lbl">변경 단가</span><input class="bep-inp" id="bep-inp" type="number" value="320"><span class="bep-unit">원</span></div>
          <div class="bep-foot"><button class="bep-cancel" id="bep-cancel">취소</button><button class="bep-save" id="bep-save">저장</button></div>
        </div>
      </div>
      <div class="seg-btns" id="seg-btns">
        <button class="seg-btn" data-n="10">10구간</button>
        <button class="seg-btn on" data-n="20">20구간</button>
        <button class="seg-btn" data-n="40">40구간</button>
      </div>
    </div>
  </div>

  <div class="charts-g">
    <div class="chart-card">
      <div class="chart-hd">
        <span class="chart-title" id="chart-title-1">ROAS · 전환율</span>
        <div class="lgnd">
          <span class="lgnd-item"><span class="lbar" id="lgnd-d1-a" style="background:#639922;"></span>ROAS</span>
          <span class="lgnd-item"><span class="lbar" id="lgnd-d1-b" style="background:#A8D78A;"></span>예상 ROAS</span>
          <span class="lgnd-item"><span class="lline" style="background:#7F77DD;"></span>전환율</span>
          <span class="lgnd-item" style="color:#B5B0EE;"><span class="ldash" style="border-top:2px dashed #B5B0EE;"></span>예상 전환율</span>
          <span class="lgnd-item" id="lgnd-goal-wrap" style="color:rgba(130,130,130,0.8);"><span class="ldash" id="lgnd-goal" style="border-top:1.5px dashed rgba(160,160,160,0.55);"></span>목표 ROAS 500%</span>
        </div>
      </div>
      <div class="chart-area"><canvas id="c1" role="img" aria-label="ROAS 및 전환율 현재/예상 복합 차트">ROAS 및 전환율</canvas></div>
    </div>
    <div class="chart-card">
      <div class="chart-hd">
        <span class="chart-title">소진액 · CPC</span>
        <div class="lgnd">
          <span class="lgnd-item"><span class="lbar" style="background:#85B7EB;"></span>소진액</span>
          <span class="lgnd-item"><span class="lline" style="background:#D85A30;"></span>CPC</span>
        </div>
      </div>
      <div class="chart-area"><canvas id="c2" role="img" aria-label="소진액 및 CPC 현재/예상 복합 차트">소진액 및 CPC</canvas></div>
    </div>
  </div>


  <div class="sum-bar">
    <div class="bar-empty" id="bar-empty">
      <svg width="14" height="14" viewBox="0 0 16 16" fill="none" style="opacity:.35;flex-shrink:0;"><circle cx="8" cy="8" r="7" stroke="currentColor" stroke-width="1.2"/><path d="M8 7v5M8 5v.5" stroke="currentColor" stroke-width="1.4" stroke-linecap="round"/></svg>
      <p>그래프에서 구간을 선택하면 구간별 CPC 수정 및 예측 데이터를 확인할 수 있습니다.</p>
    </div>
    <div class="bar-sel" id="bar-sel">
      <div class="sum-top">
        <div class="sum-tl">
          <span class="sbadge" id="b-badge"></span>
          <span class="srange" id="b-range"></span>
          <span class="sunits" id="b-units"></span>
        </div>
      </div>
      <div class="cpc-row">
        <div class="cbox"><p class="clbl">평균 CPC</p><p class="cval" id="b-avg">-</p></div>
        <div class="cbox"><p class="clbl">권장 CPC</p><p class="cval bl" id="b-rec">-</p></div>
        <div class="rc">
          <button class="rb" id="rm">-</button>
          <div class="rw"><input class="ri" id="rate" type="number" value="0"><span class="rp">%</span></div>
          <button class="rb" id="rp2">+</button>
        </div>
      </div>
      <table class="stbl">
        <thead><tr><th style="text-align:left;">항목</th><th>현재</th><th>예상</th><th>변화</th></tr></thead>
        <tbody>
          <tr><td class="itm">CPC</td><td class="vl" id="tc-c">-</td><td class="vl" id="tc-a">-</td><td class="df" id="tc-d">-</td></tr>
          <tr><td class="itm">전환율</td><td class="vl" id="tv-c">-</td><td class="vl" id="tv-a">-</td><td class="df" id="tv-d">-</td></tr>
          <tr><td class="itm">ROAS</td><td class="vl" id="tr-c">-</td><td class="vl" id="tr-a">-</td><td class="df" id="tr-d">-</td></tr>
          <tr><td class="itm">KPI 달성률</td><td class="vl" id="tk-c">-</td><td class="vl" id="tk-a">-</td><td class="df" id="tk-d">-</td></tr>
        </tbody>
      </table>
      <div class="ar"><button class="cx" id="cx">닫기</button><button class="ab" id="apply-btn" disabled>적용</button></div>
    </div>
  </div>
</div>
  </div>
</div>

<div class="panel" id="panel-spec">
  <div class="spec">
    <aside class="spec__legend">
      <h2>화면 설계서 — 유닛 RANK 분석</h2>
      <table class="spec-table">
        <thead><tr><th>No.</th><th>설명</th></tr></thead>
        <tbody>
          <tr><td><span class="num-cell">1</span></td><td><strong>기본 단가 버튼</strong><br>현재 적용 중인 기본 단가를 표시한다. 마우스 오버 시 수정 아이콘이 노출되며, 클릭 시 인라인 편집 패널이 열린다.<div class="sub-row"><span class="num-cell" style="font-size:10px;">1-1</span><span><strong>기본 단가 수정 패널</strong> — 현재 단가 확인 및 변경 단가 입력. 텍스트박스 내 상/하 버튼 클릭 시 단가가 1원 단위로 증가/감소. 저장 시 기본 단가 반영 및 권장 CPC 재산출.</span></div></td></tr>
          <tr><td><span class="num-cell">2</span></td><td><strong>구간 전환 버튼</strong><br>10 / 20 / 40구간 선택. 기본값 20구간. 변경 시 차트·구간 넘버링·요약 바 일괄 갱신, CPC 비율 초기화.</td></tr>
          <tr><td><span class="num-cell">3</span></td><td><strong>ROAS · 전환율 차트</strong><br>ROAS(진한 초록)·예상 ROAS(연한 초록), 전환율(진한 보라 실선)·예상 전환율(연한 보라 점선) 표시. 목표 ROAS는 회색 얇은 점선으로 수평 표시한다. 마우스 오버 시 툴팁 노출.
            <div class="sub-row"><span class="num-cell" style="font-size:10px;">3-1</span><span>마우스 오버 시 툴팁을 노출한다. 해당 구간에서 그래프가 제공하는 데이터를 표기한다. 툴팁 상세는 차트 툴팁 상세 디스크립션 참고.</span></div>
            <div class="sub-row"><span class="num-cell" style="font-size:10px;">3-2</span><span><strong>ROAS 막대 동작 방식</strong> — 실제 ROAS와 예상 ROAS 중 더 큰 값을 전체 높이로 먼저 그리고, 더 작은 값을 동일한 위치에 겹쳐서 그린다. 두 값 중 더 큰 쪽의 색이 항상 바깥쪽(아래)에 표시되어 비교가 쉽도록 한다. 두 값이 동일할 경우 작은값 막대가 큰값 막대를 완전히 덮어 ROAS(실제) 색만 표시된다.</span></div>
            <div class="sub-row"><span class="num-cell" style="font-size:10px;">3-3</span><span><strong>목표 ROAS 수평선</strong> — 설정된 목표 ROAS 값을 회색 얇은 점선(borderWidth 0.8)으로 차트 전체 너비에 걸쳐 수평 표시한다. 범례에 "목표 ROAS 500%"처럼 수치를 함께 표기하며, 목표 KPI가 ROAS가 아닌 캠페인에서는 선과 범례 항목이 노출되지 않는다. 툴팁 호버 시 데이터 행에는, 노출되지 않는다.</span></div>
            <div class="sub-row"><span class="num-cell" style="font-size:10px;">3-4</span><span><strong>차트 클릭 시 구간 선택</strong> — 막대 또는 영역을 클릭하면 해당 구간이 선택되어 하단 요약 바에 해당 구간의 CPC 수정 및 예측 데이터가 노출된다. 구간 선택은 차트 클릭으로만 가능하다. 선택된 구간은 마우스 오버 시 호버 밴드와 동일한 반투명 색상(rgba 0,0,0, 0.05)으로 차트 영역에 유지 표시된다. 닫기 버튼 클릭 또는 구간 전환 시 밴드가 제거된다.</span></div>
          </td></tr>
          <tr><td><span class="num-cell">4</span></td><td><strong>소진액 · CPC 차트</strong><br>소진액(파랑 막대)과 CPC(주황 실선) 표시. 마우스 오버 시 툴팁 노출. 차트 클릭 시에도 3-3과 동일하게 구간이 선택되어 요약 바에 데이터가 노출된다.</td></tr>
          <tr><td><span class="num-cell">5</span></td><td><strong>요약 바 — 미선택 상태</strong><br>구간을 선택하기 전 안내 문구를 표시한다. 차트 클릭 후 6번으로 전환.</td></tr>
          <tr><td><span class="num-cell">6</span></td><td><strong>요약 바 — 선택 상태</strong><br>차트 막대 클릭 시 해당 구간의 CPC 수정 인터페이스와 예측 데이터 표를 표시한다. 상세 구성은 하단 "요약 바 — 구간 선택 상태" 섹션 참고.</td></tr>
        </tbody>
      </table>
    </aside>
    <div class="spec__screen">
<div class="dash">
  <div class="dash-hd">
    <div>
      <p class="dash-title">유닛 RANK 분석</p>
      <p class="dash-sub">배너 · PC · 쇼핑 &nbsp;·&nbsp; 왼쪽 = 상위 RANK</p>
    </div>
    <div class="dash-r">
      <div class="base-wrap marker-host"><span class="spec-num" style="left:-18px;top:-6px;z-index:9999;">1</span>
        <button class="base-btn" id="s-base-btn">
          <span class="base-txt" id="s-base-txt">기본 단가 320원</span>
          <svg class="base-ic" width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"/><path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"/></svg>
        </button>
        <div class="bep" id="s-bep">
          <p class="bep-title">기본 단가 수정</p>
          <div class="bep-row"><span class="bep-lbl">현재 단가</span><span id="s-cur-base" style="font-size:13px;font-weight:500;color:var(--color-text-primary);">320원</span></div>
          <div class="bep-row"><span class="bep-lbl">변경 단가</span><input class="bep-inp" id="s-bep-inp" type="number" value="320"><span class="bep-unit">원</span></div>
          <div class="bep-foot"><button class="bep-cancel" id="s-bep-cancel">취소</button><button class="bep-save" id="s-bep-save">저장</button></div>
        </div>
      </div>
      <div class="seg-btns marker-host"><span class="spec-num" style="left:-18px;top:-6px;z-index:9999;">2</span>
        <button class="seg-btn" data-n="10">10구간</button>
        <button class="seg-btn on" data-n="20">20구간</button>
        <button class="seg-btn" data-n="40">40구간</button>
      </div>
    </div>
  </div>

  <div class="charts-g">
    <div class="chart-card">
      <div class="chart-hd">
        <span class="chart-title">ROAS · 전환율</span>
        <div class="lgnd">
          <span class="lgnd-item"><span class="lbar" style="background:#639922;"></span>ROAS</span>
          <span class="lgnd-item"><span class="lbar" style="background:#A8D78A;"></span>예상 ROAS</span>
          <span class="lgnd-item"><span class="lline" style="background:#7F77DD;"></span>전환율</span>
          <span class="lgnd-item" style="color:#B5B0EE;"><span class="ldash" style="border-top:2px dashed #B5B0EE;"></span>예상 전환율</span>
          <span class="lgnd-item" style="color:rgba(130,130,130,0.8);"><span class="ldash" style="border-top:1.5px dashed rgba(160,160,160,0.55);"></span>목표 ROAS 500%</span>
        </div>
      </div>
      <div class="chart-area"><span class="spec-num" style="left:-28px;top:4px;z-index:9999;">3</span><canvas id="s-c1" role="img" aria-label="ROAS 및 전환율 현재/예상 복합 차트">ROAS 및 전환율</canvas></div>
    </div>
    <div class="chart-card">
      <div class="chart-hd">
        <span class="chart-title">소진액 · CPC</span>
        <div class="lgnd">
          <span class="lgnd-item"><span class="lbar" style="background:#85B7EB;"></span>소진액</span>
          <span class="lgnd-item"><span class="lline" style="background:#D85A30;"></span>CPC</span>
        </div>
      </div>
      <div class="chart-area"><span class="spec-num" style="left:-28px;top:4px;z-index:9999;">4</span><canvas id="s-c2" role="img" aria-label="소진액 및 CPC 현재/예상 복합 차트">소진액 및 CPC</canvas></div>
    </div>
  </div>


  <div class="sum-bar">
    <div class="bar-empty marker-host" id="s-bar-empty"><span class="spec-num" style="left:-28px;top:14px;z-index:9999;">5</span>
      <svg width="14" height="14" viewBox="0 0 16 16" fill="none" style="opacity:.35;flex-shrink:0;"><circle cx="8" cy="8" r="7" stroke="currentColor" stroke-width="1.2"/><path d="M8 7v5M8 5v.5" stroke="currentColor" stroke-width="1.4" stroke-linecap="round"/></svg>
      <p>그래프에서 구간을 선택하면 구간별 CPC 수정 및 예측 데이터를 확인할 수 있습니다.</p>
    </div>
    <div class="bar-sel marker-host" id="s-bar-sel"><span class="spec-num" style="left:-28px;top:8px;z-index:9999;">6</span>
      <div class="sum-top">
        <div class="sum-tl">
          <span class="sbadge" id="s-b-badge"></span>
          <span class="srange" id="s-b-range"></span>
          <span class="sunits" id="s-b-units"></span>
        </div>
      </div>
      <div class="cpc-row">
        <div class="cbox"><p class="clbl">평균 CPC</p><p class="cval" id="s-b-avg">-</p></div>
        <div class="cbox"><p class="clbl">권장 CPC</p><p class="cval bl" id="s-b-rec">-</p></div>
        <div class="rc">
          <button class="rb" id="s-rm">-</button>
          <div class="rw"><input class="ri" id="s-rate" type="number" value="0"><span class="rp">%</span></div>
          <button class="rb" id="s-rp2">+</button>
        </div>
      </div>
      <table class="stbl">
        <thead><tr><th style="text-align:left;">항목</th><th>현재</th><th>예상</th><th>변화</th></tr></thead>
        <tbody>
          <tr><td class="itm">CPC</td><td class="vl" id="s-tc-c">-</td><td class="vl" id="s-tc-a">-</td><td class="df" id="s-tc-d">-</td></tr>
          <tr><td class="itm">전환율</td><td class="vl" id="s-tv-c">-</td><td class="vl" id="s-tv-a">-</td><td class="df" id="s-tv-d">-</td></tr>
          <tr><td class="itm">ROAS</td><td class="vl" id="s-tr-c">-</td><td class="vl" id="s-tr-a">-</td><td class="df" id="s-tr-d">-</td></tr>
          <tr><td class="itm">KPI 달성률</td><td class="vl" id="s-tk-c">-</td><td class="vl" id="s-tk-a">-</td><td class="df" id="s-tk-d">-</td></tr>
        </tbody>
      </table>
      <div class="ar"><button class="cx" id="s-cx">닫기</button><button class="ab" id="s-apply-btn" disabled>적용</button></div>
    </div>
  </div>
</div>

<div style="margin-top:32px;">
  <div style="display:flex;align-items:center;gap:8px;margin-bottom:12px;">
    <span class="spec-num" style="position:relative;left:0;top:0;margin-right:8px;box-shadow:none;">1-1</span><span style="font-size:14px;font-weight:600;color:var(--color-text-primary);">기본 단가 수정 패널</span>
  </div>
  <div style="background:var(--color-bg);border:.5px solid var(--color-border-strong);border-radius:12px;padding:24px;overflow:visible;">
    <div style="position:relative;display:inline-block;">
      <div class="bep" style="display:block;position:relative;top:0;left:0;box-shadow:none;">
        <p class="bep-title">기본 단가 수정</p>
        <div class="bep-row"><span class="bep-lbl">현재 단가</span><span style="font-size:13px;font-weight:500;color:var(--color-text-primary);">320원</span></div>
        <div class="bep-row"><span class="bep-lbl">변경 단가</span><input class="bep-inp" type="number" value="320"><span class="bep-unit">원</span></div>
        <div class="bep-foot"><button class="bep-cancel">취소</button><button class="bep-save">저장</button></div>
      </div>
    </div>
  </div>
</div>

<div style="margin-top:32px;">
  <div style="display:flex;align-items:center;gap:8px;margin-bottom:12px;">
    <span style="display:inline-flex;align-items:center;justify-content:center;min-width:22px;height:22px;padding:0 6px;border-radius:11px;background:var(--color-accent-dark);color:#fff;font-size:11px;font-weight:700;">3</span>
    <span style="font-size:14px;font-weight:600;color:var(--color-text-primary);">차트 툴팁 UI</span>
  </div>
  <div style="background:var(--color-bg);border:.5px solid var(--color-border-strong);border-radius:12px;padding:24px;overflow:visible;">
    <div style="display:flex;gap:32px;flex-wrap:wrap;">

      <div style="position:relative;display:inline-block;">
        <p style="font-size:11px;font-weight:600;color:var(--color-text-muted);margin:0 0 10px;">ROAS · 전환율 차트</p>
        <div style="background:var(--color-bg);border:1px solid var(--color-border-strong);border-radius:10px;padding:10px 14px;box-shadow:0 4px 12px rgba(0,0,0,0.08);min-width:170px;">
          <div style="display:flex;align-items:center;gap:8px;margin-bottom:8px;position:relative;">
            <span class="spec-num-alt" style="left:-24px;top:-4px;z-index:9999;">1</span>
            <span style="background:var(--color-accent-dark);color:#fff;font-size:10.5px;font-weight:700;padding:2px 9px;border-radius:10px;">2구간</span>
            <span style="font-size:11.5px;font-weight:600;color:var(--color-text-primary);position:relative;">5%–10%
              <span class="spec-num-alt" style="left:48px;top:-6px;z-index:9999;">2</span>
            </span>
          </div>
          <div style="border-top:1px solid rgba(0,0,0,0.08);padding-top:6px;position:relative;">
            <span class="spec-num-alt" style="left:-24px;top:2px;z-index:9999;">3</span>
            <div style="display:flex;align-items:center;justify-content:space-between;gap:14px;padding:3px 0;">
              <span style="display:flex;align-items:center;gap:6px;font-size:11.5px;color:var(--color-text-secondary);"><span style="width:7px;height:7px;border-radius:50%;background:#639922;display:inline-block;"></span>ROAS</span>
              <span style="font-size:12.5px;font-weight:700;color:#639922;">980%</span>
            </div>
            <div style="display:flex;align-items:center;justify-content:space-between;gap:14px;padding:3px 0;">
              <span style="display:flex;align-items:center;gap:6px;font-size:11.5px;color:var(--color-text-secondary);"><span style="width:7px;height:7px;border-radius:50%;background:#A8D78A;display:inline-block;"></span>예상 ROAS</span>
              <span style="font-size:12.5px;font-weight:700;color:#A8D78A;">1,030%</span>
            </div>
            <div style="display:flex;align-items:center;justify-content:space-between;gap:14px;padding:3px 0;">
              <span style="display:flex;align-items:center;gap:6px;font-size:11.5px;color:var(--color-text-secondary);"><span style="width:7px;height:7px;border-radius:50%;background:#7F77DD;display:inline-block;"></span>전환율</span>
              <span style="font-size:12.5px;font-weight:700;color:#7F77DD;">5.60%</span>
            </div>
            <div style="display:flex;align-items:center;justify-content:space-between;gap:14px;padding:3px 0;">
              <span style="display:flex;align-items:center;gap:6px;font-size:11.5px;color:var(--color-text-secondary);"><span style="width:7px;height:7px;border-radius:50%;background:#B5B0EE;display:inline-block;"></span>예상 전환율</span>
              <span style="font-size:12.5px;font-weight:700;color:#B5B0EE;">5.90%</span>
            </div>
          </div>
        </div>
      </div>

      <div style="position:relative;display:inline-block;">
        <p style="font-size:11px;font-weight:600;color:var(--color-text-muted);margin:0 0 10px;">소진액 · CPC 차트</p>
        <div style="background:var(--color-bg);border:1px solid var(--color-border-strong);border-radius:10px;padding:10px 14px;box-shadow:0 4px 12px rgba(0,0,0,0.08);min-width:170px;">
          <div style="display:flex;align-items:center;gap:8px;margin-bottom:8px;position:relative;">
            <span class="spec-num-alt" style="left:-24px;top:-4px;z-index:9999;">4</span>
            <span style="background:var(--color-accent-dark);color:#fff;font-size:10.5px;font-weight:700;padding:2px 9px;border-radius:10px;">2구간</span>
            <span style="font-size:11.5px;font-weight:600;color:var(--color-text-primary);position:relative;">5%–10%
              <span class="spec-num-alt" style="left:48px;top:-6px;z-index:9999;">5</span>
            </span>
          </div>
          <div style="border-top:1px solid rgba(0,0,0,0.08);padding-top:6px;position:relative;">
            <span class="spec-num-alt" style="left:-24px;top:2px;z-index:9999;">6</span>
            <div style="display:flex;align-items:center;justify-content:space-between;gap:14px;padding:3px 0;">
              <span style="display:flex;align-items:center;gap:6px;font-size:11.5px;color:var(--color-text-secondary);"><span style="width:7px;height:7px;border-radius:50%;background:#185FA5;display:inline-block;"></span>소진액</span>
              <span style="font-size:12.5px;font-weight:700;color:#185FA5;">2,600</span>
            </div>
            <div style="display:flex;align-items:center;justify-content:space-between;gap:14px;padding:3px 0;">
              <span style="display:flex;align-items:center;gap:6px;font-size:11.5px;color:var(--color-text-secondary);"><span style="width:7px;height:7px;border-radius:50%;background:#D85A30;display:inline-block;"></span>CPC</span>
              <span style="font-size:12.5px;font-weight:700;color:#D85A30;">255원</span>
            </div>
          </div>
        </div>
      </div>

    </div>

    <div style="margin-top:20px;display:flex;flex-direction:column;gap:8px;font-size:12.5px;line-height:1.7;color:#374151;">
      <p style="font-size:11px;font-weight:600;color:var(--color-text-muted);margin:0 0 2px;">ROAS · 전환율 차트 (좌측 목업)</p>
      <div style="display:flex;gap:8px;">
        <span style="flex-shrink:0;width:18px;height:18px;border-radius:9px;background:#2563eb;color:#fff;font-size:9px;font-weight:700;display:flex;align-items:center;justify-content:center;">1</span>
        <span><strong>구간 칩</strong> — 호버한 구간 번호를 초록색 둥근 칩(뱃지)으로 표시.</span>
      </div>
      <div style="display:flex;gap:8px;">
        <span style="flex-shrink:0;width:18px;height:18px;border-radius:9px;background:#2563eb;color:#fff;font-size:9px;font-weight:700;display:flex;align-items:center;justify-content:center;">2</span>
        <span><strong>퍼센트 범위</strong> — 구간 칩 옆에 일반 텍스트로 범위(예: 5%–10%)를 표시.</span>
      </div>
      <div style="display:flex;gap:8px;">
        <span style="flex-shrink:0;width:18px;height:18px;border-radius:9px;background:#2563eb;color:#fff;font-size:9px;font-weight:700;display:flex;align-items:center;justify-content:center;">3</span>
        <span><strong>데이터 행</strong> — 구분선 아래 ROAS·예상 ROAS·전환율·예상 전환율 값을 색상 점(닷)과 함께 표시. 점과 값 텍스트는 해당 시리즈 색상으로 통일된다.</span>
      </div>
      <p style="font-size:11px;font-weight:600;color:var(--color-text-muted);margin:12px 0 2px;">소진액 · CPC 차트 (우측 목업)</p>
      <div style="display:flex;gap:8px;">
        <span style="flex-shrink:0;width:18px;height:18px;border-radius:9px;background:#2563eb;color:#fff;font-size:9px;font-weight:700;display:flex;align-items:center;justify-content:center;">4</span>
        <span><strong>구간 칩</strong> — ROAS·전환율 차트와 동일하게 호버한 구간 번호를 초록색 둥근 칩으로 표시.</span>
      </div>
      <div style="display:flex;gap:8px;">
        <span style="flex-shrink:0;width:18px;height:18px;border-radius:9px;background:#2563eb;color:#fff;font-size:9px;font-weight:700;display:flex;align-items:center;justify-content:center;">5</span>
        <span><strong>퍼센트 범위</strong> — 구간 칩 옆에 동일한 형식으로 범위 표시.</span>
      </div>
      <div style="display:flex;gap:8px;">
        <span style="flex-shrink:0;width:18px;height:18px;border-radius:9px;background:#2563eb;color:#fff;font-size:9px;font-weight:700;display:flex;align-items:center;justify-content:center;">6</span>
        <span><strong>데이터 행</strong> — 구분선 아래 소진액(파랑 점)·CPC(주황 점) 값을 색상 점과 함께 표시.</span>
      </div>
    </div>

  </div>
</div>

  <!-- 그래프 동작 방식 전용 설명 섹션 -->
  <div style="margin-top:32px;padding:20px 24px;background:#fff;border:1px solid #e5e7eb;border-radius:12px;">
    <h3 style="font-size:14px;font-weight:700;color:var(--color-text-primary);margin:0 0 14px;display:flex;align-items:center;gap:8px;"><span class="num-cell" style="font-size:10px;">3-2</span>ROAS 막대 그래프 동작 방식</h3>

    <!-- 예시 그래프 UI (3개 케이스 비교) -->
    <div style="display:grid;grid-template-columns:repeat(3,1fr);gap:16px;margin-bottom:20px;">

      <!-- 케이스 1: 실제 > 예상 -->
      <div style="border:1px solid #e5e7eb;border-radius:8px;padding:14px;background:var(--color-bg-secondary);">
        <p style="font-size:11px;font-weight:600;color:var(--color-text-secondary);margin:0 0 10px;display:flex;align-items:center;gap:6px;"><span style="display:inline-flex;align-items:center;justify-content:center;width:16px;height:16px;border-radius:8px;background:#2563eb;color:#fff;font-size:9px;font-weight:700;">4</span>CASE A &nbsp;·&nbsp; 실제 &gt; 예상</p>
        <div style="position:relative;height:120px;display:flex;align-items:flex-end;justify-content:center;">
          <div style="position:relative;width:36px;height:100%;display:flex;align-items:flex-end;">
            <div style="position:absolute;bottom:0;width:36px;height:100%;background:#639922;border-radius:3px;"></div>
            <div style="position:absolute;bottom:0;width:36px;height:55%;background:#A8D78A;border-radius:3px 3px 0 0;"></div>
          </div>
        </div>
        <p style="font-size:10px;color:var(--color-text-muted);text-align:center;margin:8px 0 0;">진한 초록(실제) 전체 노출</p>
      </div>

      <!-- 케이스 2: 예상 > 실제 -->
      <div style="border:1px solid #e5e7eb;border-radius:8px;padding:14px;background:var(--color-bg-secondary);">
        <p style="font-size:11px;font-weight:600;color:var(--color-text-secondary);margin:0 0 10px;display:flex;align-items:center;gap:6px;"><span style="display:inline-flex;align-items:center;justify-content:center;width:16px;height:16px;border-radius:8px;background:#2563eb;color:#fff;font-size:9px;font-weight:700;">5</span>CASE B &nbsp;·&nbsp; 예상 &gt; 실제</p>
        <div style="position:relative;height:120px;display:flex;align-items:flex-end;justify-content:center;">
          <div style="position:relative;width:36px;height:100%;display:flex;align-items:flex-end;">
            <div style="position:absolute;bottom:0;width:36px;height:100%;background:#A8D78A;border-radius:3px;"></div>
            <div style="position:absolute;bottom:0;width:36px;height:55%;background:#639922;border-radius:3px 3px 0 0;"></div>
          </div>
        </div>
        <p style="font-size:10px;color:var(--color-text-muted);text-align:center;margin:8px 0 0;">연한 초록(예상) 전체 노출</p>
      </div>

      <!-- 케이스 3: 실제 = 예상 -->
      <div style="border:1px solid #e5e7eb;border-radius:8px;padding:14px;background:var(--color-bg-secondary);">
        <p style="font-size:11px;font-weight:600;color:var(--color-text-secondary);margin:0 0 10px;display:flex;align-items:center;gap:6px;"><span style="display:inline-flex;align-items:center;justify-content:center;width:16px;height:16px;border-radius:8px;background:#2563eb;color:#fff;font-size:9px;font-weight:700;">6</span>CASE C &nbsp;·&nbsp; 실제 = 예상</p>
        <div style="position:relative;height:120px;display:flex;align-items:flex-end;justify-content:center;">
          <div style="position:relative;width:36px;height:100%;display:flex;align-items:flex-end;">
            <div style="position:absolute;bottom:0;width:36px;height:78%;background:#639922;border-radius:3px;"></div>
          </div>
        </div>
        <p style="font-size:10px;color:var(--color-text-muted);text-align:center;margin:8px 0 0;">진한 초록만 보임 (겹침)</p>
      </div>

    </div>

    <!-- 단일 구간 확대 다이어그램: 큰값/작은값 레이어 구조 -->
    <div style="border:1px solid #e5e7eb;border-radius:8px;padding:16px 20px;margin-bottom:20px;background:var(--color-bg-secondary);">
      <p style="font-size:11px;font-weight:600;color:var(--color-text-secondary);margin:0 0 14px;">레이어 구조 (CASE B 기준 분해)</p>
      <div style="display:flex;align-items:center;gap:24px;">
        <div style="position:relative;width:56px;height:110px;display:flex;align-items:flex-end;flex-shrink:0;">
          <div style="position:absolute;bottom:0;width:56px;height:100%;background:#A8D78A;border-radius:4px;"></div>
          <div style="position:absolute;bottom:0;width:56px;height:55%;background:#639922;border-radius:4px 4px 0 0;"></div>
        </div>
        <div style="font-size:12px;color:#374151;line-height:1.8;">
          <p style="margin:0;"><strong style="display:inline-flex;align-items:center;justify-content:center;width:16px;height:16px;border-radius:8px;background:#2563eb;color:#fff;font-size:9px;margin-right:6px;">1</strong>먼저 큰 값(예상 ROAS)을 전체 높이로 그린다 — 연한 초록.</p>
          <p style="margin:8px 0 0;"><strong style="display:inline-flex;align-items:center;justify-content:center;width:16px;height:16px;border-radius:8px;background:#2563eb;color:#fff;font-size:9px;margin-right:6px;">2</strong>그 위에 작은 값(실제 ROAS)을 동일한 폭으로 겹쳐 그린다 — 진한 초록. <code style="background:#eee;padding:1px 4px;border-radius:3px;font-size:11px;">grouped:false</code>, 동일한 <code style="background:#eee;padding:1px 4px;border-radius:3px;font-size:11px;">barPercentage</code>로 너비를 일치시킨다.</p>
        </div>
      </div>
    </div>
    <div style="display:flex;flex-direction:column;gap:10px;font-size:12.5px;line-height:1.7;color:#374151;">
      <div style="display:flex;gap:8px;">
        <span style="flex-shrink:0;width:18px;height:18px;border-radius:9px;background:#2563eb;color:#fff;font-size:10px;font-weight:700;display:flex;align-items:center;justify-content:center;">1</span>
        <span>구간마다 <strong>실제 ROAS</strong>와 <strong>예상 ROAS</strong> 두 값을 비교해 <strong>더 큰 값을 전체 높이</strong>로 먼저 그린다. (레이어 구조 다이어그램 참고)</span>
      </div>
      <div style="display:flex;gap:8px;">
        <span style="flex-shrink:0;width:18px;height:18px;border-radius:9px;background:#2563eb;color:#fff;font-size:10px;font-weight:700;display:flex;align-items:center;justify-content:center;">2</span>
        <span><strong>더 작은 값</strong>을 동일한 x축 위치(같은 막대 폭)에 <strong>겹쳐서</strong> 그린다. 즉 두 막대는 너비가 같고 높이만 다르게 겹쳐 보인다. (레이어 구조 다이어그램 참고)</span>
      </div>
      <div style="display:flex;gap:8px;">
        <span style="flex-shrink:0;width:18px;height:18px;border-radius:9px;background:#2563eb;color:#fff;font-size:10px;font-weight:700;display:flex;align-items:center;justify-content:center;">3</span>
        <span><strong>색상 규칙</strong> — 더 큰 값에 해당하는 데이터(실제 또는 예상)가 항상 <strong style="color:#639922;">진한 초록(#639922, 실제 ROAS 색)</strong>으로, 더 작은 값은 <strong style="color:#A8D78A;">연한 초록(#A8D78A, 예상 ROAS 색)</strong>으로 표시되는 것이 아니라 — <u>"실제 ROAS"는 항상 진한 초록, "예상 ROAS"는 항상 연한 초록</u>으로 고정되며, 어느 값이 더 크냐에 따라 어느 색이 바깥쪽(아래, 전체 높이)에 깔리는지가 달라진다.</span>
      </div>
      <div style="display:flex;gap:8px;">
        <span style="flex-shrink:0;width:18px;height:18px;border-radius:9px;background:#2563eb;color:#fff;font-size:10px;font-weight:700;display:flex;align-items:center;justify-content:center;">4</span>
        <span><strong>실제 &gt; 예상</strong>인 구간 — 진한 초록(실제)이 전체 높이로 보이고, 연한 초록(예상)은 그 안쪽에 가려져 거의 보이지 않는다. (CASE A 참고)</span>
      </div>
      <div style="display:flex;gap:8px;">
        <span style="flex-shrink:0;width:18px;height:18px;border-radius:9px;background:#2563eb;color:#fff;font-size:10px;font-weight:700;display:flex;align-items:center;justify-content:center;">5</span>
        <span><strong>예상 &gt; 실제</strong>인 구간 — 연한 초록(예상)이 전체 높이로 보이고, 그 안쪽에 진한 초록(실제)이 더 낮은 높이로 겹쳐 보여 한눈에 "예상보다 실제가 못 미친다"는 것을 알 수 있다. (CASE B 참고)</span>
      </div>
      <div style="display:flex;gap:8px;">
        <span style="flex-shrink:0;width:18px;height:18px;border-radius:9px;background:#2563eb;color:#fff;font-size:10px;font-weight:700;display:flex;align-items:center;justify-content:center;">6</span>
        <span><strong>실제 = 예상</strong>인 경우 — 두 막대 높이가 같아 겹치며, 진한 초록(실제 ROAS) 색만 보인다. (CASE C 참고)</span>
      </div>
      <div style="display:flex;gap:8px;">
        <span style="flex-shrink:0;width:18px;height:18px;border-radius:9px;background:#2563eb;color:#fff;font-size:10px;font-weight:700;display:flex;align-items:center;justify-content:center;">7</span>
        <span><strong>전환율 꺾은선</strong>은 막대와 무관하게 별도 표시되며, 동일한 원리로 실제 전환율(보라 실선)·예상 전환율(주황 점선)을 함께 그린다. 막대와 달리 겹쳐 그리지 않고 두 선을 모두 그대로 표시한다.</span>
      </div>
      <div style="display:flex;gap:8px;">
        <span style="flex-shrink:0;width:18px;height:18px;border-radius:9px;background:#2563eb;color:#fff;font-size:10px;font-weight:700;display:flex;align-items:center;justify-content:center;">8</span>
        <span><strong>툴팁</strong>에서는 항목별 라벨(큰값/작은값) 대신 실제 ROAS·예상 ROAS의 원래 수치를 그대로 보여준다. 즉 화면에 보이는 막대 색과 무관하게 정확한 두 값을 모두 확인할 수 있다.</span>
      </div>
    </div>
  </div>

<div style="margin-top:32px;">
  <div style="display:flex;align-items:center;gap:8px;margin-bottom:12px;">
    <span style="display:inline-flex;align-items:center;justify-content:center;min-width:22px;height:22px;padding:0 6px;border-radius:11px;background:var(--color-accent-dark);color:#fff;font-size:11px;font-weight:700;">6</span>
    <span style="font-size:14px;font-weight:600;color:var(--color-text-primary);">요약 바 — 구간 선택 상태</span>
  </div>
  <div style="background:var(--color-bg);border:.5px solid var(--color-border-strong);border-radius:12px;padding:12px 18px;overflow:visible;">
    <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:10px;">
      <div style="display:flex;align-items:center;gap:6px;position:relative;">
        <span class="spec-num-alt" style="left:-28px;top:-8px;z-index:9999;">1</span>
        <span class="sbadge">3구간</span><span class="srange">10%–15%</span><span class="sunits">유닛 44개</span>
      </div>
    </div>
    <div class="cpc-row" style="margin-bottom:10px;">
      <div class="cbox marker-host"><span class="spec-num-alt" style="left:-28px;top:-8px;z-index:9999;">2</span><p class="clbl">평균 CPC</p><p class="cval">232원</p></div>
      <div class="cbox marker-host"><span class="spec-num-alt" style="left:-28px;top:-8px;z-index:9999;">3</span><p class="clbl">권장 CPC</p><p class="cval bl">258원</p></div>
      <div class="rc marker-host"><span class="spec-num-alt" style="left:-28px;top:-8px;z-index:9999;">4</span>
        <button class="rb">−</button>
        <div class="rw"><input class="ri" type="number" value="11" readonly><span class="rp">%</span></div>
        <button class="rb">+</button>
      </div>
    </div>
    <div style="position:relative;"><span class="spec-num-alt" style="left:-28px;top:8px;z-index:9999;">5</span>
      <table class="stbl">
        <thead><tr><th style="text-align:left;">항목</th><th>현재</th><th>예상</th><th>변화</th></tr></thead>
        <tbody>
          <tr><td class="itm">CPC</td><td class="vl">232원</td><td class="vl" style="color:#185FA5;">257원</td><td class="df"><span style="color:#185FA5;font-weight:500;">+25원</span></td></tr>
          <tr><td class="itm">전환율</td><td class="vl">3.80%</td><td class="vl" style="color:#185FA5;">4.12%</td><td class="df"><span style="color:#185FA5;font-weight:500;">+0.32%p</span></td></tr>
          <tr><td class="itm">ROAS</td><td class="vl">820%</td><td class="vl" style="color:#D85A30;">740%</td><td class="df"><span style="color:#D85A30;font-weight:500;">-80%</span></td></tr>
          <tr><td class="itm">KPI 달성률</td><td class="vl">57%</td><td class="vl" style="color:#D85A30;">52%</td><td class="df"><span style="color:#D85A30;font-weight:500;">-5%p</span></td></tr>
        </tbody>
      </table>
    </div>
    <div style="display:flex;justify-content:flex-end;align-items:center;gap:8px;margin-top:8px;">
      <div style="position:relative;"><span class="spec-num-alt" style="left:-28px;top:-8px;z-index:9999;">7</span><button class="cx">닫기</button></div>
      <div style="position:relative;"><span class="spec-num-alt" style="right:-28px;left:auto;top:-8px;z-index:9999;">6</span><button class="ab">적용</button></div>
    </div>
  </div>
</div>

  <!-- 요약 바 선택 상태 디스크립션 -->
  <div style="margin-top:20px;padding:20px 24px;background:#fff;border:1px solid #e5e7eb;border-radius:12px;">
    <div style="display:flex;flex-direction:column;gap:8px;font-size:12.5px;line-height:1.7;color:#374151;">
      <div style="display:flex;gap:8px;">
        <span style="flex-shrink:0;width:18px;height:18px;border-radius:9px;background:#2563eb;color:#fff;font-size:9px;font-weight:700;display:flex;align-items:center;justify-content:center;">1</span>
        <span><strong>구간 정보</strong> — 선택한 N구간, 해당 구간의 퍼센트 범위(%–%), 포함된 유닛 개수를 표시한다.</span>
      </div>
      <div style="display:flex;gap:8px;">
        <span style="flex-shrink:0;width:18px;height:18px;border-radius:9px;background:#2563eb;color:#fff;font-size:9px;font-weight:700;display:flex;align-items:center;justify-content:center;">2</span>
        <span><strong>평균 CPC</strong> — 해당 구간 유닛들의 평균 CPC 값.</span>
      </div>
      <div style="display:flex;gap:8px;">
        <span style="flex-shrink:0;width:18px;height:18px;border-radius:9px;background:#2563eb;color:#fff;font-size:9px;font-weight:700;display:flex;align-items:center;justify-content:center;">3</span>
        <span><strong>권장 CPC</strong> — KPI 유형에 따라 아래 역산 공식으로 계산된 권장값. 파란색으로 강조 표시.
              <table style="margin-top:8px;border-collapse:collapse;font-size:11px;width:100%;">
                <thead>
                  <tr style="background:#f0f4ff;">
                    <th style="border:1px solid #c7d7fd;padding:5px 10px;text-align:left;color:#1d4ed8;font-weight:600;">KPI 유형</th>
                    <th style="border:1px solid #c7d7fd;padding:5px 10px;text-align:left;color:#1d4ed8;font-weight:600;width:50px;">지표</th>
                    <th style="border:1px solid #c7d7fd;padding:5px 10px;text-align:left;color:#1d4ed8;font-weight:600;">공식</th>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <td style="border:1px solid #e2e8f0;padding:5px 10px;color:#374151;">WEB &gt; 매출 (ROAS)</td>
                    <td style="border:1px solid #e2e8f0;padding:5px 10px;color:#374151;font-weight:600;text-align:center;">ROAS</td>
                    <td style="border:1px solid #e2e8f0;padding:5px 10px;color:#374151;font-family:monospace;">권장 CPC = 목표 ROAS(%) × 객단가 × 예측 전환율</td>
                  </tr>
                  <tr style="background:#fafafa;">
                    <td style="border:1px solid #e2e8f0;padding:5px 10px;color:#374151;">WEB &gt; 전환 (Conversion)</td>
                    <td style="border:1px solid #e2e8f0;padding:5px 10px;color:#374151;font-weight:600;text-align:center;">CPA</td>
                    <td style="border:1px solid #e2e8f0;padding:5px 10px;color:#374151;font-family:monospace;">권장 CPC = 목표 CPA × 예측 전환율</td>
                  </tr>
                  <tr>
                    <td style="border:1px solid #e2e8f0;padding:5px 10px;color:#374151;">WEB &gt; 유입 (Traffic)</td>
                    <td style="border:1px solid #e2e8f0;padding:5px 10px;color:#374151;font-weight:600;text-align:center;">CPC</td>
                    <td style="border:1px solid #e2e8f0;padding:5px 10px;color:#9a9a94;font-style:italic;">—</td>
                  </tr>
                  <tr style="background:#fafafa;">
                    <td style="border:1px solid #e2e8f0;padding:5px 10px;color:#374151;">APP &gt; 매출 (ROAS)</td>
                    <td style="border:1px solid #e2e8f0;padding:5px 10px;color:#374151;font-weight:600;text-align:center;">ROAS</td>
                    <td style="border:1px solid #e2e8f0;padding:5px 10px;color:#374151;font-family:monospace;">권장 CPC = 목표 ROAS(%) × 객단가 × 예측 전환율</td>
                  </tr>
                  <tr>
                    <td style="border:1px solid #e2e8f0;padding:5px 10px;color:#374151;">APP &gt; 인앱이벤트 (In APP Event)</td>
                    <td style="border:1px solid #e2e8f0;padding:5px 10px;color:#374151;font-weight:600;text-align:center;">CPI</td>
                    <td style="border:1px solid #e2e8f0;padding:5px 10px;color:#374151;font-family:monospace;">권장 CPC = 목표 CPI × 예측 전환율</td>
                  </tr>
                  <tr style="background:#fafafa;">
                    <td style="border:1px solid #e2e8f0;padding:5px 10px;color:#374151;">APP &gt; 설치 (Install)</td>
                    <td style="border:1px solid #e2e8f0;padding:5px 10px;color:#374151;font-weight:600;text-align:center;">CPI</td>
                    <td style="border:1px solid #e2e8f0;padding:5px 10px;color:#374151;font-family:monospace;">권장 CPC = 목표 CPI × 예측 전환율</td>
                  </tr>
                </tbody>
              </table>
            </span>
      </div>
      <div style="display:flex;gap:8px;">
        <span style="flex-shrink:0;width:18px;height:18px;border-radius:9px;background:#2563eb;color:#fff;font-size:9px;font-weight:700;display:flex;align-items:center;justify-content:center;">4</span>
        <span><strong>조정 비율 입력</strong> — % 직접 입력 또는 −/+ 버튼으로 1%씩 조정. 0%이면 적용 버튼 비활성.</span>
      </div>
      <div style="display:flex;gap:8px;">
        <span style="flex-shrink:0;width:18px;height:18px;border-radius:9px;background:#2563eb;color:#fff;font-size:9px;font-weight:700;display:flex;align-items:center;justify-content:center;">5</span>
        <span><strong>예측 데이터 표</strong> — CPC·전환율·ROAS·KPI 달성률의 현재/예상/변화를 표시. CPC 비율 조정 시에만 예상값이 채워지며 미조정 시 빈값. 양수는 파랑, 음수는 주황으로 구분. 예상 전환율은 CPC 조정에 따른 변화치이며 상단 차트의 예상 전환율(연구 데이터)과는 별개 값.</span>
      </div>
      <div style="display:flex;gap:8px;">
        <span style="flex-shrink:0;width:18px;height:18px;border-radius:9px;background:#2563eb;color:#fff;font-size:9px;font-weight:700;display:flex;align-items:center;justify-content:center;">6</span>
        <span><strong>적용 버튼</strong> — CPC 비율 수정 시에만 활성화. 해당 구간 유닛에 조정된 CPC를 일괄 적용.</span>
      </div>
      <div style="display:flex;gap:8px;">
        <span style="flex-shrink:0;width:18px;height:18px;border-radius:9px;background:#2563eb;color:#fff;font-size:9px;font-weight:700;display:flex;align-items:center;justify-content:center;">7</span>
        <span><strong>닫기 버튼</strong> — 요약 바를 닫고 미선택 상태로 복귀. 구간 선택 밴드도 함께 제거.</span>
      </div>
    </div>
  </div>


    </div>
  </div>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>
<script>
function chipTooltip(prefix){
  return function(context){
    var chart = context.chart;
    var tooltipEl = document.getElementById(prefix+'-chiptip');
    if (!tooltipEl) {
      tooltipEl = document.createElement('div');
      tooltipEl.id = prefix+'-chiptip';
      tooltipEl.style.position = 'absolute';
      tooltipEl.style.pointerEvents = 'none';
      tooltipEl.style.transition = 'opacity .08s ease';
      tooltipEl.style.zIndex = 30;
      chart.canvas.parentNode.style.position = chart.canvas.parentNode.style.position || 'relative';
      chart.canvas.parentNode.appendChild(tooltipEl);
    }
    var tt = context.tooltip;
    if (tt.opacity === 0) { tooltipEl.style.opacity = 0; return; }
    if (!tt.dataPoints || !tt.dataPoints.length) { tooltipEl.style.opacity = 0; return; }

    var idx = tt.dataPoints[0].dataIndex;
    var segNum = idx+1;
    var n = chart.data.labels.length;
    var step = 100/n;
    var rangeText = Math.round(idx*step)+'%'+String.fromCharCode(8211)+Math.round((idx+1)*step)+'%';

    var rows = [];
    tt.dataPoints.forEach(function(dp){
      var lbl = dp.dataset.label, color, text;
      if (lbl === '큰값') { color='#639922'; text='ROAS : '+dp.dataset.__rawROAS[idx].toLocaleString()+'%'; }
      else if (lbl === '작은값') { color='#A8D78A'; text='예상 ROAS : '+dp.dataset.__rawPRED[idx].toLocaleString()+'%'; }
      else if (lbl === '전환율') { color='#7F77DD'; text='전환율 : '+dp.parsed.y.toFixed(2)+'%'; }
      else if (lbl === '예상 전환율') { color='#B5B0EE'; text='예상 전환율 : '+dp.parsed.y.toFixed(2)+'%'; }
      else if (lbl === '목표 ROAS') { return; }
      else if (lbl === '소진액') { color='#185FA5'; text='소진액 : '+dp.parsed.y.toLocaleString(); }
      else if (lbl === 'CPC') { color='#D85A30'; text='CPC : '+dp.parsed.y.toLocaleString()+'원'; }
      else return;
      rows.push({color:color, text:text});
    });

    var rowsHtml = rows.map(function(r){
      return '<div style="display:flex;align-items:center;justify-content:space-between;gap:14px;padding:3px 0;">'
        + '<span style="display:flex;align-items:center;gap:6px;font-size:11.5px;color:var(--color-text-secondary);font-family:Apple SD Gothic Neo, Noto Sans KR, sans-serif;">'
        + '<span style="width:7px;height:7px;border-radius:50%;background:'+r.color+';display:inline-block;flex-shrink:0;"></span>'
        + r.text.split(' : ')[0] + '</span>'
        + '<span style="font-size:12.5px;font-weight:700;color:'+r.color+';font-family:Apple SD Gothic Neo, Noto Sans KR, sans-serif;">' + r.text.split(' : ')[1] + '</span>'
        + '</div>';
    }).join('');

    tooltipEl.innerHTML =
      '<div style="background:var(--color-bg);border:1px solid var(--color-border-strong);border-radius:10px;padding:10px 14px;box-shadow:0 4px 12px rgba(0,0,0,0.08);min-width:170px;">'
      + '<div style="display:flex;align-items:center;gap:8px;margin-bottom:8px;">'
      + '<span style="background:var(--color-accent-dark);color:#fff;font-size:10.5px;font-weight:700;padding:2px 9px;border-radius:10px;font-family:Apple SD Gothic Neo, Noto Sans KR, sans-serif;">'+segNum+'구간</span>'
      + '<span style="font-size:11.5px;font-weight:600;color:var(--color-text-primary);font-family:Apple SD Gothic Neo, Noto Sans KR, sans-serif;">'+rangeText+'</span>'
      + '</div>'
      + '<div style="border-top:1px solid rgba(0,0,0,0.08);padding-top:6px;">' + rowsHtml + '</div>'
      + '</div>';

    var position = chart.canvas.getBoundingClientRect();
    var canvasRect = chart.canvas.getBoundingClientRect();
    tooltipEl.style.opacity = 1;
    tooltipEl.style.left = tt.caretX + 12 + 'px';
    tooltipEl.style.top = tt.caretY - 10 + 'px';
  };
}
</script>
<script>
(function(){
// ROAS 데이터 (전환 ROAS %)
var BR=[1200,980,820,740,660,590,520,460,400,350,300,255,215,180,150,125,100,75,50,28];
var PR=[1106.1,1046.4,707.5,775.6,583.1,661.6,504.2,532.2,389.3,398.4,290.2,268.4,194.3,222.6,143.7,135.7,86.7,95,43.8,31.6];
// CPA 데이터 (전환단가 원)
var BA_CPA=[18000,15000,12800,11200,9800,8600,7500,6500,5700,4900,4200,3600,3000,2500,2100,1700,1400,1050,700,380];
var PA_CPA=[16200,16350,11008,11760,8673,9646,7278,7527,5558,5586,4074,3780,2705,3097,1995,1853,1204,1313,602,427];
// CPI 데이터 (설치당 단가 원)
var BA_CPI=[8500,7200,6100,5400,4750,4200,3700,3250,2850,2480,2150,1850,1580,1340,1130,950,780,620,470,290];
var PA_CPI=[7565,7848,5246,5670,4199,4704,3589,3770,2773,2827,2064,1924,1422,1609,1073,1007,674,782,417,326];
var BC=[8.2,5.6,3.8,3.2,2.7,2.3,2.0,1.7,1.5,1.3,1.1,0.9,0.75,0.62,0.5,0.4,0.3,0.22,0.14,0.07];
var PC=[8.6,5.9,4.1,3.5,2.95,2.5,2.2,1.9,1.65,1.42,1.2,0.98,0.82,0.68,0.55,0.44,0.33,0.24,0.15,0.08];
var BS=[3200,2600,2100,1800,1550,1320,1100,920,760,620,500,400,310,240,180,130,90,58,32,12];
var BCPC=[280,255,232,212,194,178,163,149,136,124,113,103,93,84,76,68,61,54,46,38];
var UC=[48,46,44,42,40,38,36,34,32,30,28,26,24,22,20,18,16,14,12,10];
var TROAS=500,N=20,si=-1,cv=[],ch1=null,ch2=null;
var CUR_KPI='ROAS';

// KPI별 설정
var KPI_CONFIG={
  ROAS:{
    label1:'ROAS · 전환율', d1:BR, pd1:PR, unit1:'%', color1:'#639922', pcolor1:'#A8D78A',
    goal:500, goalLabel:'목표 ROAS 500%', goalUnit:'%'
  },
  CPA:{
    label1:'전환단가 · 전환율', d1:BA_CPA, pd1:PA_CPA, unit1:'원', color1:'#639922', pcolor1:'#A8D78A',
    goal:8000, goalLabel:'목표 CPA 8,000원', goalUnit:'원'
  },
  CPI:{
    label1:'설치단가 · 설치율', d1:BA_CPI, pd1:PA_CPI, unit1:'원', color1:'#639922', pcolor1:'#A8D78A',
    goal:3500, goalLabel:'목표 CPI 3,500원', goalUnit:'원'
  },
  CPC:{
    label1:'ROAS · 전환율', d1:BR, pd1:PR, unit1:'%', color1:'#639922', pcolor1:'#A8D78A',
    goal:200, goalLabel:'목표 CPC 200원', goalUnit:'원'
  }
};

function setKPI(kpi){
  CUR_KPI=kpi; si=-1;
  document.getElementById('bar-empty').style.display='flex';
  document.getElementById('bar-sel').style.display='none';
  setN(N);
}
window.setKPI=setKPI;

function rs(d,n){
  var r=d.length/n;
  return Array.from({length:n},function(_,i){
    var s=Math.floor(i*r),e=Math.floor((i+1)*r);
    if(e<=s){
      var nearest=Math.min(Math.round(i*r),d.length-1);
      return d[nearest]||0;
    }
    var sl=d.slice(s,e);
    return parseFloat((sl.reduce(function(a,b){return a+b;},0)/sl.length).toFixed(2));
  });
}
function mkL(n){return Array.from({length:n},function(_,i){return Math.round(i*(100/n))+'%';});}

var ttColors={'ROAS':'#639922','예상 ROAS':'#A8D78A','전환율':'#7F77DD','예상 전환율':'#B5B0EE','소진액':'#185FA5','CPC':'#D85A30'};
var tt={backgroundColor:'#fff',borderColor:'rgba(0,0,0,0.1)',borderWidth:1,titleColor:'#1a1a18',titleFont:{size:12,weight:'700'},bodyColor:'#6b6b66',bodyFont:{size:13,weight:'600'},padding:10,cornerRadius:8,displayColors:true,boxWidth:7,boxHeight:7,usePointStyle:true,footerColor:'#1a1a18',footerFont:{size:12,weight:'700'},footerMarginTop:6,callbacks:{labelTextColor:function(ctx){
    if(ctx.dataset.label==='큰값') return '#639922';
    if(ctx.dataset.label==='작은값') return '#A8D78A';
    return ttColors[ctx.dataset.label]||'#1a1a18';
  }}};
var hoverBandPlugin={id:'hoverBand',beforeDatasetsDraw:function(chart){
  var ca=chart.chartArea,n=chart.data.labels.length,colW=ca.width/n,ctx=chart.ctx;
  // 선택된 구간 밴드 (호버와 동일한 색상)
  if(si>=0){
    var sx=ca.left+si*colW;
    ctx.save();ctx.fillStyle='rgba(0,0,0,0.05)';ctx.fillRect(sx,ca.top,colW,ca.height);ctx.restore();
  }
  // 마우스 호버 밴드
  var active=chart.getActiveElements();
  if(!active||!active.length)return;
  var idx=active[0].index;
  var x=ca.left+idx*colW;
  ctx.save();ctx.fillStyle='rgba(0,0,0,0.05)';ctx.fillRect(x,ca.top,colW,ca.height);ctx.restore();
}};


function rCharts(n){
  var labels=mkL(n),step=100/n;
  var cfg=KPI_CONFIG[CUR_KPI];
  var d1=cfg.d1, pd1=cfg.pd1, c1=cfg.color1, pc1=cfg.pcolor1;
  var goalVal=cfg.goal, goalLbl=cfg.goalLabel;
  var isCPC=(CUR_KPI==='CPC');

  // 범례 텍스트 업데이트
  var metricName=CUR_KPI==='ROAS'?'ROAS':CUR_KPI==='CPA'?'전환단가':'설치단가';
  var l1=document.getElementById('lgnd-d1-a');
  var l2=document.getElementById('lgnd-d1-b');
  var goalWrap=document.getElementById('lgnd-goal-wrap');
  var titleEl=document.getElementById('chart-title-1');
  if(l1){l1.style.background=c1; if(l1.nextSibling)l1.nextSibling.textContent=metricName;}
  if(l2){l2.style.background=pc1; if(l2.nextSibling)l2.nextSibling.textContent='예상 '+metricName;}
  if(goalWrap){
    goalWrap.style.display=(isCPC)?'none':'inline-flex';
    var goalText=goalWrap.lastChild;
    if(goalText)goalText.textContent=goalLbl;
  }
  if(titleEl)titleEl.textContent=cfg.label1;

  // 차트1 데이터셋
  var ds1=[];
  {
    var goalUnit=cfg.goalUnit;
    var yRcb=CUR_KPI==='ROAS'?function(v){return v.toLocaleString()+'%';}:function(v){return v.toLocaleString()+'원';};
    ds1=[
      {type:'bar',label:'큰값',data:rs(d1,n).map(function(v,i){return Math.max(v,rs(pd1,n)[i]);}),backgroundColor:rs(d1,n).map(function(v,i){return v>=rs(pd1,n)[i]?c1:pc1;}),borderRadius:2,yAxisID:'yR',order:4,barPercentage:0.82,categoryPercentage:0.82,grouped:false,__rawROAS:rs(d1,n),__rawPRED:rs(pd1,n)},
      {type:'bar',label:'작은값',data:rs(d1,n).map(function(v,i){return Math.min(v,rs(pd1,n)[i]);}),backgroundColor:rs(d1,n).map(function(v,i){return v<=rs(pd1,n)[i]?c1:pc1;}),borderRadius:2,yAxisID:'yR',order:3,barPercentage:0.82,categoryPercentage:0.82,grouped:false,__rawROAS:rs(d1,n),__rawPRED:rs(pd1,n)},
      {type:'line',label:'전환율',data:rs(BC,n),borderColor:'#7F77DD',backgroundColor:'transparent',borderWidth:2,pointRadius:n<=20?2:1,pointBackgroundColor:'#7F77DD',tension:0.3,yAxisID:'yC',order:2},
      {type:'line',label:'예상 전환율',data:rs(PC,n),borderColor:'#B5B0EE',backgroundColor:'transparent',borderWidth:2,borderDash:[4,3],pointRadius:n<=20?2:1,pointBackgroundColor:'#B5B0EE',tension:0.3,yAxisID:'yC',order:1},
      ...(isCPC?[]:[{type:'line',label:'목표선',data:Array(n).fill(goalVal),borderColor:'rgba(160,160,160,0.55)',backgroundColor:'transparent',borderWidth:0.8,borderDash:[6,4],pointRadius:0,pointHoverRadius:0,yAxisID:'yR',order:5,tension:0}])
    ];
  }

  if(ch1)ch1.destroy();
  ch1=new Chart(document.getElementById('c1'),{plugins:[hoverBandPlugin],data:{labels:labels,datasets:ds1},
    options:{responsive:true,maintainAspectRatio:false,animation:{duration:200},interaction:{mode:'index',intersect:false},
    onClick:function(evt,elements,chart){var pts=chart.getElementsAtEventForMode(evt,'index',{intersect:false},true);if(pts&&pts.length){selSeg(pts[0].index);}},
    plugins:{legend:{display:false},tooltip:{enabled:false,external:chipTooltip('c1')}},
    scales:{x:{grid:{display:false},border:{display:false},ticks:{font:{size:9},color:'#9a9a94',maxRotation:0,autoSkip:true,maxTicksLimit:11}},
      yR:{display:true,type:'linear',position:'left',grid:{color:'rgba(0,0,0,0.04)'},border:{display:false},ticks:{font:{size:9},color:c1,callback:function(v){return CUR_KPI==='ROAS'||CUR_KPI==='CPC'?v.toLocaleString()+'%':v.toLocaleString()+'원';}}},
      yC:{type:'linear',position:'right',grid:{display:false},border:{display:false},ticks:{font:{size:9},color:'#7F77DD',callback:function(v){return v.toFixed(1)+'%';}}}
    }
  }});

  if(ch2)ch2.destroy();
  // 차트2 — CPC 유형이면 목표CPC 수평선 추가
  var ds2=[
    {type:'bar',label:'소진액',data:rs(BS,n),backgroundColor:'#85B7EB',borderRadius:2,yAxisID:'yS',order:2},
    {type:'line',label:'CPC',data:rs(BCPC,n),borderColor:'#D85A30',backgroundColor:'transparent',borderWidth:2,pointRadius:n<=20?2:1,pointBackgroundColor:'#D85A30',tension:0.3,yAxisID:'yP',order:1}
  ];
  if(isCPC){
    ds2.push({type:'line',label:'목표선',data:Array(n).fill(goalVal),borderColor:'rgba(160,160,160,0.55)',backgroundColor:'transparent',borderWidth:0.8,borderDash:[6,4],pointRadius:0,pointHoverRadius:0,yAxisID:'yP',order:3,tension:0});
  }
  ch2=new Chart(document.getElementById('c2'),{plugins:[hoverBandPlugin],data:{labels:labels,datasets:ds2},
    options:{responsive:true,maintainAspectRatio:false,animation:{duration:200},interaction:{mode:'index',intersect:false},
    onClick:function(evt,elements,chart){var pts=chart.getElementsAtEventForMode(evt,'index',{intersect:false},true);if(pts&&pts.length){selSeg(pts[0].index);}},
    plugins:{legend:{display:false},tooltip:{enabled:false,external:chipTooltip('c2')}},
    scales:{x:{grid:{display:false},border:{display:false},ticks:{font:{size:9},color:'#9a9a94',maxRotation:0,autoSkip:true,maxTicksLimit:11}},
      yS:{type:'linear',position:'left',grid:{color:'rgba(0,0,0,0.04)'},border:{display:false},ticks:{font:{size:9},color:'#185FA5',callback:function(v){return v.toLocaleString();}}},
      yP:{type:'linear',position:'right',grid:{display:false},border:{display:false},ticks:{font:{size:9},color:'#D85A30',callback:function(v){return v+'원';}}}
    }
  }});
}


function selSeg(idx){
  si=idx;
  var step=100/N,avgCpc=Math.round(cv[idx]),recCpc=Math.round(avgCpc*1.114);
  var curRoas=rs(BR,N)[idx],curCvr=rs(BC,N)[idx],predCvr=rs(PC,N)[idx];
  var unitCnt=Math.round(UC[Math.min(Math.floor(idx*(20/N)),19)]);
  document.getElementById('bar-empty').style.display='none';
  document.getElementById('bar-sel').style.display='block';
  document.getElementById('b-badge').textContent=(idx+1)+'구간';
  document.getElementById('b-range').textContent=Math.round(idx*step)+'%-'+Math.round((idx+1)*step)+'%';
  document.getElementById('b-units').textContent='유닛 '+unitCnt+'개';
  document.getElementById('b-avg').textContent=avgCpc+'원';
  document.getElementById('b-rec').textContent=recCpc+'원';
  document.getElementById('rate').value=0;
  var ab=document.getElementById('apply-btn');if(ab)ab.disabled=true;
  document.getElementById('tc-c').textContent=avgCpc.toLocaleString()+'원';
  document.getElementById('tv-c').textContent=curCvr.toFixed(2)+'%';
  document.getElementById('tv-a').textContent='-';
  document.getElementById('tv-d').innerHTML='-';
  document.getElementById('tv-a').style.color='#1a1a18';
  document.getElementById('tr-c').textContent=curRoas.toLocaleString()+'%';
  document.getElementById('tk-c').textContent=Math.round(curRoas/TROAS*100)+'%';
  updateBar();
  if(ch1)ch1.update();if(ch2)ch2.update();
}

function clearSel(){si=-1;document.getElementById('bar-empty').style.display='flex';document.getElementById('bar-sel').style.display='none';if(ch1)ch1.update();if(ch2)ch2.update();}

function dH(val,unit){
  if(val===0) return '<span style="color:var(--color-text-muted);">-</span>';
  var c=val>0?'#185FA5':'#D85A30',s=val>0?'+':'';
  return '<span style="color:'+c+';font-weight:500;">'+s+val.toLocaleString()+unit+'</span>';
}

function updateBar(){
  if(si<0)return;
  var rate=parseFloat(document.getElementById('rate').value)||0;
  function sc(id,v){var e=document.getElementById(id);if(e)e.style.color=v===0?'#1a1a18':v>0?'#185FA5':'#D85A30';}
  var applyBtn=document.getElementById('apply-btn');
  if(rate===0){
    document.getElementById('tc-a').textContent='-';sc('tc-a',0);document.getElementById('tc-d').innerHTML='-';
    document.getElementById('tv-a').textContent='-';sc('tv-a',0);document.getElementById('tv-d').innerHTML='-';
    document.getElementById('tr-a').textContent='-';sc('tr-a',0);document.getElementById('tr-d').innerHTML='-';
    document.getElementById('tk-a').textContent='-';sc('tk-a',0);document.getElementById('tk-d').innerHTML='-';
    if(applyBtn)applyBtn.disabled=true;
    return;
  }
  var avgCpc=Math.round(cv[si]),newCpc=Math.round(avgCpc*(1+rate/100)),cpcDiff=newCpc-avgCpc;
  var curCvr=rs(BC,N)[si],newCvr=parseFloat((curCvr*(1+rate/100)).toFixed(2)),cvrDiff=parseFloat((newCvr-curCvr).toFixed(2));
  var curRoas=rs(BR,N)[si],newRoas=Math.round(avgCpc*curRoas/100/newCpc*100),roasDiff=newRoas-Math.round(curRoas);
  var baseAch=Math.round(curRoas/TROAS*100),newAch=Math.round(newRoas/TROAS*100),achDiff=newAch-baseAch;
  document.getElementById('tc-a').textContent=newCpc.toLocaleString()+'원';sc('tc-a',cpcDiff);document.getElementById('tc-d').innerHTML=dH(cpcDiff,'원');
  document.getElementById('tv-a').textContent=newCvr.toFixed(2)+'%';sc('tv-a',cvrDiff);document.getElementById('tv-d').innerHTML=dH(cvrDiff,'%p');
  document.getElementById('tr-a').textContent=newRoas.toLocaleString()+'%';sc('tr-a',roasDiff);document.getElementById('tr-d').innerHTML=dH(Math.round(roasDiff),'%');
  document.getElementById('tk-a').textContent=newAch+'%';sc('tk-a',achDiff);document.getElementById('tk-d').innerHTML=dH(achDiff,'%p');
  if(applyBtn)applyBtn.disabled=false;
}

function setN(n){
  N=n;si=-1;
  document.querySelectorAll('.seg-btn').forEach(function(b){b.classList.toggle('on',parseInt(b.dataset.n)===n);});
  cv=rs(BCPC,n);rCharts(n);
  document.getElementById('bar-empty').style.display='flex';
  document.getElementById('bar-sel').style.display='none';
  var ri=document.getElementById('rate');if(ri)ri.value=0;
  var ab=document.getElementById('apply-btn');if(ab)ab.disabled=true;
}

document.querySelectorAll('#panel-demo .seg-btn').forEach(function(b){b.addEventListener('click',function(){setN(parseInt(b.dataset.n));});});
document.getElementById('cx').onclick=clearSel;
document.getElementById('rm').onclick=function(){var inp=document.getElementById('rate');inp.value=(parseInt(inp.value)||0)-1;updateBar();};
document.getElementById('rp2').onclick=function(){var inp=document.getElementById('rate');inp.value=(parseInt(inp.value)||0)+1;updateBar();};
document.getElementById('rate').oninput=updateBar;

var bBtn=document.getElementById('base-btn');
var bPanel=document.getElementById('bep');
bBtn.onclick=function(){
  bPanel.classList.toggle('open');
  bBtn.classList.toggle('active', bPanel.classList.contains('open'));
};
document.getElementById('bep-cancel').onclick=function(){bPanel.classList.remove('open');bBtn.classList.remove('active');};
document.getElementById('bep-save').onclick=function(){
  var val=parseInt(document.getElementById('bep-inp').value)||320;
  document.getElementById('base-txt').textContent='기본 단가 '+val+'원';
  document.getElementById('cur-base').textContent=val+'원';
  bPanel.classList.remove('open');
  bBtn.classList.remove('active');
};
document.addEventListener('click',function(e){
  if(!e.target.closest('.base-wrap')){bPanel.classList.remove('open');bBtn.classList.remove('active');}
});

setN(20);
})();
</script>
<script>
(function(){
var BR=[1200,980,820,740,660,590,520,460,400,350,300,255,215,180,150,125,100,75,50,28];
var PR=[1106.1,1046.4,707.5,775.6,583.1,661.6,504.2,532.2,389.3,398.4,290.2,268.4,194.3,222.6,143.7,135.7,86.7,95,43.8,31.6];
var BC=[8.2,5.6,3.8,3.2,2.7,2.3,2.0,1.7,1.5,1.3,1.1,0.9,0.75,0.62,0.5,0.4,0.3,0.22,0.14,0.07];
var PC=[8.6,5.9,4.1,3.5,2.95,2.5,2.2,1.9,1.65,1.42,1.2,0.98,0.82,0.68,0.55,0.44,0.33,0.24,0.15,0.08];
var BS=[3200,2600,2100,1800,1550,1320,1100,920,760,620,500,400,310,240,180,130,90,58,32,12];
var BCPC=[280,255,232,212,194,178,163,149,136,124,113,103,93,84,76,68,61,54,46,38];
var UC=[48,46,44,42,40,38,36,34,32,30,28,26,24,22,20,18,16,14,12,10];
var TROAS=500,N=20,si=-1,cv=[],ch1=null,ch2=null;

function rs(d,n){
  var r=d.length/n;
  return Array.from({length:n},function(_,i){
    var s=Math.floor(i*r),e=Math.floor((i+1)*r);
    if(e<=s){
      var nearest=Math.min(Math.round(i*r),d.length-1);
      return d[nearest]||0;
    }
    var sl=d.slice(s,e);
    return parseFloat((sl.reduce(function(a,b){return a+b;},0)/sl.length).toFixed(2));
  });
}
function mkL(n){return Array.from({length:n},function(_,i){return Math.round(i*(100/n))+'%';});}
var ttColors={'ROAS':'#639922','예상 ROAS':'#A8D78A','전환율':'#7F77DD','예상 전환율':'#B5B0EE','소진액':'#185FA5','CPC':'#D85A30'};
var tt={backgroundColor:'#fff',borderColor:'rgba(0,0,0,0.1)',borderWidth:1,titleColor:'#1a1a18',titleFont:{size:12,weight:'700'},bodyColor:'#6b6b66',bodyFont:{size:13,weight:'600'},padding:10,cornerRadius:8,displayColors:true,boxWidth:7,boxHeight:7,usePointStyle:true,footerColor:'#1a1a18',footerFont:{size:12,weight:'700'},footerMarginTop:6,callbacks:{labelTextColor:function(ctx){
    if(ctx.dataset.label==='큰값') return '#639922';
    if(ctx.dataset.label==='작은값') return '#A8D78A';
    return ttColors[ctx.dataset.label]||'#1a1a18';
  }}};
var hoverBandPlugin={id:'hoverBand',beforeDatasetsDraw:function(chart){
  var ca=chart.chartArea,n=chart.data.labels.length,colW=ca.width/n,ctx=chart.ctx;
  // 선택된 구간 밴드 (호버와 동일한 색상)
  if(si>=0){
    var sx=ca.left+si*colW;
    ctx.save();ctx.fillStyle='rgba(0,0,0,0.05)';ctx.fillRect(sx,ca.top,colW,ca.height);ctx.restore();
  }
  // 마우스 호버 밴드
  var active=chart.getActiveElements();
  if(!active||!active.length)return;
  var idx=active[0].index;
  var x=ca.left+idx*colW;
  ctx.save();ctx.fillStyle='rgba(0,0,0,0.05)';ctx.fillRect(x,ca.top,colW,ca.height);ctx.restore();
}};


function rCharts(n){
  var labels=mkL(n),step=100/n;
  function tCb(items){var i=items[0].dataIndex;return (i+1)+'구간  '+Math.round(i*step)+'%'+String.fromCharCode(8211)+Math.round((i+1)*step)+'%';}
  if(ch1)ch1.destroy();
  ch1=new Chart(document.getElementById('s-c1'),{plugins:[hoverBandPlugin],data:{labels:labels,datasets:[
    {type:'bar',label:'큰값',data:rs(BR,n).map(function(v,i){return Math.max(v, rs(PR,n)[i]);}),backgroundColor:rs(BR,n).map(function(v,i){return v>=rs(PR,n)[i] ? '#639922' : '#A8D78A';}),borderRadius:2,yAxisID:'yR',order:4,barPercentage:0.82,categoryPercentage:0.82,grouped:false,__rawROAS:rs(BR,n),__rawPRED:rs(PR,n)},
    {type:'bar',label:'작은값',data:rs(BR,n).map(function(v,i){return Math.min(v, rs(PR,n)[i]);}),backgroundColor:rs(BR,n).map(function(v,i){return v<=rs(PR,n)[i] ? '#639922' : '#A8D78A';}),borderRadius:2,yAxisID:'yR',order:3,barPercentage:0.82,categoryPercentage:0.82,grouped:false,__rawROAS:rs(BR,n),__rawPRED:rs(PR,n)},
    {type:'line',label:'전환율',data:rs(BC,n),borderColor:'#7F77DD',backgroundColor:'transparent',borderWidth:2,pointRadius:n<=20?2:1,pointBackgroundColor:'#7F77DD',tension:0.3,yAxisID:'yC',order:2},
    {type:'line',label:'예상 전환율',data:rs(PC,n),borderColor:'#B5B0EE',backgroundColor:'transparent',borderWidth:2,borderDash:[4,3],pointRadius:n<=20?2:1,pointBackgroundColor:'#B5B0EE',tension:0.3,yAxisID:'yC',order:1},
    {type:'line',label:'목표 ROAS',data:Array(n).fill(TROAS),borderColor:'rgba(160,160,160,0.55)',backgroundColor:'transparent',borderWidth:0.8,borderDash:[6,4],pointRadius:0,pointHoverRadius:0,yAxisID:'yR',order:5,tension:0}
  ]},options:{responsive:true,maintainAspectRatio:false,animation:{duration:200},interaction:{mode:'index',intersect:false},onClick:function(evt,elements,chart){var pts=chart.getElementsAtEventForMode(evt,'index',{intersect:false},true);if(pts&&pts.length){selSeg(pts[0].index);}},
    plugins:{legend:{display:false},tooltip:{enabled:false,external:chipTooltip('s-c1')}},
    scales:{x:{grid:{display:false},border:{display:false},ticks:{font:{size:9},color:'#9a9a94',maxRotation:0,autoSkip:true,maxTicksLimit:11}},
      yR:{type:'linear',position:'left',grid:{color:'rgba(0,0,0,0.04)'},border:{display:false},ticks:{font:{size:9},color:'#639922',callback:function(v){return v.toLocaleString()+'%';}}},
      yC:{type:'linear',position:'right',grid:{display:false},border:{display:false},ticks:{font:{size:9},color:'#7F77DD',callback:function(v){return v.toFixed(1)+'%';}}}
    }
  }});
  if(ch2)ch2.destroy();
  ch2=new Chart(document.getElementById('s-c2'),{plugins:[hoverBandPlugin],data:{labels:labels,datasets:[
    {type:'bar',label:'소진액',data:rs(BS,n),backgroundColor:'#85B7EB',borderRadius:2,yAxisID:'yS',order:2},
    {type:'line',label:'CPC',data:rs(BCPC,n),borderColor:'#D85A30',backgroundColor:'transparent',borderWidth:2,pointRadius:n<=20?2:1,pointBackgroundColor:'#D85A30',tension:0.3,yAxisID:'yP',order:1}
  ]},options:{responsive:true,maintainAspectRatio:false,animation:{duration:200},interaction:{mode:'index',intersect:false},onClick:function(evt,elements,chart){var pts=chart.getElementsAtEventForMode(evt,'index',{intersect:false},true);if(pts&&pts.length){selSeg(pts[0].index);}},
    plugins:{legend:{display:false},tooltip:{enabled:false,external:chipTooltip('s-c2')}},
    scales:{x:{grid:{display:false},border:{display:false},ticks:{font:{size:9},color:'#9a9a94',maxRotation:0,autoSkip:true,maxTicksLimit:11}},
      yS:{type:'linear',position:'left',grid:{color:'rgba(0,0,0,0.04)'},border:{display:false},ticks:{font:{size:9},color:'#185FA5',callback:function(v){return v.toLocaleString();}}},
      yP:{type:'linear',position:'right',grid:{display:false},border:{display:false},ticks:{font:{size:9},color:'#D85A30',callback:function(v){return v+'원';}}}
    }
  }});
}


function selSeg(idx){
  si=idx;
  var step=100/N,avgCpc=Math.round(cv[idx]),recCpc=Math.round(avgCpc*1.114);
  var curRoas=rs(BR,N)[idx],curCvr=rs(BC,N)[idx],predCvr=rs(PC,N)[idx];
  var unitCnt=Math.round(UC[Math.min(Math.floor(idx*(20/N)),19)]);
  document.getElementById('s-bar-empty').style.display='none';
  document.getElementById('s-bar-sel').style.display='block';
  document.getElementById('s-b-badge').textContent=(idx+1)+'구간';
  document.getElementById('s-b-range').textContent=Math.round(idx*step)+'%-'+Math.round((idx+1)*step)+'%';
  document.getElementById('s-b-units').textContent='유닛 '+unitCnt+'개';
  document.getElementById('s-b-avg').textContent=avgCpc+'원';
  document.getElementById('s-b-rec').textContent=recCpc+'원';
  document.getElementById('s-rate').value=0;
  var ab=document.getElementById('s-apply-btn');if(ab)ab.disabled=true;
  document.getElementById('s-tc-c').textContent=avgCpc.toLocaleString()+'원';
  document.getElementById('s-tv-c').textContent=curCvr.toFixed(2)+'%';
  document.getElementById('s-tv-a').textContent='-';
  document.getElementById('s-tv-d').innerHTML='-';
  document.getElementById('s-tv-a').style.color='#1a1a18';
  document.getElementById('s-tr-c').textContent=curRoas.toLocaleString()+'%';
  document.getElementById('s-tk-c').textContent=Math.round(curRoas/TROAS*100)+'%';
  updateBar();
  if(ch1)ch1.update();if(ch2)ch2.update();
}

function clearSel(){si=-1;document.getElementById('s-bar-empty').style.display='flex';document.getElementById('s-bar-sel').style.display='none';if(ch1)ch1.update();if(ch2)ch2.update();}

function dH(val,unit){
  if(val===0) return '<span style="color:var(--color-text-muted);">-</span>';
  var c=val>0?'#185FA5':'#D85A30',s=val>0?'+':'';
  return '<span style="color:'+c+';font-weight:500;">'+s+val.toLocaleString()+unit+'</span>';
}

function updateBar(){
  if(si<0)return;
  var rate=parseFloat(document.getElementById('s-rate').value)||0;
  function sc(id,v){var e=document.getElementById(id);if(e)e.style.color=v===0?'#1a1a18':v>0?'#185FA5':'#D85A30';}
  var applyBtn=document.getElementById('s-apply-btn');
  if(rate===0){
    document.getElementById('s-tc-a').textContent='-';sc('s-tc-a',0);document.getElementById('s-tc-d').innerHTML='-';
    document.getElementById('s-tv-a').textContent='-';sc('s-tv-a',0);document.getElementById('s-tv-d').innerHTML='-';
    document.getElementById('s-tr-a').textContent='-';sc('s-tr-a',0);document.getElementById('s-tr-d').innerHTML='-';
    document.getElementById('s-tk-a').textContent='-';sc('s-tk-a',0);document.getElementById('s-tk-d').innerHTML='-';
    if(applyBtn)applyBtn.disabled=true;
    return;
  }
  var avgCpc=Math.round(cv[si]),newCpc=Math.round(avgCpc*(1+rate/100)),cpcDiff=newCpc-avgCpc;
  var curCvr=rs(BC,N)[si],newCvr=parseFloat((curCvr*(1+rate/100)).toFixed(2)),cvrDiff=parseFloat((newCvr-curCvr).toFixed(2));
  var curRoas=rs(BR,N)[si],newRoas=Math.round(avgCpc*curRoas/100/newCpc*100),roasDiff=newRoas-Math.round(curRoas);
  var baseAch=Math.round(curRoas/TROAS*100),newAch=Math.round(newRoas/TROAS*100),achDiff=newAch-baseAch;
  document.getElementById('s-tc-a').textContent=newCpc.toLocaleString()+'원';sc('s-tc-a',cpcDiff);document.getElementById('s-tc-d').innerHTML=dH(cpcDiff,'원');
  document.getElementById('s-tv-a').textContent=newCvr.toFixed(2)+'%';sc('s-tv-a',cvrDiff);document.getElementById('s-tv-d').innerHTML=dH(cvrDiff,'%p');
  document.getElementById('s-tr-a').textContent=newRoas.toLocaleString()+'%';sc('s-tr-a',roasDiff);document.getElementById('s-tr-d').innerHTML=dH(Math.round(roasDiff),'%');
  document.getElementById('s-tk-a').textContent=newAch+'%';sc('s-tk-a',achDiff);document.getElementById('s-tk-d').innerHTML=dH(achDiff,'%p');
  if(applyBtn)applyBtn.disabled=false;
}

function setN(n){
  N=n;si=-1;
  document.querySelectorAll('.seg-btn').forEach(function(b){b.classList.toggle('on',parseInt(b.dataset.n)===n);});
  cv=rs(BCPC,n);rCharts(n);
  document.getElementById('s-bar-empty').style.display='flex';
  document.getElementById('s-bar-sel').style.display='none';
  var ri=document.getElementById('s-rate');if(ri)ri.value=0;
  var ab=document.getElementById('s-apply-btn');if(ab)ab.disabled=true;
}

document.querySelectorAll('#panel-spec .seg-btn').forEach(function(b){b.addEventListener('click',function(){setN(parseInt(b.dataset.n));});});
document.getElementById('s-cx').onclick=clearSel;
document.getElementById('s-rm').onclick=function(){var inp=document.getElementById('s-rate');inp.value=(parseInt(inp.value)||0)-1;updateBar();};
document.getElementById('s-rp2').onclick=function(){var inp=document.getElementById('s-rate');inp.value=(parseInt(inp.value)||0)+1;updateBar();};
document.getElementById('s-rate').oninput=updateBar;

var bBtn=document.getElementById('s-base-btn');
var bPanel=document.getElementById('s-bep');
bBtn.onclick=function(){
  bPanel.classList.toggle('open');
  bBtn.classList.toggle('active', bPanel.classList.contains('open'));
};
document.getElementById('s-bep-cancel').onclick=function(){bPanel.classList.remove('open');bBtn.classList.remove('active');};
document.getElementById('s-bep-save').onclick=function(){
  var val=parseInt(document.getElementById('s-bep-inp').value)||320;
  document.getElementById('s-base-txt').textContent='기본 단가 '+val+'원';
  document.getElementById('s-cur-base').textContent=val+'원';
  bPanel.classList.remove('open');
  bBtn.classList.remove('active');
};
document.addEventListener('click',function(e){
  if(!e.target.closest('.base-wrap')){bPanel.classList.remove('open');bBtn.classList.remove('active');}
});

setN(20);
})();
</script>
<script>
document.querySelectorAll('.tab').forEach(function(tab){
  tab.addEventListener('click',function(){
    document.querySelectorAll('.tab').forEach(function(t){t.classList.remove('tab--active');});
    document.querySelectorAll('.panel').forEach(function(p){p.classList.remove('panel--active');});
    tab.classList.add('tab--active');
    document.getElementById('panel-'+tab.dataset.tab).classList.add('panel--active');
  });
});
</script>
</body>
</html>
