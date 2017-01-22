<template>
    <div id="app">
        <left class="span" :title.sync="title" :number.sync="number" :levels.sync="lvs"  style="width: 311px; " />
        <desk class="span" :title.sync="title" :number.sync="number" :levels.sync="lvs" style="width: 1085px; " />

    </div>
</template>

<script>
import Left from './components/left'
import Desk from './components/desk'

export default {
  name: 'app',
  components: {
      Left, Desk
  },
  data () {
    return {
        title: '欢迎同学！',
        lvs : [{
            text: '三等奖',
            used: 0,
            number: 10,
            lucky: [],
            left: 10
        }, {
            text: '二等奖',
            used: 0,
            number: 5,
            lucky: [],
            left: 5
        }, {
            text: '一等奖',
            used: 0,
            number: 2,
            lucky: [],
            left: 2
        }, {
            text: '特等奖',
            used: 0,
            number: 1,
            lucky: [],
            left: 1
            }
        ],
        number: 0
    };
  }
}

</script>

<style>
body {
    background: #fafafa;
    margin: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
    height: 720px;
    width: 1410px;
    margin: 20px auto;
}

#app .span {
    height: 720px;
    float: left;
}

</style>
