<template>
<nav class="navigation__wrap">
    <ul class="navigation">
        <li class="list">
            <a href="#" class="link">
                Lorem1
            </a>
        </li>
        <li class="list">
            <a href="#" class="link">
                Lorem2
            </a>
        </li>
        <li class="list">
            <a href="#" class="link">
                Lorem3
            </a>
        </li>
        <li class="list">
            <a href="#" class="link">
                Lorem4
            </a>
        </li>
    </ul>
</nav>
</template>

<script lang="ts">

import { defineComponent } from 'vue';

export default defineComponent({
    name: "Navigation"
});

</script>

<style scoped lang="scss">

.navigation__wrap {
    padding-top: 2.5rem;

    .navigation {
        display: flex;
        gap: 31px;
        list-style-type: none;

        .list {

            .link {
                width: 48px;
                color: #252F2C;
                font-size: 14px;
                line-height: 129%;
                transition: .4s ease all;
            }

            .link:hover {
                border-bottom: 2px solid #56C6AD;
                box-shadow: 0px 1px 2px rgba(86, 198, 173, 0.25);
            }
        }
    }
}

</style>