<template>
    <div>

    <div class="banner" @click="handleBannerClick">
        <img class="banner-img" :src="bannerImg" alt="">
        <div class="banner-info">
            <div class="banner-tittle">{{ this.sightName }}</div>
            <div class="banner-number banner-icon">
                <span class="iconfont">&#xe666;</span>
                {{ this.bannerImgs.length }}
            </div>
        </div>
    </div>
    <fade>
        <common-gallary :imgs="bannerImgs" v-show="showGallary" @close="handleGallaryClose"></common-gallary>
    </fade>
    </div>
</template>

<script>
import CommonGallary from 'common/gallary/Gallary'
import Fade from 'common/fade/Fade'

    export default {
        name: 'DetailBanner',
        props: {
            sightName: String,
            bannerImg: String,
            bannerImgs: Array
        },
        data() {
            return {
                showGallary: false
            }
        },
        methods: {
            handleBannerClick () {
                this.showGallary = true
            },
            handleGallaryClose () {
                this.showGallary = false
            }
        },
        components: {
            CommonGallary,
            Fade
        }
    }
</script>

<style lang="stylus" scoped>
 // 作者的这个css写法学习
    .banner
        position: relative
        
        overflow: hidden
        height: 0
        padding-bottom: 55%
        .banner-img
            width: 100%
        .banner-info
            display: flex
            position: absolute
            left: 0
            right: 0
            bottom: 0
            line-height: .6rem
            color: #fff
            background-image: linear-gradient(top, rgba(0, 0, 0, 0) ,rgba(0, 0, 0, 0.8))
            .banner-tittle
                flex:1
                font-size: .32rem
                padding: 0 .2rem
            .banner-number
                height: .32rem
                line-height: .32rem
                margin-top: .14rem
                padding: 0 .4rem
                border-radius: .2rem
                background: rgba(0, 0, 0, .8)
                font-size: .24rem
                .banner-icon
                    font-size: .2rem

</style>