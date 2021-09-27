/* eslint-disable vue/no-deprecated-filter */
<template>
  <div class="hello">
    <h2>條件判斷 v-if / v-show</h2>
    <label>
      <input type="checkbox" v-model="isShow"> isShow: {{ isShow }}
    </label>
    <div class="wrap">
      <div v-if="isShow" class="box"> V-if </div>
      <div v-show="isShow" class="box"> V-show </div>
    </div>
    <hr>
    <hr>


    <h2>v-if , v-else-if,  v-else</h2>
    <h4>青蔥 price: {{ price }}</h4>
    <button @click="price++">Plus</button>
    <button @click="price = 0">Reset</button>
    <div class="wrap">
      <div v-if="price < 10">阿便宜拉</div>
      <div v-else-if="price < 15">還可以</div>
      <div v-else>太貴了走了走了</div>
    </div>
    <hr>
    <hr>


    <h2>v-if + template</h2>
    <h3>每行都綁一個 v-if</h3>
    <label>
      <input type="checkbox" v-model="miltiShow"> 顯示: {{ miltiShow }}
    </label>
    <h4 v-if="miltiShow" style="margin:2px 0;">名字: XXX</h4>
    <p v-if="miltiShow" style="margin:2px 0;">email: aaa@aaa.com</p>
    <p v-if="miltiShow" style="margin:2px 0;">phone: 12345678</p>


    <h3>用 template 包一起，在上面加上 v-if 控制 ( v-show 不行)</h3>
    <label>
      <input type="checkbox" v-model="miltiShow2"> 顯示: {{ miltiShow2 }}
    </label>
    <template v-if="miltiShow2">
      <h4 style="margin:2px 0;">名字: XXX</h4>
      <p style="margin:2px 0;">email: aaa@aaa.com</p>
      <p style="margin:2px 0;">phone: 12345678</p>
    </template>
    <hr>
    <hr>

    <h2>v-if 與 key 屬性</h2>
    <h4>👇 vue 2: 只有 v-if, 沒有 key 👇</h4>
    <a href="https://jsfiddle.net/kurotanshi/qo94607a/" target="_blank">demo</a>
    <h4>👇 vue 3 修正: 只有 v-if, 沒有 key 👇</h4>
    <div class="form-a">
      <label>
        <input class="label-a" type="radio" value="username" v-model="loginType">
        Username
      </label>
      <label>
        <input class="label-a" type="radio" value="email" v-model="loginType">
        Email
      </label>

      <br>
      <template v-if="loginType === 'username'">
        <label class="label-a">Username</label>
        <input class="input-a" placeholder="Enter your username">
      </template>
      <template v-else>
        <label class="label-a">Email</label>
        <input class="input-a" placeholder="Enter your email address">
      </template>
    </div>
    <hr>
    <hr>


    <h2>v-for</h2>
    <h3 style="margin-bottom:5px;">陣列 列表渲染 (值, index)</h3>
    <h4 style="margin:5px;">v-for="(item, index) in arr"</h4>
    <ul style="margin:5px;">
      <li v-for="(i, idx) in arr" :key="i">{{ i + ' - ' + idx }}</li>
    </ul>
    <h3>物件 列表渲染 (值, 屬性, index)</h3>
    <h4 style="margin:5px;">v-for="(val, key, index) in obj"</h4>
    <ul style="margin:5px;">
      <li v-for="(val, key, index) in card" :key="val">
        <p>val: {{ val }}</p>
        <p>key: {{ key }}</p>
        <p>index: {{ index }}</p>
      </li>
    </ul>

    <h4 style="margin:5px;">⭐ 如要確保物件順序，可將物件轉為陣列再進行排序</h4>
    <h4 style="margin:5px;">物件：{ '測試':'bbb', '3':'333', 'a':'aaa', '1':'111' }</h4>
    <ul style="margin:5px;">
      <li v-for="(val, key, index) in oddObj" :key="val">
        <p>val: {{ val }}</p>
        <p>key: {{ key }}</p>
        <p>index: {{ index }}</p>
      </li>
    </ul>

    <h4 style="margin:5px;">轉成 ｍap {{ oddObj2Arr }}</h4>
    <ul style="margin:5px;">
      <li v-for="(val, index) in oddObj2Arr" :key="val">
        <p>val: {{ val }}</p>
        <p>index: {{ index }}</p>
      </li>
    </ul>

    <h4 style="margin:5px;">數字 列表渲染</h4>
    <ul class="pagination">
    <li class="page-item" @click.prevent><a class="page-link" href>&lt;</a></li>
      <li class="page-item" v-for="page in 10" :key="page" @click.prevent>
        <a class="page-link" href>{{ page }}</a>
      </li>
      <li class="page-item" @click.prevent><a class="page-link" href>&gt;</a></li>
    </ul>

    <h4 style="margin:5px;">template 列表渲染</h4>
    <div class="dropdown-menu">
      <template v-for="i in links" :key="i">
        <div class="dropdown-divider"></div>
        <a class="dropdown-item" :href="i.link">{{ i.title }}</a>
      </template>
    </div>
    <hr>
    <hr>

    <h2>v-for 列表的排序與過濾</h2>
    <h4>computed 或 methods</h4>
    <span class="block" v-for="i in evenNumbers" :key="i">
      {{i + ' ' }}
    </span>
    <hr>
    <hr>

    <h2>v-for 可以使用 index 當作 key 嗎？</h2>

  </div>
</template>

<script>
export default {
  props: {
    msg: String
  },
  data() {
    return {
      isShow: true,
      price: 0,
      miltiShow: true,
      miltiShow2: true,
      loginType: 'username',
      arr: ['A', 'B', 'C', 'D'],
      card: {
        name: 'gogo 卡',
        feeback: '6%',
        date: '2021/7/1~2022/1/31'
      },
      oddObj: {
        '測試':'bbb',
        '3':'333',
        'a':'aaa',
        '1':'111'
      },
      links: [{
        link: '#1',
        title: 'AAA'
      }, {
        link: '#2',
        title: 'BBB'
      }, {
        link: '#3',
        title: 'CCC'
      }],
      numbers: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    }
  },
  mounted() {
  },
  created: ()=>{
    console.log(this)
  },
  computed: {
    oddObj2Arr() {
      const myObject = new Map();
      const order = ['測試', 'a', 3, 1,]
      // const order = [1, 3, 'a', '測試']

      for (let key of order) {
        myObject.set(key, this.oddObj[key]);
      }
      return myObject
    },
    // 只顯示偶數
    evenNumbers () {
      return this.numbers.filter(number => number % 2 === 0);
    }
  },
  methods: {

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h2 {
  color: #38cf96;
  font-weight: 900;
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
.wrap {
  display: block;
  overflow: hidden;
  margin-top: 2rem;
}

.box {
  float: left;
  margin-right: 2rem;
  display: block;
  width: 100px;
  height: 100px;
  line-height: 100px;
  text-align: center;
  background-color: pink;
  color: #fff;
  font-size: 1rem;
  border: 1px solid #000;
}

.form-a {
  width: 50%;
  margin: 20px 0 50px;
}

.label-a {
  margin-right: 1rem;
}

.input-a:not([type]) {
  margin-left: 1rem;
  min-width: 300px;
  width: 50%;
  height: 1rem;
  line-height: 1rem;
  padding: 2px 3px;
}
</style>
