<template>
  <div class="container row mx-auto goods">
    <div class="row  mb-4">
      <input type="checkbox" class="form-check-input" :id="id" :checked="state" @change="stateChange" />
      <label :for="id" class="good-pic">
        <img :src="pic" class="img-fluid" />
      </label>
      <div class="col position-relative">
        <h1 class="title">{{ title }}</h1>
        <div class="text-danger">${{ price }}</div>
        <Counter :num="count" :id="id"></Counter>
      </div>
    </div>
    <hr />
  </div>
</template>

<script>
import Counter from '@/components/Counter.vue'
export default {
  props: {
    id: {
      required: true,
      type: Number
    },
    title: {
      default: '',
      type: String
    },
    pic: {
      default: '',
      type: String
    },
    price: {
      default: 0,
      type: Number
    },
    state: {
      default: true,
      type: Boolean
    },
    count: {
      default: 1,
      type: Number
    }
  },
  components: {
    Counter
  },
  methods: {
    stateChange(e) {
      const newState = e.target.checked
      this.$emit('state-change', { id: this.id, val: newState })
    }
  }
}
</script>

<style lang="scss" scoped>
.good-pic {
  width: 150px;
}

.title {
  font: {
    size: 16px;
    weight: bold;
  }
}
</style>
