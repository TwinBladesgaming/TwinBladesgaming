body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: #020617;
    color: white;
    overflow-x: hidden;
}

/* HEADER */
header {
    text-align: center;
    padding: 20px;
}

/* LOGO */
.logo {
    width: 220px;
    max-width: 90%;
    animation: glow 2s infinite alternate;
}

@keyframes glow {
    from {
        filter: drop-shadow(0 0 5px #3b82f6);
    }
    to {
        filter: drop-shadow(0 0 20px #3b82f6);
    }
}

/* PAGE */
.page {
    display: none;
    padding: 15px;
}

.active {
    display: block;
}

/* CONTAINER */
.container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 20px;
}

/* CARD */
.card {
    width: 90%;
    max-width: 280px;
    background: #0f172a;
    border: 1px solid #3b82f6;
    border-radius: 14px;
    padding: 20px;
    text-align: center;
    transition: 0.3s;
    cursor: pointer;
}

.card:hover {
    transform: translateY(-5px);
    box-shadow: 0 0 20px #3b82f6;
}

/* TITLE */
#title {
    font-size: 32px;
    text-align: center;
    word-break: break-word;
    margin-bottom: 10px;
}

/* TEXT */
p, li, label {
    color: #cbd5e1;
}

/* BUTTON */
button {
    background: #1e293b;
    color: white;
    border: 1px solid #3b82f6;
    padding: 12px 24px;
    border-radius: 10px;
    cursor: pointer;
    transition: 0.3s;
}

button:hover {
    background: #2563eb;
}

/* NEON EFFECT */
.neon {
    background: #3b82f6;
    box-shadow: 0 0 20px #3b82f6;
}

/* SELECT */
select {
    width: 100%;
    max-width: 250px;
    padding: 10px;
    border-radius: 10px;
    background: #0f172a;
    color: white;
    border: 1px solid #3b82f6;
}

/* DOWNLOAD BOX */
.download-container {
    position: relative;
    display: inline-block;
    margin-top: 20px;
}

/* SWORDS */
.sword {
    position: absolute;
    width: 45px;
    top: -60px;
    opacity: 0;
}

.left {
    left: -30px;
}

.right {
    right: -30px;
}

.show .sword {
    animation: swordDrop 0.6s forwards;
    opacity: 1;
}

@keyframes swordDrop {
    from {
        top: -60px;
        transform: rotate(0deg);
    }

    to {
        top: 10px;
        transform: rotate(20deg);
    }
}

/* MOBILE FIX */
@media (max-width: 600px) {

    #title {
        font-size: 26px;
    }

    .logo {
        width: 180px;
    }

    .card {
        width: 85%;
    }
}
