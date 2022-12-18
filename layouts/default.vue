<template>
  <v-app>
    <nuxt></nuxt>
    <Dialog />
  </v-app>
</template>

<script>
import Dialog from '~/components/Dialog'

export default {
  components: {
    Dialog
  }
}
</script>


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
  color: #C397FF !important;
}
.text-main {
  font-size: 20px;
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
  min-height: 50px;
  &.outlined {
    border: 1px solid #C397FF;
    border-radius: 28px;
    line-height: normal;
    letter-spacing: 0.0892857143em;
    text-indent: 0.0892857143em;
    user-select: none;
    white-space: nowrap;
  }
}
.set-padding {
  padding: 0 10px;
}
</style>