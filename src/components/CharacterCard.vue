<template>
    <div class="card">
        <p>{{name}}</p>
        <img alt="Character logo" :src="img">
    </div>
</template>

<script>

export default {
    props:{
        name: {
            type: String,
            default: "Character's name"
        },
        img: {
            type: String,
            default: 'http://i.annihil.us/u/prod/marvel/i/mg/b/40/image_not_available.jpg'
        }
    }
}
</script>

<style scoped>
.card{
    width: 300px;
    padding: 5px;
    border-radius: 5px;
    display: flex;
    flex-direction: column;
}
img{
    width: 100%;
}
.card p{
    font-weight: 700;
    font-size: 1.5em;
    margin: 8px 0;
}
</style>
