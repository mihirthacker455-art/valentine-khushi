const yesBtn = document.getElementById("yesBtn");
const noBtn = document.getElementById("noBtn");
const question = document.getElementById("question");
const music = document.getElementById("bgMusic");

/* NO button messages (looping) */
const noMessages = [
    "Are you sure? 🥺",
    "Think again 😢",
    "My heart is breaking 💔",
    "Don’t do this to me 😭",
    "Okay… restarting 😌"
];
let noIndex = 0;

/* Play music on first interaction */
document.body.addEventListener("click", () => {
    music.play();
}, { once: true });

/* NO button behaviour */
noBtn.addEventListener("mouseover", () => {
    const x = Math.random() * 70;
    const y = Math.random() * 70;

    noBtn.style.position = "absolute";
    noBtn.style.left = x + "%";
    noBtn.style.top = y + "%";

    question.style.opacity = 0;
    question.style.transform = "scale(0.9)";

    setTimeout(() => {
        question.textContent = noMessages[noIndex];
        question.style.opacity = 1;
        question.style.transform = "scale(1)";

        noIndex++;
        if (noIndex >= noMessages.length) {
            noIndex = 0;
            setTimeout(() => {
                question.textContent = "Khushi, will you be my Valentine? 💖";
            }, 800);
        }
    }, 300);
});

/* YES button */
yesBtn.addEventListener("click", () => {
    startConfetti();

    document.body.innerHTML = `
        <div style="
            height:100vh;
            display:flex;
            flex-direction:column;
            justify-content:center;
            align-items:center;
            background:linear-gradient(135deg,#ff9a9e,#fad0c4);
            text-align:center;
            padding:20px;
        ">
            <h1 style="
                font-family:'Pacifico',cursive;
                font-size:3.2rem;
                color:#ff2e63;
                animation: glowPulse 2.5s infinite;
            ">
                Khushi 💖
            </h1>

            <p style="
                font-size:1.4rem;
                margin-top:20px;
                color:#5f0f40;
                max-width:500px;
            ">
                I knew it 😌<br><br>
                Khushi, you just made my heart the happiest.
                Thank you for being my Valentine 🌸
            </p>

            <p style="
                font-size:1.2rem;
                margin-top:30px;
                color:#ff2e63;
            ">
                Forever grateful, forever smiling 💕
            </p>
        </div>
    `;
});

/* CONFETTI */
const canvas = document.getElementById("confetti");
const ctx = canvas.getContext("2d");
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

function startConfetti() {
    const pieces = [];
    for (let i = 0; i < 200; i++) {
        pieces.push({
            x: Math.random() * canvas.width,
            y: Math.random() * canvas.height,
            r: Math.random() * 6 + 4,
            d: Math.random() * 10,
            color: `hsl(${Math.random() * 360},100%,70%)`
        });
    }

    function draw() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        pieces.forEach(p => {
            ctx.beginPath();
            ctx.fillStyle = p.color;
            ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
            ctx.fill();
        });
        update();
    }

    function update() {
        pieces.forEach(p => {
            p.y += Math.cos(p.d) + 1;
            if (p.y > canvas.height) p.y = 0;
        });
        requestAnimationFrame(draw);
    }
    draw();
}
