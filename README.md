<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>أثر - لوحة التحكم</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Tajawal:wght@300;400;500;700;900&display=swap');

  :root {
    --bg: #0f1117;
    --surface: #181c27;
    --surface2: #1e2335;
    --border: #2a3048;
    --gold: #c9a84c;
    --gold-light: #e8c96e;
    --green: #22c55e;
    --red: #ef4444;
    --blue: #3b82f6;
    --purple: #a855f7;
    --teal: #14b8a6;
    --text: #e8eaf0;
    --text-muted: #8892a4;
    --sidebar-w: 240px;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    font-family: 'Tajawal', sans-serif;
    background: var(--bg);
    color: var(--text);
    display: flex;
    min-height: 100vh;
    font-size: 14px;
  }

  .sidebar {
    width: var(--sidebar-w);
    background: var(--surface);
    border-left: 1px solid var(--border);
    display: flex;
    flex-direction: column;
    position: fixed;
    right: 0; top: 0; bottom: 0;
    z-index: 100;
    overflow-y: auto;
  }

  .sidebar-logo {
    padding: 20px 16px;
    border-bottom: 1px solid var(--border);
    text-align: center;
  }

  .sidebar-logo .logo-text {
    font-size: 42px;
    font-weight: 900;
    background: linear-gradient(135deg, var(--gold), var(--gold-light));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    line-height: 1;
  }

  .sidebar-logo .logo-sub {
    font-size: 10px;
    color: var(--text-muted);
    margin-top: 4px;
    letter-spacing: 0.5px;
  }

  .sidebar-nav { flex: 1; padding: 12px 8px; }

  .nav-section-label {
    font-size: 10px;
    color: var(--text-muted);
    padding: 8px 12px 4px;
    font-weight: 700;
    letter-spacing: 0.5px;
    text-transform: uppercase;
  }

  .nav-item {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 10px 12px;
    border-radius: 10px;
    cursor: pointer;
    color: var(--text-muted);
    font-size: 13px;
    font-weight: 500;
    transition: all 0.2s;
    margin-bottom: 2px;
    border: none;
    background: none;
    width: 100%;
    text-align: right;
  }

  .nav-item:hover { background: var(--surface2); color: var(--text); }
  .nav-item.active { background: linear-gradient(135deg, rgba(201,168,76,0.2), rgba(201,168,76,0.05)); color: var(--gold); border: 1px solid rgba(201,168,76,0.3); }
  .nav-item.teal-active { background: linear-gradient(135deg, rgba(20,184,166,0.2), rgba(20,184,166,0.05)); color: var(--teal); border: 1px solid rgba(20,184,166,0.3); }

  .nav-icon { font-size: 16px; width: 20px; text-align: center; }

  .sidebar-footer {
    padding: 12px 8px;
    border-top: 1px solid var(--border);
  }

  .main {
    margin-right: var(--sidebar-w);
    flex: 1;
    display: flex;
    flex-direction: column;
    min-height: 100vh;
  }

  .topbar {
    background: var(--surface);
    border-bottom: 1px solid var(--border);
    padding: 14px 24px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    position: sticky;
    top: 0;
    z-index: 50;
  }

  .topbar-title { font-size: 18px; font-weight: 700; }
  .topbar-sub { font-size: 12px; color: var(--text-muted); margin-top: 2px; }

  .content { padding: 20px 24px; flex: 1; }

  .page { display: none; }
  .page.active { display: block; }

  .stats-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 16px;
    margin-bottom: 20px;
  }

  .stat-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 18px;
    position: relative;
    overflow: hidden;
  }

  .stat-card::before {
    content: '';
    position: absolute;
    top: 0; right: 0;
    width: 60px; height: 60px;
    border-radius: 0 14px 0 60px;
    opacity: 0.1;
  }

  .stat-card.gold::before { background: var(--gold); }
  .stat-card.green::before { background: var(--green); }
  .stat-card.blue::before { background: var(--blue); }
  .stat-card.purple::before { background: var(--purple); }
  .stat-card.teal::before { background: var(--teal); }

  .stat-label { font-size: 12px; color: var(--text-muted); margin-bottom: 8px; }
  .stat-value { font-size: 32px; font-weight: 900; line-height: 1; }
  .stat-card.gold .stat-value { color: var(--gold); }
  .stat-card.green .stat-value { color: var(--green); }
  .stat-card.blue .stat-value { color: var(--blue); }
  .stat-card.purple .stat-value { color: var(--purple); }
  .stat-card.teal .stat-value { color: var(--teal); }
  .stat-sub { font-size: 11px; color: var(--text-muted); margin-top: 6px; }

  .two-col { display: grid; grid-template-columns: 1fr 1.5fr; gap: 16px; margin-bottom: 20px; }

  .card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 18px;
  }

  .card-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 16px;
  }

  .card-title { font-size: 14px; font-weight: 700; }
  .card-badge {
    font-size: 10px;
    padding: 3px 8px;
    border-radius: 20px;
    background: rgba(201,168,76,0.15);
    color: var(--gold);
    border: 1px solid rgba(201,168,76,0.3);
  }

  .card-badge-teal {
    font-size: 10px;
    padding: 3px 8px;
    border-radius: 20px;
    background: rgba(20,184,166,0.15);
    color: var(--teal);
    border: 1px solid rgba(20,184,166,0.3);
  }

  .activity-item {
    display: flex;
    align-items: flex-start;
    gap: 10px;
    padding: 10px 0;
    border-bottom: 1px solid var(--border);
  }

  .activity-item:last-child { border-bottom: none; }

  .activity-icon {
    width: 32px; height: 32px;
    border-radius: 8px;
    display: flex; align-items: center; justify-content: center;
    font-size: 14px;
    flex-shrink: 0;
  }

  .activity-text { font-size: 12px; line-height: 1.5; }
  .activity-time { font-size: 10px; color: var(--text-muted); margin-top: 2px; }

  .bracket-container { overflow-x: auto; padding: 10px 0; }

  .bracket { display: flex; gap: 0; direction: ltr; min-width: 700px; }

  .bracket-round { display: flex; flex-direction: column; justify-content: space-around; flex: 1; }

  .bracket-round-title {
    text-align: center;
    font-size: 11px;
    color: var(--gold);
    font-weight: 700;
    margin-bottom: 10px;
    padding-bottom: 6px;
    border-bottom: 1px solid rgba(201,168,76,0.2);
  }

  .match-wrapper { display: flex; align-items: center; position: relative; flex: 1; justify-content: center; padding: 6px 0; }

  .match-box {
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 8px;
    overflow: hidden;
    width: 140px;
    cursor: pointer;
    transition: all 0.2s;
  }

  .match-box:hover { border-color: var(--gold); transform: scale(1.02); }

  .match-team { display: flex; align-items: center; justify-content: space-between; padding: 6px 10px; font-size: 12px; font-weight: 600; }
  .match-team:first-child { border-bottom: 1px solid var(--border); }
  .match-team.winner { background: rgba(201,168,76,0.1); color: var(--gold); }
  .match-score { font-size: 14px; font-weight: 900; min-width: 20px; text-align: center; }
  .match-btn { display: block; width: 100%; padding: 4px; background: rgba(201,168,76,0.1); border: none; color: var(--gold); font-size: 10px; cursor: pointer; font-family: 'Tajawal', sans-serif; font-weight: 600; }
  .match-btn:hover { background: rgba(201,168,76,0.2); }

  /* Volleyball bracket - teal theme */
  .vb-match-box {
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 8px;
    overflow: hidden;
    width: 140px;
    cursor: pointer;
    transition: all 0.2s;
  }
  .vb-match-box:hover { border-color: var(--teal); transform: scale(1.02); }
  .vb-match-team { display: flex; align-items: center; justify-content: space-between; padding: 6px 10px; font-size: 12px; font-weight: 600; }
  .vb-match-team:first-child { border-bottom: 1px solid var(--border); }
  .vb-match-team.winner { background: rgba(20,184,166,0.1); color: var(--teal); }
  .vb-match-btn { display: block; width: 100%; padding: 4px; background: rgba(20,184,166,0.1); border: none; color: var(--teal); font-size: 10px; cursor: pointer; font-family: 'Tajawal', sans-serif; font-weight: 600; }
  .vb-match-btn:hover { background: rgba(20,184,166,0.2); }
  .bracket-round-title-teal {
    text-align: center; font-size: 11px; color: var(--teal); font-weight: 700;
    margin-bottom: 10px; padding-bottom: 6px; border-bottom: 1px solid rgba(20,184,166,0.2);
  }

  .search-bar { display: flex; gap: 10px; margin-bottom: 16px; align-items: center; }

  .search-input {
    flex: 1;
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 10px 14px;
    color: var(--text);
    font-family: 'Tajawal', sans-serif;
    font-size: 13px;
    outline: none;
    transition: border-color 0.2s;
  }
  .search-input:focus { border-color: var(--gold); }
  .search-input::placeholder { color: var(--text-muted); }

  .btn { padding: 10px 18px; border-radius: 10px; border: none; cursor: pointer; font-family: 'Tajawal', sans-serif; font-size: 13px; font-weight: 700; transition: all 0.2s; }
  .btn-gold { background: var(--gold); color: #000; }
  .btn-gold:hover { background: var(--gold-light); transform: translateY(-1px); }
  .btn-outline { background: transparent; border: 1px solid var(--border); color: var(--text-muted); }
  .btn-outline:hover { border-color: var(--gold); color: var(--gold); }
  .btn-red { background: rgba(239,68,68,0.15); color: var(--red); border: 1px solid rgba(239,68,68,0.3); }
  .btn-teal { background: var(--teal); color: #000; }
  .btn-teal:hover { background: #2dd4bf; transform: translateY(-1px); }
  .btn-outline-teal { background: transparent; border: 1px solid rgba(20,184,166,0.4); color: var(--teal); }
  .btn-outline-teal:hover { border-color: var(--teal); background: rgba(20,184,166,0.1); }

  .table-wrap { overflow-x: auto; }
  table { width: 100%; border-collapse: collapse; font-size: 13px; }
  th { text-align: right; padding: 10px 14px; color: var(--text-muted); font-weight: 600; font-size: 11px; border-bottom: 1px solid var(--border); white-space: nowrap; }
  td { padding: 10px 14px; border-bottom: 1px solid rgba(42,48,72,0.5); vertical-align: middle; }
  tr:hover td { background: rgba(255,255,255,0.02); }
  tr:last-child td { border-bottom: none; }

  .badge { padding: 3px 8px; border-radius: 20px; font-size: 10px; font-weight: 700; }
  .badge-green { background: rgba(34,197,94,0.15); color: var(--green); }
  .badge-gold { background: rgba(201,168,76,0.15); color: var(--gold); }
  .badge-blue { background: rgba(59,130,246,0.15); color: var(--blue); }
  .badge-red { background: rgba(239,68,68,0.15); color: var(--red); }
  .badge-teal { background: rgba(20,184,166,0.15); color: var(--teal); }

  /* Teams grid */
  .teams-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(180px, 1fr)); gap: 12px; margin-top: 16px; }

  .team-card {
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 16px 12px;
    text-align: center;
    cursor: pointer;
    transition: all 0.2s;
    position: relative;
  }
  .team-card:hover { border-color: var(--gold); transform: translateY(-2px); }
  .team-card.vb-team:hover { border-color: var(--teal); }

  .team-number { font-size: 28px; font-weight: 900; color: var(--gold); line-height: 1; }
  .team-number.teal { color: var(--teal); }
  .team-name { font-size: 13px; font-weight: 700; margin-top: 4px; }
  .team-members-list { font-size: 11px; color: var(--text-muted); margin-top: 8px; line-height: 1.6; }
  .team-wins { position: absolute; top: 8px; left: 8px; font-size: 10px; background: rgba(34,197,94,0.15); color: var(--green); padding: 2px 6px; border-radius: 10px; }

  /* Modal */
  .modal-overlay { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.7); z-index: 1000; align-items: center; justify-content: center; }
  .modal-overlay.open { display: flex; }
  .modal { background: var(--surface); border: 1px solid var(--border); border-radius: 16px; padding: 24px; width: 480px; max-width: 90vw; max-height: 85vh; overflow-y: auto; }
  .modal-title { font-size: 16px; font-weight: 700; margin-bottom: 16px; color: var(--gold); }
  .modal-title-teal { font-size: 16px; font-weight: 700; margin-bottom: 16px; color: var(--teal); }

  .form-group { margin-bottom: 14px; }
  .form-label { font-size: 12px; color: var(--text-muted); margin-bottom: 6px; display: block; }
  .form-input { width: 100%; background: var(--surface2); border: 1px solid var(--border); border-radius: 8px; padding: 10px 12px; color: var(--text); font-family: 'Tajawal', sans-serif; font-size: 13px; outline: none; }
  .form-input:focus { border-color: var(--gold); }
  .modal-actions { display: flex; gap: 10px; margin-top: 20px; justify-content: flex-end; }

  .live-dot { width: 8px; height: 8px; background: var(--green); border-radius: 50%; animation: pulse 1.5s infinite; display: inline-block; margin-left: 6px; }
  @keyframes pulse { 0%, 100% { opacity: 1; transform: scale(1); } 50% { opacity: 0.5; transform: scale(0.8); } }

  .champion-banner {
    background: linear-gradient(135deg, rgba(201,168,76,0.15), rgba(201,168,76,0.05));
    border: 1px solid rgba(201,168,76,0.4);
    border-radius: 14px;
    padding: 20px;
    text-align: center;
    margin-bottom: 20px;
    position: relative;
    overflow: hidden;
  }
  .champion-banner.teal {
    background: linear-gradient(135deg, rgba(20,184,166,0.15), rgba(20,184,166,0.05));
    border: 1px solid rgba(20,184,166,0.4);
  }
  .champion-label { font-size: 12px; color: var(--gold); margin-bottom: 6px; }
  .champion-label.teal { color: var(--teal); }
  .champion-name { font-size: 24px; font-weight: 900; color: var(--gold-light); }
  .champion-name.teal { color: #2dd4bf; }

  .pagination { display: flex; gap: 6px; justify-content: center; margin-top: 16px; align-items: center; }
  .page-btn { width: 32px; height: 32px; border-radius: 8px; border: 1px solid var(--border); background: var(--surface2); color: var(--text-muted); cursor: pointer; font-family: 'Tajawal', sans-serif; font-size: 12px; display: flex; align-items: center; justify-content: center; transition: all 0.2s; }
  .page-btn:hover, .page-btn.active { border-color: var(--gold); color: var(--gold); }
  .page-info { font-size: 12px; color: var(--text-muted); }

  .toast { position: fixed; bottom: 24px; left: 24px; background: var(--surface); border: 1px solid var(--green); border-radius: 10px; padding: 12px 18px; font-size: 13px; color: var(--green); z-index: 9999; transform: translateY(100px); transition: transform 0.3s ease; direction: rtl; }
  .toast.show { transform: translateY(0); }

  .about-section { margin-bottom: 24px; }
  .about-section h3 { font-size: 16px; font-weight: 700; color: var(--gold); margin-bottom: 12px; }
  .about-list { list-style: none; }
  .about-list li { padding: 8px 0; border-bottom: 1px solid var(--border); font-size: 13px; display: flex; align-items: flex-start; gap: 8px; }
  .about-list li::before { content: '◆'; color: var(--gold); font-size: 8px; margin-top: 4px; flex-shrink: 0; }

  .meetings-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 16px; margin-top: 12px; }
  .meeting-card { background: var(--surface2); border: 1px solid var(--border); border-radius: 12px; padding: 16px; border-right: 3px solid var(--gold); }
  .meeting-num { font-size: 11px; color: var(--gold); margin-bottom: 6px; }
  .meeting-title { font-size: 15px; font-weight: 700; margin-bottom: 4px; }
  .meeting-sub { font-size: 12px; color: var(--text-muted); }

  .budget-table { width: 100%; border-collapse: collapse; margin-top: 12px; }
  .budget-table th, .budget-table td { padding: 10px 14px; text-align: right; border-bottom: 1px solid var(--border); font-size: 13px; }
  .budget-table th { color: var(--text-muted); font-size: 11px; }
  .budget-table tr:last-child td { font-weight: 700; color: var(--gold); border-top: 2px solid var(--gold); border-bottom: none; }

  .standings-table { width: 100%; border-collapse: collapse; font-size: 13px; margin-top: 12px; }
  .standings-table th { padding: 8px 12px; text-align: right; color: var(--text-muted); font-size: 11px; border-bottom: 1px solid var(--border); }
  .standings-table td { padding: 8px 12px; border-bottom: 1px solid rgba(42,48,72,0.4); }
  .standings-table tr:first-child td { color: var(--gold); font-weight: 700; }
  .pos-num { font-weight: 900; color: var(--gold); }

  .score-input { width: 50px; background: var(--surface); border: 1px solid var(--gold); border-radius: 6px; padding: 4px 8px; color: var(--gold); font-family: 'Tajawal', sans-serif; font-size: 16px; font-weight: 900; text-align: center; outline: none; }
  .score-input.teal { border-color: var(--teal); color: var(--teal); }

  /* Player list in team card */
  .player-tag { display: inline-block; background: var(--surface); border: 1px solid var(--border); border-radius: 6px; padding: 2px 8px; font-size: 11px; margin: 2px; }

  /* Islamic reminders */
  .islam-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 16px; }
  .islam-card {
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 20px;
    border-top: 3px solid;
    transition: transform 0.2s;
    cursor: default;
  }
  .islam-card:hover { transform: translateY(-2px); }
  .islam-card.prayer { border-top-color: #f59e0b; }
  .islam-card.halakat { border-top-color: #a855f7; }
  .islam-card.parents { border-top-color: #22c55e; }
  .islam-card.sins { border-top-color: #ef4444; }

  .islam-icon { font-size: 32px; margin-bottom: 12px; }
  .islam-title { font-size: 15px; font-weight: 700; margin-bottom: 10px; }
  .islam-card.prayer .islam-title { color: #f59e0b; }
  .islam-card.halakat .islam-title { color: #a855f7; }
  .islam-card.parents .islam-title { color: #22c55e; }
  .islam-card.sins .islam-title { color: #ef4444; }

  .islam-ayah { font-size: 15px; line-height: 1.8; color: var(--gold-light); font-weight: 600; margin-bottom: 10px; padding: 12px; background: rgba(201,168,76,0.05); border-radius: 8px; border-right: 3px solid rgba(201,168,76,0.3); }
  .islam-hadith { font-size: 13px; line-height: 1.7; color: var(--text); margin-bottom: 8px; padding: 10px; background: rgba(255,255,255,0.03); border-radius: 8px; }
  .islam-source { font-size: 11px; color: var(--text-muted); font-style: italic; }
  .islam-advice { font-size: 13px; line-height: 1.7; color: var(--text-muted); margin-top: 8px; }

  .tab-bar { display: flex; gap: 8px; margin-bottom: 16px; }
  .tab-btn { padding: 8px 18px; border-radius: 8px; border: 1px solid var(--border); background: var(--surface2); color: var(--text-muted); cursor: pointer; font-family: 'Tajawal', sans-serif; font-size: 13px; font-weight: 600; transition: all 0.2s; }
  .tab-btn.active-gold { background: rgba(201,168,76,0.15); color: var(--gold); border-color: rgba(201,168,76,0.4); }
  .tab-btn.active-teal { background: rgba(20,184,166,0.15); color: var(--teal); border-color: rgba(20,184,166,0.4); }
  .tab-btn:hover { color: var(--text); border-color: var(--text-muted); }

  .vb-players-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(160px, 1fr)); gap: 10px; margin-top: 12px; }
  .vb-player-card { background: var(--surface2); border: 1px solid var(--border); border-radius: 10px; padding: 12px; display: flex; align-items: center; gap: 10px; }
  .vb-player-num { width: 30px; height: 30px; border-radius: 8px; background: rgba(20,184,166,0.15); color: var(--teal); font-weight: 900; font-size: 14px; display: flex; align-items: center; justify-content: center; flex-shrink: 0; }
  .vb-player-name { font-size: 13px; font-weight: 600; }
  .vb-player-team { font-size: 10px; color: var(--text-muted); margin-top: 2px; }

  select.form-input { appearance: none; }

  .player-checkbox-list { max-height: 300px; overflow-y: auto; border: 1px solid var(--border); border-radius: 8px; padding: 8px; }
  .player-checkbox-item { display: flex; align-items: center; gap: 8px; padding: 6px 8px; border-radius: 6px; cursor: pointer; font-size: 13px; }
  .player-checkbox-item:hover { background: var(--surface2); }
  .player-checkbox-item input { width: 16px; height: 16px; cursor: pointer; accent-color: var(--teal); }

  .vb-team-full { border-color: rgba(239,68,68,0.4) !important; }
  .vb-team-ready { border-color: rgba(34,197,94,0.4) !important; }
</style>
<style>
  .login-overlay {
    position: fixed;
    inset: 0;
    background: var(--bg);
    z-index: 9999;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .login-box {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 20px;
    padding: 40px 36px;
    width: 360px;
    max-width: 90vw;
    text-align: center;
    box-shadow: 0 20px 60px rgba(0,0,0,0.5);
  }
  .login-logo {
    font-size: 64px;
    font-weight: 900;
    background: linear-gradient(135deg, var(--gold), var(--gold-light));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    line-height: 1;
    margin-bottom: 6px;
  }
  .login-sub {
    font-size: 12px;
    color: var(--text-muted);
    margin-bottom: 32px;
    letter-spacing: 0.5px;
  }
  .login-field {
    width: 100%;
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 12px 14px;
    color: var(--text);
    font-family: 'Tajawal', sans-serif;
    font-size: 14px;
    outline: none;
    margin-bottom: 12px;
    transition: border-color 0.2s;
    text-align: right;
  }
  .login-field:focus { border-color: var(--gold); }
  .login-field::placeholder { color: var(--text-muted); }
  .login-btn {
    width: 100%;
    padding: 13px;
    background: linear-gradient(135deg, var(--gold), var(--gold-light));
    color: #000;
    border: none;
    border-radius: 10px;
    font-family: 'Tajawal', sans-serif;
    font-size: 15px;
    font-weight: 700;
    cursor: pointer;
    margin-top: 4px;
    transition: opacity 0.2s, transform 0.1s;
  }
  .login-btn:hover { opacity: 0.9; transform: translateY(-1px); }
  .login-btn:active { transform: translateY(0); }
  .login-error {
    color: var(--red);
    font-size: 12px;
    margin-top: 10px;
    min-height: 18px;
    display: none;
  }
  .login-error.show { display: block; }
  .login-footer {
    margin-top: 24px;
    font-size: 11px;
    color: var(--text-muted);
  }
  .show-pass-btn {
    background: none;
    border: none;
    color: var(--text-muted);
    cursor: pointer;
    font-size: 12px;
    margin-top: -4px;
    margin-bottom: 8px;
    font-family: 'Tajawal', sans-serif;
    display: block;
    width: 100%;
    text-align: left;
    padding: 0 4px;
  }
  .show-pass-btn:hover { color: var(--gold); }
</style>
</head>
<body>

<!-- LOGIN OVERLAY -->
<div class="login-overlay" id="login-overlay">
  <div class="login-box">
    <div class="login-logo">أثر</div>
    <div class="login-sub">لقاءات تصنع الانتماء</div>

    <input class="login-field" type="text" id="login-user" placeholder="اسم المستخدم" autocomplete="username">
    <input class="login-field" type="password" id="login-pass" placeholder="كلمة المرور" autocomplete="current-password"
      onkeydown="if(event.key==='Enter') doLogin()">
    <button class="show-pass-btn" onclick="toggleLoginPass()">👁️ إظهار كلمة المرور</button>

    <button class="login-btn" onclick="doLogin()">دخول</button>
    <div class="login-error" id="login-error">❌ اسم المستخدم أو كلمة المرور غير صحيحة</div>

    <div style="margin-top:20px;display:grid;grid-template-columns:1fr 1fr;gap:8px;text-align:right;">
      <div style="background:rgba(201,168,76,0.07);border:1px solid rgba(201,168,76,0.2);border-radius:8px;padding:8px 10px;">
        <div style="font-size:11px;color:var(--gold);font-weight:700;margin-bottom:2px;">👑 مدير النظام</div>
        <div style="font-size:10px;color:var(--text-muted);">صلاحيات كاملة</div>
      </div>
      <div style="background:rgba(59,130,246,0.07);border:1px solid rgba(59,130,246,0.2);border-radius:8px;padding:8px 10px;">
        <div style="font-size:11px;color:var(--blue);font-weight:700;margin-bottom:2px;">👁️ مشاهد</div>
        <div style="font-size:10px;color:var(--text-muted);">عرض فقط</div>
      </div>
    </div>

    <div class="login-footer">© 2026 سياف المقبلي • برنامج أثر</div>
  </div>
</div>

<aside class="sidebar">
  <div class="sidebar-logo">
    <div class="logo-text">أثر</div>
    <div class="logo-sub">لقاءات تصنع الانتماء</div>
  </div>
  <nav class="sidebar-nav">
    <div class="nav-section-label">عام</div>
    <button class="nav-item active" onclick="showPage('dashboard')">
      <span class="nav-icon">🏠</span> لوحة التحكم
    </button>
    <button class="nav-item" onclick="showPage('about')">
      <span class="nav-icon">ℹ️</span> عن البرنامج
    </button>
    <button class="nav-item" onclick="showPage('participants')">
      <span class="nav-icon">👥</span> المشاركون
    </button>
    <button class="nav-item" onclick="showPage('meetings')">
      <span class="nav-icon">📅</span> الفعاليات
    </button>
    <button class="nav-item" onclick="showPage('mic')">
      <span class="nav-icon">🎤</span> الميكروفون الحر
    </button>
    <button class="nav-item" onclick="showPage('religion')">
      <span class="nav-icon">🕌</span> الدين
    </button>
    <button class="nav-item" onclick="showPage('familytree')">
      <span class="nav-icon">🌳</span> شجرة النسب
    </button>
    <button class="nav-item" onclick="showPage('achievements')">
      <span class="nav-icon">🏅</span> الإنجازات
    </button>

    <div class="nav-section-label" style="margin-top:8px;">🂠 البلوت</div>
    <button class="nav-item" onclick="showPage('teams')">
      <span class="nav-icon">🎯</span> الفرق
    </button>
    <button class="nav-item" onclick="showPage('draw')">
      <span class="nav-icon">🎲</span> القرعة
    </button>
    <button class="nav-item" onclick="showPage('tournament')">
      <span class="nav-icon">🏆</span> البطولة
    </button>

    <div class="nav-section-label" style="margin-top:8px;">🏐 الطائرة</div>
    <button class="nav-item" onclick="showPage('vb-players')">
      <span class="nav-icon">👤</span> لاعبو الطائرة
    </button>
    <button class="nav-item" onclick="showPage('vb-teams')">
      <span class="nav-icon">🛡️</span> فرق الطائرة
    </button>
    <button class="nav-item" onclick="showPage('vb-tournament')">
      <span class="nav-icon">🏅</span> بطولة الطائرة
    </button>

    <div class="nav-section-label" style="margin-top:8px;"></div>
    <button class="nav-item" onclick="showPage('settings')">
      <span class="nav-icon">⚙️</span> الإعدادات
    </button>
  </nav>
  <div class="sidebar-footer">
    <div style="font-size:11px;color:var(--text-muted);text-align:center;">© 2026 سياف المقبلي • برنامج أثر</div>
    <div style="font-size:10px;color:var(--gold-light);text-align:center;margin-top:6px;font-weight:700;line-height:1.7;">
      ✦ تصميم وبرمجة بالكامل ✦<br>
      <span style="font-size:12px;color:var(--gold);">سياف فهد اليزيدي</span><br>
      <span style="font-size:9px;color:var(--text-muted);font-weight:400;">بكل حب وعناية لأجل عائلتنا 💛🌳</span>
    </div>
  </div>
</aside>

<main class="main">
  <header class="topbar">
    <div>
      <div class="topbar-title" id="page-title">لوحة التحكم</div>
      <div class="topbar-sub" id="page-sub">البطولة جارية الآن</div>
    </div>
    <div style="display:flex;gap:10px;align-items:center;">
      <span class="live-dot"></span>
      <span style="font-size:12px;color:var(--green);">مباشر</span>
    </div>
  </header>

  <div class="content">

    <!-- DASHBOARD -->
    <div id="page-dashboard" class="page active">
      <div class="stats-grid">
        <div class="stat-card gold">
          <div class="stat-label">إجمالي المشاركين</div>
          <div class="stat-value" id="stat-total">94</div>
          <div class="stat-sub">مشارك ومشاركة</div>
        </div>
        <div class="stat-card green">
          <div class="stat-label">فرق البلوت</div>
          <div class="stat-value" id="stat-teams">0</div>
          <div class="stat-sub">فريق بلوت</div>
        </div>
        <div class="stat-card teal">
          <div class="stat-label">فرق الطائرة</div>
          <div class="stat-value" id="stat-vb-teams">0</div>
          <div class="stat-sub">فريق طائرة (6 لاعبين)</div>
        </div>
        <div class="stat-card purple">
          <div class="stat-label">لاعبو الطائرة</div>
          <div class="stat-value" id="stat-vb-players">0</div>
          <div class="stat-sub">لاعب مسجل</div>
        </div>
      </div>

      <div class="two-col">
        <div class="card">
          <div class="card-header">
            <span class="card-title">📡 النشاط المباشر</span>
            <span class="card-badge">مباشر</span>
          </div>
          <div id="activity-feed">
            <div class="activity-item">
              <div class="activity-icon" style="background:rgba(34,197,94,0.15)">🏆</div>
              <div>
                <div class="activity-text">فاز الفريق 3 على الفريق 14 في البلوت</div>
                <div class="activity-time">منذ 2 دقيقة</div>
              </div>
            </div>
            <div class="activity-item">
              <div class="activity-icon" style="background:rgba(20,184,166,0.15)">🏐</div>
              <div>
                <div class="activity-text">تم إضافة لاعبين جدد لبطولة الطائرة</div>
                <div class="activity-time">منذ 5 دقيقة</div>
              </div>
            </div>
            <div class="activity-item">
              <div class="activity-icon" style="background:rgba(201,168,76,0.15)">📅</div>
              <div>
                <div class="activity-text">تم تحديث جدول مباريات الطائرة</div>
                <div class="activity-time">منذ 15 دقيقة</div>
              </div>
            </div>
            <div class="activity-item">
              <div class="activity-icon" style="background:rgba(168,85,247,0.15)">➕</div>
              <div>
                <div class="activity-text">تم إضافة 5 مشاركين جدد</div>
                <div class="activity-time">منذ 20 دقيقة</div>
              </div>
            </div>
          </div>
          <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-top:12px;">
            <button class="btn btn-gold" onclick="showPage('tournament')">🏆 بلوت</button>
            <button class="btn btn-teal" onclick="showPage('vb-tournament')">🏐 طائرة</button>
          </div>
        </div>

        <div class="card">
          <div class="card-header"><span class="card-title">📋 نظرة سريعة على البرنامج</span></div>
          <div style="display:grid;grid-template-columns:repeat(2,1fr);gap:10px;">
            <div style="text-align:center;padding:12px;background:var(--surface2);border-radius:10px;">
              <div style="font-size:22px;font-weight:900;color:var(--gold);">4</div>
              <div style="font-size:11px;color:var(--text-muted);">لقاءات سنوية</div>
            </div>
            <div style="text-align:center;padding:12px;background:var(--surface2);border-radius:10px;">
              <div style="font-size:22px;font-weight:900;color:var(--blue);">6-8</div>
              <div style="font-size:11px;color:var(--text-muted);">ساعات لكل لقاء</div>
            </div>
            <div style="text-align:center;padding:12px;background:var(--surface2);border-radius:10px;">
              <div style="font-size:22px;font-weight:900;color:var(--teal);">2</div>
              <div style="font-size:11px;color:var(--text-muted);">فعاليات رياضية</div>
            </div>
            <div style="text-align:center;padding:12px;background:var(--surface2);border-radius:10px;">
              <div style="font-size:22px;font-weight:900;color:var(--green);">15-35</div>
              <div style="font-size:11px;color:var(--text-muted);">الفئة العمرية</div>
            </div>
          </div>
          <div style="margin-top:12px;padding:14px;background:linear-gradient(135deg,rgba(20,184,166,0.1),rgba(20,184,166,0.03));border:1px solid rgba(20,184,166,0.2);border-radius:10px;">
            <div style="font-size:12px;color:var(--teal);font-weight:700;margin-bottom:4px;">🏐 فعالية الكرة الطائرة</div>
            <div style="font-size:12px;color:var(--text-muted);">كل فريق مكون من 6 لاعبين • مباريات تصفوية</div>
          </div>
        </div>
      </div>
    </div>

    <!-- ABOUT -->
    <div id="page-about" class="page">
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:20px;">
        <div>
          <div class="card" style="margin-bottom:16px;">
            <div class="about-section">
              <h3>🎯 أهداف البرنامج</h3>
              <ul class="about-list">
                <li>تعزيز العلاقات الأخوية بين الشباب</li>
                <li>تقوية الهوية والانتماء الأسري والاجتماعي</li>
                <li>غرس القيم التربوية بطريقة غير مباشرة</li>
                <li>ربط الشباب بالقدوات الإيجابية</li>
                <li>رفع الدافعية والطموح الشخصي والمهني</li>
                <li>صناعة بيئة آمنة وجاذبة ومستدامة للشباب</li>
              </ul>
            </div>
          </div>
          <div class="card">
            <div class="about-section">
              <h3>💰 الميزانية التقديرية السنوية</h3>
              <table class="budget-table">
                <thead><tr><th>البند</th><th>التكلفة (ريال)</th></tr></thead>
                <tbody>
                  <tr><td>استئجار مواقع اللقاءات (4×700)</td><td>2,800</td></tr>
                  <tr><td>الضيافة والوجبات (4×5000)</td><td>20,000</td></tr>
                  <tr><td>الجوائز والهدايا (4×250)</td><td>1,000</td></tr>
                  <tr><td>مطبوعات وتصاميم ودروع</td><td>1,200</td></tr>
                  <tr><td>احتياطي طوارئ</td><td>5,000</td></tr>
                  <tr><td>الإجمالي</td><td>30,000</td></tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
        <div>
          <div class="card" style="margin-bottom:16px;">
            <div class="about-section">
              <h3>📅 اللقاءات الأربعة</h3>
              <div class="meetings-grid">
                <div class="meeting-card">
                  <div class="meeting-num">اللقاء الأول • الربع الأول</div>
                  <div class="meeting-title">"من نحن؟"</div>
                  <div class="meeting-sub">لقاء افتتاحي تفاعلي يهدف لكسر الجليد وبناء الألفة بين المشاركين</div>
                </div>
                <div class="meeting-card">
                  <div class="meeting-num">اللقاء الثاني • الربع الثاني</div>
                  <div class="meeting-title">"جذورنا"</div>
                  <div class="meeting-sub">لقاء ثقافي تفاعلي يعزز الانتماء من خلال التعرف على شجرة النسب</div>
                </div>
                <div class="meeting-card">
                  <div class="meeting-num">اللقاء الثالث • الربع الثالث</div>
                  <div class="meeting-title">"أثر القدوة"</div>
                  <div class="meeting-sub">استضافة شخصية مؤثرة قريبة من اهتمامات الشباب للحديث عن تجارب الحياة</div>
                </div>
                <div class="meeting-card">
                  <div class="meeting-num">اللقاء الرابع • الربع الرابع</div>
                  <div class="meeting-title">"رحلتي"</div>
                  <div class="meeting-sub">قصة نجاح ملهمة من ظروف بسيطة حتى النجاح مع التركيز على التحديات</div>
                </div>
              </div>
            </div>
          </div>
          <div class="card">
            <div class="about-section">
              <h3>✅ عوامل نجاح البرنامج</h3>
              <ul class="about-list">
                <li>وجود الدعم المعنوي والمادي</li>
                <li>التنوع وعدم تكرار الأسلوب</li>
                <li>التركيز على التفاعل لا التلقين</li>
                <li>جودة التنظيم والاستقبال</li>
                <li>اختيار شخصيات مؤثرة قريبة من الشباب</li>
                <li>وجود تغطية إعلامية وتحفيز مستمر</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- PARTICIPANTS -->
    <div id="page-participants" class="page">
      <div class="search-bar">
        <input class="search-input" type="text" placeholder="🔍 ابحث بالاسم أو رقم الجوال..." id="search-input" oninput="filterParticipants()">
        <select class="form-input" style="width:140px;" id="age-filter" onchange="filterParticipants()">
          <option value="">جميع الأعمار</option>
          <option value="15-20">15-20 سنة</option>
          <option value="21-25">21-25 سنة</option>
          <option value="26-30">26-30 سنة</option>
          <option value="31-35">31-35 سنة</option>
          <option value="36+">36+ سنة</option>
        </select>
        <button class="btn btn-gold" onclick="openAddModal()">➕ إضافة مشارك</button>
      </div>
      <div class="card">
        <div class="card-header">
          <span class="card-title">👥 قائمة المشاركين</span>
          <span class="card-badge" id="participants-count">94 مشارك</span>
        </div>
        <div class="table-wrap">
          <table>
            <thead>
              <tr><th>#</th><th>الاسم</th><th>العمر</th><th>رقم الجوال</th><th>الحالة</th><th>فريق البلوت</th><th>فريق الطائرة</th><th>إجراءات</th></tr>
            </thead>
            <tbody id="participants-tbody"></tbody>
          </table>
        </div>
        <div class="pagination" id="pagination"></div>
      </div>
    </div>

    <!-- BALOOT TEAMS -->
    <div id="page-teams" class="page">
      <div class="card" style="margin-bottom:16px;">
        <div class="card-header"><span class="card-title">🂠 إدارة لاعبي ومزاوجة البلوت</span></div>
        <div style="padding:12px;background:rgba(201,168,76,0.05);border:1px solid rgba(201,168,76,0.2);border-radius:10px;font-size:12px;color:var(--gold);margin-bottom:14px;">
          💡 كل مباراة بلوت = 4 لاعبين • فريقان كل فريق شخصان • اللعب زوجي ضد زوجي
        </div>
        <div style="display:flex;gap:12px;flex-wrap:wrap;">
          <button class="btn btn-gold" onclick="openAddBalootPlayerModal()">👤 إضافة لاعب</button>
          <button class="btn btn-outline" onclick="autoGenerateBalootTeams()">🎲 توزيع عشوائي (ثنائيات)</button>
          <button class="btn btn-outline" onclick="openManualTeamModal()">✋ إنشاء فريق يدوي</button>
          <button class="btn btn-red" style="margin-right:auto;" onclick="resetBalootTeams()">🗑️ مسح الفرق</button>
        </div>
      </div>

      <div style="display:grid;grid-template-columns:1fr 1fr;gap:16px;">
        <div class="card">
          <div class="card-header">
            <span class="card-title">👤 لاعبو البلوت</span>
            <span class="card-badge" id="baloot-players-count">0 لاعب</span>
          </div>
          <div id="baloot-players-list" style="max-height:400px;overflow-y:auto;">
            <div style="color:var(--text-muted);font-size:13px;text-align:center;padding:20px;">لا يوجد لاعبون بعد.</div>
          </div>
        </div>

        <div class="card">
          <div class="card-header">
            <span class="card-title">🂠 الفرق (ثنائيات)</span>
            <span class="card-badge" id="teams-count-badge">0 فريق</span>
          </div>
          <div class="teams-grid" id="teams-grid" style="grid-template-columns:repeat(auto-fill,minmax(140px,1fr));">
            <div style="color:var(--text-muted);font-size:13px;text-align:center;padding:20px;grid-column:1/-1;">لا توجد فرق بعد.<br>أضف لاعبين ثم وزّع عشوائياً.</div>
          </div>
        </div>
      </div>
    </div>

    <!-- BALOOT DRAW -->
    <div id="page-draw" class="page">
      <div class="card" style="margin-bottom:16px;">
        <div class="card-header"><span class="card-title">🎲 قرعة بطولة البلوت</span></div>
        <p style="font-size:13px;color:var(--text-muted);margin-bottom:16px;">سيتم توزيع الفرق عشوائياً على شجرة البطولة.</p>
        <div style="display:flex;gap:12px;flex-wrap:wrap;">
          <button class="btn btn-gold" onclick="runDraw()">🎲 إنشاء القرعة</button>
          <button class="btn btn-outline" onclick="showPage('tournament')">🏆 عرض شجرة البطولة</button>
        </div>
      </div>
      <div id="draw-result-container">
        <div style="color:var(--text-muted);font-size:13px;text-align:center;padding:30px;">لم يتم إجراء القرعة بعد.</div>
      </div>
    </div>

    <!-- BALOOT TOURNAMENT -->
    <div id="page-tournament" class="page">
      <div style="margin-bottom:16px;display:flex;gap:10px;align-items:center;flex-wrap:wrap;">
        <button class="btn btn-gold" onclick="generateBracket()">🏆 إنشاء شجرة البطولة</button>
        <button class="btn btn-outline" onclick="showStandings()">📊 الترتيب</button>
      </div>
      <div id="champion-display"></div>
      <div class="card">
        <div class="card-header">
          <span class="card-title">🏆 شجرة بطولة البلوت</span>
          <span class="card-badge" id="current-round-label">بانتظار القرعة</span>
        </div>
        <div class="bracket-container">
          <div id="bracket-display">
            <p style="color:var(--text-muted);font-size:13px;text-align:center;padding:30px;">أضف الفرق ثم اضغط إنشاء القرعة.</p>
          </div>
        </div>
      </div>
      <div id="standings-container" style="margin-top:16px;display:none;"></div>
    </div>

    <!-- VOLLEYBALL PLAYERS -->
    <div id="page-vb-players" class="page">
      <div class="card" style="margin-bottom:16px;">
        <div class="card-header">
          <span class="card-title">🏐 لاعبو الكرة الطائرة</span>
          <span class="card-badge-teal" id="vb-players-count-badge">0 لاعب</span>
        </div>
        <div style="display:flex;gap:12px;flex-wrap:wrap;margin-bottom:16px;">
          <button class="btn btn-teal" onclick="openAddVbPlayerModal()">👤 إضافة لاعب</button>
          <button class="btn btn-outline-teal" onclick="showPage('vb-teams')">🛡️ إدارة الفرق</button>
        </div>
        <div class="vb-players-grid" id="vb-players-grid">
          <div style="color:var(--text-muted);font-size:13px;text-align:center;padding:30px;grid-column:1/-1;">لا يوجد لاعبون بعد. أضف لاعبين لبدء بطولة الطائرة.</div>
        </div>
      </div>
    </div>

    <!-- VOLLEYBALL TEAMS -->
    <div id="page-vb-teams" class="page">
      <div class="card" style="margin-bottom:16px;">
        <div class="card-header">
          <span class="card-title">🛡️ فرق الكرة الطائرة</span>
          <span class="card-badge-teal">كل فريق = 6 لاعبين</span>
        </div>
        <div style="display:flex;gap:12px;flex-wrap:wrap;">
          <button class="btn btn-teal" onclick="openAddVbTeamModal()">➕ إنشاء فريق</button>
          <button class="btn btn-outline-teal" onclick="showPage('vb-tournament')">🏅 بطولة الطائرة</button>
        </div>
        <div style="margin-top:12px;padding:12px;background:rgba(20,184,166,0.05);border:1px solid rgba(20,184,166,0.2);border-radius:10px;font-size:12px;color:var(--teal);">
          💡 كل مباراة طائرة تكون بين فريقين (12 لاعب إجمالاً على الملعب) • الفريق المكون من 6 لاعبين
        </div>
      </div>
      <div class="card">
        <div class="card-header">
          <span class="card-title">الفرق المسجلة</span>
          <span class="card-badge-teal" id="vb-teams-count-badge">0 فريق</span>
        </div>
        <div class="teams-grid" id="vb-teams-grid">
          <div style="color:var(--text-muted);font-size:13px;text-align:center;padding:30px;grid-column:1/-1;">لا توجد فرق بعد. أنشئ فريقاً وأضف له 6 لاعبين.</div>
        </div>
      </div>
    </div>

    <!-- VOLLEYBALL TOURNAMENT -->
    <div id="page-vb-tournament" class="page">
      <div style="margin-bottom:16px;display:flex;gap:10px;align-items:center;flex-wrap:wrap;">
        <button class="btn btn-teal" onclick="generateVbBracket()">🏅 إنشاء شجرة الطائرة</button>
        <button class="btn btn-outline-teal" onclick="showVbStandings()">📊 الترتيب</button>
      </div>
      <div id="vb-champion-display"></div>
      <div class="card">
        <div class="card-header">
          <span class="card-title">🏐 شجرة بطولة الطائرة</span>
          <span class="card-badge-teal" id="vb-round-label">بانتظار الفرق</span>
        </div>
        <div class="bracket-container">
          <div id="vb-bracket-display">
            <p style="color:var(--text-muted);font-size:13px;text-align:center;padding:30px;">أضف لاعبين وكوّن الفرق أولاً.</p>
          </div>
        </div>
      </div>
      <div id="vb-standings-container" style="margin-top:16px;display:none;"></div>
    </div>

    <!-- MIC PAGE -->
    <div id="page-mic" class="page">

      <!-- Big stage display -->
      <div id="mic-stage" style="background:linear-gradient(135deg,#1a1040,#0f1117);border:1px solid rgba(168,85,247,0.3);border-radius:20px;padding:40px 24px;text-align:center;margin-bottom:20px;position:relative;overflow:hidden;min-height:260px;display:flex;flex-direction:column;align-items:center;justify-content:center;">
        <div style="position:absolute;inset:0;background:radial-gradient(circle at 50% 0%,rgba(168,85,247,0.12),transparent 70%);pointer-events:none;"></div>
        <div id="mic-icon-display" style="font-size:56px;margin-bottom:12px;transition:all 0.4s;">🎤</div>
        <div id="mic-current-name" style="font-size:36px;font-weight:900;color:#e8eaf0;margin-bottom:8px;transition:all 0.3s;">اضغط "اسحب اسماً"</div>
        <div id="mic-current-sub" style="font-size:14px;color:var(--text-muted);">سيظهر هنا اسم المشارك الذي سيتحدث</div>
        <div id="mic-timer-display" style="font-size:48px;font-weight:900;color:var(--purple);margin-top:16px;display:none;font-variant-numeric:tabular-nums;">0:30</div>
      </div>

      <!-- Controls -->
      <div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:12px;margin-bottom:20px;">
        <button class="btn" style="background:var(--purple);color:#fff;font-size:16px;padding:16px;" onclick="drawMicName()">🎲 اسحب اسماً</button>
        <button class="btn" style="background:var(--green);color:#000;font-size:16px;padding:16px;" id="mic-timer-btn" onclick="toggleMicTimer()">⏱️ ابدأ العداد</button>
        <button class="btn btn-outline" style="font-size:14px;padding:16px;" onclick="resetMicSession()">🔄 إعادة تعيين</button>
      </div>

      <!-- Timer settings -->
      <div class="card" style="margin-bottom:16px;">
        <div class="card-header"><span class="card-title">⚙️ إعدادات الجلسة</span></div>
        <div style="display:flex;gap:16px;align-items:center;flex-wrap:wrap;">
          <div>
            <label style="font-size:12px;color:var(--text-muted);display:block;margin-bottom:4px;">مدة الكلام (ثانية)</label>
            <select id="mic-duration" class="form-input" style="width:120px;">
              <option value="30">30 ثانية</option>
              <option value="45">45 ثانية</option>
              <option value="60" selected>دقيقة</option>
              <option value="90">90 ثانية</option>
              <option value="120">دقيقتان</option>
            </select>
          </div>
          <div>
            <label style="font-size:12px;color:var(--text-muted);display:block;margin-bottom:4px;">موضوع الجلسة</label>
            <select id="mic-topic" class="form-input" style="width:200px;" onchange="updateMicTopic()">
              <option value="حر">🎤 حر — أي شيء</option>
              <option value="ذكرى">💭 أجمل ذكرى في حياتك</option>
              <option value="نصيحة">💡 نصيحة تتمنى لو سمعتها مبكراً</option>
              <option value="طرفة">😄 طرفة أو موقف محرج</option>
              <option value="قدوة">⭐ من هو قدوتك ولماذا؟</option>
              <option value="حلم">🚀 ما حلمك في الحياة؟</option>
              <option value="شكر">❤️ اشكر شخصاً أثّر فيك</option>
            </select>
          </div>
          <div style="margin-top:18px;">
            <span id="mic-topic-display" style="font-size:13px;color:var(--purple);font-weight:700;"></span>
          </div>
        </div>
      </div>

      <div style="display:grid;grid-template-columns:1fr 1fr;gap:16px;">

        <!-- Queue / remaining -->
        <div class="card">
          <div class="card-header">
            <span class="card-title">📋 قائمة الانتظار</span>
            <span class="card-badge" style="background:rgba(168,85,247,0.15);color:var(--purple);border-color:rgba(168,85,247,0.3);" id="mic-remaining-count">94 متبقي</span>
          </div>
          <div style="max-height:320px;overflow-y:auto;" id="mic-queue-list"></div>
        </div>

        <!-- Spoke already -->
        <div class="card">
          <div class="card-header">
            <span class="card-title">✅ تحدّثوا</span>
            <span class="card-badge badge-green" id="mic-done-count">0</span>
          </div>
          <div style="max-height:320px;overflow-y:auto;" id="mic-done-list">
            <div style="color:var(--text-muted);font-size:12px;text-align:center;padding:20px;">لم يتحدث أحد بعد</div>
          </div>
        </div>

      </div>
    </div>

    <!-- MEETINGS -->
    <div id="page-meetings" class="page">
      <div class="meetings-grid" style="grid-template-columns:repeat(2,1fr);">
        <div class="meeting-card">
          <div class="meeting-num">اللقاء الأول • شهر 1 / 1448</div>
          <div class="meeting-title">من نحن؟</div>
          <div class="meeting-sub">جلسة تعارف تفاعلية • 6 ساعات</div>
          <div style="margin-top:12px;font-size:12px;color:var(--text-muted);">📍 استراحة شبابية</div>
          <div style="margin-top:8px;font-size:12px;color:var(--teal);">🏐 فعالية الطائرة + 🂠 البلوت</div>
          <span class="badge badge-green" style="margin-top:8px;display:inline-block;">قادم</span>
        </div>
        <div class="meeting-card">
          <div class="meeting-num">اللقاء الثاني • شهر 4 / 1448</div>
          <div class="meeting-title">جذورنا</div>
          <div class="meeting-sub">شجرة النسب والتاريخ العائلي • 6 ساعات</div>
          <div style="margin-top:12px;font-size:12px;color:var(--text-muted);">📍 مجلس تراثي</div>
          <span class="badge badge-blue" style="margin-top:8px;display:inline-block;">مخطط</span>
        </div>
        <div class="meeting-card">
          <div class="meeting-num">اللقاء الثالث • شهر 7 / 1448</div>
          <div class="meeting-title">أثر القدوة</div>
          <div class="meeting-sub">استضافة شخصية مؤثرة • 6 ساعات</div>
          <div style="margin-top:12px;font-size:12px;color:var(--text-muted);">📍 قاعة فندقية</div>
          <span class="badge badge-blue" style="margin-top:8px;display:inline-block;">مخطط</span>
        </div>
        <div class="meeting-card">
          <div class="meeting-num">اللقاء الرابع • شهر 10 / 1448</div>
          <div class="meeting-title">رحلتي</div>
          <div class="meeting-sub">قصة نجاح ملهمة • 6 ساعات</div>
          <div style="margin-top:12px;font-size:12px;color:var(--text-muted);">📍 مخيم شبابي</div>
          <span class="badge badge-blue" style="margin-top:8px;display:inline-block;">مخطط</span>
        </div>
      </div>
    </div>

    <!-- RELIGION PAGE -->
    <div id="page-religion" class="page">
      <div style="margin-bottom:20px;padding:20px;background:linear-gradient(135deg,rgba(201,168,76,0.1),rgba(201,168,76,0.03));border:1px solid rgba(201,168,76,0.3);border-radius:14px;text-align:center;">
        <div style="font-size:28px;margin-bottom:8px;">🕌</div>
        <div style="font-size:18px;font-weight:700;color:var(--gold);">نصائح وتوجيهات دينية</div>
        <div style="font-size:13px;color:var(--text-muted);margin-top:4px;">تذكير بالثوابت والقيم الإسلامية للشباب</div>
      </div>

      <div class="islam-grid">

        <!-- PRAYER -->
        <div class="islam-card prayer">
          <div class="islam-icon">🕐</div>
          <div class="islam-title">الصلاة</div>
          <div class="islam-ayah">
            ﴿ إِنَّ الصَّلَاةَ كَانَتْ عَلَى الْمُؤْمِنِينَ كِتَابًا مَّوْقُوتًا ﴾
            <div style="font-size:11px;color:var(--text-muted);margin-top:4px;">سورة النساء: 103</div>
          </div>
          <div class="islam-hadith">
            قال النبي ﷺ: «أوَّلُ ما يُحاسَبُ به العبدُ يومَ القيامةِ من عملِه صلاتُه، فإن صلُحَت فقد أفلحَ وأنجحَ، وإن فسدَت فقد خابَ وخسِرَ»
            <div class="islam-source">رواه الترمذي</div>
          </div>
          <div class="islam-advice">
            ✦ حافظ على الصلوات الخمس في أوقاتها<br>
            ✦ الصلاة في الجماعة أفضل من صلاة الفرد بسبع وعشرين درجة<br>
            ✦ لا تؤجل الصلاة لأي سبب كان، فهي عمود الدين<br>
            ✦ صلِّ قبل أن يُصلَّى عليك
          </div>
        </div>

        <!-- SINS / HALAKAT -->
        <div class="islam-card sins">
          <div class="islam-icon">⚠️</div>
          <div class="islam-title">المهلكات والمحرمات</div>
          <div class="islam-ayah">
            ﴿ وَلَا تَقْرَبُوا الزِّنَا إِنَّهُ كَانَ فَاحِشَةً وَسَاءَ سَبِيلًا ﴾
            <div style="font-size:11px;color:var(--text-muted);margin-top:4px;">سورة الإسراء: 32</div>
          </div>
          <div class="islam-hadith">
            قال النبي ﷺ: «اجتَنِبوا السبعَ المُوبِقاتِ: الشِّركُ بالله، والسِّحرُ، وقتلُ النَّفسِ، وأكلُ الرِّبا، وأكلُ مالِ اليتيمِ، والتَّولِّي يومَ الزَّحفِ، وقذفُ المُحصَناتِ الغافلاتِ المُؤمِناتِ»
            <div class="islam-source">متفق عليه</div>
          </div>
          <div class="islam-advice">
            ✦ ابتعد عن الخمر والمخدرات فهي أم الخبائث<br>
            ✦ احذر الإدمان على الشاشات والألعاب حتى لا تضيع الصلاة<br>
            ✦ احفظ لسانك من الغيبة والنميمة والكذب<br>
            ✦ الحلال بيّن والحرام بيّن، فدع ما يريبك
          </div>
        </div>

        <!-- PARENTS -->
        <div class="islam-card parents">
          <div class="islam-icon">❤️</div>
          <div class="islam-title">بر الوالدين</div>
          <div class="islam-ayah">
            ﴿ وَقَضَىٰ رَبُّكَ أَلَّا تَعْبُدُوا إِلَّا إِيَّاهُ وَبِالْوَالِدَيْنِ إِحْسَانًا ﴾
            <div style="font-size:11px;color:var(--text-muted);margin-top:4px;">سورة الإسراء: 23</div>
          </div>
          <div class="islam-hadith">
            جاء رجل إلى النبي ﷺ فقال: يا رسول الله، مَن أحقُّ الناسِ بحُسن صحابتي؟ قال: «أُمُّكَ» قال: ثم مَن؟ قال: «أُمُّكَ» قال: ثم مَن؟ قال: «أُمُّكَ» قال: ثم مَن؟ قال: «أبوكَ»
            <div class="islam-source">متفق عليه</div>
          </div>
          <div class="islam-advice">
            ✦ لا تقل لهما أفٍّ ولا تنهرهما ولو كنت مشغولاً<br>
            ✦ اتصل بوالديك يومياً وتفقّد أحوالهما<br>
            ✦ الجنة تحت أقدام الأمهات — لا تضيّع هذا الكنز<br>
            ✦ رضا الله من رضا الوالدين، وسخطه من سخطهما
          </div>
        </div>

        <!-- GENERAL REMINDERS -->
        <div class="islam-card halakat">
          <div class="islam-icon">📿</div>
          <div class="islam-title">توجيهات للشباب</div>
          <div class="islam-ayah">
            ﴿ يَا أَيُّهَا الَّذِينَ آمَنُوا اتَّقُوا اللَّهَ وَكُونُوا مَعَ الصَّادِقِينَ ﴾
            <div style="font-size:11px;color:var(--text-muted);margin-top:4px;">سورة التوبة: 119</div>
          </div>
          <div class="islam-hadith">
            قال النبي ﷺ: «سبعةٌ يُظِلُّهم اللهُ في ظِلِّه يومَ لا ظِلَّ إلا ظِلُّه... وشابٌّ نشأَ في عبادةِ ربِّه»
            <div class="islam-source">متفق عليه</div>
          </div>
          <div class="islam-advice">
            ✦ الشباب مرحلة النشاط والبناء — استثمرها قبل الهرم<br>
            ✦ اغتنم خمساً قبل خمس: شبابك قبل هرمك<br>
            ✦ اختر الأصحاب الصالحين فالمرء على دين خليله<br>
            ✦ الوقت أغلى من المال — لا تقضه في اللهو المفرط<br>
            ✦ اجعل لك وِرداً يومياً من القرآن ولو آيات
          </div>
        </div>

      </div>

      <!-- Daily Reminder -->
      <div style="margin-top:20px;padding:20px;background:linear-gradient(135deg,rgba(201,168,76,0.08),rgba(168,85,247,0.05));border:1px solid rgba(201,168,76,0.2);border-radius:14px;">
        <div style="font-size:14px;font-weight:700;color:var(--gold);margin-bottom:12px;">📌 تذكير يومي</div>
        <div id="daily-reminder" style="font-size:15px;line-height:1.8;color:var(--text);"></div>
        <button class="btn btn-outline" style="margin-top:14px;font-size:12px;padding:7px 14px;" onclick="rotateDailyReminder()">🔄 تذكير آخر</button>
      </div>
    </div>

    <!-- FAMILY TREE -->
    <div id="page-familytree" class="page">
      <div style="background:linear-gradient(135deg,rgba(34,197,94,0.1),rgba(201,168,76,0.05));border:1px solid rgba(34,197,94,0.25);border-radius:20px;padding:36px 24px;text-align:center;margin-bottom:20px;position:relative;overflow:hidden;">
        <div style="font-size:56px;margin-bottom:14px;">🌳</div>
        <div style="font-size:22px;font-weight:900;color:var(--green);margin-bottom:8px;">شجرة نسب آل مقبل</div>
        <div style="font-size:13px;color:var(--text-muted);max-width:480px;margin:0 auto 22px;line-height:1.8;">
          تعرّف على أصولك وجذورك العائلية، وتتبع فروع العائلة جيلاً بعد جيل من خلال الشجرة التفاعلية الكاملة.
        </div>
        <a href="https://livefamilytrees.com/trees/?t=2501139gL6" target="_blank" rel="noopener noreferrer" class="btn" style="background:var(--green);color:#000;font-size:15px;padding:14px 32px;display:inline-block;text-decoration:none;">
          🌳 فتح شجرة النسب الكاملة
        </a>
        <div style="font-size:11px;color:var(--text-muted);margin-top:12px;">سيتم الفتح في نافذة جديدة • livefamilytrees.com</div>
        <div style="font-size:11px;color:var(--text-muted);margin-top:6px;">إن لم يفتح الزر تلقائياً، انسخ الرابط:<br>
          <a href="https://livefamilytrees.com/trees/?t=2501139gL6" target="_blank" style="color:var(--green);word-break:break-all;">https://livefamilytrees.com/trees/?t=2501139gL6</a>
        </div>
      </div>

      <div class="card">
        <div class="card-header"><span class="card-title">ℹ️ عن شجرة النسب</span></div>
        <ul class="about-list">
          <li>الشجرة توثّق أنساب وفروع عائلة آل مقبل اليزيدي عبر الأجيال</li>
          <li>تساعد الأجيال الجديدة على معرفة أصولهم وأقاربهم</li>
          <li>تُحدَّث باستمرار بإضافة المواليد والفروع الجديدة</li>
          <li>جزء من رسالة برنامج "أثر" في تعزيز الهوية والانتماء الأسري</li>
        </ul>
      </div>

      <!-- MEETING PROGRAM (LINEUP) -->
      <div class="card" style="margin-top:20px;">
        <div class="card-header">
          <span class="card-title">📋 برنامج اللقاء الأول • "من نحن؟"</span>
          <span class="card-badge">فقرات اللقاء</span>
        </div>
        <div style="display:flex;flex-direction:column;gap:0;">

          <div style="display:flex;gap:14px;padding:14px 4px;border-bottom:1px solid var(--border);align-items:flex-start;">
            <div style="width:36px;height:36px;border-radius:10px;background:rgba(34,197,94,0.15);color:var(--green);font-weight:900;font-size:16px;display:flex;align-items:center;justify-content:center;flex-shrink:0;">1</div>
            <div style="flex:1;">
              <div style="font-size:14px;font-weight:700;">🕌 كلمة افتتاحية</div>
              <div style="font-size:12px;color:var(--text-muted);margin-top:3px;">الدكتور الشيخ <strong style="color:var(--green);">صالح</strong> — كلمة توجيهية وبركة لافتتاح اللقاء</div>
              <button class="btn" style="margin-top:8px;font-size:11px;padding:6px 14px;background:var(--green);color:#000;" onclick="startSpeakerMode('الدكتور الشيخ صالح','كلمة توجيهية افتتاحية','green',true)">🎙️ بدء كلمة الشيخ (وضع المسرح)</button>
            </div>
          </div>

          <div style="display:flex;gap:14px;padding:14px 4px;border-bottom:1px solid var(--border);align-items:flex-start;">
            <div style="width:36px;height:36px;border-radius:10px;background:rgba(59,130,246,0.15);color:var(--blue);font-weight:900;font-size:16px;display:flex;align-items:center;justify-content:center;flex-shrink:0;">2</div>
            <div style="flex:1;">
              <div style="font-size:14px;font-weight:700;">🎯 التعريف باللقاء وأهدافه</div>
              <div style="font-size:12px;color:var(--text-muted);margin-top:3px;">الأستاذ <strong style="color:var(--blue);">طارق سعد</strong> يتحدث عن أهداف اللقاء الأول ورسالة برنامج "أثر" وما يُنتظر من المشاركين</div>
              <button class="btn btn-outline" style="margin-top:8px;font-size:11px;padding:6px 14px;" onclick="startSpeakerMode('طارق سعد','أهداف اللقاء ورسالة برنامج أثر','blue')">🎤 بدء فقرة التحدث</button>
            </div>
          </div>

          <div style="display:flex;gap:14px;padding:14px 4px;border-bottom:1px solid var(--border);align-items:flex-start;">
            <div style="width:36px;height:36px;border-radius:10px;background:rgba(201,168,76,0.15);color:var(--gold);font-weight:900;font-size:16px;display:flex;align-items:center;justify-content:center;flex-shrink:0;">3</div>
            <div style="flex:1;">
              <div style="font-size:14px;font-weight:700;">🂠 بطولة البلوت</div>
              <div style="font-size:12px;color:var(--text-muted);margin-top:3px;">ثنائيات تنافسية حتى التتويج بالبطل</div>
              <button class="btn btn-outline" style="margin-top:8px;font-size:11px;padding:6px 14px;" onclick="showPage('tournament')">🏆 الذهاب للبطولة</button>
            </div>
          </div>

          <div style="display:flex;gap:14px;padding:14px 4px;border-bottom:1px solid var(--border);align-items:flex-start;">
            <div style="width:36px;height:36px;border-radius:10px;background:rgba(34,197,94,0.15);color:var(--green);font-weight:900;font-size:16px;display:flex;align-items:center;justify-content:center;flex-shrink:0;">4</div>
            <div style="flex:1;">
              <div style="font-size:14px;font-weight:700;">🌳 شجرة النسب</div>
              <div style="font-size:12px;color:var(--text-muted);margin-top:3px;">جولة على شجرة نسب آل مقبل وفروع العائلة</div>
              <button class="btn btn-outline" style="margin-top:8px;font-size:11px;padding:6px 14px;" onclick="showPage('familytree')">🌳 الذهاب للشجرة</button>
            </div>
          </div>

          <div style="display:flex;gap:14px;padding:14px 4px;border-bottom:1px solid var(--border);align-items:flex-start;">
            <div style="width:36px;height:36px;border-radius:10px;background:rgba(20,184,166,0.15);color:var(--teal);font-weight:900;font-size:16px;display:flex;align-items:center;justify-content:center;flex-shrink:0;">5</div>
            <div style="flex:1;">
              <div style="font-size:14px;font-weight:700;">🏐 بطولة الكرة الطائرة</div>
              <div style="font-size:12px;color:var(--text-muted);margin-top:3px;">فرق سداسية تتنافس على اللقب</div>
              <button class="btn btn-outline" style="margin-top:8px;font-size:11px;padding:6px 14px;" onclick="showPage('vb-tournament')">🏐 الذهاب للبطولة</button>
            </div>
          </div>

          <div style="display:flex;gap:14px;padding:14px 4px;align-items:flex-start;">
            <div style="width:36px;height:36px;border-radius:10px;background:rgba(168,85,247,0.15);color:var(--purple);font-weight:900;font-size:16px;display:flex;align-items:center;justify-content:center;flex-shrink:0;">6</div>
            <div style="flex:1;">
              <div style="font-size:14px;font-weight:700;">🎤 الميكروفون الحر</div>
              <div style="font-size:12px;color:var(--text-muted);margin-top:3px;">كل مشارك يتحدث عن نفسه أو موضوع مطروح</div>
              <button class="btn btn-outline" style="margin-top:8px;font-size:11px;padding:6px 14px;" onclick="showPage('mic')">🎤 الذهاب للفقرة</button>
            </div>
          </div>

        </div>
      </div>
    </div>

    <!-- ACHIEVEMENTS -->
    <div id="page-achievements" class="page">
      <div style="background:linear-gradient(135deg,rgba(201,168,76,0.1),rgba(20,184,166,0.05));border:1px solid rgba(201,168,76,0.25);border-radius:20px;padding:30px 24px;text-align:center;margin-bottom:20px;">
        <div style="font-size:48px;margin-bottom:10px;">🏅</div>
        <div style="font-size:20px;font-weight:900;color:var(--gold);margin-bottom:6px;">شارات الإنجاز</div>
        <div style="font-size:13px;color:var(--text-muted);">تُمنح تلقائياً عند فوز فريق ببطولة البلوت أو الطائرة</div>
      </div>
      <div class="card">
        <div class="card-header">
          <span class="card-title">🎖️ سجل الأبطال</span>
        </div>
        <div id="achievements-list">
          <div style="color:var(--text-muted);font-size:13px;text-align:center;padding:20px;">لا توجد إنجازات بعد — ستظهر هنا تلقائياً عند فوز فريق بالبطولة.</div>
        </div>
      </div>
    </div>

    <!-- SETTINGS -->
    <div id="page-settings" class="page">
      <div class="card">
        <div class="card-header">
          <span class="card-title">⚙️ إعدادات البرنامج</span>
          <span id="settings-viewer-badge" style="display:none;" class="badge badge-blue">👁️ عرض فقط</span>
        </div>
        <div id="settings-admin-view">
          <div class="form-group">
            <label class="form-label">اسم البرنامج</label>
            <input class="form-input" id="setting-program-name" value="أثر - لقاءات تصنع الانتماء">
          </div>
          <div class="form-group">
            <label class="form-label">المشرف العام</label>
            <input class="form-input" id="setting-supervisor" value="سياف المقبلي">
          </div>
          <div class="form-group">
            <label class="form-label">الفئة العمرية المستهدفة</label>
            <input class="form-input" id="setting-age" value="15 - 35 سنة">
          </div>
          <div class="form-group">
            <label class="form-label">الحد الأدنى للمشاركين</label>
            <input class="form-input" type="number" id="setting-min" value="60">
          </div>
          <button class="btn btn-gold" onclick="showToast('✅ تم حفظ الإعدادات بنجاح')">💾 حفظ الإعدادات</button>
        </div>
        <div id="settings-viewer-view" style="display:none;">
          <div style="display:grid;gap:12px;">
            <div style="padding:14px;background:var(--surface2);border-radius:10px;display:flex;justify-content:space-between;align-items:center;">
              <span style="font-size:12px;color:var(--text-muted);">اسم البرنامج</span>
              <span style="font-size:13px;font-weight:700;">أثر - لقاءات تصنع الانتماء</span>
            </div>
            <div style="padding:14px;background:var(--surface2);border-radius:10px;display:flex;justify-content:space-between;align-items:center;">
              <span style="font-size:12px;color:var(--text-muted);">المشرف العام</span>
              <span style="font-size:13px;font-weight:700;">سياف المقبلي</span>
            </div>
            <div style="padding:14px;background:var(--surface2);border-radius:10px;display:flex;justify-content:space-between;align-items:center;">
              <span style="font-size:12px;color:var(--text-muted);">الفئة العمرية المستهدفة</span>
              <span style="font-size:13px;font-weight:700;">15 - 35 سنة</span>
            </div>
            <div style="padding:14px;background:var(--surface2);border-radius:10px;display:flex;justify-content:space-between;align-items:center;">
              <span style="font-size:12px;color:var(--text-muted);">الحد الأدنى للمشاركين</span>
              <span style="font-size:13px;font-weight:700;">60 مشارك</span>
            </div>
          </div>
          <div style="margin-top:16px;padding:12px;background:rgba(59,130,246,0.05);border:1px solid rgba(59,130,246,0.2);border-radius:10px;font-size:12px;color:var(--blue);text-align:center;">
            👁️ أنت في وضع المشاهدة — لا يمكن تعديل الإعدادات
          </div>
        </div>
      </div>
    </div>

  </div>
</main>

<!-- ADD BALOOT PLAYER MODAL -->
<div class="modal-overlay" id="add-baloot-player-modal">
  <div class="modal">
    <div class="modal-title">🂠 إضافة لاعب بلوت</div>
    <div class="form-group">
      <label class="form-label">اختر من قائمة المشاركين</label>
      <input class="form-input" id="baloot-player-search" placeholder="🔍 ابحث بالاسم..." oninput="filterBalootPlayerSearch()" style="margin-bottom:8px;">
      <div class="player-checkbox-list" id="baloot-player-search-list" style="max-height:280px;"></div>
    </div>
    <div class="modal-actions">
      <button class="btn btn-outline" onclick="closeModal('add-baloot-player-modal')">إلغاء</button>
      <button class="btn btn-gold" onclick="addSelectedBalootPlayers()">➕ إضافة المحددين</button>
    </div>
  </div>
</div>

<!-- MANUAL BALOOT TEAM MODAL -->
<div class="modal-overlay" id="manual-team-modal">
  <div class="modal">
    <div class="modal-title">✋ إنشاء فريق ثنائي يدوي</div>
    <div class="form-group">
      <label class="form-label">اسم الفريق (اختياري)</label>
      <input class="form-input" id="manual-team-name" placeholder="مثال: الصقور، النسور...">
    </div>
    <div class="form-group">
      <label class="form-label">اختر لاعبين اثنين بالضبط</label>
      <div class="player-checkbox-list" id="manual-team-player-list" style="max-height:300px;"></div>
    </div>
    <div id="manual-team-counter" style="font-size:12px;color:var(--text-muted);margin-top:6px;">تم اختيار 0 من 2</div>
    <div class="modal-actions">
      <button class="btn btn-outline" onclick="closeModal('manual-team-modal')">إلغاء</button>
      <button class="btn btn-gold" onclick="saveManualTeam()">✅ إنشاء الفريق</button>
    </div>
  </div>
</div>

<!-- ADD PARTICIPANT MODAL -->
<div class="modal-overlay" id="add-modal">
  <div class="modal">
    <div class="modal-title">➕ إضافة مشارك جديد</div>
    <div class="form-group">
      <label class="form-label">الاسم الكامل *</label>
      <input class="form-input" id="new-name" placeholder="أدخل الاسم">
    </div>
    <div class="form-group">
      <label class="form-label">العمر *</label>
      <input class="form-input" type="number" id="new-age" placeholder="العمر" min="10" max="60">
    </div>
    <div class="form-group">
      <label class="form-label">رقم الجوال</label>
      <input class="form-input" id="new-phone" placeholder="05XXXXXXXX">
    </div>
    <div class="modal-actions">
      <button class="btn btn-outline" onclick="closeModal('add-modal')">إلغاء</button>
      <button class="btn btn-gold" onclick="addParticipant()">إضافة</button>
    </div>
  </div>
</div>

<!-- BALOOT SCORE MODAL -->
<div class="modal-overlay" id="score-modal">
  <div class="modal">
    <div class="modal-title" id="score-modal-title">تسجيل نتيجة مباراة البلوت</div>
    <div style="display:flex;align-items:center;justify-content:center;gap:16px;margin:20px 0;">
      <div style="text-align:center;">
        <div id="team-a-name" style="font-weight:700;margin-bottom:8px;"></div>
        <input class="score-input" id="score-a" type="number" min="0" value="0">
      </div>
      <div style="color:var(--text-muted);font-weight:700;font-size:18px;">VS</div>
      <div style="text-align:center;">
        <div id="team-b-name" style="font-weight:700;margin-bottom:8px;"></div>
        <input class="score-input" id="score-b" type="number" min="0" value="0">
      </div>
    </div>
    <div class="modal-actions">
      <button class="btn btn-outline" onclick="closeModal('score-modal')">إلغاء</button>
      <button class="btn btn-gold" onclick="saveScore()">💾 حفظ النتيجة</button>
    </div>
  </div>
</div>

<!-- VB SCORE MODAL -->
<div class="modal-overlay" id="vb-score-modal">
  <div class="modal">
    <div class="modal-title-teal" id="vb-score-modal-title">🏐 تسجيل نتيجة مباراة الطائرة</div>
    <div style="font-size:12px;color:var(--text-muted);margin-bottom:16px;">أدخل عدد الأشواط الفائزة لكل فريق (best of 3 = max 3)</div>
    <div style="display:flex;align-items:center;justify-content:center;gap:16px;margin:20px 0;">
      <div style="text-align:center;">
        <div id="vb-team-a-name" style="font-weight:700;margin-bottom:8px;color:var(--teal);"></div>
        <input class="score-input teal" id="vb-score-a" type="number" min="0" max="3" value="0">
        <div style="font-size:10px;color:var(--text-muted);margin-top:4px;">أشواط</div>
      </div>
      <div style="color:var(--text-muted);font-weight:700;font-size:18px;">VS</div>
      <div style="text-align:center;">
        <div id="vb-team-b-name" style="font-weight:700;margin-bottom:8px;color:var(--teal);"></div>
        <input class="score-input teal" id="vb-score-b" type="number" min="0" max="3" value="0">
        <div style="font-size:10px;color:var(--text-muted);margin-top:4px;">أشواط</div>
      </div>
    </div>
    <div class="modal-actions">
      <button class="btn btn-outline" onclick="closeModal('vb-score-modal')">إلغاء</button>
      <button class="btn btn-teal" onclick="saveVbScore()">💾 حفظ النتيجة</button>
    </div>
  </div>
</div>

<!-- ADD VB PLAYER MODAL -->
<div class="modal-overlay" id="add-vb-player-modal">
  <div class="modal">
    <div class="modal-title-teal">🏐 إضافة لاعب طائرة</div>
    <div class="form-group">
      <label class="form-label">اسم اللاعب *</label>
      <input class="form-input" id="vb-player-name" placeholder="أدخل اسم اللاعب">
    </div>
    <div class="form-group">
      <label class="form-label">العمر</label>
      <input class="form-input" type="number" id="vb-player-age" placeholder="العمر" min="10" max="60">
    </div>
    <div class="modal-actions">
      <button class="btn btn-outline" onclick="closeModal('add-vb-player-modal')">إلغاء</button>
      <button class="btn btn-teal" onclick="addVbPlayer()">إضافة</button>
    </div>
  </div>
</div>

<!-- ADD VB TEAM MODAL -->
<div class="modal-overlay" id="add-vb-team-modal">
  <div class="modal">
    <div class="modal-title-teal">🛡️ إنشاء فريق طائرة</div>
    <div class="form-group">
      <label class="form-label">اسم الفريق *</label>
      <input class="form-input" id="vb-team-name-input" placeholder="مثال: النسور، الصقور...">
    </div>
    <div class="form-group">
      <label class="form-label">اختر 6 لاعبين للفريق</label>
      <div style="font-size:11px;color:var(--text-muted);margin-bottom:6px;" id="vb-team-selection-hint">اختر بالضبط 6 لاعبين من اللاعبين المتاحين</div>
      <div class="player-checkbox-list" id="vb-player-checkbox-list"></div>
    </div>
    <div style="margin-top:8px;font-size:12px;" id="vb-selection-counter" style="color:var(--text-muted);">تم اختيار 0 من 6 لاعبين</div>
    <div class="modal-actions">
      <button class="btn btn-outline" onclick="closeModal('add-vb-team-modal')">إلغاء</button>
      <button class="btn btn-teal" onclick="saveVbTeam()">✅ إنشاء الفريق</button>
    </div>
  </div>
</div>

<!-- SPEAKER MODE OVERLAY (full black stage for live talks) -->
<div class="login-overlay" id="speaker-mode-overlay" style="display:none;background:#000;">
  <div style="text-align:center;width:100%;max-width:600px;padding:20px;">
    <div id="speaker-mic-icon" style="font-size:90px;margin-bottom:24px;animation:pulse 2s infinite;">🎤</div>
    <div id="speaker-name" style="font-size:42px;font-weight:900;color:#fff;margin-bottom:14px;line-height:1.3;"></div>
    <div id="speaker-topic" style="font-size:18px;color:rgba(255,255,255,0.6);margin-bottom:40px;"></div>
    <button onclick="exitSpeakerMode()" style="background:rgba(255,255,255,0.08);border:1px solid rgba(255,255,255,0.2);color:rgba(255,255,255,0.7);border-radius:10px;padding:10px 24px;font-family:'Tajawal',sans-serif;font-size:13px;cursor:pointer;">✕ إنهاء الفقرة والعودة</button>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
// =====================
// DATA
// =====================
const participantsData = [
  { id:1,  name:"حماد حميد عمير المقبلي",              age:46, phone:"0555894580", status:"active" },
  { id:2,  name:"عبيدالله عبدالله المقبلي",             age:45, phone:"0552046566", status:"active" },
  { id:3,  name:"مسلم حميد عمير المقبلي",               age:43, phone:"0509965570", status:"active" },
  { id:4,  name:"خالد عايد عقيل ال مقبل",               age:41, phone:"0554318741", status:"active" },
  { id:5,  name:"عبد المطلب سالم المقبلي",              age:40, phone:"0502719567", status:"active" },
  { id:6,  name:"سلمان حميد عمير المقبلي",              age:39, phone:"0555727422", status:"active" },
  { id:7,  name:"سامي رزق الله اليزيدي",                age:38, phone:"0504893402", status:"active" },
  { id:8,  name:"عطيه عاقل بطيحان اليزيدي",            age:37, phone:"0530840961", status:"active" },
  { id:9,  name:"عبد الرحمن سعيد خضر",                 age:37, phone:"0557409357", status:"active" },
  { id:10, name:"عامر عويض اليزيدي",                   age:36, phone:"0531042993", status:"active" },
  { id:11, name:"رائد عقيل اليزيدي",                   age:35, phone:"0556370025", status:"active" },
  { id:12, name:"صالح رزق الله المقبلي اليزيدي",        age:34, phone:"0596799926", status:"active" },
  { id:13, name:"عبدالله صميل اليزيدي",                age:34, phone:"0508370108", status:"active" },
  { id:14, name:"خالد حماد حميد المقبلي",               age:34, phone:"0537150534", status:"active" },
  { id:15, name:"خليل رزق الله اليزيدي",               age:33, phone:"0595929746", status:"active" },
  { id:16, name:"عامر حميد عمير المقبلي",               age:33, phone:"0554397859", status:"active" },
  { id:17, name:"عبدالله عابد عقيل ال مقبل",            age:32, phone:"0538965168", status:"active" },
  { id:18, name:"سوعيد عبدالعزيز فيصل اليزيدي",        age:32, phone:"0507309044", status:"active" },
  { id:19, name:"ثامر عويض بطيحان ال مقبل",            age:31, phone:"0599473512", status:"active" },
  { id:20, name:"عمير حميد عمير المقبلي",               age:31, phone:"0549660826", status:"active" },
  { id:21, name:"مشهور مشعل اليزيدي",                  age:30, phone:"0531513289", status:"active" },
  { id:22, name:"احمد محمد عزيز المقبلي",               age:30, phone:"0533356116", status:"active" },
  { id:23, name:"طارق سعد خضر",                        age:30, phone:"0555783596", status:"active" },
  { id:24, name:"عبد الله سعيد خضر",                   age:30, phone:"0501038641", status:"active" },
  { id:25, name:"فهد محمد عزيز اليزيدي",               age:29, phone:"0501486383", status:"active" },
  { id:26, name:"محمد حميد عمير",                      age:29, phone:"0592801450", status:"active" },
  { id:27, name:"رزق الله عاقل المقبلي",               age:29, phone:"0580472409", status:"active" },
  { id:28, name:"رامي عبد العزيز رزيق المقبلي اليزيدي", age:28, phone:"0559802139", status:"active" },
  { id:29, name:"مشاري عويض ال مقبل",                  age:28, phone:"0559737321", status:"active" },
  { id:30, name:"عبد الرحيم سعيد خضر",                 age:28, phone:"0558502414", status:"active" },
  { id:31, name:"راشد مشعل فيصل ال مقبل",              age:27, phone:"0508765717", status:"active" },
  { id:32, name:"نواف سعيد خضر",                       age:27, phone:"0538304547", status:"active" },
  { id:33, name:"فارس راشد اليزيدي",                   age:26, phone:"0555409562", status:"active" },
  { id:34, name:"سمير رديد خاضر اليزيدي",              age:26, phone:"0551239058", status:"active" },
  { id:35, name:"طايل مشعل فيصل اليزيدي",              age:26, phone:"0599050695", status:"active" },
  { id:36, name:"محمد عايد عقيل ال مقبل",              age:25, phone:"0537105709", status:"active" },
  { id:37, name:"ريان عبد العزيز رزيق المقبلي اليزيدي", age:25, phone:"0553881049", status:"active" },
  { id:38, name:"رزيق حميد عمير المقبلي",              age:25, phone:"0580646283", status:"active" },
  { id:39, name:"عبد المجيد سعيد خضر",                 age:25, phone:"0598610153", status:"active" },
  { id:40, name:"وائل جمعان رزيق المقبلي اليزيدي",     age:24, phone:"0582826411", status:"active" },
  { id:41, name:"نواف عبد العزيز فيصل اليزيدي",        age:24, phone:"0555273291", status:"active" },
  { id:42, name:"عماد عبد الهادي ال مقبل",             age:24, phone:"0553502390", status:"active" },
  { id:43, name:"اياد محمد عزيز المقبلي",              age:24, phone:"0502609668", status:"active" },
  { id:44, name:"معتز سعد خضر",                        age:24, phone:"0533848382", status:"active" },
  { id:45, name:"عبدالعزيز رزق الله اليزيدي",          age:23, phone:"0537759373", status:"active" },
  { id:46, name:"فايز راشد المقبلي",                   age:23, phone:"0581220232", status:"active" },
  { id:47, name:"عابد جمعان رزيق اليزيدي",             age:23, phone:"0582824854", status:"active" },
  { id:48, name:"عبد الله حميد المقبلي",               age:23, phone:"0593119937", status:"active" },
  { id:49, name:"بندر سعيد خضر",                       age:23, phone:"0590766402", status:"active" },
  { id:50, name:"عبدالرحمن عبد العزيز رزيق المقبلي اليزيدي", age:22, phone:"0553422979", status:"active" },
  { id:51, name:"خالد رديد اليزيدي",                   age:22, phone:"0536528033", status:"active" },
  { id:52, name:"مشهور مسلم المقبلي",                  age:22, phone:"0580708902", status:"active" },
  { id:53, name:"حسن قبيل جديع المقبلي",               age:22, phone:"0540290998", status:"active" },
  { id:54, name:"سعد سعيد خضر",                        age:22, phone:"0590727354", status:"active" },
  { id:55, name:"سعود سعيد خضر",                       age:22, phone:"0596842263", status:"active" },
  { id:56, name:"بدر عيضه بطيحان ال مقبل",             age:21, phone:"غير متوفر",  status:"active" },
  { id:57, name:"نواف مصلح رزيق اليزيدي",              age:20, phone:"0507965581", status:"active" },
  { id:58, name:"عارف عويض ال مقبل",                   age:20, phone:"0559101340", status:"active" },
  { id:59, name:"فايز سلطان المقبلي",                  age:20, phone:"0582296709", status:"active" },
  { id:60, name:"يوسف حميد عمير المقبلي",              age:20, phone:"0597757568", status:"active" },
  { id:61, name:"وليد مسلم حميد المقبلي",              age:20, phone:"0596981940", status:"active" },
  { id:62, name:"حسين قبيل جديع المقبلي",              age:20, phone:"0581761028", status:"active" },
  { id:63, name:"محمد سعيد خضر",                       age:20, phone:"0591608404", status:"active" },
  { id:64, name:"فيصل سعود خضر",                       age:20, phone:"0557686762", status:"active" },
  { id:65, name:"مشاري مصلح رزيق اليزيدي",             age:19, phone:"0595108133", status:"active" },
  { id:66, name:"مجاهد حسين المقبلي",                  age:19, phone:"0580831377", status:"active" },
  { id:67, name:"ناصر عقيل المقبلي",                   age:19, phone:"0558097471", status:"active" },
  { id:68, name:"الوليد خالد عايد ال مقبل",            age:19, phone:"0531077851", status:"active" },
  { id:69, name:"وسيم مشغل فيصل المقبلي",              age:19, phone:"0599448923", status:"active" },
  { id:70, name:"نايف سعد خضر",                        age:19, phone:"0500728099", status:"active" },
  { id:71, name:"راكان سعود خضر",                      age:19, phone:"0534716296", status:"active" },
  { id:72, name:"سياف فهد عزيز مخضور المقبلي",         age:18, phone:"0592866977", status:"active" },
  { id:73, name:"عزام مصلح رزيق اليزيدي",              age:18, phone:"0580321474", status:"active" },
  { id:74, name:"موسى مصنف شداد المقبلي",              age:18, phone:"0558183977", status:"active" },
  { id:75, name:"بدر عبدالله جديع المقبلي",            age:18, phone:"0580204487", status:"active" },
  { id:76, name:"ذياب عويض ال مقبل",                   age:18, phone:"0597187882", status:"active" },
  { id:77, name:"عبدالرحمن مقبول جديع المقبلي",        age:18, phone:"0597828045", status:"active" },
  { id:78, name:"حسام مخضور عزيز المقبلي",             age:17, phone:"0591715051", status:"active" },
  { id:79, name:"حسام عايد عقيل ال مقبل",              age:17, phone:"0552873116", status:"active" },
  { id:80, name:"محمد حسين المقبلي",                   age:17, phone:"0573697088", status:"active" },
  { id:81, name:"احمد عبدالله جديع المقبلي",           age:17, phone:"0593150163", status:"active" },
  { id:82, name:"موفق قبيل جديع المقبلي",              age:17, phone:"0592650730", status:"active" },
  { id:83, name:"عبدالله عبيدالله عبدالله المقبلي",    age:16, phone:"0555894580", status:"active" },
  { id:84, name:"عبدالله عقيل المقبلي",                age:16, phone:"0504398991", status:"active" },
  { id:85, name:"عيسى عبدالله جديع المقبلي",           age:16, phone:"0580204487", status:"active" },
  { id:86, name:"عبدالله مقبول جديع المقبلي",          age:16, phone:"0599068121", status:"active" },
  { id:87, name:"أحمد سعيد خضر",                       age:16, phone:"0596832557", status:"active" },
  { id:88, name:"بتال مصلح رزيق اليزيدي",              age:15, phone:"0580700181", status:"active" },
  { id:89, name:"هاني مصنف شداد المقبلي",              age:15, phone:"0597642939", status:"active" },
  { id:90, name:"منصور عبيدالله عبدالله المقبلي",      age:15, phone:"0555894580", status:"active" },
  { id:91, name:"مهند حسين المقبلي",                   age:15, phone:"0509965570", status:"active" },
  { id:92, name:"اسماعيل حميد عمير المقبلي",           age:15, phone:"0549660826", status:"active" },
  { id:93, name:"عيسى حميد عمير المقبلي",              age:14, phone:"0549660826", status:"active" },
  { id:94, name:"حسين جديع مخضور المقبلي",             age:46, phone:"0555894580", status:"active" },
];

const dailyReminders = [
  "«مَن صلَّى الفجرَ فهو في ذِمَّةِ اللهِ» — ابدأ يومك بالصلاة في وقتها واحرص على الفجر خاصةً.",
  "«بِرُّ الوالدَيْنِ يزيدُ في العُمرِ ويُوسِّعُ في الرزقِ» — اتصل بأمك وأبوك اليوم قبل أن ينتهي اليوم.",
  "«طَلَبُ العِلمِ فريضةٌ على كلِّ مسلمٍ» — اقرأ آية تتدبّرها أو استمع لمحاضرة نافعة اليوم.",
  "«المسلمُ مَن سَلِمَ المسلمون من لسانِه ويدِه» — احذر ما تنشره في الجوالات والتطبيقات.",
  "«خيرُكم مَن تعلَّمَ القرآنَ وعلَّمَه» — خصص 10 دقائق يومياً لتلاوة القرآن الكريم.",
  "«إذا مات الإنسان انقطع عنه عملُه إلا من ثلاثة: صدقة جارية، أو علم يُنتفع به، أو ولدٌ صالح يدعو له» — اجعل لك أثراً ينتفع به الناس.",
  "«لا يُؤمِنُ أحدُكم حتى يُحِبَّ لأخيه ما يُحِبُّ لنفسِه» — كُن كريم القلب مع إخوانك.",
];

let filteredParticipants = [...participantsData];
let currentPage = 1;
const perPage = 15;

// Baloot state
let teams = [];
let matches = [];
let currentMatchIndex = -1;

// Volleyball state
let vbPlayers = [];
let vbTeams = [];
let vbMatches = [];
let currentVbMatchIndex = -1;
let dailyReminderIndex = 0;

// =====================
// NAVIGATION
// =====================
function showPage(page) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
  document.getElementById('page-' + page).classList.add('active');
  document.querySelectorAll('.nav-item').forEach(n => {
    if (n.getAttribute('onclick') && n.getAttribute('onclick').includes("'" + page + "'")) n.classList.add('active');
  });
  const titles = {
    dashboard: ['لوحة التحكم', 'البطولات جارية الآن'],
    about: ['عن البرنامج', 'برنامج أثر التربوي الترفيهي'],
    participants: ['إدارة المشاركين', '94 مشارك مسجل'],
    teams: ['فرق البلوت', 'إنشاء وإدارة فرق البلوت'],
    draw: ['قرعة البلوت', 'توزيع الفرق عشوائياً'],
    tournament: ['بطولة البلوت', 'شجرة المباريات'],
    'vb-players': ['لاعبو الطائرة', 'إدارة لاعبي الكرة الطائرة'],
    'vb-teams': ['فرق الطائرة', 'كل فريق = 6 لاعبين'],
    'vb-tournament': ['بطولة الطائرة', 'شجرة مباريات الكرة الطائرة'],
    meetings: ['الفعاليات', 'اللقاءات الأربعة السنوية'],
    mic: ['الميكروفون الحر 🎤', 'كل مشارك يتحدث 30-120 ثانية'],
    religion: ['الدين', 'نصائح وتوجيهات إسلامية للشباب'],
    familytree: ['شجرة النسب', 'آل مقبل اليزيدي 🌳'],
    achievements: ['الإنجازات', 'شارات أبطال البلوت والطائرة 🏅'],
    settings: ['الإعدادات', 'إعدادات البرنامج'],
  };
  if (titles[page]) {
    document.getElementById('page-title').textContent = titles[page][0];
    document.getElementById('page-sub').textContent = titles[page][1];
  }
  if (page === 'participants') renderParticipants();
  if (page === 'dashboard') updateDashboard();
  if (page === 'teams') { renderTeams(); renderBalootPlayers(); }
  if (page === 'vb-players') renderVbPlayers();
  if (page === 'vb-teams') renderVbTeams();
  if (page === 'religion') showDailyReminder();
  if (page === 'mic') initMicPage();
  if (page === 'achievements') renderAchievements();
}

// =====================
// PARTICIPANTS
// =====================
function filterParticipants() {
  const q = document.getElementById('search-input').value.trim().toLowerCase();
  const af = document.getElementById('age-filter').value;
  filteredParticipants = participantsData.filter(p => {
    const matchQ = !q || p.name.toLowerCase().includes(q) || p.phone.includes(q);
    let matchA = true;
    if (af === '15-20') matchA = p.age >= 15 && p.age <= 20;
    else if (af === '21-25') matchA = p.age >= 21 && p.age <= 25;
    else if (af === '26-30') matchA = p.age >= 26 && p.age <= 30;
    else if (af === '31-35') matchA = p.age >= 31 && p.age <= 35;
    else if (af === '36+') matchA = p.age >= 36;
    return matchQ && matchA;
  });
  currentPage = 1;
  renderParticipants();
}

function renderParticipants() {
  const tbody = document.getElementById('participants-tbody');
  const total = filteredParticipants.length;
  const start = (currentPage - 1) * perPage;
  const slice = filteredParticipants.slice(start, start + perPage);
  document.getElementById('participants-count').textContent = total + ' مشارك';

  const isViewer = currentRole === 'viewer';

  // Show/hide add button and actions column header
  const addBtn = document.querySelector('#page-participants .btn-gold');
  if (addBtn) addBtn.style.display = isViewer ? 'none' : '';
  const actionsHeader = document.querySelector('#page-participants thead th:last-child');
  if (actionsHeader) actionsHeader.style.display = isViewer ? 'none' : '';

  tbody.innerHTML = slice.map((p, i) => {
    const balootTeam = getParticipantTeam(p.id);
    const vbTeam = getVbParticipantTeam(p.id);
    const ageBadge = p.age >= 30 ? 'badge-gold' : p.age >= 20 ? 'badge-green' : 'badge-blue';
    return `<tr>
      <td style="color:var(--text-muted);font-weight:700;">${start + i + 1}</td>
      <td style="font-weight:600;">${p.name}</td>
      <td><span class="badge ${ageBadge}">${p.age} سنة</span></td>
      <td style="color:var(--text-muted);direction:ltr;text-align:right;">${p.phone || '-'}</td>
      <td><span class="badge badge-green">نشط</span></td>
      <td>${balootTeam ? `<span class="badge badge-gold">${balootTeam}</span>` : '<span style="color:var(--text-muted)">-</span>'}</td>
      <td>${vbTeam ? `<span class="badge badge-teal">${vbTeam}</span>` : '<span style="color:var(--text-muted)">-</span>'}</td>
      ${isViewer ? '' : `<td>
        <button class="btn btn-outline" style="padding:4px 10px;font-size:11px;" onclick="editParticipant(${p.id})">✏️</button>
        <button class="btn btn-red" style="padding:4px 10px;font-size:11px;margin-right:4px;" onclick="deleteParticipant(${p.id})">🗑️</button>
      </td>`}
    </tr>`;
  }).join('');
  renderPagination(total);
}

function getParticipantTeam(pid) {
  for (const t of teams) {
    if (t.members && t.members.includes(pid)) return t.name;
  }
  return null;
}

function getVbParticipantTeam(playerId) {
  for (const t of vbTeams) {
    if (t.playerIds && t.playerIds.some(id => id == playerId)) return t.name;
  }
  return null;
}

function renderPagination(total) {
  const pages = Math.ceil(total / perPage);
  const el = document.getElementById('pagination');
  if (pages <= 1) { el.innerHTML = ''; return; }
  let html = `<button class="page-btn" onclick="changePage(${currentPage-1})" ${currentPage===1?'disabled':''}>›</button>`;
  for (let i = 1; i <= pages; i++) {
    html += `<button class="page-btn ${i===currentPage?'active':''}" onclick="changePage(${i})">${i}</button>`;
  }
  html += `<button class="page-btn" onclick="changePage(${currentPage+1})" ${currentPage===pages?'disabled':''}>‹</button>`;
  html += `<span class="page-info">${(currentPage-1)*perPage+1} - ${Math.min(currentPage*perPage,total)} من ${total}</span>`;
  el.innerHTML = html;
}

function changePage(p) {
  const pages = Math.ceil(filteredParticipants.length / perPage);
  if (p < 1 || p > pages) return;
  currentPage = p;
  renderParticipants();
}

function openAddModal() {
  document.getElementById('new-name').value = '';
  document.getElementById('new-age').value = '';
  document.getElementById('new-phone').value = '';
  document.getElementById('add-modal').classList.add('open');
}

function addParticipant() {
  const name = document.getElementById('new-name').value.trim();
  const age = parseInt(document.getElementById('new-age').value);
  const phone = document.getElementById('new-phone').value.trim();
  if (!name) { showToast('⚠️ يرجى إدخال الاسم'); return; }
  if (!age || age < 10) { showToast('⚠️ يرجى إدخال عمر صحيح'); return; }
  const newId = Math.max(...participantsData.map(p => p.id)) + 1;
  participantsData.push({ id: newId, name, age, phone, status: 'active' });
  filteredParticipants = [...participantsData];
  closeModal('add-modal');
  renderParticipants();
  updateDashboard();
  showToast('✅ تم إضافة المشارك بنجاح');
}

function deleteParticipant(id) {
  if (!confirm('هل تريد حذف هذا المشارك؟')) return;
  const idx = participantsData.findIndex(p => p.id === id);
  if (idx > -1) participantsData.splice(idx, 1);
  filteredParticipants = [...participantsData];
  renderParticipants();
  updateDashboard();
  showToast('🗑️ تم حذف المشارك');
}

function editParticipant(id) { showToast('✏️ ميزة التعديل قريباً'); }

// =====================
// BALOOT PLAYERS & TEAMS
// =====================
let balootPlayers = []; // { id, name } — subset of participantsData added to baloot

function openAddBalootPlayerModal() {
  document.getElementById('baloot-player-search').value = '';
  renderBalootPlayerSearchList('');
  document.getElementById('add-baloot-player-modal').classList.add('open');
}

function filterBalootPlayerSearch() {
  const q = document.getElementById('baloot-player-search').value.trim().toLowerCase();
  renderBalootPlayerSearchList(q);
}

function renderBalootPlayerSearchList(q) {
  const already = balootPlayers.map(p => p.id);
  const available = participantsData.filter(p => {
    if (already.includes(p.id)) return false;
    return !q || p.name.toLowerCase().includes(q);
  });
  const el = document.getElementById('baloot-player-search-list');
  if (available.length === 0) {
    el.innerHTML = '<div style="color:var(--text-muted);font-size:12px;padding:10px;">لا يوجد مزيد من المشاركين أو لا توجد نتائج.</div>';
    return;
  }
  el.innerHTML = available.map(p => `
    <label class="player-checkbox-item">
      <input type="checkbox" value="${p.id}">
      <span>${p.name}</span>
      <span style="font-size:10px;color:var(--text-muted);margin-right:auto;">${p.age} سنة</span>
    </label>
  `).join('');
}

function addSelectedBalootPlayers() {
  const checked = [...document.querySelectorAll('#baloot-player-search-list input:checked')];
  if (checked.length === 0) { showToast('⚠️ اختر لاعباً واحداً على الأقل'); return; }
  checked.forEach(cb => {
    const pid = parseInt(cb.value);
    const p = participantsData.find(x => x.id === pid);
    if (p) balootPlayers.push({ id: p.id, name: p.name });
  });
  closeModal('add-baloot-player-modal');
  renderBalootPlayers();
  showToast(`✅ تمت إضافة ${checked.length} لاعب للبلوت`);
}

function renderBalootPlayers() {
  const el = document.getElementById('baloot-players-list');
  const badge = document.getElementById('baloot-players-count');
  if (badge) badge.textContent = balootPlayers.length + ' لاعب';
  if (balootPlayers.length === 0) {
    el.innerHTML = '<div style="color:var(--text-muted);font-size:13px;text-align:center;padding:20px;">لا يوجد لاعبون بعد.</div>';
    return;
  }
  el.innerHTML = balootPlayers.map((p, i) => {
    const team = teams.find(t => t.members && t.members.includes(p.id));
    return `<div style="display:flex;align-items:center;gap:10px;padding:8px 0;border-bottom:1px solid var(--border);">
      <div style="width:26px;height:26px;border-radius:6px;background:rgba(201,168,76,0.15);color:var(--gold);font-weight:900;font-size:12px;display:flex;align-items:center;justify-content:center;flex-shrink:0;">${i+1}</div>
      <div style="flex:1;font-size:13px;font-weight:600;">${p.name}</div>
      <div>${team ? `<span class="badge badge-gold">${team.name}</span>` : '<span style="font-size:10px;color:var(--text-muted);">بدون فريق</span>'}</div>
      <button onclick="removeBalootPlayer(${p.id})" style="background:none;border:none;color:var(--red);cursor:pointer;font-size:14px;">✕</button>
    </div>`;
  }).join('');
}

function removeBalootPlayer(pid) {
  balootPlayers = balootPlayers.filter(p => p.id !== pid);
  // also remove from teams
  teams.forEach(t => { t.members = (t.members||[]).filter(id => id !== pid); });
  teams = teams.filter(t => t.members.length > 0);
  renderBalootPlayers();
  renderTeams();
  updateDashboard();
}

function autoGenerateBalootTeams() {
  if (balootPlayers.length < 2) { showToast('⚠️ أضف لاعبين أولاً (2 على الأقل)'); return; }
  if (balootPlayers.length % 2 !== 0) { showToast(`⚠️ عدد اللاعبين (${balootPlayers.length}) يجب أن يكون زوجياً لتوزيع الثنائيات`); return; }
  // Clear existing teams
  teams = [];
  const shuffled = [...balootPlayers].sort(() => Math.random() - 0.5);
  const teamNames = ['الصقور','النسور','الأسود','الذئاب','الفهود','العقبان','الأبطال','النجوم','الرياح','البروق','الأمواج','الجبال'];
  for (let i = 0; i < shuffled.length; i += 2) {
    const tName = teamNames[teams.length] || `فريق ${teams.length + 1}`;
    teams.push({
      id: teams.length + 1,
      name: tName,
      members: [shuffled[i].id, shuffled[i+1].id],
      memberNames: [shuffled[i].name, shuffled[i+1].name],
      wins: 0, losses: 0
    });
  }
  renderTeams();
  renderBalootPlayers();
  updateDashboard();
  showToast(`🎲 تم توزيع ${teams.length} ثنائي عشوائياً!`);
}

function openManualTeamModal() {
  if (balootPlayers.length < 2) { showToast('⚠️ أضف لاعبين أولاً'); return; }
  document.getElementById('manual-team-name').value = '';
  const unassigned = balootPlayers.filter(p => !teams.some(t => t.members.includes(p.id)));
  const el = document.getElementById('manual-team-player-list');
  if (unassigned.length < 2) {
    el.innerHTML = '<div style="color:var(--text-muted);font-size:12px;padding:10px;">جميع اللاعبين في فرق. أضف لاعبين جدد.</div>';
  } else {
    el.innerHTML = unassigned.map(p => `
      <label class="player-checkbox-item">
        <input type="checkbox" value="${p.id}" onchange="updateManualTeamCounter()">
        <span>${p.name}</span>
      </label>
    `).join('');
  }
  document.getElementById('manual-team-counter').textContent = 'تم اختيار 0 من 2';
  document.getElementById('manual-team-modal').classList.add('open');
}

function updateManualTeamCounter() {
  const count = document.querySelectorAll('#manual-team-player-list input:checked').length;
  const el = document.getElementById('manual-team-counter');
  el.textContent = `تم اختيار ${count} من 2`;
  el.style.color = count === 2 ? 'var(--gold)' : count > 2 ? 'var(--red)' : 'var(--text-muted)';
}

function saveManualTeam() {
  const checked = [...document.querySelectorAll('#manual-team-player-list input:checked')].map(cb => parseInt(cb.value));
  if (checked.length !== 2) { showToast('⚠️ يجب اختيار لاعبين اثنين بالضبط'); return; }
  const nameInput = document.getElementById('manual-team-name').value.trim();
  const p1 = balootPlayers.find(p => p.id === checked[0]);
  const p2 = balootPlayers.find(p => p.id === checked[1]);
  const tName = nameInput || `${p1.name} و ${p2.name}`;
  teams.push({ id: teams.length + 1, name: tName, members: checked, memberNames: [p1.name, p2.name], wins: 0, losses: 0 });
  closeModal('manual-team-modal');
  renderTeams();
  renderBalootPlayers();
  updateDashboard();
  showToast(`✅ تم إنشاء فريق: ${tName}`);
}

function resetBalootTeams() {
  if (!confirm('هل تريد مسح جميع الفرق؟')) return;
  teams = [];
  renderTeams();
  renderBalootPlayers();
  updateDashboard();
  showToast('🗑️ تم مسح جميع الفرق');
}

function renderTeams() {
  const grid = document.getElementById('teams-grid');
  const badge = document.getElementById('teams-count-badge');
  if (badge) badge.textContent = teams.length + ' فريق';
  if (teams.length === 0) {
    grid.innerHTML = '<div style="color:var(--text-muted);font-size:13px;text-align:center;padding:20px;grid-column:1/-1;">لا توجد فرق بعد.<br>أضف لاعبين ثم وزّع عشوائياً.</div>';
    return;
  }
  grid.innerHTML = teams.map(t => `
    <div class="team-card" style="min-width:0;">
      ${t.wins > 0 ? `<div class="team-wins">✓ ${t.wins}</div>` : ''}
      <div class="team-number" style="font-size:20px;">🂠</div>
      <div class="team-name" style="font-size:12px;">${t.name}</div>
      <div style="margin-top:8px;">
        ${(t.memberNames||[]).map(n => `<div style="font-size:11px;color:var(--text-muted);padding:2px 0;border-bottom:1px solid rgba(255,255,255,0.05);">▸ ${n}</div>`).join('')}
      </div>
      <div style="margin-top:6px;"><span class="badge badge-gold">${(t.members||[]).length} لاعبين</span></div>
    </div>
  `).join('');
}

// =====================
// BALOOT DRAW & TOURNAMENT
// =====================
function runDraw() {
  if (teams.length === 0) { showToast('⚠️ أنشئ الفرق أولاً من صفحة الفرق'); return; }
  const shuffled = [...teams].sort(() => Math.random() - 0.5);
  const container = document.getElementById('draw-result-container');
  container.innerHTML = `
    <div class="card">
      <div class="card-header">
        <span class="card-title">🎲 نتيجة القرعة</span>
        <span class="card-badge">${teams.length} فريق</span>
      </div>
      <div style="display:grid;grid-template-columns:repeat(auto-fill,minmax(120px,1fr));gap:10px;margin-top:12px;">
        ${shuffled.map((t, i) => `
          <div style="background:var(--surface2);border:1px solid var(--border);border-radius:8px;padding:10px;text-align:center;">
            <div style="font-size:10px;color:var(--gold);margin-bottom:4px;">المركز ${i+1}</div>
            <div style="font-size:13px;font-weight:700;">${t.name}</div>
          </div>
        `).join('')}
      </div>
      <button class="btn btn-gold" style="margin-top:16px;" onclick="generateBracket();showPage('tournament')">🏆 بدء البطولة</button>
    </div>
  `;
  showToast('🎲 تمت القرعة بنجاح!');
}

function generateBracket() {
  if (teams.length === 0) { showToast('⚠️ أنشئ الفرق أولاً'); return; }
  const shuffled = [...teams].sort(() => Math.random() - 0.5);
  const size = Math.pow(2, Math.ceil(Math.log2(shuffled.length)));
  const padded = [...shuffled];
  while (padded.length < size) padded.push(null);
  matches = [];
  let matchId = 0;
  for (let i = 0; i < padded.length; i += 2) {
    matches.push({ id: matchId++, round: 1, teamA: padded[i], teamB: padded[i+1], scoreA: null, scoreB: null, winner: null });
  }
  const totalRounds = Math.log2(size);
  let prevRound = matches.filter(m => m.round === 1);
  for (let r = 2; r <= totalRounds; r++) {
    const newM = [];
    for (let i = 0; i < prevRound.length; i += 2) {
      newM.push({ id: matchId++, round: r, teamA: null, teamB: null, scoreA: null, scoreB: null, winner: null, prevA: prevRound[i].id, prevB: prevRound[i+1]?.id });
    }
    matches.push(...newM);
    prevRound = newM;
  }
  renderBracket();
  document.getElementById('current-round-label').textContent = `دور الـ ${size}`;
}

function renderBracket() {
  const display = document.getElementById('bracket-display');
  const totalRounds = Math.max(...matches.map(m => m.round));
  const roundNames = { 1: 'دور أول', 2: 'ربع النهائي', 3: 'نصف النهائي', 4: 'النهائي' };
  let html = '<div class="bracket">';
  for (let r = 1; r <= totalRounds; r++) {
    const rm = matches.filter(m => m.round === r);
    const rName = roundNames[r] || `دور ${r}`;
    html += `<div class="bracket-round"><div class="bracket-round-title">${rName}</div>`;
    rm.forEach(m => {
      const tA = m.teamA ? m.teamA.name : 'TBD';
      const tB = m.teamB ? m.teamB.name : 'TBD';
      const membersA = m.teamA && m.teamA.memberNames ? `<div style="font-size:9px;color:var(--text-muted);line-height:1.3;">${m.teamA.memberNames.join(' & ')}</div>` : '';
      const membersB = m.teamB && m.teamB.memberNames ? `<div style="font-size:9px;color:var(--text-muted);line-height:1.3;">${m.teamB.memberNames.join(' & ')}</div>` : '';
      const sA = m.scoreA !== null ? m.scoreA : '-';
      const sB = m.scoreB !== null ? m.scoreB : '-';
      const winA = m.winner && m.winner.id === m.teamA?.id;
      const winB = m.winner && m.winner.id === m.teamB?.id;
      html += `<div class="match-wrapper">
        <div class="match-box" onclick="openScoreModal(${m.id})">
          <div class="match-team ${winA ? 'winner' : ''}" style="flex-direction:column;align-items:flex-start;gap:1px;padding:7px 10px;">
            <div style="display:flex;width:100%;justify-content:space-between;align-items:center;"><span style="font-weight:700;">${tA}</span><span class="match-score">${sA}</span></div>
            ${membersA}
          </div>
          <div class="match-team ${winB ? 'winner' : ''}" style="flex-direction:column;align-items:flex-start;gap:1px;padding:7px 10px;">
            <div style="display:flex;width:100%;justify-content:space-between;align-items:center;"><span style="font-weight:700;">${tB}</span><span class="match-score">${sB}</span></div>
            ${membersB}
          </div>
          ${!m.winner ? '<button class="match-btn">تسجيل النتيجة</button>' : '<div style="padding:3px;text-align:center;font-size:10px;color:var(--green);">✓ انتهت</div>'}
        </div>
      </div>`;
    });
    html += '</div>';
  }
  html += '</div>';
  display.innerHTML = html;
  checkChampion();
}

function openScoreModal(matchId) {
  const m = matches.find(x => x.id === matchId);
  if (!m || !m.teamA || !m.teamB) { showToast('⚠️ هذه المباراة تنتظر نتيجة الدور السابق'); return; }
  currentMatchIndex = matchId;
  document.getElementById('score-modal-title').textContent = `${m.teamA.name} ضد ${m.teamB.name}`;
  document.getElementById('team-a-name').textContent = m.teamA.name;
  document.getElementById('team-b-name').textContent = m.teamB.name;
  document.getElementById('score-a').value = m.scoreA || 0;
  document.getElementById('score-b').value = m.scoreB || 0;
  document.getElementById('score-modal').classList.add('open');
}

function saveScore() {
  const sA = parseInt(document.getElementById('score-a').value);
  const sB = parseInt(document.getElementById('score-b').value);
  if (sA === sB) { showToast('⚠️ لا يمكن التعادل في البلوت'); return; }
  const m = matches.find(x => x.id === currentMatchIndex);
  m.scoreA = sA; m.scoreB = sB;
  m.winner = sA > sB ? m.teamA : m.teamB;
  if (m.winner.wins !== undefined) m.winner.wins++;
  const loser = sA > sB ? m.teamB : m.teamA;
  if (loser && loser.losses !== undefined) loser.losses++;
  const nextMatch = matches.find(nm => nm.prevA === m.id || nm.prevB === m.id);
  if (nextMatch) {
    if (nextMatch.prevA === m.id) nextMatch.teamA = m.winner;
    else nextMatch.teamB = m.winner;
  }
  closeModal('score-modal');
  renderBracket();
  renderTeams();
  updateDashboard();
  showToast(`🏆 فاز ${m.winner.name}!`);
}

function checkChampion() {
  const finalMatch = matches.find(m => m.round === Math.max(...matches.map(x => x.round)));
  const display = document.getElementById('champion-display');
  if (finalMatch && finalMatch.winner) {
    const champTeam = finalMatch.winner;
    const memberNames = champTeam.memberNames || [];
    display.innerHTML = `<div class="champion-banner">
      <div class="champion-label">🎉 بطل بطولة البلوت</div>
      <div class="champion-name">🏆 ${champTeam.name}</div>
      ${memberNames.length ? `<div style="margin-top:10px;display:flex;gap:10px;justify-content:center;flex-wrap:wrap;">
        ${memberNames.map(n => `
          <div style="background:rgba(201,168,76,0.15);border:1px solid rgba(201,168,76,0.4);border-radius:12px;padding:10px 18px;">
            <div style="font-size:22px;">🥇</div>
            <div style="font-size:13px;font-weight:700;color:var(--gold-light);margin-top:4px;">${n}</div>
            <div style="font-size:10px;color:var(--gold);margin-top:2px;">بطل البلوت 2026</div>
          </div>
        `).join('')}
      </div>` : ''}
    </div>`;
    awardBalootAchievement(champTeam);
  } else {
    display.innerHTML = '';
  }
}

// =====================
// ACHIEVEMENT BADGES
// =====================
let achievements = []; // { id, type:'baloot'|'volleyball', icon, title, names, date }
let lastBalootChampionId = null;
let lastVbChampionId = null;

function awardBalootAchievement(champTeam) {
  if (lastBalootChampionId === champTeam.id) return; // already awarded
  lastBalootChampionId = champTeam.id;
  achievements.push({
    id: 'baloot-' + champTeam.id + '-' + Date.now(),
    type: 'baloot',
    icon: '🥇',
    title: 'بطل بطولة البلوت 2026',
    names: champTeam.memberNames || [champTeam.name],
    teamName: champTeam.name,
    date: new Date().toLocaleDateString('ar-SA')
  });
  showToast(`🏅 تم منح شارة "بطل البلوت" لفريق ${champTeam.name}!`);
  renderAchievements();
}

function showStandings() {
  const sc = document.getElementById('standings-container');
  if (sc.style.display === 'block') { sc.style.display = 'none'; return; }
  const sorted = [...teams].sort((a, b) => (b.wins || 0) - (a.wins || 0));
  sc.innerHTML = `<div class="card">
    <div class="card-header"><span class="card-title">📊 ترتيب فرق البلوت</span></div>
    <table class="standings-table">
      <thead><tr><th>#</th><th>الفريق</th><th>انتصارات</th><th>خسائر</th></tr></thead>
      <tbody>${sorted.map((t, i) => `<tr>
        <td class="pos-num">${i+1}</td><td>${t.name}</td>
        <td style="color:var(--green)">${t.wins || 0}</td>
        <td style="color:var(--red)">${t.losses || 0}</td>
      </tr>`).join('')}</tbody>
    </table>
  </div>`;
  sc.style.display = 'block';
}

// =====================
// VOLLEYBALL PLAYERS
// =====================
function openAddVbPlayerModal() {
  document.getElementById('vb-player-name').value = '';
  document.getElementById('vb-player-age').value = '';
  document.getElementById('add-vb-player-modal').classList.add('open');
}

function addVbPlayer() {
  const name = document.getElementById('vb-player-name').value.trim();
  const age = parseInt(document.getElementById('vb-player-age').value) || 0;
  if (!name) { showToast('⚠️ أدخل اسم اللاعب'); return; }
  const newId = vbPlayers.length > 0 ? Math.max(...vbPlayers.map(p => p.id)) + 1 : 1;
  vbPlayers.push({ id: newId, name, age, teamId: null });
  closeModal('add-vb-player-modal');
  renderVbPlayers();
  updateDashboard();
  showToast('✅ تم إضافة اللاعب: ' + name);
}

function renderVbPlayers() {
  const grid = document.getElementById('vb-players-grid');
  const badge = document.getElementById('vb-players-count-badge');
  if (badge) badge.textContent = vbPlayers.length + ' لاعب';
  if (vbPlayers.length === 0) {
    grid.innerHTML = '<div style="color:var(--text-muted);font-size:13px;text-align:center;padding:30px;grid-column:1/-1;">لا يوجد لاعبون بعد. ابدأ بإضافة لاعبين.</div>';
    return;
  }
  grid.innerHTML = vbPlayers.map((p, i) => {
    const team = vbTeams.find(t => t.playerIds && t.playerIds.includes(p.id));
    return `<div class="vb-player-card">
      <div class="vb-player-num">${i + 1}</div>
      <div>
        <div class="vb-player-name">${p.name}</div>
        <div class="vb-player-team">${team ? '🛡️ ' + team.name : '⚪ بدون فريق'}</div>
      </div>
    </div>`;
  }).join('');
}

// =====================
// VOLLEYBALL TEAMS
// =====================
function openAddVbTeamModal() {
  document.getElementById('vb-team-name-input').value = '';
  // Build player checkbox list — only unassigned players
  const available = vbPlayers.filter(p => !vbTeams.some(t => t.playerIds && t.playerIds.includes(p.id)));
  const list = document.getElementById('vb-player-checkbox-list');
  if (available.length === 0) {
    list.innerHTML = '<div style="color:var(--text-muted);font-size:13px;padding:10px;">لا يوجد لاعبون متاحون. أضف لاعبين أولاً.</div>';
  } else {
    list.innerHTML = available.map(p => `
      <label class="player-checkbox-item">
        <input type="checkbox" value="${p.id}" onchange="updateVbSelectionCount()">
        <span>${p.name}</span>
        ${p.age ? `<span style="font-size:10px;color:var(--text-muted);margin-right:auto;">${p.age} سنة</span>` : ''}
      </label>
    `).join('');
  }
  document.getElementById('vb-selection-counter').textContent = 'تم اختيار 0 من 6 لاعبين';
  document.getElementById('add-vb-team-modal').classList.add('open');
}

function updateVbSelectionCount() {
  const checked = document.querySelectorAll('#vb-player-checkbox-list input:checked').length;
  const counter = document.getElementById('vb-selection-counter');
  counter.textContent = `تم اختيار ${checked} من 6 لاعبين`;
  counter.style.color = checked === 6 ? 'var(--teal)' : checked > 6 ? 'var(--red)' : 'var(--text-muted)';
}

function saveVbTeam() {
  const name = document.getElementById('vb-team-name-input').value.trim();
  if (!name) { showToast('⚠️ أدخل اسم الفريق'); return; }
  const checked = [...document.querySelectorAll('#vb-player-checkbox-list input:checked')].map(cb => parseInt(cb.value));
  if (checked.length !== 6) { showToast(`⚠️ يجب اختيار 6 لاعبين بالضبط (اخترت ${checked.length})`); return; }
  const newId = vbTeams.length > 0 ? Math.max(...vbTeams.map(t => t.id)) + 1 : 1;
  vbTeams.push({ id: newId, name, playerIds: checked, wins: 0, losses: 0 });
  closeModal('add-vb-team-modal');
  renderVbTeams();
  renderVbPlayers();
  updateDashboard();
  showToast(`✅ تم إنشاء فريق "${name}" بـ 6 لاعبين`);
}

function renderVbTeams() {
  const grid = document.getElementById('vb-teams-grid');
  const badge = document.getElementById('vb-teams-count-badge');
  if (badge) badge.textContent = vbTeams.length + ' فريق';
  if (vbTeams.length === 0) {
    grid.innerHTML = '<div style="color:var(--text-muted);font-size:13px;text-align:center;padding:30px;grid-column:1/-1;">لا توجد فرق بعد.</div>';
    return;
  }
  grid.innerHTML = vbTeams.map(t => {
    const players = t.playerIds.map(id => vbPlayers.find(p => p.id === id)).filter(Boolean);
    const isReady = players.length === 6;
    return `<div class="team-card vb-team ${isReady ? 'vb-team-ready' : 'vb-team-full'}">
      ${t.wins > 0 ? `<div class="team-wins" style="background:rgba(20,184,166,0.15);color:var(--teal);">✓ ${t.wins}</div>` : ''}
      <div class="team-number teal">🏐</div>
      <div class="team-name">${t.name}</div>
      <div class="team-members-list" style="text-align:right;">
        ${players.map(p => `<div style="font-size:11px;padding:2px 0;border-bottom:1px solid rgba(255,255,255,0.05);">▸ ${p.name}</div>`).join('')}
      </div>
      <div style="margin-top:8px;">
        <span class="badge badge-teal">${players.length}/6 لاعب</span>
      </div>
    </div>`;
  }).join('');
}

// =====================
// VOLLEYBALL TOURNAMENT
// =====================
function generateVbBracket() {
  if (vbTeams.length < 2) { showToast('⚠️ تحتاج فريقين على الأقل'); return; }
  const shuffled = [...vbTeams].sort(() => Math.random() - 0.5);
  const size = Math.pow(2, Math.ceil(Math.log2(shuffled.length)));
  const padded = [...shuffled];
  while (padded.length < size) padded.push(null);
  vbMatches = [];
  let matchId = 0;
  for (let i = 0; i < padded.length; i += 2) {
    vbMatches.push({ id: matchId++, round: 1, teamA: padded[i], teamB: padded[i+1], scoreA: null, scoreB: null, winner: null });
  }
  const totalRounds = Math.log2(size);
  let prevRound = vbMatches.filter(m => m.round === 1);
  for (let r = 2; r <= totalRounds; r++) {
    const newM = [];
    for (let i = 0; i < prevRound.length; i += 2) {
      newM.push({ id: matchId++, round: r, teamA: null, teamB: null, scoreA: null, scoreB: null, winner: null, prevA: prevRound[i].id, prevB: prevRound[i+1]?.id });
    }
    vbMatches.push(...newM);
    prevRound = newM;
  }
  renderVbBracket();
  document.getElementById('vb-round-label').textContent = `${vbTeams.length} فريق`;
}

function renderVbBracket() {
  const display = document.getElementById('vb-bracket-display');
  const totalRounds = Math.max(...vbMatches.map(m => m.round));
  const roundNames = { 1: 'دور أول', 2: 'ربع النهائي', 3: 'نصف النهائي', 4: 'النهائي' };
  let html = '<div class="bracket">';
  for (let r = 1; r <= totalRounds; r++) {
    const rm = vbMatches.filter(m => m.round === r);
    const rName = roundNames[r] || `دور ${r}`;
    html += `<div class="bracket-round"><div class="bracket-round-title-teal">${rName}</div>`;
    rm.forEach(m => {
      const tA = m.teamA ? m.teamA.name : 'TBD';
      const tB = m.teamB ? m.teamB.name : 'TBD';
      const sA = m.scoreA !== null ? m.scoreA : '-';
      const sB = m.scoreB !== null ? m.scoreB : '-';
      const winA = m.winner && m.winner.id === m.teamA?.id;
      const winB = m.winner && m.winner.id === m.teamB?.id;
      html += `<div class="match-wrapper">
        <div class="vb-match-box" onclick="openVbScoreModal(${m.id})">
          <div class="vb-match-team ${winA ? 'winner' : ''}"><span>${tA}</span><span class="match-score">${sA}</span></div>
          <div class="vb-match-team ${winB ? 'winner' : ''}"><span>${tB}</span><span class="match-score">${sB}</span></div>
          ${!m.winner ? '<button class="vb-match-btn">تسجيل النتيجة</button>' : '<div style="padding:3px;text-align:center;font-size:10px;color:var(--teal);">✓ انتهت</div>'}
        </div>
      </div>`;
    });
    html += '</div>';
  }
  html += '</div>';
  display.innerHTML = html;
  checkVbChampion();
}

function openVbScoreModal(matchId) {
  const m = vbMatches.find(x => x.id === matchId);
  if (!m || !m.teamA || !m.teamB) { showToast('⚠️ هذه المباراة تنتظر نتيجة الدور السابق'); return; }
  currentVbMatchIndex = matchId;
  document.getElementById('vb-score-modal-title').textContent = `🏐 ${m.teamA.name} ضد ${m.teamB.name}`;
  document.getElementById('vb-team-a-name').textContent = m.teamA.name;
  document.getElementById('vb-team-b-name').textContent = m.teamB.name;
  document.getElementById('vb-score-a').value = m.scoreA || 0;
  document.getElementById('vb-score-b').value = m.scoreB || 0;
  document.getElementById('vb-score-modal').classList.add('open');
}

function saveVbScore() {
  const sA = parseInt(document.getElementById('vb-score-a').value);
  const sB = parseInt(document.getElementById('vb-score-b').value);
  if (sA === sB) { showToast('⚠️ لا يمكن التعادل في الطائرة'); return; }
  if (sA > 3 || sB > 3) { showToast('⚠️ الحد الأقصى 3 أشواط'); return; }
  const m = vbMatches.find(x => x.id === currentVbMatchIndex);
  m.scoreA = sA; m.scoreB = sB;
  m.winner = sA > sB ? m.teamA : m.teamB;
  if (m.winner.wins !== undefined) m.winner.wins++;
  const loser = sA > sB ? m.teamB : m.teamA;
  if (loser && loser.losses !== undefined) loser.losses++;
  const nextMatch = vbMatches.find(nm => nm.prevA === m.id || nm.prevB === m.id);
  if (nextMatch) {
    if (nextMatch.prevA === m.id) nextMatch.teamA = m.winner;
    else nextMatch.teamB = m.winner;
  }
  closeModal('vb-score-modal');
  renderVbBracket();
  renderVbTeams();
  updateDashboard();
  showToast(`🏐 فاز ${m.winner.name}!`);
}

function checkVbChampion() {
  const finalMatch = vbMatches.find(m => m.round === Math.max(...vbMatches.map(x => x.round)));
  const display = document.getElementById('vb-champion-display');
  if (finalMatch && finalMatch.winner) {
    const champTeam = finalMatch.winner;
    const players = (champTeam.playerIds || []).map(id => vbPlayers.find(p => p.id === id)).filter(Boolean);
    display.innerHTML = `<div class="champion-banner teal">
      <div class="champion-label teal">🎉 بطل بطولة الطائرة</div>
      <div class="champion-name teal">🏐 ${champTeam.name}</div>
      ${players.length ? `<div style="margin-top:10px;display:flex;gap:8px;justify-content:center;flex-wrap:wrap;">
        ${players.map(p => `
          <div style="background:rgba(20,184,166,0.15);border:1px solid rgba(20,184,166,0.4);border-radius:10px;padding:7px 12px;">
            <span style="font-size:11px;font-weight:700;color:#2dd4bf;">🥇 ${p.name}</span>
          </div>
        `).join('')}
      </div>` : ''}
      <div style="margin-top:8px;font-size:11px;color:var(--teal);">شارة فريقية: بطل الطائرة 2026 🏐</div>
    </div>`;
    awardVbAchievement(champTeam, players);
  } else {
    display.innerHTML = '';
  }
}

function awardVbAchievement(champTeam, players) {
  if (lastVbChampionId === champTeam.id) return;
  lastVbChampionId = champTeam.id;
  achievements.push({
    id: 'vb-' + champTeam.id + '-' + Date.now(),
    type: 'volleyball',
    icon: '🏐',
    title: 'بطل بطولة الطائرة 2026',
    names: players.map(p => p.name),
    teamName: champTeam.name,
    date: new Date().toLocaleDateString('ar-SA')
  });
  showToast(`🏅 تم منح شارة "بطل الطائرة" لفريق ${champTeam.name}!`);
  renderAchievements();
}

function renderAchievements() {
  const el = document.getElementById('achievements-list');
  if (!el) return;
  if (achievements.length === 0) {
    el.innerHTML = '<div style="color:var(--text-muted);font-size:13px;text-align:center;padding:20px;">لا توجد إنجازات بعد — ستظهر هنا تلقائياً عند فوز فريق بالبطولة.</div>';
    return;
  }
  el.innerHTML = [...achievements].reverse().map(a => `
    <div style="background:var(--surface2);border:1px solid var(--border);border-radius:12px;padding:14px;margin-bottom:10px;display:flex;align-items:center;gap:14px;">
      <div style="font-size:32px;">${a.icon}</div>
      <div style="flex:1;">
        <div style="font-size:13px;font-weight:700;color:${a.type==='baloot'?'var(--gold)':'var(--teal)'};">${a.title}</div>
        <div style="font-size:12px;color:var(--text-muted);margin-top:2px;">${a.names.join(' • ')}</div>
        <div style="font-size:10px;color:var(--text-muted);margin-top:4px;">فريق: ${a.teamName} • ${a.date}</div>
      </div>
    </div>
  `).join('');
}

function showVbStandings() {
  const sc = document.getElementById('vb-standings-container');
  if (sc.style.display === 'block') { sc.style.display = 'none'; return; }
  const sorted = [...vbTeams].sort((a, b) => (b.wins || 0) - (a.wins || 0));
  sc.innerHTML = `<div class="card">
    <div class="card-header"><span class="card-title">📊 ترتيب فرق الطائرة</span></div>
    <table class="standings-table">
      <thead><tr><th>#</th><th>الفريق</th><th>لاعبون</th><th>انتصارات</th><th>خسائر</th></tr></thead>
      <tbody>${sorted.map((t, i) => `<tr>
        <td class="pos-num" style="color:var(--teal)">${i+1}</td>
        <td>${t.name}</td>
        <td style="color:var(--teal)">${t.playerIds.length}</td>
        <td style="color:var(--green)">${t.wins || 0}</td>
        <td style="color:var(--red)">${t.losses || 0}</td>
      </tr>`).join('')}</tbody>
    </table>
  </div>`;
  sc.style.display = 'block';
}

// =====================
// DASHBOARD
// =====================
function updateDashboard() {
  document.getElementById('stat-total').textContent = participantsData.length;
  document.getElementById('stat-teams').textContent = teams.length;
  document.getElementById('stat-vb-teams').textContent = vbTeams.length;
  document.getElementById('stat-vb-players').textContent = vbPlayers.length;
}

// =====================
// RELIGION
// =====================
function showDailyReminder() {
  const el = document.getElementById('daily-reminder');
  if (el) el.textContent = dailyReminders[dailyReminderIndex];
}

function rotateDailyReminder() {
  dailyReminderIndex = (dailyReminderIndex + 1) % dailyReminders.length;
  showDailyReminder();
}

// =====================
// UTILITIES
// =====================
function closeModal(id) {
  document.getElementById(id).classList.remove('open');
}

function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 3000);
}

document.querySelectorAll('.modal-overlay').forEach(o => {
  o.addEventListener('click', e => { if (e.target === o) o.classList.remove('open'); });
});

// =====================
// 🎤 MICROPHONE ACTIVITY
// =====================
let micQueue    = [];   // remaining participants
let micDone     = [];   // already spoke
let micCurrent  = null;
let micTimerInterval = null;
let micSecondsLeft   = 60;
let micRunning  = false;
let micInitialized = false;

function initMicPage() {
  if (!micInitialized) {
    micQueue = [...participantsData].sort(() => Math.random() - 0.5);
    micDone  = [];
    micInitialized = true;
  }
  updateMicTopic();
  renderMicQueues();
}

function updateMicTopic() {
  const sel = document.getElementById('mic-topic');
  const display = document.getElementById('mic-topic-display');
  if (sel && display) {
    display.textContent = sel.value !== 'حر' ? `📌 الموضوع: "${sel.options[sel.selectedIndex].text.replace(/.*—\s*/,'')}"` : '';
  }
}

function drawMicName() {
  if (micQueue.length === 0) {
    showToast('🎉 تحدّث الجميع! يمكنك إعادة التعيين');
    return;
  }
  // Stop any running timer
  if (micRunning) stopMicTimer();

  micCurrent = micQueue.shift();

  // Animate name display
  const nameEl = document.getElementById('mic-current-name');
  const subEl  = document.getElementById('mic-current-sub');
  const iconEl = document.getElementById('mic-icon-display');

  nameEl.style.opacity = '0';
  nameEl.style.transform = 'scale(0.8)';
  setTimeout(() => {
    nameEl.textContent = micCurrent.name;
    nameEl.style.opacity = '1';
    nameEl.style.transform = 'scale(1)';
    nameEl.style.transition = 'all 0.35s cubic-bezier(0.34,1.56,0.64,1)';
    iconEl.textContent = '🎤';
    iconEl.style.transform = 'scale(1.2)';
    setTimeout(() => iconEl.style.transform = 'scale(1)', 300);

    const topic = document.getElementById('mic-topic')?.value;
    const topicText = topic && topic !== 'حر'
      ? document.getElementById('mic-topic')?.options[document.getElementById('mic-topic').selectedIndex]?.text?.replace(/.*—\s*/,'')
      : 'قل أي شيء يخطر ببالك!';
    subEl.textContent = `📌 ${topicText}`;
  }, 150);

  // Reset timer display
  const dur = parseInt(document.getElementById('mic-duration')?.value || 60);
  micSecondsLeft = dur;
  const timerEl = document.getElementById('mic-timer-display');
  timerEl.style.display = 'block';
  timerEl.textContent = formatMicTime(dur);
  timerEl.style.color = 'var(--purple)';

  const btn = document.getElementById('mic-timer-btn');
  btn.textContent = '⏱️ ابدأ العداد';
  btn.style.background = 'var(--green)';

  renderMicQueues();
}

function toggleMicTimer() {
  if (!micCurrent) { showToast('⚠️ اسحب اسماً أولاً'); return; }
  if (micRunning) {
    stopMicTimer();
  } else {
    startMicTimer();
  }
}

function startMicTimer() {
  micRunning = true;
  const btn = document.getElementById('mic-timer-btn');
  btn.textContent = '⏸️ إيقاف مؤقت';
  btn.style.background = 'var(--gold)';
  btn.style.color = '#000';

  micTimerInterval = setInterval(() => {
    micSecondsLeft--;
    const timerEl = document.getElementById('mic-timer-display');
    timerEl.textContent = formatMicTime(micSecondsLeft);

    // Color changes as time runs out
    if (micSecondsLeft <= 10) {
      timerEl.style.color = 'var(--red)';
      timerEl.style.animation = 'pulse 0.6s infinite';
    } else if (micSecondsLeft <= 20) {
      timerEl.style.color = '#f59e0b';
    }

    if (micSecondsLeft <= 0) {
      stopMicTimer();
      timerEl.textContent = '⏰ انتهى الوقت!';
      timerEl.style.color = 'var(--red)';
      showToast(`✅ انتهى وقت ${micCurrent.name}`);
      // Move to done
      if (micCurrent && !micDone.find(p => p.id === micCurrent.id)) {
        micDone.push(micCurrent);
        micCurrent = null;
        renderMicQueues();
      }
    }
  }, 1000);
}

function stopMicTimer() {
  micRunning = false;
  clearInterval(micTimerInterval);
  const btn = document.getElementById('mic-timer-btn');
  btn.textContent = '▶️ استئناف';
  btn.style.background = 'var(--green)';
  btn.style.color = '#000';
}

function formatMicTime(s) {
  const m = Math.floor(s / 60);
  const sec = s % 60;
  return `${m}:${sec.toString().padStart(2,'0')}`;
}

function resetMicSession() {
  if (!confirm('إعادة تعيين الجلسة؟ ستعود كل الأسماء لقائمة الانتظار.')) return;
  stopMicTimer();
  micCurrent = null;
  micInitialized = false;
  initMicPage();
  // Reset stage
  document.getElementById('mic-current-name').textContent = 'اضغط "اسحب اسماً"';
  document.getElementById('mic-current-sub').textContent = 'سيظهر هنا اسم المشارك الذي سيتحدث';
  document.getElementById('mic-timer-display').style.display = 'none';
  document.getElementById('mic-icon-display').textContent = '🎤';
  document.getElementById('mic-timer-btn').textContent = '⏱️ ابدأ العداد';
  document.getElementById('mic-timer-btn').style.background = 'var(--green)';
  showToast('🔄 تمت إعادة التعيين');
}

function markMicDone() {
  if (!micCurrent) return;
  stopMicTimer();
  if (!micDone.find(p => p.id === micCurrent.id)) micDone.push(micCurrent);
  micCurrent = null;
  document.getElementById('mic-current-name').textContent = 'اضغط "اسحب اسماً"';
  document.getElementById('mic-timer-display').style.display = 'none';
  renderMicQueues();
  showToast('✅ تم تسجيل المشارك');
}

function renderMicQueues() {
  // Queue list
  const qEl = document.getElementById('mic-queue-list');
  const remaining = micQueue.length;
  const countEl = document.getElementById('mic-remaining-count');
  if (countEl) countEl.textContent = remaining + ' متبقي';

  if (remaining === 0) {
    qEl.innerHTML = '<div style="color:var(--text-muted);font-size:12px;text-align:center;padding:20px;">🎉 تحدّث الجميع!</div>';
  } else {
    qEl.innerHTML = micQueue.map((p, i) => `
      <div style="display:flex;align-items:center;gap:8px;padding:7px 0;border-bottom:1px solid rgba(42,48,72,0.5);">
        <div style="width:22px;height:22px;border-radius:6px;background:rgba(168,85,247,0.15);color:var(--purple);font-size:11px;font-weight:900;display:flex;align-items:center;justify-content:center;flex-shrink:0;">${i+1}</div>
        <span style="font-size:12px;flex:1;">${p.name}</span>
        <button onclick="skipToMic(${p.id})" style="background:none;border:1px solid rgba(168,85,247,0.3);color:var(--purple);border-radius:6px;padding:2px 6px;font-size:10px;cursor:pointer;">اختر</button>
      </div>
    `).join('');
  }

  // Done list
  const dEl = document.getElementById('mic-done-list');
  const dCount = document.getElementById('mic-done-count');
  if (dCount) dCount.textContent = micDone.length;

  if (micDone.length === 0) {
    dEl.innerHTML = '<div style="color:var(--text-muted);font-size:12px;text-align:center;padding:20px;">لم يتحدث أحد بعد</div>';
  } else {
    dEl.innerHTML = [...micDone].reverse().map((p, i) => `
      <div style="display:flex;align-items:center;gap:8px;padding:7px 0;border-bottom:1px solid rgba(42,48,72,0.5);">
        <div style="font-size:14px;">✅</div>
        <span style="font-size:12px;flex:1;color:var(--text-muted);">${p.name}</span>
        <span style="font-size:10px;color:var(--green);">تحدّث</span>
      </div>
    `).join('');
  }
}

function skipToMic(pid) {
  // Move this person to front of queue then draw
  const idx = micQueue.findIndex(p => p.id === pid);
  if (idx > -1) {
    const [p] = micQueue.splice(idx, 1);
    micQueue.unshift(p);
    drawMicName();
  }
}

// =====================
// SPEAKER MODE (full-screen black stage)
// =====================
function startSpeakerMode(name, topic, color, isClergy) {
  const overlay = document.getElementById('speaker-mode-overlay');
  const nameEl  = document.getElementById('speaker-name');
  const topicEl = document.getElementById('speaker-topic');
  const iconEl  = document.getElementById('speaker-mic-icon');

  const colorMap = { blue: '#3b82f6', green: '#22c55e', gold: '#c9a84c', teal: '#14b8a6', purple: '#a855f7' };
  const c = colorMap[color] || '#fff';

  nameEl.textContent = name;
  nameEl.style.color = c;
  topicEl.textContent = topic || '';
  iconEl.textContent = isClergy ? '🕌' : '🎤';

  overlay.style.display = 'flex';
  overlay.style.opacity = '0';
  requestAnimationFrame(() => {
    overlay.style.transition = 'opacity 0.4s';
    overlay.style.opacity = '1';
  });
}

function exitSpeakerMode() {
  const overlay = document.getElementById('speaker-mode-overlay');
  overlay.style.opacity = '0';
  setTimeout(() => overlay.style.display = 'none', 300);
}

// =====================
// FAMILY TREE
// =====================
function openFamilyTree() {
  window.open('https://livefamilytrees.com/trees/?t=2501139gL6', '_blank', 'noopener,noreferrer');
}

// =====================
// LOGIN & ROLES
// =====================
let currentRole = null; // 'admin' | 'viewer'

const USERS = [
  { username: 'sayyaf', password: 'sayyaf@11', role: 'admin',  label: 'مدير النظام' },
  { username: 'user',   password: '1111',       role: 'viewer', label: 'مشاهد'       },
];

function doLogin() {
  const username = document.getElementById('login-user').value.trim();
  const password = document.getElementById('login-pass').value;
  const err      = document.getElementById('login-error');

  const matched = USERS.find(u => u.username === username && u.password === password);

  if (matched) {
    currentRole = matched.role;
    err.classList.remove('show');
    const overlay = document.getElementById('login-overlay');
    overlay.style.transition = 'opacity 0.4s';
    overlay.style.opacity = '0';
    setTimeout(() => {
      overlay.style.display = 'none';
      applyRoleRestrictions();
      showUserBadge(matched.label);
    }, 400);
  } else {
    err.classList.add('show');
    document.getElementById('login-pass').value = '';
    document.getElementById('login-pass').focus();
  }
}

function applyRoleRestrictions() {
  if (currentRole !== 'viewer') return;

  // 1. Hide ALL sidebar nav items except "الفعاليات" (meetings) and "شجرة النسب" (familytree)
  const allowedPages = ['meetings', 'familytree'];
  document.querySelectorAll('.nav-item').forEach(btn => {
    const onclick = btn.getAttribute('onclick') || '';
    const isAllowed = allowedPages.some(p => onclick.includes("'" + p + "'"));
    if (!isAllowed) btn.style.display = 'none';
  });

  // 2. Hide nav section labels (البلوت / الطائرة headers) since their pages are hidden
  document.querySelectorAll('.nav-section-label').forEach(label => {
    if (label.textContent.trim() !== '') label.style.display = 'none';
  });

  // 3. Force landing on the meetings page (not dashboard) for viewer
  showPage('meetings');

  // 4. Inside the meetings page: hide every action/edit button (start segment, draw, tournament links, speaker mode triggers)
  document.querySelectorAll('#page-meetings button').forEach(btn => btn.style.display = 'none');

  // 5. Block all write/navigation-to-edit functions — show toast instead
  const blocked = [
    'openAddBalootPlayerModal','autoGenerateBalootTeams','openManualTeamModal',
    'resetBalootTeams','runDraw','generateBracket','openScoreModal','saveScore',
    'openAddVbPlayerModal','addVbPlayer','openAddVbTeamModal','saveVbTeam',
    'generateVbBracket','openVbScoreModal','saveVbScore',
    'openAddModal','addParticipant','deleteParticipant','editParticipant',
    'openAddTeamModal','startSpeakerMode','drawMicName','toggleMicTimer',
    'resetMicSession','markMicDone','skipToMic',
  ];
  blocked.forEach(fn => {
    window[fn] = function() { showViewerToast(); };
  });

  // 6. Lock down showPage so viewer can only ever land on allowed pages
  const originalShowPage = showPage;
  window.showPage = function(page) {
    if (allowedPages.includes(page)) {
      originalShowPage(page);
      if (page === 'meetings') {
        document.querySelectorAll('#page-meetings button').forEach(btn => btn.style.display = 'none');
      }
    } else {
      showViewerToast();
    }
  };
}

function showViewerToast() {
  const t = document.getElementById('toast');
  t.textContent = '🔒 صلاحية المشاهدة فقط — لا يمكن التعديل';
  t.style.borderColor = 'var(--red)';
  t.style.color = 'var(--red)';
  t.classList.add('show');
  setTimeout(() => {
    t.classList.remove('show');
    t.style.borderColor = '';
    t.style.color = '';
  }, 3000);
}

function showUserBadge(label) {
  const footer = document.querySelector('.sidebar-footer');
  if (!footer) return;
  const roleColor = currentRole === 'admin' ? 'var(--gold)' : 'var(--blue)';
  const roleIcon  = currentRole === 'admin' ? '👑' : '👁️';
  footer.innerHTML = `
    <div style="text-align:center;">
      <div style="font-size:12px;font-weight:700;color:${roleColor};margin-bottom:4px;">${roleIcon} ${label}</div>
      <div style="font-size:10px;color:var(--text-muted);">© 2026 سياف المقبلي</div>
      <div style="font-size:9px;color:var(--gold-light);margin-top:6px;font-weight:700;line-height:1.6;">
        ✦ تصميم وبرمجة بالكامل ✦<br>
        <span style="font-size:11px;color:var(--gold);">سياف فهد اليزيدي</span><br>
        <span style="font-size:8px;color:var(--text-muted);font-weight:400;">بكل حب وعناية لأجل عائلتنا 💛🌳</span>
      </div>
      <button onclick="doLogout()" style="margin-top:8px;background:rgba(239,68,68,0.1);border:1px solid rgba(239,68,68,0.3);color:var(--red);border-radius:8px;padding:5px 14px;font-family:'Tajawal',sans-serif;font-size:11px;cursor:pointer;width:100%;">تسجيل الخروج</button>
    </div>
  `;
}

function doLogout() {
  currentRole = null;
  // Reload page to reset everything
  location.reload();
}

function toggleLoginPass() {
  const f = document.getElementById('login-pass');
  f.type = f.type === 'password' ? 'text' : 'password';
}

// Init
updateDashboard();
showDailyReminder();
</script>
</body>
</html>
