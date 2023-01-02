<template>
    <div class="bg-gray-900 min-h-screen">
        <Navbar />

        <div class="max-w-5xl mx-auto mt-4 text-gray-100 bg-gray-700 min-h-screen p-4 rounded-md">
            <slot />
        </div>
    </div>
</template>

<script>
import Navbar from '../components/Navbar.vue';

export default {
    data() {
        return {
        //
        };
    },
    components: { Navbar }
}
</script>