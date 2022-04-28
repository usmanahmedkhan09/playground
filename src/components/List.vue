<template>
  <div class="list" v-for="item in dataSource" :key="item.no">
    <ListItem :item="item" />
  </div>
</template>
<script setup lang="ts">
import ListItem from "./ListItem.vue";
import { inject } from "vue";
const { dataSource } = inject("list");
</script>
<style lang="scss">
.list {
  height: 70px;
  background: #ffffff00 0% 0% no-repeat padding-box;
  border-radius: 6px;
  opacity: 1;
  border-bottom: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-inline: 1rem;

  &-trash {
    display: none;
  }

  &:hover {
    background: #ffffff 0% 0% no-repeat padding-box;
    box-shadow: 0px 0px 40px #0000000d;
    border: 1px solid #ffffff;
    border-radius: 6px;
    opacity: 1;

    .list-trash {
      display: inline-block;
    }
  }
}

p {
  margin: unset;
}

.float--left {
  float: left;
}
.color {
  color: #12b886;
}
</style>
