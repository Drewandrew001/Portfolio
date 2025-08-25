<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Andrew Nyamwange Omwamba - Portfolio</title>
  <style>
    :root{
      --green:#0a0; /* primary */
      --green-dark:#070; /* hover */
      --bg:#111; --fg:#eee; --muted:#d4ffd4; --card:#222;
    }
    *{box-sizing:border-box}
    body{margin:0;font-family:Arial,Helvetica,sans-serif;background:var(--bg);color:var(--fg);line-height:1.6}
    header{background:var(--green);color:#fff;padding:2rem 1rem;text-align:center}
    header h1{margin:0;font-size:2.4rem}
    header p{font-size:1.1rem;color:var(--muted)}
    nav{background:#000;padding:.6rem;text-align:center;position:sticky;top:0;z-index:5}
    nav a{color:#0f0;margin:0 14px;text-decoration:none;font-weight:bold}
    nav a:hover{color:#fff}
    section{padding:2rem;max-width:980px;margin:auto}
    h2{color:#0f0;border-bottom:2px solid #0f0;padding-bottom:.3rem;margin-top:0}
    .grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(240px,1fr));gap:1rem}
    .card{background:var(--card);border-radius:12px;box-shadow:0 6px 14px rgba(0,0,0,.45);padding:1rem}
    .btn{display:inline-block;margin:10px 10px 0 0;padding:10px 18px;border:none;border-radius:9px;background:var(--green);color:#fff;font-size:1rem;cursor:pointer;text-decoration:none;transition:.25s}
    .btn:hover{background:var(--green-dark)}
    .muted{color:#bfbfbf}
    footer{text-align:center;padding:1rem;background:#000;color:#0f0;margin-top:2rem}
    /* Admin panel */
    #adminToggle{font-size:.9rem;opacity:.75}
    #uploadPanel{display:none;margin-top:1rem}
    .row{display:flex;gap:10px;flex-wrap:wrap;align-items:center}
    input[type=file]{background:#000;border:1px solid #333;color:#ddd;padding:10px;border-radius:8px}
    input[type=text]{background:#000;border:1px solid #333;color:#ddd;padding:10px;border-radius:8px;min-width:260px}
    progress{width:260px;height:14px}
    .pill{display:inline-block;background:#003300;color:#9cff9c;padding:4px 10px;border-radius:999px;font-size:.85rem}
    .tip{font-size:.9rem;color:#cfe9cf}
    .hide{display:none}
  </style>
</head>
<body>
  <header>
    <h1>Andrew Nyamwange Omwamba</h1>
    <p>Teacher | Computer Instructor | CBC Competent</p>
  </header>  <nav>
    <a href="#about">About</a>
    <a href="#experience">Experience</a>
    <a href="#contact">Contact</a>
  </nav>  <section id="about">
    <h2>About Me</h2>
    <p>
      Hello! My name is <strong>Andrew Nyamwange Omwamba</strong>.
      I am a dedicated teacher by profession with experience in both academic and computer instruction.
      I am passionate about education, technology, and empowering learners through the CBC curriculum.
    </p>
  </section>  <section id="experience">
    <h2>Experience</h2>
    <div class="grid">
      <div class="card">
        <h3>Gichuru Boys High School</h3>
        <p>Taught as a professional educator, focusing on nurturing students’ academic and personal growth.</p>
      </div>
      <div class="card">
        <h3>NEXGEN Cyber (Computer Training)</h3>
        <p>Computer instructor guiding learners in digital literacy, computer applications, and modern skills.</p>
      </div>
      <div class="card">
        <h3>CBC Competence</h3>
        <p>Well-versed with the Competency Based Curriculum (CBC) to meet modern educational standards.</p>
      </div>
    </div>
  </section>  <section id="contact">
    <h2>Contact Me</h2>
    <p>📞 Phone: 0706 265 491</p>
    <p>📱 WhatsApp: 0755 151 901</p>
    <p>📧 Email: <a href="mailto:nyamwangeandrew91@gmail.com">nyamwangeandrew91@gmail.com</a></p><a class="btn" href="https://wa.me/254755151901?text=I%20want%20to%20hire%20you" target="_blank">📩 Hire Me</a>
<button class="btn" onclick="alert('Send your tip via M-Pesa to: 0706265491')">💸 Tip Me</button>
<a id="cvLink" class="btn" href="docs/cv.pdf" download>📂 Download CV & Documents</a>

<div class="muted" style="margin-top:12px">
  <button id="adminToggle" class="btn" style="background:#003300">Owner Tools</button>
  <span class="pill">Private</span>
</div>

<div id="uploadPanel" class="card">
  <h3>Upload New CV / Documents</h3>
  <p class="tip">Uploads go to your Cloudinary account (free). After upload, the Download button updates automatically for <em>you</em> and anyone who loads this page with the new link embedded; to make it permanent for all visitors, update the site file later with the new URL (or ask me to wire a database).</p>
  <div class="row">
    <input id="cloudName" type="text" placeholder="Cloudinary cloud name (e.g. yourname)" />
    <input id="uploadPreset" type="text" placeholder="Unsigned upload preset" />
    <input id="folder" type="text" placeholder="Folder (optional, e.g. cv)" />
  </div>
  <div class="row" style="margin-top:8px">
    <input id="file" type="file" accept=".pdf,.doc,.docx,.zip" />
    <button id="uploadBtn" class="btn">⬆️ Upload</button>
    <progress id="prog" max="100" value="0" class="hide"></progress>
  </div>
  <p id="status" class="tip"></p>
</div>

  </section>  <footer>
    <p>&copy; 2025 Andrew Nyamwange Omwamba | All Rights Reserved</p>
  </footer>  <script>
    // --- Owner Tools toggle (hidden by default). Show when URL has ?admin=1 or after passphrase.
    const adminToggle = document.getElementById('adminToggle');
    const panel = document.getElementById('uploadPanel');
    const params = new URLSearchParams(location.search);
    if (params.get('admin') === '1') panel.style.display = 'block';
    adminToggle.addEventListener('click', () => {
      const ok = prompt('Enter owner passphrase to open uploads (set any phrase you like):', localStorage.getItem('andrew_pass')||'');
      if(ok){ localStorage.setItem('andrew_pass', ok); panel.style.display='block'; }
    });

    // --- Cloudinary unsigned upload (no secret keys in browser) ---
    const fileInput = document.getElementById('file');
    const uploadBtn = document.getElementById('uploadBtn');
    const statusEl = document.getElementById('status');
    const prog = document.getElementById('prog');
    const cvLink = document.getElementById('cvLink');
    const cloudNameEl = document.getElementById('cloudName');
    const presetEl = document.getElementById('uploadPreset');
    const folderEl = document.getElementById('folder');

    // restore last values to save typing
    cloudNameEl.value = localStorage.getItem('cloudName') || '';
    presetEl.value = localStorage.getItem('uploadPreset') || '';
    folderEl.value = localStorage.getItem('folder') || '';

    uploadBtn.addEventListener('click', async () => {
      const file = fileInput.files && fileInput.files[0];
      const cloud = cloudNameEl.value.trim();
      const preset = presetEl.value.trim();
      const folder = folderEl.value.trim();

      if(!file){ alert('Choose a file first (PDF/DOC/ZIP).'); return; }
      if(!cloud || !preset){ alert('Enter your Cloudinary cloud name and unsigned preset.'); return; }

      localStorage.setItem('cloudName', cloud);
      localStorage.setItem('uploadPreset', preset);
      localStorage.setItem('folder', folder);

      const url = `https://api.cloudinary.com/v1_1/${cloud}/auto/upload`;
      const fd = new FormData();
      fd.append('file', file);
      fd.append('upload_preset', preset);
      if(folder) fd.append('folder', folder);

      statusEl.textContent = 'Uploading…';
      prog.classList.remove('hide');
      prog.value = 0;

      try{
        const resp = await fetch(url, { method:'POST', body: fd });
        const data = await resp.json();
        if(!data || !data.secure_url){ throw new Error(data.error?.message || 'Upload failed'); }

        // Update the Download button live
        cvLink.href = data.secure_url;
        cvLink.setAttribute('download','');
        statusEl.textContent = 'Uploaded ✔  Download button updated to latest file.';
        prog.classList.add('hide');

      }catch(err){
        statusEl.textContent = 'Error: ' + err.message;
        prog.classList.add('hide');
      }
    });

    // upload progress (best-effort with XHR for progress events)
    (function enableProgress(){
      uploadBtn.removeEventListener('click', ()=>{});
      uploadBtn.addEventListener('click', function handler(ev){
        // override to use XHR for progress
        const file = fileInput.files && fileInput.files[0];
        const cloud = cloudNameEl.value.trim();
        const preset = presetEl.value.trim();
        const folder = folderEl.value.trim();
        if(!file || !cloud || !preset) return; // main click handler already alerts

        ev.preventDefault();
        const url = `https://api.cloudinary.com/v1_1/${cloud}/auto/upload`;
        const fd = new FormData();
        fd.append('file', file);
        fd.append('upload_preset', preset);
        if(folder) fd.append('folder', folder);

        const xhr = new XMLHttpRequest();
        xhr.open('POST', url);
        xhr.upload.addEventListener('progress', (e)=>{
          if(e.lengthComputable){ prog.classList.remove('hide'); prog.value = Math.round(e.loaded*100/e.total); }
        });
        xhr.onload = ()=>{
          try{ const data = JSON.parse(xhr.responseText);
            if(!data.secure_url) throw new Error(data.error?.message || 'Upload failed');
            cvLink.href = data.secure_url; cvLink.setAttribute('download','');
            statusEl.textContent = 'Uploaded ✔  Download button updated to latest file.'; prog.classList.add('hide');
          }catch(err){ statusEl.textContent = 'Error: '+err.message; prog.classList.add('hide'); }
        };
        xhr.onerror = ()=>{ statusEl.textContent = 'Network error during upload'; prog.classList.add('hide'); };
        statusEl.textContent = 'Uploading…'; xhr.send(fd);
      }, { once:true });
    })();
  </script></body>
</html>
