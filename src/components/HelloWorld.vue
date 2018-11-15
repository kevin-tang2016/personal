<template>
    <div class="hello-world">
        <input type="text" v-model="inputVal">
        <h1>{{reversedMsg }}</h1>
        <button>点击</button>
        <h5 v-for="(item,index) in arr"  :key="index" @click="clickEvent(index)">{{item}}<br/></h5>
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
</template>

<script>
    import _ from 'lodash'
    import  Name  from "./name"
    import  CustomInput  from "./custom-input"
    import  BaseCheckbox  from "./base-checkbox"
export default {
    name: 'HelloWorld',
    components:{
        Name,
        CustomInput,
        BaseCheckbox
    },
    data () {
        return {
            msg: 'tang',
            inputVal:"",
            arr:["test1","test2","test3"],
            searchText:"子组件自动聚焦",
            checked:true,
             lastIndex:""
        }
    },
    mounted(){
        if(this.$refs.customInput){
            this.$refs.customInput.focus()
        }
    },
    methods : {
        clickEvent(index){
            if(this.lastIndex === index){
                return
            }
            this.arr.splice(index,1,`clicked${index}`)
            this.lastIndex = index
        },
        changed(){
            this.msg ="tang by changed"
        }
    },
    watch:{
        inputVal(newVal,oldVal){
            console.log(`newVal-${newVal},oldVal-${oldVal}`)
        },
        checked(newVal,oldVal){
            console.log(`newVal-${newVal},oldVal-${oldVal}`)
        }
    },
    computed:{
        reversedMsg(){
            return this.msg.split('').reverse().join('')
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
</style>
