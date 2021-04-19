<template>
  <div class="v-top32-column">
    <h2 class="v-top32-header">{{header}}</h2>
    <div class="v-top32-pair" v-for="(pair, index) of left" :key="index">
      <button class="v-top32-button"
        v-bind:class="{selected: pair.upper.selected}"
        v-on:click="handleClick('left', index, 'upper')"
      >
        <span><b>{{pair.upper.position}}</b></span>{{pair.upper.value}}
      </button>
      <button class="v-top32-button"
        v-bind:class="{selected: pair.lower.selected}"
        v-on:click="handleClick('left', index, 'lower')"
      >
        <span><b>{{pair.lower.position}}</b></span>{{pair.lower.value}}
      </button>
    </div>
    <!-- <br :v-if="index===0"/>
    <br :v-if="index===0"/> -->
    <div class="v-top32-pair" v-for="(pair, index) of right" :key="pair.position">
      <button class="v-top32-button"
        v-bind:class="{selected: pair.upper.selected, unselected: pair.lower.selected && !pair.upper.selected}"
        v-on:click="handleClick('right', index, 'upper')">
        <span><b>{{pair.upper.position}}</b></span>{{pair.upper.value}}
      </button>
      <button class="v-top32-button"
        v-on:click="handleClick('right', index, 'lower')"
        v-bind:class="{selected: pair.lower.selected, unselected: pair.upper.selected && !pair.lower.selected}"
      >
        <span><b>{{pair.lower.position}}</b></span>{{pair.lower.value}}
      </button>
    </div>
  </div>
</template>
<script>
export default {
  name: 'top-32-column',
  props: {
    header: String,
    index: Number,
    left: Array,
    right: Array,
    onChange: Function
  },
  methods: {
    handleClick: function(side, index, pairPosition) {
      this.onChange && this.onChange(side, this.index, index, pairPosition);
    }
  }
}
</script>
