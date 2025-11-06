<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Plate to Heart - Dashboard</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700;800&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg: #0e141b;
      --panel: #131b26;
      --accent: linear-gradient(135deg, #00bfa5 0%, #00796b 100%);
      --card-bg: rgba(255, 255, 255, 0.03);
      --muted: #9aa4b2;
      --text: #e6eef3;
      --success: #16a34a;
      --danger: #ef4444;
    }

    body {
      margin: 0;
      font-family: 'Inter', sans-serif;
      background: radial-gradient(1000px 600px at 10% 10%, rgba(0, 123, 98, 0.08), transparent), linear-gradient(180deg, #071018, #09141b);
      color: var(--text);
      -webkit-font-smoothing: antialiased;
    }

    .topbar {
      position: sticky;
      top: 0;
      z-index: 50;
      display: flex;
      align-items: center;
      justify-content: space-between;
      background: rgba(255, 255, 255, 0.02);
      backdrop-filter: blur(6px);
      padding: 14px 20px;
      border-bottom: 1px solid rgba(255, 255, 255, 0.03);
    }

    .brand {
      display: flex;
      align-items: center;
      gap: 12px;
      font-weight: 800;
      font-size: 18px;
    }

    .brand .logo {
      width: 40px;
      height: 40px;
      border-radius: 10px;
      background: var(--accent);
      display: flex;
      align-items: center;
      justify-content: center;
      color: #041014;
      font-weight:800;
    }

    .wrap {
      display: grid;
      grid-template-columns: 260px 1fr;
      gap: 24px;
      padding: 20px;
      min-height: calc(100vh - 60px);
    }

    @media (max-width: 900px) {
      .wrap {
        grid-template-columns: 1fr;
      }
    }

    .sidebar {
      background: var(--panel);
      border-radius: 14px;
      padding: 16px;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      border: 1px solid rgba(255, 255, 255, 0.04);
    }

    .nav button {
      display: flex;
      align-items: center;
      gap: 12px;
      padding: 12px;
      border: none;
      border-radius: 10px;
      background: transparent;
      color: var(--text);
      font-weight: 600;
      cursor: pointer;
      width:100%;
      text-align:left;
    }

    .nav button:hover, .nav button.active {
      background: var(--accent);
      color: #041014;
    }

    .main {
      background: transparent;
      border-radius: 16px;
      padding: 0;
    }

    .page-card {
      background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
      border-radius: 14px;
      padding: 18px;
      border: 1px solid rgba(255,255,255,0.03);
      box-shadow: 0 8px 30px rgba(2,6,23,0.6);
      margin-bottom: 16px;
    }

    .home-header {
      display: flex;
      align-items: center;
      gap: 10px;
      font-size: 22px;
      font-weight: 700;
      margin-bottom: 6px;
    }

    .home-subtitle {
      color: var(--muted);
      font-size: 14px;
      margin-bottom: 20px;
    }

    .kpi-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 16px;
      margin-bottom: 20px;
    }

    .kpi-card {
      background: linear-gradient(145deg, rgba(0, 191, 165, 0.12), rgba(0, 121, 107, 0.04));
      border: 1px solid rgba(255, 255, 255, 0.04);
      border-radius: 14px;
      padding: 16px;
      box-shadow: 0 8px 24px rgba(0, 0, 0, 0.28);
    }

    .kpi-title { font-weight: 600; color: var(--muted); margin-bottom: 8px; }
    .kpi-value { font-size: 26px; font-weight: 800; }

    .quick-actions { background: rgba(255,255,255,0.02); padding: 20px; border-radius: 14px; border: 1px solid rgba(255,255,255,0.03);} 
    .btns { display:flex; gap:12px; flex-wrap:wrap; }
    .btn { padding:10px 16px; border-radius:10px; border:none; font-weight:700; cursor:pointer; }
    .btn.primary { background:var(--accent); color:#041014; }
    .btn.outline { background:transparent; border:1px solid rgba(255,255,255,0.06); color:var(--text); }

    /* donor list */
    .donor-row{display:flex;align-items:center;justify-content:space-between;padding:12px;border-radius:10px;margin-bottom:10px;background:linear-gradient(180deg, rgba(255,255,255,0.01), transparent);border:1px solid rgba(255,255,255,0.02)}
    .avatar{width:56px;height:56px;border-radius:10px;background:rgba(255,255,255,0.03);display:flex;align-items:center;justify-content:center;font-weight:700}
    .muted{color:var(--muted)}

    input[type=text], input[type=number], select{background:transparent;border:1px solid rgba(255,255,255,0.04);padding:8px;border-radius:8px;color:var(--text)}

    .location-status{font-size:12px;margin-top:6px}
    .location-status.success{color:var(--success)}
    .location-status.error{color:var(--danger)}

  </style>
</head>
<body>
  <div class="topbar">
    <div class="brand">
      <div class="logo">🍽</div>
      <div>Plate to Heart</div>
    </div>
    <div style="display:flex;gap:10px;align-items:center">
      <input id="globalSearch" placeholder="Search..." style="padding:8px 10px;border-radius:8px;background:rgba(255,255,255,0.02);border:1px solid rgba(255,255,255,0.03);color:var(--text)" />
      <button class="btn outline" onclick="exportData()">Export</button>
    </div>
  </div>

  <div class="wrap">
    <aside class="sidebar">
      <div>
        <div style="font-weight:700;margin-bottom:12px">Dashboard</div>
        <div class="nav">
          <button id="nav-home" class="active" onclick="show('home');setActive('nav-home')">🏠 Home</button>
          <button id="nav-upload" onclick="show('upload');setActive('nav-upload')">⬆️ Upload Plate</button>
          <button id="nav-available" onclick="show('available');setActive('nav-available')">📦 Available Plates</button>
          <button id="nav-history" onclick="show('history');setActive('nav-history')">📜 History</button>
        </div>
      </div>
      <div style="display:flex;flex-direction:column;gap:8px">
        <div class="muted" style="font-size:13px">Signed in</div>
        <button class="btn outline" onclick="handleLogout()">🚪 Logout</button>
      </div>
    </aside>

    <main class="main">
      <!-- HOME -->
      <section id="home" class="page-card">
        <div class="home-header">👋 Welcome Back</div>
        <div class="home-subtitle">Manage food donations and help reduce waste in your community</div>

        <div class="kpi-grid">
          <div class="kpi-card">
            <div class="kpi-title">Total Plates Available</div>
            <div id="totalPlates" class="kpi-value">0</div>
          </div>

          <div class="kpi-card">
            <div class="kpi-title">Active Donors</div>
            <div id="totalDonors" class="kpi-value">0</div>
          </div>

          <div class="kpi-card">
            <div class="kpi-title">Total Pickups (History)</div>
            <div id="totalHistory" class="kpi-value">0</div>
          </div>
        </div>

        <div class="quick-actions">
          <h4 style="margin:0 0 10px">Quick Actions</h4>
          <div class="btns">
            <button class="btn primary" onclick="show('upload');setActive('nav-upload')">⬆️ Upload New Plate</button>
            <button class="btn outline" onclick="show('available');setActive('nav-available')">📦 View Available Plates</button>
          </div>
        </div>
      </section>

      <!-- UPLOAD -->
      <section id="upload" class="page-card" style="display:none">
        <h3 style="margin:0 0 8px">Upload Plate Availability</h3>
        <p class="muted">Donors can add plates here. Location and optional address help volunteers find pickups faster.</p>

        <form id="uploadForm" style="margin-top:12px">
          <div style="display:flex;gap:10px;margin-bottom:10px">
            <input id="u_name" type="text" placeholder="Donor name (e.g. Hotel Sunshine)" style="flex:2" required />
            <select id="u_type" style="flex:1">
              <option value="hotel">Hotel</option>
              <option value="hostel">Hostel</option>
              <option value="charity">Charity</option>
            </select>
          </div>

          <div style="display:flex;gap:10px;margin-bottom:10px">
            <input id="u_plates" type="number" min="1" placeholder="Number of plates" required style="flex:1" />
            <div style="flex:2">
              <div style="display:flex;gap:8px;align-items:center">
                <input id="u_location" type="text" placeholder="Location (optional)" style="flex:1" />
                <button type="button" class="btn primary" id="getLocationBtn" onclick="getCurrentLocation()">📍 Get</button>
              </div>
              <div id="locationStatus" class="location-status"></div>
            </div>
          </div>

          <div style="display:flex;gap:10px;align-items:center;margin-bottom:10px">
            <div style="flex:1">
              <div class="muted">Food Type</div>
              <label style="margin-right:12px"><input type="radio" name="foodType" value="Veg" checked> Veg</label>
              <label><input type="radio" name="foodType" value="Non-Veg"> Non-Veg</label>
            </div>
            <div style="flex:2">
              <div class="muted">Curry Name (optional)</div>
              <input id="u_curry" type="text" placeholder="e.g. Sambar / Chicken Curry" />
            </div>
          </div>

          <div style="display:flex;gap:10px">
            <button type="submit" class="btn primary">Upload to Available Plates</button>
            <button type="button" class="btn outline" onclick="show('home')">Cancel</button>
          </div>
        </form>
      </section>

      <!-- AVAILABLE -->
      <section id="available" class="page-card" style="display:none">
        <h3 style="margin:0 0 8px">Available Plates</h3>
        <div class="page-card" style="margin-top:10px;padding:12px">
          <div id="donorList" class="muted">Loading donors...</div>
        </div>
      </section>

      <!-- HISTORY -->
      <section id="history" class="page-card" style="display:none">
        <h3 style="margin:0 0 8px">Pickup History</h3>
        <p class="muted">Completed pickups are stored here for audit and reporting.</p>
        <div class="page-card" style="margin-top:8px;padding:12px">
          <div id="historyList" class="muted">Loading history...</div>
        </div>
        <div style="margin-top:12px;display:flex;gap:10px;flex-wrap:wrap">
          <button class="btn primary" onclick="clearHistory()">Clear History</button>
          <button class="btn outline" onclick="exportData()">Export Data (console)</button>
        </div>
      </section>

    </main>
  </div>

  <!-- Firebase-powered script attached -->
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/12.5.0/firebase-app.js";
    import { getAnalytics } from "https://www.gstatic.com/firebasejs/12.5.0/firebase-analytics.js";
    import {
      getFirestore, collection, addDoc, getDocs, onSnapshot,
      updateDoc, deleteDoc, doc, serverTimestamp
    } from "https://www.gstatic.com/firebasejs/12.5.0/firebase-firestore.js";

    const firebaseConfig = {
      apiKey: "AIzaSyCayftL5J0J8tU227qDL1cguBTkfXtj4Fg",
      authDomain: "plate-to-heart-30bd2.firebaseapp.com",
      projectId: "plate-to-heart-30bd2",
      storageBucket: "plate-to-heart-30bd2.firebasestorage.app",
      messagingSenderId: "940060297380",
      appId: "1:940060297380:web:fca392b7dd3da5dce27e31",
      measurementId: "G-K6Q9KHRZYC"
    };

    const app = initializeApp(firebaseConfig);
    try { getAnalytics(app); } catch(e) { /* analytics optional */ }
    const db = getFirestore(app);

    // state
    let donors = [];
    let history = [];
    let currentLocationData = null;

    const toInt = v => Number.isFinite(+v) ? Math.max(0, Math.floor(+v)) : 0;
    const esc = s => s ? String(s).replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":"&#39;"}[c])) : '';

    function renderSummary(){
      const total = donors.reduce((s,d) => s + toInt(d.plates), 0);
      document.getElementById('totalPlates').textContent = total;
      document.getElementById('totalDonors').textContent = donors.length;
      document.getElementById('totalHistory').textContent = history.length;
    }

    function renderDonors(){
      const container = document.getElementById('donorList');
      container.innerHTML = '';
      if(!donors || donors.length === 0){
        container.innerHTML = '<div class="muted">No plates available right now.</div>';
        renderSummary();
        return;
      }

      donors.forEach(d => {
        const status = d.status || 'available';
        const plateCount = toInt(d.plates);

        const node = document.createElement('div');
        node.className = 'donor-row';

        node.innerHTML = `
          <div style="display:flex;align-items:center;gap:12px;flex:1">
            <div class="avatar">${esc(d.name ? d.name.charAt(0).toUpperCase() : 'H')}</div>
            <div style="flex:1">
              <div style="display:flex;align-items:center;justify-content:space-between;gap:12px">
                <div style="font-weight:700;color:#eafaf5">${esc(d.name)} <span class="muted" style="font-weight:700"> · ${esc(d.type || '')}</span></div>
                <div style="font-weight:800">${plateCount} <span class="muted">plates</span></div>
              </div>
              <div class="muted" style="margin-top:6px">${d.location ? esc(d.location) + ' · ' : ''}${d.foodType ? esc(d.foodType) : ''}${d.curry ? ' · ' + esc(d.curry) : ''}</div>

              ${status === 'pickup_requested' ? `
                <div class="page-card" id="pickup-form-${d.id}" style="margin-top:12px">
                  <div style="font-weight:700;margin-bottom:8px;color:var(--success)">📦 Pickup Details</div>
                  <div style="display:flex;gap:10px;margin-bottom:8px">
                    <label style="min-width:120px">Your Name:</label>
                    <input type="text" id="picker-name-${d.id}" placeholder="Enter your name" required style="flex:1" />
                  </div>
                  <div style="display:flex;gap:10px;align-items:center">
                    <label style="min-width:120px">How many plates?</label>
                    <input type="number" id="pickup-qty-${d.id}" min="1" max="${plateCount}" value="1" />
                    <div class="muted">(Max: ${plateCount})</div>
                  </div>
                  <div style="display:flex;gap:8px;margin-top:8px">
                    <button class="btn outline" onclick="completePickup('${d.id}')">Complete Pickup</button>
                    <button class="btn outline" onclick="cancelRequest('${d.id}')">Cancel Request</button>
                  </div>
                </div>
              ` : ''}

            </div>
          </div>
          <div style="display:flex;flex-direction:column;align-items:flex-end;gap:8px;margin-left:12px">
            ${status === 'pickup_requested' ? `<button class="btn outline" onclick="cancelRequest('${d.id}')">Cancel</button>` : `<div style="display:flex;gap:8px"><button class="btn primary" onclick="requestPickup('${d.id}')">Request Pickup</button><button class="btn outline" onclick="quickRemove('${d.id}')">Quick Remove</button></div>`}
          </div>
        `;

        container.appendChild(node);
      });

      renderSummary();
    }

    function renderHistory(){
      const el = document.getElementById('historyList');
      el.innerHTML = '';
      if(!history || history.length === 0){ el.innerHTML = '<div class="muted">No pickups completed yet.</div>'; return; }

      history.slice().reverse().forEach(rec => {
        const ts = rec.ts && rec.ts.seconds ? new Date(rec.ts.seconds * 1000).toLocaleString() : (rec.ts ? new Date(rec.ts).toLocaleString() : '');
        const totalPlates = toInt(rec.plates);
        const pickupQuantity = toInt(rec.pickupQuantity || rec.plates);
        const remainingPlates = toInt(rec.remainingPlates || 0);
        const pickerName = rec.pickerName || 'Unknown';

        const row = document.createElement('div');
        row.className = 'donor-row';
        row.style.borderBottom = '1px dashed rgba(255,255,255,0.03)';
        row.innerHTML = `
          <div style="flex:1">
            <div style="font-weight:700">${esc(rec.name)} <span class="muted">· ${esc(rec.type || '')}</span></div>
            <div class="muted" style="margin-top:6px">${rec.location ? esc(rec.location) + ' · ' : ''}${rec.foodType ? esc(rec.foodType) : ''}${rec.curry ? ' · ' + esc(rec.curry) : ''}</div>
            ${pickerName && pickerName !== 'Unknown' ? `<div class="muted" style="margin-top:6px;color:var(--success)">👤 Picked up by: <strong>${esc(pickerName)}</strong></div>` : ''}
          </div>
          <div style="text-align:right;min-width:160px">
            <div style="font-weight:800">${pickupQuantity > 0 ? `✓ ${pickupQuantity} picked` : `${totalPlates} plates`}</div>
            ${remainingPlates > 0 ? `<div class="muted" style="color:#ffb86b;margin-top:6px">${remainingPlates} left</div>` : ''}
            <div class="muted" style="margin-top:8px">${ts}</div>
          </div>
        `;
        el.appendChild(row);
      });

      renderSummary();
    }

    // Location tracking
    window.getCurrentLocation = function(){
      const statusDiv = document.getElementById('locationStatus');
      const locationInput = document.getElementById('u_location');
      const getLocationBtn = document.getElementById('getLocationBtn');

      if(!navigator.geolocation){ statusDiv.textContent = 'Geolocation not supported.'; statusDiv.className='location-status error'; return; }
      getLocationBtn.disabled = true; getLocationBtn.textContent = 'Getting...'; statusDiv.textContent='Getting your location...'; statusDiv.className='location-status';

      navigator.geolocation.getCurrentPosition(async function(position){
        const lat = position.coords.latitude; const lng = position.coords.longitude; const accuracy = position.coords.accuracy;
        currentLocationData = { lat, lng, accuracy };
        try{
          const response = await fetch(`https://nominatim.openstreetmap.org/reverse?format=json&lat=${lat}&lon=${lng}&zoom=18&addressdetails=1`);
          const data = await response.json();
          if(data && data.address){
            const addr = data.address; const parts = [];
            if(addr.road) parts.push(addr.road); if(addr.house_number) parts.push(addr.house_number);
            if(addr.suburb || addr.neighbourhood) parts.push(addr.suburb || addr.neighbourhood);
            if(addr.city || addr.town || addr.village) parts.push(addr.city || addr.town || addr.village);
            if(addr.state) parts.push(addr.state);
            const address = parts.length ? parts.join(', ') : `${lat.toFixed(6)}, ${lng.toFixed(6)}`;
            locationInput.value = address; currentLocationData.address = address;
            statusDiv.textContent = `✓ Location found: ${address}`; statusDiv.className='location-status success';
          } else {
            locationInput.value = `${lat.toFixed(6)}, ${lng.toFixed(6)}`; currentLocationData.address = locationInput.value;
            statusDiv.textContent = `✓ Location found: ${lat.toFixed(6)}, ${lng.toFixed(6)}`; statusDiv.className='location-status success';
          }
        }catch(e){ locationInput.value = `${lat.toFixed(6)}, ${lng.toFixed(6)}`; currentLocationData.address = locationInput.value; statusDiv.textContent = `✓ Location found: ${lat.toFixed(6)}, ${lng.toFixed(6)}`; statusDiv.className='location-status success'; }
        getLocationBtn.disabled = false; getLocationBtn.textContent = '📍 Get';
      }, function(error){
        let errorMsg = 'Unable to get your location. ';
        switch(error.code){ case error.PERMISSION_DENIED: errorMsg += 'Location access denied.'; break; case error.POSITION_UNAVAILABLE: errorMsg += 'Position unavailable.'; break; case error.TIMEOUT: errorMsg += 'Timed out.'; break; default: errorMsg += 'Unknown.'; break; }
        document.getElementById('locationStatus').textContent = errorMsg; document.getElementById('locationStatus').className='location-status error';
        document.getElementById('getLocationBtn').disabled = false; document.getElementById('getLocationBtn').textContent = '📍 Get';
      }, { enableHighAccuracy: true, timeout:10000, maximumAge:0 });
    };

    // UPLOAD handler
    document.getElementById('uploadForm').addEventListener('submit', async function(e){
      e.preventDefault();
      const name = document.getElementById('u_name').value.trim();
      const type = document.getElementById('u_type').value || 'hotel';
      const plates = toInt(document.getElementById('u_plates').value);
      const location = document.getElementById('u_location').value.trim();
      const curry = document.getElementById('u_curry').value.trim();
      const foodType = (document.querySelector('input[name="foodType"]:checked') || {}).value || '';

      if(!name || plates <= 0){ alert('Enter donor name and 1 or more plates.'); return; }

      try{
        const donorData = { name, type, plates, location, curry, foodType, status:'available', ts: serverTimestamp() };
        if(currentLocationData){ donorData.locationLat = currentLocationData.lat; donorData.locationLng = currentLocationData.lng; donorData.locationAccuracy = currentLocationData.accuracy; if(currentLocationData.address) donorData.locationAddress = currentLocationData.address; }
        await addDoc(collection(db,'donors'), donorData);
        document.getElementById('uploadForm').reset(); document.getElementById('locationStatus').textContent=''; currentLocationData = null; show('available'); alert('Uploaded successfully!');
      }catch(err){ console.error('Upload failed', err); alert('Failed to upload. Check console.'); }
    });

    // Actions
    window.requestPickup = async function(id){ try{ await updateDoc(doc(db,'donors',id),{ status:'pickup_requested' }); alert('Pickup requested.'); }catch(e){ console.error(e); alert('Failed to request pickup'); } };
    window.cancelRequest = async function(id){ try{ await updateDoc(doc(db,'donors',id),{ status:'available' }); }catch(e){ console.error(e); alert('Failed to cancel'); } };

    window.quickRemove = async function(id){ if(!confirm('Move this donor to history (remove from Available)?')) return; try{ const donor = donors.find(d=>d.id===id); if(!donor) throw new Error('donor not found'); const totalPlates = toInt(donor.plates); await addDoc(collection(db,'history'),{ ...donor, plates: totalPlates, pickupQuantity: totalPlates, remainingPlates:0, ts: serverTimestamp() }); await deleteDoc(doc(db,'donors',id)); }catch(e){ console.error(e); alert('Failed to move to history'); } };

    window.completePickup = async function(id){ try{
      const donor = donors.find(d => d.id === id); if(!donor) throw new Error('donor not found');
      const pickerNameInput = document.getElementById(`picker-name-${id}`); const pickerName = pickerNameInput ? pickerNameInput.value.trim() : '';
      const pickupQtyInput = document.getElementById(`pickup-qty-${id}`); const pickupQuantity = toInt(pickupQtyInput ? pickupQtyInput.value : 0);
      const totalPlates = toInt(donor.plates);
      if(!pickerName){ alert('Please enter your name before completing the pickup.'); return; }
      if(pickupQuantity <=0 || pickupQuantity > totalPlates){ alert(`Please enter a valid quantity between 1 and ${totalPlates}.`); return; }
      const remainingPlates = totalPlates - pickupQuantity;
      await addDoc(collection(db,'history'), {...donor, plates: totalPlates, pickupQuantity, remainingPlates, pickerName, ts: serverTimestamp() });
      if(remainingPlates>0){ await updateDoc(doc(db,'donors',id),{ plates: remainingPlates, status:'available' }); alert(`Pickup completed! ${pickupQuantity} picked up by ${pickerName}. ${remainingPlates} left.`); } else { await deleteDoc(doc(db,'donors',id)); alert(`Pickup completed! All ${pickupQuantity} picked up by ${pickerName}.`); }
    }catch(e){ console.error(e); alert('Failed to complete pickup'); } };

    window.clearHistory = async function(){ if(!confirm('Clear entire history? This cannot be undone.')) return; try{ const snap = await getDocs(collection(db,'history')); const deletes = []; snap.forEach(d=>deletes.push(deleteDoc(doc(db,'history',d.id)))); await Promise.all(deletes); alert('History cleared!'); }catch(e){ console.error(e); alert('Failed to clear history'); } };

    window.exportData = function(){ console.log('donors', donors); console.log('history', history); alert('Data exported to console. Open DevTools to inspect.'); };

    window.handleLogout = function(){ if(confirm('Are you sure you want to logout?')) { window.location = 'login-new.html'; } };

    window.show = function(id){ ['home','upload','available','history'].forEach(k=>{ const el = document.getElementById(k); if(el) el.style.display = (k===id)?'block':'none'; }); };

    function setActive(id){ document.querySelectorAll('.nav button').forEach(b=>b.classList.remove('active')); const btn = document.getElementById(id); if(btn) btn.classList.add('active'); }

    // realtime listeners
    onSnapshot(collection(db,'donors'), (snap)=>{ donors = snap.docs.map(d=>({ id:d.id, ...d.data() })); donors.sort((a,b)=> (b.ts?.seconds||0) - (a.ts?.seconds||0)); renderDonors(); }, (err)=>{ console.error('donors snapshot error',err); document.getElementById('donorList').textContent = 'Failed to load donors.'; });

    onSnapshot(collection(db,'history'), (snap)=>{ history = snap.docs.map(d=>({ id:d.id, ...d.data() })); history.sort((a,b)=> (b.ts?.seconds||0) - (a.ts?.seconds||0)); renderHistory(); }, (err)=>{ console.error('history snapshot error',err); document.getElementById('historyList').textContent = 'Failed to load history.'; });

    (function init(){ show('home'); })();
  </script>
</body>
</html>

