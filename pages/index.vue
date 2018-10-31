<template>
  <section class="container">
    <div>
      <logo/>
      <h1 class="title">
        nuxt-demo2
      </h1>
      <h2 class="subtitle">
        srr模块的nuxt
      </h2>
      <div class="links">
        <nuxt-link 
          class="button--green" 
          to="/login"
        >
          前往登录页面
        </nuxt-link>
      </div>
      <div>
        store的count:{{ count }}
      </div>
      <button @click="handleAdd">count + 1 </button>
      <button @click="handleDown">count + 1 </button>
    </div>
  </section>
</template>

<script>
import { mapMutations, mapGetters } from 'vuex'
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  },
  computed: {
    ...mapGetters(["count"])
  },
  mounted () {
  },
  methods: {
    handleAdd() {
      const newCount = this.count + 1;
      this.setCount(newCount)
    },

    handleDown() {
      const newCount = this.count - 1;
      this.setCount(newCount)
    },

    ...mapMutations({
      setCount: "SET_COUNT"
    })
  }
}
</script>

<style>

.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
