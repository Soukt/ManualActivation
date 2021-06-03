<template>
  <h1>{{ msg }}</h1>
</template>

<script>
export default {
  props: ["msg"],
};
</script>

<style>
h1 {
  text-align: left;
  font-size: 3em;
  width: 100%;
  padding: 1em 0 1em 1.5em;
  color: white;
  background-image: url("https://www.smarttech.com/-/media/images/about/genericbackground.jpg");
  background-size: cover;
  margin: 0px;
  font-weight: bold;
}
</style>
