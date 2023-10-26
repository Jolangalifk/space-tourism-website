<script setup>
import { ref, onMounted } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import axios from 'axios';
import Navbar from '@/components/Navbar.vue';

const route = useRoute();
const router = useRouter();
const destination = ref(null);
const destinationList = ref([]);

const handleDestinationSelection = (selectedDestination) => {
    destination.value = selectedDestination;
    router.push({ name: 'destination', params: { name: selectedDestination.name.toLowerCase() } });
};

const isDestinationActive = (dest) => {
    const destinationName = route.params.name;
    return dest.name && dest.name.toLowerCase() === destinationName.toLowerCase();
};

onMounted(async () => {
    try {
        const response = await axios.get('/src/assets/api/data.json');

        if (response.status === 200) {
            if (response.data && Array.isArray(response.data.destinations)) {
                destinationList.value = response.data.destinations;
                const selectedDestination = destinationList.value.find(dest => route.params.name && dest.name.toLowerCase() === route.params.name.toLowerCase());
                destination.value = selectedDestination;
            } else {
                console.error('Data.json tidak memiliki properti destinations yang sesuai.');
            }
        } else {
            console.error('Error fetching data. Status code:', response.status);
        }
    } catch (error) {
        console.error('Error fetching data:', error);
    }
});
</script>

<template>
    <body>
        <Navbar />
        <main>
            <h1 class="title"><span>01</span>PICK YOUR DESTINATION</h1>
            <div class="destination" v-if="destination">
                <div class="destination-image">
                    <img :src="destination.images.png" alt="Destination Image" />
                </div>
                <div class="destination-text">
                    <div class="destination-list">
                        <ul>
                            <li v-for="dest in destinationList" :key="dest.name" @click="handleDestinationSelection(dest)"
                                :class="{ active: isDestinationActive(dest) }">
                                <router-link :to="{ name: 'destination', params: { name: dest.name.toLowerCase() } }"
                                    active-class="active">
                                    {{ dest.name.toUpperCase() }}
                                </router-link>
                            </li>
                        </ul>
                    </div>
                    <h1>{{ destination.name.toUpperCase() }}</h1>
                    <p>{{ destination.description }}</p>
                    <div class="destination-distance-and-time">
                        <div class="destination-distance">
                            <p>AVG. DISTANCE</p>
                            <h2>{{ destination.distance.toUpperCase() }}</h2>
                        </div>
                        <div class="destination-time">
                            <p>EST. TRAVEL TIME</p>
                            <h2>{{ destination.travel.toUpperCase() }}</h2>
                        </div>
                    </div>
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
    background-image: url('@/assets/image/background-destination-desktop.jpg');
}

main {
    padding: 1rem;
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

.destination {
    display: flex;
    align-items: center;
    flex-direction: row;
    justify-content: space-between;
    padding: 2rem;
}

.destination-image {
    width: 500px;
    height: 500px;
    margin-left: 11rem;
}

.destination-image img {
    width: 100%;
}

.destination-text {
    display: flex;
    flex-direction: column;
    padding: 2rem;
    padding-left: 5rem;
    padding-right: 5rem;
    width: 50%;
}

.destination-text h1 {
    color: white;
    font-size: 8rem;
    font-family: 'Bellefair', serif;
    margin: 0;
}

.destination-text p {
    width: 90%;
    color: #D0D6F9;
    font-size: 1.3rem;
    margin-bottom: 4rem;
    font-family: 'Barlow', sans-serif;
}

.destination-list {
    width: 65%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding-left: 0;
}

.destination-list ul {
    width: 100%;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    list-style: none;
    padding: 0;
}

.destination-list ul li {
    padding-bottom: 0.5rem;
}

.destination-list ul li.active {
    border-bottom: 4px solid white;
    color: white;
    transition: 0.4s;
}

.destination-list ul li:hover {
    border-bottom: 4px solid rgba(255, 255, 255, 0.1);
    transition: 0.4s;
}

.destination-list ul li a {
    text-decoration: none;
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 1.5rem;
    font-weight: normal;
    color: #D0D6F9;
    letter-spacing: 3px;
}

.destination-list ul li a.active {
    color: white;
}

.destination-distance-and-time {
    width: 80%;
    display: flex;
    flex-direction: row;
    padding-top: 2rem;
    border-top: 1px solid rgba(255, 255, 255, 0.2);
}

.destination-distance {
    display: flex;
    flex-direction: column;
    width: 50%;
}

.destination-distance p {
    color: #D0D6F9;
    font-size: 1rem;
    font-family: 'Barlow Condensed', sans-serif;
    letter-spacing: 3px;
    margin: 0;
}

.destination-distance h2 {
    color: white;
    font-size: 2rem;
    font-family: 'Bellefair', serif;
    margin: 0;
}

.destination-time {
    display: flex;
    flex-direction: column;
    width: 50%;
}

.destination-time p {
    color: #D0D6F9;
    font-size: 1rem;
    font-family: 'Barlow Condensed', sans-serif;
    letter-spacing: 3px;
    margin: 0;
}

.destination-time h2 {
    color: white;
    font-size: 2rem;
    font-family: 'Bellefair', serif;
    margin: 0;
}
</style>