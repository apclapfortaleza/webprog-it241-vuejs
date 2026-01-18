<template>
  <div class="vanilla">
    <h2>{{ name }}</h2>
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: 'Vanilla!!!!!!',
      message: 'I LOVE VANILLA!!!!! and Chocolate'
    };
  }
};
</script>

<style>
 .vanilla {
  background-color: blue;
  padding: 2px;
  border-radius: 2px;
  color: white;
 }
</style>