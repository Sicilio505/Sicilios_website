<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Feed the Cat</title>
    <style>
        body {
            text-align: center;
            font-family: Arial, sans-serif;
            background-color: #f8f9fa;
        }
        .container {
            position: relative;
            display: inline-block;
            margin-top: 50px;
        }
        .cat {
            width: 150px;
            height: auto;
        }
        .food {
            width: 100px;
            height: auto;
            position: absolute;
            top: -80px;
            left: 50%;
            transform: translateX(-50%);
            display: none;
        }
        .fireworks {
            display: none;
            font-size: 50px;
            color: red;
            position: absolute;
            top: -150px;
            left: 50%;
            transform: translateX(-50%);
        }
        .message {
            display: none;
            font-size: 24px;
            margin-top: 20px;
        }
        .final {
            display: none;
            font-size: 24px;
            margin-top: 20px;
            font-weight: bold;
            color: green;
        }
    </style>
</head>
<body>

    <h1>CLICK ON THE CAT</h1>
    <div class="container">
        <img src="https://upload.wikimedia.org/wikipedia/commons/3/3a/Cat03.jpg" class="cat" id="cat">
        <button id="feedButton" style="display: none;">FEED THE CAT</button>
        <img src="https://upload.wikimedia.org/wikipedia/commons/6/6a/Bowl_of_rice.jpg" class="food" id="food">
        <div class="fireworks" id="fireworks">🎆🎇🎆</div>
    </div>

    <div class="message" id="goodGirl">GOOD GIRL</div>
    <div class="final" id="goodnight">Goodnight</div>
    
    <script>
        let cat = document.getElementById("cat");
        let food = document.getElementById("food");
        let feedButton = document.getElementById("feedButton");
        let fireworks = document.getElementById("fireworks");
        let goodGirl = document.getElementById("goodGirl");
        let goodnight = document.getElementById("goodnight");

        cat.addEventListener("click", function() {
            feedButton.style.display = "block";
            food.style.display = "block";
        });

        feedButton.addEventListener("mousedown", function(event) {
            document.addEventListener("mousemove", moveFood);
        });

        document.addEventListener("mouseup", function() {
            document.removeEventListener("mousemove", moveFood);
            if (isOverlapping(cat, food)) {
                feedButton.style.display = "none";
                food.style.display = "none";
                goodGirl.style.display = "block";
                fireworks.style.display = "block";

                setTimeout(() => {
                    goodGirl.style.display = "none";
                    fireworks.style.display = "none";
                    goodnight.style.display = "block";
                }, 2000);
            }
        });

        function moveFood(event) {
            food.style.position = "absolute";
            food.style.left = event.pageX - 50 + "px";
            food.style.top = event.pageY - 50 + "px";
        }

        function isOverlapping(element1, element2) {
            let rect1 = element1.getBoundingClientRect();
            let rect2 = element2.getBoundingClientRect();

            return !(
                rect1.top > rect2.bottom ||
                rect1.bottom < rect2.top ||
                rect1.left > rect2.right ||
                rect1.right < rect2.left
            );
        }
    </script>

</body>
</html>