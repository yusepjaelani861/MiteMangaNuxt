<template>
    <div class="bg-gray-700 p-2">
        <div class="flex justify-between items-center">
            <div class="flex items-center">
                <h1 class="text-2xl p-1 text-white mr-4 font-bold">
                    MiteManga
                </h1>
                <ul class="flex text-lg">
                    <li class="mr-2">
                        <nuxt-link to="/" class="text-white">Home</nuxt-link>
                    </li>
                    <li class="mr-2">
                        <a href="#" class="text-white">About</a>
                    </li>
                    <li class="mr-2">
                        <a href="#" class="text-white">Contact</a>
                    </li>
                </ul>
            </div>

            <input type="text" class="bg-white rounded p-2" placeholder="Search" />
        </div>
    </div>
</template>