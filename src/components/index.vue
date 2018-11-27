<template>
    <div class="index-page">
        <audio src="/static/audio.mp3" autoplay loop></audio>
        <div class="square">
            <img src="/static/timg.gif" alt="">
            <!--<div class="tips">{{timeout}}</div>-->
        </div>
        <div class="edit_wrap  none" :class="{ }">
            <input type="text" v-model="inputVal">
            <h1>{{reversedMsg }}</h1>
            <h1>vuex:{{name }}</h1>
            <button @click="changeName">点击改变vuex 状态</button>
            <h5 v-for="(item,index) in arr"  :key="index" @click="clickEvent(index)">{{item | changeText | toUpper }}<br/></h5>
            <Name :name="msg" @changed="changed">
                <template slot="first">
                    <div>需要放到子组件的内容slot--click name1</div>
                </template>
                <template slot="second">
                    <div>slot--->需要放到子组件的内容{{inputVal}}</div>
                </template>
                <div>其他DOM部分</div>
                <custom-input v-model="searchText" ref="customInput" />
            </Name>
            <base-checkbox v-model="checked" />
        </div>
    </div>
</template>

<script>
    import _ from 'lodash'
    import  { mapState,mapActions }  from 'vuex'
    import  Carousel  from "./carrousel"
    import  Name  from "./name"
    import  CustomInput  from "./custom-input"
    import  BaseCheckbox  from "./base-checkbox"
export default {
    name: 'Index',
    components:{
        Carousel,
        Name,
        CustomInput,
        BaseCheckbox
    },
    data () {
        return {
            isActive:false,
            timeout:10,
            msg: 'tang',
            inputVal:"",
            arr:["test1","test2","test3"],
            searchText:"子组件自动聚焦",
            checked:true,
            lastIndex:""
        }
    },
    filters:{
        changeText(value){
            if(!value) return ""
            value = value.toString()
            return _.capitalize(value)
        },
        toUpper(value){
            return _.toUpper(value)
        }
    },
    mounted(){
        if(this.$refs.customInput){
            this.$refs.customInput.focus()
        }
    },
    methods : {
        timeouted(){
            let time = setInterval(()=>{
                if(!this.timeout){
                    this.isActive = true
                    clearInterval(time)
                   return
                }
                this.timeout--
            },1000)
        },
        clickEvent(index){
            if(this.lastIndex === index){
                return
            }
            this.arr.splice(index,1,`clicked${index}`)
            this.lastIndex = index
        },
        changed(){
            this.msg ="tang by changed"
        },
        ...mapActions(["changeName"])
    },
    watch:{

    },
    computed:{
        ...mapState([
                "name"
        ]),
        reversedMsg(){
            return this.msg.split('').reverse().join('')
        }
    },
    mounted(){
//        this.timeouted()
    }
}
</script>
<style scoped lang="less">
.square{
    position: absolute;
    left:0;
    right:0;
    top:0;
    bottom:0;
    margin:auto;
    width:500px;
    height:350px;
    img{
        display: block;
        width:100%;
        height:317px;;
    }
    .tips{
        font-size:20px;
        margin:2px 0;
    }
}
h1, h2 {
  font-weight: normal;
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
.none{
    display: none;
}
.edit_wrap{
    position: absolute;
    left:0;
    right:0;
    margin:0 auto;
}
.block{
    display: block;
    opacity: 1;
    filter:alpha(opacity=1);
    transition:opacity 1s linear;
}
</style>
