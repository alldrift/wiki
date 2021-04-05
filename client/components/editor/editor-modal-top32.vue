<template lang='pug'>
  v-card.editor-modal-media.animated.fadeInLeft(flat, tile, :class='`is-editor-` + editorKey')
    v-container.pa-3(grid-list-lg, fluid)
      v-layout(row, wrap)
        v-card.radius-7.animated
          v-card-text
            h1 hello
        //- v-card.radius-7.animated.fadeInLeft.wait-p1s(:light='!$vuetify.theme.dark', :dark='$vuetify.theme.dark')
            v-card-text
              h1 HELLOOO
</template>
<script>
export default {

}
</script>


<style lang='scss'>
.editor-modal-media {
  position: fixed !important;
  top: 112px;
  left: 64px;
  z-index: 10;
  width: calc(100vw - 64px - 17px);
  height: calc(100vh - 112px - 24px);
  background-color: rgba(darken(mc('grey', '900'), 3%), .9) !important;
  overflow: auto;
}
</style>
