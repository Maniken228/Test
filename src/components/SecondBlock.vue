<template>
  <div class="second__box">
      <Result/>
      <SBBottom/>
  </div>
</template>

<script>
import Result from "@/components/Result.vue";
import SBBottom from "@/components/SB-Bottom.vue";

export default {
    name: "SecondBlock",
    components: {SBBottom, Result}
}
</script>

<style scoped lang="scss">

.second__box {
    width: 595px;
    height: 524px;
    background: #56C6AD;
    border-radius: 0px 10px 10px 0px;
}

</style>