<template>
  <div class="page">
    <div class="list-wrapper">list</div>
    <div class="sidebar-wrapper">
      sidebar
    </div>
  </div>
</template>
<style lang="scss" scoped>
.page {
  display: flex;
  flex-flow: row nowrap;
  justify-content: space-between;
  height: 100%;
  width: 100%;
}

.list-wrapper {
  background-color: aquamarine;
  height: 100%;
  width: 70%;
}
.sidebar-wrapper {
  background-color: lemonchiffon;
  height: 100%;
  width: 30%;
}
</style>
