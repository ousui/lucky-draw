<template>
    <div class="left">
        <img class="logo" src="../assets/logo.jpg"/>
        <div>
            <span class="field">
                　欢迎词：<input placeholder="输入欢迎词。" type="text" v-model="title" @input="$parent.title=$event.target.value;"/>
            </span>
            <span class="field">
                到场人数：<input v-model.number="people" type="number"/>
            </span>
            <span class="field">
                <label v-for="(lv, i) in levels"><input type="radio"
                                                        v-bind="picked"
                                                        @click="doing ? '' : picked = lv"
                                                        name="levels"
                                                        :value="i" :disabled="doing || lv.used == 1" />&nbsp;&nbsp;{{ lv.text }}
                    <input style="width: 40px; text-align: right;" v-model="lv.number" @input="lv.left=$event.target.value" type="number" /> <span style="font-size: 12px; font-weight: 100;">位</span> </label>
            </span>
            <span class="field">
                <button @click="startstop" >{{ !doing ? '开始抽奖' : '停　　止' }}</button>
            </span>
            <span class="field" style="color: red; text-align: center;">
                {{ msg }}
            </span>

        </div>
    </div>

</template>

<script>
import Desk from './desk'

export default {
  name: 'left',
  methods: {
    changez (tv) {
        this.$parent.title = tv;
    },
    startstop () {
        if (this.pool.length >= this.people) {
            this.msg = '抽奖人数不够啦！';
            this.$parent.number = 0;
            return;
        } else {
            this.msg = '　';
        }




        var status = true;
        if (this.doing) { // 正在抽奖，执行停止序列
            status = this.stop();
        } else { // 没有抽奖，执行开始序列。
            status = this.start();
        }

        if (status) {
            this.doing = !this.doing;
        }

    },
    start () {

        if (this.picked == null) {
            this.msg = '选择奖项！';
            return false;
        }


        if (this.picked.left == 0) {
            this.msg = '本轮抽奖完成，请选择下一组！';
            return false;
        }

        if (--this.picked.left == 0) {
            this.picked.used = 1;
        };

        var parent = this.$parent;
        var t = this;
        var startNo = this.getRandom();
        var i = 0;
        this.loop = setInterval(function() {
            if (startNo > t.people) { // 优先判断
                startNo = 1;
            }
            startNo++;
            if (t.pool.indexOf(startNo) < 0) {
                // 如果 startNo 在 pool 中，跳过本次循环
                t.picked.lucky[t.picked.number - t.picked.left - 1] = parent.number = startNo;

            }

            i++;
        }, 1);
        return true;
    },
    stop () {
        clearInterval(this.loop);
        var lucky = this.$parent.number;

        this.pool.push(lucky);
        return true;
    },
    getRandom() {
        return Math.floor(Math.random()*this.people)+1;
    }
  },
  data :function() {
    return {
        doing: false,
        title: this.$parent.title,
        people: 50,
        picked: null,
        levels: this.$parent.lvs,
        pool: [],
        msg: ' 　 '
    }
  }
}




</script>

<style>
.left {
    background: #ececec;
    border: 1px solid #ddd;
    border-right: none;
}

.left .field {
    width: 100%;
    padding: 5px 5px 2px 5px;
    display: block;
    text-align: left;
}

.left .field input:not([type="radio"]) {
    width: 200px;
    padding: 0px;
    margin: 0px;
    border: 0px;
    border-bottom: 1px dotted;
    background: transparent;
    font-size: 16px;
    font-weight: 900;
    color: #333;
}

.left .field label {
    width: 200px;
    display: block;
    margin: 5px auto;
    font-size: 24px;
    cursor: pointer;
    font-weight: 900;
}

.left .field label:last-child {
    color: red;
}

.left .field button {
    width: 280px;
    height: 48px;
    display: block;
    font-size: 24px;
    margin: 10px 10px;
    font-weight: 900;
    background: #fff;
    border: 1px solid;
    cursor: pointer;
}

.left .field button:hover {
    background: #efefef;
}

.left .field button:active {
    margin: 11px 9px 9px 11px;
}


</style>