<template>
    <h1>Search Stickers</h1>
    <search @buscar="getStickers" />
    <loading v-show="loading" />
    <div class="row">
        <div class="col-12 col-md-4 g-3" v-for="sticker in stickers" :key="sticker.id">
            <card :gif="sticker" />
        </div>
    </div>
</template>

<script>
import Card from '@/components/Card.vue'
import Search from '@/components/Search.vue'
import Loading from '@/components/Loading.vue'
import swal from 'sweetalert2'

export default {
    components: { Card, Search, Loading },
    data: () => ({
        stickers: [],
        loading: true,
    }),
    created() {
        this.getStickers()
    },
    methods: {
        async getStickers(busqueda = 'pokemon') {
            if (busqueda.trim() === '') {
                swal.fire({
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

            const res = await fetch(`https://api.giphy.com/v1/stickers/search?api_key=j7BlDSJiFihdSx0rRijxCjbMVHxrYh40&q=${busqueda}`)
            
            const { data } = await res.json()

            this.stickers = data

            this.loading = false
        }
    }
}
</script>