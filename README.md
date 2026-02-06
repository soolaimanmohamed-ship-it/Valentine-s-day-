<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Cute Savage Valentine 💘</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
body{
  font-family: Arial, sans-serif;
  background: linear-gradient(135deg,#ffd6e7,#e0f2ff);
  text-align:center;
  padding:20px;
}
.card{
  background:#fff;
  border-radius:18px;
  padding:25px;
  max-width:420px;
  margin:20px auto;
  box-shadow:0 10px 30px rgba(0,0,0,.1);
}
input,select,button{
  width:100%;
  padding:12px;
  margin-top:10px;
  border-radius:10px;
  border:1px solid #ddd;
  font-size:16px;
}
button{
  background:#ff4f93;
  color:#fff;
  font-weight:bold;
  border:none;
  cursor:pointer;
}
.hidden{display:none;}
.heart{
  font-size:70px;
  cursor:pointer;
  animation:pulse 1.2s infinite;
}
@keyframes pulse{
  0%{transform:scale(1)}
  50%{transform:scale(1.2)}
  100%{transform:scale(1)}
}
footer a{
  color:#555;
  margin:0 8px;
  cursor:pointer;
  text-decoration:none;
}
</style>
</head>

<body>

<!-- MAIN -->
<div class="card" id="main">
<h2>💘 Cute Savage Valentine</h2>
<p>Send a Valentine… even <b>you</b> won’t know what it says 😌</p>

<input id="from" placeholder="Your Name 😎">
<input id="to" placeholder="Their Name 👀">

<select id="type">
<option value="">Choose Category</option>
<option value="friend">Friend 😎</option>
<option value="crush">Crush 😳</option>
<option value="lover">Lover 💘</option>
<option value="family">Family 🤍</option>
<option value="ex">Ex 😌</option>
</select>

<button onclick="sendValentine()">Send Valentine 💌</button>
</div>

<!-- SENT -->
<div class="card hidden" id="sent">
<h3>💌 Sent!</h3>
<p>Only they will know what they received 😏</p>
<input id="link" readonly>
<button onclick="copyLink()">Copy Link 🔗</button>
<button onclick="shareWA()">Share on WhatsApp 📲</button>
</div>

<!-- COVER -->
<div class="card hidden" id="cover">
<h3>💌 Someone sent you a Valentine</h3>
<p>Tap to open…</p>
<div class="heart" onclick="openCard()">❤️</div>
</div>

<!-- MESSAGE -->
<div class="card hidden" id="message">
<h3>Your Valentine 💖</h3>
<p id="msg"></p>
<p id="names"></p>
<button onclick="goHome()">Send One Back 😏</button>
</div>

<!-- ABOUT -->
<div class="card hidden" id="about">
<h3>About</h3>
<p>This is a fun Valentine message generator.  
No login, no data stored. Just for entertainment.</p>
<button onclick="goHome()">⬅ Back</button>
</div>

<!-- CONTACT -->
<div class="card hidden" id="contact">
<h3>Contact</h3>
<p>Email: <b>soolaimanmohamed@gmail.com</b></p>
<button onclick="goHome()">⬅ Back</button>
</div>

<footer>
<a onclick="showAbout()">About</a> |
<a onclick="showContact()">Contact</a>
</footer>

<script>
const BASE_URL = "https://soolaimanmohamed-ship-it.github.io/Valentine-s-day/";

const messages = {
  friend:["Unlimited teasing rights 😌","Bestie vibes 😎","Chaos but loyal 😂","Friendship > everything"],
  crush:["Low-key obsessed 😏","This took courage 😳","Not flirting… maybe 👀","Rent-free in my head"],
  lover:["You’re my Valentine 😌","You’re home 🏠","Always you 💘","Soft love 💞"],
  family:["Family is everything 🤍","Forever grateful 🙏","Home is you 🏡","Love without conditions"],
  ex:["No hate, just growth 😌","Chapter closed 📕","Boundaries matter 🚧","Moved on 💨"]
};

function hideAll(){
  document.querySelectorAll('.card').forEach(c=>c.classList.add('hidden'));
}

function sendValentine(){
  let f=from.value.trim(), t=to.value.trim(), tp=type.value;
  if(!f||!t||!tp){alert("Fill all fields");return;}
  let m=messages[tp][Math.floor(Math.random()*messages[tp].length)];
  let data=btoa(JSON.stringify({f,t,m}));
  let url=BASE_URL+"?v="+data;

  hideAll();
  sent.classList.remove("hidden");
  link.value=url;
}

function copyLink(){
  link.select();
  document.execCommand("copy");
  alert("Link copied 😌");
}

function shareWA(){
  let text="💘 Someone sent you a Valentine… only you can see it 😌\n\n"+link.value;
  window.open("https://wa.me/?text="+encodeURIComponent(text));
}

const p=new URLSearchParams(location.search);
if(p.get("v")){
  let d=JSON.parse(atob(p.get("v")));
  hideAll();
  cover.classList.remove("hidden");
  window.card=d;
}

function openCard(){
  hideAll();
  message.classList.remove("hidden");
  msg.innerText=card.m;
  names.innerText="From: "+card.f+" → To: "+card.t;
}

function showAbout(){ hideAll(); about.classList.remove("hidden"); }
function showContact(){ hideAll(); contact.classList.remove("hidden"); }
function goHome(){ window.location.href=BASE_URL; }
</script>

</body>
</html>
