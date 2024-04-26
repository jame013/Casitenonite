<script>
    import { goto } from "$app/navigation";
    let q = [
        { question: "que1", answer: "answer 1" },
        { question: "que2", answer: "answer 2" },
        { question: "que3", answer: "answer 3" },
        { question: "que4", answer: "answer 4" },
        { question: "que 5", answer: "answer 5" },
    ];

    let choice = [
        { c1: "answer 1", c2: "choice2" },
        { c1: "answer 2", c2: "choice2" },
        { c1: "choice", c2: "answer 3" },
        { c1: "answer 4", c2: "choice2" },
        { c1: "answer 5", c2: "choice2" },
    ];

    let question_no = 0;
    let count = 1;
    let flag1 = false;

    let flag2 = false;

    let bg_answer = "";
    let bg_circle = "";
    let chip = 100;
    let score = [
        { correct: false, wrong: false },
        { correct: false, wrong: false },
        { correct: false, wrong: false },
        { correct: false, wrong: false },
        { correct: false, wrong: false },
    ];

    const remove_chip = () => {
        chip = chip - random_fee;
    };

    let tick = 5;
    const timer = setInterval(() => {
        tick -= 1;
    }, 1000);
    $: if (tick < 0) {
        if (question_no < q.length - 1) {
            score[question_no].wrong = true;
            rnd();
            question_no += 1;
            remove_chip();
            count += 1;
            tick = 5;
        } else {
            score[question_no].wrong = true;
            tick = 0;
            goto(`/`, { replaceState: true });
            clearInterval(timer);
        }
    }
    const nextPage = () => {
        setTimeout(() => {
            if (count < 5) {
                count++;
                tick = 5;
            }
            question_no++;
            flag1 = false;
            flag2 = false;
            rnd();
            console.log(score);
            console.log(rnd);
        }, 500);
    };

    let random_fee = 0;

    let rnd = () => {
        random_fee = Math.floor(Math.random() * (30 - 10 + 1) + 10);
    };

    $: console.log(question_no, q.length);
</script>

<div class=" "></div>
<body class="text-sm bg-cover bg-no-repeat min-h-screen">
    <nav
        class="max-w-[900px] items-center m-auto backdrop-blur sticky top-4 bg-"
    >
        <div
            class="nav-con items-center flex justify-center m-auto bg-white-200/20 rounded-2xl p-2"
        >
            <ul class=" flex px-3 gap-28 flex-row">
                <li class=" text-white text-2xl"><a href="/">Home</a></li>
                <li class=" text-white text-2xl">
                    <a href="/game">Game</a>
                </li>
                <li class=" text-white text-2xl"><a href="/lastest">lastest</a></li>
            </ul>
        </div>
    </nav>

    <div class="flex justify-center mt-20 scale-150">
        <img class="w-20 h-20" src="./img/coin.png" alt="" />
        <div class=" absolute mt-8">{tick}</div>
    </div>
    <div class="container m-auto z-10">
        <div class="m-auto max-w-[800px] mt-20">
            <div class="home-box w-full bg-[#333] mx-auto p-[30px] rounded-md">
                <div class="nav-content flex justify-between items-center mb-3">
                    <h1 class=" text-green-300 mb-1">Quesion {count} of 5</h1>
                    <div class=" text-white font-bold">
                        จำนวนชิฟที่มี {chip}
                    </div>
                </div>

                <hr />
                <h3 class=" text-white mt-3 mb-5">Instruction:</h3>
                <p class=" text-white mb-4">
                    {q[question_no].question}
                </p>
                <div class=" items-center justify-between flex gap-20">
                    <button
                        class={`p-1 border-none rounded-md mt-2 w-full transition-colors duration-500 ${flag1 ? bg_answer : "bg-white"}`}
                        disabled={flag1 || flag2}
                        on:click={() => {
                            console.log(
                                q[question_no].answer == choice[question_no].c1,
                            );
                            nextPage();
                            if (
                                q[question_no].answer == choice[question_no].c1
                            ) {
                                flag1 = true;
                                bg_answer = "bg-green-500";
                                score[question_no].correct = true;
                            } else {
                                flag1 = true;
                                bg_answer = "bg-red-500";
                                score[question_no].wrong = true;
                                console.log("Take point");
                                remove_chip();
                            }
                        }}
                        >{choice[question_no].c1}
                    </button>
                    <button
                        class={`p-1 border-none rounded-md mt-2 w-full transition-colors duration-500 ${flag2 ? bg_answer : "bg-white"}`}
                        on:click={() => {
                            nextPage();
                            if (
                                q[question_no].answer === choice[question_no].c2
                            ) {
                                flag2 = true;
                                bg_answer = "bg-green-500";
                                score[question_no].correct = true;
                            } else {
                                flag2 = true;
                                bg_answer = "bg-red-500";
                                score[question_no].wrong = true;
                                remove_chip();
                            }
                        }}
                        >{choice[question_no].c2}
                    </button>
                </div>

                <br />

                <div class=" flex justify-between items-center">
                    <div class="flex">
                        <div
                            class={`border-white border aspect-square h-6 rounded-full ${
                                !score[0].correct && !score[0].wrong
                                    ? "bg-transparent"
                                    : score[0].correct && !score[0].wrong
                                      ? "bg-green-500"
                                      : "bg-red-500"
                            }`}
                        ></div>
                        <div
                            class={`border-white border aspect-square h-6 rounded-full ${
                                !score[1].correct && !score[1].wrong
                                    ? "bg-transparent"
                                    : score[1].correct && !score[1].wrong
                                      ? "bg-green-500"
                                      : "bg-red-500"
                            }`}
                        ></div>
                        <div
                            class={`border-white border aspect-square h-6 rounded-full ${
                                !score[2].correct && !score[2].wrong
                                    ? "bg-transparent"
                                    : score[2].correct && !score[2].wrong
                                      ? "bg-green-500"
                                      : "bg-red-500"
                            }`}
                        ></div>
                        <div
                            class={`border-white border aspect-square h-6 rounded-full ${
                                !score[3].correct && !score[3].wrong
                                    ? "bg-transparent"
                                    : score[3].correct && !score[3].wrong
                                      ? "bg-green-500"
                                      : "bg-red-500"
                            }`}
                        ></div>
                        <div
                            class={`border-white border aspect-square h-6 rounded-full ${
                                !score[4].correct && !score[4].wrong
                                    ? "bg-transparent"
                                    : score[4].correct && !score[4].wrong
                                      ? "bg-green-500"
                                      : "bg-red-500"
                            }`}
                        ></div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</body>

<style>
    body {
        background:
        /* top, transparent black, faked with gradient */
            linear-gradient(rgba(0, 0, 0, 0.8), rgba(0, 0, 0, 0.8)),
            /* bottom, image */
                url(https://images.unsplash.com/photo-1614030424754-24d0eebd46b2);
    }
</style>
