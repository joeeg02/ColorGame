# ColorGame
Aquí encontrarás el código fuente de mi trabajo ColorGame
HTML:


<!DOCTYPE html>
<html lang="es">
    <head>
        <meta charset="UTF-8">
        <link rel="stylesheet" href="style.css">
    </head>
    <title>ColorGame</title>
    <body style="background-color: #232323;">
        <h1 id = "h1"> The Great <br> <span id="colorDisplay"></span> <br> Guessing Game <br>
        </h1>
        <div id="stripe">
            <button id="reset">Nuevos Colores</button>
            <span id="message"></span>
            <button class="selected" id="hard">HARD</button>
            <button id="easy">EASY</button>
        </div>
        <div class="container" style="margin: 0 auto;"> 
            <div class="square"></div>
            <div class="square"></div>
            <div class="square"></div>
            <div class="square"></div>
            <div class="square"></div>
            <div class="square"></div>
        </div> 
        <script src="colorgame.js"></script>
    </body>
</html>

-------------------------------------------------------------------------------------------------------

JAVASCRIPT:

console.log("Hola ColorGame");

let numberSquares = 6;
let colors = generateRandomColors(numberSquares);
let pickedColor;
let squares = document.querySelectorAll(".square");
let colorDisplay = document.querySelector("#colorDisplay");
let message = document.querySelector("#message");
let h1 = document.querySelector("h1");
let resetButton = document.querySelector("#reset");
let easy = document.querySelector("#easy");
let hard = document.querySelector("#hard");

reset();

function reset() {
    colors = generateRandomColors(numberSquares);
    pickedColor = pickColor();
    colorDisplay.textContent = pickedColor;
    for (let i = 0; i < squares.length; i++) {
        if (colors[i]) {
            squares[i].style.display = "block";
            squares[i].style.backgroundColor = colors[i];
        } else {
            squares[i].style.display = "none"; // Oculta los cuadrados extra
        }
    }
    message.textContent = "";
    h1.style.backgroundColor = "";
    resetButton.textContent = "Nuevos Colores";
}

for (let i = 0; i < squares.length; i++) {
    squares[i].addEventListener("click", function () {
        let clickedColor = squares[i].style.backgroundColor;
        if (clickedColor !== pickedColor) {
            squares[i].style.backgroundColor = "transparent";
            message.textContent = "Inténtalo nuevamente";
        } else {
            message.textContent = "¡Ganaste!";
            h1.style.backgroundColor = pickedColor;
            changeColors(pickedColor);
            resetButton.textContent = "Play Again?";
        }
    });
}

function changeColors(color) {
    for (let i = 0; i < squares.length; i++) {
        squares[i].style.backgroundColor = color;
    }
}

function pickColor() {
    let azar = Math.floor(Math.random() * colors.length);
    return colors[azar];
}

function randomColor() {
    let r = Math.floor(Math.random() * 256);
    let g = Math.floor(Math.random() * 256);
    let b = Math.floor(Math.random() * 256);
    return `rgb(${r}, ${g}, ${b})`;
}

function generateRandomColors(num) {
    let colores = [];
    for (let i = 0; i < num; i++) {
        colores.push(randomColor());
    }
    return colores;
}

resetButton.addEventListener("click", reset);

easy.addEventListener("click", function () {
    numberSquares = 3;
    reset();
    hard.classList.remove("selected");
    easy.classList.add("selected");
});

hard.addEventListener("click", function () {
  numberSquares = 6; 
  reset(); 
  hard.classList.add("selected"); 
  easy.classList.remove("selected"); 
})
