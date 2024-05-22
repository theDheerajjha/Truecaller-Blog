<template>
    <div class="site-header">
        <div class="logo-container">
            <img src="../assets/truecaller.svg" alt="Site Logo" class="site-logo" />
        </div>
        <div class="header-img-container" v-if="showHeaderImage">
            <img src="../assets/header.jpg" alt="Header Image" class="header-image" />
            <h1 class="header-text">The Truecaller Blog</h1>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Header',
    props: {
        showHeaderImage: {
            type: Boolean,
            default: false
        }
    }
};
</script>

<style scoped>
.site-header {
    width: 100%;
    background-color: #f8f9fa;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    display: flex;
    flex-direction: column;
    align-items: center;
}

.logo-container {
    width: 100%;
    display: flex;
    justify-content: flex-start;
    padding: 10px 20px;
    position: fixed;
    z-index: 99;
    background-color: white;
    top: 0;
}

.site-logo {
    height: 40px;
    margin-left: 5px;
}

.header-img-container {
    width: 100%;
    position: relative;
}

.header-text {
    color:rgb(255, 250, 250);
    position: absolute;
    font-size:4rem;
    font-family: Arial, Helvetica, sans-serif;
    top: 50%; /* Center vertically */
    left: 50%; /* Center horizontally */
    transform: translate(-50%, -50%); /* Adjust to perfectly center the text */
    background-color: none; /* Optional: background with transparency for better visibility */
    text-align: center; /* Optional: center the text */
    width: 100%; /* Optional: ensure text container spans full width */
}

.header-image {
    width: 100%;
    height: auto;
    display: block;
}

@media (max-width: 768px) {
    .logo-container {
        padding: 10px;
    }

    .site-logo {
        height: 35px;
    }
}

@media (max-width: 480px) {
    .logo-container {
        padding: 8px;
    }

    .site-logo {
        height: 30px;
    }
}
</style>
