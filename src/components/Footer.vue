<template>
  <div class="footer position-fixed bottom-0 start-50 translate-middle-x bg-secondary text-light ">
    <div class="mt-2 bottom">
      <input type="checkbox" id="all" class="form-check-input ms-2" :checked="isAll" @change="allChecked" />
      <label for="all" class="me-5">Tick all</label>
      <span class="me-2"
        >Total : <span class="text-danger">${{ sum.toFixed(2) }}</span>
      </span>
      <button class="btn btn-sm btn-primary ms-2">Checkout({{ totalItem }})</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    isAll: {
      default: false,
      type: Boolean
    },
    sum: {
      dafault: 0,
      type: Number
    },
    totalItem: {
      default: 0,
      type: Number
    }
  },
  methods: {
    allChecked(e) {
      const allChecked = e.target.checked
      this.$emit('allChecked', allChecked)
    }
  }
}
</script>

<style lang="scss" scoped>
.footer {
  width: 100%;
  height: 50px;
  
  .bottom {
    background-color: #6c757d;
  }
}
</style>
