<template>
  <div class="smartPage">
    <Title msg="SMART software activation" />
    <SoftwareActivation :file="fileExt" />
  </div>
</template>
<script>
import Title from "./components/Title.vue";
import SoftwareActivation from "./components/SoftwareActivation.vue";
export default {
  name: "App",
  components: { Title, SoftwareActivation },
  data() {
    return { fileExt: ".png" };
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.smartPage {
  display: flex;
  flex-direction: column;
}
</style>
