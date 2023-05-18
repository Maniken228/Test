<template>
    <div class="calculator__wrap">
        <div class="calculator__row">
            <div class="amount_wrap">
                <label class="calculator__text">Amount?</label>
                <div class="massage" :class="{ on: displayMessage }">
                    {{ message }}
                </div>
            </div>
            <div class="calculator__input-wrap">
                <input
                    class="calculator__input"
                    type="number"
                    v-model.number="investmentAmount"
                    @input="handleAmountChange"
                />
                <div class="button__wrap">
                    <button class="calculator__button" @click="decrementAmount">
                        <img
                            class="button__photo"
                            alt="button"
                            src="../assets/-.webp"
                            draggable="false"
                        />
                    </button>
                    <button class="calculator__button" @click="incrementAmount">
                        <img
                            class="button__photo"
                            alt="button"
                            src="../assets/+.webp"
                            draggable="false"
                        />
                    </button>
                </div>
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
                        :label="getCurrencyLabel(option)"
                        :value="option.value"
                    ></el-option>
                </template>
            </el-select>
        </div>

        <div class="calculator__row">
            <label class="calculator__text">Period?</label>
            <el-select
                class="calculator__input"
                v-model="investmentPeriod"
                @change="calculate"
                style="padding: 0px"
            >
                <el-option
                    v-for="option in periodOptions"
                    :key="option.value"
                    :label="option.label"
                    :value="option.value"
                ></el-option>
            </el-select>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

interface CurrencyOption {
    value: string;
    label: string;
    interestRate: number;
}

export default defineComponent({
    name: "Calculator",
    props: {
        investmentResult: {
            type: Number,
            required: true,
        },
    },
    data() {
        return {
            investmentAmount: 0,
            selectedCurrency: "TUSD",
            investmentPeriod: "1",
            currencyOptions: [
                {
                    value: "TUSD",
                    label: "TUSD (Test US Dollar)",
                    interestRate: 0.12,
                },
                {
                    value: "TEUR",
                    label: "TEUR (Test Euro)",
                    interestRate: 0.13,
                },
                {
                    value: "TCNY",
                    label: "TCNY (Test Chinese Yuan)",
                    interestRate: 0.2,
                },
                {
                    value: "TINR",
                    label: "TINR (Test Indian Rupee)",
                    interestRate: 0.33,
                },
                {
                    value: "TBRL",
                    label: "TBRL (Test Brazilian Real)",
                    interestRate: 0.21,
                },
                {
                    value: "TIDR",
                    label: "TIDR (Test Indonesian Rupiah)",
                    interestRate: 0.8,
                },
            ] as CurrencyOption[],
            isSelectOpen: false,
            filterText: "",
            periodOptions: [
                { label: "1 month", value: "1" },
                { label: "3 months", value: "3" },
                { label: "6 months", value: "6" },
                { label: "12 months", value: "12" },
                { label: "24 months", value: "24" },
            ],
            displayMessage: false,
            message: "",
            calculatedResult: 0,
        };
    },

    watch: {
        investmentAmount: {
            handler: "calculate",
            immediate: true,
        },
        selectedCurrency: {
            handler: "calculate",
            immediate: true,
        },
        investmentPeriod: {
            handler: "calculate",
            immediate: true,
        },
    },

    computed: {
        filteredCurrencies(): CurrencyOption[] {
            const filterText = this.filterText.toLowerCase();
            return this.currencyOptions.filter((option) =>
                option.label.toLowerCase().includes(filterText)
            );
        },
    },

    methods: {
        handleAmountChange() {
            if (this.investmentAmount < 1000 || this.investmentAmount > 1000000) {
                this.displayMessage = true;
                this.message = "Lorem ipsum dolor sit";
                setTimeout(() => {
                    this.displayMessage = false;
                    this.message = "";
                }, 5000);
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
            const { investmentAmount, selectedCurrency, investmentPeriod } = this;
            const selectedCurrencyOption = this.currencyOptions.find(
                (option) => option.value === selectedCurrency
            );

            if (selectedCurrencyOption) {
                const interestRate = selectedCurrencyOption.interestRate;
                const months = parseInt(investmentPeriod);
                const calculatedResult = investmentAmount * interestRate * (months / 12);
                this.calculatedResult = parseFloat(calculatedResult.toFixed(2));
                this.$emit("result-updated", this.calculatedResult);
            }
        },

        handleSelectVisibility(visible: boolean) {
            this.isSelectOpen = visible;
        },

        filterCurrencies(value: string, option: CurrencyOption) {
            if (option && option.label) {
                return (
                    option.label.toLowerCase().indexOf(value.toLowerCase()) !== -1
                );
            }
            return false;
        },

        getCurrencySymbol(currency: string): string {
            switch (currency) {
                case "TUSD":
                    return "$";
                case "TEUR":
                    return "€";
                case "TCNY":
                    return "¥";
                case "TINR":
                    return "₹";
                case "TBRL":
                    return "R$";
                case "TIDR":
                    return "Rp";
                default:
                    return "";
            }
        },

        getCurrencyLabel(option: CurrencyOption): string {
            const symbol = this.getCurrencySymbol(option.value);
            return `${option.label} (${symbol})`;
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

        .calculator__input-wrap {
            width: 547px;
            position: relative;

            .button__wrap {
                display: flex;
                gap: 7px;
                position: absolute;
                top: 50%;
                right: 10px;
                transform: translate(-50%, -50%);

                .calculator__button {
                    width: 19px;
                    height: 19px;
                    cursor: pointer;
                    transition: all .3s ease;

                    .button__photo {
                        width: 100%;
                        height: 100%;
                    }
                }

                .calculator__button:active {
                    transform: scale(0.8);
                }
            }
        }

        .amount_wrap {
            width: 547px;
            display: flex;
            justify-content: space-between;

            .massage {
                color: #ff0000;
                opacity: 0;
                transition: 0.3s all ease;
            }

            .on {
                transition: 0.3s all ease;
                opacity: 1;
            }
        }
    }
}

.calculator__text {
    font-size: 16px;
    line-height: 18px;
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

.input__text {
    width: 490px;
    padding-top: 1.8rem;
    padding-left: 1rem;
    font-weight: 600;
    font-size: 14px;
    line-height: 20px;
    color: #636e72;
}

</style>