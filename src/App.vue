<template>
  <div class="animations__background">
    <AnimCategory />
    <AnimList />
  </div>
</template>

<script>
import "./global.css"
import AnimCategory from './components/AnimCategory.vue'
import AnimList from './components/AnimList.vue'

export default {
  name: 'App',
  components: {
    AnimList,
    AnimCategory
  }
}
</script>

<style>
#app {
  display: flex;
  justify-content: flex-end;
  background: no-repeat url('./assets/gta.jpg');
}
.animations__background{
  display: flex;
  justify-content: flex-end;
  background: linear-gradient(to left, #131A1BF2 0%, #131A1BF2 50%, #131A1B00 100%);
  width: 800px;
}
</style>
