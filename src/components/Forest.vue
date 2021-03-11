<template>
  <div class="forest">
    <canvas
      id="myCanvas"
      width="4000"
      height="3000"
      :style="[{ marginLeft: marginLeft + 'px', marginTop: marginTop + 'px' }]"
    >
    </canvas>
  </div>
</template>

<script>
export default {
  name: "Forest",
  props: {
    marginLeft: {
      type: Number,
      required: true
    },
    marginTop: {
      type: Number,
      required: true
    }
  },
  setup() {
    return {};
  }
};
</script>

<style scoped>
#myCanvas {
  background-color: rgba(172, 118, 47, 0.5);
}
</style>
