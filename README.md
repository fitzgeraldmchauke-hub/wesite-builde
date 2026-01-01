<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Password Security</title>
<style>
  body {
    font-family: sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background: #f2f2f2;
    margin: 0;
  }
  .container {
    background: white;
    padding: 30px;
    border-radius: 12px;
    box-shadow: 0 4px 15px rgba(0,0,0,0.1);
    width: 350px;
    text-align: center;
  }
  .container h1 {
    font-size: 24px;
    margin-bottom: 20px;
  }
  .password-wrapper {
    position: relative;
  }
  .container input {
    width: 100%;
    padding: 12px 40px 12px 12px;
    border-radius: 6px;
    border: 1px solid #ccc;
    font-size: 16px;
    box-sizing: border-box;
  }
  .toggle {
    position: absolute;
    right: 12px;
    top: 50%;
    transform: translateY(-50%);
    cursor: pointer;
    color: #555;
    font-weight: bold;
    user-select: none;
  }
  #result {
    font-weight: bold;
    margin-top: 10px;
  }
  .strength-bar {
    height: 8px;
    background: #eee;
    border-radius: 4px;
    margin-top: 12px;
    overflow: hidden;
  }
  .strength-fill {
    height: 100%;
    width: 0%;
    background: green;
    border-radius: 4px;
    transition: width 0.3s, background 0.3s;
  }
</style>
</head>
<body>
<div class="container">
  <h1>🔒 Password Security</h1>
  <div class="password-wrapper">
    <input type="password" id="password" placeholder="Enter password" oninput="check()">
    <span class="toggle" onclick="togglePassword()">Show</span>
  </div>
  <div class="strength-bar">
    <div id="strength-fill" class="strength-fill"></div>
  </div>
  <div id="result">⌨️ Type a password first</div>
</div>
<script>
function togglePassword() {
  const input = document.getElementById("password");
  const toggle = document.querySelector(".toggle");
  if (input.type === "password") {
    input.type = "text";
    toggle.textContent = "Hide";
  } else {
    input.type = "password";
    toggle.textContent = "Show";
  }
}

function check() {
  const password = document.getElementById("password").value;
  let score = 0;

  if (/[A-Z]/.test(password)) score++;
  if (/[a-z]/.test(password)) score++;
  if (/[0-9]/.test(password)) score++;
  if (/[^A-Za-z0-9]/.test(password)) score++;

  const result = document.getElementById("result");
  const fill = document.getElementById("strength-fill");

  const percent = (score / 4) * 100;
  fill.style.width = percent + "%";

  if (score <= 1) {
    result.textContent = "❌ Weak password";
    result.style.color = "red";
    fill.style.background = "red";
  } else if (score === 2 || score === 3) {
    result.textContent = "⚠️ Medium password";
    result.style.color = "orange";
    fill.style.background = "orange";
  } else {
    result.textContent = "✅ Strong password";
    result.style.color = "green";
    fill.style.background = "green";
  }

  if (password.length === 0) {
    result.textContent = "⌨️ Type a password first";
    result.style.color = "black";
    fill.style.width = "0%";
  }
}
</script>
</body>
</html>
