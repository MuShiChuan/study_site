<template>
    <div>
        EmailRegister <br/>
        <div class="bottom">
            <a @click.prevent="setComName" href="javascript:;">返回</a>
        </div>
    </div>
</template>

<script>
    export default {
        name: "EmailRegister",
        methods:{
            setComName(){
                this.$emit('setComName','Login')
            }
        },
    }
</script>

<style scoped>

</style>