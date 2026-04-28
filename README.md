<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CN OPK Firebase</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">

<style>
body{margin:0;font-family:Inter;background:#0f0f1a;color:white}
header{text-align:center;padding:20px;font-size:26px;font-weight:700;background:linear-gradient(90deg,#7c3aed,#22d3ee);-webkit-background-clip:text;color:transparent}
.container{max-width:1000px;margin:auto;padding:15px}
.card{background:rgba(255,255,255,0.05);padding:15px;border-radius:15px;margin-bottom:15px}
input,select,button{width:100%;padding:12px;margin-top:10px;border-radius:10px;border:none}
button{background:linear-gradient(90deg,#7c3aed,#22d3ee);color:white;font-weight:600}
.slot{display:flex;justify-content:space-between;background:rgba(255,255,255,0.08);padding:10px;margin-top:5px;border-radius:10px}
.available{color:#22c55e}
.taken{color:#ef4444}
.admin{display:none}
</style>

<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js"></script>
</head>

<body>
<header>🔥 CN OPK CLOUD SYSTEM</header>

<div class="container">

<div class="card">
<h3>Book Slot</h3>
<input id="name" placeholder="Bigo Name">
<input id="id" placeholder="Bigo ID">
<input id="lvl" placeholder="Level">
<input id="agency" placeholder="Agency">
<input id="gmail" placeholder="Gmail">

<!-- DATE SELECTION ADDED HERE -->
<input id="date" type="date">

<select id="time"></select>
<button onclick="book()">Reserve</button>
</div>

<div class="card">
<h3>Slots</h3>
<div id="slots"></div>
</div>

<div class="card">
<h3>Admin</h3>
<input id="adminPass" type="password" placeholder="Password">
<button onclick="login()">Login</button>
</div>

<div class="card admin" id="adminPanel">
<h3>Dashboard</h3>
<div id="records"></div>
</div>

</div>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
import { getFirestore, collection, addDoc, getDocs, query, where } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

const firebaseConfig = {
  apiKey: "AIzaSyBJBT_BAeos1hb_fKJzSontJVgBub9Wjhc",
  authDomain: "opk-system-cn.firebaseapp.com",
  projectId: "opk-system-cn",
  storageBucket: "opk-system-cn.firebasestorage.app",
  messagingSenderId: "1098097772017",
  appId: "1:1098097772017:web:4e015378c786d6b404f050",
  measurementId: "G-CKMWK5W51Z"
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);

const start=20,endHour=22,endMin=15;

function generateSlots(){
 let slots=[],h=start,m=0;
 while(h<endHour||(h===endHour&&m<=endMin)){
  let t=`${h>12?h-12:h}:${m.toString().padStart(2,'0')} ${h>=12?'PM':'AM'}`;
  slots.push(t);
  m+=15;if(m>=60){m=0;h++}
 }
 return slots;
}

async function render(){
 slots.innerHTML="";
 time.innerHTML="";

 const selectedDate = date.value;
 if(!selectedDate) return;

 const snapshot = await getDocs(collection(db,"bookings"));
 let booked = snapshot.docs.map(d=>d.data()).filter(b=>b.date.split('T')[0]===selectedDate);

 generateSlots().forEach(t=>{
  let taken=booked.find(b=>b.time===t);

  let div=document.createElement('div');
  div.className='slot';
  div.innerHTML=`<span>${t}</span><span class="${taken?'taken':'available'}">${taken?'Not Available':'Available'}</span>`;
  slots.appendChild(div);

  if(!taken){
   let opt=document.createElement('option');
   opt.value=t;
   opt.innerText=t;
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

 if(!data.date) return alert('Select date');
 if(!data.time) return alert('No slot');

 const q=query(collection(db,"bookings"),where("time","==",data.time));
 const snap=await getDocs(q);

 let exist=snap.docs.find(d=>d.data().date===data.date);
 if(exist)return alert('Already taken');

 await addDoc(collection(db,"bookings"),data);
 alert('Booked ✅');
 render();
}

function login(){
 if(adminPass.value==='TRD123'){
  adminPanel.style.display='block';
  loadRecords();
 }else alert('Wrong password');
}

async function loadRecords(){
 records.innerHTML="";
 const snapshot = await getDocs(collection(db,"bookings"));
 snapshot.forEach(doc=>{
  let b=doc.data();
  let div=document.createElement('div');
  div.className='slot';
  div.innerHTML=`<span>${b.name} (${b.id})</span><span>${b.time} | ${b.date}</span>`;
  records.appendChild(div);
 });
}

render();
</script>

</body>
</html>
