<template>
  <header class="header">
    <h1 class="header__title">Notes</h1>
    <form class="header__form">
        <input type="text" class="header__form-input" placeholder="Search..." v-model="search">
    </form>
  </header>
</template>

<script>
export default {
   data() {
     return {
        search: ''
     }
  },
  watch: {
      search(val) {
        this.$emit('getSearch' , val)
      }
  }
}
</script>

<style  >
   .header {
    padding: 20px 0;
    box-shadow: var(--secondaryShadow);
   }
   .header__title {
    text-align: center;
    margin-bottom: 8px;
   }
   .header__form {
    text-align: center;
   }
   .header__form-input {

    padding: 10px  15px;
    box-shadow: var(--secondaryShadow);
    border: 0;
    border-radius: 5px;
   }
</style>