<script setup>
import { ref, onMounted } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import axios from 'axios';
import Navbar from '@/components/Navbar.vue';

const route = useRoute();
const router = useRouter();
const crew = ref(null);
const crewList = ref([]);

const handleCrewSelection = (selectedCrew) => {
    crew.value = selectedCrew;
    router.push({ role: 'crew', params: { role: selectedCrew.role.toLowerCase() } });
};

const isCrewActive = (cr) => {
    const crewRole = route.params.role;
    return cr.role && cr.role.toLowerCase() === crewRole.toLowerCase();
};

onMounted(async () => {
    try {
        const response = await axios.get('/src/assets/api/data.json');

        if (response.status === 200) {
            if (response.data && Array.isArray(response.data.crew)) {
                crewList.value = response.data.crew;
                const selectedCrew = crewList.value.find(cr => route.params.role && cr.role.toLowerCase() === route.params.role.toLowerCase());
                crew.value = selectedCrew;
            } else {
                console.error('Data.json tidak memiliki properti crew yang sesuai.');
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
            <div class="h1">
                <h1 class="title"><span>02</span>MEET YOUR CREW</h1>
            </div>
            <div class="crew" v-if="crew">
                <div class="crew-text">
                    <h2>{{ crew.role.toUpperCase() }}</h2>
                    <h1>{{ crew.name.toUpperCase() }}</h1>
                    <p>{{ crew.bio }}</p>
                    <div class="crew-list">
                        <ul>
                            <li v-for="cr in crewList" :key="cr.role" @click="handleCrewSelection(cr)"
                                :class="{ active: isCrewActive(cr) }">
                                <router-link :to="{ name: 'crew', params: { role: cr.role.toLowerCase() } }"
                                    active-class="active">
                                    <div class="rounded-link" :class="{ active: isCrewActive(cr) }"></div>
                                </router-link>
                            </li>
                        </ul>
                    </div>
                </div>
                <div class="crew-image">
                    <img :src="crew.images.png" :alt="crew.name">
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
    width: 60%;
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
    width: 75%;
    color: #D0D6F9;
    font-size: 1.3rem;
    margin-bottom: 4rem;
    font-family: 'Barlow', sans-serif;
}

.crew-list {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    width: 100%;
}

.rounded-link {
    border-radius: 50%;
    width: 20px;
    height: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #979797;
    cursor: pointer;
}

.rounded-link.active {
    background-color: white;
    transition: 0.4s;
}


.crew-list ul {
    display: flex;
    list-style: none;
    width: 100%;
    padding: 0;
    gap: 30px;
}

.crew-list ul li {
    cursor: pointer;
}

.crew-image {
    width: 40%;
    display: flex;
    align-items: center;
}

.crew-image img {
    width: 100%;
}

@media (max-width: 768px) {
    .h1 {
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 2rem;
    }

    .title {
        color: white;
        font-size: 1.2rem;
        font-family: 'Barlow Condensed', sans-serif;
        padding: 0;
        letter-spacing: 3px;
    }

    .title span {
        color: rgba(93, 93, 93, 0.7);
        font-size: 1.2rem;
        font-weight: bold;
        font-family: 'Barlow Condensed', sans-serif;
        letter-spacing: 5px;
        margin-right: 1rem;
    }

    .crew {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        padding-left: 0;
        align-items: center;
    }

    .crew-text {
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 2rem;
        padding-top: 2.5rem;
        width: 100%;
    }

    .crew-text h2 {
        color: rgba(255, 255, 255, 0.5);
        font-size: 1.1rem;
        font-family: 'Bellefair', serif;
        letter-spacing: 0;
    }

    .crew-text h1 {
        color: white;
        font-size: 1.5rem;
        font-family: 'Bellefair', serif;
        margin: 0;
        margin-bottom: 1rem;
    }

    .crew-text p {
        width: 120%;
        color: #D0D6F9;
        font-size: 1rem;
        font-family: 'Barlow', sans-serif;
        text-align: center;
    }

    .crew-list {
        order: -1;
        margin-bottom: 2rem;
    }

    .crew-list ul {
        display: flex;
        list-style: none;
        width: 100%;
        padding: 0;
        gap: 20px;
        justify-content: center;
    }

    .crew-list ul li {
        cursor: pointer;
    }

    .rounded-link {
        width: 12px;
        height: 12px;
    }

    .crew-image {
        order: -1;
        width: 350px;
        height: 250px;
        border-bottom: 2px solid #979797;
    }

    .crew-image img {
        width: 100%;
        height: 100%;
    }
}

@media (min-width: 768px) and (max-width: 1024px) {
    .h1 {
        display: flex;
        padding: 2rem;
    }

    .title {
        color: white;
        font-size: 1.5rem;
        font-family: 'Barlow Condensed', sans-serif;
        padding: 0;
        letter-spacing: 3px;
    }

    .title span {
        color: rgba(93, 93, 93, 0.7);
        font-size: 1.5rem;
        font-weight: bold;
        font-family: 'Barlow Condensed', sans-serif;
        letter-spacing: 5px;
        margin-right: 1rem;
    }

    .crew {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        padding-left: 0;
        align-items: center;
    }

    .crew-text {
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 2rem;
        padding-top: 2.5rem;
        width: 100%;
    }

    .crew-text h2 {
        color: rgba(255, 255, 255, 0.5);
        font-size: 2rem;
        font-family: 'Bellefair', serif;
        letter-spacing: 0;
    }

    .crew-text h1 {
        color: white;
        font-size: 3rem;
        font-family: 'Bellefair', serif;
        margin: 0;
        margin-bottom: 1rem;
    }

    .crew-text p {
        width: 75%;
        color: #D0D6F9;
        font-size: 1.2rem;
        font-family: 'Barlow', sans-serif;
        text-align: center;
    }

    .crew-list {
        margin-bottom: 2rem;
    }

    .crew-list ul {
        display: flex;
        list-style: none;
        width: 100%;
        padding: 0;
        gap: 20px;
        justify-content: center;
    }

    .crew-list ul li {
        cursor: pointer;
    }

    .rounded-link {
        width: 15px;
        height: 15px;
    }

    
}
</style>