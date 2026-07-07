<!DOCTYPE html>
<html>
<head>
  <title>Thanks for your interest!</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 80px 20px;
      background: #F9F9F9;
    }
    .card {
      background: white;
      border-radius: 12px;
      padding: 48px 40px;
      max-width: 480px;
      margin: 0 auto;
      box-shadow: 0 2px 12px rgba(0,0,0,0.08);
    }
    h2 {
      color: #111;
      font-size: 24px;
      margin-bottom: 12px;
    }
    p {
      color: #555;
      font-size: 16px;
      line-height: 1.5;
    }
    .spinner {
      display: inline-block;
      width: 32px;
      height: 32px;
      border: 3px solid #E0E0E0;
      border-top-color: #2563EB;
      border-radius: 50%;
      animation: spin 0.8s linear infinite;
      margin-bottom: 16px;
    }
    @keyframes spin {
      to { transform: rotate(360deg); }
    }
  </style>
</head>

<body>

<div class="card">

<div id="loading">
<div class="spinner"></div>
<h2>Confirming your interest...</h2>
</div>

<div id="success" style="display:none;">
<h2>You're all set!</h2>
<p>Thanks for your interest — we'll be in touch shortly.</p>
</div>

<div id="error" style="display:none;">
<h2>Something went wrong</h2>
<p>Please try clicking the link in your email again.</p>
</div>

</div>

<script>

window.addEventListener('load', async () => {

const params = new URLSearchParams(window.location.search);

const email = params.get('email');

if (!email) {
  console.log("No email found in URL.");
  document.getElementById('loading').style.display = 'none';
  document.getElementById('error').style.display = 'block';
  return;
}

try {

await fetch('https://script.google.com/macros/s/AKfycbzyq-A3wlCWxnRw5GyvVPTgvwW5A7gEEtipL04CNOpYqQrcoz3eCBIQFMc2fRttBNUNoQ/exec', {

method: 'POST',

headers: {
'Content-Type': 'application/json'
},

body: JSON.stringify({

email: email,
name: params.get('name'),
title: params.get('title'),
company: params.get('company'),
source: 'apollo outbound'

})

});

document.getElementById('loading').style.display = 'none';
document.getElementById('success').style.display = 'block';

} catch (err) {

console.error(err);

document.getElementById('loading').style.display = 'none';
document.getElementById('error').style.display = 'block';

}

});

</script>

</body>
</html>
