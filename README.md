<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Be My Valentine</title>
<style>
    html, body {
        width: 100%;
        height: 100%;
        margin: 0;
        font-family: Arial, sans-serif;
        background-color: #ffe6f0;
        overflow: hidden;
        position: relative;
    }

    h1 {
        text-align: center;
        margin-top: 80px;
    }

    button {
        padding: 12px 24px;
        font-size: 18px;
        border: none;
        border-radius: 8px;
        cursor: pointer;
        position: absolute;
    }

    #yes-button {
        background-color: #ff4d6d;
        color: white;
        top: 250px;
        left: 40%;
    }

    #no-button {
        background-color: #ccc;
        top: 250px;
        left: 55%;
    }

    #penguins {
        display: none;
        text-align: center;
        margin-top: 40px;
    }

    #penguins img {
        width: 250px;
        border-radius: 12px;
    }
</style>
</head>
<body>

<h1 id="question">Will you be my Valentine? ❤️</h1>

<button id="yes-button">Yes</button>
<button id="no-button">No</button>

<div id="penguins">
    <h2>Yay! ❤️</h2>
    <img src="https://media.giphy.com/media/3oriO0OEd9QIDdllqo/giphy.gif" alt="Hugging penguins">
</div>

<script>
window.addEventListener('load', function () {
    const noButton = document.getElementById('no-button');
    const yesButton = document.getElementById('yes-button');
    const penguins = document.getElementById('penguins');
    const question = document.getElementById('question');

    const speed = 15; // How fast the button moves

    // Move the No button away from the cursor
    document.addEventListener('mousemove', function(e) {
        const rect = noButton.getBoundingClientRect();
        const mouseX = e.clientX;
        const mouseY = e.clientY;

        // Distance between mouse and button center
        const dx = mouseX - (rect.left + rect.width / 2);
        const dy = mouseY - (rect.top + rect.height / 2);
        const distance = Math.sqrt(dx*dx + dy*dy);

        // If mouse is close, move the button
        if(distance < 100) { 
            let newX = rect.left - dx / distance * speed;
            let newY = rect.top - dy / distance * speed;

            // Keep button inside viewport
            const maxX = window.innerWidth - rect.width;
            const maxY = window.innerHeight - rect.height;
            newX = Math.min(Math.max(0, newX), maxX);
            newY = Math.min(Math.max(0, newY), maxY);

            noButton.style.left = newX + "px";
            noButton.style.top = newY + "px";
        }
    });

    // Clicking Yes shows penguins
    yesButton.addEventListener('click', function () {
        question.style.display = 'none';
        yesButton.style.display = 'none';
        noButton.style.display = 'none';
        penguins.style.display = 'block';
    });
});
</script>

</body>
</html>
