<!DOCTYPE html>
<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Сердечки та Любов</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            background-color: black;
        }
        canvas {
            position: absolute;
            top: 0;
            left: 0;
        }
    </style>
</head>
<body>
    <canvas id="canvas"></canvas>
    <script>
        const canvas = document.getElementById("canvas");
        const ctx = canvas.getContext("2d");

        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        class Heart {
            constructor() {
                this.x = Math.random() * canvas.width;
                this.y = Math.random() * canvas.height - canvas.height;
                this.size = Math.random() * 20 + 10;
                this.speedY = Math.random() * 2 + 1;
                this.opacity = Math.random() * 0.5 + 0.5;
            }

            draw() {
                ctx.globalAlpha = this.opacity;
                ctx.fillStyle = "red";
                ctx.beginPath();
                ctx.moveTo(this.x, this.y);
                ctx.arc(this.x - this.size / 2, this.y, this.size / 2, Math.PI, 0, false);
                ctx.arc(this.x + this.size / 2, this.y, this.size / 2, Math.PI, 0, false);
                ctx.lineTo(this.x, this.y + this.size);
                ctx.closePath();
                ctx.fill();
                ctx.globalAlpha = 1;
            }

            update() {
                this.y += this.speedY;
                if (this.y > canvas.height) {
                    this.y = Math.random() * canvas.height - canvas.height;
                    this.x = Math.random() * canvas.width;
                    this.opacity = Math.random() * 0.5 + 0.5;
                }
            }
        }

        const hearts = [];
        for (let i = 0; i < 50; i++) {
            hearts.push(new Heart());
        }

        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            hearts.forEach(heart => {
                heart.update();
                heart.draw();
            });
            requestAnimationFrame(animate);
        }

        animate();

        canvas.addEventListener("click", () => {
            ctx.font = "50px Arial";
            ctx.fillStyle = "white";
            ctx.textAlign = "center";
            ctx.fillText("Я тебе люблю!", canvas.width / 2, canvas.height / 2);
        });

        window.addEventListener("resize", () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });
    </script>
</body>
</html>
