<html lang="en">
<head>
<meta charset="UTF-8">
<title>Cute Savage Valentine 💘</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
body{
  font-family: Arial, sans-serif;
  background:#ffe6f0;
  text-align:center;
  padding:20px;
}
.box{
  background:#fff;
  padding:20px;
  border-radius:12px;
  max-width:420px;
  margin:20px auto;
  box-shadow:0 8px 20px rgba(0,0,0,.1);
}
input,select,button{
  width:100%;
  padding:10px;
  margin-top:10px;
  font-size:16px;
}
button{
  background:#ff4081;
  color:#fff;
  border:none;
  font-weight:bold;
  cursor:pointer;
}
.hidden{display:none;}
</style>
</head>

<body>

<!-- ========== SENDER VIEW ========== -->
<div class="box" id="senderBox">
  <h2>Send Valentine 💘</h2>

  <input id="fromName" placeholder="Your Name">
  <input id="toName" placeholder="Their Name">

  <select id="category">
    <option value="">Choose Category</option>
    <option value="friend">Friend 😎</option>
    <option value="crush">Crush 😳</option>
    <option value="lover">Lover 💘</option>
    <option value="family">Family 🤍</option>
    <option value="ex">Ex 😌</option>
  </select>

  <button onclick="sendValentine()">Send Valentine</button>
</div>

<!-- ========== LINK GENERATED ========== -->
<div class="box hidden" id="linkBox">
  <h3>Link Generated ✅</h3>
  <p>Only the receiver will know the message 😏</p>
  <input id="shareLink" readonly>
  <button onclick="copyLink()">Copy Link 🔗</button>
</div>

<!-- ========== RECEIVER VIEW ========== -->
<div class="box hidden" id="receiverBox">
  <h2>Your Valentine 💖</h2>
  <p id="finalMessage" style="font-size:18px;"></p>
  <p id="finalNames" style="margin-top:10px;"></p>
</div>

<script>
const BASE_URL = "https://soolaimanmohamed-ship-it.github.io/Valentine-s-day/";

/* ===== Messages ===== */
const messages = {
  friend: [
    "Best friends forever 😎",
    "Chaos but loyal 😂",
    "You’re my safe place 🤍",
    "Friendship > everything 🔥",
    "Chosen family vibes 😌"
  ],
  crush: [
    "Low-key obsessed 😏",
    "This took courage 😳",
    "Not flirting… maybe 👀",
    "Rent-free in my head 😌",
    "Hope this made you smile 😊"
  ],
  lover: [
    "Always you 💘",
    "You’re my home 🏠",
    "Still choosing you 😌",
    "Soft love, strong bond 💞",
    "My peace in human form 🤍"
  ],
  family: [
    "Family is everything 🤍",
    "Forever grateful for you 🙏",
    "Home is you 🏡",
    "Love without conditions 🫂",
    "My strength always 💪"
  ],
  ex: [
    "No hate, just growth 😌",
    "Lesson learned 💭",
    "Chapter closed 📕",
    "Wishing you peace ✨",
    "We both evolved 🔥"
  ]
};

/* ===== Sender logic ===== */
function sendValentine(){
  const from = document.getElementById("fromName").value.trim();
  const to = document.getElementById("toName").value.trim();
  const cat = document.getElementById("category").value;

  if(!from || !to || !cat){
    alert("Please fill all fields");
    return;
  }

  const msgList = messages[cat];
  const msg = msgList[Math.floor(Math.random()*msgList.length)];

  // Unicode-safe encoding
  const payload = encodeURIComponent(JSON.stringify({
    from: from,
    to: to,
    msg: msg
  }));

  const link = BASE_URL + "?v=" + payload;

  document.getElementById("senderBox").classList.add("hidden");
  document.getElementById("linkBox").classList.remove("hidden");
  document.getElementById("shareLink").value = link;
}

function copyLink(){
  const l = document.getElementById("shareLink");
  l.select();
  document.execCommand("copy");
  alert("Link copied 👍");
}

/* ===== Receiver logic ===== */
const params = new URLSearchParams(window.location.search);
if(params.get("v")){
  try{
    const data = JSON.parse(decodeURIComponent(params.get("v")));

    document.getElementById("senderBox").classList.add("hidden");
    document.getElementById("linkBox").classList.add("hidden");
    document.getElementById("receiverBox").classList.remove("hidden");

    document.getElementById("finalMessage").innerText = data.msg;
    document.getElementById("finalNames").innerText =
      "From: " + data.from + " → To: " + data.to;

  }catch(err){
    alert("Invalid or broken Valentine link");
  }
}
</script>

</body>
</html>
