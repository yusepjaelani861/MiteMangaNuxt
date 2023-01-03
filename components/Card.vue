<template>
    <div class="w-full p-1 rounded-md">
        <nuxt-link :to="'/komik/' + komik.slug">
            <div class="bg-gray-500 rounded">
                <div class="flex justify-center">
                    <img :src="'https://api.mitenime.my.id/api/v1/images/?url=https://i0.wp.com/'+ komik.image.replace('https://', '')"
                        :alt="komik.title" class="object-contain h-64 rounded-t-md" />
                </div>
                <div class="flex flex-col justify-center items-center bg-gray-400 w-full px-4 py-1 rounded-b-md h-20">
                    <h1 class="text-sm font-bold line-clamp-2 mb-2 text-center">{{ komik.title }}</h1>
                    <nuxt-link :to="komik.new_chapter.slug ? '/chapter/' + komik.new_chapter.slug : '#'" class="bg-gray-500 text-white text-xs rounded p-1 px-2">{{ komik.new_chapter.chapter }}</nuxt-link>
                </div>
            </div>
        </nuxt-link>
    </div>
</template>

<script>
export default {
    props: ['komik'],
    data() {
        return {
            //
        }
    }
}
</script>