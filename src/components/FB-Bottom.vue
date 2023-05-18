<template>
    <div class="first__box-bottom">
        <div class="info">
            Lorem ipsum
            <div class="info__circle">
                <img class="bb" src="../assets/i.webp" alt="info" draggable="false">
            </div>
        </div>
        <label class="label" for="checkbox">
            <input type="checkbox" id="checkbox"/>
            <span class="slide move">
            </span>
        </label>
        <div class="info">
            Lorem ipsum dolor sit
            <div class="info__circle info__circle-second ">
                <div class="window">
                    Lorem ipsum dolor sit amet consectetur adipisicing
                    elit. Minus cumque animi mollitia ipsam quae
                    fuga voluptatibus aut quia autem nulla corrupti
                    suscipit quam, rem
                </div>
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
        gap: 10px;

        .info__circle {
            width: 14px;
            height: 14px;
            background: #CFCFCF;
            border-radius: 50%;
            transition: .3s all ease;
            position: relative;

            img {
                width: 100%;
                height: 100%;
            }
        }

        .window {
            width: 350px;
            height: 74px;
            position: absolute;
            opacity: 0;
            visibility: hidden;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -120%);
            border-radius: 8px;
            background: rgba(37, 47, 44, 1);
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.2);
            z-index: 10;
            color: #FFFFFF;
            font-weight: 400;
            font-size: 12px;
            line-height: 18px;
            padding: 10px 15px;
            transition: all .4s ease;
        }

        .window:before {
            content: "";
            display: block;
            width: 12.73px;
            height: 12.73px;
            background: rgba(37, 47, 44, 1);
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.2);
            opacity: 1;
            z-index: 9;
            visibility: hidden;
            position: absolute;
            transform: rotate(45deg) translate(-50%, 25%);
            top: 88%;
            left: 50%;
            transition: all .4s ease;
        }

        .info__circle-second:hover {
            background: #56C6AD;

            .window {
                visibility: visible;
                opacity: 0.9;
            }

            .window:before {
                opacity: 0.9;
                visibility: visible;
            }
        }
    }

    .label {
        width: 62px;
        height: 32px;
        display: inline-block;
        position: relative;

        .slide {
            background: #ccc;
            bottom: 0;
            cursor: pointer;
            left: 0;
            position: absolute;
            right: 0;
            top: 0;
            transition: all 0.5s cubic-bezier(0.86, 0.09, 0.43, 1.15);
        }

        .slide:before {
            content: "";
            width: 24px;
            height: 24px;
            background: #fff;
            bottom: 4px;
            left: 6px;
            position: absolute;
            transition: all 0.5s cubic-bezier(0.86, 0.09, 0.43, 1.15);
        }
    }

    .label input {
        display: none;
    }

    .slide.move {
        border-radius: 50px;
    }

    .slide.move:before {
        border-radius: 50%;
    }

    input:checked + .slide {
        background: #E0F3EF;
    }

    input:checked + .slide:before {
        transform: translateX(26px);
        background: #56C6AD;
        box-shadow: 0px 2px 4px rgba(86, 198, 173, 0.4);
    }
}

</style>