<!--./components/Projects.vue-->

<template>
    <div class="outline-projects">
        <div class="projects-track">
            <!-- Original Projekte -->
            <div class="project-card" v-for="(project, index) in projects" :key="'original-' + index">
                <img :src="project.image" :alt="project.title">
                <h3> {{ project.title }} </h3>
            </div>
            
            <!-- Duplizierte Projekte für nahtlose Loop -->
            <div class="project-card" v-for="(project, index) in projects" :key="'duplicate-' + index">
                <img :src="project.image" :alt="project.title">
                <h3> {{ project.title }} </h3>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const projects = ref([
    { title: 'Projekt 1', image: '/path/to/image1.jpg' },
    { title: 'Projekt 2', image: '/path/to/image2.jpg' },
    { title: 'Projekt 3', image: '/path/to/image3.jpg' },
    { title: 'Projekt 4', image: '/path/to/image4.jpg' },
    { title: 'Projekt 5', image: '/path/to/image5.jpg' },
]);
</script>

<style scoped lang="scss">
@import '../assets/style.scss';

.outline-projects {
    width: 100%;
    height: 100%;
    min-height: 0;
    background-color: white;
    overflow: hidden;
    display: flex;
    align-items: center;
    position: relative;
}

.projects-track {
    display: flex;
    gap: 2rem;
    animation: scroll 50s linear infinite; 
    transition: animation-duration 0.8s ease;
    
    &:hover {
        animation-play-state: paused; 
    }
}

.project-card {
    min-width: 300px;
    height: 200px;
    background-color: $main-red;
    border-radius: 15px;
    padding: 1rem;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    
    img {
        width: 100%;
        height: 120px;
        object-fit: cover;
        border-radius: 10px;
    }
    
    h3 {
        margin-top: 0.5rem;
        color: white;
        font-size: 1.2rem;
    }
}

// Die Animation
@keyframes scroll {
    0% {
        transform: translateX(0);
    }
    100% {
        transform: translateX(-50%);
    }
}
</style>