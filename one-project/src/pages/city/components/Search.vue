<template>
<div>
    <div class="search">
        <input class="search-input" type="text" placeholder="输入地名" v-model="keyword">
    </div>
    <div class="search-content" ref="search" v-show="keyword">
        <ul>
            <li 
                class="search-item border-bottom" 
                v-for="item in list" :key="item.id" @click="handleCityClick(item.name)">
                {{ item.name }}
            </li>
            <!-- 这里用v-show来实现 提示信息的现实 -->
            <li class="search-item border-bottom" v-show="hasNoData">
                没有找到匹配数据
            </li>
        </ul>
    </div>
</div>
</template>

<script>
import Bscroll from 'better-scroll'
import {mapMutations} from 'vuex'
    export default {
        name: 'CitySearch',
        props: {
            cities: Object
        },
        data() {
            return {
                keyword: '',
                list: [],
                timer: null
            }
        },
        computed: {
            hasNoData() {
                return !this.list.length
            }
        },
        watch: {
            keyword() {
                if (this.timer) {
                    clearTimeout(this.timer)
                }
                // 解决第一次搜索后 city list, 删除掉关键词后 列表不清空的
                if (!this.keyword) {
                    this.list = []
                    return
                }
                this.timer = setTimeout(() => {
                    let result = []
                    //遍历对象查找出符合keyword的 值放入result数组中
                    for (let i in this.cities) {
                        this.cities[i].forEach(value => {
                            if (value.spell.indexOf(this.keyword) > -1 || value.name.indexOf(this.keyword) > -1) {
                                result.push(value)
                            }
                        })
                    }
                    this.list = result
                }, 100)
            }
        },
        methods: {
            handleCityClick (city) {
                //这里只能是触发一个changeCity事件,并没有直接修改内容
                // this.$store.dispatch('changeCity', city)
                // 这里直接commit修改state种的内容也可以
            // this.$store.commit('changeCity', city)
                //vue-router 的编程式导航,说白的就是router-link的js方法
                // 类比a标签和js中的window.location()方法直接通过js修改链接,跳转

                this.changeCity(city)
                this.$router.push('/')
            },
            ...mapMutations(['changeCity'])
        },
        mounted() {
            //添加滚动功能
            this.bscroll = new Bscroll(this.$refs.search)  
        }
    }
</script>

<style lang="stylus" scoped>
    @import '~style/varibles.styl'
    .search
        height: .72rem
        padding: 0 .1rem
        background: $bgColor
        .search-input
            box-sizing: border-box
            width: 100%
            height: .62rem
            padding: 0 .1rem
            line-height: .62rem
            text-align: center 
            border-radius: .06rem
            color: #666
    .search-content
        z-index: 1
        overflow: hidden
        position: absolute
        top: 1.58rem
        left: 0
        right: 0
        bottom: 0
        background: green
        .search-item
            line-height: .62rem
            padding-left: .2rem
            background: #fff
            color: #666
</style>
