<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>AKR Win — Admin Panel</title>

  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: Inter, Arial, sans-serif;
    }

    :root {
      --bg: #f4f7fb;
      --card: #ffffff;
      --text: #172033;
      --muted: #7a8498;
      --primary: #5b5cf0;
      --primary-dark: #4546cf;
      --green: #16a673;
      --red: #e54d5f;
      --orange: #f39c38;
      --border: #e7eaf0;
      --sidebar: #15182b;
    }

    body {
      background: var(--bg);
      color: var(--text);
      min-height: 100vh;
    }

    button,
    input,
    select {
      font: inherit;
    }

    .app {
      display: flex;
      min-height: 100vh;
    }

    /* SIDEBAR */
    .sidebar {
      width: 250px;
      background: var(--sidebar);
      color: white;
      padding: 22px 15px;
      position: fixed;
      inset: 0 auto 0 0;
      z-index: 100;
      transition: .3s;
    }

    .brand {
      display: flex;
      align-items: center;
      gap: 12px;
      padding: 8px 12px 28px;
    }

    .brand-logo {
      width: 42px;
      height: 42px;
      border-radius: 12px;
      display: grid;
      place-items: center;
      background: linear-gradient(135deg, #6b6df7, #3839c8);
      font-weight: 800;
    }

    .brand h2 {
      font-size: 20px;
    }

    .brand span {
      display: block;
      color: #949ab6;
      font-size: 11px;
      margin-top: 3px;
    }

    .nav-title {
      color: #707792;
      font-size: 11px;
      text-transform: uppercase;
      margin: 15px 12px 8px;
      letter-spacing: 1px;
    }

    .nav-item {
      width: 100%;
      border: 0;
      background: transparent;
      color: #bfc4d8;
      padding: 13px 14px;
      margin-bottom: 4px;
      border-radius: 9px;
      display: flex;
      align-items: center;
      gap: 12px;
      cursor: pointer;
      text-align: left;
      transition: .2s;
    }

    .nav-item:hover,
    .nav-item.active {
      color: white;
      background: #292d4b;
    }

    .nav-icon {
      width: 22px;
      text-align: center;
    }

    /* MAIN */
    .main {
      margin-left: 250px;
      width: calc(100% - 250px);
    }

    .topbar {
      height: 72px;
      background: white;
      border-bottom: 1px solid var(--border);
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0 28px;
      position: sticky;
      top: 0;
      z-index: 50;
    }

    .menu-btn {
      display: none;
      border: 0;
      background: transparent;
      font-size: 25px;
      cursor: pointer;
    }

    .topbar-left h3 {
      font-size: 19px;
    }

    .topbar-left p {
      color: var(--muted);
      font-size: 12px;
      margin-top: 3px;
    }

    .admin-profile {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .avatar {
      width: 39px;
      height: 39px;
      background: #e7e8ff;
      color: var(--primary);
      border-radius: 50%;
      display: grid;
      place-items: center;
      font-weight: 700;
    }

    .admin-profile small {
      display: block;
      color: var(--muted);
      font-size: 11px;
    }

    /* CONTENT */
    .content {
      padding: 26px;
    }

    .page-title {
      margin-bottom: 22px;
    }

    .page-title h1 {
      font-size: 25px;
    }

    .page-title p {
      color: var(--muted);
      margin-top: 5px;
      font-size: 13px;
    }

    /* STATS */
    .stats {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 18px;
      margin-bottom: 22px;
    }

    .stat-card {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 14px;
      padding: 20px;
      box-shadow: 0 3px 15px rgba(30, 35, 60, .03);
    }

    .stat-top {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .stat-icon {
      width: 43px;
      height: 43px;
      border-radius: 11px;
      display: grid;
      place-items: center;
      font-size: 20px;
      background: #eeefff;
    }

    .stat-label {
      color: var(--muted);
      font-size: 13px;
    }

    .stat-value {
      font-size: 27px;
      font-weight: 750;
      margin-top: 13px;
    }

    .stat-change {
      font-size: 11px;
      margin-top: 7px;
    }

    .positive {
      color: var(--green);
    }

    .negative {
      color: var(--red);
    }

    /* GRID */
    .dashboard-grid {
      display: grid;
      grid-template-columns: 2fr 1fr;
      gap: 20px;
      margin-bottom: 22px;
    }

    .card {
      background: white;
      border: 1px solid var(--border);
      border-radius: 14px;
      padding: 20px;
      box-shadow: 0 3px 15px rgba(30, 35, 60, .03);
    }

    .card-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 18px;
    }

    .card-header h3 {
      font-size: 16px;
    }

    .card-header span {
      color: var(--muted);
      font-size: 12px;
    }

    /* CHART */
    .chart {
      height: 260px;
      display: flex;
      align-items: flex-end;
      gap: 12px;
      padding: 15px 5px 0;
      border-bottom: 1px solid var(--border);
    }

    .bar-wrap {
      flex: 1;
      height: 100%;
      display: flex;
      flex-direction: column;
      justify-content: flex-end;
      align-items: center;
      gap: 8px;
    }

    .bar {
      width: 65%;
      min-height: 10px;
      background: linear-gradient(to top, var(--primary), #8586ff);
      border-radius: 7px 7px 0 0;
      transition: .4s;
    }

    .bar:hover {
      opacity: .8;
      transform: scaleY(1.03);
    }

    .bar-wrap small {
      color: var(--muted);
      font-size: 10px;
    }

    /* ACTIVITY */
    .activity {
      display: flex;
      flex-direction: column;
      gap: 14px;
    }

    .activity-item {
      display: flex;
      gap: 12px;
      align-items: center;
    }

    .activity-icon {
      width: 36px;
      height: 36px;
      border-radius: 10px;
      background: #f0f1ff;
      display: grid;
      place-items: center;
    }

    .activity-info {
      flex: 1;
    }

    .activity-info strong {
      display: block;
      font-size: 12px;
    }

    .activity-info small {
      color: var(--muted);
      font-size: 11px;
    }

    /* TABLE */
    .table-card {
      overflow: hidden;
    }

    .table-tools {
      display: flex;
      gap: 10px;
      margin-bottom: 17px;
    }

    .search {
      flex: 1;
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 10px 12px;
      outline: none;
    }

    .filter {
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 10px;
      background: white;
      outline: none;
    }

    .table-container {
      overflow-x: auto;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      min-width: 700px;
    }

    th,
    td {
      text-align: left;
      padding: 14px 12px;
      border-bottom: 1px solid var(--border);
      font-size: 12px;
    }

    th {
      color: var(--muted);
      font-size: 11px;
      font-weight: 600;
      text-transform: uppercase;
    }

    .badge {
      display: inline-block;
      padding: 5px 9px;
      border-radius: 20px;
      font-size: 10px;
      font-weight: 600;
    }

    .badge.green {
      color: #087b53;
      background: #e6f8f1;
    }

    .badge.orange {
      color: #a96209;
      background: #fff2dd;
    }

    .badge.red {
      color: #b52e40;
      background: #fde9ed;
    }

    .badge.blue {
      color: #4045b9;
      background: #ebebff;
    }

    /* ROUND CARDS */
    .rounds {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 15px;
    }

    .round-card {
      border: 1px solid var(--border);
      padding: 17px;
      border-radius: 12px;
    }

    .round-head {
      display: flex;
      justify-content: space-between;
      margin-bottom: 14px;
    }

    .round-id {
      font-weight: 700;
      font-size: 13px;
    }

    .round-time {
      color: var(--muted);
      font-size: 11px;
    }

    .progress {
      height: 7px;
      background: #eceef4;
      border-radius: 10px;
      overflow: hidden;
      margin: 10px 0;
    }

    .progress div {
      height: 100%;
      background: var(--primary);
      border-radius: inherit;
    }

    .round-meta {
      display: flex;
      justify-content: space-between;
      color: var(--muted);
      font-size: 11px;
    }

    /* SECTIONS */
    .section {
      display: none;
    }

    .section.active {
      display: block;
    }

    .empty {
      padding: 50px 20px;
      text-align: center;
      color: var(--muted);
    }

    /* TOAST */
    .toast {
      position: fixed;
      right: 22px;
      bottom: 22px;
      background: #1c2033;
      color: white;
      padding: 13px 17px;
      border-radius: 9px;
      font-size: 12px;
      opacity: 0;
      transform: translateY(20px);
      pointer-events: none;
      transition: .3s;
      z-index: 999;
    }

    .toast.show {
      opacity: 1;
      transform: translateY(0);
    }

    /* RESPONSIVE */
    @media (max-width: 1100px) {
      .stats {
        grid-template-columns: repeat(2, 1fr);
      }

      .dashboard-grid {
        grid-template-columns: 1fr;
      }

      .rounds {
        grid-template-columns: 1fr;
      }
    }

    @media (max-width: 760px) {
      .sidebar {
        transform: translateX(-100%);
      }

      .sidebar.open {
        transform: translateX(0);
      }

      .main {
        margin-left: 0;
        width: 100%;
      }

      .menu-btn {
        display: block;
      }

      .topbar {
        padding: 0 16px;
      }

      .content {
        padding: 16px;
      }

      .stats {
        grid-template-columns: 1fr;
      }

      .admin-profile > div:last-child {
        display: none;
      }
    }
  </style>
</head>

<body>

<div class="app">

  <!-- SIDEBAR -->
  <aside class="sidebar" id="sidebar">

    <div class="brand">
      <div class="brand-logo">AK</div>
      <div>
        <h2>AKR Win</h2>
        <span>ADMIN CONTROL PANEL</span>
      </div>
    </div>

    <div class="nav-title">Management</div>

    <button class="nav-item active" data-section="dashboard">
      <span class="nav-icon">▦</span>
      Dashboard
    </button>

    <button class="nav-item" data-section="users">
      <span class="nav-icon">♙</span>
      Users
    </button>

    <button class="nav-item" data-section="bets">
      <span class="nav-icon">◎</span>
      Bets
    </button>

    <button class="nav-item" data-section="rounds">
      <span class="nav-icon">◷</span>
      Game Rounds
    </button>

    <div class="nav-title">Finance</div>

    <button class="nav-item" data-section="transactions">
      <span class="nav-icon">₹</span>
      Transactions
    </button>

    <button class="nav-item" data-section="reports">
      <span class="nav-icon">▥</span>
      Reports
    </button>

    <div class="nav-title">System</div>

    <button class="nav-item" data-section="settings">
      <span class="nav-icon">⚙</span>
      Settings
    </button>

  </aside>

  <!-- MAIN -->
  <main class="main">

    <header class="topbar">

      <div class="topbar-left">
        <button class="menu-btn" id="menuBtn">☰</button>
        <h3 id="topTitle">Dashboard</h3>
        <p>AKR Win administration</p>
      </div>

      <div class="admin-profile">
        <div class="avatar">A</div>
        <div>
          <strong>Administrator</strong>
          <small>Super Admin</small>
        </div>
      </div>

    </header>

    <div class="content">

      <!-- DASHBOARD -->
      <section class="section active" id="dashboard">

        <div class="page-title">
          <h1>Dashboard Overview</h1>
          <p>Monitor your platform activity and financial statistics.</p>
        </div>

        <div class="stats">

          <div class="stat-card">
            <div class="stat-top">
              <span class="stat-label">Total Users</span>
              <div class="stat-icon">👥</div>
            </div>
            <div class="stat-value" id="totalUsers">12,480</div>
            <div class="stat-change positive">↑ 8.4% this month</div>
          </div>

          <div class="stat-card">
            <div class="stat-top">
              <span class="stat-label">Total Bets</span>
              <div class="stat-icon">🎯</div>
            </div>
            <div class="stat-value" id="totalBets">84,621</div>
            <div class="stat-change positive">↑ 12.7% this month</div>
          </div>

          <div class="stat-card">
            <div class="stat-top">
              <span class="stat-label">Revenue</span>
              <div class="stat-icon">₹</div>
            </div>
            <div class="stat-value" id="revenue">₹8,42,610</div>
            <div class="stat-change positive">↑ 6.2% this month</div>
          </div>

          <div class="stat-card">
            <div class="stat-top">
              <span class="stat-label">Active Rounds</span>
              <div class="stat-icon">◷</div>
            </div>
            <div class="stat-value" id="activeRounds">3</div>
            <div class="stat-change">Currently running</div>
          </div>

        </div>

        <div class="dashboard-grid">

          <!-- CHART -->
          <div class="card">
            <div class="card-header">
              <h3>Bet Activity</h3>
              <span>Last 7 days</span>
            </div>

            <div class="chart">

              <div class="bar-wrap">
                <div class="bar" style="height:45%"></div>
                <small>Mon</small>
              </div>

              <div class="bar-wrap">
                <div class="bar" style="height:62%"></div>
                <small>Tue</small>
              </div>

              <div class="bar-wrap">
                <div class="bar" style="height:51%"></div>
                <small>Wed</small>
              </div>

              <div class="bar-wrap">
                <div class="bar" style="height:78%"></div>
                <small>Thu</small>
              </div>

              <div class="bar-wrap">
                <div class="bar" style="height:69%"></div>
                <small>Fri</small>
              </div>

              <div class="bar-wrap">
                <div class="bar" style="height:91%"></div>
                <small>Sat</small>
              </div>

              <div class="bar-wrap">
                <div class="bar" style="height:82%"></div>
                <small>Sun</small>
              </div>

            </div>
          </div>

          <!-- ACTIVITY -->
          <div class="card">

            <div class="card-header">
              <h3>Recent Activity</h3>
              <span>Live</span>
            </div>

            <div class="activity">

              <div class="activity-item">
                <div class="activity-icon">👤</div>
                <div class="activity-info">
                  <strong>New user registered</strong>
                  <small>2 minutes ago</small>
                </div>
              </div>

              <div class="activity-item">
                <div class="activity-icon">₹</div>
                <div class="activity-info">
                  <strong>Deposit recorded</strong>
                  <small>7 minutes ago</small>
                </div>
              </div>

              <div class="activity-item">
                <div class="activity-icon">🎯</div>
                <div class="activity-info">
                  <strong>Bet recorded</strong>
                  <small>11 minutes ago</small>
                </div>
              </div>

              <div class="activity-item">
                <div class="activity-icon">✓</div>
                <div class="activity-info">
                  <strong>Withdrawal processed</strong>
                  <small>18 minutes ago</small>
                </div>
              </div>

              <div class="activity-item">
                <div class="activity-icon">◷</div>
                <div class="activity-info">
                  <strong>New round opened</strong>
                  <small>23 minutes ago</small>
                </div>
              </div>

            </div>

          </div>

        </div>

        <!-- ACTIVE ROUNDS -->
        <div class="card" style="margin-bottom:22px">

          <div class="card-header">
            <h3>Active Game Rounds</h3>
            <span>3 active</span>
          </div>

          <div class="rounds">

            <div class="round-card">
              <div class="round-head">
                <span class="round-id">ROUND #10281</span>
                <span class="badge green">OPEN</span>
              </div>
              <div class="round-time">Closes in 00:38</div>
              <div class="progress">
                <div style="width:72%"></div>
              </div>
              <div class="round-meta">
                <span>1,248 bets</span>
                <span>₹84,620</span>
              </div>
            </div>

            <div class="round-card">
              <div class="round-head">
                <span class="round-id">ROUND #10282</span>
                <span class="badge green">OPEN</span>
              </div>
              <div class="round-time">Closes in 01:38</div>
              <div class="progress">
                <div style="width:46%"></div>
              </div>
              <div class="round-meta">
                <span>628 bets</span>
                <span>₹41,280</span>
              </div>
            </div>

            <div class="round-card">
              <div class="round-head">
                <span class="round-id">ROUND #10283</span>
                <span class="badge orange">UPCOMING</span>
              </div>
              <div class="round-time">Starts in 02:38</div>
              <div class="progress">
                <div style="width:15%"></div>
              </div>
              <div class="round-meta">
                <span>0 bets</span>
                <span>₹0</span>
              </div>
            </div>

          </div>
        </div>

        <!-- RECENT BETS -->
        <div class="card table-card">

          <div class="card-header">
            <h3>Recent Bets</h3>
            <span>Latest activity</span>
          </div>

          <div class="table-container">

            <table>
              <thead>
                <tr>
                  <th>Bet ID</th>
                  <th>User</th>
                  <th>Type</th>
                  <th>Amount</th>
                  <th>Round</th>
                  <th>Status</th>
                </tr>
              </thead>

              <tbody>
                <tr>
                  <td>#BET98231</td>
                  <td>Rahul K.</td>
                  <td><span class="badge blue">Color</span></td>
                  <td>₹500</td>
                  <td>#10281</td>
                  <td><span class="badge green">Recorded</span></td>
                </tr>

                <tr>
                  <td>#BET98230</td>
                  <td>Priya S.</td>
                  <td><span class="badge blue">Number</span></td>
                  <td>₹250</td>
                  <td>#10281</td>
                  <td><span class="badge green">Recorded</span></td>
                </tr>

                <tr>
                  <td>#BET98229</td>
                  <td>Arjun P.</td>
                  <td><span class="badge blue">Big-Small</span></td>
                  <td>₹1,000</td>
                  <td>#10281</td>
                  <td><span class="badge green">Recorded</span></td>
                </tr>

              </tbody>
            </table>

          </div>

        </div>

      </section>

      <!-- USERS -->
