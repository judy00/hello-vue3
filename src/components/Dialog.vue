<template>
  <div class="comp-dialog">
    Dialog
  </div>
</template>

<script>
export default {
  name: 'Dialog',
  props: {
    msg: String
  },
  data() {
    return {
      title: '我是 Dialog'
    }
  },
  created() {
    console.log('Dialog created')
  }
}
</script>

<style>
.comp-dialog {
  border: 2px solid orange;
  padding: 20px;
}
</style>
