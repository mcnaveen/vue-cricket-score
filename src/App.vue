<template>
  <router-view />
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Fira+Code:wght@300;400;500;600;700&display=swap");
body {
  font-size: 16px;
  background-color: #1d3557;
  height: 100vh;
  color: rgba(0, 0, 0, 0.6);
  font-family: "Fira Code", monospace;
  font-weight: 600;
  line-height: 1.618;
  -webkit-font-smoothing: antialiased;
  -moz-font-smoothing: grayscale;
  overflow-x: hidden;
}
::-webkit-scrollbar {
  width: 8px;
  height: 8px;
}
::-webkit-scrollbar-thumb {
  background-color: rgba(182, 241, 87, 0.302);
  border-radius: 8px;
}
::-webkit-scrollbar-thumb:hover {
  background-color: rgba(191, 18, 253, 0.5);
}
</style>
