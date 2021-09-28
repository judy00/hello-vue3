<template>
  <div class="comp-tab">
    Tab B
    <input v-model="title">
  </div>
</template>

<script>
export default {
  name: 'TabBName',
  props: {
    msg: String
  },
  data() {
    return {
      title: '我是 TAB B'
    }
  },
  // 透過 this.$options.name 可以取得子元件的 name 屬性
  created () {
    this.$emit('update', `${this.$options.name} Created.`);
  },
  mounted () {
    this.$emit('update', `${this.$options.name} Mounted.`);
  },
  unmounted () {
    this.$emit('update', `${this.$options.name} Unmounted.`);
  },
  activated () {
    this.$emit('update2', `${this.$options.name} Activated.`);
  },
  deactivated () {
    this.$emit('update2', `${this.$options.name} Deactivated.`);
  },
}
</script>

<style>
.comp-tab {
  border: 2px solid pink;
  padding: 20px;
}
</style>
