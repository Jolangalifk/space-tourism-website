<template>
    <header>
        <router-link to="/">
            <div class="header-image">
                <img src="@/assets/icon/space-logo.svg" alt="Space logo" />
            </div>
        </router-link>
        <div class="header-line"></div>
        <nav v-if="!showMenu">
            <ul>
                <li v-for="(route, index) in routes" :key="index" :class="{ active: isRouteActive(route.to) }">
                    <span>{{ index.toString().padStart(2, '0') }}</span>
                    <router-link :to="route.to">{{ route.label }}</router-link>
                </li>
            </ul>
        </nav>
        <button @click="toggleMenu" :class="{ cross: showMenu }">
            <div></div>
            <div></div>
            <div></div>
        </button>
        <div v-if="showMenu" class="menu-popup">
            <div v-for="(route, index) in routes" :key="index" :class="{ active: isRouteActive(route.to) }">
                <span>{{ index.toString().padStart(2, '0') }}</span>
                <router-link :to="route.to" @click="closeMenu">{{ route.label }}</router-link>
            </div>
        </div>
    </header>
</template>

<script setup>
import { useRoute, useRouter } from "vue-router";
import { ref, onBeforeMount, onBeforeUnmount } from "vue";

const route = useRoute();
const router = useRouter();
const showMenu = ref(false);
const menuClicked = ref(false);

const routes = [
    { to: "/", label: "HOME" },
    { to: "/destination/moon", label: "DESTINATION" },
    { to: "/crew/Commander", label: "CREW" },
    { to: "/technology/Launch vehicle", label: "TECHNOLOGY" },
];

let currentDestination = route.params.name || "";
let currentCrew = route.params.role || "";
let currentTechnology = route.params.name || "";

const isRouteActive = (to) => {
    if (to === "/destination/moon") {
        return currentDestination === "moon";
    } else if (to === "/destination/mars") {
        return currentDestination === "mars";
    } else if (to === "/destination/europa") {
        return currentDestination === "europa";
    } else if (to === "/destination/titan") {
        return currentDestination === "titan";
    }

    if (to === "/crew/Commander") {
        return currentCrew === "Commander";
    } else if (to === "/crew/pilot") {
        return currentCrew === "Pilot";
    } else if (to === "/crew/Flight engineer") {
        return currentCrew === "Flight engineer";
    } else if (to === "/crew/Flight surgeon") {
        return currentCrew === "Flight surgeon";
    }

    if (to === "/technology/Launch vehicle") {
        return currentTechnology === "Launch vehicle";
    } else if (to === "/technology/Spacecraft") {
        return currentTechnology === "Spacecraft";
    } else if (to === "/technology/Space suit") {
        return currentTechnology === "Space suit";
    } else if (to === "/technology/Space station") {
        return currentTechnology === "Space station";
    }
    return route.path === to;
};

const toggleMenu = () => {
    showMenu.value = !showMenu.value;
    menuClicked.value = showMenu.value;
};

const closeMenu = () => {
    showMenu.value = false;
    menuClicked.value = false;
};

const handleResize = () => {
    if (window.innerWidth <= 768) {
        showMenu.value = menuClicked.value;
    } else {
        showMenu.value = false;
    }
};

onBeforeMount(() => {
    window.addEventListener("resize", handleResize);
    handleResize();
});

onBeforeUnmount(() => {
    window.removeEventListener("resize", handleResize);
});
</script>

<style scoped>
header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 2rem;
    padding-right: 0;
    padding-left: 3rem;
    background-color: transparent;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

nav {
    display: flex;
    align-items: center;
    height: 80px;
    width: 60%;
    padding-left: 7rem;
    padding-right: 8rem;
    background-color: rgba(93, 93, 93, 0.1);
    backdrop-filter: blur(30px);
}

nav ul {
    width: 100%;
    height: 80px;
    display: flex;
    list-style: none;
    justify-content: space-between;
}

nav ul li {
    height: 100%;
    display: flex;
    align-items: center;
    margin-left: 0;
    cursor: pointer;
}

nav ul li.active {
    border-bottom: 4px solid white;
    transition: 0.4s;
}

nav ul li:hover {
    border-bottom: 4px solid rgba(255, 255, 255, 0.1);
    transition: 0.4s;
}

nav ul li span {
    color: white;
    font-size: 1rem;
    font-weight: 600;
    margin-right: 1rem;
    font-family: 'Barlow Condensed', sans-serif;
}

nav ul li a {
    text-decoration: none;
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 1rem;
    font-weight: normal;
    color: white;
    letter-spacing: 3px;
}

.header-image {
    width: 40px;
    height: 40px;
}

.header-image img {
    width: 100%;
    height: 100%;
}

.header-line {
    z-index: 2;
    position: absolute;
    width: 35%;
    height: 1px;
    background-color: rgba(255, 255, 255, 0.2);
    left: 10%;
}

button {
    display: none;
}

@media (max-width: 768px) {
    .header-line {
        display: none;
    }

    nav {
        display: none;
    }

    button {
        display: block;
        z-index: 2;
        position: absolute;
        top: 2rem;
        right: 2rem;
        width: 40px;
        height: 40px;
        background-color: transparent;
        border: none;
        cursor: pointer;
    }

    button div {
        width: 25px;
        height: 3px;
        margin: 5px;
        transition: 0.4s;
        background-color: #D0D6F9;
    }

    button.cross div:nth-child(1) {
        transform: rotate(45deg) translate(6px, 6px);
    }

    button.cross div:nth-child(2) {
        opacity: 0;
    }

    button.cross div:nth-child(3) {
        transform: rotate(-45deg) translate(5px, -5px);
    }

    .menu-popup {
        z-index: 1;
        position: absolute;
        top: 0;
        right: 0;
        width: 70%;
        height: 100vh;
        background-color: rgba(93, 93, 93, 0.1);
        backdrop-filter: blur(30px);
        display: flex;
        flex-direction: column;
        padding-left: 1rem;
        padding-top: 7rem;
        display: block;
    }

    .menu-popup div {
        margin: 1rem;
        margin-right: 0;
    }

    .menu-popup div.active {
        border-right: 5px solid white;
        transition: 0.4s;
    }

    .menu-popup div span {
        font-size: 1.2rem;
        font-weight: 600;
        color: white;
        font-family: 'Barlow Condensed', sans-serif;
        margin-right: 1rem;
        letter-spacing: 3px;
    }

    .menu-popup div a {
        font-size: 1.2rem;
        color: white;
        text-decoration: none;
        font-family: 'Barlow Condensed', sans-serif;
        letter-spacing: 5px;
    }

    header {
        padding: 0;
        padding-left: 2rem;
        padding-top: 2rem;
    }

    .header-image {
        width: 30px;
        height: 30px;
    }
}

@media (min-width: 768px) and (max-width: 1024px) {
    header {
        padding: 0;
        padding-left: 2rem;
    }

    .header-line {
        display: none;
    }

    nav {
        width: 60%;
        padding-left: 1rem;
        padding-right: 1rem;
    }

    nav ul li span {
        display: none;
    }
}
</style>