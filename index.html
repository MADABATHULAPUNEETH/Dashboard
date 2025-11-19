from flask import Flask, jsonify, request, send_from_directory, Response
from flask_cors import CORS
import random, time, os, threading

app = Flask(__name__, static_folder='static', static_url_path='/static')
CORS(app)

# ---------------------
# Simulated data state
# ---------------------
NUM_BOTTLES = 6
bottles = []
for i in range(NUM_BOTTLES):
    lvl = random.randint(40, 90)
    hist = [max(5, min(98, lvl + random.randint(-3,3))) for _ in range(60)]
    bottles.append({"id": i, "level": lvl, "history": hist})

events = [
    {"time": "10:42:31", "text": "Underfill bottle detected"},
    {"time": "10:42:30", "text": "Label: BEVERAGE"},
    {"time": "10:42:29", "text": "Conveyor resumed"},
]

production_summary = [
    {"time": "10:42:31", "status": "OK", "fill": 98, "label": "Identified", "dimensions": "10x12"},
    {"time": "10:42:30", "status": "Underfilled", "fill": 55, "label": "Not Identified", "dimensions": "10x11"},
]

# Background thread to gently update simulated bottle values over time
def background_simulator():
    while True:
        time.sleep(2.0)
        for b in bottles:
            delta = random.randint(-3, 3)
            b['level'] = max(5, min(98, b['level'] + delta))
            b['history'].append(b['level'])
            if len(b['history']) > 240:
                b['history'].pop(0)
        # occasionally add events
        if random.random() < 0.08:
            events.insert(0, {"time": time.strftime("%H:%M:%S"), "text": f"Auto-sample: bottle {random.randint(1,NUM_BOTTLES)}"})
            if len(events) > 24:
                events[:] = events[:24]

# start background thread
t = threading.Thread(target=background_simulator, daemon=True)
t.start()

# ---------------------
# API endpoints
# ---------------------
@app.route('/api/metrics', methods=['GET'])
def api_metrics():
    """
    Returns JSON:
    {
      "bottles": [{"id":0,"level":72,"history":[...]} , ...],
      "events":[{"time":"10:42:31","text":"Underfill"}],
      "production_summary":[{"time":"10:42:31","status":"OK","fill":98,...}, ...]
    }
    """
    # Provide a shallow copy to avoid race conditions
    resp = {
        "bottles": [ {"id": b["id"], "level": b["level"], "history": b["history"][-120:]} for b in bottles ],
        "events": events[:12],
        "production_summary": production_summary[:10]
    }
    return jsonify(resp)

# Serve logo.png or logo.svg if present in static folder or project root
@app.route('/logo.png')
def logo_png():
    # look in static first, then root
    static_path = os.path.join(app.static_folder or "static", "logo.png")
    if os.path.exists(static_path):
        return send_from_directory(app.static_folder, "logo.png")
    root_path = os.path.join(os.getcwd(), "logo.png")
    if os.path.exists(root_path):
        return send_from_directory(os.getcwd(), "logo.png")
    return Response(status=404)

@app.route('/logo.svg')
def logo_svg():
    static_path = os.path.join(app.static_folder or "static", "logo.svg")
    if os.path.exists(static_path):
        return send_from_directory(app.static_folder, "logo.svg")
    root_path = os.path.join(os.getcwd(), "logo.svg")
    if os.path.exists(root_path):
        return send_from_directory(os.getcwd(), "logo.svg")
    return Response(status=404)

# ---------------------
# Serve the frontend HTML from root
# ---------------------
# The full single-file HTML (converted from index.html). If you prefer, you can store
# index.html on disk and serve it with send_from_directory instead.
INDEX_HTML = r"""
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>Sasha Innoworks — Live Dashboard (Flask)</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700;800&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#061026; --panel:#0e2033; --muted:#9fc0d9; --text:#eaf7ff;
  --sub:#cfeaf9; --accent:#2fb8ff; --accent-2:#6ecbff; --amber:#f1a63c;
  --radius:14px;
}
*{box-sizing:border-box}
body{margin:0;min-height:100vh;background:linear-gradient(180deg,#031021 0%,var(--bg) 100%);color:var(--text);font-family:Inter,system-ui,-apple-system,Segoe UI,Roboto,"Helvetica Neue",Arial}
.wrap{max-width:1180px;margin:18px auto;padding:16px;display:grid;gap:14px}
header.top{display:flex;align-items:center;gap:14px;padding:12px;border-radius:14px;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.006));border:1px solid rgba(47,184,255,0.06)}
.logo{width:60px;height:60px;border-radius:10px;background:linear-gradient(90deg,var(--amber),#d68a2a);display:flex;align-items:center;justify-content:center;font-weight:800;color:#081214}
.title{font-size:28px;font-weight:800;margin:0}
.company{font-size:12px;color:var(--sub);margin-top:4px}
.layout{display:grid;grid-template-columns:1fr 380px;gap:16px;margin-top:8px}
.panel{background:linear-gradient(180deg, rgba(255,255,255,0.01), rgba(255,255,255,0.006));padding:12px;border-radius:var(--radius);border:1px solid rgba(255,255,255,0.02)}
.feed-top{display:flex;justify-content:space-between;align-items:center;margin-bottom:8px}
.feed-area{height:360px;border-radius:12px;border:2px solid rgba(255,255,255,0.03);position:relative;display:flex;align-items:center;justify-content:center;overflow:hidden}
.camera{position:absolute;right:16px;top:12px;padding:6px 8px;border-radius:8px;background:rgba(255,255,255,0.03);color:var(--sub);font-weight:700}
.track{position:absolute;left:18px;right:18px;bottom:30px;height:60px;border-radius:999px;background:linear-gradient(180deg, rgba(255,255,255,0.01), rgba(255,255,255,0.00));display:flex;align-items:center;justify-content:space-around;padding:8px 24px;border:1px solid rgba(255,255,255,0.02)}
.wheel{width:26px;height:26px;border-radius:50%;background:linear-gradient(180deg, rgba(0,0,0,0.25), rgba(255,255,255,0.02))}
.bottle-strip{display:flex;gap:44px;align-items:flex-end;will-change:transform}
.bottle-box{width:72px;height:160px;display:flex;align-items:flex-end;justify-content:center}
.small{background:transparent;border:1px solid rgba(255,255,255,0.04);padding:6px 10px;border-radius:10px;color:var(--sub);cursor:pointer}
.controls{display:flex;align-items:center;justify-content:space-between;margin-top:12px}
.flow{display:flex;gap:10px;align-items:center;color:var(--sub);font-weight:700}
.dot{width:12px;height:12px;border-radius:50%;background:rgba(255,255,255,0.05);border:1px solid rgba(255,255,255,0.03);cursor:pointer}
.dot.active{background:linear-gradient(90deg,var(--accent),var(--accent-2));box-shadow:0 8px 22px rgba(47,184,255,0.08)}
.metrics{display:flex;flex-direction:column;gap:12px}
.metric-card{padding:12px;border-radius:10px;background:linear-gradient(180deg, rgba(255,255,255,0.01), transparent);border:1px solid rgba(255,255,255,0.02)}
.metric-title{font-weight:800;color:var(--sub);margin-bottom:6px}
.big-val{font-size:26px;font-weight:800}
.progress{height:12px;border-radius:999px;background:rgba(255,255,255,0.03);overflow:hidden}
.progress>i{display:block;height:100%;width:0;background:linear-gradient(90deg,var(--accent),var(--accent-2));transition:width 600ms ease}
.events{max-height:170px;overflow:auto;margin-top:8px}
.events li{padding:8px 6px;border-bottom:1px solid rgba(255,255,255,0.02);color:var(--sub)}
.bottom{margin-top:12px;display:grid;grid-template-columns:1fr 420px;gap:16px}
table{width:100%;border-collapse:collapse}
thead th{color:var(--sub);font-weight:800;text-align:left;padding:10px;border-bottom:1px solid rgba(255,255,255,0.03)}
tbody td{padding:12px 8px;border-bottom:1px solid rgba(255,255,255,0.02);color:var(--text)}
.graph-panel{padding:12px;border-radius:12px;background:linear-gradient(180deg, rgba(255,255,255,0.01), transparent);border:1px solid rgba(255,255,255,0.02)}
.canvas{width:100%;height:180px;display:block}
.bottle-selected{outline:3px solid rgba(47,184,255,0.12);border-radius:12px;padding:4px}
@media (max-width:980px){.layout{grid-template-columns:1fr}.bottom{grid-template-columns:1fr}.metrics{order:2}}
.liquid-amber { fill: var(--amber); opacity: 0.95; }
.liquid-cyan { fill: var(--accent); opacity: 0.95; }
</style>
</head>
<body>
<div class="wrap">
  <header class="top">
    <img id="logoImg" src="/logo.png" alt="logo" onerror="applyPlaceholderLogo()" style="width:60px;height:60px;border-radius:10px;object-fit:cover;border:3px solid rgba(0,0,0,0.06)">
    <div>
      <div class="title">Dashboard</div>
      <div class="company">Sasha Innoworks</div>
    </div>
    <div style="margin-left:auto;display:flex;gap:12px;align-items:center">
      <div style="color:var(--sub);font-weight:700">Operator: <span style="color:var(--text)">Operator 1</span></div>
      <button class="small">Profile</button>
    </div>
  </header>

  <div class="layout">
    <!-- left -->
    <section class="panel">
      <div class="feed-top">
        <div style="font-weight:800;font-size:18px">Conveyor Feed</div>
        <div style="color:var(--sub)">Status: <strong id="statusText" style="color:var(--accent)">Running</strong></div>
      </div>

      <div class="feed-area" id="feedArea">
        <div class="camera">CAM</div>
        <div style="width:92%;max-width:880px;position:relative">
          <div class="bottle-strip" id="bottleStrip" aria-hidden="true">
            <div class="bottle-box"><svg class="bottle-svg" data-bid="0" viewBox="0 0 72 160" width="72" height="160">
              <path d="M26 0h20a6 6 0 0 1 6 6v16a10 10 0 0 1 10 10v110a12 12 0 0 1-12 12H22a12 12 0 0 1-12-12V32a10 10 0 0 1 10-10V6a6 6 0 0 1 6-6z" fill="none" stroke="#eaf7ff" stroke-width="3"/>
              <rect class="liquid-rect liquid-amber" x="16" y="72" rx="8" width="40" height="68"></rect>
            </svg></div>
            <div class="bottle-box"><svg class="bottle-svg" data-bid="1" viewBox="0 0 72 160" width="72" height="160">
              <path d="M26 0h20a6 6 0 0 1 6 6v16a10 10 0 0 1 10 10v110a12 12 0 0 1-12 12H22a12 12 0 0 1-12-12V32a10 10 0 0 1 10-10V6a6 6 0 0 1 6-6z" fill="none" stroke="#eaf7ff" stroke-width="3" stroke-dasharray="6 6"/>
              <rect class="liquid-rect liquid-amber" x="16" y="92" rx="8" width="40" height="48"></rect>
            </svg></div>
            <div class="bottle-box"><svg class="bottle-svg" data-bid="2" viewBox="0 0 72 160" width="72" height="160">
              <path d="M26 0h20a6 6 0 0 1 6 6v16a10 10 0 0 1 10 10v110a12 12 0 0 1-12 12H22a12 12 0 0 1-12-12V32a10 10 0 0 1 10-10V6a6 6 0 0 1 6-6z" fill="none" stroke="#eaf7ff" stroke-width="3"/>
              <rect class="liquid-rect liquid-amber" x="16" y="64" rx="8" width="40" height="96"></rect>
            </svg></div>
            <div class="bottle-box"><svg class="bottle-svg" data-bid="3" viewBox="0 0 72 160" width="72" height="160">
              <path d="M26 0h20a6 6 0 0 1 6 6v16a10 10 0 0 1 10 10v110a12 12 0 0 1-12 12H22a12 12 0 0 1-12-12V32a10 10 0 0 1 10-10V6a6 6 0 0 1 6-6z" fill="none" stroke="#eaf7ff" stroke-width="3"/>
              <rect class="liquid-rect liquid-amber" x="16" y="98" rx="8" width="40" height="40"></rect>
            </svg></div>
            <div class="bottle-box"><svg class="bottle-svg" data-bid="0" viewBox="0 0 72 160" width="72" height="160">
              <path d="M26 0h20a6 6 0 0 1 6 6v16a10 10 0 0 1 10 10v110a12 12 0 0 1-12 12H22a12 12 0 0 1-12-12V32a10 10 0 0 1 10-10V6a6 6 0 0 1 6-6z" fill="none" stroke="#eaf7ff" stroke-width="3"/>
              <rect class="liquid-rect liquid-amber" x="16" y="68" rx="8" width="40" height="88"></rect>
            </svg></div>
            <div class="bottle-box"><svg class="bottle-svg" data-bid="1" viewBox="0 0 72 160" width="72" height="160">
              <path d="M26 0h20a6 6 0 0 1 6 6v16a10 10 0 0 1 10 10v110a12 12 0 0 1-12 12H22a12 12 0 0 1-12-12V32a10 10 0 0 1 10-10V6a6 6 0 0 1 6-6z" fill="none" stroke="#eaf7ff" stroke-width="3"/>
              <rect class="liquid-rect liquid-amber" x="16" y="86" rx="8" width="40" height="60"></rect>
            </svg></div>
          </div>

          <div class="track" aria-hidden="true">
            <div class="wheel"></div><div class="wheel"></div><div class="wheel"></div><div class="wheel"></div>
          </div>
        </div>
      </div>

      <div class="controls">
        <div class="flow">
