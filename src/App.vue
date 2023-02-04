<script setup>
import Main from './components/Main.vue'
</script>

<template>

    <Main/>
</template>

<style>
@import 'assets/fonts/fonts.css';

body {
    overflow-x: hidden;


}

body, * {
    margin: 0;
    padding: 0;
}
@media screen and (min-width: 1050px) {

    body{
        min-width: 500px;
    }
}

</style>
