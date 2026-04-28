<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CN OPK PRO DASHBOARD</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">

<style>
:root{
  --bg:#0b0b14;
  --card:rgba(255,255,255,0.06);
  --glass:rgba(255,255,255,0.08);
  --primary:#7c3aed;
  --accent:#22d3ee;
  --green:#22c55e;
  --red:#ef4444;
  --text:#e5e7eb;
}

*{box-sizing:border-box;font-family:Inter}
body{margin:0;background:linear-gradient(135deg,#0b0b14,#020617);color:var(--text)}

header{
  text-align:center;
  padding:18px;
  font-size:24px;
  font-weight:800;
  background:linear-gradient(90deg,var(--primary),var(--accent));
  -webkit-background-clip:text;
  color:transparent;
}

.container{max-width:1100px;margin:auto;padding:15px}

.grid{display:grid;gap:15px}
@media(min-width:768px){.grid{grid-template-columns:1fr 1fr}}

.card{
  background:var(--card);
  border-radius:16px;
  padding:15px;
  backdrop-filter:blur(10px);
}

input,select,button{
  width:100%;padding:12px;margin-top:10px;
  border-radius:10px;border:none;font-size:14px
}

input,select{background:#0f172a;color:white}

button{
  background:linear-gradient(90deg,var(--primary),var(--accent));
  color:white;font-weight:700;cursor:pointer
}

.slot{
  display:flex;justify-content:space-between;
  padding:10px;margin-top:6px;
  border-radius:10px;background:var(--glass)
}

.available{color:var(--green)}
.taken{color:var(--red)}

.badge{
  padding:5px 10px;border-radius:999px;
  background:var(--accent);color:black;font-size:12px
}

.admin{display:none}
.stats{display:flex;justify-content:space-between;margin-top:10px}

</style>
</head>

<body>
<header>🚀 CN OPK PRO DASHBOARD</header>

<div class="container grid">

<!-- BOOKING -->
<div class="card">
<h3>📅 Book OPK Slot</h3>
<input id="name" placeholder="Bigo Name">
<input id="id" placeholder="Bigo ID">
<input id="lvl" placeholder="Level">
<input id="agency" placeholder="Agency">
<input id="gmail" placeholder="Gmail">

<input id="date" type="date">

<select id="time"></select>
<button onclick="book()">Reserve Slot</button>
</div>

<!-- SLOTS -->
<div class="card">
<h3>⏰ Live Slots</h3>
<div id="slots"></div>
</div>

<!-- ADMIN -->
<div class="card">
<h3>🔐 Admin Login</h3>
<input id="adminPass" type="password" placeholder="Password">
<button onclick="login()">Login</button>
</div>

<!-- DASHBOARD -->
<div class="card admin" id="adminPanel">
<h3>📊 Pro Dashboard</h3>

<div class="stats">
<span>Total Bookings:</span>
<span class="badge" id="total">0</span>
</div>

<div class="stats">
<span>Today:</span>
<span class="badge" id="today">0</span>
</div>

<div id="records"></div>
</div>

</div>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
import { getFirestore, collection, addDoc, getDocs } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

const firebaseConfig = {
  apiKey: "AIzaSyBJBT_BAeos1hb_fKJzSontJVgBub9Wjhc",
  authDomain: "opk-system-cn.firebaseapp.com",
  projectId: "opk-system-cn",
  storageBucket: "opk-system-cn.appspot.com",
  messagingSenderId: "1098097772017",
  appId: "1:1098097772017:web:4e015378c786d6b404f050"
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);

const start=20,endHour=22,endMin=15;

function generateSlots(){
 let slots=[],h=start,m=0;
 while(h<endHour||(h===endHour&&m<=endMin)){
  slots.push(`${h>12?h-12:h}:${m.toString().padStart(2,'0')} ${h>=12?'PM':'AM'}`);
  m+=15;if(m>=60){m=0;h++}
 }
 return slots;
}

function getDate(){
 return document.getElementById("date").value;
}

async function render(){
 const slotsDiv=document.getElementById("slots");
 const time=document.getElementById("time");
 const date=getDate();

 slotsDiv.innerHTML="";
 time.innerHTML="";

 if(!date) return;

 const snap=await getDocs(collection(db,"bookings"));
 let bookings=snap.docs.map(d=>d.data());

 let filtered=bookings.filter(b=>b.date===date);

 generateSlots().forEach(t=>{
  let taken=filtered.find(b=>b.time===t);

  let div=document.createElement("div");
  div.className="slot";
  div.innerHTML=`<span>${t}</span><span class="${taken?'taken':'available'}">${taken?'Not Available':'Available'}</span>`;
  slotsDiv.appendChild(div);

  if(!taken){
   let opt=document.createElement("option");
   opt.value=t;
   opt.textContent=t;
   time.appendChild(opt);
  }
 });
}

async function book(){
 let data={
  name:name.value,
  id:id.value,
  lvl:lvl.value,
  agency:agency.value,
  gmail:gmail.value,
  time:time.value,
  date:date.value
 };

 if(!data.date||!data.time) return alert("Fill all fields");

 let snap=await getDocs(collection(db,"bookings"));
 let exist=snap.docs.map(d=>d.data()).find(b=>b.date===data.date && b.time===data.time);

 if(exist) return alert("Slot already taken");

 await addDoc(collection(db,"bookings"),data);
 alert("Booked ✅");
 render();
 loadAdmin();
}

function login(){
 if(adminPass.value==='TRD123'){
  adminPanel.style.display='block';
  loadAdmin();
 } else alert("Wrong password");
}

async function loadAdmin(){
 const records=document.getElementById("records");
 const total=document.getElementById("total");
 const today=document.getElementById("today");

 records.innerHTML="";

 const snap=await getDocs(collection(db,"bookings"));
 let data=snap.docs.map(d=>d.data());

 total.innerText=data.length;

 let todayDate=new Date().toISOString().split('T')[0];
 let todayCount=data.filter(b=>b.date===todayDate).length;
 today.innerText=todayCount;

 data.forEach(b=>{
  let div=document.createElement("div");
  div.className="slot";
  div.innerHTML=`<span>${b.name} (${b.id})</span><span>${b.time} | ${b.date}</span>`;
  records.appendChild(div);
 });
}

render();
</script>

</body>
</html>
