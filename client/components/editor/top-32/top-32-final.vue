<template>
  <div class="v-top32-column">
    <h2 class="v-top32-header">Final</h2>
    <div class="v-top32-pair final">
      <h3>Final</h3>
      <button class="v-top32-button"
        v-bind:class="{selected: gold.upper.selected}"
        v-on:click="handleClick('gold', 'upper')"
      >
        <span><b>{{gold.upper.position}}</b></span>{{gold.upper.value}}
      </button>
      <button class="v-top32-button"
        v-bind:class="{selected: gold.lower.selected}"
        v-on:click="handleClick('gold', 'lower')"
      >
        <span><b>{{gold.lower.position}}</b></span>{{gold.lower.value}}
      </button>
    </div>
    <div class="v-top32-pair bronze">
      <h3>Bronze</h3>
      <button class="v-top32-button"
        v-bind:class="{selected: bronze.upper.selected}"
        v-on:click="handleClick('bronze', 'upper')"
      >
        <span><b>{{bronze.upper.position}}</b></span>{{bronze.upper.value}}
      </button>
      <button class="v-top32-button"
        v-bind:class="{selected: bronze.lower.selected}"
        v-on:click="handleClick('bronze', 'lower')"
      >
        <span><b>{{bronze.lower.position}}</b></span>{{bronze.lower.value}}
      </button>
    </div>
  </div>
</template>
<script>
export default {
  name: 'top-32-final',
  props: {
    gold: Object,
    bronze: Object,
    onChange: Function
  },
  methods: {
    handleClick: function(type, pairPosition) {
      this.onChange && this.onChange(type, pairPosition);
    }
  }
}
</script>
