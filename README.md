<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>HelpNearby</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:wght@600;700&family=Figtree:wght@400;500;600&display=swap">
<style>
:root {
  --bg: #f2f6f5;
  --surface: #ffffff;
  --ink: #14292b;
  --muted: #5a6e70;
  --line: #d9e3e2;
  --brand: #0e6b68;
  --brand-ink: #ffffff;
  --brand-soft: #dff0ee;
  --star: #c98600;
  --good: #1b7a43;
  --good-soft: #e1f3e8;
  --warn: #a45a00;
  --warn-soft: #fdf0dc;
  --alert: #b3261e;
  --alert-soft: #fdeceb;
  --display: "Bricolage Grotesque", "Figtree", system-ui, sans-serif;
  --body: "Figtree", system-ui, -apple-system, "Segoe UI", sans-serif;
}
* { box-sizing: border-box; }
[hidden] { display: none !important; }
html { scroll-behavior: smooth; }
body { margin: 0; background: var(--bg); color: var(--ink); font: 16px/1.55 var(--body); }
a { color: var(--brand); }
h1, h2, h3 { font-family: var(--display); line-height: 1.2; margin: 0; text-wrap: balance; }
p { margin: 0; }
button, input, select, textarea { font: inherit; color: inherit; }
button { cursor: pointer; }
:focus-visible { outline: 3px solid var(--brand); outline-offset: 2px; }

.topbar { position: sticky; top: 0; z-index: 10; background: var(--surface); border-bottom: 1px solid var(--line); }
.topbar-in { max-width: 1040px; margin: 0 auto; padding: 10px 20px; display: flex; align-items: center; gap: 20px; flex-wrap: wrap; }
.logo { font: 700 20px var(--display); color: var(--brand); text-decoration: none; display: flex; align-items: center; gap: 8px; }
.logo svg { width: 26px; height: 26px; }
nav { display: flex; gap: 4px; overflow-x: auto; flex: 1; min-width: 0; scrollbar-width: none; }
nav::-webkit-scrollbar { display: none; }
nav a { white-space: nowrap; text-decoration: none; color: var(--muted); font-weight: 500; padding: 8px 12px; border-radius: 8px; }
nav a:hover { background: var(--bg); color: var(--ink); }
nav a[aria-current="page"] { color: var(--brand); background: var(--brand-soft); font-weight: 600; }
.who { font-size: 14px; color: var(--muted); }
@media (max-width: 720px) {
  .topbar-in { gap: 6px 12px; padding: 8px 16px; }
  .logo { flex: 1; }
  nav { order: 3; flex: 0 0 100%; margin-inline: -8px; padding-bottom: 2px; }
  main { padding-inline: 16px; }
}

main { max-width: 1040px; margin: 0 auto; padding: 28px 20px 64px; }
.page { display: none; flex-direction: column; gap: 22px; }
.page.on { display: flex; }
.page-head { display: flex; flex-direction: column; gap: 6px; }
.page-head h1 { font-size: clamp(26px, 4vw, 36px); }
.page-head p { color: var(--muted); max-width: 62ch; }

.card { background: var(--surface); border: 1px solid var(--line); border-radius: 14px; padding: 20px; min-width: 0; }
.card h2 { font-size: 19px; }
.card-head { display: flex; justify-content: space-between; align-items: baseline; gap: 12px; margin-bottom: 14px; }
.grid2 { display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 18px; }
.grid3 { display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 18px; }
@media (max-width: 820px) { .grid3 { grid-template-columns: repeat(2, minmax(0, 1fr)); } }
@media (max-width: 620px) { .grid2, .grid3 { grid-template-columns: minmax(0, 1fr); } }

.btn { border: 1.5px solid var(--brand); background: transparent; color: var(--brand); font-weight: 600; padding: 9px 16px; border-radius: 10px; text-decoration: none; display: inline-block; }
.btn:hover { background: var(--brand-soft); }
.btn.solid { background: var(--brand); color: var(--brand-ink); }
.btn.solid:hover { filter: brightness(1.1); }
.btn.small { padding: 6px 12px; font-size: 14px; }
.chips { display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 14px; }
.chip { border: 1.5px solid var(--line); background: var(--surface); border-radius: 99px; padding: 5px 14px; font-weight: 500; font-size: 14px; }
.chip.on { background: var(--brand); border-color: var(--brand); color: var(--brand-ink); }
.row-actions { display: flex; gap: 8px; align-items: center; flex-wrap: wrap; justify-content: flex-end; }
.danger { border-color: var(--alert); color: var(--alert); }
.danger:hover { background: var(--alert-soft); }
.linkbtn { background: none; border: 0; color: var(--brand); font-weight: 600; padding: 0; text-decoration: underline; text-underline-offset: 3px; }

.pill { display: inline-block; padding: 2px 10px; border-radius: 99px; font-size: 13px; font-weight: 600; }
.pill.good { background: var(--good-soft); color: var(--good); }
.pill.warn { background: var(--warn-soft); color: var(--warn); }
.pill.brand { background: var(--brand-soft); color: var(--brand); }
.stars { color: var(--star); font-weight: 600; }
.muted { color: var(--muted); }
.small-text { font-size: 14px; }

/* status banner */
.status { display: flex; gap: 16px; align-items: center; background: var(--brand); color: var(--brand-ink); border-radius: 16px; padding: 22px; flex-wrap: wrap; }
.status h1 { font-size: clamp(22px, 3.4vw, 30px); }
.status p { opacity: .9; }
.status .grow { flex: 1; min-width: 220px; display: flex; flex-direction: column; gap: 4px; }
.status .btn { border-color: #fff; color: #fff; }
.status .btn:hover { background: rgba(255,255,255,.14); }

/* readings */
.readings { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; }
.reading { background: var(--bg); border-radius: 10px; padding: 14px; display: flex; flex-direction: column; gap: 4px; }
.reading b { font: 700 28px var(--display); font-variant-numeric: tabular-nums; }
.reading small { color: var(--muted); }

/* lists */
.list { list-style: none; margin: 0; padding: 0; display: flex; flex-direction: column; }
.list > li { padding: 14px 0; border-top: 1px solid var(--line); display: flex; gap: 14px; align-items: flex-start; justify-content: space-between; min-width: 0; }
.list > li:first-child { border-top: 0; padding-top: 0; }
.list > li:last-child { padding-bottom: 0; }
.list .grow { flex: 1; min-width: 0; }
.list .when { font-size: 13px; color: var(--muted); font-variant-numeric: tabular-nums; white-space: nowrap; }
.timeline > li { position: relative; padding-left: 22px; display: block; }
.timeline > li::before { content: ""; position: absolute; left: 0; top: 20px; width: 10px; height: 10px; border-radius: 50%; background: var(--brand); }
.timeline > li:first-child::before { top: 6px; }

.avatar { width: 52px; height: 52px; border-radius: 50%; display: grid; place-items: center; background: var(--brand-soft); color: var(--brand); font: 700 18px var(--display); flex: none; }
.avatar.lg { width: 64px; height: 64px; font-size: 22px; }

/* medicines */
.med { align-items: center; }
.med input { width: 24px; height: 24px; accent-color: var(--good); flex: none; }
.med.done .name { text-decoration: line-through; color: var(--muted); }
.progress { height: 8px; background: var(--bg); border-radius: 99px; overflow: hidden; margin: 6px 0 14px; }
.progress > i { display: block; height: 100%; background: var(--good); border-radius: 99px; transition: width .25s; }

/* team */
.person { display: flex; flex-direction: column; gap: 14px; }
.person-top { display: flex; gap: 14px; align-items: center; }
.checks { display: flex; flex-wrap: wrap; gap: 6px; }
.tags { display: flex; flex-wrap: wrap; gap: 6px; }
.tag { background: var(--bg); border-radius: 6px; padding: 2px 8px; font-size: 13px; color: var(--muted); }
dl.facts { margin: 0; display: grid; grid-template-columns: auto 1fr; gap: 6px 14px; font-size: 14px; }
dl.facts dt { color: var(--muted); }
dl.facts dd { margin: 0; }

/* care options */
.option { display: flex; flex-direction: column; gap: 10px; transition: border-color .15s, box-shadow .15s; }
.option.match { border-color: var(--brand); box-shadow: 0 0 0 2px var(--brand-soft); }
.option h3 { font-size: 18px; }
.option ul { margin: 0; padding-left: 18px; color: var(--muted); font-size: 15px; }
.option .foot { margin-top: auto; display: flex; justify-content: space-between; align-items: center; gap: 10px; flex-wrap: wrap; padding-top: 6px; }
.needs { display: flex; flex-wrap: wrap; gap: 10px; }
.needs label { display: flex; align-items: center; gap: 8px; border: 1.5px solid var(--line); border-radius: 10px; padding: 8px 12px; cursor: pointer; background: var(--surface); }
.needs label:has(input:checked) { border-color: var(--brand); background: var(--brand-soft); }
.needs input { accent-color: var(--brand); }

/* forms */
form.stack { display: flex; flex-direction: column; gap: 14px; }
.field { display: flex; flex-direction: column; gap: 5px; min-width: 0; }
.field label { font-size: 13px; font-weight: 600; color: var(--muted); }
.field input, .field select, .field textarea { border: 1px solid var(--line); border-radius: 8px; padding: 9px 11px; background: var(--surface); width: 100%; }
.row2 { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; }
@media (max-width: 520px) { .row2 { grid-template-columns: 1fr; } }
.notice { border-radius: 10px; padding: 10px 14px; font-weight: 500; }
.notice.ok { background: var(--good-soft); color: var(--good); }
.notice.err { background: var(--alert-soft); color: var(--alert); }

/* emergency */
.sos { display: flex; justify-content: space-between; align-items: center; gap: 14px; flex-wrap: wrap; background: var(--alert-soft); border: 1px solid #f0b9b5; border-radius: 14px; padding: 16px 20px; }
.sos b { color: var(--alert); }
.sos .btn { border-color: var(--alert); color: var(--alert); }
.sos .btn:hover { background: #fff; }

/* how it works */
.steps { counter-reset: s; display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 18px; list-style: none; margin: 0; padding: 0; }
@media (max-width: 720px) { .steps { grid-template-columns: minmax(0, 1fr); } }
.steps li { counter-increment: s; background: var(--surface); border: 1px solid var(--line); border-radius: 14px; padding: 18px; display: flex; flex-direction: column; gap: 6px; }
.steps li::before { content: counter(s); width: 30px; height: 30px; border-radius: 50%; background: var(--brand); color: #fff; display: grid; place-items: center; font: 700 15px var(--display); }
.steps b { font-family: var(--display); font-size: 17px; }

dialog { border: 1px solid var(--line); border-radius: 16px; padding: 22px; width: min(460px, calc(100vw - 32px)); background: var(--surface); color: var(--ink); }
dialog::backdrop { background: rgba(10, 25, 27, .45); }
footer { max-width: 1040px; margin: 0 auto; padding: 0 20px 40px; color: var(--muted); font-size: 14px; }
</style>
</head>
<body>

<header class="topbar">
  <div class="topbar-in">
    <a class="logo" href="#overview" aria-label="HelpNearby home">
      <svg viewBox="0 0 32 32" aria-hidden="true"><circle cx="16" cy="16" r="15" fill="#0e6b68"/><path d="M16 24s-7-4.4-7-9.6A4.1 4.1 0 0 1 16 12a4.1 4.1 0 0 1 7 2.4C23 19.600 16 24 16 24z" fill="#fff"/></svg>
      HelpNearby
    </a>
    <nav id="nav" aria-label="Sections">
      <a href="#overview">Overview</a>
      <a href="#visits">Visits</a>
      <a href="#updates">Care updates</a>
      <a href="#medicines">Medicines</a>
      <a href="#team">Care team</a>
      <a href="#options">Care options</a>
    </nav>
    <span class="who">Hi Sarbajeet</span>
  </div>
</header>

<main>

<!-- OVERVIEW -->
<section class="page" id="overview" aria-label="Overview">
  <div class="status">
    <div class="grow">
      <h1>Everything is on track</h1>
      <p>Meera Sharma · Care plan active · Next visit today at 6:00 PM</p>
    </div>
    <a class="btn" href="#visits">Schedule a visit</a>
  </div>

  <div class="grid2">
    <div class="card">
      <div class="card-head"><h2>Next visit</h2><a href="#visits" class="small-text">See all</a></div>
      <div id="ov-next"></div>
    </div>
    <div class="card">
      <div class="card-head"><h2>Today's health</h2><span class="pill good">Stable</span></div>
      <div class="readings">
        <div class="reading"><small>Blood pressure</small><b>124/78</b><small>mmHg · normal</small></div>
        <div class="reading"><small>Blood sugar</small><b>102</b><small>mg/dL · normal</small></div>
      </div>
    </div>
  </div>

  <div class="grid2">
    <div class="card">
      <div class="card-head"><h2>Recent care updates</h2><a href="#updates" class="small-text">See all</a></div>
      <ul class="list timeline" id="ov-updates"></ul>
    </div>
    <div class="card">
      <div class="card-head"><h2>Medicine today</h2><a href="#medicines" class="small-text">Manage</a></div>
      <div id="ov-meds"></div>
    </div>
  </div>

  <div class="card">
    <div class="card-head"><h2>Your care team</h2><a href="#team" class="small-text">See all</a></div>
    <ul class="list" id="ov-team"></ul>
  </div>

  <div class="card">
    <div class="card-head"><h2>How HelpNearby works</h2></div>
    <ol class="steps">
      <li><b>We match a verified caregiver</b><span class="muted">Every nurse and companion passes an ID and background check before their first visit.</span></li>
      <li><b>Visits follow a written plan</b><span class="muted">Medicines, readings and routines are agreed with your family and shown here.</span></li>
      <li><b>You see every update</b><span class="muted">Notes, readings and medicine checks appear after each visit so you are never guessing.</span></li>
    </ol>
  </div>

  <div class="sos">
    <span><b>Need urgent help?</b> Call the emergency line any time of day. A care coordinator answers.</span>
    <a class="btn" href="#emergency" id="sos-open">Emergency support</a>
  </div>
</section>

<!-- VISITS -->
<section class="page" id="visits" aria-label="Visits">
  <div class="page-head"><h1>Visits</h1><p>Upcoming and past visits for Meera. Schedule a new one and your care coordinator will confirm it.</p></div>
  <div class="grid2">
    <div class="card">
      <div class="card-head"><h2>Upcoming</h2></div>
      <ul class="list" id="visit-upcoming"></ul>
    </div>
    <div class="card">
      <div class="card-head"><h2>Schedule a visit</h2></div>
      <form class="stack" id="visit-form" novalidate>
        <div class="field"><label for="v-type">Type of visit</label>
          <select id="v-type">
            <option>Nurse health check</option>
            <option>Companion visit</option>
            <option>Medicine support</option>
            <option>Post-hospital recovery check</option>
          </select></div>
        <div class="row2">
          <div class="field"><label for="v-date">Date</label><input type="date" id="v-date"></div>
          <div class="field"><label for="v-time">Start time</label><input type="time" id="v-time" value="10:00"></div>
        </div>
        <div class="row2">
          <div class="field"><label for="v-len">Length</label>
            <select id="v-len"><option value="30">30 minutes</option><option value="60" selected>60 minutes</option><option value="120">2 hours</option><option value="240">4 hours</option></select></div>
          <div class="field"><label for="v-who">Caregiver</label>
            <select id="v-who"><option>Riya Nair</option><option>Sunita Patel</option><option>Any available</option></select></div>
        </div>
        <div class="field"><label for="v-note">Notes for the caregiver (optional)</label><textarea id="v-note" rows="3" placeholder="For example: please check her feet, she mentioned some swelling."></textarea></div>
        <div id="v-msg" role="alert" hidden></div>
        <button class="btn solid" type="submit">Request visit</button>
      </form>
    </div>
  </div>
  <div class="card">
    <div class="card-head"><h2>Past visits</h2></div>
    <ul class="list" id="visit-past"></ul>
  </div>
</section>

<!-- UPDATES -->
<section class="page" id="updates" aria-label="Care updates">
  <div class="page-head"><h1>Care updates</h1><p>Notes from Meera's care team, newest first.</p></div>
  <div class="grid2">
    <div class="card">
      <div class="card-head"><h2>Timeline</h2></div>
      <div class="chips" id="upd-filter" role="group" aria-label="Filter updates">
        <button type="button" class="chip on" data-f="all">All</button>
        <button type="button" class="chip" data-f="Riya Nair">Riya</button>
        <button type="button" class="chip" data-f="Sunita Patel">Sunita</button>
        <button type="button" class="chip" data-f="Family">Family notes</button>
      </div>
      <ul class="list timeline" id="all-updates"></ul>
    </div>
    <div class="card">
      <div class="card-head"><h2>Leave a note for the team</h2></div>
      <form class="stack" id="note-form" novalidate>
        <div class="field"><label for="n-text">Note</label><textarea id="n-text" rows="4" placeholder="For example: she said her knee hurt on the stairs."></textarea></div>
        <div id="n-msg" role="alert" hidden></div>
        <button class="btn solid" type="submit">Add note</button>
      </form>
    </div>
  </div>
</section>

<!-- MEDICINES -->
<section class="page" id="medicines" aria-label="Medicines">
  <div class="page-head"><h1>Medicines</h1><p>Tick each medicine once it has been taken. Your care team sees the same list.</p></div>
  <div class="grid2">
    <div class="card"><div class="card-head"><h2>Today</h2><button type="button" class="linkbtn" id="med-reset">Reset for a new day</button></div><div id="med-today"></div></div>
    <div class="card">
      <div class="card-head"><h2>Add a medicine</h2></div>
      <form class="stack" id="med-form" novalidate>
        <div class="row2">
          <div class="field"><label for="m-name">Name</label><input type="text" id="m-name" placeholder="Calcium"></div>
          <div class="field"><label for="m-dose">Dose</label><input type="text" id="m-dose" placeholder="1 tablet"></div>
        </div>
        <div class="field"><label for="m-time">When</label>
          <select id="m-time"><option>Morning, after breakfast</option><option>Afternoon</option><option>Evening, with dinner</option><option>Bedtime</option></select></div>
        <div id="m-msg" role="alert" hidden></div>
        <button class="btn solid" type="submit">Add medicine</button>
      </form>
    </div>
    <div class="card">
      <div class="card-head"><h2>Prescribed by</h2></div>
      <dl class="facts">
        <dt>Doctor</dt><dd>Dr. A. Banerjee, General Physician</dd>
        <dt>Last review</dt><dd>3 weeks ago</dd>
        <dt>Next review</dt><dd>In 9 days</dd>
        <dt>Allergies</dt><dd>None recorded</dd>
      </dl>
      <p class="muted small-text" style="margin-top:14px">Do not change a
