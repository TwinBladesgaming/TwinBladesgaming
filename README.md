<!DOCTYPE html>
<html lang="en">

<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>TwinBladesGaming</title>

<style>

body{
    margin:0;
    font-family:Arial,sans-serif;
    background:#020617;
    color:white;
    overflow-x:hidden;
}

/* HEADER */
header{
    text-align:center;
    padding:20px;
}

/* LOGO */
.logo{
    width:220px;
    max-width:90%;
    animation:glow 2s infinite alternate;
}

@keyframes glow{
    from{
        filter:drop-shadow(0 0 5px #3b82f6);
    }
    to{
        filter:drop-shadow(0 0 20px #3b82f6);
    }
}

/* PAGES */
.page{
    display:none;
    padding:15px;
}

.active{
    display:block;
}

/* SECTION TITLE */
.section-title{
    text-align:center;
    font-size:32px;
    margin-bottom:20px;
}

/* CONTAINER */
.container{
    display:flex;
    flex-wrap:wrap;
    justify-content:center;
    gap:20px;
}

/* MODPACK CARD */
.card{
    width:90%;
    max-width:280px;
    background:#0f172a;
    border:1px solid #3b82f6;
    border-radius:15px;
    padding:20px;
    text-align:center;
    transition:0.3s;
    cursor:pointer;
}

.card:hover{
    transform:translateY(-5px);
    box-shadow:0 0 20px #3b82f6;
}

/* TEXT */
p,li,label{
    color:#cbd5e1;
}

/* BUTTON */
button{
    background:#1e293b;
    color:white;
    border:1px solid #3b82f6;
    padding:12px 24px;
    border-radius:10px;
    cursor:pointer;
    transition:0.3s;
}

button:hover{
    background:#2563eb;
}

/* NEON */
.neon{
    background:#3b82f6;
    box-shadow:0 0 20px #3b82f6;
}

/* SELECT */
select{
    width:100%;
    max-width:250px;
    padding:10px;
    border-radius:10px;
    background:#0f172a;
    color:white;
    border:1px solid #3b82f6;
}

/* DETAILS */
#title{
    text-align:center;
    font-size:30px;
}

/* DOWNLOAD */
.download-container{
    position:relative;
    display:inline-block;
    margin-top:20px;
}

/* SWORDS */
.sword{
    position:absolute;
    width:45px;
    top:-60px;
    opacity:0;
}

.left{
    left:-30px;
}

.right{
    right:-30px;
}

.show .sword{
    animation:swordDrop 0.6s forwards;
    opacity:1;
}

@keyframes swordDrop{
    from{
        top:-60px;
        transform:rotate(0deg);
    }

    to{
        top:10px;
        transform:rotate(20deg);
    }
}

/* AD BOX */
.ad-box{
    width:90%;
    max-width:700px;
    height:100px;
    margin:30px auto;
    border:1px dashed #3b82f6;
    display:flex;
    justify-content:center;
    align-items:center;
    color:#94a3b8;
    border-radius:12px;
}

/* MOBILE */
@media(max-width:600px){

    .logo{
        width:180px;
    }

    #title{
        font-size:24px;
    }

    .card{
        width:85%;
    }

}

</style>
</head>

<body>

<!-- HEADER -->
<header>
    <img src="logo.png" class="logo">
</header>

<!-- HOME PAGE -->
<div id="home" class="page active">

    <h1 class="section-title">TwinBlades Modpacks</h1>

    <!-- TOP AD -->
    <div class="ad-box">
        AD SPACE
    </div>

    <div class="container" id="modList"></div>

    <!-- BOTTOM AD -->
    <div class="ad-box">
        AD SPACE
    </div>

</div>

<!-- DETAILS PAGE -->
<div id="details" class="page">

    <button onclick="goBack()">⬅ Back</button>

    <h2 id="title"></h2>

    <p id="desc"></p>

    <!-- GAMEPLAY IMAGE -->
    <img id="gameplay"
         src=""
         style="width:100%;max-width:500px;border-radius:12px;display:block;margin:auto;">

    <br>

    <p><b>Requirements:</b></p>

    <ul id="req"></ul>

    <label>Select Minecraft Version</label><br>
    <select id="mc"></select>

    <br><br>

    <label>Select Modpack Version</label><br>
    <select id="modv"></select>

    <br><br>

    <!-- AD -->
    <div class="ad-box">
        AD SPACE
    </div>

    <!-- DOWNLOAD -->
    <div class="download-container" id="downloadBox">

        <img class="sword left"
             src="https://i.imgur.com/6X12UGK.png">

        <img class="sword right"
             src="https://i.imgur.com/6X12UGK.png">

        <button id="downloadBtn"
                onclick="activateDownload()">
            Download
        </button>

    </div>

</div>

<script>

/* MODPACK DATABASE */
const modpacks = [

{
    name:"BladeCraft",
    desc:"FPS + Combat Modpack",
    image:"https://images.unsplash.com/photo-1542751371-adc38448a05e",
    req:["Minecraft 1.20+","4GB RAM"],
    mc:["1.20","1.19"],
    versions:["v1.0","v2.0"],
    link:"https://yourlink1.com"
},

{
    name:"MagicWorld",
    desc:"Fantasy + Magic Mods",
    image:"https://images.unsplash.com/photo-1511512578047-dfb367046420",
    req:["Minecraft 1.19+","3GB RAM"],
    mc:["1.19"],
    versions:["v1.0"],
    link:"https://yourlink2.com"
}

];

let currentLink = "";

/* LOAD MODPACKS */
const container = document.getElementById("modList");

modpacks.forEach(mod => {

    const card = document.createElement("div");

    card.className = "card";

    card.innerHTML = `
        <h2>${mod.name}</h2>
        <p>${mod.desc}</p>
        <button>View Pack</button>
    `;

    card.onclick = () => openDetails(mod);

    container.appendChild(card);

});

/* OPEN DETAILS */
function openDetails(mod){

    document.getElementById("home").classList.remove("active");

    document.getElementById("details").classList.add("active");

    document.getElementById("title").innerText = mod.name;

    document.getElementById("desc").innerText = mod.desc;

    document.getElementById("gameplay").src = mod.image;

    /* REQUIREMENTS */
    let reqList = document.getElementById("req");

    reqList.innerHTML = "";

    mod.req.forEach(r => {

        let li = document.createElement("li");

        li.innerText = r;

        reqList.appendChild(li);

    });

    /* MC VERSION */
    let mc = document.getElementById("mc");

    mc.innerHTML = "";

    mod.mc.forEach(v => {

        let opt = document.createElement("option");

        opt.text = v;

        mc.add(opt);

    });

    /* MODPACK VERSION */
    let mv = document.getElementById("modv");

    mv.innerHTML = "";

    mod.versions.forEach(v => {

        let opt = document.createElement("option");

        opt.text = v;

        mv.add(opt);

    });

    currentLink = mod.link;

}

/* GO BACK */
function goBack(){

    document.getElementById("details").classList.remove("active");

    document.getElementById("home").classList.add("active");

}

/* DOWNLOAD */
function activateDownload(){

    const box = document.getElementById("downloadBox");

    const btn = document.getElementById("downloadBtn");

    btn.classList.add("neon");

    box.classList.add("show");

    setTimeout(() => {

        if(currentLink){

            window.open(currentLink, "_blank");

        }

    },700);

}

</script>

</body>
</html>
