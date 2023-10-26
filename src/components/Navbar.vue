<template>
    <header>
        <div class="header-image">
            <img src="@/assets/icon/space-logo.svg" alt="Space logo" />
        </div>
        <div class="header-line"></div>
        <nav>
            <ul>
                <li v-for="(route, index) in routes" :key="index" :class="{ active: isRouteActive(route.to) }">
                    <span>{{ index.toString().padStart(2, '0') }}</span>
                    <RouterLink :to="route.to">{{ route.label }}</RouterLink>
                </li>
            </ul>
        </nav>
    </header>
</template>

<script setup>
import { useRoute } from "vue-router";

const isRouteActive = (to) => {
    const route = useRoute();
    return route.path === to;
};

const routes = [
    { to: "/", label: "HOME" },
    { to: "/destination/moon", label: "DESTINATION" },
    { to: "/crew", label: "CREW" },
    { to: "/technology", label: "TECHNOLOGY" },
];
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
</style>