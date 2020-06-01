<template>
    <div class="home">
        <!-- <img alt="Vue logo" src="../assets/logo.png" /> -->
        <h1>Web Browser Fingerprint 検証サイト</h1>
        <ShowUserAgent />
    </div>
</template>

<script>
// @ is an alias to /src
import ShowUserAgent from "@/components/ShowUserAgent.vue";

export default {
    name: "Home",
    components: {
        ShowUserAgent
    }
};
</script>

<style scoped lang="scss">
h1 {
    margin-top: 4rem;
}
</style>
