# OPK-BOOKING-SYSTEM
BIGO HOST ONLINE OPK BOOKING
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>OPK GenZ System</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">

<style>
:root{
  --bg:#0f0f1a;
  --card:#18182a;
  --accent:#7c3aed;
  --accent2:#22c55e;
  --text:#ffffff;
  --muted:#9ca3af;
}

*{box-sizing:border-box;font-family:Inter,sans-serif}
body{margin:0;background:linear-gradient(135deg,#0f0f1a,#1a1a2e);color:var(--text)}
.wrap{max-width:900px;margin:auto;padding:15px}

.logo{
  text-align:center;margin-bottom:10px
}
.logo div{
  width:70px;height:70px;margin:auto;border-radius:20px;
  background:linear-gradient(135deg,#7c3aed,#22c55e);
  display:flex;align-items:center;justify-content:center;
  font-weight:700;font-size:24px
}

h1{text-align:center;margin:10px 0}
.subtitle{text-align:center;color:var(--muted);font-size:13px;margin-bottom:15px}

.card{
  background:var(--card);
  padding:18px;
  border-radius:18px;
  box-shadow:0 10px 30px rgba(0,0,0,.4);
  margin-bottom:15px
}

input,button{
  width:100%;padding:14px;margin:6px 0;
  border:none;border-radius:12px;font-size:14px
}

input{background:#0f0f1a;color:white}
input::placeholder{color:#6b7280}

button{
  background:linear-gradient(135deg,#7c3aed,#6366f1);
  color:white;font-weight:600
}

button:hover{opacity:.9}

.badge{
  background:#0f0f1a;border:1px solid #2a2a40;
  padding:6px 10px;border-radius:999px;
  font-size:12px;color:var(--muted);
  display:inline-block;margin-top:5px
}

.status{text-align:center;margin-top:10px;font-size:13px}
.ok{color:var(--accent2)}
.err{color:#ef4444}

.table-wrap{overflow:auto}

table{width:100%;border-collapse:collapse;margin-top:10px}
th,td{padding:10px;border-bottom:1px solid #2a2a40;font-size:12px}

@media(max-width:600px){
  input,button{font-size:13px;padding:12px}
}
</style>
</head>

<body>

<div class="wrap">

<div class="logo">
  <div>CN</div>
</div>

<h1>OPK Booking</h1>
<div class="subtitle">Fast • Clean • Mobile Friendly</div>

<div class="card">
<h3>Create Booking</h3>

<input id="name" placeholder="Bigo Name">
<input id="bigo" placeholder="Bigo ID">
<input id="agency" placeholder="Agency">
<input id="email" placeholder="Email">
<input id="level" placeholder="Host Level">
<input id="date" type="date" onchange="loadDaily()">
<input id="time" placeholder="Time (ex. 8:00 PM)">

<div id="daily" class="badge">Daily OPK: 0</div>

<button onclick="book()">Reserve Slot</button>
<div id="status" class="status"></div>
</div>

<div class="card">
<h3>Dashboard</h3>
<button onclick="load()">Refresh</button>

<div class="table-wrap">
<table>
<thead>
<tr>
<th>Name</th><th>ID</th><th>Date</th><th>Time</th>
</tr>
</thead>
<tbody id="table"></tbody>
</table>
</div>
</div>

</div>

<script>

const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID"
};

firebase.initializeApp(firebaseConfig);
const db = firebase.firestore();

async function isTaken(d,t){
 let snap = await db.collection("bookings").where("date","==",d).where("time","==",t).get();
 return !snap.empty;
}

async function loadDaily(){
 let d=date.value;
 if(!d)return;
 let snap = await db.collection("bookings").where("date","==",d).get();
 daily.innerText = `Daily OPK: ${snap.size}`;
}

async function book(){
 let d=date.value,t=time.value;
 if(await isTaken(d,t)) return setStatus('Slot already taken','err');

 await db.collection("bookings").add({
  name:name.value,
  bigo:bigo.value,
  date:d,
  time:t
 });

 setStatus('Booked ✔','ok');
 load();
 loadDaily();
}

async function load(){
 let snap = await db.collection("bookings").get();
 table.innerHTML='';
 snap.forEach(doc=>{
  let b=doc.data();
  table.innerHTML+=`<tr><td>${b.name}</td><td>${b.bigo}</td><td>${b.date}</td><td>${b.time}</td></tr>`;
 });
}

function setStatus(msg,type){
 status.textContent=msg;
 status.className='status '+type;
}

load();

</script>

</body>
</html>
