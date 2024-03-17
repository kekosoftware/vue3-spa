<template>
    <h1>Gif Router</h1>
    <img :src="img" :alt="name">
</template>

<script>
export default {
    data: () => ({
        img: "",
        name: "",
    }),
    created() {
        this.getRandomGif()
    },
    methods: {
        async getRandomGif() {
            const data = await fetch("https://api.giphy.com/v1/gifs/random?api_key=j7BlDSJiFihdSx0rRijxCjbMVHxrYh40")
            const res = await data.json()

            this.img = res.data.images.original.url
            this.name = res.data.title
        }
    }
}
</script>