<template>
    <div class="wrapper">
        <swiper :options="swiperOption" v-if="showSwiper">
            <!-- slides 这里有bug-->
            <swiper-slide v-for="item in list" :key="item.id" >
                <img class="swiper-img" :src="item.imgUrl" alt="">
            </swiper-slide>

            <!-- 这里写的时候有一个bug, src链接方式不知道怎么弄 -->
            <!-- 这里的路径不知道怎么了,chrome 看的路径和这里明显不一样 -->
            <!-- <swiper-slide><img class="swiper-img" src="~style/swiper-1.jpg" alt=""></swiper-slide>
            <swiper-slide><img class="swiper-img" src="~style/swiper-2.jpg" alt=""></swiper-slide>
            <swiper-slide><img class="swiper-img" src="~style/swiper-3.jpg" alt=""></swiper-slide>
            <swiper-slide><img class="swiper-img" src="~style/swiper-4.jpg" alt=""></swiper-slide> -->
            <!-- Optional controls -->
            <div class="swiper-pagination"  slot="pagination"></div>
        </swiper>
    </div>
</template>

<script>
export default {
    name: 'HomeSwiper',
    props: {
        list: Array //设定接受的类型 ,这里循环路径不知道怎么搞本地,不该了 从父组件接受数据怎么用,就简单了
    },
    computed: { //解决list数组的初始化问题,最开始是空值,所以可能会导致bug的解决
        showSwiper() {
            return this.list.length
        }
    },
    data () {
        return {
            swiperOption: {
                pagination: '.swiper-pagination',
                loop: true
            }
            // swiperList: [{
            //     id: '001',
            //     imgUrl: 'style/swiper-1.jpg'
            // },{
            //     id: '002',
            //     imgUrl: 'style/swiper-2.jpg'
            // },{
            //     id: '003',
            //     imgUrl: 'style/swiper-3.jpg'
            // }]
        }
    }

}
</script>

<style lang="stylus" scoped>
    .wrapper >>> .swiper-pagination-bullet-active
        background: #fff
    .swiper-img
        width: 100%
</style>