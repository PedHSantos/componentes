<!
Lorenna Buriti N21 2B
Marcus Vinicius N22 2B
Matheus Yuji N24 2B
Pedro Henrique N27 2B
Winicius Cobo N36 2B
 - ->
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <title>Componentes</title>
    <meta charset="UTF-8">
    <style>
        canvas {
            border: 1px solid #d3d3d3;
            background-color: #A0A0A0;
        }
    </style>
    <script>
        var cor = 'blue';
        var cont = 1;
        var myGamePiece;
        var moveStep = 20;
        var intervalId;

        function startGame() {
            myGamePiece = new component(30, 30, "red", 10, 120);
            myGameArea.start();
        }

        var myGameArea = {
            canvas: document.createElement("canvas"),
            start: function() {
                this.canvas.width = 480;
                this.canvas.height = 270;
                this.context = this.canvas.getContext("2d");
                document.body.insertBefore(this.canvas, document.body.childNodes[0]);
                this.interval = setInterval(updateGameArea, 20);
            },
            clear: function() {
                this.context.clearRect(0, 0, this.canvas.width, this.canvas.height);
            }
        }

        function component(width, height, color, x, y) {
            this.width = width;
            this.height = height;
            this.x = x;
            this.y = y;
            this.update = function() {
                var ctx = myGameArea.context;
                ctx.fillStyle = cont % 10 === 0 ? 'red' : 'blue';
                ctx.fillRect(this.x, this.y, this.width, this.height);
                cont++;
            }
        }

        function updateGameArea() {
            myGameArea.clear();
            myGamePiece.update();
        }

        function moveUp() {
            myGamePiece.y = Math.max(0, myGamePiece.y - moveStep);
        }

        function moveDown() {
            myGamePiece.y = Math.min(myGameArea.canvas.height - myGamePiece.height, myGamePiece.y + moveStep);
        }

        function moveLeft() {
            myGamePiece.x = Math.max(0, myGamePiece.x - moveStep);
        }

        function moveRight() {
            myGamePiece.x = Math.min(myGameArea.canvas.width - myGamePiece.width, myGamePiece.x + moveStep);
        }

        function startMoving(direction) {
            if (intervalId) clearInterval(intervalId);
            intervalId = setInterval(() => {
                if (direction === 'up') moveUp();
                if (direction === 'down') moveDown();
                if (direction === 'left') moveLeft();
                if (direction === 'right') moveRight();
            }, 100);
        }

        function stopMoving() {
            clearInterval(intervalId);
        }
    </script>
</head>
<body onload="startGame();">
    <div>
        <button onmousedown="startMoving('up')" onmouseup="stopMoving()" onmouseleave="stopMoving()">Cima</button>
        <button onmousedown="startMoving('down')" onmouseup="stopMoving()" onmouseleave="stopMoving()">Baixo</button>
        <button onmousedown="startMoving('left')" onmouseup="stopMoving()" onmouseleave="stopMoving()">Esquerda</button>
        <button onmousedown="startMoving('right')" onmouseup="stopMoving()" onmouseleave="stopMoving()">Direita</button>
    </div>
</body>
</html>
