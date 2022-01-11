<template>
    <div class="card">
        <img :src="details.poster" alt="">

        <h2>{{ details.title }}</h2>

        <div class="info">{{ details.author }}</div>
        <div class="info">{{ details.year }}</div>
        {{ details.genre }}
    </div>
</template>

<script>
export default {
    name: "DiscCard",
    props: {
        details: Object
    }
}
</script>

<style scoped lang="scss">
@import '../styles/variables.scss';
.card {
    width: calc( (100% / 5) - 40px );
    margin: 20px;
    background-color: $primary_color;
    padding: 20px;
    text-align: center;
    h2 {
        text-transform: uppercase;
        font-size: 20px;
        margin: 15px 0;
    }
    .info {
        color: gray;
    }
}
</style>