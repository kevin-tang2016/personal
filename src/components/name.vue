<template>
    <div class="name">
        {{name}}<br/>
        <button @click="changeParent">调用父方法</button><br/>
        <slot name="second"></slot>
        <slot name="first"></slot>
        <slot></slot>
    </div>
</template>
<script>
export default {
    name: 'Name',
    props:["name"],
    data () {
        return {

        }
    },
    methods : {
        changeParent(){
            this.$emit("changed")
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
