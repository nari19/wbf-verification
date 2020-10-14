<template>
  <footer class="footer">
    <div class="wrapper">
      <p>&copy;nari19 | 2020</p>
      <p></p>
    </div>
  </footer>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Footer extends Vue {}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
footer {
  width: 100%;
  color: #b3bcc5;
  padding: 30px 0;
  font-weight: bold;
}
</style>
