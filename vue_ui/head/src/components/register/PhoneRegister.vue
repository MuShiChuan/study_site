<template>
    <div>
        PhoneRegister <br/>
        <div class="bottom">
            <a @click.prevent="setComName" href="javascript:;">返回</a>
        </div>
    </div>
</template>

<script>
    export default {
        name: "PhoneRegister",
        methods:{
            setComName(){
                this.$emit('setComName','Login')
            }
        },
    }
</script>

<style scoped>

</style>