<template>
  <v-app>
    <nuxt></nuxt>
  </v-app>
</template>

<style lang="scss">
.v-application {
    font-family: 'Quicksand', sans-serif;
}
.v-toolbar__title {
    text-align: center;
    width: 100%;
    font-weight: bold;
}
.v-application .primary {
  background-color: #C397FF !important;
  border-color: #C397FF !important;
}
.text-primary {
  color: #C397FF;
}
.text-title {
  font-size: 20px;
  font-weight: bold;
}
.w-100 {
  width: 100%;
}
.my-btn {
  font-size: 20px !important;
  text-transform: none !important;
  height: auto !important;
  padding: 10px 0 !important;
  font-weight: bold;
}
</style>