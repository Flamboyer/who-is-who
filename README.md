[quien es quien.txt](https://github.com/user-attachments/files/25287815/quien.es.quien.txt)
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>¿Quién es Quién? Pro</title>

<style>
body {
    font-family: Arial, sans-serif;
    background: linear-gradient(-45deg, #1e1e2f, #2b2b50, #3a3a70, #1e1e2f);
    background-size: 400% 400%;
    animation: bgMove 12s ease infinite;
    color: white;
    text-align: center;
    margin: 0;
    padding: 20px;
}

@keyframes bgMove {
    0% {background-position: 0% 50%;}
    50% {background-position: 100% 50%;}
    100% {background-position: 0% 50%;}
}

h1 {
    margin-bottom: 10px;
}

#board {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
    gap: 20px;
    max-width: 1000px;
    margin: auto;
    perspective: 1000px;
}

.card {
    position: relative;
    width: 100%;
    height: 220px;
    transform-style: preserve-3d;
    transition: transform 0.6s, opacity 0.4s;
    cursor: pointer;
    animation: fadeIn 0.6s ease forwards;
}

.card-inner {
    position: absolute;
    width: 100%;
    height: 100%;
    background: #2d2d44;
    border-radius: 15px;
    padding: 10px;
    backface-visibility: hidden;
}

.card img {
    width: 100%;
    border-radius: 10px;
}

.card p {
    margin: 8px 0 0;
    font-weight: bold;
}

.card:hover {
    transform: scale(1.05) rotateY(5deg);
}

.card.eliminated {
    transform: rotateY(180deg);
    opacity: 0.4;
    filter: grayscale(100%);
}

button {
    margin: 15px 10px;
    padding: 12px 25px;
    border: none;
    border-radius: 10px;
    background: linear-gradient(45deg, #5865f2, #7b89ff);
    color: white;
    font-size: 16px;
    cursor: pointer;
    transition: transform 0.2s, box-shadow 0.2s;
}

button:hover {
    transform: scale(1.05);
    box-shadow: 0 0 15px rgba(123,137,255,0.7);
}

#secret {
    margin-top: 15px;
    font-size: 18px;
    color: #00ffcc;
}

@keyframes fadeIn {
    from {opacity: 0; transform: translateY(20px);}
    to {opacity: 1; transform: translateY(0);}
}
</style>
</head>

<body>

<h1>¿Quién es Quién?</h1>
<p>Haz clic en las cartas para eliminarlas.</p>

<div id="board"></div>

<button onclick="randomCharacter()">Elegir personaje secreto</button>
<button onclick="resetGame()">Reiniciar tablero</button>

<div id="secret"></div>

<audio id="flipSound" src="https://www.soundjay.com/buttons/sounds/button-16.mp3"></audio>

<script>
const characters = [
    { name: "Rey", img: "img/rey.png" },
    { name: "Princesa", img: "img/princesa.png" },
    { name: "Mago", img: "img/mago.png" },
    { name: "Mini P.E.K.K.A", img: "img/pekka.png" },
    { name: "Bruja", img: "img/bruja.png" },
    { name: "Gigante", img: "img/gigante.png" }
];

const board = document.getElementById("board");
const flipSound = document.getElementById("flipSound");

function createBoard() {
    board.innerHTML = "";
    characters.forEach((character, index) => {
        const card = document.createElement("div");
        card.classList.add("card");
        card.style.animationDelay = (index * 0.1) + "s";

        const inner = document.createElement("div");
        inner.classList.add("card-inner");

        inner.innerHTML = `
            <img src="${character.img}" alt="${character.name}">
            <p>${character.name}</p>
        `;

        card.appendChild(inner);

        card.onclick = () => {
            card.classList.toggle("eliminated");
            flipSound.currentTime = 0;
            flipSound.play();
        };

        board.appendChild(card);
    });
}

function randomCharacter() {
    const random = characters[Math.floor(Math.random() * characters.length)];
    document.getElementById("secret").innerText =
        "Tu personaje secreto es: " + random.name;
}

function resetGame() {
    createBoard();
    document.getElementById("secret").innerText = "";
}

createBoard();
</script>

</body>
</html>
