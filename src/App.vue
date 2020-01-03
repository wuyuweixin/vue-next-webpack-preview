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
      <td>{{scount}}</td>
    </tr>
    <tr>
      <td>String</td>
      <td></td>
      <td>{{state.name}}</td>
    </tr>
    <tr>
      <td>Array[0]</td>
      <td>{{list[0]}}</td>
      <td>{{slist[0]}}</td>
    </tr>
    <tr>
      <td>Array[1]</td>
      <td>{{list[1]}}</td>
      <td>{{slist[1]}}</td>
    </tr>
    <tr>
      <td>Object</td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td>ref</td>
      <td></td>
      <td>{{scount}}</td>
    </tr>
    <tr>
      <td>state</td>
      <td></td>
      <td>{{scount}}</td>
    </tr>
    <tr>
      <td>state.ext</td>
      <td></td>
      <td>{{state.ext}}</td>
    </tr>
    <tr>
      <td>state.Array[0]</td>
      <td></td>
      <td>{{state.slist[0]}}</td>
    </tr>
    <tr>
      <td>state.Array[1]</td>
      <td></td>
      <td>{{state.slist[1]}}</td>
    </tr>
    <tr>
      <td>computed</td>
      <td>{{computedCount}}</td>
      <td>{{computedVal}}</td>
    </tr>
    <tr>
      <td>watch</td>
      <td>{{watchValue}}</td>
      <td>{{watchVal}}</td>
    </tr>
  </table>
  <div style="display: flex">
    <div @click="inc" class="btn">classic</div>
    <div @click="sinc" class="btn">composition</div>
  </div>
</template>

<script>
  import {ref, reactive, watch, computed} from 'vue'

  export default {
    setup() {
      const state = reactive({
        name: '',
        slist: [1, 2]
      })
      const scount = ref(0)
      const watchVal = ref(0)
      const slist = [2, 3]
      const sinc = () => {
        scount.value++
        state.slist[0]++
        state.slist[1]++
        slist[0]++
        slist[1]++
        state.ext = 10 * scount.value
        state.name = Math.random().toString(36).replace(/^0./, '')
      }
      watch(() => {
        watchVal.value = scount.value + 2
      })
      const computedVal = computed(() => {
        return scount.value + 1
      })

      return {
        state,
        slist,
        scount,
        watchVal,
        computedVal,
        sinc
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
      inc() {
        this.count++
        this.list[0]++
        this.list[1]++
      }
    },
    computed: {
      computedCount() {
        return this.count + 2
      }
    },
    watch: {
      count(newValue, oldValue) {
        this.watchValue = oldValue
      },
      scount(newValue) {
        console.log(newValue)
      }
    },
    beforeCreate() {
      console.log('beforeCreate')
    },
    created() {
      console.log('created')
    },
    beforeMount() {
      console.log('beforeMount')
    },
    mounted() {
      console.log('mounted')
    },
    beforeUpdate() {
      console.log('beforeUpdate')
    },
    beforeUnmount() {
      console.log('beforeUnmount')
    },
    deactivated() {
      console.log('deactivated')
    },
    activated() {
      console.log('activated')
    },
    unmounted() {
      console.log('unmounted')
    },
    updated() {
      console.log('updated')
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
