<template>
    <GuestLayout>
        <div v-if="success === true">
            <div class="md:flex text-gray-300 font-light mb-4">
                <div class="flex-shrink-0 md:w-80 w-full mr-4 mb-4">
                    <img :src="'https://api.mitenime.my.id/api/v1/images/?url=https://i0.wp.com/' + komik.image.replace('https://', '')" alt="One Piece"
                        class="object-contain h-full rounded-md" />
                </div>
                <div class="break-words">
                    <h1 class="text-2xl mb-2 font-medium">
                        {{ komik.title }}
                    </h1>
                    <p class="text-lg mb-1">{{ komik.original }}</p>
                    <p class="text-lg mb-1"><strong>Author</strong>: {{ komik.author }}</p>
                    <p class="text-lg mb-1"><strong>Status</strong>: {{ komik.status }}</p>
                    <p class="text-lg mb-1"><strong>Genre</strong>:
                        <a v-for="genre in komik.genres" :key="genre.id" :href="'/genre/' + genre.slug"
                            class="text-blue-500">{{ genre.name }}, </a>
                    </p>
                    <p class="text-lg mb-1"><strong>Released</strong>: {{ komik.released }}</p>
                    <p class="text-lg mb-1"><strong>Type</strong>: <a v-for="tipe in komik.types" :href="tipe.url"
                            class="text-blue-500">{{ tipe.name }}</a>
                    </p>
                    <p class="text-lg mb-1"><strong>Total Chapters</strong>: {{ komik.total_chapter }}</p>
                    <p class="text-lg mb-1"><strong>Sinopsis</strong>: {{ komik.description }}</p>
                </div>
            </div>
            <h1 class="text-2xl font-medium text-gray-300 mb-2 underline">Chapter List</h1>
            <div class="w-full overflow-auto max-h-80 mb-4">
                <div class="grid md:grid-cols-5 grid-cols-3 gap-4">
                    <nuxt-link :to="'/chapter/' + chapter.slug" v-for="chapter in komik.chapters" :key="chapter.id"
                        class="bg-slate-800 hover:bg-slate-900 rounded-md p-2">
                        <h1 class="text-lg font-medium text-gray-300">{{ chapter.title }}</h1>
                        <p class="text-gray-300 text-xs">{{ convertDate(chapter.created_at) }}</p>
                    </nuxt-link>
                </div>
            </div>
        </div>

        <NotFound v-else />
    </GuestLayout>
</template>

<script>
import GuestLayout from '../../Layouts/GuestLayout.vue';
import NotFound from '../../components/NotFound.vue';

export default {
    data() {
        return {
            //
        }
    },
    async asyncData({ params, $config: { baseAPI_URL } }) {
        const res = await fetch(`${baseAPI_URL}/api/v1/komikcast/komik/${params.slug}`)
        const data = await res.json()

        return {
            komik: data.data,
            success: data.success
        }
    },
    methods: {
        convertDate(date) {
            return new Date(date).toLocaleDateString('id-ID', {
                year: 'numeric',
                month: 'long',
                day: 'numeric'
            })
        }
    },
    components: { GuestLayout, NotFound }
}
</script>