<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
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
    margin-top: 50px;
    font-size: 2rem;
    padding: 0 10px;
}

button {
    padding: 12px 24px;
    font-size: 1.2rem;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    position: absolute;
    z-index: 10;
}

#yes-button {
    background-color: #ff4d6d;
    color: white;
}

#no-button {
    background-color: #ccc;
}

#penguins {
    display: none;
    text-align: center;
    margin-top: 40px;
}

#penguins img {
    width: 80%;
    max-width: 300px;
    border-radius: 12px;
}

@media (max-width: 600px) {
    button {
        font-size: 1rem;
        padding: 10px 20px;
    }
}
</style>
</head>
<body>

<h1 id="question">Will you be my Valentine? ❤️</h1>

<button id="yes-button">Yes</button>
<button id="no-button">No</button>

<div id="penguins">
    <h2>Yay! ❤️</h2>
    <!-- Penguin GIF embedded directly -->
    <img src="https://media.giphy.com/media/3oriO0OEd9QIDdllqo/giphy.gif" alt="Hugging penguins">
</div>

<script>
window.addEventListener('load', function () {
    const question = document.getElementById('question');
    const yesButton = document.getElementById('yes-button');
    const noButton = document.getElementById('no-button');
    const penguins = document.getElementById('penguins');
    const speed = 15;

    // Place buttons below the question dynamically
    function positionButtons() {
        const questionRect = question.getBoundingClientRect();
        yesButton.style.top = questionRect.bottom + 20 + "px";
        yesButton.style.left = "40%";
        noButton.style.top = questionRect.bottom + 20 + "px";
        noButton.style.left = "55%";
    }

    positionButtons();

    // Function to move No button
    function moveNoButton(mouseX, mouseY) {
        const rect = noButton.getBoundingClientRect();
        const dx = mouseX - (rect.left + rect.width / 2);
        const dy = mouseY - (rect.top + rect.height / 2);
        const distance = Math.sqrt(dx*dx + dy*dy);

        if(distance < 100) {
            let newX = rect.left - dx / distance * speed;
            let newY = rect.top - dy / distance * speed;

            const questionBottom = question.getBoundingClientRect().bottom + 10;
            const maxX = window.innerWidth - rect.width;
            const maxY = window.innerHeight - rect.height;

            newX = Math.min(Math.max(0, newX), maxX);
            newY = Math.min(Math.max(questionBottom, newY), maxY);

            noButton.style.left = newX + "px";
            noButton.style.top = newY + "px";
        }
    }

    // Desktop: mouse move
    document.addEventListener('mousemove', function(e) {
        moveNoButton(e.clientX, e.clientY);
    });

    // Mobile: touch move
    document.addEventListener('touchmove', function(e) {
        if(e.touches.length > 0) {
            moveNoButton(e.touches[0].clientX, e.touches[0].clientY);
        }
    }, { passive: true });

    // Clicking Yes shows penguins
    yesButton.addEventListener('click', function() {
        question.style.display = 'none';
        yesButton.style.display = 'none';
        noButton.style.display = 'none';
        penguins.style.display = 'block';
    });

    // Reposition buttons on resize
    window.addEventListener('resize', positionButtons);
});
</script>

</body>
</html>
