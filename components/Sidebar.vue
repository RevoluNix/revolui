<template>
    <div class="w-60 bg-[#06283D] h-full flex flex-col p-4">
      <div>
        <div class="flex items-center mb-5">
          <img src="./public/avatar.png" alt="User Profile" class="rounded-full w-10 h-10 mr-2" />
          <div class="flex-grow">
            <span class="block font-bold text-sm text-white">Gabriel Guillou</span>
            <span class="block text-xs text-gray-400">12/09/2002</span>
          </div>
          <span class="w-5 h-5">
            <Icon name="mdi-cog" class="text-white w-full h-full" />
          </span>
        </div>
        <div class="flex justify-center mb-5">
          <div class="bg-[#526D7B] w-full max-w-xs p-2 rounded-full flex justify-around items-center">
            <button class="w-10 h-10 flex justify-center items-center">
              <Icon name="mdi-account" class="text-white w-6 h-6" />
            </button>
            <button class="w-10 h-10 flex justify-center items-center">
              <Icon name="mdi-folder" class="text-white w-6 h-6" />
            </button>
            <button class="w-10 h-10 flex justify-center items-center">
              <Icon name="mdi-lock" class="text-white w-6 h-6" />
            </button>
          </div>
        </div>
        <div class="mt-2 flex-grow">
          <div v-for="(list, key) in lists" :key="key" class="py-2 text-sm text-gray-400">
            <div class="flex justify-between items-center cursor-pointer" @click="toggleList(key)">
              <span>{{ list.title }}</span>
              <Icon :name="isListOpen(key) ? 'mdi-chevron-down' : 'mdi-chevron-right'" class="text-white" />
            </div>
            <div v-if="isListOpen(key)" class="ml-4">
              <div v-for="item in list.items" :key="item.name" @click="$emit('selectItem', item.name)" :class="{'bg-[#0F4C75]': activeItem === item.name}" class="py-2 text-sm text-gray-400 flex items-center cursor-pointer">
                <Icon :name="item.icon" class="mr-2" />
                {{ item.name }}
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import { reactive, computed } from 'vue';
  import { mapping } from '@/data/mapping';
  
  export default {
    props: {
      activeItem: String,
    },
    setup(props) {
      const openLists = reactive({});
      const lists = mapping.lists;
  
      // Open all lists by default
      Object.keys(lists).forEach(key => {
        openLists[key] = true;
      });
  
      const toggleList = (key) => {
        openLists[key] = !openLists[key];
      };
  
      const isListOpen = (key) => {
        return !!openLists[key];
      };
  
      const allItems = computed(() => {
        return Object.values(lists).flatMap(list => list.items);
      });
  
      return {
        openLists,
        lists,
        toggleList,
        isListOpen,
        allItems
      };
    }
  };
  </script>
  
  <style scoped>
  /* Additional styles if needed */
  </style>
  