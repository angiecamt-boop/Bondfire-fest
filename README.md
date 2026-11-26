# Bondfire-fest
JUEGO INTERACTIVO
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>¿Qué espíritu del Bonfire Night eres?</title>

<style>
*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Arial, sans-serif;
}

body{
background:linear-gradient(180deg,#1b1638,#2c1f59,#392c7c);
min-height:100vh;
display:flex;
justify-content:center;
align-items:center;
padding:20px;
color:white;
}

.container{
background:rgba(255,255,255,0.08);
backdrop-filter:blur(10px);
padding:30px;
border-radius:20px;
max-width:700px;
width:100%;
box-shadow:0 0 25px rgba(255,255,255,0.1);
}

h1{
text-align:center;
margin-bottom:15px;
color:#ffd166;
}

.subtitle{
text-align:center;
margin-bottom:30px;
}

.question{
display:none;
}

.question.active{
display:block;
}

.question h2{
margin-bottom:20px;
}

.option{
display:block;
width:100%;
padding:15px;
margin:10px 0;
border:none;
border-radius:12px;
background:#ffffff20;
color:white;
cursor:pointer;
transition:0.3s;
font-size:16px;
}

.option:hover{
background:#ff9f1c;
transform:scale(1.02);
}

.progress{
height:10px;
background:#ffffff20;
border-radius:20px;
margin-bottom:25px;
overflow:hidden;
}

.bar{
height:100%;
width:0%;
background:#ffd166;
transition:0.4s;
}

.result{
display:none;
text-align:center;
}

.result h2{
margin-bottom:15px;
}

.icon{
font-size:70px;
margin-bottom:15px;
}

.result-box{
padding:20px;
border-radius:15px;
margin-top:15px;
}

.restart{
margin-top:25px;
padding:12px 25px;
border:none;
border-radius:10px;
background:#ffd166;
color:#222;
font-weight:bold;
cursor:pointer;
}
</style>
</head>
<body>

<div class="container">

<h1>🔥 Bonfire Box</h1>
<p class="subtitle">Descubre qué espíritu del Bonfire Night eres</p>

<div class="progress">
<div class="bar" id="bar"></div>
</div>

<div id="quiz"></div>

<div class="result" id="result">
<div class="icon" id="icon"></div>
<h2 id="title"></h2>
<p id="description"></p>

<div class="result-box">
<h3>Mensaje secreto</h3>
<p id="secret"></p>
</div>

<button class="restart" onclick="location.reload()">
Volver a jugar
</button>
</div>

</div>

<script>

const questions = [

{
question:"Al llegar a una celebración, ¿qué haces primero?",
answers:[
{text:"Reunir a todos y animar el ambiente",type:"A"},
{text:"Buscar la atracción principal",type:"B"},
{text:"Observar las luces y decoración",type:"C"},
{text:"Investigar la historia del evento",type:"D"}
]
},

{
question:"¿Qué elemento del Bonfire Night te atrae más?",
answers:[
{text:"La gran hoguera",type:"A"},
{text:"Los fuegos artificiales",type:"B"},
{text:"Las linternas",type:"C"},
{text:"Las tradiciones",type:"D"}
]
},

{
question:"¿Qué recuerdo te llevarías?",
answers:[
{text:"Una antorcha simbólica",type:"A"},
{text:"Una foto del espectáculo",type:"B"},
{text:"Un farol decorativo",type:"C"},
{text:"Un libro histórico",type:"D"}
]
},

{
question:"¿Cómo prefieres aprender?",
answers:[
{text:"Participando en grupo",type:"A"},
{text:"Viviendo experiencias",type:"B"},
{text:"Por medio del arte",type:"C"},
{text:"Investigando y leyendo",type:"D"}
]
},

{
question:"¿Qué color te representa?",
answers:[
{text:"Naranja",type:"A"},
{text:"Azul brillante",type:"B"},
{text:"Dorado",type:"C"},
{text:"Morado",type:"D"}
]
}

];

let current = 0;

let scores = {
A:0,
B:0,
C:0,
D:0
};

const quiz = document.getElementById("quiz");
const bar = document.getElementById("bar");

function loadQuestion(){

bar.style.width=((current/questions.length)*100)+"%";

if(current >= questions.length){
showResult();
return;
}

const q = questions[current];

quiz.innerHTML = `
<div class="question active">
<h2>${current+1}. ${q.question}</h2>
${q.answers.map(answer=>
`<button class="option"
onclick="choose('${answer.type}')">
${answer.text}
</button>`
).join("")}
</div>
`;
}

function choose(type){
scores[type]++;
current++;
loadQuestion();
}

function showResult(){

bar.style.width="100%";

quiz.style.display="none";
document.getElementById("result").style.display="block";

const winner = Object.keys(scores).reduce((a,b)=>
scores[a]>scores[b]?a:b);

const results = {

A:{
icon:"🔥",
title:"Guardián de la Hoguera",
description:
"Eres quien reúne a las personas y mantiene viva la tradición.",
secret:
"Busca el símbolo 🔥 en la caja para descubrir un mensaje oculto."
},

B:{
icon:"🎆",
title:"Maestro de los Fuegos Artificiales",
description:
"Tu creatividad y energía convierten cualquier evento en un espectáculo.",
secret:
"Busca el símbolo 🎆 en la caja para desbloquear tu sorpresa."
},

C:{
icon:"🕯️",
title:"Portador de la Luz",
description:
"Aprecias los detalles, el diseño y el significado detrás de cada experiencia.",
secret:
"Busca el símbolo 🕯️ en la caja para encontrar tu recompensa."
},

D:{
icon:"🎭",
title:"Explorador de Tradiciones",
description:
"Te fascinan las historias, culturas y curiosidades del mundo.",
secret:
"Busca el símbolo 🎭 en la caja y descubre un dato exclusivo."
}

};

const result = results[winner];

document.getElementById("icon").innerHTML=result.icon;
document.getElementById("title").innerHTML=result.title;
document.getElementById("description").innerHTML=result.description;
document.getElementById("secret").innerHTML=result.secret;
}

loadQuestion();

</script>

</body>
</html>
