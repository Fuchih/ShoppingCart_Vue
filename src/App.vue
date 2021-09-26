<template>
  <div>
    <Header></Header>
    <Goods
      v-for="item in list"
      :key="item.id"
      :id="item.id"
      :title="item.goods_name"
      :pic="item.goods_img"
      :price="item.goods_price"
      :state="item.goods_state"
      :count="item.goods_count"
      @state-change="getNewState"
    ></Goods>
    <Footer
    :isAll="isAllCheck"
    :sum="amount"
    :totalItem="total"
    @allChecked="getAllChecked"
    ></Footer>
  </div>
</template>

<script>
import Counter from '@/components/Counter.vue'
import Footer from '@/components/Footer.vue'
import Header from '@/components/Header.vue'
import Goods from '@/components/Goods.vue'
import bus from '@/components/eventBus.js'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    Header,
    Goods,
    Counter,
    Footer
  },
  data() {
    return {
      list: []
    }
  },
  created() {
    this.initCardList()
    bus.$on('share', (val) => {
      this.list.some((item) => {
        if (item.id === val.id && val.count > 0) item.goods_count = val.count
      })
    })
  },
  methods: {
    async initCardList() {
      const { data: res } = await axios.get('../data.json')
      if (res.status === 200) {
        this.list = res.list
      }
    },
    getNewState(e) {
      this.list.some((item) => {
        if (item.id === e.id) {
          item.goods_state = e.val
          return true
        }
      })
    },
    getAllChecked(e) {
      this.list.forEach((item) => (item.goods_state = e))
    }
  },
  computed: {
    isAllCheck() {
      return this.list.every((item) => item.goods_state)
    },
    amount() {
      return this.list
        .filter((item) => item.goods_state)
        .reduce((sum, item) => {
          return (sum += item.goods_price * item.goods_count)
        }, 0)
    },
    total() {
      return this.list.filter((item) => item.goods_state).reduce((itemSum, item) => (itemSum += item.goods_count), 0)
    }
  }
}
</script>

<style lang="scss">
div {
  background-color: #f2f3ed;
}
</style>
