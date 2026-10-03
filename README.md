<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Random Quiz Challenge</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

body{
    min-height:100vh;
    font-family:Arial, sans-serif;
    background:#07111f;
    color:white;
    display:flex;
    justify-content:center;
    align-items:center;
    padding:20px;
    overflow-x:hidden;
}

/* Animated Background */

body::before,
body::after{
    content:"";
    position:fixed;
    width:400px;
    height:400px;
    border-radius:50%;
    filter:blur(100px);
    opacity:.15;
    z-index:-1;
    animation:float 8s infinite alternate;
}

body::before{
    background:#00d9ff;
    top:-150px;
    left:-150px;
}

body::after{
    background:#7b2cff;
    bottom:-150px;
    right:-150px;
    animation-delay:2s;
}

@keyframes float{
    from{
        transform:translate(0,0);
    }
    to{
        transform:translate(80px,50px);
    }
}

.container{
    width:min(850px,100%);
}

/* Header */

.header{
    text-align:center;
    margin-bottom:25px;
}

.badge{
    display:inline-block;
    padding:7px 15px;
    border:1px solid #4ddfff;
    border-radius:30px;
    color:#4ddfff;
    font-size:11px;
    letter-spacing:2px;
    margin-bottom:15px;
}

h1{
    font-size:clamp(36px,6vw,60px);
}

h1 span{
    color:#4ddfff;
}

.header p{
    color:#8290a5;
    margin-top:10px;
}

/* HUD */

.hud{
    display:flex;
    justify-content:space-between;
    gap:12px;
    margin-bottom:15px;
}

.hud-box{
    flex:1;
    background:#0d1929;
    border:1px solid #20334c;
    border-radius:13px;
    padding:12px 18px;
}

.hud-box small{
    display:block;
    color:#718097;
    font-size:10px;
    letter-spacing:1px;
    margin-bottom:4px;
}

.hud-box strong{
    color:#4ddfff;
    font-size:21px;
}

/* Progress */

.progress-area{
    margin-bottom:15px;
}

.progress-text{
    display:flex;
    justify-content:space-between;
    font-size:11px;
    color:#718097;
    margin-bottom:6px;
}

.progress{
    height:6px;
    background:#17263a;
    border-radius:20px;
    overflow:hidden;
}

.progress-bar{
    height:100%;
    width:0%;
    background:#4ddfff;
    transition:.4s;
}

/* Card */

.card{
    background:rgba(13,25,41,.96);
    border:1px solid #243951;
    border-radius:25px;
    padding:35px;
    box-shadow:0 25px 80px rgba(0,0,0,.4);
    text-align:center;
}

/* Category */

.category{
    display:inline-block;
    padding:7px 13px;
    background:#12253a;
    border:1px solid #29445f;
    border-radius:20px;
    color:#4ddfff;
    font-size:11px;
    letter-spacing:1px;
    margin-bottom:20px;
}

/* Question */

.question-number{
    color:#66768c;
    font-size:12px;
    margin-bottom:12px;
}

.question{
    font-size:clamp(22px,4vw,31px);
    line-height:1.35;
    font-weight:bold;
    min-height:85px;
    display:flex;
    justify-content:center;
    align-items:center;
}

/* Answers */

.answers{
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:12px;
    margin-top:25px;
}

.answer{
    position:relative;
    border:1px solid #29405b;
    background:#101f32;
    color:white;
    padding:17px 15px;
    border-radius:13px;
    cursor:pointer;
    font-size:15px;
    transition:.2s;
}

.answer:hover{
    border-color:#4ddfff;
    background:#132b43;
    transform:translateY(-3px);
}

.answer.correct{
    background:#075c49;
    border-color:#00ffc8;
    animation:correct .35s;
}

.answer.wrong{
    background:#652638;
    border-color:#ff526b;
    animation:shake .35s;
}

@keyframes correct{
    50%{
        transform:scale(1.04);
    }
}

@keyframes shake{
    25%{transform:translateX(-6px);}
    50%{transform:translateX(6px);}
    75%{transform:translateX(-4px);}
}

/* Feedback */

.feedback{
    min-height:30px;
    margin-top:18px;
    font-size:14px;
    font-weight:bold;
}

/* Next Button */

.next{
    display:none;
    margin:15px auto 0;
    padding:13px 27px;
    border:0;
    border-radius:11px;
    background:#4ddfff;
    color:#031019;
    font-weight:bold;
    cursor:pointer;
    transition:.2s;
}

.next:hover{
    transform:translateY(-2px);
    box-shadow:0 8px 25px rgba(77,223,255,.2);
}

.next.show{
    display:block;
}

/* Result */

.result{
    display:none;
}

.result.show{
    display:block;
}

.result-icon{
    font-size:70px;
    margin-bottom:10px;
}

.result h2{
    font-size:32px;
    color:#4ddfff;
}

.result p{
    color:#8190a5;
    margin-top:10px;
}

.final-score{
    font-size:52px;
    font-weight:bold;
    margin:20px 0;
}

.restart{
    border:0;
    padding:14px 28px;
    border-radius:11px;
    background:#4ddfff;
    color:#031019;
    font-weight:bold;
    cursor:pointer;
    margin-top:20px;
}

/* Start Screen */

.start-screen{
    text-align:center;
}

.start-screen .big-icon{
    font-size:80px;
    margin-bottom:15px;
}

.start-screen h2{
    font-size:30px;
    margin-bottom:10px;
}

.start-screen p{
    color:#8190a5;
    line-height:1.6;
}

.start-btn{
    margin-top:25px;
    border:0;
    padding:15px 35px;
    border-radius:12px;
    background:#4ddfff;
    color:#031019;
    font-weight:bold;
    cursor:pointer;
    font-size:15px;
}

/* Mobile */

@media(max-width:600px){

    body{
        padding:12px;
    }

    .card{
        padding:25px 15px;
    }

    .answers{
        grid-template-columns:1fr;
    }

    .hud-box{
        padding:10px;
    }

    .question{
        min-height:110px;
    }
}
</style>
</head>

<body>

<div class="container">

    <!-- HEADER -->

    <div class="header">

        <div class="badge">
            RANDOM KNOWLEDGE CHALLENGE
        </div>

        <h1>
            Brain <span>Rush</span> 🧠
        </h1>

        <p>
            Different questions. Every round. No pattern.
        </p>

    </div>


    <!-- HUD -->

    <div class="hud">

        <div class="hud-box">
            <small>SCORE</small>
            <strong id="score">0</strong>
        </div>

        <div class="hud-box">
            <small>QUESTION</small>
            <strong>
                <span id="current">1</span>/10
            </strong>
        </div>

        <div class="hud-box">
            <small>STREAK</small>
            <strong id="streak">0 🔥</strong>
        </div>

    </div>


    <!-- PROGRESS -->

    <div class="progress-area">

        <div class="progress-text">
            <span>QUIZ PROGRESS</span>
            <span id="progressText">0%</span>
        </div>

        <div class="progress">
            <div
                class="progress-bar"
                id="progressBar">
            </div>
        </div>

    </div>


    <!-- GAME -->

    <div class="card" id="gameCard">

        <div class="category" id="category">
            CATEGORY
        </div>

        <div class="question-number">
            QUESTION
        </div>

        <div class="question" id="question">
            Loading...
        </div>

        <div class="answers" id="answers">
        </div>

        <div class="feedback" id="feedback">
        </div>

        <button
            class="next"
            id="nextBtn"
            onclick="nextQuestion()">

            NEXT QUESTION →

        </button>

    </div>


    <!-- RESULT -->

    <div class="card result" id="result">

        <div class="result-icon">
            🏆
        </div>

        <h2>
            Quiz Complete!
        </h2>

        <p>
            Your final score
        </p>

        <div
            class="final-score"
            id="finalScore">
            0 / 100
        </div>

        <p id="resultMessage">
        </p>

        <button
            class="restart"
            onclick="location.reload()">

            PLAY AGAIN 🔄

        </button>

    </div>

</div>


<script>

/* =====================================================
   QUESTION DATABASE
   ===================================================== */

const questionBank = [

    /* SCIENCE */

    {
        category:"🔬 SCIENCE",
        question:"What gas do humans need to breathe to survive?",
        answers:["Oxygen","Carbon Dioxide","Hydrogen","Helium"],
        correct:"Oxygen"
    },

    {
        category:"🔬 SCIENCE",
        question:"What is H₂O commonly known as?",
        answers:["Salt","Water","Oxygen","Hydrogen"],
        correct:"Water"
    },

    {
        category:"🔬 SCIENCE",
        question:"What force keeps us on the ground?",
        answers:["Magnetism","Gravity","Friction","Electricity"],
        correct:"Gravity"
    },

    {
        category:"🔬 SCIENCE",
        question:"What is the hardest natural substance?",
        answers:["Gold","Iron","Diamond","Silver"],
        correct:"Diamond"
    },

    {
        category:"🔬 SCIENCE",
        question:"Which organ pumps blood around the human body?",
        answers:["Brain","Liver","Heart","Lung"],
        correct:"Heart"
    },


    /* SPACE */

    {
        category:"🚀 SPACE",
        question:"Which planet is known as the Red Planet?",
        answers:["Venus","Mars","Jupiter","Mercury"],
        correct:"Mars"
    },

    {
        category:"🚀 SPACE",
        question:"How many planets are in our Solar System?",
        answers:["7","8","9","10"],
        correct:"8"
    },

    {
        category:"🚀 SPACE",
        question:"What is the closest star to Earth?",
        answers:["Sirius","The Sun","Polaris","Vega"],
        correct:"The Sun"
    },

    {
        category:"🚀 SPACE",
        question:"Which planet is famous for its large rings?",
        answers:["Saturn","Mars","Venus","Earth"],
        correct:"Saturn"
    },

    {
        category:"🚀 SPACE",
        question:"What is Earth's natural satellite?",
        answers:["Mars","Moon","Sun","Venus"],
        correct:"Moon"
    },


    /* ANIMALS */

    {
        category:"🐾 ANIMALS",
        question:"What is the largest land animal?",
        answers:["Elephant","Giraffe","Rhino","Hippo"],
        correct:"Elephant"
    },

    {
        category:"🐾 ANIMALS",
        question:"Which animal is known as the King of the Jungle?",
        answers:["Tiger","Lion","Leopard","Bear"],
        correct:"Lion"
    },

    {
        category:"🐾 ANIMALS",
        question:"How many legs does a spider have?",
        answers:["6","8","10","12"],
        correct:"8"
    },

    {
        category:"🐾 ANIMALS",
        question:"Which animal is famous for changing its color?",
        answers:["Elephant","Chameleon","Horse","Penguin"],
        correct:"Chameleon"
    },

    {
        category:"🐾 ANIMALS",
        question:"Which is the fastest land animal?",
        answers:["Lion","Cheetah","Horse","Tiger"],
        correct:"Cheetah"
    },


    /* SPORTS */

    {
        category:"🏆 SPORTS",
        question:"How many players are on a cricket team?",
        answers:["9","10","11","12"],
        correct:"11"
    },

    {
        category:"🏆 SPORTS",
        question:"How many rings are on the Olympic flag?",
        answers:["4","5","6","7"],
        correct:"5"
    },

    {
        category:"🏆 SPORTS",
        question:"Which sport uses a racket and shuttlecock?",
        answers:["Tennis","Badminton","Squash","Golf"],
        correct:"Badminton"
    },

    {
        category:"🏆 SPORTS",
        question:"How many players are on the field for one soccer team?",
        answers:["9","10","11","12"],
        correct:"11"
    },

    {
        category:"🏆 SPORTS",
        question:"Which country is famous for the sport of sumo?",
        answers:["China","Japan","Korea","Thailand"],
        correct:"Japan"
    },


    /* HISTORY */

    {
        category:"🏛️ HISTORY",
        question:"Who was the first person to walk on the Moon?",
        answers:["Neil Armstrong","Albert Einstein","Elon Musk","Buzz Aldrin"],
        correct:"Neil Armstrong"
    },

    {
        category:"🏛️ HISTORY",
        question:"Which ancient civilization built the pyramids of Giza?",
        answers:["Romans","Egyptians","Greeks","Vikings"],
        correct:"Egyptians"
    },

    {
        category:"🏛️ HISTORY",
        question:"Which ship famously sank in 1912?",
        answers:["Titanic","Mayflower","Victoria","Endeavour"],
        correct:"Titanic"
    },

    {
        category:"🏛️ HISTORY",
        question:"Who painted the Mona Lisa?",
        answers:["Van Gogh","Leonardo da Vinci","Picasso","Michelangelo"],
        correct:"Leonardo da Vinci"
    },


    /* WORLD */

    {
        category:"🌍 WORLD",
        question:"Which is the largest ocean on Earth?",
        answers:["Atlantic","Indian","Pacific","Arctic"],
        correct:"Pacific"
    },

    {
        category:"🌍 WORLD",
        question:"Which is the largest continent?",
        answers:["Africa","Asia","Europe","North America"],
        correct:"Asia"
    },

    {
        category:"🌍 WORLD",
        question:"Which country is famous for the Eiffel Tower?",
        answers:["Italy","France","Spain","Germany"],
        correct:"France"
    },

    {
        category:"🌍 WORLD",
        question:"Which country is shaped like a boot?",
        answers:["Greece","Italy","Portugal","Spain"],
        correct:"Italy"
    },

    {
        category:"🌍 WORLD",
        question:"Which country is home to the Great Wall?",
        answers:["Japan","China","India","Korea"],
        correct:"China"
    },


    /* SRI LANKA */

    {
        category:"🇱🇰 SRI LANKA",
        question:"What is the capital city of Sri Lanka?",
        answers:["Colombo","Kandy","Sri Jayawardenepura Kotte","Galle"],
        correct:"Sri Jayawardenepura Kotte"
    },

    {
        category:"🇱🇰 SRI LANKA",
        question:"Which animal is the national animal of Sri Lanka?",
        answers:["Elephant","Lion","Leopard","Peacock"],
        correct:"Elephant"
    },

    {
        category:"🇱🇰 SRI LANKA",
        question:"Which city is famous for the Temple of the Tooth?",
        answers:["Galle","Kandy","Jaffna","Colombo"],
        correct:"Kandy"
    },

    {
        category:"🇱🇰 SRI LANKA",
        question:"What is Sri Lanka famous for producing?",
        answers:["Tea","Wheat","Coffee only","Corn only"],
        correct:"Tea"
    },

    {
        category:"🇱🇰 SRI LANKA",
        question:"Which ocean surrounds Sri Lanka?",
        answers:["Atlantic Ocean","Indian Ocean","Pacific Ocean","Arctic Ocean"],
        correct:"Indian Ocean"
    },


    /* FOOD */

    {
        category:"🍕 FOOD",
        question:"Which country is famous for pizza?",
        answers:["Italy","India","Brazil","Japan"],
        correct:"Italy"
    },

    {
        category:"🍔 FOOD",
        question:"What is the main ingredient in traditional sushi?",
        answers:["Rice","Potato","Bread","Corn"],
        correct:"Rice"
    },

    {
        category:"🍫 FOOD",
        question:"Chocolate is mainly made from what?",
        answers:["Cocoa beans","Coffee beans","Rice","Milk"],
        correct:"Cocoa beans"
    },

    {
        category:"🍯 FOOD",
        question:"Which insect produces honey?",
        answers:["Ant","Bee","Butterfly","Fly"],
        correct:"Bee"
    },


    /* NATURE */

    {
        category:"🌿 NATURE",
        question:"What is the process by which plants make food?",
        answers:["Digestion","Photosynthesis","Respiration","Fermentation"],
        correct:"Photosynthesis"
    },

    {
        category:"🌿 NATURE",
        question:"Which is the largest rainforest in the world?",
        answers:["Amazon","Congo","Daintree","Borneo"],
        correct:"Amazon"
    },

    {
        category:"🌿 NATURE",
        question:"What do bees collect from flowers?",
        answers:["Sand","Nectar","Leaves","Water"],
        correct:"Nectar"
    },

    {
        category:"🌿 NATURE",
        question:"Which season is usually the coldest?",
        answers:["Summer","Spring","Winter","Autumn"],
        correct:"Winter"
    },


    /* MOVIES */

    {
        category:"🎬 MOVIES",
        question:"Which movie features the character Jack Dawson?",
        answers:["Titanic","Avatar","Inception","Joker"],
        correct:"Titanic"
    },

    {
        category:"🎬 MOVIES",
        question:"Which superhero uses a shield with a star?",
        answers:["Iron Man","Batman","Captain America","Thor"],
        correct:"Captain America"
    },

    {
        category:"🎬 MOVIES",
        question:"Which movie features a magical school called Hogwarts?",
        answers:["Harry Potter","The Matrix","Avatar","Frozen"],
        correct:"Harry Potter"
    },

    {
        category:"🎬 MOVIES",
        question:"Which superhero is also known as the Dark Knight?",
        answers:["Superman","Batman","Spider-Man","Hulk"],
        correct:"Batman"
    },


    /* GENERAL */

    {
        category:"🧠 GENERAL",
        question:"How many days are there in a leap year?",
        answers:["364","365","366","367"],
        correct:"366"
    },

    {
        category:"🧠 GENERAL",
        question:"How many colors are traditionally in a rainbow?",
        answers:["5","6","7","8"],
        correct:"7"
    },

    {
        category:"🧠 GENERAL",
        question:"How many sides does a triangle have?",
        answers:["2","3","4","5"],
        correct:"3"
    },

    {
        category:"🧠 GENERAL",
        question:"Which instrument has black and white keys?",
        answers:["Guitar","Piano","Violin","Drum"],
        correct:"Piano"
    },

    {
        category:"🧠 GENERAL",
        question:"How many minutes are in one hour?",
        answers:["30","45","60","90"],
        correct:"60"
    }

];


/* =====================================================
   GAME VARIABLES
   ===================================================== */

let questions = [];
let currentQuestion = 0;
let score = 0;
let streak = 0;
let answered = false;


/* =====================================================
   SHUFFLE FUNCTION
   ===================================================== */

function shuffle(array){

    return array.sort(() => Math.random() - 0.5);

}


/* =====================================================
   START GAME
   ===================================================== */

function startGame(){

    /*
       Select 10 random questions
       from the entire question database.
    */

    questions =
        shuffle([...questionBank])
        .slice(0,10);

    currentQuestion = 0;
    score = 0;
    streak = 0;

    document.getElementById("score").innerText = score;
    document.getElementById("streak").innerText = "0 🔥";

    loadQuestion();

}


/* =====================================================
   LOAD QUESTION
   ===================================================== */

function loadQuestion(){

    answered = false;

    const q =
        questions[currentQuestion];

    document.getElementById("current")
        .innerText = currentQuestion + 1;

    document.getElementById("category")
        .innerText = q.category;

    document.getElementById("question")
        .innerText = q.question;

    document.getElementById("feedback")
        .innerText = "";

    document.getElementById("nextBtn")
        .classList.remove("show");


    /* Progress */

    const progress =
        (currentQuestion / questions.length) * 100;

    document.getElementById("progressBar")
        .style.width = progress + "%";

    document.getElementById("progressText")
        .innerText = Math.round(progress) + "%";


    /* Answers */

    const answersContainer =
        document.getElementById("answers");

    answersContainer.innerHTML = "";


    const shuffledAnswers =
        shuffle([...q.answers]);


    shuffledAnswers.forEach(answer => {

        const button =
            document.createElement("button");

        button.className = "answer";

        button.innerText = answer;

        button.onclick =
            () => checkAnswer(button,answer);

        answersContainer.appendChild(button);

    });

}


/* =====================================================
   CHECK ANSWER
   ===================================================== */

function checkAnswer(button,answer){

    if(answered) return;

    answered = true;

    const q =
        questions[currentQuestion];


    /* CORRECT */

    if(answer === q.correct){

        button.classList.add("correct");

        streak++;

        /*
           Normal = 10 points
           Streak bonus = +5
        */

        let points = 10;

        if(streak >= 3){
            points = 15;
        }

        score += points;

        document.getElementById("score")
            .innerText = score;

        document.getElementById("streak")
            .innerText = streak + " 🔥";

        document.getElementById("feedback")
            .innerText =
            "✅ Correct! +" + points + " points";

        document.getElementById("feedback")
            .style.color = "#00ffc8";

    }


    /* WRONG */

    else{

        button.classList.add("wrong");

        streak = 0;

        document.getElementById("streak")
            .innerText = "0 🔥";

        document.getElementById("feedback")
            .innerText =
            "❌ Wrong! Correct answer: " + q.correct;

        document.getElementById("feedback")
            .style.color = "#ff526b";


        /*
           Highlight correct answer
        */

        document
            .querySelectorAll(".answer")
            .forEach(btn => {

                if(btn.innerText === q.correct){

                    btn.classList.add("correct");

                }

            });

    }


    document.getElementById("nextBtn")
        .classList.add("show");

}


/* =====================================================
   NEXT QUESTION
   ===================================================== */

function nextQuestion(){

    currentQuestion++;

    if(currentQuestion >= questions.length){

        finishGame();

        return;

    }

    loadQuestion();

}


/* =====================================================
   FINISH GAME
   ===================================================== */

function finishGame(){

    document.getElementById("gameCard")
        .style.display = "none";

    document.getElementById("result")
        .classList.add("show");


    /*
       Maximum score can be 150
       because of streak bonus.
    */

    document.getElementById("finalScore")
        .innerText = score + " points";


    let message = "";


    if(score >= 130){

        message =
            "🔥 Incredible! Your brain was on fire!";

    }

    else if(score >= 100){

        message =
            "🏆 Excellent! You have strong general knowledge.";

    }

    else if(score >= 70){

        message =
            "👏 Nice work! Keep learning and exploring.";

    }

    else{

        message =
            "🌱 Good attempt! Try again and beat your score.";

    }


    document.getElementById("resultMessage")
        .innerText = message;

}


/* =====================================================
   START
   ===================================================== */

startGame();

</script>

</body>
</html>
