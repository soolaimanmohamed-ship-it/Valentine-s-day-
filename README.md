<!DOCTYPE html>
<html>
<head>
<title>Cute Savage Valentine 💘</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h2>💘 Cute Savage Valentine</h2>

<input id="from" placeholder="Your Name">
<input id="to" placeholder="Their Name">

<select id="type">
  <option value="">Choose</option>
  <option value="crush">Crush</option>
  <option value="friend">Friend</option>
  <option value="lover">Lover</option>
</select>

<button onclick="sendValentine()">Send 💌</button>

<p id="result"></p>

<hr>

<div id="receiver" style="display:none">
  <h3>Your Valentine 💖</h3>
  <p id="msg"></p>
  <p id="names"></p>
</div>

<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-firestore-compat.js"></script>

<script>
/* Firebase */
firebase.initializeApp({
  apiKey: "YOUR_KEY",
  authDomain: "YOUR_DOMAIN",
  projectId: "YOUR_PROJECT_ID"
});
const db = firebase.firestore();

/* Messages */
const messages = {
  crush: ["Low-key obsessed 😏","This took courage 😳"],
  friend:["Bestie energy 😎","Chaos but loyal 😂"],
  lover:["Always you 💘","You’re home 🏠"]
};

/* Sender */
async function sendValentine(){
  const f = from.value.trim();
  const t = to.value.trim();
  const tp = type.value;
  if(!f||!t||!tp) return alert("Fill all");

  const msg = messages[tp][Math.floor(Math.random()*messages[tp].length)];

  const doc = await db.collection("valentines").add({
    from:f,to:t,msg,created:Date.now()
  });

  const link = location.origin + location.pathname + "?id=" + doc.id;
  result.innerText = "Share this link:\n" + link;
}

/* Receiver */
const id = new URLSearchParams(location.search).get("id");
if(id){
  db.collection("valentines").doc(id).get().then(d=>{
    if(!d.exists) return;
    receiver.style.display="block";
    msg.innerText = d.data().msg;
    names.innerText = "From: "+d.data().from+" → To: "+d.data().to;
  });
}
</script>

</body>
</html>
