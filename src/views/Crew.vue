<script setup>
import Navbar from '../components/Navbar.vue';
</script>

<template>
    <body>
        <Navbar />
        <main>
            <h1 class="title"><span>02</span>MEET YOUR CREW</h1>
            <div class="crew">
                <div class="crew-text">
                    <h2>PILOT</h2>
                    <h1>VICTOR GLOVER</h1>
                    <p>Pilot on the first operational flight of the SpaceX Crew Dragon to the International Space Station.
                        Glover is a commander in the U.S. Navy where he pilots an F/A-18.He was a crew member of Expedition
                        64, and served as a station systems flight engineer. </p>
                </div>
                <div class="crew-image">
                    <img src="@/assets/image/crew/image-victor-glover.png" alt="">
                </div>
            </div>
        </main>
    </body>
</template>

<style scoped>
body {
    margin: 0;
    padding: 0;
    font-family: 'Roboto', sans-serif;
    background-color: black;
    background-image: url('@/assets/image/background-crew-desktop.png');
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

.crew {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    padding-left: 4rem;
}

.crew-text {
    display: flex;
    flex-direction: column;
    padding: 5rem;
    padding-top: 8rem;
    width: 50%;
}

.crew-text h2 {
    color: rgba(255, 255, 255, 0.5);
    font-size: 2rem;
    font-family: 'Bellefair', serif;
    letter-spacing: 3px;
}

.crew-text h1 {
    color: white;
    font-size: 4rem;
    font-family: 'Bellefair', serif;
    margin: 0;
    margin-bottom: 1rem;
}

.crew-text p {
    width: 95%;
    color: #D0D6F9;
    font-size: 1.3rem;
    margin-bottom: 4rem;
    font-family: 'Barlow', sans-serif;
}

.crew-image {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 600px;
    margin-right: 5rem;
}

.crew-image img {
    width: 100%;
}

</style>