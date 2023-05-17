<template>
  <div class="">
      <div class="">
          <h3 class="">
              Profit
          </h3>
          <p class="">
              {{ investmentResult }}
          </p>
      </div>
      <div class="">
          <h3 class="">
              Percent
          </h3>
          <div class="">
              59%
          </div>
          <p class="">
              Lorem ipsum dolor sit amet consectetur adipisicing elit
          </p>
      </div>
  </div>
</template>

<script>
import { defineComponent, PropType } from "vue";

export default defineComponent({
    name: "Result",
    props: {
        investmentResult: {
            type: Number,
            default: 0,
        },
    },
});
</script>

<style scoped>

</style>