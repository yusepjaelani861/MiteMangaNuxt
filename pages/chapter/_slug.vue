<template>
    <GuestLayout>
        <div v-if="success === true">
            <div class="flex justify-center items-center mb-4">
                <h1 class="text-2xl p-1 text-white mr-4 font-medium">
                    {{ slug }}
                </h1>
            </div>
    
            <div class="w-full" v-if="chapter.images.length > 0">
                <img v-for="chapters in chapter.images" :key="chapters.id" :src="'https://api.mitenime.my.id/api/v1/images/?url=' + chapters.image"
                 class="w-full" />
            </div>
    
            <div v-else>
                <p class="text-white text-center">No Image</p>
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
        };
    },
    async asyncData({ params, $config: { baseAPI_URL } }) {
        const res = await fetch(`${baseAPI_URL}/api/v1/komikcast/chapter/${params.slug}`)
        const data = await res.json()

        return {
            chapter: data.data,
            slug: params.slug,
            success: data.success
        }
    },
    components: { GuestLayout }
}
</script>