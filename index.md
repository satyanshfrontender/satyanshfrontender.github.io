<!DOCTYPE html>
<html>
    <head>
        <title>Color Game</title>
        <style type="text/css">
            body{
                background-color: black;
                margin: 0;
                font-family: "Montserrat", "Avenir";
            }

            .square{
                width: 30%;
                background: purple;
                padding-bottom: 30%;
                float: left;
                margin: 0.67%;
                border-radius: 25%;
                transition: background-color 0.6s;
                -webkit-transition: background-color 0.6s;
                -moz-transition: background-color 0.6s;
            }

            #container{
                margin: 20px auto;
                max-width: 600px;
            }

            h1{
                color: whitesmoke;
                text-align: center;
                background-color: #4863A0;
                margin: 0;
                font-weight: normal;
                text-transform: uppercase;
                line-height: 1.1;
                padding: 20px 0;
            }
            
            #ColorDisplay{
                font-size: 200%;
            }
            #message{
                display: inline-block;
                width: 20%;
            }

            #stripe{
                background-color: whitesmoke;
                height: 30px;
                text-align: center;
            }
            
            .selected{
                background-color: blue;
            }

            button{
                border: none;
                background: none;
                text-transform: uppercase;
                height: 100%;
                font-weight: 700;
                color: steelblue;
                letter-spacing: 1px;
                font-size: inherit;
                transition: all 0.6s;
                outline: none;
            }

            button:hover{
                color: whitesmoke;
                background: steelblue;
            }

            </style>

    </head>
    <body>
        <h1>
            THE GREAT 
            <br>
            <span id="ColorDisplay">RGB</span> 
            <br>
            GAME</h1>
        
        <div id="stripe">
            <button id="reset"> New Colors</button>
            <button class="mode">Easy</button>
            <button class="mode selected">Hard</button>
            <span id="message"></span>
        </div>
        <div>
            <span id="message"></span>
        </div>

        <div id="container">
            <div class="square"></div>
            <div class="square"></div>
            <div class="square"></div>
            <div class="square"></div>
            <div class="square"></div>
            <div class="square"></div>    
        </div>

        <script type="text/javascript">
        var numSquares = 6;
            var colors = [];
            var pickedColor;
            var h1 = document.querySelector("h1");
            var squares = document.querySelectorAll(".square");
            var ColorDisplay = document.getElementById("ColorDisplay");
            var messageDisplay = document.querySelector("#message");
            var resetButton = document.querySelector("#reset");
            var modeButtons = document.querySelectorAll(".mode");


            init();

            function init() {
                setupModeButtons();
                setupSquares();
                reset();
            }

            function setupModeButtons() {
                for (var i = 0; i < modeButtons.length; i++) {
                    modeButtons[i].addEventListener("click", function () {
                        modeButtons[0].classList.remove("selected");
                        modeButtons[1].classList.remove("selected");
                        this.classList.add("selected");
                        this.textContent === "Easy" ? numSquares = 3 : numSquares = 6;
                        reset();
                    });
                }
            }

            function setupSquares() {
                for (var i = 0; i < squares.length; i++) {
                    //add click listeners
                    squares[i].addEventListener("click", function () {
                        //grab color of clicked sqaure
                        var clickedColor = this.style.backgroundColor;
                        //compare color to picked color
                        if (clickedColor === pickedColor) {
                            messageDisplay.textContent = "Correct";
                            resetButton.textContent = "Play Again";
                            changeColors(clickedColor);
                            h1.style.backgroundColor = clickedColor;
                        }
                        else {
                            this.style.backgroundColor = "black";
                            messageDisplay.textContent = "Try Again";
                        }
                    });
                }
            }


            function reset() {
                colors = generateRandomColors(numSquares);
                //ColorDisplay to match pickedColor
                pickedColor = pickColor();
                //Change color display to match picked color
                ColorDisplay.textContent = pickedColor;
                resetButton.textContent = "New Colors";
                messageDisplay.textContent = "";
                //change colors of square
                for (var i = 0; i < squares.length; i++) {
                    if (colors[i]) {
                        squares[i].style.display = "block";
                        squares[i].style.backgroundColor = colors[i];
                    }
                    else {
                        squares[i].style.display = "none";
                    }
                    squares[i].style.backgroundColor = colors[i];
                }
                h1.style.backgroundColor = "steelblue";
            }

            resetButton.addEventListener("click", function () {
                reset();
            })


            function changeColors(color) {
                for (var i = 0; i < squares.length; i++) {
                    squares[i].style.backgroundColor = color;
                }
            }

            function pickColor() {
                var range = Math.floor(Math.random() * colors.length);
                return colors[range];
            }

            function generateRandomColors(num) {
                var arr = [];
                for (var i = 0; i < num; i++) {
                    arr.push(randomColor())
                }
                return arr;
            }

            function randomColor() {
                var r = Math.floor(Math.random() * 256);
                var g = Math.floor(Math.random() * 256);
                var b = Math.floor(Math.random() * 256);
                return "rgb(" + r + ", " + g + ", " + b + ")";

            }
        </script>
        
    </body>
</html>
