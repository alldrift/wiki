<template lang='pug'>
  v-card.editor-modal-media.animated.fadeInLeft(flat, tile, :class='`is-editor-` + editorKey')
    v-container.pa-3(grid-list-lg, fluid)
      v-row
        v-col.d-flex.justify-center.align-center(cols=2)
          v-card
            v-card-title.justify-center Top-32
            v-card-subtitle.text-center Insert 32 pilots
            v-card-text
              v-textarea(rows=10, row-height=10)
            v-card-actions.justify-center
              v-btn Generate
        v-col
          v-card
            v-card-title.justify-center Tournament bracket
            v-card-text
              <div>d</div>

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
