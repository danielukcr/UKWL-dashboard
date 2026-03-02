
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Moderation Dashboard</title>
  <style>
    :root{
      --bg:#0b1220;
      --panel:#0f1a31;
      --panel2:#111f3a;
      --text:#e7ecff;
      --muted:#aab3d6;
      --accent:#5b8cff;
      --danger:#ff4d6d;
      --ok:#19c37d;
      --warn:#ffb020;
      --border:rgba(255,255,255,.10);
      --shadow: 0 12px 40px rgba(0,0,0,.45);
      --radius:18px;
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial;
      background: radial-gradient(1200px 800px at 15% 10%, rgba(91,140,255,.22), transparent 60%),
                  radial-gradient(1000px 700px at 90% 20%, rgba(255,77,109,.10), transparent 55%),
                  var(--bg);
      color:var(--text);
      min-height:100vh;
    }
    .topbar{
      position:sticky; top:0;
      backdrop-filter: blur(10px);
      background: rgba(11,18,32,.65);
      border-bottom: 1px solid var(--border);
      z-index: 10;
    }
    .topbar-inner{
      max-width:1100px;
      margin:0 auto;
      padding:14px 18px;
      display:flex;
      align-items:center;
      justify-content:space-between;
      gap:14px;
    }
    .brand{
      display:flex; align-items:center; gap:12px;
      min-width: 220px;
    }
    .brand-title{
      font-weight:800;
      letter-spacing:.4px;
      line-height:1.1;
    }
    .brand-sub{
      color:var(--muted);
      font-size:12px;
      margin-top:2px;
    }
    .banner{
      height:18px;
      width: 420px;
      max-width: 48vw;
      object-fit:cover;
      border-radius:999px;
      border:1px solid var(--border);
      opacity:.95;
    }
    .wrap{
      max-width:1100px;
      margin:0 auto;
      padding:22px 18px 60px;
    }

    .grid{
      display:grid;
      grid-template-columns: 1.25fr .85fr;
      gap:18px;
    }
    @media (max-width: 980px){
      .grid{grid-template-columns: 1fr;}
      .banner{display:none}
    }

    .card{
      background: linear-gradient(180deg, rgba(17,31,58,.9), rgba(15,26,49,.92));
      border:1px solid var(--border);
      border-radius: var(--radius);
      box-shadow: var(--shadow);
      padding:18px;
    }
    .card h2{
      margin:0 0 4px;
      font-size:18px;
      letter-spacing:.2px;
    }
    .hint{
      margin:0 0 14px;
      color:var(--muted);
      font-size:13px;
      line-height:1.4;
    }

    .form{
      display:grid;
      gap:12px;
    }
    .row{
      display:grid;
      grid-template-columns: 1fr 1fr;
      gap:12px;
    }
    @media (max-width: 620px){
      .row{grid-template-columns:1fr;}
    }
    label{
      display:block;
      font-size:12px;
      color:var(--muted);
      margin:0 0 6px;
    }
    input, select, textarea{
      width:100%;
      background: rgba(255,255,255,.06);
      border:1px solid var(--border);
      color:var(--text);
      padding:12px 12px;
      border-radius: 14px;
      outline:none;
      transition: .15s ease;
      font-size:14px;
    }
    textarea{min-height: 110px; resize: vertical;}
    input:focus, select:focus, textarea:focus{
      border-color: rgba(91,140,255,.65);
      box-shadow: 0 0 0 4px rgba(91,140,255,.14);
    }
    .actions{
      display:flex;
      gap:10px;
      flex-wrap:wrap;
      align-items:center;
      margin-top:4px;
    }
    button{
      border:0;
      cursor:pointer;
      padding:11px 14px;
      border-radius: 14px;
      font-weight:700;
      letter-spacing:.2px;
      color: var(--text);
      background: rgba(91,140,255,.90);
      transition: .15s ease;
    }
    button:hover{transform: translateY(-1px); filter:brightness(1.05)}
    button:disabled{opacity:.55; cursor:not-allowed; transform:none}
    .btn-ghost{
      background: rgba(255,255,255,.08);
      border: 1px solid var(--border);
      font-weight:650;
    }
    .btn-danger{
      background: rgba(255,77,109,.90);
    }

    .status{
      margin-top: 10px;
      font-size: 13px;
      color: var(--muted);
      line-height: 1.4;
    }
    .status.ok{color: rgba(25,195,125,.95)}
    .status.err{color: rgba(255,77,109,.95)}
    .status.warn{color: rgba(255,176,32,.95)}

    .preview{
      display:grid;
      gap:12px;
    }
    .pill{
      display:inline-flex;
      gap:8px;
      align-items:center;
      padding:8px 10px;
      border-radius:999px;
      border:1px solid var(--border);
      background: rgba(255,255,255,.05);
      color: var(--muted);
      font-size: 12px;
      width: fit-content;
    }
    .pill b{color: var(--text); font-weight:800}
    .thumb{
      width:100%;
      border-radius: var(--radius);
      border:1px solid var(--border);
      overflow:hidden;
      background: rgba(0,0,0,.15);
    }
    .thumb img{
      width:100%;
      display:block;
      object-fit:cover;
      aspect-ratio: 16 / 9;
    }
    .small{
      font-size:12px; color: var(--muted); line-height:1.5;
    }

    /* Login overlay */
    .overlay{
      position:fixed;
      inset:0;
      display:flex;
      align-items:center;
      justify-content:center;
      background: rgba(0,0,0,.55);
      backdrop-filter: blur(10px);
      z-index: 999;
      padding: 18px;
    }
    .login{
      width:min(520px, 100%);
      background: linear-gradient(180deg, rgba(17,31,58,.98), rgba(15,26,49,.98));
      border:1px solid var(--border);
      border-radius: 22px;
      box-shadow: var(--shadow);
      padding: 18px;
    }
    .login h1{
      margin:0 0 6px;
      font-size: 20px;
      letter-spacing:.2px;
    }
    .login p{
      margin:0 0 14px;
      color: var(--muted);
      font-size: 13px;
      line-height: 1.45;
    }
    .login .row1{
      display:grid;
      grid-template-columns: 1fr auto;
      gap: 10px;
      align-items:end;
    }
  </style>
</head>
<body>

  <!-- Login Gate -->
  <div class="overlay" id="overlay">
    <div class="login">
      <h1>Moderation Dashboard</h1>
      <p>Enter the dashboard password to continue.</p>

      <div class="row1">
        <div>
          <label for="pw">Password</label>
          <input id="pw" type="password" placeholder="Enter password" autocomplete="current-password" />
        </div>
        <button id="btnLogin">Login</button>
      </div>

      <div class="status" id="loginStatus" style="margin-top:10px;"></div>
      <p class="small" style="margin-top:12px;">
        Note: this password check is client-side only. If you host this publicly, it is not secure.
      </p>
    </div>
  </div>

  <div class="topbar">
    <div class="topbar-inner">
      <div class="brand">
        <div>
          <div class="brand-title">Moderation Dashboard</div>
          <div class="brand-sub">Log actions to Discord via webhook</div>
        </div>
      </div>
      <img class="banner" id="bannerImg" alt="Banner" />
      <div style="display:flex; gap:10px; align-items:center;">
        <button class="btn-ghost" id="btnLogout" title="Logout">Logout</button>
      </div>
    </div>
  </div>

  <div class="wrap">
    <div class="grid">
      <div class="card">
        <h2>Create Moderation Log</h2>
        <p class="hint">Fill the details and click <b>Send to Discord</b>. This will post an embed to your webhook.</p>

        <form class="form" id="modForm">
          <div class="row">
            <div>
              <label for="discordUser">Discord username</label>
              <input id="discordUser" name="discordUser" placeholder="e.g. user#1234 or @user" required />
            </div>
            <div>
              <label for="discordId">Discord ID</label>
              <input id="discordId" name="discordId" placeholder="e.g. 123456789012345678" required />
            </div>
          </div>

          <div class="row">
            <div>
              <label for="type">Type</label>
              <select id="type" name="type" required>
                <option value="Mute">Mute</option>
                <option value="Kick">Kick</option>
                <option value="Ban">Ban</option>
                <option value="Blacklist">Blacklist</option>
                <option value="Ban-bolo">Ban-bolo</option>
                <option value="Warning">Warning</option>
              </select>
            </div>
            <div>
              <label for="givenBy">Given By</label>
              <input id="givenBy" name="givenBy" placeholder="Your username" required />
            </div>
          </div>

          <div>
            <label for="reason">Reason</label>
            <textarea id="reason" name="reason" placeholder="Enter reason..." required></textarea>
          </div>

          <div class="actions">
            <button type="submit" id="btnSend">Send to Discord</button>
            <button type="button" class="btn-ghost" id="btnClear">Clear</button>
          </div>

          <div class="status" id="status"></div>
        </form>
      </div>

      <div class="card">
        <h2>Preview</h2>
        <p class="hint">This is roughly what your embed will contain.</p>

        <div class="preview">
          <div class="pill">Type: <b id="pvType">Mute</b></div>
          <div class="pill">User: <b id="pvUser">—</b></div>
          <div class="pill">ID: <b id="pvId">—</b></div>
          <div class="pill">Given By: <b id="pvGivenBy">—</b></div>
          <div class="pill">Reason: <b id="pvReason">—</b></div>

          <div class="thumb">
            <img id="thumbImg" alt="Thumbnail" />
          </div>

          <p class="small">
            Tip: If you share/host this page, your webhook can be stolen from the source. A backend proxy is safer.
          </p>
        </div>
      </div>
    </div>
  </div>

<script>
  // =========================
  // CONFIG (your details)
  // =========================
  const WEBHOOK_URL = "https://discord.com/api/webhooks/1477933777245437954/nlEA9GN0e52JSBnTtn3sJnSdzf5z7ICSq5LY50ujD7D8w9fWePnsZSDGWxfjW9nBC8bV";
  const DASHBOARD_PASSWORD = "0506_0";

  const LARGE_IMAGE_URL = "https://media.discordapp.net/attachments/1372809054027644969/1477558796481073304/Untitled_design_2.png?ex=69a5335c&is=69a3e1dc&hm=37a15950158fd4bc1bfc3500c2378d16bd651c08695b063a73ecb583cf2a2358&=&format=webp&quality=lossless&width=1857&height=53";
  const THUMBNAIL_URL = "https://media.discordapp.net/attachments/1372809054027644969/1477563760053977110/Screenshot_2026-03-01_071019-removebg-preview.png?ex=69a537fc&is=69a3e67c&hm=aa6665acc07a1da4a9ee45b037d0ff75b9fe7cadbb33c6a9a5ec170a1292089e&=&format=webp&quality=lossless&width=671&height=378";

  // =========================
  // Helpers
  // =========================
  function escapeMarkdown(s){
    return String(s ?? "")
      .replace(/\\/g, "\\\\")
      .replace(/\*/g, "\\*")
      .replace(/_/g, "\\_")
      .replace(/`/g, "\\`")
      .replace(/~/g, "\\~")
      .replace(/\|/g, "\\|");
  }

  function typeColor(type){
    // Discord embed colors are integers (0xRRGGBB).
    switch(type){
      case "Ban": return 0xFF4D6D;
      case "Kick": return 0xFFB020;
      case "Mute": return 0x5B8CFF;
      case "Warning": return 0xFFB020;
      case "Blacklist": return 0xA855F7;
      case "Ban-bolo": return 0x22C55E;
      default: return 0x5B8CFF;
    }
  }

  function setStatus(el, msg, cls){
    el.className = "status " + (cls || "");
    el.textContent = msg || "";
  }

  // =========================
  // Login gate
  // =========================
  const overlay = document.getElementById("overlay");
  const pw = document.getElementById("pw");
  const btnLogin = document.getElementById("btnLogin");
  const loginStatus = document.getElementById("loginStatus");
  const btnLogout = document.getElementById("btnLogout");

  function isLoggedIn(){
    return localStorage.getItem("moddash_loggedin") === "1";
  }
  function showApp(){
    overlay.style.display = "none";
  }
  function showLogin(){
    overlay.style.display = "flex";
    pw.value = "";
  }

  btnLogin.addEventListener("click", () => {
    if(pw.value === DASHBOARD_PASSWORD){
      localStorage.setItem("moddash_loggedin", "1");
      setStatus(loginStatus, "", "");
      showApp();
    } else {
      setStatus(loginStatus, "Incorrect password.", "err");
    }
  });

  pw.addEventListener("keydown", (e) => {
    if(e.key === "Enter"){
      e.preventDefault();
      btnLogin.click();
    }
  });

  btnLogout.addEventListener("click", () => {
    localStorage.removeItem("moddash_loggedin");
    showLogin();
  });

  // Init login state
  if(isLoggedIn()) showApp(); else showLogin();

  // =========================
  // UI init
  // =========================
  document.getElementById("bannerImg").src = LARGE_IMAGE_URL;
  document.getElementById("thumbImg").src = THUMBNAIL_URL;

  const form = document.getElementById("modForm");
  const statusEl = document.getElementById("status");
  const btnSend = document.getElementById("btnSend");
  const btnClear = document.getElementById("btnClear");

  // Preview elements
  const pvType = document.getElementById("pvType");
  const pvUser = document.getElementById("pvUser");
  const pvId = document.getElementById("pvId");
  const pvGivenBy = document.getElementById("pvGivenBy");
  const pvReason = document.getElementById("pvReason");

  function updatePreview(){
    const discordUser = document.getElementById("discordUser").value.trim();
    const discordId = document.getElementById("discordId").value.trim();
    const type = document.getElementById("type").value;
    const reason = document.getElementById("reason").value.trim();
    const givenBy = document.getElementById("givenBy").value.trim();

    pvType.textContent = type || "—";
    pvUser.textContent = discordUser || "—";
    pvId.textContent = discordId || "—";
    pvGivenBy.textContent = givenBy || "—";
    pvReason.textContent = (reason ? (reason.length > 60 ? reason.slice(0, 60) + "…" : reason) : "—");
  }

  ["discordUser","discordId","type","reason","givenBy"].forEach(id => {
    document.getElementById(id).addEventListener("input", updatePreview);
    document.getElementById(id).addEventListener("change", updatePreview);
  });
  updatePreview();

  btnClear.addEventListener("click", () => {
    form.reset();
    updatePreview();
    setStatus(statusEl, "", "");
  });

  // =========================
  // Submit -> Discord Webhook
  // =========================
  form.addEventListener("submit", async (e) => {
    e.preventDefault();
    setStatus(statusEl, "", "");

    const discordUser = document.getElementById("discordUser").value.trim();
    const discordId = document.getElementById("discordId").value.trim();
    const type = document.getElementById("type").value;
    const reason = document.getElementById("reason").value.trim();
    const givenBy = document.getElementById("givenBy").value.trim();

    if(!discordUser || !discordId || !type || !reason || !givenBy){
      setStatus(statusEl, "Please fill in all fields.", "warn");
      return;
    }

    // Basic ID check (optional)
    if(!/^\d{10,25}$/.test(discordId)){
      setStatus(statusEl, "Discord ID looks invalid (expected numbers only). Sending anyway is blocked—please fix it.", "err");
      return;
    }

    btnSend.disabled = true;
    setStatus(statusEl, "Sending to Discord...", "");

    const nowISO = new Date().toISOString();

    const payload = {
      username: "Moderation Logs",
      // You can also set avatar_url if you want
      embeds: [
        {
          title: `Moderation Action: ${type}`,
          color: typeColor(type),
          timestamp: nowISO,
          thumbnail: { url: THUMBNAIL_URL },
          image: { url: LARGE_IMAGE_URL },
          fields: [
            { name: "Discord Username", value: escapeMarkdown(discordUser), inline: true },
            { name: "Discord ID", value: escapeMarkdown(discordId), inline: true },
            { name: "Type", value: escapeMarkdown(type), inline: true },
            { name: "Reason", value: escapeMarkdown(reason), inline: false },
            { name: "Given By", value: escapeMarkdown(givenBy), inline: true },
          ],
          footer: { text: "Moderation Dashboard" }
        }
      ]
    };

    try{
      const res = await fetch(WEBHOOK_URL, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(payload)
      });

      if(!res.ok){
        const text = await res.text().catch(() => "");
        setStatus(statusEl, `Discord rejected the request (${res.status}). ${text ? "Details: " + text : ""}`, "err");
      } else {
        setStatus(statusEl, "Sent successfully ✅", "ok");
        // Optional: clear after send
        // form.reset(); updatePreview();
      }
    } catch(err){
      setStatus(statusEl, "Failed to send (network/CORS). If you opened this as a file:// URL, try hosting it via a local server.", "err");
    } finally {
      btnSend.disabled = false;
    }
  });
</script>

</body>
</html>
