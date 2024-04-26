<script>
    let q = {
        q1: "question 1",
    };
    let choice = { c1: "choice 1", c2: "choice2" };
    // let circle = "bg-gray-300"
    let bg_c1 = "bg-white";
    let bg_c2 = "bg-black";
    let count = 1;
    let flag1 = false;
    let flag2 = false;

    let bon1 = false;
    let bon2 = true;
    const nextPage = () => {
        setTimeout(() => {
            count++;
            flag1 = false;
            flag2 = false;
        }, 500);
    };
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
                <li class=" text-white text-2xl"><a href="/game">Game</a></li>
                <li class=" text-white text-2xl"><a href="/lastest">lastest</a></li>
            </ul>
        </div>
    </nav>


    <div class=" items-center m-auto flex justify-center mt-20">
        <img class="w-100 h-100" src="/img/2.jpg" alt="" />
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
