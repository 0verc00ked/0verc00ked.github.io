<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Lupid Prototype</title>
  <link rel="icon" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 64 64'%3E%3Crect width='64' height='64' rx='14' fill='%23101012'/%3E%3Cpath d='M14 23h28' stroke='%23ff9548' stroke-width='4' stroke-linecap='round'/%3E%3Ccircle cx='42' cy='22' r='6' fill='%2386b9ff'/%3E%3C/svg%3E" />
  <style>
    :root {
      --bg: #0b0c0f;
      --shell: #121316;
      --shell-2: #17191d;
      --panel: #17191d;
      --panel-2: #1c1f24;
      --panel-3: #14161a;
      --line: #262a31;
      --line-soft: #2e333c;
      --text: #f2f4f7;
      --soft: #a8aebb;
      --muted: #707887;
      --orange: #f38a42;
      --orange-soft: rgba(243, 138, 66, 0.16);
      --orange-strong: rgba(243, 138, 66, 0.34);
      --blue: #a6c2ff;
      --blue-soft: rgba(166, 194, 255, 0.14);
      --green: #8fd0ab;
      --green-soft: rgba(143, 208, 171, 0.16);
      --violet: #9b7bff;
      --violet-soft: rgba(155, 123, 255, 0.14);
      --red: #df6c75;
      --red-soft: rgba(223, 108, 117, 0.14);
      --radius-xl: 26px;
      --radius-lg: 20px;
      --radius-md: 16px;
      --radius-sm: 12px;
      --shadow: 0 28px 90px rgba(0, 0, 0, 0.34);
      --card-shadow: 0 20px 50px rgba(0, 0, 0, 0.26);
      --max: 1560px;
      --sans: Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      --mono: "IBM Plex Mono", ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;
    }

    * { box-sizing: border-box; }
    html, body {
      margin: 0;
      min-height: 100%;
      background:
        radial-gradient(circle at top left, rgba(251,139,59,0.06), transparent 26%),
        radial-gradient(circle at top right, rgba(126,174,248,0.05), transparent 22%),
        linear-gradient(180deg, #0e0f12 0%, #090a0d 100%);
      color: var(--text);
      font-family: var(--sans);
    }
    body::before {
      content: "";
      position: fixed;
      inset: 0;
      background:
        linear-gradient(90deg, rgba(255,255,255,0.02) 1px, transparent 1px),
        linear-gradient(rgba(255,255,255,0.015) 1px, transparent 1px);
      background-size: 92px 92px;
      mask-image: linear-gradient(180deg, rgba(0,0,0,.42), transparent 92%);
      pointer-events: none;
    }
    a { color: inherit; text-decoration: none; }
    button, input { font: inherit; }

    .shell {
      max-width: var(--max);
      margin: 0 auto;
      padding: 18px;
    }

    .app {
      display: grid;
      grid-template-columns: 248px minmax(0, 1fr);
      min-height: calc(100vh - 36px);
      border: 1px solid #302721;
      border-radius: 28px;
      background: linear-gradient(180deg, rgba(17,18,22,0.98), rgba(14,15,18,0.98));
      box-shadow: var(--shadow);
      overflow: hidden;
    }

    .sidebar {
      display: flex;
      flex-direction: column;
      padding: 14px 16px 18px;
      border-right: 1px solid var(--line);
      background: linear-gradient(180deg, rgba(17,18,21,.98), rgba(14,15,18,.98));
    }

    .brand {
      display: flex;
      align-items: center;
      gap: 12px;
      min-height: 54px;
      padding-bottom: 14px;
      margin-bottom: 16px;
      border-bottom: 1px solid var(--line);
    }

    .brand-lock {
      width: 42px;
      height: 42px;
      flex: 0 0 auto;
      border-radius: 14px;
      border: 1px solid var(--line-soft);
      background: linear-gradient(180deg, rgba(34,36,42,.9), rgba(18,20,24,.96));
      display: grid;
      place-items: center;
      box-shadow: inset 0 1px 0 rgba(255,255,255,.05);
      overflow: hidden;
    }

    .brand-lock svg {
      width: 30px;
      height: 30px;
      display: block;
    }

    .brand h1 {
      margin: 0;
      font-size: 14px;
      letter-spacing: .06em;
      text-transform: uppercase;
    }

    .brand p {
      margin: 3px 0 0;
      color: var(--muted);
      font-size: 11px;
      line-height: 1.35;
    }

    .brand-word {
      font-size: 24px;
      font-weight: 800;
      letter-spacing: -.05em;
      line-height: 1;
      margin-bottom: 3px;
    }

    .nav-group + .nav-group { margin-top: 14px; }

    .group-label {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin: 0 0 8px;
      color: var(--muted);
      font-size: 10px;
      font-family: var(--mono);
      text-transform: uppercase;
      letter-spacing: .12em;
    }

    .nav-list {
      display: grid;
      gap: 4px;
      margin-left: 14px;
      padding-left: 10px;
      border-left: 1px solid rgba(255,255,255,.08);
    }

    .nav-item {
      width: 100%;
      display: grid;
      grid-template-columns: 34px minmax(0, 1fr) auto;
      align-items: center;
      gap: 12px;
      min-height: 48px;
      padding: 6px 8px;
      border-radius: 14px;
      border: 1px solid transparent;
      background: rgba(255,255,255,.015);
      color: var(--soft);
      text-align: left;
      cursor: pointer;
      transition: 160ms ease;
      backdrop-filter: blur(12px);
      -webkit-backdrop-filter: blur(12px);
    }

    .nav-item:hover {
      border-color: #343a43;
      background: rgba(255,255,255,.028);
      color: var(--text);
    }

    .nav-item.active {
      border-color: #564131;
      background:
        linear-gradient(180deg, rgba(255,255,255,.05), rgba(0,0,0,.04)),
        linear-gradient(90deg, rgba(251,139,59,.30), rgba(251,139,59,.08) 38%, transparent 74%);
      box-shadow:
        inset 0 1px 0 rgba(255,255,255,.06),
        0 10px 24px rgba(0,0,0,.18),
        0 0 0 1px rgba(251,139,59,.06);
      color: var(--text);
    }

    .nav-icon {
      width: 34px;
      height: 34px;
      display: grid;
      place-items: center;
      border-radius: 12px;
      border: 1px solid var(--line);
      background: linear-gradient(180deg, rgba(32,35,41,.92), rgba(18,20,24,.96));
      color: #d2d7e2;
      font-size: 12px;
      font-family: var(--mono);
      backdrop-filter: blur(10px);
      -webkit-backdrop-filter: blur(10px);
    }

    .nav-icon svg {
      width: 16px;
      height: 16px;
      display: block;
      stroke: currentColor;
      fill: none;
      stroke-width: 1.9;
      stroke-linecap: round;
      stroke-linejoin: round;
    }

    .nav-item.active .nav-icon {
      border-color: #544233;
      background: linear-gradient(180deg, rgba(251,139,59,.22), rgba(255,255,255,.03));
      color: #fff0e6;
    }

    .nav-item strong {
      display: block;
      font-size: 13px;
      letter-spacing: -.02em;
    }

    .nav-item span {
      display: block;
      margin-top: 1px;
      color: var(--muted);
      font-size: 10.5px;
    }

    .nav-count {
      min-width: 28px;
      height: 28px;
      padding: 0 8px;
      display: inline-grid;
      place-items: center;
      border-radius: 999px;
      border: 1px solid var(--line);
      background: rgba(255,255,255,.02);
      color: var(--text);
      font-size: 11px;
      font-family: var(--mono);
    }

    .nav-note {
      padding: 14px;
      border-radius: 20px;
      border: 1px solid rgba(255,255,255,.08);
      background:
        radial-gradient(circle at top left, rgba(251,139,59,.2), transparent 42%),
        linear-gradient(180deg, rgba(36,39,45,.9), rgba(21,23,28,.94));
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      margin-top: auto;
      box-shadow: inset 0 1px 0 rgba(255,255,255,.06), var(--card-shadow);
    }

    .nav-note h3 {
      margin: 0 0 8px;
      font-size: 15px;
      letter-spacing: -.02em;
    }

    .nav-note p {
      margin: 0;
      color: var(--soft);
      font-size: 13px;
      line-height: 1.5;
    }

    .main {
      padding: 18px;
      overflow: auto;
    }

    .topbar {
      display: grid;
      grid-template-columns: minmax(0, 1fr) minmax(260px, 320px) auto;
      gap: 14px;
      align-items: center;
      min-height: 68px;
      padding: 14px 16px;
      border-radius: 18px;
      border: 1px solid var(--line);
      background: linear-gradient(180deg, rgba(28,30,35,.76), rgba(18,19,23,.9));
      margin-bottom: 16px;
      backdrop-filter: blur(18px);
      -webkit-backdrop-filter: blur(18px);
      box-shadow: inset 0 1px 0 rgba(255,255,255,.05);
    }

    .topbar h2 {
      margin: 0;
      font-size: 18px;
      letter-spacing: -.03em;
    }

    .topbar p {
      margin: 4px 0 0;
      color: var(--muted);
      font-size: 12px;
    }

    .search {
      width: 100%;
      min-height: 40px;
      display: flex;
      align-items: center;
      gap: 10px;
      padding: 0 14px;
      border-radius: 14px;
      border: 1px solid var(--line);
      background: rgba(255,255,255,.035);
      color: var(--muted);
      font-size: 13px;
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      box-shadow: inset 0 1px 0 rgba(255,255,255,.04);
    }

    .top-pills {
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
      justify-content: flex-end;
    }

    .pill {
      min-height: 34px;
      display: inline-flex;
      align-items: center;
      gap: 8px;
      padding: 0 12px;
      border-radius: 999px;
      border: 1px solid var(--line);
      background: rgba(255,255,255,.03);
      color: var(--soft);
      font-size: 11px;
      font-weight: 700;
      font-family: var(--mono);
      text-transform: uppercase;
      letter-spacing: .06em;
    }

    .pill strong { color: var(--text); }
    .dot { width: 8px; height: 8px; border-radius: 999px; display: inline-block; background: currentColor; }

    .screen { display: none; animation: fade .18s ease; }
    .screen.active { display: block; }

    @keyframes fade {
      from { opacity: 0; transform: translateY(8px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .hero {
      padding: 26px 24px 22px;
      border-radius: 24px;
      border: 1px solid rgba(255,255,255,.075);
      background:
        radial-gradient(circle at top left, rgba(255,255,255,.05), transparent 32%),
        linear-gradient(180deg, rgba(34,37,43,.78), rgba(18,20,24,.94));
      margin-bottom: 16px;
      backdrop-filter: blur(18px);
      -webkit-backdrop-filter: blur(18px);
      box-shadow: inset 0 1px 0 rgba(255,255,255,.06), var(--card-shadow);
    }

    .hero-top {
      display: flex;
      justify-content: space-between;
      gap: 14px;
      align-items: flex-start;
      flex-wrap: wrap;
    }

    .eyebrow {
      display: inline-flex;
      align-items: center;
      min-height: 34px;
      padding: 0 14px;
      border-radius: 999px;
      border: 1px solid var(--line-soft);
      background: rgba(255,255,255,.03);
      color: var(--soft);
      font-size: 11px;
      font-family: var(--mono);
      text-transform: uppercase;
      letter-spacing: .08em;
    }

    .hero h3 {
      margin: 14px 0 8px;
      font-size: 30px;
      line-height: 1.02;
      letter-spacing: -.06em;
      max-width: 980px;
    }

    .hero p {
      margin: 0;
      color: var(--soft);
      font-size: 15px;
      line-height: 1.55;
    }

    .hero-copy {
      max-width: 1040px;
    }

    .badge {
      display: inline-flex;
      align-items: center;
      min-height: 36px;
      padding: 0 12px;
      border-radius: 999px;
      border: 1px solid transparent;
      font-size: 11px;
      font-weight: 700;
      font-family: var(--mono);
      text-transform: uppercase;
      letter-spacing: .06em;
    }

    .green { color: var(--green); background: var(--green-soft); border-color: rgba(111,200,143,.18); }
    .blue { color: var(--blue); background: var(--blue-soft); border-color: rgba(126,174,248,.18); }
    .amber { color: var(--orange); background: var(--orange-soft); border-color: rgba(251,139,59,.18); }
    .violet { color: var(--violet); background: var(--violet-soft); border-color: rgba(155,123,255,.18); }
    .red { color: var(--red); background: var(--red-soft); border-color: rgba(223,108,117,.18); }

    .cta-row, .tabs, .filters {
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
    }

    .tabs { margin-top: 16px; }

    .tab, .chip-btn, .btn {
      min-height: 40px;
      padding: 0 14px;
      border-radius: 14px;
      border: 1px solid rgba(255,255,255,.08);
      background:
        linear-gradient(180deg, rgba(255,255,255,.035), rgba(255,255,255,.012)),
        rgba(19,21,26,.88);
      color: var(--soft);
      cursor: pointer;
      transition: 150ms ease;
      backdrop-filter: blur(14px);
      -webkit-backdrop-filter: blur(14px);
      box-shadow: inset 0 1px 0 rgba(255,255,255,.05);
    }

    .tab:hover, .chip-btn:hover, .btn:hover { color: var(--text); border-color: rgba(255,255,255,.13); }
    .tab.active {
      color: var(--text);
      border-color: rgba(243,138,66,.26);
      background:
        radial-gradient(circle at top left, rgba(251,139,59,.18), transparent 70%),
        linear-gradient(180deg, rgba(251,139,59,.16), rgba(255,255,255,.03)),
        rgba(255,255,255,.02);
    }

    .btn.primary {
      background: linear-gradient(180deg, #f99553, #dd7b38);
      border-color: #c16c33;
      color: #1a1008;
      font-weight: 800;
    }

    .summary-strip {
      display: grid;
      grid-template-columns: repeat(6, minmax(0, 1fr));
      gap: 12px;
      margin-top: 18px;
    }

    .summary {
      position: relative;
      min-height: 122px;
      padding: 16px;
      border-radius: 22px;
      border: 1px solid rgba(255,255,255,.08);
      background:
        radial-gradient(circle at top left, rgba(255,255,255,.045), transparent 44%),
        linear-gradient(180deg, rgba(36,39,45,.84), rgba(20,22,27,.92));
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      box-shadow: inset 0 1px 0 rgba(255,255,255,.06), var(--card-shadow);
    }

    .summary::before {
      content: "";
      position: absolute;
      left: 16px;
      right: 16px;
      top: 0;
      height: 1px;
      background: linear-gradient(90deg, rgba(255,255,255,.18), transparent 70%);
      opacity: .45;
    }

    .summary::after {
      content: "";
      position: absolute;
      left: 16px;
      top: 16px;
      width: 34px;
      height: 4px;
      border-radius: 999px;
      background: rgba(255,255,255,.14);
      opacity: .9;
    }

    .summary small, .label {
      display: block;
      margin: 12px 0 10px;
      color: var(--muted);
      font-size: 10px;
      font-family: var(--mono);
      text-transform: uppercase;
      letter-spacing: .12em;
    }

    .summary strong {
      display: block;
      font-size: 22px;
      line-height: 1.05;
      letter-spacing: -.04em;
    }

    .summary em {
      display: block;
      margin-top: 7px;
      color: var(--muted);
      font-style: normal;
      font-size: 12px;
      line-height: 1.45;
    }

    .stats-4, .stats-3, .grid-top, .grid-2, .grid-3, .scope, .zenith-lower, .zenith-main, .zenith-bottom {
      display: grid;
      gap: 14px;
      margin-bottom: 14px;
    }

    .stats-4 { grid-template-columns: repeat(4, minmax(0, 1fr)); }
    .stats-3 { grid-template-columns: repeat(3, minmax(0, 1fr)); }
    .grid-top { grid-template-columns: minmax(0, 2.2fr) minmax(300px, .9fr); }
    .grid-2 { grid-template-columns: repeat(2, minmax(0, 1fr)); }
    .grid-3 { grid-template-columns: repeat(3, minmax(0, 1fr)); }
    .scope { grid-template-columns: 320px minmax(0, 1fr); }
    .zenith-lower { grid-template-columns: 1.2fr 1.1fr .9fr; }
    .zenith-main { grid-template-columns: minmax(0, 1.9fr) minmax(340px, .95fr); }
    .zenith-bottom { grid-template-columns: 1.15fr .95fr .9fr; }

    .panel {
      position: relative;
      border-radius: 24px;
      border: 1px solid rgba(255,255,255,.08);
      background:
        radial-gradient(circle at top left, rgba(255,255,255,.04), transparent 40%),
        linear-gradient(180deg, rgba(35,38,44,.82), rgba(18,20,24,.94));
      overflow: hidden;
      backdrop-filter: blur(18px);
      -webkit-backdrop-filter: blur(18px);
      box-shadow: inset 0 1px 0 rgba(255,255,255,.06), var(--card-shadow);
    }

    .panel::before {
      content: "";
      position: absolute;
      inset: 0 0 auto 0;
      height: 1px;
      background: linear-gradient(90deg, rgba(255,255,255,.18), transparent 66%);
      opacity: .48;
      pointer-events: none;
    }

    .panel-head {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      gap: 12px;
      padding: 16px 18px 14px;
      border-bottom: 1px solid rgba(255,255,255,.06);
    }

    .panel-head h4 {
      margin: 0;
      font-size: 15px;
      letter-spacing: -.02em;
    }

    .panel-head span {
      color: var(--muted);
      font-size: 11px;
      font-family: var(--mono);
    }

    .panel-body { padding: 16px 18px 18px; }

    .focus-list {
      display: grid;
      gap: 10px;
    }

    .focus-item {
      display: grid;
      grid-template-columns: minmax(0, 1fr) auto;
      gap: 12px;
      padding: 16px;
      border-radius: 18px;
      border: 1px solid rgba(255,255,255,.07);
      background:
        linear-gradient(180deg, rgba(255,255,255,.03), rgba(255,255,255,.015)),
        rgba(17,19,23,.82);
      box-shadow: inset 0 1px 0 rgba(255,255,255,.05);
    }

    .focus-item h5 {
      margin: 0 0 4px;
      font-size: 15px;
      letter-spacing: -.02em;
    }

    .focus-item p {
      margin: 0;
      color: var(--soft);
      font-size: 13px;
      line-height: 1.45;
    }

    .focus-meta {
      margin-top: 8px;
      color: var(--muted);
      font-size: 11px;
      font-family: var(--mono);
    }

    .mini-stat-row {
      display: grid;
      grid-template-columns: repeat(4, minmax(0, 1fr));
      gap: 12px;
      margin-top: 12px;
    }

    .mini-stat {
      padding: 14px 15px;
      border-radius: 18px;
      border: 1px solid rgba(255,255,255,.07);
      background:
        linear-gradient(180deg, rgba(255,255,255,.03), rgba(255,255,255,.012)),
        rgba(17,19,23,.82);
    }

    .mini-stat strong {
      display: block;
      font-size: 20px;
      letter-spacing: -.03em;
      margin: 6px 0 2px;
    }

    .stack-bar {
      display: flex;
      height: 10px;
      overflow: hidden;
      border-radius: 999px;
      background: rgba(255,255,255,.05);
      margin-top: 12px;
    }

    .stack-bar span { display: block; height: 100%; }

    .metric-card {
      position: relative;
      padding: 16px 18px;
      border-radius: 22px;
      border: 1px solid rgba(255,255,255,.08);
      background:
        radial-gradient(circle at top left, rgba(255,255,255,.04), transparent 44%),
        linear-gradient(180deg, rgba(36,39,45,.82), rgba(18,20,24,.92));
      box-shadow: inset 0 1px 0 rgba(255,255,255,.05), var(--card-shadow);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
    }

    .metric-card::after {
      content: "";
      position: absolute;
      left: 18px;
      top: 16px;
      width: 38px;
      height: 4px;
      border-radius: 999px;
      background: rgba(255,255,255,.12);
    }

    .metric-card .value {
      margin: 14px 0 6px;
      font-size: 28px;
      line-height: 1;
      letter-spacing: -.05em;
      font-weight: 800;
    }

    .metric-card p {
      margin: 0;
      color: var(--soft);
      font-size: 13px;
    }

    .chart {
      height: 250px;
      border-radius: 22px;
      border: 1px solid rgba(255,255,255,.07);
      background:
        linear-gradient(rgba(255,255,255,.04) 1px, transparent 1px) 0 0 / 100% 25%,
        linear-gradient(90deg, rgba(255,255,255,.03) 1px, transparent 1px) 0 0 / 16.6% 100%,
        linear-gradient(180deg, rgba(19,21,25,.9), rgba(15,16,20,.96));
      overflow: hidden;
      position: relative;
      box-shadow: inset 0 1px 0 rgba(255,255,255,.04);
    }

    .chart::after {
      content: "";
      position: absolute;
      inset: 0;
      background: radial-gradient(circle at 70% 0%, rgba(243,138,66,.08), transparent 35%);
      pointer-events: none;
    }

    .chart svg { width: 100%; height: 100%; display: block; }

    .donut-wrap {
      display: flex;
      align-items: center;
      gap: 16px;
      flex-wrap: wrap;
    }

    .donut {
      width: 156px;
      height: 156px;
      flex: 0 0 auto;
    }

    .legend {
      display: grid;
      gap: 10px;
      min-width: 170px;
    }

    .legend-row {
      display: flex;
      justify-content: space-between;
      gap: 10px;
      align-items: center;
      font-size: 13px;
      color: var(--soft);
    }

    .legend-row em {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      font-style: normal;
    }

    .legend-row i {
      width: 8px;
      height: 8px;
      border-radius: 999px;
      display: inline-block;
      background: currentColor;
    }

    .legend-row strong { color: var(--text); }

    .stack {
      display: grid;
      gap: 12px;
    }

    .signal {
      position: relative;
      padding: 16px 18px;
      border-radius: 20px;
      border: 1px solid rgba(255,255,255,.07);
      background:
        linear-gradient(180deg, rgba(255,255,255,.03), rgba(255,255,255,.012)),
        rgba(18,20,24,.88);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      box-shadow: inset 0 1px 0 rgba(255,255,255,.05);
    }

    .signal::before {
      content: "";
      position: absolute;
      left: 14px;
      top: 12px;
      width: 7px;
      height: 7px;
      border-radius: 999px;
      background: rgba(243,138,66,.75);
      box-shadow: 0 0 12px rgba(243,138,66,.28);
    }

    .signal h5, .signal p, .signal .micro { padding-left: 14px; }

    .mini-stack {
      display: grid;
      gap: 12px;
    }

    .mini-grid {
      display: grid;
      gap: 12px;
      grid-template-columns: 1fr 1fr;
    }

    .signal h5 {
      margin: 0 0 6px;
      font-size: 16px;
      letter-spacing: -.02em;
    }

    .signal p {
      margin: 0;
      color: var(--soft);
      font-size: 13px;
      line-height: 1.48;
    }

    .signal .micro {
      margin-top: 10px;
      color: var(--muted);
      font-size: 11px;
      font-family: var(--mono);
    }

    table {
      width: 100%;
      border-collapse: separate;
      border-spacing: 0 8px;
      font-size: 13px;
    }

    th, td {
      padding: 14px 12px;
      border-bottom: 0;
      text-align: left;
      vertical-align: top;
    }

    th {
      color: var(--muted);
      font-size: 11px;
      font-family: var(--mono);
      text-transform: uppercase;
      letter-spacing: .08em;
      font-weight: 600;
    }

    tbody td {
      background:
        linear-gradient(180deg, rgba(255,255,255,.028), rgba(255,255,255,.012)),
        rgba(16,18,22,.86);
      border-top: 1px solid rgba(255,255,255,.05);
      border-bottom: 1px solid rgba(255,255,255,.04);
    }

    tbody tr td:first-child {
      border-left: 1px solid rgba(255,255,255,.05);
      border-top-left-radius: 14px;
      border-bottom-left-radius: 14px;
    }

    tbody tr td:last-child {
      border-right: 1px solid rgba(255,255,255,.05);
      border-top-right-radius: 14px;
      border-bottom-right-radius: 14px;
    }

    .mono { font-family: var(--mono); }
    .soft { color: var(--soft); }

    .list {
      display: grid;
      gap: 0;
    }

    .list-row {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      gap: 12px;
      padding: 14px 0;
      border-bottom: 1px solid rgba(255,255,255,.06);
    }

    .list-row:last-child { border-bottom: 0; padding-bottom: 0; }
    .list-row h5 {
      margin: 0 0 5px;
      font-size: 14px;
      letter-spacing: -.02em;
    }
    .list-row p {
      margin: 0;
      color: var(--soft);
      font-size: 13px;
      line-height: 1.45;
    }

    .feed {
      display: grid;
      gap: 0;
    }

    .feed-row {
      display: grid;
      grid-template-columns: 74px 1fr auto;
      gap: 12px;
      align-items: start;
      padding: 12px 0;
      border-bottom: 1px solid rgba(255,255,255,.06);
    }

    .feed-row:last-child { border-bottom: 0; padding-bottom: 0; }
    .feed-row time {
      color: var(--muted);
      font-size: 11px;
      font-family: var(--mono);
    }
    .feed-row h5 {
      margin: 0 0 4px;
      font-size: 14px;
      letter-spacing: -.02em;
    }
    .feed-row p {
      margin: 0;
      color: var(--soft);
      font-size: 13px;
      line-height: 1.45;
    }

    .scope-card {
      padding: 18px;
      border-radius: 24px;
      border: 1px solid rgba(255,255,255,.08);
      background:
        radial-gradient(circle at top left, rgba(255,255,255,.04), transparent 40%),
        linear-gradient(180deg, rgba(35,38,44,.82), rgba(18,20,24,.94));
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      box-shadow: inset 0 1px 0 rgba(255,255,255,.05), var(--card-shadow);
    }

    .scope-card h4 {
      margin: 0 0 12px;
      font-size: 16px;
      letter-spacing: -.02em;
    }

    .scope-line {
      display: flex;
      gap: 10px;
      align-items: center;
      padding: 9px 0;
      color: var(--soft);
      font-size: 14px;
    }

    .scope-icon {
      width: 28px;
      height: 28px;
      display: grid;
      place-items: center;
      border-radius: 10px;
      border: 1px solid rgba(255,255,255,.08);
      background: linear-gradient(180deg, rgba(255,255,255,.05), rgba(255,255,255,.015));
      color: var(--text);
      font-size: 11px;
      font-weight: 700;
      flex: 0 0 auto;
    }

    .chips {
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
    }

    .chip {
      min-height: 34px;
      display: inline-flex;
      align-items: center;
      padding: 0 12px;
      border-radius: 14px;
      border: 1px solid rgba(255,255,255,.07);
      background:
        linear-gradient(180deg, rgba(255,255,255,.03), rgba(255,255,255,.012)),
        rgba(16,18,22,.84);
      color: var(--soft);
      font-size: 13px;
    }

    .review {
      display: grid;
      grid-template-columns: 1fr 64px 1fr;
      gap: 12px;
      align-items: center;
      margin-bottom: 14px;
    }

    .review-node {
      padding: 20px;
      border-radius: 24px;
      border: 1px solid rgba(255,255,255,.08);
      background:
        radial-gradient(circle at top left, rgba(255,255,255,.04), transparent 38%),
        linear-gradient(180deg, rgba(34,37,43,.84), rgba(18,20,24,.94));
      box-shadow: inset 0 1px 0 rgba(255,255,255,.05), var(--card-shadow);
    }

    .review-node h4 {
      margin: 0 0 6px;
      font-size: 18px;
      letter-spacing: -.03em;
    }

    .review-node p {
      margin: 0;
      color: var(--soft);
      font-size: 14px;
      line-height: 1.45;
    }

    .review-arrow {
      text-align: center;
      color: var(--muted);
      font-size: 26px;
    }

    .callout {
      padding: 20px;
      border-radius: 24px;
      border: 1px solid rgba(126,174,248,.22);
      background:
        radial-gradient(circle at top left, rgba(126,174,248,.11), transparent 44%),
        linear-gradient(180deg, rgba(27,30,37,.98), rgba(19,21,26,.98));
      margin-bottom: 14px;
      box-shadow: inset 0 1px 0 rgba(255,255,255,.05), var(--card-shadow);
    }

    .callout h4 {
      margin: 0 0 8px;
      font-size: 18px;
      letter-spacing: -.03em;
    }

    .callout p, .callout li {
      color: var(--soft);
      font-size: 14px;
      line-height: 1.5;
    }

    .callout ul {
      margin: 10px 0 0 18px;
      padding: 0;
    }

    .workflow {
      display: grid;
      gap: 12px;
    }

    .workflow-step {
      display: grid;
      grid-template-columns: 52px 1fr auto;
      gap: 14px;
      align-items: start;
      padding: 20px;
      border-radius: 24px;
      border: 1px solid rgba(255,255,255,.08);
      background:
        linear-gradient(180deg, rgba(255,255,255,.03), rgba(255,255,255,.012)),
        rgba(18,20,24,.9);
      box-shadow: inset 0 1px 0 rgba(255,255,255,.05);
    }

    .workflow-icon {
      width: 48px;
      height: 48px;
      display: grid;
      place-items: center;
      border-radius: 16px;
      border: 1px solid rgba(255,255,255,.08);
      background: linear-gradient(180deg, rgba(255,255,255,.05), rgba(255,255,255,.012));
      color: var(--orange);
      font-size: 18px;
      font-weight: 800;
    }

    .workflow-step h5 {
      margin: 0 0 6px;
      font-size: 16px;
      letter-spacing: -.02em;
    }

    .workflow-step p {
      margin: 0;
      color: var(--soft);
      font-size: 14px;
      line-height: 1.45;
    }

    .code {
      padding: 18px;
      border-radius: 22px;
      border: 1px solid rgba(255,255,255,.08);
      background:
        radial-gradient(circle at top left, rgba(126,174,248,.06), transparent 38%),
        linear-gradient(180deg, rgba(17,19,24,.98), rgba(13,15,19,.98));
      color: #d6dce8;
      font-family: var(--mono);
      font-size: 12px;
      line-height: 1.62;
      white-space: pre-wrap;
      box-shadow: inset 0 1px 0 rgba(255,255,255,.04);
    }

    .login {
      max-width: 580px;
      margin: 0 auto;
    }

    .field { margin-bottom: 12px; }
    .field label {
      display: block;
      margin-bottom: 6px;
      color: var(--soft);
      font-size: 12px;
      font-weight: 600;
    }
    .field input {
      width: 100%;
      min-height: 48px;
      padding: 0 14px;
      border-radius: 14px;
      border: 1px solid var(--line);
      background: #15171b;
      color: var(--text);
    }

    @media (max-width: 1420px) {
      .summary-strip { grid-template-columns: repeat(4, minmax(0, 1fr)); }
      .grid-top { grid-template-columns: 1fr; }
      .grid-3, .zenith-lower { grid-template-columns: 1fr 1fr; }
    }

    @media (max-width: 1180px) {
      .app { grid-template-columns: 1fr; }
      .sidebar { display: none; }
      .topbar { grid-template-columns: 1fr; }
      .search { width: 100%; }
      .top-pills { justify-content: flex-start; }
      .stats-4, .stats-3, .grid-2, .grid-3, .scope, .review, .zenith-lower, .mini-grid { grid-template-columns: 1fr; }
      .review-arrow { display: none; }
    }

    @media (max-width: 760px) {
      .shell { padding: 8px; }
      .main { padding: 10px; }
      .hero, .panel, .metric-card { border-radius: 18px; }
      .summary-strip { grid-template-columns: 1fr 1fr; }
      table, tbody, tr, th, td { display: block; width: 100%; }
      thead { display: none; }
      tbody tr {
        display: block;
        padding-bottom: 12px;
        margin-bottom: 12px;
        border-bottom: 1px solid var(--line);
      }
      tbody tr:last-child { border-bottom: 0; padding-bottom: 0; margin-bottom: 0; }
      td { border-bottom: 0; padding: 6px 0; }
      .feed-row { grid-template-columns: 1fr; }
    }
  </style>
</head>
<body>
  <div class="shell">
    <div class="app">
      <aside class="sidebar">
        <div class="brand">
          <div class="brand-lock" aria-hidden="true">
            <svg viewBox="0 0 64 64" fill="none" xmlns="http://www.w3.org/2000/svg">
              <circle cx="32" cy="32" r="26" stroke="rgba(255,255,255,0.92)" stroke-width="2.6"/>
              <path d="M12 38C20 23 38 16 54 15C38 19 24 28 16 39C14.5 40.8 13.2 41.5 12 38Z" fill="rgba(255,255,255,0.96)"/>
              <path d="M18 43C23 40.5 29 39 37 39.5C31 41.2 26.5 44 21 48C19.2 48.9 17.4 47 18 43Z" fill="rgba(255,255,255,0.96)"/>
            </svg>
          </div>
          <div>
            <div class="brand-word">Lupid</div>
            <p>Agent security and observability</p>
          </div>
        </div>

        <div class="nav-group">
          <div class="group-label"><span>Main</span><span>⌄</span></div>
          <div class="nav-list">
            <button class="nav-item" data-screen="login">
              <div class="nav-icon" aria-hidden="true">
                <svg viewBox="0 0 24 24"><path d="M6 20h12"/><path d="M8 20v-9"/><path d="M16 20v-9"/><path d="M4 11l8-7 8 7"/><path d="M10 20v-5h4v5"/></svg>
              </div>
              <div><strong>Login</strong><span>Operator entry</span></div>
            </button>
            <button class="nav-item active" data-screen="zenith">
              <div class="nav-icon" aria-hidden="true">
                <svg viewBox="0 0 24 24"><path d="M4 18h16"/><path d="M7 14l3-4 3 2 4-6"/><circle cx="7" cy="14" r="1"/><circle cx="10" cy="10" r="1"/><circle cx="13" cy="12" r="1"/><circle cx="17" cy="6" r="1"/></svg>
              </div>
              <div><strong>Zenith</strong><span>Fleet overview</span></div>
              <div class="nav-count">4</div>
            </button>
            <button class="nav-item" data-screen="tracks">
              <div class="nav-icon" aria-hidden="true">
                <svg viewBox="0 0 24 24"><rect x="4" y="5" width="16" height="14" rx="2"/><path d="M8 9h8"/><path d="M8 13h5"/><path d="M8 17h7"/></svg>
              </div>
              <div><strong>Tracks</strong><span>Agent inventory</span></div>
              <div class="nav-count">128</div>
            </button>
            <button class="nav-item" data-screen="ephemeris">
              <div class="nav-icon" aria-hidden="true">
                <svg viewBox="0 0 24 24"><circle cx="12" cy="8" r="3"/><path d="M5 20c1.5-4 12.5-4 14 0"/><path d="M19 5l1.5 1.5"/><path d="M20.5 8.5L19 10"/></svg>
              </div>
              <div><strong>Ephemeris</strong><span>Agent detail</span></div>
            </button>
          </div>
        </div>

        <div class="nav-group">
          <div class="group-label"><span>Operations</span><span>⌄</span></div>
          <div class="nav-list">
            <button class="nav-item" data-screen="passes">
              <div class="nav-icon" aria-hidden="true">
                <svg viewBox="0 0 24 24"><rect x="4" y="5" width="16" height="14" rx="2"/><path d="M8 9h8"/><path d="M8 13h8"/><path d="M8 17h4"/></svg>
              </div>
              <div><strong>Passes</strong><span>Sessions</span></div>
            </button>
            <button class="nav-item" data-screen="trails">
              <div class="nav-icon" aria-hidden="true">
                <svg viewBox="0 0 24 24"><path d="M5 19V5"/><path d="M5 19h14"/><path d="M8 15l3-3 2 2 4-5"/></svg>
              </div>
              <div><strong>Trails</strong><span>Audit log</span></div>
            </button>
            <button class="nav-item" data-screen="vault">
              <div class="nav-icon" aria-hidden="true">
                <svg viewBox="0 0 24 24"><path d="M6 11h12v8H6z"/><path d="M8 11V8a4 4 0 0 1 8 0v3"/><circle cx="12" cy="15" r="1.4"/></svg>
              </div>
              <div><strong>Vault</strong><span>Credentials and leases</span></div>
            </button>
            <button class="nav-item" data-screen="relay">
              <div class="nav-icon" aria-hidden="true">
                <svg viewBox="0 0 24 24"><path d="M7 8h4"/><path d="M13 8h4"/><path d="M7 16h4"/><path d="M13 16h4"/><path d="M11 8l2 8"/></svg>
              </div>
              <div><strong>Relay</strong><span>MCP sessions and servers</span></div>
            </button>
            <button class="nav-item" data-screen="impacts">
              <div class="nav-icon" aria-hidden="true">
                <svg viewBox="0 0 24 24"><path d="M12 4l8 14H4L12 4z"/><path d="M12 10v4"/><circle cx="12" cy="17" r="1"/></svg>
              </div>
              <div><strong>Impacts</strong><span>Alerts and approvals</span></div>
              <div class="nav-count">7</div>
            </button>
          </div>
        </div>

        <div class="nav-group">
          <div class="group-label"><span>Governance</span><span>⌄</span></div>
          <div class="nav-list">
            <button class="nav-item" data-screen="constellations">
              <div class="nav-icon" aria-hidden="true">
                <svg viewBox="0 0 24 24"><circle cx="7" cy="8" r="2.2"/><circle cx="17" cy="7" r="2.2"/><circle cx="12" cy="16" r="2.2"/><path d="M8.8 9.3l1.8 4.2"/><path d="M15.2 8.2l-2.2 6"/><path d="M9 8.4l5.8-1"/></svg>
              </div>
              <div><strong>Constellations</strong><span>Teams and owners</span></div>
            </button>
            <button class="nav-item" data-screen="calibration">
              <div class="nav-icon" aria-hidden="true">
                <svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="3.4"/><path d="M12 3v3"/><path d="M12 18v3"/><path d="M3 12h3"/><path d="M18 12h3"/><path d="M5.6 5.6l2.1 2.1"/><path d="M16.3 16.3l2.1 2.1"/><path d="M18.4 5.6l-2.1 2.1"/><path d="M7.7 16.3l-2.1 2.1"/></svg>
              </div>
              <div><strong>Calibration</strong><span>Policy and simulation</span></div>
            </button>
          </div>
        </div>

        <div class="nav-group">
          <div class="nav-note">
            <h3>Watchfloor</h3>
            <p>Agent-first control. Review fleet drift, approvals, and access from one surface.</p>
            <div class="cta-row" style="margin-top:12px;">
              <button class="btn primary" style="min-height:34px;padding:0 12px;">Open queue</button>
              <button class="btn" style="min-height:34px;padding:0 12px;">Review</button>
            </div>
          </div>
        </div>
      </aside>

      <main class="main">
        <div class="topbar">
          <div>
            <h2>Lupid / Agent Operations</h2>
            <p>Control plane for governed AI agents</p>
          </div>
          <div class="search">Search agents, passes, alerts, servers</div>
          <div class="top-pills">
            <div class="pill"><span class="dot" style="color:var(--green)"></span><strong>Live</strong></div>
            <div class="pill"><strong>128 agents</strong></div>
            <div class="pill"><strong>31 leases</strong></div>
            <div class="pill"><strong>9 MCP sessions</strong></div>
            <div class="pill"><strong>Read only</strong></div>
          </div>
        </div>

        <section class="screen" id="screen-login">
          <div class="hero login">
            <div class="hero-top">
              <div>
                <div class="eyebrow">Operator access</div>
                <h3>Enter the watchfloor</h3>
                <p>Access the fleet control surface.</p>
              </div>
              <div class="badge blue">Prototype</div>
            </div>
            <div class="field">
              <label>Email</label>
              <input value="ops@lupid.io" readonly />
            </div>
            <div class="field">
              <label>Password</label>
              <input value="meteor-line-1442" readonly />
            </div>
            <div class="cta-row">
              <button class="btn primary" data-screen-link="zenith">Open Zenith</button>
              <button class="btn">SSO via Orbit ID</button>
            </div>
          </div>
        </section>

        <section class="screen active" id="screen-zenith">
          <div class="hero">
            <div class="hero-top">
              <div class="hero-copy">
                <div class="eyebrow">Zenith</div>
                <h3>Know which agents are healthy, drifting, or blocked</h3>
                <p>Fleet posture, policy pressure, approvals, and shadow activity in one scan.</p>
              </div>
              <div class="badge green">Fleet nominal</div>
            </div>

            <div class="summary-strip">
              <div class="summary"><small>Governed fleet</small><strong>117 healthy</strong><em>8 watched, 3 blocked</em></div>
              <div class="summary"><small>Policy posture</small><strong>94.8% allow</strong><em>deny rate up 0.7% this hour</em></div>
              <div class="summary"><small>Approvals queue</small><strong>12 pending</strong><em>3 requests stale beyond SLA</em></div>
              <div class="summary"><small>Critical alerts</small><strong>3 unacked</strong><em>2 tied to one agent family</em></div>
              <div class="summary"><small>Shadow pressure</small><strong>4 runtime traces</strong><em>2 promote, 2 isolate</em></div>
              <div class="summary"><small>Access pressure</small><strong>6 leases + 9 MCP</strong><em>highest on payments-router</em></div>
            </div>

            <div class="tabs" style="margin-top:14px;">
              <button class="tab active">Fleet posture</button>
              <button class="tab">Policy outcomes</button>
              <button class="tab">Approvals</button>
              <button class="tab">Shadow discovery</button>
              <button class="tab">Vault pressure</button>
            </div>
          </div>

          <div class="zenith-main">
            <div class="stack">
              <div class="panel">
                <div class="panel-head">
                  <h4>Fleet decision plane</h4>
                  <span>GET /agents/stats + /audit</span>
                </div>
                <div class="panel-body">
                  <div class="mini-stat-row">
                    <div class="mini-stat"><small class="label">Healthy</small><strong>117</strong><span class="soft">Nominal agents</span></div>
                    <div class="mini-stat"><small class="label">Watched</small><strong style="color:#f0be77;">8</strong><span class="soft">Needs review</span></div>
                    <div class="mini-stat"><small class="label">Shadow</small><strong style="color:var(--violet);">4</strong><span class="soft">Unclaimed runtime</span></div>
                    <div class="mini-stat"><small class="label">Blocked</small><strong style="color:var(--red);">3</strong><span class="soft">Execution blocked</span></div>
                  </div>
                  <div class="stack-bar">
                    <span style="width:91.4%;background:var(--green);"></span>
                    <span style="width:3.1%;background:var(--orange);"></span>
                    <span style="width:2.3%;background:var(--red);"></span>
                    <span style="width:3.2%;background:var(--violet);"></span>
                  </div>
                  <div class="chart" style="margin-top:14px;">
                    <svg viewBox="0 0 1000 250" preserveAspectRatio="none">
                      <defs>
                        <linearGradient id="zenithArea" x1="0" x2="0" y1="0" y2="1">
                          <stop offset="0%" stop-color="rgba(243,138,66,0.32)"/>
                          <stop offset="100%" stop-color="rgba(243,138,66,0.02)"/>
                        </linearGradient>
                      </defs>
                      <polyline fill="url(#zenithArea)" stroke="none" points="0,214 80,208 160,180 250,176 340,170 430,168 520,170 610,174 700,188 790,194 890,186 1000,198 1000,250 0,250"/>
                      <polyline fill="none" stroke="#f38a42" stroke-width="3.2" points="0,214 80,208 160,180 250,176 340,170 430,168 520,170 610,174 700,188 790,194 890,186 1000,198"/>
                      <polyline fill="none" stroke="#a6c2ff" stroke-width="2.8" points="0,232 80,230 160,220 250,222 340,218 430,216 520,214 610,216 700,222 790,226 890,220 1000,228"/>
                      <polyline fill="none" stroke="#9b7bff" stroke-width="2.8" points="0,238 80,236 160,234 250,232 340,230 430,228 520,229 610,230 700,233 790,236 890,233 1000,238"/>
                      <line x1="710" y1="0" x2="710" y2="250" stroke="#384253" stroke-width="1.2" stroke-dasharray="5 5"/>
                      <rect x="670" y="14" width="118" height="26" rx="13" fill="rgba(18,20,24,.8)" stroke="rgba(126,174,248,.15)"/>
                      <text x="689" y="31" fill="#a6c2ff" font-family="IBM Plex Mono, monospace" font-size="12">deny uptick</text>
                    </svg>
                  </div>
                  <div class="tabs" style="margin-top:12px;">
                    <button class="tab active">Decision mix</button>
                    <button class="tab">Review load</button>
                    <button class="tab">Drift by team</button>
                  </div>
                </div>
              </div>

              <div class="zenith-bottom">
                <div class="panel">
                  <div class="panel-head">
                    <h4>Evidence feed</h4>
                    <span>last fleet-changing events</span>
                  </div>
                  <div class="panel-body">
                    <div class="feed">
                      <div class="feed-row"><time>11:42Z</time><div><h5>sales-pilot-07 denied</h5><p>CRM export blocked because elevated data classes hit a deny policy.</p></div><div class="badge red">deny</div></div>
                      <div class="feed-row"><time>11:38Z</time><div><h5>payments-router lease issued</h5><p>stripe_writer lease issued with short TTL.</p></div><div class="badge green">allow</div></div>
                      <div class="feed-row"><time>11:27Z</time><div><h5>shadow-west-3 detected</h5><p>Unregistered runtime fingerprinted from MCP discovery traffic.</p></div><div class="badge violet">shadow</div></div>
                    </div>
                  </div>
                </div>

                <div class="panel">
                  <div class="panel-head">
                    <h4>Pending approvals</h4>
                    <span>GET /hitl/requests</span>
                  </div>
                  <div class="panel-body">
                    <div class="list">
                      <div class="list-row"><div><h5>support-orbit-eu</h5><p>CRM write-back for escalated case.</p></div><span class="badge amber">6m</span></div>
                      <div class="list-row"><div><h5>procure-agent-02</h5><p>Vendor master update.</p></div><span class="badge amber">11m</span></div>
                      <div class="list-row"><div><h5>payments-router</h5><p>Risk override during reconciliation.</p></div><span class="badge blue">new</span></div>
                    </div>
                  </div>
                </div>

                <div class="panel">
                  <div class="panel-head">
                    <h4>Shadow queue</h4>
                    <span>GET /shadow</span>
                  </div>
                  <div class="panel-body">
                    <div class="list">
                      <div class="list-row"><div><h5>shadow-west-3</h5><p>CrewAI fingerprint from staging subnet.</p></div><span class="badge violet">promote</span></div>
                      <div class="list-row"><div><h5>shadow-east-1</h5><p>Unknown runtime probing MCP registry.</p></div><span class="badge red">block</span></div>
                    </div>
                  </div>
                </div>
              </div>
            </div>

            <div class="stack">
              <div class="panel">
                <div class="panel-head">
                  <h4>Needs attention</h4>
                  <span>open these agents first</span>
                </div>
                <div class="panel-body">
                  <div class="focus-list">
                    <div class="focus-item">
                      <div>
                        <h5>sales-pilot-07</h5>
                        <p>Quarantined after denied CRM export with PII.</p>
                        <div class="focus-meta">Revenue Systems • agt_01HTR58K6C</div>
                      </div>
                      <div class="badge red">open</div>
                    </div>
                    <div class="focus-item">
                      <div>
                        <h5>support-orbit-eu</h5>
                        <p>Approval pressure and tool density above baseline.</p>
                        <div class="focus-meta">Support Engineering • 2 live passes</div>
                      </div>
                      <div class="badge amber">review</div>
                    </div>
                    <div class="focus-item">
                      <div>
                        <h5>shadow-west-3</h5>
                        <p>Unregistered runtime with repeat MCP probing.</p>
                        <div class="focus-meta">staging subnet • promote or block</div>
                      </div>
                      <div class="badge violet">decide</div>
                    </div>
                    <div class="focus-item">
                      <div>
                        <h5>payments-router</h5>
                        <p>High activity, active leases, one pending override.</p>
                        <div class="focus-meta">3 passes • 41 MCP calls • 2 leases</div>
                      </div>
                      <div class="badge blue">inspect</div>
                    </div>
                  </div>
                </div>
              </div>

              <div class="panel">
                <div class="panel-head">
                  <h4>Fleet distribution</h4>
                  <span>registration and status</span>
                </div>
                <div class="panel-body">
                  <div class="donut-wrap">
                    <svg class="donut" viewBox="0 0 120 120">
                      <circle cx="60" cy="60" r="40" fill="none" stroke="#252a31" stroke-width="10"></circle>
                      <circle cx="60" cy="60" r="40" fill="none" stroke="#8fd0ab" stroke-width="10" stroke-dasharray="230 21" transform="rotate(-90 60 60)" stroke-linecap="round"></circle>
                      <circle cx="60" cy="60" r="40" fill="none" stroke="#f38a42" stroke-width="10" stroke-dasharray="18 233" stroke-dashoffset="-230" transform="rotate(-90 60 60)" stroke-linecap="round"></circle>
                      <circle cx="60" cy="60" r="40" fill="none" stroke="#df6c75" stroke-width="10" stroke-dasharray="12 239" stroke-dashoffset="-248" transform="rotate(-90 60 60)" stroke-linecap="round"></circle>
                      <circle cx="60" cy="60" r="40" fill="none" stroke="#9b7bff" stroke-width="10" stroke-dasharray="12 239" stroke-dashoffset="-260" transform="rotate(-90 60 60)" stroke-linecap="round"></circle>
                      <text x="60" y="58" text-anchor="middle" font-size="22" font-weight="800" fill="#f2f4f7">128</text>
                      <text x="60" y="74" text-anchor="middle" font-size="11" fill="#707887">fleet</text>
                    </svg>
                    <div class="legend">
                      <div class="legend-row"><em style="color:var(--green)"><i></i>Active</em><strong>117</strong></div>
                      <div class="legend-row"><em style="color:var(--orange)"><i></i>Suspended</em><strong>4</strong></div>
                      <div class="legend-row"><em style="color:var(--red)"><i></i>Quarantined</em><strong>3</strong></div>
                      <div class="legend-row"><em style="color:var(--violet)"><i></i>Shadow</em><strong>4</strong></div>
                    </div>
                  </div>
                </div>
              </div>

              <div class="panel">
                <div class="panel-head">
                  <h4>Access pressure</h4>
                  <span>credential and tool-call exposure</span>
                </div>
                <div class="panel-body">
                  <div class="list">
                    <div class="list-row"><div><h5>Expiring leases</h5><p>6 leases expire within 15 minutes.</p></div><strong>6</strong></div>
                    <div class="list-row"><div><h5>Live MCP sessions</h5><p>9 sessions across 6 approved servers.</p></div><strong>9</strong></div>
                    <div class="list-row"><div><h5>Denied tool calls</h5><p>3 denied this hour.</p></div><strong>3</strong></div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </section>

        <section class="screen" id="screen-tracks">
          <div class="hero">
            <div class="hero-top">
              <div>
                <div class="eyebrow">Tracks</div>
                <h3>Every agent in one table</h3>
                <p>Status, trust, passes, leases, relay access, and last activity.</p>
              </div>
              <div class="cta-row">
                <button class="btn primary">Register agent</button>
                <button class="btn">Export</button>
              </div>
            </div>
            <div class="filters" style="margin-top:16px;">
              <button class="chip-btn">All status</button>
              <button class="chip-btn">Trust level</button>
              <button class="chip-btn">Framework</button>
              <button class="chip-btn">Has alerts</button>
              <button class="chip-btn">Has passes</button>
            </div>
          </div>
          <div class="stats-4">
            <div class="metric-card"><small class="label">Governed</small><div class="value">128</div><p>117 active, 11 under action</p></div>
            <div class="metric-card"><small class="label">Watched</small><div class="value" style="color:#f0be77;">8</div><p>Approval or policy pressure</p></div>
            <div class="metric-card"><small class="label">Quarantined</small><div class="value" style="color:var(--red);">3</div><p>Execution blocked</p></div>
            <div class="metric-card"><small class="label">Shadow</small><div class="value" style="color:var(--violet);">4</div><p>Unregistered runtimes</p></div>
          </div>
          <div class="grid-top">
            <div class="panel">
              <div class="panel-head">
                <h4>Agent inventory</h4>
                <span>GET /agents</span>
              </div>
              <div class="panel-body">
                <table>
                  <thead>
                    <tr><th>Agent</th><th>Status</th><th>Trust</th><th>Owner</th><th>Framework</th><th>Passes</th><th>Vault</th><th>Relay</th><th>Last active</th></tr>
                  </thead>
                  <tbody>
                    <tr><td><strong>payments-router</strong><div class="soft mono">agt_01HTR4M2XQ / commerce</div></td><td><span class="badge green">active</span></td><td>high</td><td>Revenue Systems</td><td>LangGraph</td><td>3</td><td>2 leases</td><td>2 servers</td><td class="mono">14s ago</td></tr>
                    <tr><td><strong>support-orbit-eu</strong><div class="soft mono">agt_01HTR5RAJP / support</div></td><td><span class="badge amber">suspended</span></td><td>medium</td><td>Support Engineering</td><td>OpenAI SDK</td><td>2</td><td>1 expiring</td><td>1 server</td><td class="mono">29s ago</td></tr>
                    <tr><td><strong>sales-pilot-07</strong><div class="soft mono">agt_01HTR58K6C / revops</div></td><td><span class="badge red">quarantined</span></td><td>medium</td><td>Revenue Systems</td><td>CrewAI</td><td>0</td><td>revoked</td><td>blocked</td><td class="mono">3m ago</td></tr>
                    <tr><td><strong>shadow-west-3</strong><div class="soft mono">sha_01HWH17P4D / staging</div></td><td><span class="badge violet">shadow</span></td><td>unknown</td><td>Unclaimed</td><td>Unknown</td><td>1</td><td>n/a</td><td>observe only</td><td class="mono">9m ago</td></tr>
                  </tbody>
                </table>
              </div>
            </div>
            <div class="stack">
              <div class="signal">
                <h5>Inventory signal</h5>
                <p>Most operator effort is clustered in three agents, not across the fleet.</p>
                <div class="micro">focus on exceptions, not totals</div>
              </div>
              <div class="panel">
                <div class="panel-head"><h4>Open next</h4><span>recommended pivots</span></div>
                <div class="panel-body">
                  <div class="list">
                    <div class="list-row"><div><h5>sales-pilot-07</h5><p>Quarantined, revoked credentials, deny cluster.</p></div><span class="badge red">urgent</span></div>
                    <div class="list-row"><div><h5>support-orbit-eu</h5><p>Approval pressure and one expiring lease.</p></div><span class="badge amber">watch</span></div>
                    <div class="list-row"><div><h5>shadow-west-3</h5><p>Needs promote vs block decision.</p></div><span class="badge violet">decide</span></div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </section>

        <section class="screen" id="screen-ephemeris">
          <div class="hero">
            <div class="hero-top">
              <div>
                <div class="eyebrow">Ephemeris</div>
                <h3>payments-router</h3>
                <p>Identity, runtime, policy, evidence, and control.</p>
              </div>
              <div class="cta-row">
                <div class="badge green">active</div>
                <button class="btn">Suspend</button>
                <button class="btn">Rotate key</button>
                <button class="btn">Quarantine</button>
              </div>
            </div>
            <div class="summary-strip">
              <div class="summary"><small>Owner</small><strong>Revenue Systems</strong></div>
              <div class="summary"><small>Trust</small><strong>High</strong></div>
              <div class="summary"><small>Framework</small><strong>LangGraph</strong></div>
              <div class="summary"><small>Passes</small><strong>3 live</strong></div>
              <div class="summary"><small>Leases</small><strong>2 active</strong></div>
              <div class="summary"><small>Relay</small><strong>2 servers</strong></div>
              <div class="summary"><small>Policy ratio</small><strong>96.8% allow</strong></div>
              <div class="summary"><small>Last active</small><strong>11:38Z</strong></div>
            </div>
          </div>

          <div class="scope">
            <div class="stack">
              <div class="scope-card">
                <h4>Object record</h4>
                <div class="scope-line"><div class="scope-icon">ID</div><span class="mono">agt_01HTR4M2XQ</span></div>
                <div class="scope-line"><div class="scope-icon">Ow</div><span>Revenue Systems</span></div>
                <div class="scope-line"><div class="scope-icon">Ve</div><span>v1.9.7</span></div>
                <div class="scope-line"><div class="scope-icon">Ke</div><span>Ed25519 key present</span></div>
              </div>
              <div class="scope-card">
                <h4>Current passes</h4>
                <div class="scope-line"><div class="scope-icon">P1</div><span class="mono">pas_01J2K4ZR / us-east-1 / 14m</span></div>
                <div class="scope-line"><div class="scope-icon">P2</div><span class="mono">pas_01J2K4QX / eu-west-1 / 9m</span></div>
                <div class="scope-line"><div class="scope-icon">P3</div><span class="mono">pas_01J2JZZV / ended</span></div>
              </div>
            </div>

            <div class="stack">
              <div class="panel">
                <div class="panel-head">
                  <h4>Recent activity</h4>
                  <span>agent chart</span>
                </div>
                <div class="panel-body">
                  <div class="chart">
                    <svg viewBox="0 0 1000 250" preserveAspectRatio="none">
                      <polyline fill="rgba(126,174,248,0.08)" stroke="none" points="0,210 90,184 180,188 280,150 380,156 470,112 580,116 700,158 820,146 920,168 1000,162 1000,250 0,250"/>
                      <polyline fill="none" stroke="#7eaef8" stroke-width="3" points="0,210 90,184 180,188 280,150 380,156 470,112 580,116 700,158 820,146 920,168 1000,162"/>
                      <polyline fill="none" stroke="#fb8b3b" stroke-width="2.8" points="0,224 100,218 190,210 280,208 370,170 470,166 580,170 700,214 810,208 918,214 1000,206"/>
                    </svg>
                  </div>
                </div>
              </div>

              <div class="grid-2">
                <div class="panel">
                  <div class="panel-head">
                    <h4>Tools</h4>
                    <span>declared access</span>
                  </div>
                  <div class="panel-body">
                    <div class="chips">
                      <div class="chip">ledger.lookup</div>
                      <div class="chip">vault.lease</div>
                      <div class="chip">fraud.review</div>
                      <div class="chip">ticket.open</div>
                    </div>
                  </div>
                </div>
                <div class="panel">
                  <div class="panel-head">
                    <h4>Leases</h4>
                    <span>active now</span>
                  </div>
                  <div class="panel-body">
                    <div class="list">
                      <div class="list-row"><div><h5>stripe_writer</h5><p>AWS Secrets • 12m left</p></div><span class="badge green">active</span></div>
                      <div class="list-row"><div><h5>ledger_read</h5><p>Vault • 43m left</p></div><span class="badge amber">expiring</span></div>
                    </div>
                  </div>
                </div>
              </div>

              <div class="grid-2">
                <div class="signal">
                  <h5>Current posture</h5>
                  <p>Healthy primary identity, elevated write activity, still inside allowed boundary.</p>
                  <div class="micro">96.8% allow • 2 review events today</div>
                </div>
                <div class="signal">
                  <h5>Why this agent matters</h5>
                  <p>Highest combined MCP, vault, and pass volume in the governed fleet.</p>
                  <div class="micro">3 passes • 41 MCP calls • 2 live leases</div>
                </div>
              </div>

              <div class="panel">
                <div class="panel-head">
                  <h4>Recent trails</h4>
                  <span>GET /audit?agent_id=...</span>
                </div>
                <div class="panel-body">
                  <div class="feed">
                    <div class="feed-row"><time>11:38Z</time><div><h5>credential_issued</h5><p>stripe_writer lease created with 120s TTL.</p></div><div class="badge green">allow</div></div>
                    <div class="feed-row"><time>11:30Z</time><div><h5>tool_call</h5><p>ledger lookup completed within boundary.</p></div><div class="badge green">allow</div></div>
                    <div class="feed-row"><time>11:25Z</time><div><h5>data_redacted</h5><p>Customer email masked before response.</p></div><div class="badge blue">masked</div></div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </section>

        <section class="screen" id="screen-passes">
          <div class="hero">
            <div class="hero-top">
              <div>
                <div class="eyebrow">Passes</div>
                <h3>Runtime windows by agent</h3>
                <p>Session state, network context, policy summary, replay.</p>
              </div>
              <div class="badge amber">27 live</div>
            </div>
            <div class="filters" style="margin-top:16px;">
              <button class="chip-btn">All agents</button>
              <button class="chip-btn">Active</button>
              <button class="chip-btn">Ended</button>
              <button class="chip-btn">Replay available</button>
            </div>
          </div>
          <div class="grid-2">
            <div class="panel">
              <div class="panel-head">
                <h4>Pass inventory</h4>
                <span>GET /sessions</span>
              </div>
              <div class="panel-body">
                <table>
                  <thead><tr><th>Agent</th><th>Pass</th><th>Status</th><th>Duration</th><th>Source IP</th><th>Policy summary</th><th>Replay</th></tr></thead>
                  <tbody>
                    <tr><td><strong>payments-router</strong></td><td class="mono">pas_01J2K4ZR</td><td><span class="badge green">active</span></td><td>14m 22s</td><td class="mono">10.18.4.22</td><td>39 allow / 2 review</td><td>Open timeline</td></tr>
                    <tr><td><strong>support-orbit-eu</strong></td><td class="mono">pas_01J2L61M</td><td><span class="badge amber">active</span></td><td>09m 11s</td><td class="mono">10.22.14.9</td><td>61 allow / 3 review</td><td>Open timeline</td></tr>
                    <tr><td><strong>sales-pilot-07</strong></td><td class="mono">pas_01J2KZ1A</td><td><span class="badge red">ended</span></td><td>03m 02s</td><td class="mono">10.31.7.44</td><td>8 allow / 1 review / 3 deny</td><td>Replay incident</td></tr>
                  </tbody>
                </table>
              </div>
            </div>
            <div class="stack">
              <div class="signal">
                <h5>Pass pressure</h5>
                <p>Two agents account for most live session activity and almost all replay demand.</p>
                <div class="micro">payments-router + support-orbit-eu dominate</div>
              </div>
              <div class="panel">
                <div class="panel-head">
                  <h4>Replay preview</h4>
                  <span>GET /sessions/{id}/replay</span>
                </div>
                <div class="panel-body">
                  <div class="feed">
                    <div class="feed-row"><time>00:00</time><div><h5>session.start</h5><p>payments-router authenticated from us-east-1.</p></div><div class="badge blue">start</div></div>
                    <div class="feed-row"><time>03:12</time><div><h5>policy_allow</h5><p>ledger.lookup approved.</p></div><div class="badge green">allow</div></div>
                    <div class="feed-row"><time>06:41</time><div><h5>vault.lease_issued</h5><p>stripe_writer lease issued.</p></div><div class="badge green">allow</div></div>
                    <div class="feed-row"><time>09:08</time><div><h5>session.end</h5><p>Pass terminated cleanly.</p></div><div class="badge amber">ended</div></div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </section>

        <section class="screen" id="screen-trails">
          <div class="hero">
            <div class="hero-top">
              <div>
                <div class="eyebrow">Trails</div>
                <h3>Immutable audit for every agent decision</h3>
                <p>Filter by agent, outcome, event type, and time.</p>
              </div>
              <div class="cta-row">
                <button class="btn">Export CSV</button>
                <button class="btn">Prune</button>
              </div>
            </div>
            <div class="filters" style="margin-top:16px;">
              <button class="chip-btn">Agent</button>
              <button class="chip-btn">Event type</button>
              <button class="chip-btn">Outcome</button>
              <button class="chip-btn">Last 24h</button>
            </div>
          </div>
          <div class="grid-2">
            <div class="panel">
              <div class="panel-head">
                <h4>Audit stream</h4>
                <span>GET /audit</span>
              </div>
              <div class="panel-body">
                <table>
                  <thead><tr><th>Time</th><th>Agent</th><th>Event</th><th>Outcome</th><th>Risk</th><th>Resource</th></tr></thead>
                  <tbody>
                    <tr><td class="mono">11:42:17Z</td><td>sales-pilot-07</td><td>policy_deny</td><td><span class="badge red">deny</span></td><td>92%</td><td>crm.export.customer_records</td></tr>
                    <tr><td class="mono">11:38:03Z</td><td>payments-router</td><td>credential_issued</td><td><span class="badge green">allow</span></td><td>8%</td><td>vault.lease.stripe_writer</td></tr>
                    <tr><td class="mono">11:27:19Z</td><td>shadow-west-3</td><td>shadow_detected</td><td><span class="badge violet">observe</span></td><td>61%</td><td>mcp.edge.discovery</td></tr>
                  </tbody>
                </table>
              </div>
            </div>
            <div class="stack">
              <div class="signal">
                <h5>Trail signal</h5>
                <p>Most high-risk records today are either export denies or shadow detections.</p>
                <div class="micro">92% top risk on sales-pilot-07</div>
              </div>
              <div class="panel">
                <div class="panel-head">
                  <h4>Selected event</h4>
                  <span>detail JSON</span>
                </div>
                <div class="panel-body">
                  <div class="code">{
  "agent_id": "agt_01HTR58K6C",
  "session_id": "pas_01J2KZ1A",
  "event_type": "policy_deny",
  "resource": "crm.export.customer_records",
  "risk_score": 0.92,
  "detail": {
    "data_classes": ["pii"],
    "matched_policy": "external_export_requires_approval",
    "target_domain": "sync-river.app"
  }
}</div>
                </div>
              </div>
            </div>
          </div>
        </section>

        <section class="screen" id="screen-vault">
          <div class="hero">
            <div class="hero-top">
              <div>
                <div class="eyebrow">Vault</div>
                <h3>Credential exposure by agent</h3>
                <p>Stored credentials, active leases, revocation, countdowns.</p>
              </div>
              <div class="cta-row">
                <button class="btn primary">Issue lease</button>
                <button class="btn">Store credential</button>
              </div>
            </div>
            <div class="filters" style="margin-top:16px;">
              <button class="chip-btn">Credentials</button>
              <button class="chip-btn">Leases</button>
              <button class="chip-btn">Active</button>
              <button class="chip-btn">Expiring</button>
            </div>
          </div>
          <div class="grid-2">
            <div class="panel">
              <div class="panel-head">
                <h4>Lease inventory</h4>
                <span>GET /vault/leases</span>
              </div>
              <div class="panel-body">
                <table>
                  <thead><tr><th>Agent</th><th>Service</th><th>Type</th><th>Backend</th><th>TTL</th><th>Status</th></tr></thead>
                  <tbody>
                    <tr><td><strong>payments-router</strong></td><td>stripe_writer</td><td>api_key</td><td>AWS Secrets</td><td>12m</td><td><span class="badge green">active</span></td></tr>
                    <tr><td><strong>sales-pilot-07</strong></td><td>salesforce_sync</td><td>oauth2</td><td>Vault</td><td>revoked</td><td><span class="badge red">revoked</span></td></tr>
                    <tr><td><strong>support-orbit-eu</strong></td><td>zendesk_read</td><td>token</td><td>Static AES-GCM</td><td>43m</td><td><span class="badge amber">expiring</span></td></tr>
                  </tbody>
                </table>
              </div>
            </div>
            <div class="stack">
              <div class="stats-3">
                <div class="metric-card"><small class="label">Active leases</small><div class="value">24</div><p>Spread across 11 agents</p></div>
                <div class="metric-card"><small class="label">Expiring</small><div class="value" style="color:#f0be77;">6</div><p>Within 15 minutes</p></div>
                <div class="metric-card"><small class="label">Revoked today</small><div class="value" style="color:var(--red);">1</div><p>sales-pilot-07</p></div>
              </div>
              <div class="signal">
                <h5>Exposure now</h5>
                <p>24 active leases. 6 expiring soon. 1 revoked today.</p>
                <div class="micro">blast radius stays visible</div>
              </div>
              <div class="panel">
                <div class="panel-head">
                  <h4>Credential actions</h4>
                  <span>store / issue / revoke</span>
                </div>
                <div class="panel-body">
                  <div class="list">
                    <div class="list-row"><div><h5>Store credential</h5><p>Encrypted at rest. Value shown once.</p></div><span class="badge blue">ready</span></div>
                    <div class="list-row"><div><h5>Issue lease</h5><p>Short TTL with one-time reveal.</p></div><span class="badge green">primary</span></div>
                    <div class="list-row"><div><h5>Revoke</h5><p>Per lease or all for one agent.</p></div><span class="badge red">admin</span></div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </section>

        <section class="screen" id="screen-relay">
          <div class="hero">
            <div class="hero-top">
              <div>
                <div class="eyebrow">Relay</div>
                <h3>MCP usage by agent</h3>
                <p>Sessions, grants, server health, and tool call volume.</p>
              </div>
              <div class="cta-row">
                <button class="btn primary">Register server</button>
                <button class="btn">Grant access</button>
              </div>
            </div>
          </div>
          <div class="grid-2">
            <div class="panel">
              <div class="panel-head">
                <h4>MCP sessions</h4>
                <span>GET /mcp/sessions</span>
              </div>
              <div class="panel-body">
                <table>
                  <thead><tr><th>Agent</th><th>Server</th><th>Transport</th><th>Calls</th><th>Status</th></tr></thead>
                  <tbody>
                    <tr><td><strong>payments-router</strong></td><td>Stripe MCP</td><td>http</td><td>41</td><td><span class="badge green">active</span></td></tr>
                    <tr><td><strong>support-orbit-eu</strong></td><td>Zendesk MCP</td><td>http</td><td>18</td><td><span class="badge amber">active</span></td></tr>
                    <tr><td><strong>sales-pilot-07</strong></td><td>CRM MCP</td><td>http</td><td>3</td><td><span class="badge red">terminated</span></td></tr>
                  </tbody>
                </table>
              </div>
            </div>
            <div class="stack">
              <div class="signal">
                <h5>Relay signal</h5>
                <p>Traffic is healthy overall, but the CRM MCP path carries disproportionate deny pressure.</p>
                <div class="micro">41 Stripe calls • 18 Zendesk • 3 denied CRM</div>
              </div>
              <div class="panel">
                <div class="panel-head">
                  <h4>Registered servers</h4>
                  <span>GET /mcp/servers</span>
                </div>
                <div class="panel-body">
                  <div class="list">
                    <div class="list-row"><div><h5>Stripe MCP</h5><p>2 agents granted • circuit closed</p></div><span class="badge green">healthy</span></div>
                    <div class="list-row"><div><h5>Zendesk MCP</h5><p>1 agent granted • circuit closed</p></div><span class="badge green">healthy</span></div>
                    <div class="list-row"><div><h5>CRM MCP</h5><p>2 agents granted • elevated deny rate</p></div><span class="badge amber">watch</span></div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </section>

        <section class="screen" id="screen-impacts">
          <div class="hero">
            <div class="hero-top">
              <div>
                <div class="eyebrow">Impacts</div>
                <h3>Agent-linked alerts and approvals</h3>
                <p>What the agent tried, why it surfaced, what to decide.</p>
              </div>
              <div class="cta-row">
                <button class="btn primary">Approve</button>
                <button class="btn">Change</button>
                <button class="btn">Deny</button>
              </div>
            </div>
          </div>

          <div class="review">
            <div class="review-node">
              <h4>sales-pilot-07</h4>
              <p>RevOps pilot. Outbound CRM automation profile.</p>
            </div>
            <div class="review-arrow">→</div>
            <div class="review-node">
              <h4>External CRM export</h4>
              <p>Unapproved domain. Elevated data classes.</p>
            </div>
          </div>

          <div class="callout">
            <h4>Lupid AI recommends deny.</h4>
            <p>The request falls outside the current export profile and peer baseline.</p>
            <ul>
              <li>Target domain is outside the approved trust boundary.</li>
              <li>PII is present in the outbound payload.</li>
              <li>Peer agents do not hold this capability.</li>
            </ul>
          </div>

          <div class="workflow">
            <div class="workflow-step">
              <div class="workflow-icon">T</div>
              <div><h5>Trigger</h5><p>External CRM export from a watched agent.</p></div>
              <div class="badge amber">reviewing</div>
            </div>
            <div class="workflow-step">
              <div class="workflow-icon" style="color:var(--red);">R</div>
              <div><h5>Remove unsafe capability</h5><p>Revoke outbound CRM write scope.</p></div>
              <div class="badge blue">recommended</div>
            </div>
            <div class="workflow-step">
              <div class="workflow-icon" style="color:var(--blue);">N</div>
              <div><h5>Notify owners and security</h5><p>Send Slack and email.</p></div>
              <div class="badge green">prepared</div>
            </div>
          </div>

          <div class="grid-2" style="margin-top:14px;">
            <div class="signal">
              <h5>Why this surfaced</h5>
              <p>Alert severity is driven by external export plus PII plus peer mismatch, not just one rule hit.</p>
              <div class="micro">policy + peer baseline + destination trust</div>
            </div>
            <div class="signal">
              <h5>Operator action</h5>
              <p>Approve only with narrowed scope. The cleaner path is deny, revoke, and notify owners.</p>
              <div class="micro">decision required before queue expiry</div>
            </div>
          </div>
        </section>

        <section class="screen" id="screen-constellations">
          <div class="hero">
            <div class="hero-top">
              <div>
                <div class="eyebrow">Constellations</div>
                <h3>Teams behind the fleet</h3>
                <p>Ownership, watched agents, pending review, operator scope.</p>
              </div>
              <div class="badge violet">6 teams</div>
            </div>
          </div>
          <div class="panel">
            <div class="panel-head">
              <h4>Ownership map</h4>
              <span>teams and fleets</span>
            </div>
            <div class="panel-body">
              <table>
                <thead><tr><th>Team</th><th>Scope</th><th>Agents</th><th>Watched</th><th>Pending</th><th>Operators</th></tr></thead>
                <tbody>
                  <tr><td><strong>Revenue Systems</strong></td><td>commerce / revops</td><td>24</td><td>3</td><td>2</td><td>commerce@lupid.io</td></tr>
                  <tr><td><strong>Support Engineering</strong></td><td>customer ops</td><td>19</td><td>1</td><td>1</td><td>support@lupid.io</td></tr>
                  <tr><td><strong>Platform Security</strong></td><td>cross-tenant governance</td><td>128</td><td>8</td><td>12</td><td>security@lupid.io</td></tr>
                </tbody>
              </table>
            </div>
          </div>
        </section>

        <section class="screen" id="screen-calibration">
          <div class="hero">
            <div class="hero-top">
              <div>
                <div class="eyebrow">Calibration</div>
                <h3>Policy editing and agent-aware simulation</h3>
                <p>Validate, simulate, save, reload.</p>
              </div>
              <div class="cta-row">
                <button class="btn">Validate</button>
                <button class="btn">Reload all</button>
                <button class="btn primary">Publish</button>
              </div>
            </div>
          </div>
          <div class="grid-2">
            <div class="panel">
              <div class="panel-head">
                <h4>Current policy pack</h4>
                <span>payments-router</span>
              </div>
              <div class="panel-body">
                <div class="code">permit(
  principal == Agent::"payments-router",
  action in [Action::"ledger.lookup", Action::"vault.lease"],
  resource
)
when {
  context.tenant == "commerce" &&
  !context.external_domain &&
  !context.contains_unapproved_pii
};</div>
              </div>
            </div>
            <div class="panel">
              <div class="panel-head">
                <h4>Simulation</h4>
                <span>POST /policies/simulate</span>
              </div>
              <div class="panel-body">
                <div class="list">
                  <div class="list-row"><div><h5>Agent</h5><p>payments-router / commerce / high trust</p></div></div>
                  <div class="list-row"><div><h5>Scenario</h5><p>External export with customer email payload.</p></div></div>
                  <div class="list-row"><div><h5>Expected</h5><p>Deny or require approval.</p></div><span class="badge red">deny</span></div>
                </div>
              </div>
            </div>
          </div>
          <div class="grid-2" style="margin-top:14px;">
            <div class="signal">
              <h5>Simulation guidance</h5>
              <p>Policy tuning should be validated against one real agent context at a time, not abstract examples.</p>
              <div class="micro">trust, tenant, external domain, data class</div>
            </div>
            <div class="signal">
              <h5>Publication risk</h5>
              <p>Reloading all policies is safe here because the deny delta is isolated to one outbound action family.</p>
              <div class="micro">publish after validation and replay check</div>
            </div>
          </div>
        </section>
      </main>
    </div>
  </div>

  <script>
    const navButtons = document.querySelectorAll("[data-screen]");
    const jumpButtons = document.querySelectorAll("[data-screen-link]");
    const screens = document.querySelectorAll(".screen");

    function activateScreen(name) {
      navButtons.forEach((button) => {
        button.classList.toggle("active", button.dataset.screen === name);
      });
      screens.forEach((screen) => {
        screen.classList.toggle("active", screen.id === "screen-" + name);
      });
      window.scrollTo({ top: 0, behavior: "smooth" });
    }

    navButtons.forEach((button) => {
      button.addEventListener("click", () => activateScreen(button.dataset.screen));
    });

    jumpButtons.forEach((button) => {
      button.addEventListener("click", () => activateScreen(button.dataset.screenLink));
    });
  </script>
</body>
</html>
