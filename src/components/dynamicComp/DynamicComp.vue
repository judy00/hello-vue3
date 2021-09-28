<template>
  <div class="hello">
    <h2>v-bind:is 與動態元件</h2>
      <input v-model="currentTabVbind" type="radio" id="taba" name="TabA" :value="'TabA'">
      <label for="taba">TabA</label>

      <input v-model="currentTabVbind" type="radio" id="tabb" name="TabB" :value="'TabB'">
      <label for="tabb">TabB</label>

      <component :is="currentTabVbindComp"></component>


    <h2>keep-alive 保留元件狀態</h2>
      <input v-model="currentTabKeepAlive" type="radio" id="taba-keep-alive" name="TabA-keep-alive" :value="'TabA'">
      <label for="taba-keep-alive">TabA</label>

      <input v-model="currentTabKeepAlive" type="radio" id="tabb-keep-alive" name="TabB-keep-alive" :value="'TabB'">
      <label for="tabb-keep-alive">TabB</label>

      <keep-alive>
        <component :is="currentTabKeepAliveComp"></component>
      </keep-alive>


    <h2>include 、 exclude 與 max 屬性</h2>
      <h4>👉 include="TabA,TabB"，只保留 TabA 與 TabB 的狀態</h4>
      <input v-model="currentTabInclude" type="radio" id="taba-include" name="TabA-include" :value="'TabA'">
      <label for="taba-include">TabA</label>

      <input v-model="currentTabInclude" type="radio" id="tabb-include" name="TabB-include" :value="'TabB'">
      <label for="tabb-include">TabB</label>

      <input v-model="currentTabInclude" type="radio" id="tabc-include" name="TabC-include" :value="'TabC'">
      <label for="tabc-include">TabC</label>

      <keep-alive include="TabAName,TabBName">
        <component :is="currentTabIncludeComp"></component>
      </keep-alive>


      <h4>👉 exclude="TabA，不保留 TabA 的狀態</h4>
      <input v-model="currentTabExclude" type="radio" id="taba-exclude" name="TabA-exclude" :value="'TabA'">
      <label for="taba-exclude">TabA</label>

      <input v-model="currentTabExclude" type="radio" id="tabb-exclude" name="TabB-exclude" :value="'TabB'">
      <label for="tabb-exclude">TabB</label>

      <input v-model="currentTabExclude" type="radio" id="tabc-exclude" name="TabC-exclude" :value="'TabC'">
      <label for="tabc-exclude">TabC</label>

      <keep-alive :exclude="/Tab(AName|BName)/">
        <component :is="currentTabExcludeComp"></component>
      </keep-alive>


      <h4>👉 :max="1"，指定瀏覽器暫存的元件數量，只會保留最後引入的 1 個子元件狀態</h4>
      <input v-model="currentTabMax" type="radio" id="taba-max" name="TabA-max" :value="'TabA'">
      <label for="taba-max">TabA</label>

      <input v-model="currentTabMax" type="radio" id="tabb-max" name="TabB-max" :value="'TabB'">
      <label for="tabb-max">TabB</label>

      <input v-model="currentTabMax" type="radio" id="tabc-max" name="TabC-max" :value="'TabC'">
      <label for="tabc-max">TabC</label>

      <keep-alive :max="1">
        <component :is="currentTabMaxComp"></component>
      </keep-alive>


    <h2>Hooks: activated 與 deactivated</h2>
    <p>兩組 Hooks function 給 keep-alive 來使用，分別是 activated 與 deactivated 這兩個 lifecycle hook</p>

      <input v-model="currentTabCreate" type="radio" id="taba-create" name="TabA-create" :value="'TabA'">
      <label for="taba-create">TabA</label>

      <input v-model="currentTabCreate" type="radio" id="tabb-create" name="TabB-create" :value="'TabB'">
      <label for="tabb-create">TabB</label>

      <input v-model="currentTabCreate" type="radio" id="tabc-create" name="TabC-create" :value="'TabC'">
      <label for="tabc-create">TabC</label>

    <h4>👉 原始狀態，印出 created 、 mounted 、 unmounted 階段</h4>
    <p>「建立新的元件」(created) → 「銷毀目前元件」(unmounted) → 「掛載新的元件」(mounted)</p>

      <component :is="currentTabCreateComp" @update="printString"></component>

    <h4>👉 加回 keep-alive</h4>
    <p>只 created 和 mounted 一次</p>
      <!-- <keep-alive>
        <component :is="currentTabCreateComp" @update="printString"></component>
      </keep-alive> -->

    <h4>👉 加回 keep-alive，加上 activated 與 deactivated 兩個 hook</h4>
    <p>「建立新的元件」(created) → 「暫停目前元件」(deactivated) → 「掛載新的元件」(mounted) → 「啟用新的元件」(activated) 這幾個階段</p>
      <!-- <keep-alive>
        <component :is="currentTabCreateComp" @update="printString" @update2="printString"></component>
      </keep-alive> -->
  </div>
</template>

<script>
import TabA from '@/components/dynamicComp/TabA'
import TabB from '@/components/dynamicComp/TabB'
import TabC from '@/components/dynamicComp/TabC'

export default {
  components: {
    TabA,
    TabB,
    TabC
  },
  data() {
    return {
      currentTabVbind: 'TabA',
      currentTabKeepAlive: 'TabA',
      currentTabInclude: 'TabA',
      currentTabExclude: 'TabA',
      currentTabMax: 'TabA',
      currentTabCreate: 'TabA',
    }
  },
  computed: {
    currentTabVbindComp () {
      return this.currentTabVbind;
    },
    currentTabKeepAliveComp () {
      return this.currentTabKeepAlive;
    },
    currentTabIncludeComp () {
      return this.currentTabInclude;
    },
    currentTabExcludeComp () {
      return this.currentTabExclude;
    },
    currentTabMaxComp () {
      return this.currentTabMax;
    },
    currentTabCreateComp () {
      return this.currentTabCreate;
    }
  },
  methods: {
    printString (str) {
      console.log(str)
    },
  }
}
</script>

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
