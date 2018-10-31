<template>
  <section class="container">
    <h2>这里是登录页面</h2>
    <div class="links">
      <nuxt-link 
        class="button--green" 
        to="/"
      >
        返回首页
      </nuxt-link>
    </div>
    <div>
      store的count:{{ count }}
    </div>
    <div>
      测试异步获取数据后在渲染页面
      <h3>{{ title }}列表</h3>
      <ul>
        <li
          v-for="(it) in list"
          :key="it.id"
          class="movie-item"
        >
          <h6>{{ it.title }}</h6>
          <img 
            :src="it.images.large" 
            alt=""
          >
        </li>
      </ul>
    </div>
  </section>
</template>

<script>
import { mapMutations, mapGetters } from 'vuex'
import axios from 'axios';

export default {
  asyncData(ctx) {
    return axios.get(`http://127.0.0.1:3000/v2/movie/top250?start=25&count=25`).then(res => {
      console.log(ctx.store.state)
      // console.log(process.client)
      return {
        title: res.data.title,
        list: res.data.subjects
      }
    }).catch((e) => {
      ctx.error({ statusCode: 404, message: 'Post not found' })
    })
  },
  components: {
  },
  computed: {
    ...mapGetters(["count"])
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
  flex-direction: column;
}
.movie-item{
  border-bottom: 1px solid #549;
  padding-bottom: 5px;
  margin-bottom: 20px;
}
</style>
