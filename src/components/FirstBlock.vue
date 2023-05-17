<template>
    <div class="first__box">
        <Navigation/>
        <Calculator @result-updated="updateResult"/>
        <FBBottom/>
    </div>
    <div class="second__box">
        <Result :investmentResult="investmentResult"/>
        <SBBottom/>
    </div>
</template>

<script lang="ts">
import {defineComponent} from "vue";
import Navigation from "@/components/Navigation.vue";
import Calculator from "@/components/Calculator.vue";
import FBBottom from "@/components/FB-Bottom.vue";
import Result from "@/components/Result.vue";
import SBBottom from "@/components/SB-Bottom.vue";

export default defineComponent({
    name: "FirstBlock",
    components: {
        SBBottom, Result,
        FBBottom,
        Calculator,
        Navigation,
    },
    data() {
        return {
            investmentResult: 0,
        };
    },
    methods: {
        updateResult(result: number) {
            this.investmentResult = result;
        },
    },
});
</script>

<style scoped lang="scss">

.first__box {
    width: 685px;
    height: 524px;
    border-radius: 10px 0px 0px 10px;
    padding-left: 2.8rem;
}

.second__box {
    width: 595px;
    height: 524px;
    background: #56C6AD;
    border-radius: 0px 10px 10px 0px;
}

</style>