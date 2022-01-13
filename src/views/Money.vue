<template>
  <div class="nav-rapper">
    <div class="content">
      记账
    </div>
    <Nav/>
  </div>
</template>

<script lang="ts">
export default {
  name: 'Money'
};
</script>

<style lang="scss" scoped>
.nav-rapper {
  border: 1px solid green;
  display: flex;
  flex-direction: column;
  height: 100vh;
}

.content {
  flex-grow: 1;
  overflow: auto;
}
</style>