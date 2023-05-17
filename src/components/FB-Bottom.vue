<template>
    <div class="first__box-bottom">
        <div class="info">
            Lorem ipsum
            <div class="info__circle">
                <img class="bb" src="../assets/i.webp" alt="info" draggable="false">
            </div>
        </div>
        <input type="radio">
        <div class="info">
            Lorem ipsum dolor sit
            <div class="info__circle info__circle-second">
                <img class="bb" src="../assets/i.webp" alt="info" draggable="false">
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import {defineComponent} from "vue";


export default defineComponent({
    name: "FB-Bottom"
});
</script>

<style scoped lang="scss">

.first__box-bottom {
    width: 415px;
    height: 32px;
    margin-top: 3rem;
    display: flex;
    justify-content: space-between;
    align-items: center;

    .info {
        display: flex;
        align-items: center;

        .info__circle {
            width: 14px;
            height: 14px;
            background: #CFCFCF;
            border-radius: 50%;
            transition: .3s all ease;

            img {
                width: 100%;
                height: 100%;
            }
        }

        .info__circle-second:hover {
            background: #56C6AD;
        }
    }
}

</style>