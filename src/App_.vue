<template>
  <div id ="app">
    <Dog breed="bulldog"/>
    </div>
</template>
<script>
import Dog from "./components/Dog";

export default {
  name: "app",
  components: {
    Dog
  }
};
</script>
