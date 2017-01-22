<template>
    <div class="desk">
        <h1>{{ title }}</h1>
        <div class="main">
            {{ number < 10 ? '0' + number : number }}
        </div>
        <div class="footer">
            <ul>
                <li v-for="(lv, i) in levels" >{{ lv.text }} ({{ lv.left < 10 ? '0' + lv.left : lv.left }}/{{ lv.number < 10 ? '0' + lv.number : lv.number }})：
                    <lv v-for="(lu, j) in lv.lucky"><span style="font-size: 2px; font-weight: 100;">{{ j+1 < 10 ? '0' + (j+1) : j+1 }}.</span><span style="font-size: 16px; font-weight: 800; color: red;">{{ lu < 10 ? '0' + lu : lu }}</span>;&nbsp;&nbsp;&nbsp;&nbsp;</lv></li>
            </ul>
        </div>
    </div>
</template>

<script>

export default {
  name: 'desk',
  props: ['title', 'number', 'levels'],
  data () {
    return {
    }
  }
}

</script>

<style>
    .desk {
        border: 1px solid #ddd;
        border-left: none;
        background: #fdfdfd;
    }

    .desk h1 {
        height: 155px;
        line-height: 155px;
        font-size: 68px;
        margin: 0px 0px;
    }

    .desk .main {
        font-weight: 900;
        font-size: 26em;
        line-height: 455px;
        height: 445px;
        border-top: 1px solid;
        border-bottom: 1px solid;
    }

    .desk .footer {
        background: #ececec;
        height: 118px;
    }

    .desk ul {
        text-align: left;
        margin: 0;
        padding: 8px 40px;

    }
    .desk ul li {
        font-size: 18px;
    }
    .desk ul li lv {
        font-weight: 900;
    }
</style>

