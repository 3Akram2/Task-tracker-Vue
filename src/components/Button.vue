<template>
    <button @click="onClick()" v-bind:style="{backgroundColor: color}" class="btn">{{btext}}</button>
</template>
<script>
export default{
    name:'Button',
    props:{
        btext:String,
        color: String
    },
    methods:{
        onClick(){
            this.$emit('toggle-add-task')
        },

    }
}
</script>
