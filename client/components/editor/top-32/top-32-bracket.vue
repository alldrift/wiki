<template>
  <div>
    <!-- <h1>Tournament table</h1> -->
    <div class="v-top32" v-if="list.length === 32">
      <top-32-column :header="'Top-32'" :index="0" :left="left[0]" :right="right[0]" :onChange="handleChange" />
      <top-32-column :header="'Top-16'" :index="1" :left="left[1]" :right="right[1]" :onChange="handleChange" />
      <top-32-column :header="'Top-8'" :index="2" :left="left[2]" :right="right[2]" :onChange="handleChange" />
      <top-32-column :header="'Top-4'" :index="3" :left="left[3]" :right="right[3]" :onChange="handleChange" />
      <top-32-final :gold="gold" :bronze="bronze" :onChange="handleFinals" />
    </div>
  </div>
</template>
<script>
import Top32Column from './top-32-column.vue'
import Top32Final from './top-32-final.vue'
export default {
  name: 'top-32-bracket',
  props: {
    list: Array
  },
  data() {
    return {
      input: '',
      // list: [],
      left: [],
      right: [],
      gold: {},
      bronze: {},
      error: ''
    }
  },
  watch: {
    list: function(oldV, newV) {
      if(oldV !== newV) {
        console.log(`old: ${JSON.stringify(oldV)}`)
        console.log(`new: ${JSON.stringify(newV)}`)
        this.generateBracket();
      }

    }
  },
  components: {
    Top32Column,
    Top32Final
  },
  methods: {
    handleChange: function(side, x, y, pairPosition, clear) {
      console.log(side, x, y, pairPosition);
      const newX = x + 1;
      const newY = y / 2 | 0;
      const newPairPosition = y % 2 == 0 ? 'upper' : 'lower';
      const oppositePairPosition = this.getOppositePairPosition(pairPosition);
      const pair = this[side][x][y];

      clear = pair[pairPosition].selected ? true : clear;
      this[side][newX][newY][newPairPosition] = clear ? this.getEmptyHalf() : {...pair[pairPosition]};
      if (pair[pairPosition].value) {
        pair[pairPosition].selected = !clear;
      }
      pair[oppositePairPosition].selected = false;

      if (x < 4) {
        this.handleChange(side, newX, newY, newPairPosition, true);
      }

      if (x == 3 && !clear && side === 'left') {
        this.gold.upper = {...pair[pairPosition]};
        this.gold.upper.selected = false;
        this.bronze.upper = {...pair[oppositePairPosition]};
        this.bronze.upper.selected = false;
      }
      else if (x == 3 && !clear && side === 'right') {
        this.gold.lower = {...pair[pairPosition]};
        this.bronze.lower = {...pair[oppositePairPosition]};
        this.gold.lower.selected = false;
        this.bronze.lower.selected = false;
      }
      else if (x == 3 && clear && side === 'left') {
        this.gold.upper = this.getEmptyHalf();
        this.bronze.upper = this.getPair();
      }
      else if (x == 3 && clear && side === 'right') {
        this.gold.lower = this.getEmptyHalf();
        this.bronze.lower = this.getPair();
      }
    },
    handleFinals: function(type, position) {
      console.log(`handleFinals: ${type} ${position}`);
      const opposite = this.getOppositePairPosition(position);
      const selected = this[type][position].selected;
      this[type][position].selected = !selected;
      this[type][opposite].selected = selected && !this[type][opposite].selected;
    },
    generateBracket: function() {
      // const list = this.input.split('\n').filter(i => i);
      // const length = list.length;
      // if (length !== 32) {
      //   this.error = `Provided items: ${length}. Required: 32`;
      // }
      // this.list = list;
      this.left = this.getLeft();
      this.right = this.getRight();
      this.gold = this.getPair();
      this.bronze = this.getPair();
    },
    getOppositePairPosition: function(pairPosition) {
      return pairPosition === 'upper' ? 'lower': 'upper';
    },
    getExample: function() {
      this.input = example;
    },
    getLeft: function() {
      return [
        this.getLeftTop32(),
        this.getEmptyTop(16),
        this.getEmptyTop(8),
        this.getEmptyTop(4),
        this.getEmptyTop(2),
        this.getEmptyTop(2)
      ]
    },
    getRight: function() {
      return [
        this.getRightTop32(),
        this.getEmptyTop(16),
        this.getEmptyTop(8),
        this.getEmptyTop(4),
        this.getEmptyTop(2),
        this.getEmptyTop(2)
      ]
    },
    getPair: function(upperPosition, lowerPosition) {
      if (upperPosition && lowerPosition) {
        return {
          upper: { position: upperPosition, value: this.list[upperPosition - 1], selected: false },
          lower: { position: lowerPosition, value: this.list[lowerPosition - 1], selected: false }
        };
      }
      else {
        return {
          upper: this.getEmptyHalf(),
          lower: this.getEmptyHalf()
        }
      }
    },
    getEmptyHalf: function() {
      return { position: '', value: '', selected: false };
    },
    getEmptyTop: function(number) {
      const count = number/4;
      const result = [];
      for (let i = 0; i < count; ++i) {
        result.push(this.getPair());
      }

      return result;
    },
    getLeftTop32: function() {
      console.log(this.getPair(1, 32));
      return [
        this.getPair(1, 32),
        this.getPair(16, 17),
        this.getPair(8, 25),
        this.getPair(9, 24),
        this.getPair(4, 29),
        this.getPair(13, 20),
        this.getPair(5, 28),
        this.getPair(12, 21)
      ];
    },
    getRightTop32: function() {
      return [
        this.getPair(2, 31),
        this.getPair(15, 18),
        this.getPair(7, 26),
        this.getPair(10, 23),
        this.getPair(3, 30),
        this.getPair(14, 19),
        this.getPair(6, 27),
        this.getPair(11, 22)
      ];
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

<style scoped>
/* .row {
  display: inline-flex;
  flex-direction: row;
  justify-content: center;
  overflow: scroll;
  padding-left: '20px !important';
} */
</style>
