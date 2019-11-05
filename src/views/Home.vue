<template>
    <div class="cc-home">
      <TopBar />
      <Form />
    </div>
</template>

<script>
import Form from '../components/Form';
import TopBar from '../components/TopBar';

export default {
    name: 'Home',
    components: {
      Form,
      TopBar
    },

}
</script>

<style scoped>
    .cc-home {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        font-size: 1.2rem;
        height: 100vh;
        background: no-repeat url("../assets/bg.jpg");
        -webkit-background-size: cover;
        -moz-background-size: cover;
        -o-background-size: cover;
        background-size: cover;
    }
</style>