<template>
    <div class="result__wrap">
        <div class="result__box">
            <h3>
                Profit
            </h3>
            <p class="result">
                {{ displayResult }}
            </p>
        </div>
        <div class="result__box">
            <h3>
                Percent
            </h3>
            <div class="result">
                59%
            </div>
            <p class="result__text">
                Lorem ipsum dolor sit amet consectetur adipisicing elit
            </p>
        </div>
    </div>
</template>

<script lang="ts">
import {defineComponent, PropType} from "vue";

export default defineComponent({
    name: "Result",
    props: {
        result: {
            type: Number,
            default: 0,
        },
    },
    computed: {
        displayResult(): string {
            if (this.result < 1000 || this.result > 1000000) {
                return "0.00";
            } else {
                return this.formatResult(this.result);
            }
        },
    },
    methods: {
        formatResult(value: number): string {
            const parts = value.toFixed(2).split(".");
            parts[0] = parts[0].replace(/\B(?=(\d{3})+(?!\d))/g, ",");
            return parts.join(".");
        },
    },
});
</script>

<style scoped lang="scss">

.result__wrap {
    padding-top: 4rem;
    display: flex;
    flex-direction: column;
    gap: 36px;

    .result__box {
        display: flex;
        flex-direction: column;
        gap: 6px;

        h3 {
            font-weight: 400;
            font-size: 16px;
            line-height: 18px;
            color: #FFFFFF;
        }

        .result {
            font-weight: 700;
            font-size: 55px;
            line-height: 64px;
            color: #FFFFFF;
        }

        .result__text {
            font-weight: 400;
            font-size: 12px;
            line-height: 18px;
            color: #FFFFFF;
        }
    }
}

</style>