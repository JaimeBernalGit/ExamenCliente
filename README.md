<!DOCTYPE html>
<html lang="en">
<head>
    <script src="https://t.contentsquare.net/uxa/84a293d804adf.js"></script>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <canvas id="canvas"></canvas>
</body>
</html>
<style>
    body {
        margin: 0;
        overflow-x: hidden;
    }
    #canvas {
        background: linear-gradient(-80deg, lightgreen, lightblue);
    }
</style>
<script>
    var canvas = document.getElementById("canvas");
    var c = canvas.getContext("2d");
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
    let raton = {
        x: undefined,
        y: undefined
    };
    class Cuadradito {
        constructor(x, y, dx, dy, longitud) {
        this.x = x;
        this.y = y;
        this.dx = dx;
        this.dy = dy;
        this.longitud = longitud;
        this.minLongitud = longitud;
        this.maxLongitud = longitud * 3;
        let r = Math.floor(Math.random() * 256);
        let g = Math.floor(Math.random() * 256);
        let b = Math.floor(Math.random() * 256);
        this.color = `rgb(${r}, ${g}, ${b})`;
    }
    dibuja() {
        c.beginPath();
        c.moveTo(this.x, this.y);
        c.lineTo(this.x + this.longitud, this.y);
        c.lineTo(this.x + this.longitud, this.y + this.longitud);
        c.lineTo(this.x, this.y + this.longitud);
        c.closePath();
        c.fillStyle = this.color;
        c.fill();
        this.actualiza();
        }
    actualiza() {
        if ( raton.x - this.x < 80 && raton.x - this.x > -80 && raton.y - this.y < 80 && raton.y - this.y > -80) {
            if (this.longitud < this.maxLongitud)
                this.longitud += 1;
            } else {
            if (this.longitud > this.minLongitud)
            this.longitud -= 1;
            }
            if ( this.x + this.longitud / 2 >= window.innerWidth || this.x - this.longitud / 2 <= 0) {
            this.dx = -this.dx;
            }
            if (this.y + this.longitud / 2 >= window.innerHeight || this.y - this.longitud / 2 <= 0) {
            this.dy = -this.dy;
            }
            this.x += this.dx;
            this.y += this.dy;
        }
    }
    let cuadraditos = [];
    for (let i = 0; i < 2800; i++) {
    let x = Math.random() * window.innerWidth;
    let y = Math.random() * window.innerHeight;
    let dx = (Math.random() - 0.5) * 1;
    let dy = (Math.random() - 0.5) * 1;
    let longitud = Math.random() * 20 + 4;
    cuadraditos.push(new Cuadradito(x, y, dx, dy, longitud));
    }
    function anima() {
        requestAnimationFrame(anima);
        c.clearRect(0, 0, window.innerWidth, window.innerHeight);
        cuadraditos.forEach(cuadradito => {
        cuadradito.dibuja();
        });
    }
    anima();



    window.addEventListener('mousemove', function (e) {
        raton.x = e.x;
        raton.y = e.y;
    });

    window.addEventListener('resize', function () {
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
    });
</script>
