<template>
  <div class="count-box">
    <button @click="handleCount" class="minus">-</button>
    <input :value="value" @change="handleChange" type="text" class="inp">
    <button @click="handleCount" class="add">+</button>
  </div>
</template>

<script>
export default {

  props: {
    value: {
      type: Number,
      default: 1
    }
  },
  methods: {
    handleCount (e) {
      if (e.target.classList.contains('minus')) {
        if (this.value <= 1) {
          return
        }
        this.$emit('input', this.value - 1)
      }
      if (e.target.classList.contains('add')) {
        this.$emit('input', this.value + 1)
      }
    },

    handleChange (e) {
      // console.log(e.target.value)
      const num = +e.target.value // 转数字处理
      if (isNaN(num) || num < 1 || num % 1 !== 0) {
        e.target.value = this.value
        return
      }
      this.$emit('input', num)
    }
  }
}
</script>

<style lang="less" scoped>
.count-box {
  width: 110px;
  display: flex;
  .add, .minus {
    width: 30px;
    height: 30px;
    outline: none;
    border: none;
    background-color: #efefef;
  }
  .inp {
    width: 40px;
    height: 30px;
    outline: none;
    border: none;
    margin: 0 5px;
    background-color: #efefef;
    text-align: center;
  }
}
</style>
