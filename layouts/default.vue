<template>
    <div class="relative min-h-screen bg-gray-100">
      <!-- Sidebar -->
      <div class="fixed top-0 left-0 h-full z-20">
        <Sidebar :activeItem="activeItem" @selectItem="selectItem" />
      </div>
      <!-- Horizontal bar -->
      <div class="sticky top-0 p-2 text-white z-10 w-full" :style="{ backgroundColor: 'rgba(140, 157, 166, 0.9)', left: '15rem', width: 'calc(100% - 15rem)' }">
        <div class="flex items-center">
          <!-- White squares with larger Docker icons -->
          <div v-for="(item, index) in allItems" :key="index" @click="selectItem(item.name)" :class="{'border border-blue-500': activeItem === item.name, 'bg-blue-100': activeItem === item.name}" class="w-12 h-12 bg-white m-1 rounded-lg flex items-center justify-center cursor-pointer hover-effect">
            <Icon :name="item.icon" class="text-blue-500 w-8 h-8" />
          </div>
        </div>
      </div>
      <div class="flex flex-1 ml-60">
        <!-- Main content -->
        <MainContent backgroundImage="/backgroundrevolui.png">
          <nuxt />
          <div v-if="selectedImage" class="w-full h-full flex items-center justify-center mt-4">
            <img :src="`/images/${selectedImage}`" alt="Displayed Image" class="max-w-full max-h-full object-cover" />
          </div>
        </MainContent>
      </div>
    </div>
  </template>
  
  <script>
  import Sidebar from '@/components/Sidebar.vue';
  import MainContent from '@/components/MainContent.vue';
  import { mapping } from '@/data/mapping';
  
  export default {
    components: {
      Sidebar,
      MainContent,
    },
    data() {
      return {
        selectedImage: null,
        activeItem: null,
        activeSidebarItem: null,
        lists: mapping.lists
      };
    },
    computed: {
      allItems() {
        return Object.values(this.lists).flatMap(list => list.items);
      }
    },
    methods: {
      selectItem(itemName) {
        const selected = this.findItem(itemName);
        if (selected) {
          this.selectedImage = selected.image;
          this.activeItem = itemName;
          this.activeSidebarItem = selected.sidebarItem;
        }
      },
      findItem(itemName) {
        for (const list of Object.values(this.lists)) {
          for (const item of list.items) {
            if (item.name === itemName) {
              return item;
            }
          }
        }
        return null;
      }
    }
  };
  </script>
  
  <style scoped>
  .hover-effect {
    transition: box-shadow 0.3s ease;
  }
  .hover-effect:hover,
  .border-blue-500 {
    box-shadow: 0 0 10px 5px rgba(0, 123, 255, 0.5);
  }
  .bg-blue-100 {
    background-color: #ebf8ff;
  }
  .bg-blue-700 {
    background-color: #2b6cb0;
  }
  </style>
  