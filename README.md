# Jarvis-warehouse
<!DOCTYPE html>
<html lang="kk">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<meta name="theme-color" content="#07111f">
<title>JARVIS — Warehouse</title>

<style>
*{box-sizing:border-box}
body{
 margin:0;
 font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Arial,sans-serif;
 background:#050b14;
 color:#eaf4ff
}
header{
 padding:18px;
 background:linear-gradient(135deg,#08182c,#0b2744);
 border-bottom:1px solid #1b4568;
 position:sticky;top:0;z-index:10
}
.logo{
 font-size:30px;
 font-weight:800;
 letter-spacing:3px;
 color:#67c7ff
}
.sub{color:#8da9bf;font-size:13px;margin-top:4px}
.container{padding:16px;max-width:1100px;margin:auto}
.nav{
 display:flex;
 gap:8px;
 overflow-x:auto;
 margin-bottom:16px
}
.nav button{
 white-space:nowrap;
 background:#0c1b2c;
 color:#a9c6dc;
 border:1px solid #1d3b55;
 padding:11px 14px;
 border-radius:12px
}
.nav button.active{
 background:#123d5c;
 color:#fff;
 border-color:#4ebcff
}
.card{
 background:#0b1624;
 border:1px solid #19344c;
 border-radius:16px;
 padding:16px;
 margin-bottom:14px
}
h2{margin:0 0 14px}
h3{margin:0 0 10px}
.grid{
 display:grid;
 grid-template-columns:repeat(auto-fit,minmax(150px,1fr));
 gap:10px
}
.kpi{
 padding:16px;
 background:#0e2033;
 border-radius:14px;
 border:1px solid #19415d
}
.kpi b{
 display:block;
 font-size:25px;
 color:#69caff
}
table{
 width:100%;
 border-collapse:collapse;
 font-size:14px
}
th,td{
 padding:10px 7px;
 border-bottom:1px solid #183047;
 text-align:left
}
th{color:#7fa8c4}
input,select{
 width:100%;
 padding:12px;
 border-radius:10px;
 border:1px solid #25445c;
 background:#07121f;
 color:#fff;
 margin:5px 0 10px
}
button{
 cursor:pointer
}
.primary{
 background:#168bd1;
 color:white;
 border:0;
 padding:12px 16px;
 border-radius:11px;
 font-weight:700
}
.danger{
 background:#a52e3b;
 color:#fff;
 border:0;
 padding:8px 11px;
 border-radius:8px
}
.voice{
 position:fixed;
 right:20px;
 bottom:20px;
 width:65px;
 height:65px;
 border-radius:50%;
 border:2px solid #4fc4ff;
 background:#092238;
 color:#72d1ff;
 font-size:25px;
 box-shadow:0 0 25px #12628b;
 z-index:20
}
.small{font-size:12px;color:#7895aa}
.hidden{display:none}
.badge{
 padding:4px 8px;
 border-radius:8px;
 background:#123e56;
 color:#8bd9ff;
 font-size:12px
}
</style>
</head>

<body>

<header>
 <div class="logo">JARVIS</div>
 <div class="sub">Warehouse Intelligence System</div>
</header>

<div class="container">

<div class="nav">
 <button class="active" onclick="show('dashboard',this)">Dashboard</button>
 <button onclick="show('stock',this)">Склад</button>
 <button onclick="show('requests',this)">Заявки</button>
 <button onclick="show('tools',this)">Инструмент</button>
 <button onclick="show('history',this)">История</button>
</div>

<!-- DASHBOARD -->
<section id="dashboard">

<div class="card">
 <h2>Дрим Сити Эко</h2>
 <div class="small">Қазіргі объект</div>
</div>

<div class="grid">

<div class="kpi">
 <span class="small">Номенклатура</span>
 <b id="kpiItems">0</b>
</div>

<div class="kpi">
 <span class="small">Операциялар</span>
 <b id="kpiOps">0</b>
</div>

<div class="kpi">
 <span class="small">Заявкалар</span>
 <b id="kpiReq">0</b>
</div>

<div class="kpi">
 <span class="small">Құралдар</span>
 <b id="kpiTools">0</b>
</div>

</div>

<div class="card">
 <h3>Кезектер</h3>
 <div class="grid">
  <div class="kpi">
   <b>4</b>
   <span class="small">4-інші кезек</span>
  </div>
  <div class="kpi">
   <b>5</b>
   <span class="small">5-інші кезек</span>
  </div>
 </div>
</div>

<div class="card">
 <h3>JARVIS</h3>
 <div id="jarvisMessage">
 Дайынмын. Дауыстық команданы күтіп тұрмын.
 </div>
</div>

</section>


<!-- STOCK -->
<section id="stock" class="hidden">

<div class="card">
 <h2>Склад</h2>

 <input id="search" placeholder="Материал іздеу..." oninput="renderStock()">

 <table>
 <thead>
 <tr>
  <th>Материал</th>
  <th>Ед.</th>
  <th>4 кезек</th>
  <th>5 кезек</th>
  <th>Барлығы</th>
 </tr>
 </thead>
 <tbody id="stockTable"></tbody>
 </table>
</div>

<div class="card">
 <h3>Операция</h3>

 <select id="opType">
  <option value="in">Приход</option>
  <option value="out">Расход</option>
  <option value="writeoff">Списание</option>
  <option value="move">Перемещение</option>
 </select>

 <select id="material"></select>

 <input id="qty" type="number" min="1" placeholder="Количество">

 <select id="queue">
  <option value="4">4-інші кезек</option>
  <option value="5">5-інші кезек</option>
 </select>

 <select id="toQueue">
  <option value="5">→ 5-інші кезек</option>
  <option value="4">→ 4-інші кезек</option>
 </select>

 <input id="note" placeholder="Ескерту">

 <button class="primary" onclick="operation()">Операция орындау</button>
</div>

</section>


<!-- REQUESTS -->
<section id="requests" class="hidden">

<div class="card">
 <h2>Заявки</h2>

 <input id="reqMaterial" placeholder="Материал">

 <input id="reqQty" type="number" placeholder="Количество">

 <select id="reqQueue">
  <option value="4">4-інші кезек</option>
  <option value="5">5-інші кезек</option>
 </select>

 <input id="reqPerson" placeholder="Кім сұрады">

 <input id="reqDate" type="date">

 <input id="reqSupplier" placeholder="Поставщик">

 <input id="reqNote" placeholder="Ескерту">

 <button class="primary" onclick="addRequest()">Заявка қосу</button>
</div>

<div class="card">
 <table>
 <thead>
 <tr>
  <th>Материал</th>
  <th>Саны</th>
  <th>Кезек</th>
  <th>Статус</th>
 </tr>
 </thead>
 <tbody id="requestTable"></tbody>
 </table>
</div>

</section>


<!-- TOOLS -->
<section id="tools" class="hidden">

<div class="card">
 <h2>Инструмент</h2>

 <input id="toolName" placeholder="Инструмент атауы">

 <input id="toolId" placeholder="Инвентарный №">

 <input id="toolHolder" placeholder="Кім алды">

 <button class="primary" onclick="addTool()">Инструмент қосу</button>
</div>

<div class="card">
 <table>
 <thead>
 <tr>
  <th>Инструмент</th>
  <th>№</th>
  <th>Кімде</th>
  <th>Статус</th>
 </tr>
 </thead>
 <tbody id="toolTable"></tbody>
 </table>
</div>

</section>


<!-- HISTORY -->
<section id="history" class="hidden">

<div class="card">
 <h2>Операциялар тарихы</h2>

 <table>
 <thead>
 <tr>
  <th>Уақыт</th>
  <th>Операция</th>
  <th>Материал</th>
  <th>Саны</th>
  <th>Кезек</th>
 </tr>
 </thead>

 <tbody id="historyTable"></tbody>
 </table>

</div>

</section>

</div>


<button class="voice" onclick="voiceCommand()">🎙️</button>


<script>

const materials=[
 {name:"Муфта DN 225 SDR 17",unit:"дана",q4:0,q5:0},
 {name:"Втулка DN 225 SDR 17",unit:"дана",q4:0,q5:0},
 {name:"Фланец D200 PN10",unit:"дана",q4:0,q5:0},
 {name:"Задвижка DN150, 8 тесік",unit:"дана",q4:0,q5:0},
 {name:"Труба чугун D100, L=3 м",unit:"дана",q4:0,q5:0},
 {name:"Цемент",unit:"қап",q4:0,q5:0},
 {name:"Битумная мастика",unit:"",q4:0,q5:0},
 {name:"Грунтовка",unit:"",q4:0,q5:0},
 {name:"ПВХ лента",unit:"рулон",q4:0,q5:0},
 {name:"Пена",unit:"баллон",q4:0,q5:0},
 {name:"Бензин",unit:"литр",q4:0,q5:0}
];

let operations=[];
let requests=[];
let tools=[];


function save(){
 localStorage.setItem("jarvis_materials",JSON.stringify(materials));
 localStorage.setItem("jarvis_operations",JSON.stringify(operations));
 localStorage.setItem("jarvis_requests",JSON.stringify(requests));
 localStorage.setItem("jarvis_tools",JSON.stringify(tools));
}

function load(){

 let a=localStorage.getItem("jarvis_materials");
 let b=localStorage.getItem("jarvis_operations");
 let c=localStorage.getItem("jarvis_requests");
 let d=localStorage.getItem("jarvis_tools");

 if(a) Object.assign(materials,JSON.parse(a));
 if(b) operations=JSON.parse(b);
 if(c) requests=JSON.parse(c);
 if(d) tools=JSON.parse(d);
}


function show(id,btn){

 document.querySelectorAll("section").forEach(x=>x.classList.add("hidden"));
 document.getElementById(id).classList.remove("hidden");

 document.querySelectorAll(".nav button").forEach(x=>x.classList.remove("active"));
 if(btn)btn.classList.add("active");

 renderAll();
}


function renderStock(){

 let search=document.getElementById("search").value.toLowerCase();

 let html="";

 materials
 .filter(m=>m.name.toLowerCase().includes(search))
 .forEach(m=>{

 let total=m.q4+m.q5;

 html+=`
 <tr>
 <td>${m.name}</td>
 <td>${m.unit}</td>
 <td>${m.q4}</td>
 <td>${m.q5}</td>
 <td><b>${total}</b></td>
 </tr>
 `;
 });

 document.getElementById("stockTable").innerHTML=html;
}


function renderMaterialSelect(){

 let html="";

 materials.forEach((m,i)=>{
  html+=`<option value="${i}">${m.name}</option>`;
 });

 document.getElementById("material").innerHTML=html;
}


function operation(){

 let type=document.getElementById("opType").value;
 let index=Number(document.getElementById("material").value);
 let qty=Number(document.getElementById("qty").value);
 let queue=document.getElementById("queue").value;
 let to=document.getElementById("toQueue").value;
 let note=document.getElementById("note").value;

 if(!qty || qty<=0){
  alert("Количество енгіз");
  return;
 }

 let m=materials[index];

 if(type==="in"){
  if(queue==="4")m.q4+=qty;
  else m.q5+=qty;
 }

 if(type==="out" || type==="writeoff"){

  let balance=queue==="4"?m.q4:m.q5;

  if(balance<qty){
   alert("Қалдық жеткіліксіз!");
   return;
  }

  if(queue==="4")m.q4-=qty;
  else m.q5-=qty;
 }

 if(type==="move"){

  let balance=queue==="4"?m.q4:m.q5;

  if(balance<qty){
   alert("Қалдық жеткіліксіз!");
   return;
  }

  if(queue==="4"){
   m.q4-=qty;
   m.q5+=qty;
  }else{
   m.q5-=qty;
   m.q4+=qty;
  }
 }

 let names={
  in:"Приход",
  out:"Расход",
  writeoff:"Списание",
  move:"Перемещение"
 };

 operations.unshift({
  time:new Date().toLocaleString("ru-RU"),
  type:names[type],
  material:m.name,
  qty:qty,
  queue:queue
 });

 save();
 renderAll();

 document.getElementById("qty").value="";
 document.getElementById("note").value="";

 alert("JARVIS: Операция орындалды.");
}


function renderHistory(){

 let html="";

 operations.forEach(o=>{
 html+=`
 <tr>
  <td>${o.time}</td>
  <td><span class="badge">${o.type}</span></td>
  <td>${o.material}</td>
  <td>${o.qty}</td>
  <td>${o.queue}-інші</td>
 </tr>
 `;
 });

 document.getElementById("historyTable").innerHTML=html;
}


function addRequest(){

 let material=document.getElementById("reqMaterial").value;
 let qty=Number(document.getElementById("reqQty").value);

 if(!material || !qty){
  alert("Материал мен санын енгіз");
  return;
 }

 requests.unshift({
  material,
  qty,
  queue:document.getElementById("reqQueue").value,
  person:document.getElementById("reqPerson").value,
  date:document.getElementById("reqDate").value,
  supplier:document.getElementById("reqSupplier").value,
  note:document.getElementById("reqNote").value,
  status:"Күтуде"
 });

 save();
 renderAll();

 alert("Заявка қосылды.");
}


function renderRequests(){

 let html="";

 requests.forEach(r=>{
 html+=`
 <tr>
  <td>${r.material}</td>
  <td>${r.qty}</td>
  <td>${r.queue}-інші</td>
  <td>${r.status}</td>
 </tr>
 `;
 });

 document.getElementById("requestTable").innerHTML=html;
}


function addTool(){

 let name=document.getElementById("toolName").value;
 let id=document.getElementById("toolId").value;
 let holder=document.getElementById("toolHolder").value;

 if(!name){
  alert("Инструмент атауын енгіз");
  return;
 }

 tools.push({
  name,
  id,
  holder,
  status:holder?"У рабочего":"На складе"
 });

 save();
 renderAll();

 document.getElementById("toolName").value="";
 document.getElementById("toolId").value="";
 document.getElementById("toolHolder").value="";
}


function renderTools(){

 let html="";

 tools.forEach(t=>{
 html+=`
 <tr>
  <td>${t.name}</td>
  <td>${t.id}</td>
  <td>${t.holder||"—"}</td>
  <td>${t.status}</td>
 </tr>
 `;
 });

 document.getElementById("toolTable").innerHTML=html;
}


function renderDashboard(){

 document.getElementById("kpiItems").textContent=materials.length;
 document.getElementById("kpiOps").textContent=operations.length;
 document.getElementById("kpiReq").textContent=requests.length;
 document.getElementById("kpiTools").textContent=tools.length;
}


function renderAll(){

 renderStock();
 renderMaterialSelect();
 renderHistory();
 renderRequests();
 renderTools();
 renderDashboard();
}


function voiceCommand(){

 if(!("webkitSpeechRecognition" in window)){
  alert("Бұл браузерде дауыс тану қолжетімсіз.");
  return;
 }

 let recognition=new webkitSpeechRecognition();

 recognition.lang="ru-RU";
 recognition.continuous=false;
 recognition.interimResults=false;

 recognition.onstart=()=>{
  document.getElementById("jarvisMessage").textContent=
  "JARVIS тыңдап тұр...";
 };

 recognition.onresult=e=>{

  let text=e.results[0][0].transcript;

  document.getElementById("jarvisMessage").textContent=
  "Сіз айттыңыз: "+text;

  processVoice(text);
 };

 recognition.onerror=()=>{
  document.getElementById("jarvisMessage").textContent=
  "Дауыс командасын түсіне алмадым.";
 };

 recognition.start();
}


function processVoice(text){

 let t=text.toLowerCase();

 if(
  t.includes("қалдық") ||
  t.includes("остаток")
 ){

  let result=materials.map(m=>
   m.name+": "+(m.q4+m.q5)+" "+m.unit
  ).join("\n");

  document.getElementById("jarvisMessage").innerText=result;
  return;
 }

 if(t.includes("джарвис")){
  document.getElementById("jarvisMessage").innerText=
  "Иә. Командаңызды қабылдадым.";
 }
}


load();
renderAll();

</script>

</body>
</html>