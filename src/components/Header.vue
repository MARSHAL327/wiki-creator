<template>
    <header>
        <div class="container">
            <div class="logo">
                <img src="@/assets/molotok_logo.svg" alt="">
            </div>
            <div class="project-title">
                Инструмент для создания Wiki
            </div>
        </div>
    </header>
</template>

<script>
export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: "Header"
}
</script>

<style scoped>
header{
    background-color: #0E1025;
    padding: 20px;
}

header .container{
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.project-title{
    color: #ffffff;
    font-size: 32px;
    font-weight: bold;
}
</style>