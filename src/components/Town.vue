<template>
  <div class="town">
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
  name: "Town",
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

<style scoped></style>
