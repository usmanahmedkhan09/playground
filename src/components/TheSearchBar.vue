<template>
  <div>
    <input
      class="searchBar__input"
      type="text"
      name="search"
      autocomplete="off"
      placeholder="Search or Add..."
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
    />
    <div class="buttons-wrapper" v-if="modelValue">
      <button @click="$emit('ClearSearchQuery')">
        <img
          @click="$emit('ClearSearchQuery')"
          src="/clear.svg"
          alt="clear"
          srcset=""
        />
      </button>
      <button :disabled="exactMatch" @click="$emit('StoreItemInList')">
        <img src="/add.svg" alt="add" srcset="" />
      </button>
    </div>
  </div>
</template>
<script lang="ts" setup>
import { defineProps, defineEmits, inject } from "vue";

const { exactMatch } = inject("list");

defineProps(["modelValue"]);
defineEmits(["update:modelValue", "StoreItemInList", "ClearSearchQuery"]);
</script>

<style scoped lang="scss">
.container {
  position: relative;
}
.buttons-wrapper {
  position: absolute;
  top: 1rem;
  left: 75rem;
  display: flex;
  width: 5rem;
  justify-content: space-around;

  & button {
    background: none;
    border: none;
  }
}
.searchBar__input {
  width: -webkit-fill-available;
  height: 60px;
  background: #f1f3f5 0% 0% no-repeat padding-box;
  border-radius: 6px;
  opacity: 1;
  margin: auto;
  border: none;
  padding-inline: 1rem;
  font-size: 1rem;

  &:focus {
    outline: none;
  }

  &::placeholder {
    color: #adb5bd;
    opacity: 1;
    font: normal normal normal 14px/19px Open Sans;
  }
}
</style>
