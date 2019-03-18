<template>
    <div>
    <button type="button" @click="reg1()">添加</button>
    </div>
</template>

<script>
    export default {
        name: "User",
        methods:{
            reg1() {
                this.$router.push('/add')
            }
        }
    }
</script>

<style scoped>

</style>
