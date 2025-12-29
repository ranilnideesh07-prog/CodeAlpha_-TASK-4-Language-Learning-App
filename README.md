# CodeAlpha_-TASK-4-Language-Learning-App
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Language Learning App</title>

<style>
body {
    font-family: Arial, sans-serif;
    background: #f4f6f8;
    margin: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

.app {
    width: 380px;
    background: #ffffff;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 4px 10px rgba(0,0,0,0.1);
}

h2 {
    text-align: center;
}

.nav button {
    margin: 5px;
    padding: 6px 10px;
    border: none;
    border-radius: 5px;
    background: #007bff;
    color: white;
    cursor: pointer;
}

.card {
    border: 1px solid #ddd;
    padding: 15px;
    border-radius: 8px;
    margin-top: 15px;
    text-align: center;
}

.word {
    font-size: 20px;
    font-weight: bold;
}

.translation {
    margin-top: 10px;
    color: #555;
}

button {
    margin-top: 10px;
    padding: 7px 12px;
    border: none;
    border-radius: 5px;
    background: #28a745;
    color: white;
    cursor: pointer;
}

.quiz {
    margin-top: 15px;
}

input {
    width: 100%;
    padding: 6px;
    margin-top: 8px;
}
</style>
</head>

<body>

<div class="app">
    <h2>Language Learning</h2>

    <div class="nav">
        <button onclick="showSection('vocab')">Vocabulary</button>
        <button onclick="showSection('quiz')">Quiz</button>
        <button onclick="showSection('grammar')">Grammar</button>
    </div>

    <!-- Vocabulary Section -->
    <div id="vocab" class="section">
        <div class="card">
            <div class="word" id="word">Hola</div>
            <div class="translation" id="translation" style="display:none;">
                Hello (Spanish)
            </div>
            <button onclick="toggleTranslation()">Show Translation</button>
            <button onclick="nextWord()">Next</button>
        </div>
    </div>

    <!-- Quiz Section -->
    <div id="quiz" class="section" style="display:none;">
        <div class="quiz">
            <p>Translate: <b id="quizWord"></b></p>
            <input type="text" id="answer" placeholder="Your answer">
            <button onclick="checkAnswer()">Submit</button>
            <p id="result"></p>
        </div>
    </div>

    <!-- Grammar Section -->
    <div id="grammar" class="section" style="display:none;">
        <div class="card">
            <h4>Basic Grammar</h4>
            <p>Nouns: Name of a person, place or thing.</p>
            <p>Example: Casa (House)</p>
        </div>
    </div>
</div>

<script>
const words = [
    { word: "Hola", translation: "Hello" },
    { word: "Gracias", translation: "Thank you" },
    { word: "Amigo", translation: "Friend" },
    { word: "Casa", translation: "House" }
];

let index = 0;

function showSection(id) {
    document.querySelectorAll(".section").forEach(s => s.style.display = "none");
    document.getElementById(id).style.display = "block";
    if (id === "quiz") loadQuiz();
}

function toggleTranslation() {
    const t = document.getElementById("translation");
    t.style.display = t.style.display === "none" ? "block" : "none";
}

function nextWord() {
    index = (index + 1) % words.length;
    document.getElementById("word").innerText = words[index].word;
    document.getElementById("translation").innerText = words[index].translation;
    document.getElementById("translation").style.display = "none";
}

function loadQuiz() {
    const random = Math.floor(Math.random() * words.length);
    localStorage.setItem("quizIndex", random);
    document.getElementById("quizWord").innerText = words[random].word;
    document.getElementById("result").innerText = "";
    document.getElementById("answer").value = "";
}

function checkAnswer() {
    const i = localStorage.getItem("quizIndex");
    const user = document.getElementById("answer").value.toLowerCase();
    const correct = words[i].translation.toLowerCase();

    document.getElementById("result").innerText =
        user === correct ? "✅ Correct!" : "❌ Wrong! Answer: " + correct;
}
</script>

</body>
</html>
