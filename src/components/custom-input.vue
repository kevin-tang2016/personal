<template>
    <div class="custom-input">
        <input type="text" :value="value" @input="input" ref="input">
    </div>
</template>
<script>
export default {
    name: 'CustomInput',
    props:["value"],
    data () {
        return {

        }
    },
    methods : {
        input($event){
            this.$emit('input',$event.target.value)
        },
        focus(){
            this.$refs.input.focus()
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
