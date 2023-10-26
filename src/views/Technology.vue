<script setup>
import Navbar from '@/components/Navbar.vue'
</script>

<template>
    <body>
        <Navbar />
        <main>
            <h1 class="title"><span>03</span>SPACE LAUNCH 101</h1>
            <div class="technology">
                <div class="technology-text">
                    <h2>THE TERMINOLOGY…</h2>
                    <h1>LAUNCH VEHICLE</h1>
                    <p>A launch vehicle or carrier rocket is a rocket-propelled vehicle used to carry a payload from Earth's
                        surface to space, usually to Earth orbit or beyond. Our WEB-X carrier rocket is the most powerful in
                        operation. Standing 150 metres tall, it's quite an awe-inspiring sight on the launch pad!
                    </p>
                </div>
                <div class="technology-image">
                    <img src="@/assets/image/technology/image-launch-vehicle.png" alt="">
                </div>
            </div>
        </main>
    </body>
</template>

<style scoped>
body {
    margin: 0;
    padding: 0;
    background-image: url('@/assets/image/background-technology-desktop.jpg');
}

main {
    padding: 1rem;
    padding-bottom: 0;
}

.title {
    color: white;
    font-size: 1.8rem;
    font-family: 'Barlow Condensed', sans-serif;
    padding: 2rem;
    padding-left: 9rem;
    padding-right: 5rem;
    letter-spacing: 5px;
}

.title span {
    color: rgba(93, 93, 93, 0.7);
    font-size: 1.8rem;
    font-weight: bold;
    font-family: 'Barlow Condensed', sans-serif;
    letter-spacing: 5px;
    margin-right: 1rem;
}

.technology {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    padding-left: 4rem;
}

.technology-text {
    display: flex;
    flex-direction: column;
    padding: 5rem;
    padding-top: 8rem;
    width: 50%;
}

.technology-text h2 {
    color: rgba(255, 255, 255, 0.5);
    font-size: 1.2rem;
    font-family: 'Barlow Condensed', sans-serif;
    letter-spacing: 5px;
}

.technology-text h1 {
    color: white;
    font-size: 4rem;
    font-family: 'Bellefair', serif;
}

.technology-text p {
    color: #D0D6F9;
    font-size: 1.3rem;
    font-family: 'Barlow', sans-serif;
}

.technology-image {
    width: 500px;
    height: 500px;
    margin-left: 11rem;
}

.technology-image img {
    width: 100%;
}
</style>