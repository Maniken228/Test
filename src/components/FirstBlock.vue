<template>
    <div class="first__box">
        <Navigation/>
        <div class="">
        </div>
    </div>
</template>

<script lang="ts">
import Navigation from "@/components/Navigation.vue";
import {defineComponent} from "vue";

export default defineComponent({
    name: "FirstBlock",
    components: {Navigation}
});
</script>

<style scoped lang="scss">

.first__box {
    width: 685px;
    height: 524px;
    border-radius: 10px 0px 0px 10px;
    padding-left: 2.8rem;
}

</style>