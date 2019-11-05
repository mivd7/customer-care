<template>
    <div class="topbar"> 
        <img src="../assets/carebare.png" alt="care" class="topbar__logo"/>
        <p class="topbar__language"><u>Language</u></p>
    </div>
</template>

<script>
export default {

}
</script>

<style>
    .topbar {
        background-color: #2f3069;
        color: #eee;
        height: 65px;
        width: 100%;
    }
    h1 {
        text-align: center;
    }
    .topbar__language {
        position: absolute;
        top: 5px;
        right: 40px;
        text-align: right;
        width: 50%;
    }
    .topbar__logo {
        margin: 10px;
        max-height: 75%;
        max-width: 30%;
    }
</style>