<template>
  <GuestLayout>
    <div class="flex justify-center items-center mb-4">
      <h1 class="text-2xl p-1 text-white mr-4 font-medium">
        New Updated!
      </h1>
    </div>

    <div class="grid md:grid-cols-5 grid-cols-3 justify-center">
      <Card v-for="komik in komiks" :key="komik.id" :komik="komik" />
    </div>

    <div v-if="isLoading === true" class="flex justify-center items-center">
      <Loader />
    </div>


  </GuestLayout>
</template>

<script>
import GuestLayout from '../Layouts/GuestLayout.vue';
import Card from '../components/Card.vue';
import Loader from '../components/Loader.vue';

export default {
  name: "IndexPage",
  data() {
    return {
      komiks: [],
      pagination: {},
      isLoading: true,
    }
  },
  async asyncData({ query, $config: { baseAPI_URL } }) {
    const res = await fetch(`${baseAPI_URL}/api/v1/komikcast/?page=${query.page || 1}`)
    const data = await res.json()
    return {
      data,
    }
  },
  created() {
    this.pagination = this.data.pagination
    setTimeout(() => {
      this.komiks = this.data.data
      this.isLoading = false
    }, 500)


  },
  mounted() {
    window.onscroll = () => {
      if (this.$route.path === '/' && this.pagination.next_page !== null && window.innerHeight + document.documentElement.scrollTop === document.documentElement.offsetHeight) {
        if (this.isLoading === false) {
          this.isLoading = true
          setTimeout(() => {
            fetch(`${this.$config.baseAPI_URL}/api/v1/komikcast/?page=${this.pagination.next_page}`)
              .then(res => res.json())
              .then(data => {
                this.komiks = [...this.komiks, ...data.data]
                this.pagination = data.pagination
                this.isLoading = false
                this.$router.push({ path: '/', query: { page: this.pagination.current_page } })
              })
          }, 500);
        }
      }
    }
  },
  components: { GuestLayout, Card, Loader }
}
</script>
