<script setup>
import { ref, onMounted } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import axios from 'axios';
import Navbar from '@/components/Navbar.vue';

const route = useRoute();
const router = useRouter();
const technology = ref(null);
const technologyList = ref([]);

const handleTechnologySelection = (selectedTechnology) => {
    technology.value = selectedTechnology;
    router.push({ name: 'technology', params: { name: selectedTechnology.name.toLowerCase() } });
};

const isTechnologyActive = (tech) => {
    const technologyName = route.params.name;
    return tech.name && tech.name.toLowerCase() === technologyName.toLowerCase();
};

onMounted(async () => {
    try {
        const response = await axios.get('/src/assets/api/data.json');

        if (response.status === 200) {
            if (response.data && Array.isArray(response.data.technology)) {
                technologyList.value = response.data.technology;
                const selectedTechnology = technologyList.value.find(tech => route.params.name && tech.name.toLowerCase() === route.params.name.toLowerCase());
                technology.value = selectedTechnology;
            } else {
                console.error('Data.json tidak memiliki properti technology yang sesuai.');
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
                <h1 class="title"><span>03</span>SPACE LAUNCH 101</h1>
            </div>
            <div class="technology" v-if="technology">
                <div class="technology-list">
                    <ul>
                        <li v-for="(tech, index) in technologyList" :key="tech.name"
                            @click="handleTechnologySelection(tech)" :class="{ active: isTechnologyActive(tech) }">
                            <router-link :to="{ name: 'technology', params: { name: tech.name.toLowerCase() } }"
                                active-class="active">
                                <div class="rounded-link" :class="{ active: isTechnologyActive(tech) }">
                                    <p>{{ index + 1 }}</p>
                                </div>
                            </router-link>
                        </li>
                    </ul>
                </div>
                <div class="technology-text">
                    <h2>THE TERMINOLOGY…</h2>
                    <h1>{{ technology.name.toUpperCase() }}</h1>
                    <p>{{ technology.description }}</p>
                </div>
                <div class="technology-image">
                    <img :src="technology.images.landscape" alt="Technology Image" />
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

.technology-list {
    display: flex;
    flex-direction: column;
    padding: 5rem;
    padding-top: 8rem;
}

.technology-list ul {
    width: fit-content;
    list-style: none;
    padding: 0;
}

.technology-list ul li {
    color: white;
    font-size: 1.2rem;
    font-family: 'Barlow Condensed', sans-serif;
    letter-spacing: 5px;
    margin-bottom: 2rem;
    cursor: pointer;
}

.technology-list ul li a {
    text-decoration: none;
}

.rounded-link {
    width: 90px;
    height: 90px;
    border-radius: 50%;
    border: 1px solid white;
    display: flex;
    justify-content: center;
    align-items: center;
}

.rounded-link p {
    color: white;
    font-size: 2.5rem;
    font-family: 'Bellefair', sans-serif;
    letter-spacing: 5px;
    padding-left: 5px;
}

.rounded-link.active {
    background-color: white;
}

.rounded-link.active p {
    color: black;
}

.technology-text {
    display: flex;
    flex-direction: column;
    padding: 5rem;
    padding-left: 0;
    padding-right: 0;
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
    width: 80%;
}

.technology-image {
    width: 500px;
    height: 500px;
    margin-left: 11rem;
}

.technology-image img {
    width: 100%;
}

@media (max-width: 768px) {
    main {
        padding: 0;
    }

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

    .technology {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: center;
        padding: 0;
    }

    .technology-list {
        display: flex;
        padding: 0;
        padding-top: 2.5rem;
    }

    .technology-list ul {
        width: 100%;
        list-style: none;
        padding: 0;
        display: flex;
        justify-content: space-between;
        gap: 1.5rem;
    }

    .rounded-link {
        width: 50px;
        height: 50px;
        border-radius: 50%;
        border: 1px solid white;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .rounded-link p {
        font-size: 1.2rem;
    }

    .technology-text {
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 3rem;
        padding-top: 0rem;
        width: 100%;
    }

    .technology-text h2 {
        color: rgba(255, 255, 255, 0.5);
        font-size: 1rem;
        font-family: 'Barlow Condensed', sans-serif;
        letter-spacing: 5px;
    }

    .technology-text h1 {
        color: white;
        font-size: 2rem;
        font-family: 'Bellefair', serif;
        margin: 0;
        margin-bottom: 1rem;
    }

    .technology-text p {
        width: 115%;
        color: #D0D6F9;
        font-size: 1rem;
        font-family: 'Barlow', sans-serif;
        text-align: center;
    }

    .technology-image {
        width: 100%;
        height: 200px;
        margin: 0;
        padding: 0;
        order: -1;
        border: 1px solid white;
    }

    .technology-image img {
        width: 100%;
        height: 100%;
    }
}

@media (min-width: 768px) and (max-width: 1024px) {
    main {
        padding: 0;
    }

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

    .technology {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: center;
        padding: 0;
    }

    .technology-list {
        display: flex;
        padding: 0;
        padding-top: 2.5rem;
        margin-bottom: 2rem;
    }

    .technology-list ul {
        width: 100%;
        list-style: none;
        padding: 0;
        display: flex;
        justify-content: space-between;
        gap: 1.5rem;
    }

    .rounded-link {
        width: 50px;
        height: 50px;
        border-radius: 50%;
        border: 1px solid white;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .rounded-link p {
        font-size: 1.2rem;
    }

    .technology-text {
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 3rem;
        padding-top: 0rem;
        width: 100%;
    }

    .technology-text h1 {
        color: white;
        font-size: 3rem;
        font-family: 'Bellefair', serif;
        margin: 0;
        margin-bottom: 1rem;
        margin-top: 0.5rem;
    }

    .technology-text p {
        width: 71%;
        text-align: center;
        font-size: 1.2rem;
    }

    .rounded-link {
        width: 80px;
        height: 80px;
        border-radius: 50%;
        border: 1px solid white;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .rounded-link p {
        font-size: 2rem;
    }
    
    .technology-image {
        width: 100%;
        height: 350px;
        margin: 0;
        padding: 0;
        order: -1;
        border: 1px solid white;
        margin-bottom: 2rem;
        margin-top: 1rem;
    }
    
}
</style>