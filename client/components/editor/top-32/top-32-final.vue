<template>
  <div class="column">
    <h2>Final</h2>
    <div class="final">
      <div class="pair">
        <h3>Final</h3>
        <button
          v-bind:class="{selected: gold.upper.selected}"
          v-on:click="handleClick('gold', 'upper')"
        >
          <span><b>{{gold.upper.position}}</b></span>{{gold.upper.value}}
        </button>
        <button
          v-bind:class="{selected: gold.lower.selected}"
          v-on:click="handleClick('gold', 'lower')"
        >
          <span><b>{{gold.lower.position}}</b></span>{{gold.lower.value}}
        </button>
      </div>

      <div class="pair bronze">
        <h3>Bronze</h3>
        <button
          v-bind:class="{selected: bronze.upper.selected}"
          v-on:click="handleClick('bronze', 'upper')"
        >
          <span><b>{{bronze.upper.position}}</b></span>{{bronze.upper.value}}
        </button>
        <button
          v-bind:class="{selected: bronze.lower.selected}"
          v-on:click="handleClick('bronze', 'lower')"
        >
          <span><b>{{bronze.lower.position}}</b></span>{{bronze.lower.value}}
        </button>
      </div>
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

<style lang='scss' scoped>
$border-style: 1px solid #9e9e9e;
.column {
  display: flex;
  flex-direction: column;
  h2 {
    background-color: whitesmoke;
    border-right: 1px solid grey;
    padding: 5px 0;
  }
  h3 {
    margin: 5px 0;
  }
  .final {
    margin: auto 20px;
  }
  &:first-of-type > div {
    margin-top: 4px;
    margin-bottom: 4px;
  }
  .bronze {
    position: absolute;
  }
}

.column:not(:first-of-type) > .final > .pair:first-of-type > button:first-of-type:before {
  content:"";
  position: absolute;
  border-top:$border-style;
  top: 100%;
  border-left: $border-style;
  left: 0;
  width: 16px;
  margin-left: -21px;
}

button {
   padding: 0 3px 0 0;
   min-width: 150px;
}
button {
/* Permalink - use to edit and share this gradient: https://colorzilla.com/gradient-editor/#ffffff+0,e5e5e5+100;White+3D */
  background: rgb(255,255,255); /* Old browsers */
  background: -moz-radial-gradient(center, ellipse cover,  rgba(255,255,255,1) 0%, rgba(229,229,229,1) 100%); /* FF3.6-15 */
  background: -webkit-radial-gradient(center, ellipse cover,  rgba(255,255,255,1) 0%,rgba(229,229,229,1) 100%); /* Chrome10-25,Safari5.1-6 */
  background: radial-gradient(ellipse at center,  rgba(255,255,255,1) 0%,rgba(229,229,229,1) 100%); /* W3C, IE10+, FF16+, Chrome26+, Opera12+, Safari7+ */
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#ffffff', endColorstr='#e5e5e5',GradientType=1 ); /* IE6-9 fallback on horizontal gradient */
  text-align: left;
  border: 1px solid #9e9e9e;
  transform: translateY(1px);
  height: 22px;
  font-family: "Source Sans Pro",Arial,Helvetica,sans-serif;
  font-size: 13px;
  padding-right: 10px;
}

.pair {
  display: flex;
  flex-direction: column;

  > button:first-of-type {
    border-top-left-radius: 3px;
    border-top-right-radius: 3px;
    border-bottom: 1px solid whitesmoke;
  }

  > button:last-of-type {
    border-top: 1px solid whitesmoke;
    border-bottom-left-radius: 3px;
    border-bottom-right-radius: 3px;
  }
}
.pair > button:active {
  border-color: green;
}
.pair > button.selected {
  border-width: 1px;
  border-color: green;
  background:rgba(56, 255, 0, 0.1);
  & span {
    background:rgba(63, 153, 51, 0.432);
  }
}
.pair > button > span {
  position: static;
  text-align: center;
  display: inline-block;
  width: 20px;
  border-right: 1px solid #9e9e9e;
  margin-right: 2px;
  background-color: gainsboro;
}
</style>
