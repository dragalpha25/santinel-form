
<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SANTINEL – Fiche d'inscription</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<style>
@import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@300;400;500;600&family=Syne:wght@700;800&display=swap');

:root {
  --orange: #E05A1E;
  --orange-light: #FFF3ED;
  --navy: #0F2040;
  --navy-mid: #1A3260;
  --slate: #64748B;
  --border: #DDE3EE;
  --bg: #F0F3F9;
  --white: #FFFFFF;
  --green: #059669;
  --red: #DC2626;
  --locked: #94A3B8;
  --locked-bg: #F8FAFC;
}

* { box-sizing: border-box; margin: 0; padding: 0; }

body {
  font-family: 'DM Sans', sans-serif;
  background: var(--bg);
  color: var(--navy);
  min-height: 100vh;
}

/* ─── HEADER ─── */
header {
  background: var(--navy);
  padding: 0 2rem;
  height: 64px;
  display: flex;
  align-items: center;
  gap: 1.5rem;
  position: sticky;
  top: 0;
  z-index: 200;
  box-shadow: 0 2px 20px rgba(0,0,0,.3);
}
.logo {
  font-family: 'Syne', sans-serif;
  font-weight: 800;
  font-size: 1.6rem;
  color: var(--white);
  letter-spacing: .06em;
}
.logo em { color: var(--orange); font-style: normal; }
.header-divider { width: 1px; height: 32px; background: rgba(255,255,255,.15); }
.header-title {
  font-size: .75rem;
  font-weight: 500;
  color: rgba(255,255,255,.55);
  letter-spacing: .12em;
  text-transform: uppercase;
}
.progress-wrap {
  margin-left: auto;
  display: flex;
  align-items: center;
  gap: .75rem;
}
.progress-track {
  width: 160px;
  height: 3px;
  background: rgba(255,255,255,.12);
  border-radius: 2px;
  overflow: hidden;
}
.progress-fill {
  height: 100%;
  background: var(--orange);
  border-radius: 2px;
  transition: width .4s ease;
  width: 0%;
}
.progress-pct {
  font-size: .72rem;
  color: rgba(255,255,255,.45);
  font-weight: 500;
  min-width: 36px;
}

/* ─── LAYOUT ─── */
.page {
  max-width: 820px;
  margin: 2.5rem auto 5rem;
  padding: 0 1rem;
}

/* ─── ROLE BANNER ─── */
.role-banner {
  display: flex;
  gap: 1rem;
  margin-bottom: 1.75rem;
}
.role-pill {
  display: flex;
  align-items: center;
  gap: .5rem;
  padding: .5rem 1rem;
  border-radius: 8px;
  font-size: .78rem;
  font-weight: 600;
  letter-spacing: .05em;
}
.role-pill.candidate {
  background: var(--orange-light);
  color: var(--orange);
  border: 1.5px solid #F5C4A8;
}
.role-pill.receiver {
  background: #EFF6FF;
  color: #2563EB;
  border: 1.5px solid #BFDBFE;
}
.role-pill svg { flex-shrink: 0; }

/* ─── SECTION CARD ─── */
.section-card {
  background: var(--white);
  border-radius: 14px;
  overflow: hidden;
  margin-bottom: 1.25rem;
  box-shadow: 0 2px 12px rgba(15,32,64,.07);
  border: 1px solid var(--border);
}
.section-card.locked {
  opacity: .7;
  pointer-events: none;
}
.section-head {
  padding: .7rem 1.4rem;
  display: flex;
  align-items: center;
  gap: .65rem;
}
.section-head.candidate-head { background: var(--navy); }
.section-head.locked-head { background: #CBD5E1; }
.section-head h3 {
  font-family: 'Syne', sans-serif;
  font-weight: 700;
  font-size: .8rem;
  letter-spacing: .12em;
  text-transform: uppercase;
}
.section-head.candidate-head h3 { color: var(--white); }
.section-head.locked-head h3 { color: #64748B; }
.section-badge {
  margin-left: auto;
  font-size: .65rem;
  font-weight: 600;
  letter-spacing: .08em;
  padding: .2rem .6rem;
  border-radius: 20px;
}
.badge-candidate { background: var(--orange); color: white; }
.badge-locked { background: rgba(100,116,139,.2); color: #64748B; }
.section-icon { font-size: .95rem; }
.section-body { padding: 1.4rem; }

/* ─── FIELDS ─── */
.row { display: grid; gap: 1rem; margin-bottom: 1rem; }
.row:last-child { margin-bottom: 0; }
.cols-2 { grid-template-columns: 1fr 1fr; }
.cols-1 { grid-template-columns: 1fr; }
@media(max-width:560px) { .cols-2 { grid-template-columns: 1fr; } }

.field { display: flex; flex-direction: column; gap: .3rem; }
label {
  font-size: .68rem;
  font-weight: 600;
  letter-spacing: .1em;
  text-transform: uppercase;
  color: var(--slate);
}
.req { color: var(--orange); margin-left: 2px; }

input[type=text], input[type=email], input[type=tel], input[type=date] {
  width: 100%;
  border: 1.5px solid var(--border);
  border-radius: 8px;
  padding: .6rem .9rem;
  font-family: 'DM Sans', sans-serif;
  font-size: .95rem;
  color: var(--navy);
  background: #FAFBFE;
  transition: border-color .2s, box-shadow .2s, background .2s;
  outline: none;
}
input:focus {
  border-color: var(--navy);
  background: var(--white);
  box-shadow: 0 0 0 3px rgba(15,32,64,.08);
}
input.locked-field {
  background: var(--locked-bg);
  border-color: #E2E8F0;
  color: var(--locked);
  cursor: not-allowed;
}

/* ─── INITIALS / SIGNATURE ─── */
.sig-box {
  border: 2px dashed var(--orange);
  border-radius: 12px;
  background: var(--orange-light);
  padding: 1.5rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
}
.sig-label-area {
  text-align: center;
}
.sig-label-area h4 {
  font-family: 'Syne', sans-serif;
  font-weight: 700;
  font-size: .95rem;
  color: var(--navy);
  margin-bottom: .25rem;
}
.sig-label-area p {
  font-size: .78rem;
  color: var(--slate);
  line-height: 1.5;
}
.initials-wrap {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: .5rem;
  width: 100%;
  max-width: 280px;
}
#initials-input {
  text-align: center;
  font-family: 'Syne', sans-serif;
  font-size: 2.2rem;
  font-weight: 800;
  letter-spacing: .25em;
  text-transform: uppercase;
  border: 2px solid var(--orange);
  border-radius: 10px;
  background: var(--white);
  padding: .5rem 1rem;
  color: var(--navy);
  width: 100%;
  max-width: 200px;
}
#initials-input:focus {
  box-shadow: 0 0 0 4px rgba(224,90,30,.15);
}
.sig-preview {
  display: none;
  flex-direction: column;
  align-items: center;
  gap: .25rem;
}
.sig-preview.visible { display: flex; }
.sig-stamp {
  font-family: 'Syne', sans-serif;
  font-weight: 800;
  font-size: 3rem;
  color: var(--navy);
  letter-spacing: .3em;
  line-height: 1;
  border-bottom: 3px solid var(--orange);
  padding-bottom: .2rem;
}
.sig-date-stamp {
  font-size: .7rem;
  color: var(--slate);
  letter-spacing: .06em;
}
.sig-legal {
  font-size: .7rem;
  color: var(--slate);
  text-align: center;
  max-width: 340px;
  line-height: 1.5;
  border-top: 1px solid #F5C4A8;
  padding-top: .75rem;
  width: 100%;
}
.sig-legal strong { color: var(--orange); }

/* ─── LOCKED SECTION NOTICE ─── */
.locked-notice {
  display: flex;
  align-items: center;
  gap: .6rem;
  background: #F1F5F9;
  border: 1px solid #CBD5E1;
  border-radius: 8px;
  padding: .75rem 1rem;
  font-size: .8rem;
  color: #475569;
  margin-bottom: 1rem;
}
.locked-notice svg { flex-shrink: 0; color: #94A3B8; }

/* ─── SUBMIT ─── */
.submit-card {
  background: var(--navy);
  border-radius: 14px;
  padding: 1.75rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1.25rem;
  box-shadow: 0 8px 30px rgba(15,32,64,.2);
}
.submit-card h3 {
  font-family: 'Syne', sans-serif;
  font-weight: 700;
  font-size: 1rem;
  color: var(--white);
  letter-spacing: .06em;
}
.email-row {
  display: flex;
  gap: .75rem;
  width: 100%;
  max-width: 480px;
  align-items: flex-end;
}
.email-row .field { flex: 1; }
.email-row label { color: rgba(255,255,255,.5); }
.email-row input {
  background: rgba(255,255,255,.08);
  border-color: rgba(255,255,255,.2);
  color: white;
}
.email-row input::placeholder { color: rgba(255,255,255,.3); }
.email-row input:focus {
  background: rgba(255,255,255,.12);
  border-color: var(--orange);
  box-shadow: 0 0 0 3px rgba(224,90,30,.25);
}
.btn {
  display: flex;
  align-items: center;
  gap: .55rem;
  padding: .75rem 2rem;
  border: none;
  border-radius: 9px;
  font-family: 'Syne', sans-serif;
  font-weight: 700;
  font-size: .9rem;
  letter-spacing: .1em;
  text-transform: uppercase;
  cursor: pointer;
  transition: all .2s;
}
.btn-primary {
  background: var(--orange);
  color: white;
  box-shadow: 0 4px 16px rgba(224,90,30,.4);
}
.btn-primary:hover { background: #c94d14; transform: translateY(-1px); }
.btn-primary:active { transform: translateY(0); }
.btn-primary:disabled { background: #94A3B8; box-shadow: none; cursor: not-allowed; transform: none; }
.submit-note {
  font-size: .73rem;
  color: rgba(255,255,255,.35);
  text-align: center;
  max-width: 400px;
  line-height: 1.6;
}

/* ─── TOAST ─── */
#toast {
  position: fixed;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%) translateY(100px);
  background: var(--navy);
  color: white;
  padding: .7rem 1.75rem;
  border-radius: 50px;
  font-size: .88rem;
  font-weight: 500;
  border-left: 4px solid var(--orange);
  transition: transform .3s cubic-bezier(.34,1.56,.64,1);
  pointer-events: none;
  z-index: 9999;
  box-shadow: 0 8px 24px rgba(0,0,0,.2);
  white-space: nowrap;
}
#toast.show { transform: translateX(-50%) translateY(0); }

/* fade-in */
.section-card { animation: fadeUp .35s ease both; }
.section-card:nth-child(2) { animation-delay: .05s; }
.section-card:nth-child(3) { animation-delay: .1s; }
.section-card:nth-child(4) { animation-delay: .15s; }
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(14px); }
  to   { opacity: 1; transform: translateY(0); }
}
</style>
</head>
<body>

<header>
  <div class="logo">S<em>A</em>NTINEL</div>
  <div class="header-divider"></div>
  <div class="header-title">Fiche d'inscription participant(e)</div>
  <div class="progress-wrap">
    <div class="progress-track"><div class="progress-fill" id="pBar"></div></div>
    <div class="progress-pct" id="pPct">0 %</div>
  </div>
</header>

<div class="page">

  <!-- Role legend -->
  <div class="role-banner">
    <div class="role-pill candidate">
      <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
      À remplir par le participant
    </div>
    <div class="role-pill receiver">
      <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><rect x="3" y="8" width="18" height="13" rx="2"/><path d="M3 8l9 6 9-6"/><path d="M8 8V5a4 4 0 0 1 8 0v3"/></svg>
      Réservé au formateur / établissement
    </div>
  </div>

  <!-- ══ SECTION 1 : COORDONNÉES PERSONNELLES ══ -->
  <div class="section-card">
    <div class="section-head candidate-head">
      <span class="section-icon">👤</span>
      <h3>Coordonnées personnelles</h3>
      <span class="section-badge badge-candidate">Participant</span>
    </div>
    <div class="section-body">
      <div class="row cols-2">
        <div class="field">
          <label>Prénom <span class="req">*</span></label>
          <input type="text" id="prenom" placeholder="Jean" oninput="prog()">
        </div>
        <div class="field">
          <label>Nom <span class="req">*</span></label>
          <input type="text" id="nom" placeholder="Tremblay" oninput="prog()">
        </div>
      </div>
      <div class="row cols-1">
        <div class="field">
          <label>Adresse du domicile (No civique, rue, ville et code postal)</label>
          <input type="text" id="adresse_domicile" placeholder="123, rue des Érables, Montréal QC H2X 1Y3" oninput="prog()">
        </div>
      </div>
      <div class="row cols-2">
        <div class="field">
          <label>Téléphone (domicile)</label>
          <input type="tel" id="tel_domicile" placeholder="514 555-0001" oninput="prog()">
        </div>
        <div class="field">
          <label>Courrier électronique</label>
          <input type="email" id="courriel_perso" placeholder="jean.tremblay@courriel.com" oninput="prog()">
        </div>
      </div>
    </div>
  </div>

  <!-- ══ SECTION 2 : COORDONNÉES TRAVAIL ══ -->
  <div class="section-card">
    <div class="section-head candidate-head">
      <span class="section-icon">🏢</span>
      <h3>Coordonnées relatives au travail</h3>
      <span class="section-badge badge-candidate">Participant</span>
    </div>
    <div class="section-body">
      <div class="row cols-2">
        <div class="field">
          <label>Métier ou profession</label>
          <input type="text" id="metier" placeholder="Infirmier(ère), pompier…" oninput="prog()">
        </div>
        <div class="field">
          <label>Nom de l'établissement</label>
          <input type="text" id="etablissement" placeholder="Centre hospitalier XYZ" oninput="prog()">
        </div>
      </div>
      <div class="row cols-2">
        <div class="field">
          <label>Téléphone (établissement)</label>
          <input type="tel" id="tel_etab" placeholder="450 555-0002" oninput="prog()">
        </div>
        <div class="field">
          <label>Adresse de l'établissement</label>
          <input type="text" id="adresse_etab" placeholder="456, boul. des Laurentides, Laval QC H7G 2W1" oninput="prog()">
        </div>
      </div>
      <div class="row cols-2">
        <div class="field">
          <label>Prénom et nom du supérieur</label>
          <input type="text" id="superieur" placeholder="Marie Dupont" oninput="prog()">
        </div>
        <div class="field">
          <label>Courrier électronique (supérieur)</label>
          <input type="email" id="courriel_sup" placeholder="marie.dupont@etablissement.com" oninput="prog()">
        </div>
      </div>
    </div>
  </div>

  <!-- ══ SECTION 3 : COURS ══ -->
  <div class="section-card">
    <div class="section-head candidate-head">
      <span class="section-icon">📚</span>
      <h3>Renseignements sur le cours</h3>
      <span class="section-badge badge-candidate">Participant</span>
    </div>
    <div class="section-body">
      <div class="row cols-2">
        <div class="field">
          <label>Titre du cours <span class="req">*</span></label>
          <input type="text" id="titre_cours" placeholder="Premiers secours en milieu de travail" oninput="prog()">
        </div>
        <div class="field">
          <label>Date du cours <span class="req">*</span></label>
          <input type="date" id="date_cours" oninput="prog()">
        </div>
      </div>
    </div>
  </div>

  <!-- ══ SIGNATURE PAR INITIALES ══ -->
  <div class="section-card">
    <div class="section-head candidate-head">
      <span class="section-icon">✍️</span>
      <h3>Signature électronique</h3>
      <span class="section-badge badge-candidate">Participant</span>
    </div>
    <div class="section-body">
      <div class="sig-box">
        <div class="sig-label-area">
          <h4>Signez avec vos initiales</h4>
          <p>Entrez vos initiales ci-dessous. Elles serviront de signature électronique et seront intégrées au PDF soumis.</p>
        </div>
        <div class="initials-wrap">
          <input type="text" id="initials-input" maxlength="4" placeholder="J.T." oninput="updateSig()" autocomplete="off" spellcheck="false">
        </div>
        <div class="sig-preview" id="sig-preview">
          <div class="sig-stamp" id="sig-stamp"></div>
          <div class="sig-date-stamp" id="sig-date"></div>
        </div>
        <p class="sig-legal">
          En entrant mes initiales, je confirme que les informations fournies sont exactes et j'accepte qu'elles constituent ma <strong>signature électronique</strong> valide pour ce formulaire d'inscription.
        </p>
      </div>
    </div>
  </div>

  <!-- ══ SECTIONS VERROUILLÉES (formateur) ══ -->
  <div class="section-card locked">
    <div class="section-head locked-head">
      <span class="section-icon">🔒</span>
      <h3>Objets d'évaluation obligatoires</h3>
      <span class="section-badge badge-locked">Formateur</span>
    </div>
    <div class="section-body">
      <div class="locked-notice">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="11" width="18" height="11" rx="2"/><path d="M7 11V7a5 5 0 0 1 10 0v4"/></svg>
        Cette section est réservée au formateur et sera complétée à la réception du formulaire.
      </div>
      <table style="width:100%;border-collapse:collapse;font-size:.82rem;opacity:.5;">
        <thead>
          <tr>
            <th style="background:#E2E8F0;padding:.5rem .75rem;text-align:left;border-radius:6px 0 0 0;">Objet d'évaluation</th>
            <th style="background:#E2E8F0;padding:.5rem .75rem;text-align:center;">Bloc</th>
            <th style="background:#E2E8F0;padding:.5rem .75rem;text-align:center;">Échec</th>
            <th style="background:#E2E8F0;padding:.5rem .75rem;text-align:center;">Abandon</th>
            <th style="background:#E2E8F0;padding:.5rem .75rem;text-align:center;border-radius:0 6px 0 0;">Réussite</th>
          </tr>
        </thead>
        <tbody id="evalPreviewBody"></tbody>
      </table>
    </div>
  </div>

  <div class="section-card locked">
    <div class="section-head locked-head">
      <span class="section-icon">🔒</span>
      <h3>Résultat, présence &amp; formateurs</h3>
      <span class="section-badge badge-locked">Formateur</span>
    </div>
    <div class="section-body">
      <div class="locked-notice">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="11" width="18" height="11" rx="2"/><path d="M7 11V7a5 5 0 0 1 10 0v4"/></svg>
        Résultat global (abandon / échec / réussite), confirmations de présence, noms des formateurs et commentaires — réservés au formateur.
      </div>
      <div class="row cols-2" style="opacity:.4;pointer-events:none;">
        <div class="field"><label>Nom du formateur principal</label><input class="locked-field" type="text" disabled placeholder="Sera complété par le formateur"></div>
        <div class="field"><label>Nom du formateur en RCR</label><input class="locked-field" type="text" disabled placeholder="Sera complété par le formateur"></div>
      </div>
    </div>
  </div>

  <!-- ══ SUBMIT ══ -->
  <div class="submit-card">
    <h3>📨 Soumettre la fiche</h3>
    <div class="email-row">
      <div class="field">
        <label>Adresse courriel de destination <span class="req" style="color:var(--orange);">*</span></label>
        <input type="email" id="dest_email" placeholder="formation@santinel.com" oninput="prog()">
      </div>
    </div>
    <button class="btn btn-primary" id="submitBtn" onclick="generateAndSend()" disabled>
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M22 2L11 13"/><path d="M22 2L15 22 11 13 2 9l20-7z"/></svg>
      Générer le PDF et envoyer
    </button>
    <p class="submit-note">Le PDF est généré localement dans votre navigateur puis votre client courriel s'ouvre. Aucune donnée transmise à un serveur tiers.</p>
  </div>

</div>

<div id="toast"></div>

<script>
const { jsPDF } = window.jspdf;

const evalItems = [
  { label: "Utilisation du matériel contenu dans la trousse", bloc: 1 },
  { label: "Tenue du registre d'accidents, d'incidents et de premiers secours", bloc: 1 },
  { label: "Arrêt cardiorespiratoire (DEA)", bloc: 2 },
  { label: "Obstruction des voies respiratoires", bloc: 2 },
  { label: "Altération de l'état de conscience / Anaphylaxie", bloc: 2 },
  { label: "Application de la séquence d'intervention", bloc: 3 },
  { label: "Séquence d'appréciations – problème médical", bloc: 3 },
  { label: "Utilisation des méthodes de protection", bloc: 4 },
  { label: "Séquence d'appréciation – problème traumatique", bloc: 4 },
  { label: "Hémorragie grave", bloc: 4 },
];

// Build locked preview table
(function() {
  const tbody = document.getElementById('evalPreviewBody');
  evalItems.forEach(item => {
    const tr = document.createElement('tr');
    tr.style.cssText = 'border-bottom:1px solid #EEF2F7;';
    tr.innerHTML = `
      <td style="padding:.45rem .75rem;">${item.label}</td>
      <td style="text-align:center;padding:.45rem;"><span style="background:#CBD5E1;color:#64748B;border-radius:4px;padding:.1rem .4rem;font-size:.72rem;font-weight:700;">${item.bloc}</span></td>
      <td style="text-align:center;">☐</td>
      <td style="text-align:center;">☐</td>
      <td style="text-align:center;">☐</td>`;
    tbody.appendChild(tr);
  });
})();

// ── SIGNATURE ──────────────────────────────────────────────────────────────
function updateSig() {
  const raw = document.getElementById('initials-input').value.trim().toUpperCase();
  const preview = document.getElementById('sig-preview');
  const stamp = document.getElementById('sig-stamp');
  const datestamp = document.getElementById('sig-date');
  if (raw.length >= 1) {
    stamp.textContent = raw;
    datestamp.textContent = 'Signé le ' + new Date().toLocaleDateString('fr-CA', { year:'numeric', month:'long', day:'numeric' });
    preview.classList.add('visible');
  } else {
    preview.classList.remove('visible');
  }
  prog();
}

// ── PROGRESS ───────────────────────────────────────────────────────────────
const requiredFields = ['prenom','nom','titre_cours','date_cours','dest_email'];

function prog() {
  const filledReq = requiredFields.filter(id => document.getElementById(id).value.trim()).length;
  const hasSig = document.getElementById('initials-input').value.trim().length >= 1;
  const total = requiredFields.length + 1;
  const filled = filledReq + (hasSig ? 1 : 0);
  const pct = Math.round(filled / total * 100);
  document.getElementById('pBar').style.width = pct + '%';
  document.getElementById('pPct').textContent = pct + ' %';
  const allReady = filledReq === requiredFields.length && hasSig && document.getElementById('dest_email').value.includes('@');
  document.getElementById('submitBtn').disabled = !allReady;
}

function v(id) { return document.getElementById(id)?.value?.trim() || ''; }

// ── PDF ────────────────────────────────────────────────────────────────────
function generateAndSend() {
  const initials = v('initials-input').toUpperCase();
  const signDate = new Date().toLocaleDateString('fr-CA', { year:'numeric', month:'long', day:'numeric' });

  const doc = new jsPDF({ unit: 'mm', format: 'letter' });
  const PW = 216, M = 15;
  let y = 15;

  const C_NAVY   = [15, 32, 64];
  const C_ORANGE = [224, 90, 30];
  const C_SLATE  = [100, 116, 139];
  const C_LIGHT  = [240, 243, 249];
  const C_BORDER = [220, 227, 238];
  const C_LOCKED = [200, 210, 225];
  const C_WHITE  = [255, 255, 255];

  const IW = PW - M * 2; // inner width
  const H2 = (IW - 6) / 2; // half col

  function sf(style, size, rgb) {
    doc.setFont('helvetica', style);
    doc.setFontSize(size);
    doc.setTextColor(...(rgb || C_NAVY));
  }

  function sectionBar(title, locked) {
    doc.setFillColor(...(locked ? C_LOCKED : C_NAVY));
    doc.rect(M, y, IW, 8, 'F');
    sf('bold', 8, locked ? C_SLATE : C_WHITE);
    doc.text((locked ? '🔒 ' : '') + title.toUpperCase(), M + 3, y + 5.5);
    if (locked) {
      sf('bold', 6.5, C_SLATE);
      doc.text('RÉSERVÉ AU FORMATEUR', PW - M - 3, y + 5.5, { align: 'right' });
    }
    y += 11;
  }

  function fieldPair(lbl1, val1, lbl2, val2) {
    sf('bold', 6, C_SLATE); doc.text(lbl1.toUpperCase(), M, y);
    if (lbl2) { sf('bold', 6, C_SLATE); doc.text(lbl2.toUpperCase(), M + H2 + 6, y); }
    y += 3.5;
    sf('normal', 9, C_NAVY); doc.text(val1 || '—', M, y);
    if (lbl2 !== undefined) { sf('normal', 9, C_NAVY); doc.text(val2 || '—', M + H2 + 6, y); }
    doc.setDrawColor(...C_BORDER); doc.setLineWidth(.3);
    doc.line(M, y + 1.5, M + H2, y + 1.5);
    if (lbl2 !== undefined) doc.line(M + H2 + 6, y + 1.5, M + IW, y + 1.5);
    y += 8;
  }

  function fieldFull(lbl, val) {
    sf('bold', 6, C_SLATE); doc.text(lbl.toUpperCase(), M, y); y += 3.5;
    sf('normal', 9, C_NAVY); doc.text(val || '—', M, y);
    doc.setDrawColor(...C_BORDER); doc.line(M, y + 1.5, M + IW, y + 1.5);
    y += 8;
  }

  // ── LOGO + TITLE ──
  doc.setFillColor(...C_NAVY);
  doc.rect(M, y, 54, 11, 'F');
  sf('bold', 17, C_WHITE); doc.text('SANTINEL', M + 3, y + 8);
  sf('bold', 13, C_ORANGE); doc.text("FICHE D'INSCRIPTION PARTICIPANT(E)", M + 58, y + 5);
  sf('normal', 7.5, C_SLATE); doc.text('Premiers secours – Formulaire participant', M + 58, y + 9.5);
  y += 15;
  doc.setDrawColor(...C_ORANGE); doc.setLineWidth(.7);
  doc.line(M, y, M + IW, y); y += 7;

  // ── COORDONNÉES PERSONNELLES ──
  sectionBar('Coordonnées personnelles');
  fieldPair('Prénom', v('prenom'), 'Nom', v('nom'));
  fieldFull("Adresse du domicile (No civique, rue, ville et code postal)", v('adresse_domicile'));
  fieldPair('Téléphone (domicile)', v('tel_domicile'), 'Courrier électronique', v('courriel_perso'));

  // ── COORDONNÉES TRAVAIL ──
  sectionBar('Coordonnées relatives au travail');
  fieldPair('Métier ou profession', v('metier'), "Nom de l'établissement", v('etablissement'));
  fieldPair("Téléphone (établissement)", v('tel_etab'), "Adresse de l'établissement", v('adresse_etab'));
  fieldPair('Prénom et nom du supérieur', v('superieur'), 'Courrier électronique (supérieur)', v('courriel_sup'));

  // ── RENSEIGNEMENTS ADDITIONNELS ──
  sectionBar('Renseignements additionnels');
  fieldPair('Titre du cours', v('titre_cours'), 'Date', v('date_cours'));

  // ── SIGNATURE ÉLECTRONIQUE ──
  y += 2;
  doc.setFillColor(255, 243, 237);
  doc.setDrawColor(...C_ORANGE); doc.setLineWidth(.5);
  doc.roundedRect(M, y, IW, 28, 3, 3, 'FD');
  sf('bold', 7.5, C_SLATE); doc.text('SIGNATURE ÉLECTRONIQUE DU PARTICIPANT', M + 4, y + 5.5);

  // Initials large display
  sf('bold', 26, C_NAVY);
  doc.text(initials, M + 4, y + 19);
  doc.setDrawColor(...C_ORANGE); doc.setLineWidth(.8);
  doc.line(M + 4, y + 21, M + 4 + doc.getTextWidth(initials) + 2, y + 21);

  // Legal text
  sf('normal', 6.5, C_SLATE);
  const legalLines = doc.splitTextToSize(
    `En soumettant ce formulaire avec mes initiales «\u00A0${initials}\u00A0», je confirme que les informations ci-dessus sont exactes et j'accepte que ces initiales constituent ma signature électronique valide. Signé le : ${signDate}`,
    IW - 45
  );
  doc.text(legalLines, M + 40, y + 10);
  y += 33;

  // ── LOCKED SECTION (page 1) ──
  sectionBar('Résultat global', true);
  doc.setFillColor(...C_LIGHT);
  doc.rect(M, y, IW, 12, 'F');
  doc.setDrawColor(...C_LOCKED); doc.rect(M, y, IW, 12, 'S');
  const resLabels = ['ABANDON', 'ÉCHEC', 'RÉUSSITE'];
  const resW = 38;
  resLabels.forEach((lbl, i) => {
    doc.setFillColor(...C_LOCKED);
    doc.roundedRect(M + 3 + i * (resW + 4), y + 2, resW, 8, 2, 2, 'F');
    sf('bold', 8, C_WHITE);
    doc.text(lbl, M + 3 + i * (resW + 4) + resW / 2, y + 7.2, { align: 'center' });
  });
  y += 17;

  // ── PAGE 2 ──
  doc.addPage(); y = 15;

  // Logo mini
  doc.setFillColor(...C_NAVY);
  doc.rect(M, y, 38, 8, 'F');
  sf('bold', 12, C_WHITE); doc.text('SANTINEL', M + 2, y + 6);
  sf('bold', 11, C_ORANGE); doc.text("OBJETS D'ÉVALUATION OBLIGATOIRES", M + 42, y + 6);
  y += 12;
  doc.setDrawColor(...C_ORANGE); doc.setLineWidth(.5); doc.line(M, y, M + IW, y); y += 7;

  // Eval table header
  const CW = [106, 13, 20, 20, 22];
  const TH = ['Objet d\'évaluation', 'Bloc', 'Échec', 'Abandon', 'Réussite'];
  doc.setFillColor(...C_NAVY);
  doc.rect(M, y, IW, 7.5, 'F');
  let cx = M + 2;
  sf('bold', 7, C_WHITE);
  TH.forEach((h, i) => {
    doc.text(h, cx + (i > 0 ? CW[i]/2 : 0), y + 5, { align: i > 0 ? 'center' : 'left' });
    cx += CW[i];
  });
  y += 7.5;

  evalItems.forEach((item, idx) => {
    const rh = 7.5;
    if (idx % 2 === 0) { doc.setFillColor(...C_LIGHT); doc.rect(M, y, IW, rh, 'F'); }
    doc.setDrawColor(...C_BORDER); doc.setLineWidth(.2);
    doc.rect(M, y, IW, rh, 'S');
    sf('normal', 7, C_NAVY); doc.text(item.label, M + 2, y + 5);
    doc.setFillColor(...C_ORANGE);
    doc.roundedRect(M + CW[0] + 1.5, y + 1.5, 10, 4.5, 1, 1, 'F');
    sf('bold', 6.5, C_WHITE); doc.text(String(item.bloc), M + CW[0] + 6.5, y + 5, { align: 'center' });
    // empty checkboxes
    [0,1,2].forEach(ci => {
      const bx = M + CW[0] + CW[1] + CW.slice(2, 2+ci).reduce((a,b)=>a+b,0) + CW[ci+2]/2;
      doc.setDrawColor(...C_LOCKED); doc.setFillColor(248,250,252);
      doc.rect(bx - 2.5, y + 2, 5, 4, 'FD');
    });
    y += rh;
  });

  y += 8;

  // Presence section (locked)
  sectionBar('Renseignements additionnels – Présence', true);
  const presItems = [
    "Le participant a été présent à l'ensemble de la formation.",
    "Le participant a fait les exercices pratiques.",
    "La participant a réussi les évaluations obligatoires.",
  ];
  presItems.forEach(label => {
    doc.setFillColor(...C_LIGHT);
    doc.roundedRect(M, y, IW, 7, 1.5, 1.5, 'F');
    sf('normal', 7.5, C_NAVY); doc.text(label, M + 3, y + 4.7);
    // NON/OUI boxes
    ['NON','OUI'].forEach((lbl, li) => {
      const bx = M + IW - 26 + li * 14;
      doc.setFillColor(...C_LOCKED);
      doc.roundedRect(bx, y + 1.3, 11, 4.5, 1, 1, 'F');
      sf('bold', 6, C_WHITE); doc.text(lbl, bx + 5.5, y + 4.8, { align: 'center' });
    });
    y += 8.5;
  });

  y += 6;

  // Formateurs
  sectionBar('Formateurs', true);
  fieldPair('Nom du formateur principal', '', 'Nom du formateur en RCR', '');

  // Commentaires
  y += 2;
  sf('bold', 6, C_SLATE); doc.text('COMMENTAIRES', M, y); y += 3;
  doc.setFillColor(...C_LIGHT); doc.setDrawColor(...C_BORDER);
  doc.roundedRect(M, y, IW, 24, 2, 2, 'FD');
  y += 28;

  // Signature formateur placeholder
  sectionBar('Signature du formateur', true);
  doc.setFillColor(...C_LIGHT); doc.setDrawColor(...C_BORDER);
  doc.roundedRect(M, y, IW, 14, 2, 2, 'FD');
  sf('normal', 7, C_SLATE); doc.text('Signature du formateur :', M + 4, y + 5);
  doc.line(M + 4, y + 10.5, M + 70, y + 10.5);
  y += 18;

  // Footer both pages
  [1, 2].forEach(pg => {
    doc.setPage(pg);
    doc.setFillColor(...C_NAVY);
    doc.rect(0, 272, 216, 7, 'F');
    sf('normal', 6, [160, 175, 190]);
    doc.text('1061, ch. du Côteau-Rouge, Longueuil J4K 1W5  ·  tél. 450 679-7801  ·  téléc. 450 670-4504', PW/2, 275.5, { align:'center' });
  });

  // ── EXPORT ──
  const fname = `Santinel_Inscription_${v('nom')}_${v('prenom')}.pdf`.replace(/\s+/g,'_');
  const blob = doc.output('blob');
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url; a.download = fname;
  document.body.appendChild(a); a.click(); document.body.removeChild(a);

  const dest = v('dest_email');
  const subj = encodeURIComponent(`Fiche d'inscription – ${v('prenom')} ${v('nom')}`);
  const body = encodeURIComponent(
    `Bonjour,\n\nVeuillez trouver ci-joint la fiche d'inscription de ${v('prenom')} ${v('nom')} pour le cours : ${v('titre_cours') || 'non spécifié'} (${v('date_cours') || 'date non spécifiée'}).\n\nSigné électroniquement par initiales «\u00A0${v('initials-input').toUpperCase()}\u00A0» le ${new Date().toLocaleDateString('fr-CA')}.\n\nCordialement,\n${v('prenom')} ${v('nom')}`
  );
  setTimeout(() => { window.location.href = `mailto:${dest}?subject=${subj}&body=${body}`; }, 500);

  toast('✓ PDF téléchargé — votre client courriel va s\'ouvrir !');
  URL.revokeObjectURL(url);
}

function toast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 3800);
}

prog();
</script>
</body>
</html>
