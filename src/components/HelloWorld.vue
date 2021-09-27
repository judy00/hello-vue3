/* eslint-disable vue/no-deprecated-filter */
<template>
  <div class="hello">
    <!-- <p>1 日幣 = 0.278 台幣</p>
    <div>台幣 <input type="text" v-model="twd" @input="tw2jp"></div>
    <div>日幣 <input type="text" v-model="jpy" @input="jp2tw"></div> -->

    <p>1 日幣 = 0.278 台幣</p>
    <div>台幣 <input type="text" v-model="twd"></div>
    <div>日幣 <input type="text" v-model="jpy"></div>
    <div>美金 <input type="text" v-model="usd"></div>

    <!-- <p>filter: {{ price | toUpperCase }}</p> -->
    <!-- <p>method: {{ toUpperCase('asdfg') }}</p> -->
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  filters: {
    toUpperCase(value) {
      return value.toUpperCase()
    }
  },
  data() {
    return {
      name: 'sam',
      price: 100,
      count: 5,

      twd: 0.278,
      // jpy: 1,
    }
  },
  mounted() {
    // this.totalMethod()
    // this.total2()
  },
  created: ()=>{
    console.log(this)
  },
  computed: {
    totalComputed() {
      console.log('這是 totalComputed')
      return this.price * this.count
    },
    // point 5, computed get set
    jpy: {
      get() {
        return Number.parseFloat(Number(this.twd) / 0.278).toFixed(3)
      },
      set(val) {
        this.twd = Number.parseFloat(Number(val) * 0.278).toFixed(3)
      }
    },

    usd: {
      get() {
        // return Number.parseFloat(Number(this.twd) / 28.540).toFixed(3)
        return this.twd
      },
      set(newValue, oldValue, test) {
        console.log('newValue :>> ', newValue);
        console.log('oldValue :>> ', oldValue);
        console.log('test :>> ', test);
        this.twd = Number.parseFloat(Number(newValue) * 28.540).toFixed(3)
      }
    }
    // usd: {
    //   get() {
    //     return Number.parseFloat(Number(this.twd) / 28.540).toFixed(3)
    //   },
    //   set(val) {
    //     this.twd = Number.parseFloat(Number(val) * 28.540).toFixed(3)
    //   }
    // }
  },
  methods: {

    // tw2jp() {
    //   console.log('tw2jp :>> ');
    //   this.jpy = Number.parseFloat(Number(this.twd) / 0.278).toFixed(3)
    // },
    // jp2tw() {
    //   console.log('jp2tw :>> ');
    //   this.twd = Number.parseFloat(Number(this.jpy) * 0.278).toFixed(3)
    // },

    // toUpperCase(value) {
    //   return value.toUpperCase()
    // }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
