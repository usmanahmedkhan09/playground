<template>
  <div>
    <p>{{ item.name }}</p>
    <p class="float--left" :class="item.exactMatch ? 'color' : ''">
      #{{ item.no }}
    </p>
  </div>
  <div>
    <span>
      {{
        formatDistance(subMinutes(new Date(item.date), 0), new Date(), {
          addSuffix: true,
        })
      }}
    </span>
    <img
      @click="deleteItem(item.no)"
      class="list-trash"
      src="/trash.svg"
      alt=""
      srcset=""
    />
  </div>
</template>
<script setup lang="ts">
import { formatDistance, subMinutes } from "date-fns";
import { defineProps, inject } from "vue";
const { deleteItem } = inject("list");
defineProps(["item"]);
</script>
