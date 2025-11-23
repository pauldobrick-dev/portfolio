<template>
    <nav class="navbar">
        <div class="navbar-container">
            <!-- Logo -->
            <div class="logo">
                <img src="../assets/Logo.png" alt="Logo"/>
                <span class="logo-text">Paul Dobrick</span>
            </div>
            
            <!-- Alles rechts: Links + Button -->
            <div class="nav-right">
                <a href="#projekte" class="nav-link">Projekte</a>
                <a href="#pakete" class="nav-link">Pakete</a>
                <a href="#kontakt" class="contact-btn">
                    Kontakt
                </a>
            </div>
        </div>
    </nav>
</template>

<script setup lang="ts">
</script>

<style scoped lang="scss">
@import '../assets/style.scss';

.navbar {
    background-color: $main-red;
    width: 100%;
    height: 70px;
    position: fixed;
    top: 0;
    left: 0;
    z-index: 1000;
    backdrop-filter: blur(10px);
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.navbar-container {
    max-width: 1400px;
    margin: 0 auto;
    height: 100%;
    padding: 0 2rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.logo {
    display: flex;
    align-items: center;
    gap: 1rem;

    cursor: pointer;
    
    img {
        height: 40px;
        width: auto;
        transition: transform 0.3s ease;
        
        &:hover {
            transform: scale(1.05);
        }
    }
    
    .logo-text {
        color: white;
        font-family: "Roboto Condensed", sans-serif;
        font-size: 1rem;
        font-weight: 400;
    }
}

.nav-right {
    display: flex;
    align-items: center;
    gap: 2rem;
}

.nav-link {
    color: white;
    font-family: "Roboto Condensed", sans-serif;
    font-size: 1rem;
    font-weight: 500;
    text-decoration: none;
    position: relative;
    transition: color 0.3s ease;
    
    &::after {
        content: '';
        position: absolute;
        bottom: -5px;
        left: 0;
        width: 0;
        height: 2px;
        background-color: white;
        transition: width 0.3s ease;
    }
    
    &:hover {
        color: rgba(255, 255, 255, 0.9);
        
        &::after {
            width: 100%;
        }
    }
}

.contact-btn {
    background-color: white;
    color: $main-red;
    font-family: "Roboto Condensed", sans-serif;
    font-weight: 700;
    font-size: 1rem;
    padding: 0.5rem 2rem;
    border-radius: 30px;
    text-decoration: none;
    transition: all 0.3s ease;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
    
    &:hover {
        transform: translateY(-2px);
        box-shadow: 0 4px 12px rgba(0, 0, 0, 0.25);
    }
}

// Responsive
@media (max-width: 768px) {
    .logo-text {
        display: none; // Name auf Mobile ausblenden
    }
    
    .nav-right {
        gap: 1rem;
    }
    
    .nav-link {
        font-size: 0.9rem;
    }
    
    .contact-btn {
        padding: 0.6rem 1.2rem;
        font-size: 0.9rem;
    }
}
</style>