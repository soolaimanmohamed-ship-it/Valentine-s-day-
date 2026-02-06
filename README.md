
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Valentine Test</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
body{font-family:Arial;text-align:center;padding:20px;background:#ffe6f0}
.box{background:#fff;padding:20px;border-radius:10px;max-width:400px;margin:auto}
input,select,button{width:100%;padding:10px;margin-top:10px}
button{background:#ff4081;color:#fff;border:none;font-weight:bold}
</style>
</head>

<body>

<div class="box" id="sender">
<h2>Send Valentine 💘</h2>

<input id="fromName" placeholder="Your Name">
<input id="toName" placeholder="Their Name">

<select id="relation">
  <option value="">Choose Category</option>
  <option value="friend">Friend</option>
  <option value="crush">Crush</option>
  <option value="lover">Lover</option>
</select>

<button onclick="send()">Send</button>
</div>

<div class="box" id="result" style="display:none">
<h3>Link Generated ✅</h3>
<input id="shareLink" readonly>
<button onclick="copyLink()">Copy Link</button>
</div>

<div class="box" id="receiver" style="display:none">
<h2>Your Valentine 💖</h2>
<p id="message"></p>
<p id="names"></p>
</div>

<script>
const BASE_URL = "https://soolaimanmohamed-ship-it.github.io/Valentine-s-day/";

const messages = {
  friend:["Best friends forever 😎","You’re my safe space 🤍"],
  crush:["Low-key obsessed 😏","This took courage 😳"],
  lover:["Always you 💘","You’re home 🏠"]
};

function send(){
  const from = document.getElementById("fromName").value.trim();
  const to = document.getElementById("toName").value.trim();
  const rel = document.getElementById("relation").value;

  if(!from || !to || !rel){
    alert("Fill all fields");
    return;
  }

  const msg = messages[rel][Math.floor(Math.random()*messages[rel].length)];
  const data = btoa(JSON.stringify({from,to,msg}));

  const link = BASE_URL + "?v=" + data;

  document.getElementById("sender").style.display="none";
  document.getElementById("result").style.display="block";
  document.getElementById("shareLink").value = link;
}

function copyLink(){
  const l = document.getElementById("shareLink");
  l.select();
  document.execCommand("copy");
  alert("Copied 👍");
}

const params = new URLSearchParams(window.location.search);
if(params.get("v")){
  const d = JSON.parse(atob(params.get("v")));
  document.getElementById("sender").style.display="none";
  document.getElementById("result").style.display="none";
  document.getElementById("receiver").style.display="block";

  document.getElementById("message").innerText = d.msg;
  document.getElementById("names").innerText =
    "From: " + d.from + " → To: " + d.to;
}
</script>

</body>
</html>
