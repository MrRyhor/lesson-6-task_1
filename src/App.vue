<template>
    <user-age title="Please enter the user's age:" v-model:ageVal.check.setColor="ageValue" />    
</template>

<script>
import UserAge from './components/UserAge.vue'

export default {
    name: 'App',
    components: {
        UserAge,
    },

    data() {
        return {
            ageValue: null,
        }
    },
}
</script>

<style lang="scss">
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
