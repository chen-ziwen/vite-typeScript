<template>
    <div class="skin-total flex">
        <div class="border flex main" :style="mainStyle">
            <slot></slot>
        </div>

        <div class="border flex extra" :style="extraStyle">
            <slot name="extra"></slot>
        </div>
    </div>
</template>

<script lang="ts" setup>
import { computed, useSlots } from "vue";

const slots = useSlots();
const props = defineProps<SmartBarProps>();

interface SmartBarProps {
    skinFolder: string;
    theme: string;
    mainColor?: string;
    extraColor?: string;
}

const mainStyle = computed(() => {
    const style = {
        borderImageSource: `url(/assets/images/${props.skinFolder}/${props.theme}.png)`,
        color: props.mainColor || "black"
    }
    return style;
});
const extraStyle = computed(() => {
    const style = {
        display: slots.extra ? "flex" : "none",
        borderImageSource: `url(/assets/images/${props.skinFolder}/${props.theme}_2.png)`,
        color: props.extraColor || "black"
    }
    return style;
})

</script>

<style  lang="scss" scoped>
.border {
    border-image-slice: 0 40 0 40 fill;
    border-image-width: 0px 40px 0px 40px;
    border-image-outset: 0px 40px 0px 40px;
    border-image-repeat: stretch stretch;
    // margin: 0 65px;
}
.flex {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    font-size: 24px;
}
.skin-total {
    .main {
        z-index: 1;
        height: 70px;
    }
    .extra {
        z-index: 0;
        height: 70px;
        margin-left: 44px;
    }
}
</style>