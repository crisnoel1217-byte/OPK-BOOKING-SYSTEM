
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>CN OPK Pro System</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">

<style>
:root{
  --bg:#0a0a12;
  --card:#111827;
  --accent:#7c3aed;
  --accent2:#22d3ee;
  --green:#22c55e;
  --red:#ef4444;
}

*{margin:0;padding:0;box-sizing:border-box;font-family:Inter}
body{background:linear-gradient(135deg,#020617,#0a0a12);color:white}

header{
  text-align:center;
  padding:18px;
  font-size:22px;
  font-weight:700;
  background:linear-gradient(90deg,var(--accent),var(--accent2));
  -webkit-background-clip:text;
  color:transparent;
}

.container{max-width:1100px;margin:auto;padding:15px}
.grid{display:grid;gap:15px}
@media(min-width:768px){.grid{grid-template-columns:1fr 1fr}}

.card{
  background:rgba(255,255,255,0.05);
  padding:15px;
  border-radius:14px;
  backdrop-filter:blur(10px);
}

input,select,button{
  width:100%;
  padding:12px;
  margin-top:10px;
  border-radius:10px;
  border:none;
}

input,select{background:#020617;color:white}

button{
  background:linear-gradient(90deg,var(--accent),var(--accent2));
  font-weight:600;
  cursor:pointer;
}

.slot{
  display:flex;
  justify-content:space-between;
  padding:10px;
  margin-top:6px;
  border-radius:10px;
  background:rgba(255,255,255,0.08);
}

.available{color:var(--green)}
.taken{color:var(--red)}

.badge{
  background:var(--accent2);
  color:black;
  padding:4px 10px;
  border-radius:999px;
  font-size:12px;
}

.admin{display:none}
.stats{display:flex;justify-content:space-between;margin-top:8px}

</style>
</head>

<body>
<header>🚀 CN OPK PRO SYSTEM</header>

<div class="container grid">

<div class="card">
<h3>📅 Booking</h3>
<input id="name" placeholder="Bigo Name" />
<input id="id" placeholder="Bigo ID" />
<input id="lvl" placeholder="Level" />
<input id="agency" placeholder="Agency" />
<input id="gmail" placeholder="Gmail" />
<input id="date" type="date" />
<select id="time"></select>
<button id="bookBtn">Reserve</button>
</div>

<div class="card">
<h3>⏰ Slots</h3>
<div id="slots"></div>
</div>

<div class="card">
<h3>🔐 Admin</h3>
<input id="adminPass" type="password" placeholder="Password" />
<button id="loginBtn">Login</button>
</div>

<div class="card admin" id="adminPanel">
<h3>📊 Dashboard</h3>
<div class="stats"><span>Total</span><span id="total" class="badge">0</span></div>
<div class="stats"><span>Today</span><span id="today" class="badge">0</span></div>
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

const els = {
  date: document.getElementById("date"),
  slots: document.getElementById("slots"),
  time: document.getElementById("time"),
  bookBtn: document.getElementById("bookBtn"),
  loginBtn: document.getElementById("loginBtn"),
  adminPanel: document.getElementById("adminPanel"),
  records: document.getElementById("records"),
  total: document.getElementById("total"),
  today: document.getElementById("today")
};

const generateSlots = () => {
 let slots=[],h=20,m=0;
 while(h<22||(h===22&&m<=15)){
  slots.push(`${h>12?h-12:h}:${m.toString().padStart(2,'0')} ${h>=12?'PM':'AM'}`);
  m+=15;if(m>=60){m=0;h++}
 }
 return slots;
};

async function fetchBookings(){
 const snap = await getDocs(collection(db,"bookings"));
 return snap.docs.map(d=>d.data());
}

async function render(){
 const date = els.date.value;
 els.slots.innerHTML="";
 els.time.innerHTML="";
 if(!date) return;

 const data = await fetchBookings();
 const filtered = data.filter(b=>b.date===date);

 generateSlots().forEach(t=>{
  const taken = filtered.find(b=>b.time===t);

  const div=document.createElement("div");
  div.className="slot";
  div.innerHTML=`<span>${t}</span><span class="${taken?'taken':'available'}">${taken?'Not Available':'Available'}</span>`;
  els.slots.appendChild(div);

  if(!taken){
   const opt=document.createElement("option");
   opt.value=t; opt.textContent=t;
   els.time.appendChild(opt);
  }
 });
}

async function book(){
 const data={
  name:name.value,
  id:id.value,
  lvl:lvl.value,
  agency:agency.value,
  gmail:gmail.value,
  date:els.date.value,
  time:els.time.value
 };

 if(!data.date||!data.time) return alert("Select date & time");

 const existing = await fetchBookings();
 if(existing.find(b=>b.date===data.date && b.time===data.time))
  return alert("Slot taken");

 await addDoc(collection(db,"bookings"),data);
 alert("Booked ✅");
 render();
 loadAdmin();
}

function login(){
 if(adminPass.value==='TRD123'){
  els.adminPanel.style.display='block';
  loadAdmin();
 } else alert("Wrong password");
}

async function loadAdmin(){
 const data = await fetchBookings();
 els.records.innerHTML="";
 els.total.innerText=data.length;

 const today=new Date().toISOString().split('T')[0];
 els.today.innerText=data.filter(b=>b.date===today).length;

 data.forEach(b=>{
  const div=document.createElement("div");
  div.className="slot";
  div.innerHTML=`<span>${b.name}</span><span>${b.time} | ${b.date}</span>`;
  els.records.appendChild(div);
 });
}

els.date.addEventListener("change",render);
els.bookBtn.addEventListener("click",book);
els.loginBtn.addEventListener("click",login);

</script>
</body>
</html>
