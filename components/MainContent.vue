<template>
    <div class="main-content flex-1 p-6 bg-cover bg-no-repeat" :style="{ backgroundImage: `url(${backgroundImage})` }">
      <slot></slot>
    </div>
  </template>
  
  <script>
  export default {
    name: 'MainContent',
    props: {
      backgroundImage: {
        type: String,
        required: true,
      },
    },
  };
  </script>
  
  <style scoped>
  .main-content {
    min-height: 100vh;
  }
  </style>
  