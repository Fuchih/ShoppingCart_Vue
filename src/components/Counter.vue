<template>
  <div>
    <div class="position-absolute  change-num">
      <button @click="sub" class="btn btn-sm btn-secondary">-</button>
      <span> {{ num }} </span>
      <button @click="add" class="btn btn-sm btn-secondary">+</button>
    </div>
  </div>
</template>

<script>
// import bus from '@/components/eventBus.js'

export default {
  props: {
    id: {
      type: Number
    },
    num: {
      default: 1,
      type: Number
    }
  },
  methods: {
    sub() {
      this.$emit('numChange', this.num - 1)
      //  const obj = { id: this.id, count: this.num -1 }
      // bus.$emit('share', obj)
    },
    add() {
      this.$emit('numChange', this.num + 1)
      // const obj = { id: this.id, count: this.num + 1 }
      // bus.$emit('share', obj)
    }
  }
}
</script>

<style lang="scss" scoped>
.change-num {
  bottom: 20px;
  right: -35px;
}
</style>
