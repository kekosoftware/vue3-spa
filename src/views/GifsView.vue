<template>
    <h1>Search Gifs</h1>
    <div class="row">
        <div class="col-12 col-md-4 g-3" v-for="gif in gifs" :key="gif.id">
            <div class="card">
                <img height="250" 
                    class="card-img-top" 
                    :src="gif.images.original.url" 
                    :alt="gif.id"
                    loading="lazy"
                />
                <div class="card-body">
                    <h5 class="card-title">{{ gif.title }}</h5>
                    
                    <a href="#" class="btn btn-primary">Download</a>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data: () => ({
        gifs: []
    }),
    created() {
        this.getGifs()
    },
    methods: {
        async getGifs() {
            const res = await fetch(`https://api.giphy.com/v1/gifs/search?api_key=j7BlDSJiFihdSx0rRijxCjbMVHxrYh40&q=picachu`)
            const { data } = await res.json()

            this.gifs = data
        }
    }
}
</script>