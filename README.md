# Software-Engineering
Bei Risiken oder Nebenwirkungen, lesen sie die Packungsbeilage oder Fragen sie einen Arzt oder Apotheker 

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Snake</title>
</head>
<body>

    <canvas  id="canvas" width="480" height="480"> 


    </canvas>

    <script>
        let canvas = document.getElementById("canvas");
        let ctx = canvas.getContext("2d");
        let rows = 20;
        let cols = 20;
        let snake= [
            
        {x: 19,y: 3 }
        
    
        ]; //Arrays und JSON
        let food;
        let cellWidth = canvas.width / cols;
        let cellHeight = canvas.height / rows;
        let direction = "LEFT";
        let foodcollected = false;

        placefood();
        
        setInterval(gameloop, 100);
        document.addEventListener("keydown", keyDown);


        draw();
       
            function draw(){
                ctx.fillStyle = "black";
                ctx.fillRect(0, 0, canvas.width, canvas.height);
                ctx.fillStyle = "white";
                
                snake.forEach(part => add(part.x, part.y));

                ctx.fillStyle = "lightgreen";
                add(food.x, food.y); // food

                requestAnimationFrame(draw);
               
            }

            function placefood(){
                let randomX = Math.floor(Math.random() * cols);
                let randomY = Math.floor(Math.random() * rows) ;

                food = {
                    x: randomX,
                    y: randomY

                };
            }


            function add( x, y){
                ctx.fillRect( x * cellWidth, y * cellHeight, cellWidth - 1, cellHeight - 1);


            }

            function shiftsnake(){
                for (let i = snake.length - 1; i > 0; i--) {
                    const part = snake[i];
                    const lastpart = snake[i - 1];
                    part.x = lastpart.x;
                    part.y = lastpart.y;
                    //???    
                }

            }

            function gameloop(){
                
                if (foodcollected){
                    snake = [{
                        x: snake[0].x, 
                        y:snake[0].y
                    }, ...snake];
                            //schlange erweitern
                    
                    foodcollected = false; 
                    //nach einer erweiterung aufhöhren zu addieren
                }

                shiftsnake();

                if (direction == "LEFT"){

                    snake[0].x--;
                }

                if (direction == "RIGHT"){

                 snake[0].x++;
                }
                if (direction == "UP"){

                    snake[0].y--;
                }
                if (direction == "DOWN"){

                    snake[0].y++;
                }
                    
                    
                if (snake[0].x == food.x && 
                    snake[0].y == food.y){
                        //futter einsammeln
                        foodcollected = true;
                        placefood();
                    }
                

               

            }

            function keyDown(e) {
                if(e.keyCode == 37){
                    direction = "LEFT";
                }
                if(e.keyCode == 38){
                    direction = "UP";
                }
                if(e.keyCode == 39){
                    direction = "RIGHT";
                }
                if(e.keyCode == 40){
                    direction = "DOWN";
                }
            }

    </script>

</body>
</html>
