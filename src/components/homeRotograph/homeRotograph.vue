<template>

    <div class="carousel">
        <el-carousel ref="carouselRef" arrow="never" height="520px" :autoplay="false" @change="change">
            <el-carousel-item v-for="item in rotograph" :key="item.cover">
                <div class="carousel-item">
                    <div class="carousel-img-box">
                        <el-image class="carousel-img" :src="item.cover" fit="cover" />
                    </div>
                </div>
            </el-carousel-item>

            <!-- 轮播图底部 -->
            <div class="carousel-bottom">
                <div class="carousel-title">{{ carouselTitle? carouselTitle: props.rotograph[0]?.title }}</div>
                <div class="toggle-button">
                    <div class="button-item" v-throttle="{ fun: carouselSwitch, params: [false], time: 500 }">
                        <SvgIcon name="rightArrow" class="arrow-icon rotation" color="#fff">
                        </SvgIcon>
                    </div>
                    <div class="button-item" v-throttle="{ fun: carouselSwitch, params: [true], time: 500 }">
                        <SvgIcon name="leftArrow" class="arrow-icon" color="#fff"></SvgIcon>
                    </div>
                </div>
            </div>
        </el-carousel>
    </div>
</template>

<script lang="ts" setup>
import { rotographList } from "@/types/home/live";
import { vThrottle } from "@/utils/customInstruction/throttle"
import { ElCarousel, ElCarouselItem, ElImage } from 'element-plus';
import { ref } from 'vue';

const props = defineProps({
    rotograph: {
        type: Array as () => rotographList,
        required: true,
        default: () => []
    }
})

const carouselRef = ref()
const carouselTitle = ref("")
//切换轮播图 true 下一张 false 上一张
const carouselSwitch = (is: boolean) => {
    if (is) {
        carouselRef.value.next()

    } else {
        carouselRef.value.prev()
    }
}


//轮播图变化事件
const change = (index: number) => {
    carouselTitle.value = props.rotograph[index].title
}
</script>

<style lang="scss" scoped>
@import "./static/css/homeRotograph.scss";
</style>