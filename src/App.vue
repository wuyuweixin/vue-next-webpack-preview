<template>
  <div class="top"><img src="./logo.png" alt="">
    <h1>Hello Vue 3!</h1></div>
  <table>
    <tr>
      <th class="type">type</th>
      <th class="classic">classic</th>
      <th class="composition">composition</th>
    </tr>
    <tr>
      <td>Number</td>
      <td>{{count}}</td>
      <td>{{cCount}}</td>
    </tr>
    <tr>
      <td>String</td>
      <td></td>
      <td>{{state.name}}</td>
    </tr>
    <tr>
      <td>Array[0]</td>
      <td>{{list[0]}}</td>
      <td>{{cList[0]}}</td>
    </tr>
    <tr>
      <td>Array[1]</td>
      <td>{{list[1]}}</td>
      <td>{{cList[1]}}</td>
    </tr>
    <tr>
      <td>Object</td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td>ref</td>
      <td></td>
      <td>{{cCount}}</td>
    </tr>
    <tr>
      <td>state</td>
      <td></td>
      <td>{{cCount}}</td>
    </tr>
    <tr>
      <td>state.ext</td>
      <td></td>
      <td>{{state.ext}}</td>
    </tr>
    <tr>
      <td>state.Array[0]</td>
      <td></td>
      <td>{{state.list[0]}}</td>
    </tr>
    <tr>
      <td>state.Array[1]</td>
      <td></td>
      <td>{{state.list[1]}}</td>
    </tr>
    <tr>
      <td>computed</td>
      <td>{{computedValue}}</td>
      <td>{{computedVal}}</td>
    </tr>
    <tr>
      <td>watch</td>
      <td>{{watchValue}}</td>
      <td>{{watchVal}}</td>
    </tr>
  </table>
  <div style="display: flex">
    <div @click="classic" class="btn">classic</div>
    <div @click="composition" class="btn">composition</div>
  </div>
</template>

<script>
  import {
    ref,
    reactive,
    watch,
    computed,
    onBeforeMount,
    onUpdated,
    onActivated,
    onBeforeUnmount,
    onBeforeUpdate,
    onDeactivated,
    onErrorCaptured,
    onMounted,
    onRenderTracked,
    onRenderTriggered,
    onUnmounted
  } from 'vue'

  const debug = false

  function log(msg = '') {
    debug && console.log(msg)
  }

  export default {
    setup() {
      const state = reactive({
        name: '',
        list: [1, 2]
      })
      const cCount = ref(0)
      const watchVal = ref(0)
      const cList = [2, 3]
      const composition = () => {
        cCount.value++
        state.list[0]++
        state.list[1]++
        cList[0]++
        cList[1]++
        state.ext = 10 * cCount.value
        state.name = Math.random().toString(36).replace(/^0./, '')
      }
      watch(() => {
        watchVal.value = cCount.value + 2
      })
      const computedVal = computed(() => {
        return cCount.value + 1
      })

      onBeforeMount(() => {
        log('composition:onBeforeMount')
      })
      onUpdated(() => {
        log('composition:onUpdated')
      })
      onActivated(() => {
        log('composition:onActivated')
      })
      onBeforeUnmount(() => {
        log('composition:onBeforeUnmount')
      })
      onBeforeUpdate(() => {
        log('composition:onBeforeUpdate')
      })
      onDeactivated(() => {
        log('composition:onDeactivated')
      })
      onErrorCaptured(() => {
        log('composition:onErrorCaptured')
      })
      onMounted(() => {
        log('composition:onMounted')
      })
      onRenderTracked((e) => {
        log(e)
        log('composition:onRenderTracked')
      })
      onRenderTriggered((e) => {
        log(e)
        log('composition:onRenderTriggered')
      })
      onUnmounted(() => {
        log('composition:onUnmounted')
      })
      return {
        state,
        cList,
        cCount,
        watchVal,
        computedVal,
        composition
      }
    },
    data() {
      return {
        count: 0,
        list: [1, 2],
        watchValue: 0,
        open: false
      }
    },
    methods: {
      classic() {
        this.count++
        this.list[0]++
        this.list[1]++
      }
    },
    computed: {
      computedValue() {
        return this.count + 2
      }
    },
    watch: {
      count(newValue, oldValue) {
        this.watchValue = oldValue
      },
      cCount(newValue) {
        log(newValue)
      }
    },
    beforeCreate() {
      log('classic:beforeCreate')
    },
    created() {
      log('classic:created')
    },
    beforeMount() {
      log('classic:beforeMount')
    },
    mounted() {
      log('classic:mounted')
    },
    beforeUpdate() {
      log('classic:beforeUpdate')
    },
    beforeUnmount() {
      log('classic:beforeUnmount')
    },
    deactivated() {
      log('classic:deactivated')
    },
    activated() {
      log('classic:activated')
    },
    unmounted() {
      log('classic:unmounted')
    },
    updated() {
      log('classic:updated')
    }
  }
</script>

<style scoped>
  * {
    margin: 0;
    padding: 0;
  }

  *:focus {
    outline: none;
  }

  html, body {
    height: 100%;
  }

  table {
    width: 100%;
    border-collapse: collapse;
  }

  table, th, td {
    border: 1px #35495e solid;
  }

  th {
    background-color: #41b883;
  }

  td {
    text-align: center;
  }

  th, td {
    padding: 6px 0;
  }

  .type {
    width: 28%;
  }

  .classic {
    width: 36%;
  }

  .composition {
    width: 36%;
  }

  img {
    height: 45px;
    display: inline-block;
  }

  p {
    font-weight: bold;
  }

  h1 {
    font-family: Arial, Helvetica, sans-serif;
    display: inline-block;
  }


  .btn {
    width: 100%;
    flex: 1;
    background-color: #41b883;
    border: none;
    height: 50px;
    margin: 10px 0;
    line-height: 50px;
    font-size: 1.5em;
    text-align: center;
    border-radius: 4px;
  }

  .btn:first-child {
    margin-right: 4px;
  }

  .btn:last-child {
    margin-left: 4px;
  }

  .top {
    margin-top: 30px;
    height: 45px;
    line-height: 45px;
    justify-content: center;
    display: flex;
  }
</style>
