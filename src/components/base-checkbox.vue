<template>
    <div class="base-checkbox">
        <input type="checkbox" :checked="checked" @change="change">
    </div>
</template>
<script>
export default {
    name: 'BaseCheckbox',
    model: {
        prop: 'checked',
        event: 'change'
    },
    props: {
        checked: Boolean
    },
    data () {
        return {

        }
    },
    methods : {
        change($event){
            this.$emit('change',$event.target.checked)
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
