<template>
  <div class="second__box-bottom">
      <div class="review__wrap">
          <div class="review__grade">
              <figure class="grade">
                  <img class="star" alt="star" src="../assets/star.webp" draggable="false">
              </figure>
              <figure class="grade">
                  <img class="star" alt="star" src="../assets/star.webp" draggable="false">
              </figure>
              <figure class="grade">
                  <img class="star" alt="star" src="../assets/star.webp" draggable="false">
              </figure>
              <figure class="grade">
                  <img class="star" alt="star" src="../assets/star.webp" draggable="false">
              </figure>
              <figure class="grade">
                  <img class="star" alt="star" src="../assets/star.webp" draggable="false">
              </figure>
          </div>
          <button class="review__button">
              Lorem ipsum dolor sit
          </button>
      </div>
      <p class="bottom__text">
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Minus cumque animi mollitia ipsam quae
          fuga voluptatibus aut quia autem nulla corrupti suscipit quam, rem veniam, reiciendis,
          temporibus magni quis velit! Lorem ipsum dolor sit amet consectetur adipisicing elit.
          Minus cumque animi mollitia ipsam quae fuga voluptatibus aut quia autem nulla corrupti
          suscipit quam, rem veniam, reiciendis, temporibus magni quis velit! Lorem ipsum dolor
          sit amet consectetur adipisicing
      </p>
  </div>
</template>

<script lang="ts">
import {defineComponent} from "vue";

export default defineComponent({
    name: "SB-Bottom"
});
</script>

<style scoped lang="scss">

.second__box-bottom {
    display: flex;
    flex-direction: column;
    gap: 20px;
    padding-top: 1.5rem;

    .review__wrap {
        height: 48px;
        display: flex;
        align-items: center;
        gap: 40px;

        .review__grade {
            height: 23px;
            display: flex;
            align-items: center;
            gap: 7px;

            .grade {


                .star {
                    width: 100%;
                    height: 100%;
                }
            }

            .grade:first-child {
                width: 17px;
                height: 16px;
            }

            .grade:nth-child(2) {
                width: 20px;
                height: 19px;
            }

            .grade:nth-child(3) {
                width: 22px;
                height: 21px;
            }

            .grade:nth-child(4) {
                width: 23px;
                height: 22px;
            }

            .grade:last-child {
                width: 24px;
                height: 23px;
            }
        }

        .review__button {
            width: 321px;
            height: 48px;
            background: #56C6AD;
            border: 2px solid #FFFFFF;
            border-radius: 7px;
            font-weight: 700;
            font-size: 18px;
            line-height: 21px;
            text-align: center;
            text-transform: uppercase;
            color: #FFFFFF;
            transition: all .4s ease;
            cursor: pointer;
        }

        .review__button:active {
            transform: scale(0.9);
        }

        .review__button:hover {
            border: 2px solid #B28B84;
            color: #B28B84;
        }
    }

    .bottom__text {
        width: 495px;
        height: 108px;
        font-weight: 300;
        font-size: 12px;
        line-height: 18px;
        text-align: justify;
        color: #FFFFFF;
    }
}

</style>