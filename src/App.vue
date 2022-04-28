<template>
  <div class="container">
    <Drag />
    <!-- <Sales /> -->
    <!-- <Graph /> -->
    <!-- <div>
      <SearchBar
        v-model="searchQuery"
        @Store-Item="updateList()"
        @Clear-Search="searchQuery = ''"
      />
      <List />
    </div> -->
    <!-- <div>
      <button
        class="sort--btn"
        @click="sortByKey('name')"
        :class="defaultSortKey === 'name' ? 'active' : ''"
      >
        Sort by Value
      </button>
      <button class="sort--btn" @click="sortByKey('date')">
        Sort by Added date
      </button>
    </div> -->
  </div>
</template>

<script lang="ts" setup>
// import { ref, provide, onMounted, computed, onBeforeUnmount } from "vue";
import Drag from "@/components/dragndrop.vue";
// import SearchBar from "./components/TheSearchBar.vue";
// import List from "./components/List.vue";
// import Graph from "./components/graph.vue";
// import Sales from "./components/sales.vue";

// interface Item {
//   name: string;
//   no: number;
//   date: string;
//   exactMatch: boolean;
// }

// let searchQuery = ref("");

// const list = ref<Item[]>([]);

// const defaultSortKey = ref("name");

// const exactMatch = computed(() => {
//   return list.value.some((item) => item.name === searchQuery.value);
// });

// function sortByKey(value: string) {
//   localStorage.setItem("sortKey", value);
//   list.value.sort((a, b) => {
//     if (value === "name") {
//       return a.name.localeCompare(b.name);
//     } else {
//       let dateA = new Date(a.date);
//       let dateB = new Date(b.date);
//       return dateB.getTime() - dateA.getTime();
//     }
//   });
// }
// const dataSource = computed(() => {
//   let sortedList = [...list.value];
//   sortedList = sortedList
//     .filter((item) => {
//       return (
//         item.name.toLowerCase().indexOf(searchQuery.value.toLowerCase()) >= 0
//       );
//     })
//     .map((item) => {
//       if (item.name.toLowerCase() === searchQuery.value.toLowerCase()) {
//         return { ...item, exactMatch: true };
//       }
//       return item;
//     });
//   return sortedList;
// });

// provide("list", {
//   dataSource,
//   exactMatch,
//   updateList,
//   deleteItem,
// });

// function deleteItem(value: number) {
//   const updatedList = list.value.filter((item) => item.no !== value);
//   list.value = [...updatedList];
//   localStorage.setItem("list", JSON.stringify(list.value));
// }

// function updateList() {
//   let newItem: Item = {
//     name: searchQuery.value,
//     no: list.value.length + 1,
//     date: new Date().toString(),
//     exactMatch: false,
//   };

//   let localList = JSON.parse(localStorage.getItem("list") as string);

//   if (localList) {
//     list.value = [...localList];
//   }
//   if (searchQuery.value) {
//     list.value.push(newItem);
//   }

//   localStorage.setItem("list", JSON.stringify(list.value));
//   searchQuery.value = "";
// }

// function attachEscListner(value: boolean) {
//   const callback = (e: any) => {
//     if (e.code === "Escape") searchQuery.value = "";
//   };
//   if (value) {
//     document.addEventListener("keyup", callback);
//   } else {
//     document.removeEventListener("keyup", callback);
//   }
// }

// onMounted(() => {
//   updateList();
//   if (localStorage.sortKey) {
//     sortByKey(localStorage.sortKey);
//   } else {
//     sortByKey(defaultSortKey.value);
//   }
//   attachEscListner(true);
// });

// onBeforeUnmount(() => {
//   attachEscListner(false);
// });
</script>

<style lang="scss">
.container {
  display: grid;
  grid-template-rows: 1fr;
  grid-template-columns: 1fr 1fr;
  gap: 10px;
}
.btn__sort--value {
  background: none;
}

.active {
  background: white;
  border: none;
}
</style>
