<template>
    <div class="calculator__wrap">
        <div class="calculator__row">
            <label class="calculator__text">Amount?</label>
            <div class="calculator__input-wrapper">
                <button class="calculator__button" @click="decrementAmount">-</button>
                <input class="calculator__input" type="number" v-model.number="investmentAmount" @input="handleAmountChange" />
                <button class="calculator__button" @click="incrementAmount">+</button>
            </div>
        </div>

        <div class="calculator__row">
            <label class="calculator__text">Currency?</label>
            <el-select
                    class="calculator__input"
                    v-model="selectedCurrency"
                    @change="calculate"
                    @visible-change="handleSelectVisibility"
                    filterable
                    v-bind:filter-method="filterCurrencies"
                    placeholder="Select currency"
                    style="padding: 0px"
            >
                <template #default>
                    <el-input
                            v-model="filterText"
                            prefix-icon="el-icon-search"
                            style="height: 40px !important;"
                            placeholder="Lorum"
                    ></el-input>
                    <p class="input__text">Additional content after the dropdown</p>
                    <hr/>
                    <el-option
                            v-for="option in filteredCurrencies"
                            :key="option.value"
                            :label="option.label"
                            :value="option.value"
                    ></el-option>
                </template>
            </el-select>
        </div>

        <div class="calculator__row">
            <label class="calculator__text">Period?</label>
            <el-select class="calculator__input" v-model="investmentPeriod" @change="calculate" style="padding: 0px">
                <el-option v-for="option in periodOptions" :key="option.value" :label="option.label"
                           :value="option.value"></el-option>
            </el-select>
        </div>
    </div>
</template>

<script lang="ts">
import {defineComponent} from "vue";

interface CurrencyOption {
    value: string;
    label: string;
    interestRate: number;
}

export default defineComponent({
    name: "Calculator",
    data() {
        return {
            investmentAmount: 0,
            selectedCurrency: "TUSD",
            investmentPeriod: "1",
            currencyOptions: [
                { value: "TUSD", label: "TUSD (Test US Dollar)", interestRate: 0.12 },
                { value: "TEUR", label: "TEUR (Test Euro)", interestRate: 0.13 },
                { value: "TCNY", label: "TCNY (Test Chinese Yuan)", interestRate: 0.2 },
                { value: "TINR", label: "TINR (Test Indian Rupee)", interestRate: 0.33 },
                { value: "TBRL", label: "TBRL (Test Brazilian Real)", interestRate: 0.21 },
                { value: "TIDR", label: "TIDR (Test Indonesian Rupiah)", interestRate: 0.8 },
            ] as CurrencyOption[],
            investmentResult: 0,
            isSelectOpen: false,
            filterText: "",
            periodOptions: [
                { label: "1 month", value: "1" },
                { label: "3 months", value: "3" },
                { label: "6 months", value: "6" },
                { label: "12 months", value: "12" },
                { label: "24 months", value: "24" },
            ],
        };
    },

    computed: {
        filteredCurrencies(): CurrencyOption[] {
            const filterText = this.filterText.toLowerCase();
            return this.currencyOptions.filter((option) => option.label.toLowerCase().includes(filterText));
        },
    },

    methods: {
        handleAmountChange() {
            if (this.investmentAmount < 1000 || this.investmentAmount > 1000000) {
                alert("Invalid amount. Please enter a value between 1000 and 1000000.");
            }
        },

        incrementAmount() {
            if (this.investmentAmount < 1000000) {
                this.investmentAmount += 1000;
                this.handleAmountChange();
            }
        },

        decrementAmount() {
            if (this.investmentAmount > 1000) {
                this.investmentAmount -= 1000;
                this.handleAmountChange();
            }
        },
        calculate() {
            const {investmentAmount, selectedCurrency, investmentPeriod} = this;
            const selectedCurrencyOption = this.currencyOptions.find((option) => option.value === selectedCurrency);

            if (selectedCurrencyOption) {
                const interestRate = selectedCurrencyOption.interestRate;
                const months = parseInt(investmentPeriod);
                const result = investmentAmount * Math.pow(1 + interestRate, months / 12);
                this.investmentResult = parseFloat(result.toFixed(2));

                this.$emit("result-updated", this.investmentResult);
            }
        },

        handleSelectVisibility(visible: boolean) {
            this.isSelectOpen = visible;
        },

        filterCurrencies(value: string, option: CurrencyOption) {
            if (option && option.label) {
                return option.label.toLowerCase().indexOf(value.toLowerCase()) !== -1;
            }
            return false;
        },
    },
});
</script>

<style scoped lang="scss">
.calculator__wrap {
    display: flex;
    opacity: 1;
    flex-direction: column;
    gap: 28px;
    padding-top: 3rem;

    .calculator__row {
        display: flex;
        flex-direction: column;
        gap: 12px;

        .calculator__text {
            font-size: 16px;
            line-height: 18px;
        }

        .calculator__input {
            width: 547px;
            height: 50px;
            background: #F4F5F6;
            padding-left: 1.3rem;
            border-radius: 6px;
        }

        .calculator__input:focus {
            border: 1px solid #42b983;
        }
    }
}

.input__text {
    width: 490px;
    padding-top: 1.8rem;
    padding-left: 1rem;
    font-weight: 400;
    font-size: 14px;
    line-height: 18px;
    color: #838C8A;
}


.calculator__input-wrapper {
    display: flex;
    align-items: center;
    gap: 10px;
}

.calculator__button {
    width: 30px;
    height: 30px;
    font-size: 18px;
    display: flex;
    justify-content: center;
    align-items: center;
    border: none;
    background: none;
    cursor: pointer;
}

.calculator__input {
    width: 547px;
    height: 50px;
    background: #f4f5f6;
    padding-left: 1.3rem;
    border-radius: 6px;
}

.calculator__input:focus {
    border: 1px solid #42b983;
}
</style>
