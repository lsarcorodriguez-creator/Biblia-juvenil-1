<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Biblia Juvenil</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
:root{
  --bg:#f3f5ff;
  --card:#ffffff;
  --text:#222;
  --primary:#4b4bff;
}
.dark{
  --bg:#121212;
  --card:#1f1f1f;
  --text:#f1f1f1;
  --primary:#8f8fff;
}

body{
  margin:0;
  font-family:'Segoe UI',sans-serif;
  background:var(--bg);
  color:var(--text);
  transition:.3s;
}

header{
  background:url("https://images.unsplash.com/photo-1504052434569-70ad5836ab65") center/cover;
  color:white;
  text-align:center;
  padding:60px 20px;
}

.container{display:flex;}

main{
  flex:1;
  padding:20px;
  max-width:1200px;
}

aside{
  width:250px;
  background:var(--card);
  padding:20px;
  box-shadow:-3px 0 10px rgba(0,0,0,.1);
  position:sticky;
  top:0;
  height:100vh;
}

aside h3{color:var(--primary);}

aside button, select{
  width:100%;
  margin-bottom:10px;
  padding:10px;
  border:none;
  border-radius:10px;
  background:var(--primary);
  color:white;
  cursor:pointer;
}

#lector{
  background:var(--card);
  padding:25px;
  border-radius:15px;
  margin-bottom:30px;
}

#lector img{
  width:100%;
  max-height:300px;
  object-fit:cover;
  border-radius:15px;
  margin:10px 0;
}

.grid{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(150px,1fr));
  gap:15px;
}

.list{display:block;}

.book{
  background:var(--card);
  padding:15px;
  border-radius:12px;
  cursor:pointer;
  text-align:center;
  box-shadow:0 4px 10px rgba(0,0,0,.1);
  margin-bottom:10px;
}

.book img{
  width:40px;
  margin-bottom:6px;
}

h2{
  color:var(--primary);
  text-align:center;
}
</style>
</head>

<body>

<header>
<h1>📖 Biblia Juvenil</h1>
<p>Génesis a Apocalipsis • Palabra viva para hoy</p>
</header>

<div class="container">

<main>

<!-- TEXTO SUPERIOR -->
<div id="lector">
<h3>📘 Lectura Bíblica</h3>
<p>Selecciona un libro para comenzar.</p>
</div>

<h2>Antiguo Testamento</h2>
<div id="antiguo" class="grid"></div>

<h2>Nuevo Testamento</h2>
<div id="nuevo" class="grid"></div>

</main>

<!-- MENÚ LATERAL DERECHO -->
<aside>
<h3>⚙️ Configuración</h3>
<button onclick="modoGrid()">🟦 Cuadrícula</button>
<button onclick="modoList()">📋 Listado</button>
<button onclick="modoOscuro()">🌙 Modo Oscuro</button>

<h3>🌍 Idioma</h3>
<select onchange="alert('Idioma: '+this.value)">
  <option>Español</option>
  <option>English</option>
  <option>Português</option>
</select>

<p style="font-size:.85em;margin-top:20px;">
📖 Biblia Juvenil<br>
Salmos 119:105
</p>
</aside>

</div>

<script>
const librosAT=[
"Génesis","Éxodo","Levítico","Números","Deuteronomio","Josué","Jueces","Rut",
"1 Samuel","2 Samuel","1 Reyes","2 Reyes","1 Crónicas","2 Crónicas",
"Esdras","Nehemías","Ester","Job","Salmos","Proverbios","Eclesiastés",
"Cantares","Isaías","Jeremías","Lamentaciones","Ezequiel","Daniel","Oseas",
"Joel","Amós","Abdías","Jonás","Miqueas","Nahúm","Habacuc","Sofonías",
"Hageo","Zacarías","Malaquías"
];

const librosNT=[
"Mateo","Marcos","Lucas","Juan","Hechos","Romanos","1 Corintios",
"2 Corintios","Gálatas","Efesios","Filipenses","Colosenses",
"1 Tesalonicenses","2 Tesalonicenses","1 Timoteo","2 Timoteo",
"Tito","Filemón","Hebreos","Santiago","1 Pedro","2 Pedro",
"1 Juan","2 Juan","3 Juan","Judas","Apocalipsis"
];

const personajes={
"Génesis":["Adán","Noé","Abraham"],
"Éxodo":["Moisés"],"Levítico":["Aarón"],"Números":["Moisés"],
"Deuteronomio":["Moisés"],"Josué":["Josué"],
"Jueces":["Débora","Gedeón","Sansón"],"Rut":["Rut"],
"1 Samuel":["Samuel"],"2 Samuel":["David"],
"1 Reyes":["Salomón"],"2 Reyes":["Elías"],
"1 Crónicas":["David"],"2 Crónicas":["Salomón"],
"Esdras":["Esdras"],"Nehemías":["Nehemías"],"Ester":["Ester"],
"Job":["Job"],"Salmos":["David"],"Proverbios":["Salomón"],
"Eclesiastés":["Salomón"],"Cantares":["Salomón"],
"Isaías":["Isaías"],"Jeremías":["Jeremías"],
"Lamentaciones":["Jeremías"],"Ezequiel":["Ezequiel"],
"Daniel":["Daniel"],"Oseas":["Oseas"],"Joel":["Joel"],
"Amós":["Amós"],"Abdías":["Abdías"],"Jonás":["Jonás"],
"Miqueas":["Miqueas"],"Nahúm":["Nahúm"],
"Habacuc":["Habacuc"],"Sofonías":["Sofonías"],
"Hageo":["Hageo"],"Zacarías":["Zacarías"],
"Malaquías":["Malaquías"],
"Mateo":["Jesús"],"Marcos":["Jesús"],"Lucas":["Jesús"],
"Juan":["Jesús"],"Hechos":["Pedro","Pablo"],
"Romanos":["Pablo"],"1 Corintios":["Pablo"],
"2 Corintios":["Pablo"],"Gálatas":["Pablo"],
"Efesios":["Pablo"],"Filipenses":["Pablo"],
"Colosenses":["Pablo"],"1 Tesalonicenses":["Pablo"],
"2 Tesalonicenses":["Pablo"],"1 Timoteo":["Pablo"],
"2 Timoteo":["Pablo"],"Tito":["Pablo"],
"Filemón":["Pablo"],"Hebreos":["Jesucristo"],
"Santiago":["Santiago"],"1 Pedro":["Pedro"],
"2 Pedro":["Pedro"],"1 Juan":["Juan"],
"2 Juan":["Juan"],"3 Juan":["Juan"],
"Judas":["Judas"],"Apocalipsis":["Jesucristo"]
};

function crear(lista,id){
  const c=document.getElementById(id);
  lista.forEach(l=>{
    let d=document.createElement("div");
    d.className="book";
    d.innerHTML=`<img src="https://cdn-icons-png.flaticon.com/512/29/29302.png"><strong>${l}</strong>`;
    d.onclick=()=>leer(l);
    c.appendChild(d);
  });
}

function leer(libro){
  const pers=personajes[libro];
  const elegido=pers[Math.floor(Math.random()*pers.length)];
  document.getElementById("lector").innerHTML=`
    <h3>${libro}</h3>
    <p><b>Personaje principal:</b> ${pers.join(", ")}</p>
    <img src="https://source.unsplash.com/800x400/?${elegido},bible">
    <p>
      En <b>${libro}</b>, Dios usa la vida de <b>${elegido}</b> para enseñarnos
      fe, obediencia y esperanza para nuestro tiempo.
    </p>
    <blockquote>
      “Tu palabra es una lámpara a mis pies.” – Salmos 119:105
    </blockquote>
  `;
  window.scrollTo({top:0,behavior:"smooth"});
}

function modoGrid(){
  document.querySelectorAll("#antiguo,#nuevo").forEach(e=>e.className="grid");
}
function modoList(){
  document.querySelectorAll("#antiguo,#nuevo").forEach(e=>e.className="list");
}
function modoOscuro(){
  document.body.classList.toggle("dark");
}

crear(librosAT,"antiguo");
crear(librosNT,"nuevo");
</script>

</body>
</html>

