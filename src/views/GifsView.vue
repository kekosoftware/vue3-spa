<template>
    <h1>Search Gifs</h1>
    <search @buscar="getGifs" />
    <loading v-show="loading" />
    <div class="row">
        <div class="col-12 col-md-4 g-3" v-for="gif in gifs" :key="gif.id">
            <card :gif="gif" />
        </div>
    </div>
</template>

<script>
import Card from '@/components/Card.vue'
import Search from '@/components/Search.vue'
import Loading from '@/components/Loading.vue'
import Swal from 'sweetalert2'

export default {
    components: { Card, Search, Loading},
    data: () => ({
        gifs: [],
        loading: true,
    }),
    created() {
        this.getGifs()
    },
    methods: {
        async getGifs(busqueda = 'pokemon') {
            if (busqueda.trim() === '') {
                Swal.fire({
                    title: "Búsqueda vacía",
                    icon: "error",
                    showConfirmButton: false,
                    showCloseButton: true,
                    timer: 3000,
                    timerProgressBar: true
                })
                return
            }
            this.loading = true
            
            const res = await fetch(`https://api.giphy.com/v1/gifs/search?api_key=j7BlDSJiFihdSx0rRijxCjbMVHxrYh40&q=${busqueda}`)
            
            const { data } = await res.json()
            
            this.gifs = data
            
            this.loading = false
        }
    }
}
</script>