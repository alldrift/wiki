<template>
  <div class="column">
    <h2>{{header}}</h2>
    <div class="pair" v-for="(pair, index) of left" :key="index">
      <button
        v-bind:class="{selected: pair.upper.selected}"
        v-on:click="handleClick('left', index, 'upper')"
      >
        <span><b>{{pair.upper.position}}</b></span>{{pair.upper.value}}
      </button>
      <button
        v-bind:class="{selected: pair.lower.selected}"
        v-on:click="handleClick('left', index, 'lower')"
      >
        <span><b>{{pair.lower.position}}</b></span>{{pair.lower.value}}
      </button>
    </div>
    <!-- <br :v-if="index===0"/>
    <br :v-if="index===0"/> -->
    <div class="pair" v-for="(pair, index) of right" :key="pair.position">
      <button
        v-bind:class="{selected: pair.upper.selected, unselected: pair.lower.selected && !pair.upper.selected}"
        v-on:click="handleClick('right', index, 'upper')">
        <span><b>{{pair.upper.position}}</b></span>{{pair.upper.value}}
      </button>
      <button
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

  div {
    margin: auto 20px;
  }

  &:first-of-type > div {
    margin-top: 4px;
    margin-bottom: 4px;
  }

  .pair > button:first-of-type::after {
    content:"";
    width: 18px;
    position: absolute;
    border-right: $border-style;
    margin-left: 2px;
    left: 100%;
    height: 26px;
  }
  .pair:nth-child(even) > button:first-of-type::after {
    border-top: $border-style;
    top: 100%;
  }
  .pair:nth-child(odd) > button:first-of-type::after {
    border-bottom: $border-style;
    bottom: 0%;
  }
  &:nth-of-type(2) > div {
    &.pair > button:first-of-type::after {
      height: 52px;
    }
  }
  &:nth-of-type(3) > div {
    &.pair > button:first-of-type::after {
      height: 108px;
    }
  }
  &:nth-of-type(4) > div {
    &.pair > button:first-of-type::after {
      height: 210px;
    }
  }
}

.column:not(:first-of-type) > div > button:first-of-type:before {
  content:"";
  position: absolute;
  border-top:$border-style;
  top: 100%;
  border-left: $border-style;
  left: 0;
  width: 16px;
  margin-left: -21px;
}

.column > .pair > button {
   padding: 0 3px 0 0;
   min-width: 150px;
}
.column > .pair > button {
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
  display:table-cell; vertical-align:middle;
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
