<template>
  <div class="hello">
    <h2>v-bind:is 與動態元件</h2>
      <input v-model="currentTab" type="radio" id="taba" name="TabA" :value="'TabA'">
      <label for="taba">TabA</label>

      <input v-model="currentTab" type="radio" id="tabb" name="TabB" :value="'TabB'">
      <label for="tabb">TabB</label>

      <component :is="currentTabComponent"></component>


    <h2>keep-alive 保留元件狀態</h2>
      <input v-model="currentTab" type="radio" id="taba" name="TabA" :value="'TabA'">
      <label for="taba">TabA</label>

      <input v-model="currentTab" type="radio" id="tabb" name="TabB" :value="'TabB'">
      <label for="tabb">TabB</label>

      <keep-alive>
        <component :is="currentTabComponent"></component>
      </keep-alive>


    <h2>include 、 exclude 與 max 屬性</h2>
      <h4>👉 include="TabA, TabB"，只保留 TabA 與 TabB 的狀態</h4>
      <input v-model="currentTab" type="radio" id="taba" name="TabA" :value="'TabA'">
      <label for="taba">TabA</label>

      <input v-model="currentTab" type="radio" id="tabb" name="TabB" :value="'TabB'">
      <label for="tabb">TabB</label>

      <input v-model="currentTab" type="radio" id="tabc" name="TabC" :value="'TabC'">
      <label for="tabc">TabC</label>

      <keep-alive include="TabA, TabB">
        <component :is="currentTabComponent"></component>
      </keep-alive>

      <h4>👉 exclude="TabA，不保留 TabA 的狀態</h4>
      <input v-model="currentTab" type="radio" id="taba" name="TabA" :value="'TabA'">
      <label for="taba">TabA</label>

      <input v-model="currentTab" type="radio" id="tabb" name="TabB" :value="'TabB'">
      <label for="tabb">TabB</label>

      <input v-model="currentTab" type="radio" id="tabc" name="TabC" :value="'TabC'">
      <label for="tabc">TabC</label>

      <keep-alive exclude="TabA">
        <component :is="currentTabComponent"></component>
      </keep-alive>

      <h4>👉 :max="2"，指定瀏覽器暫存的元件數量，只會保留最後引入的 2 個子元件狀態</h4>
      <input v-model="currentTab" type="radio" id="taba" name="TabA" :value="'TabA'">
      <label for="taba">TabA</label>

      <input v-model="currentTab" type="radio" id="tabb" name="TabB" :value="'TabB'">
      <label for="tabb">TabB</label>

      <input v-model="currentTab" type="radio" id="tabc" name="TabC" :value="'TabC'">
      <label for="tabc">TabC</label>

      <keep-alive :max="2">
        <component :is="currentTabComponent"></component>
      </keep-alive>

    <h2>Hooks: activated 與 deactivated</h2>
    <p>兩組 Hooks function 給 keep-alive 來使用，分別是 activated 與 deactivated 這兩個 lifecycle hook</p>

    <h4>👉 原始狀態，印出 created 、 mounted 、 unmounted 階段</h4>
    <p>「建立新的元件」(created) → 「銷毀目前元件」(unmounted) → 「掛載新的元件」(mounted)</p>
      <input v-model="currentTab" type="radio" id="taba" name="TabA" :value="'TabA'">
      <label for="taba">TabA</label>

      <input v-model="currentTab" type="radio" id="tabb" name="TabB" :value="'TabB'">
      <label for="tabb">TabB</label>

      <input v-model="currentTab" type="radio" id="tabc" name="TabC" :value="'TabC'">
      <label for="tabc">TabC</label>

      <!-- <component :is="currentTabComponent" @update="test"></component> -->

    <h4>👉 加回 keep-alive</h4>
      <!-- <keep-alive>
        <component :is="currentTabComponent" @update="test"></component>
      </keep-alive> -->

    <h4>👉 加回 keep-alive，加上 activated 與 deactivated 兩個 hook</h4>
    <p>「建立新的元件」(created) → 「暫停目前元件」(deactivated) → 「掛載新的元件」(mounted) → 「啟用新的元件」(activated) 這幾個階段</p>
      <keep-alive>
        <component :is="currentTabComponent" @update="test" @update2="test"></component>
      </keep-alive>
  </div>
</template>

<script>
import TabA from '@/components/TabA'
import TabB from '@/components/TabB'
import TabC from '@/components/TabC'

export default {
  components: {
    TabA,
    TabB,
    TabC
  },
  data() {
    return {
      currentTab: 'TabA'
    }
  },
  computed: {
    currentTabComponent () {
      return this.currentTab;
    }
  },
  methods: {
    test (str) {
      console.log(str)
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h2 {
  color: #25b57f;
  font-weight: 900;
  margin-top: 60px;
  margin-bottom: 10px;
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
  color: #25b57f;
}
</style>
