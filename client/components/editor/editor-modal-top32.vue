<template lang='pug'>
  v-card.editor-modal-media.animated.fadeInLeft(flat, tile, :class='`is-editor-` + editorKey')
    v-container.pa-3(grid-list-lg, fluid)
      v-row
        v-col.d-flex.justify-center.align-center(cols=2)
          v-card.modal-input
            v-card-title.justify-center Top-32
            v-card-subtitle.text-center Insert 32 pilots
            v-card-text
              v-textarea(outlined, autgrow, rows=32, row-height=10, v-model="input")
            v-card-actions.justify-center
              v-btn(v-on:click="handleExample") Example
              v-btn(v-on:click="handleGenerate") Generate
        v-col
          v-card
            v-card-title.justify-center Tournament bracket
            v-card-text(id="bracket")
              top-32-bracket(:list="list")
            v-card-actions.justify-center
              v-btn(v-on:click="handleAdd") Add

</template>
<script>
import Top32Bracket from './top-32/top-32-bracket'
export default {
  data() {
    return {
      input: '',
      list: Array(32).fill("")
    }
  },
  components: {
    Top32Bracket
  },
  methods: {
    handleExample: function() {
      console.log('handleExample');
      this.input = example;
    },
    handleGenerate: function() {
      console.log('handleGenerate');
      const list = this.input.split('\n').filter(i => i);
      const length = list.length;
      if (length !== 32) {
        console.log('error');
        // this.error = `Provided items: ${length}. Required: 32`;
      }
      this.list = list;

    },
    handleAdd: function() {
      console.log('add');
      const elem = document.getElementById('bracket');
      let inner = elem.innerHTML;
      this.$root.$emit('editorInsert', {
        kind: 'TOP32',
        html: inner
      });
    }
  }
}

const example =
`81 Лосев Евгений
69 Головня Алексей
78 Идиятулин Дамир
31 Чивчян Георгий
10 Пучинин Аркадий
47 Щербак Анатолий
95 Горковенко Николай
5 Воробьев Федор
21 Гусев Григорий
24 Ермохин Дмитрий
13 Федоров Илья
22 Григорьев Евгений
17 Омаров Магомед
72 Дубовик Антон
71 Сак Сергей
15 Азаров Степан
8 Астапов Андрей
90 Шиков Никита
14 Чивчян Владимир
27 Кабаргин Сергей
6 Тиводар Роман
88 Цареградцев Аркадий
43 SHAK
79 Абрамов Борис
77 Дзежиц Федор
30 Онегов Аким
23 Никулин Иван
70 Бибаев Георгий
19 Фетисов Никита
75 Тихомиров Дмитрий
11 Куренбин Иван
55 Ружейников Евгений`;
</script>


<style lang='scss'>
.modal-input {
  height: 100%;
}

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
