<template>
  <div class="home-hot">
    <HomePanel title="人气推荐" subTitle="人气爆款 不容错过">
      <div style="position: relative; height: 426px;" ref="target">
        <!-- 面板内容 -->
        <transition name="fade">
          <ul class="goods-list" ref="pannel" v-if="list.length">
            <li v-for="item in list" :key="item.id">
                <RouterLink :to="`/product/${item.id}`">
                    <img :src="item.picture" alt="">
                    <p class="name">{{item.title}}</p>
                    <p class="desc">{{item.alt}}</p>
                </RouterLink>
            </li>
          </ul>
          <HomeSkeleton v-else></HomeSkeleton>
        </transition>
      </div>
    </HomePanel>
  </div>
</template>


<script>
import HomePanel from './home-panel.vue';
import { findHot } from '@/api/home';
import HomeSkeleton from './home-skeleton.vue'
import { useLazyData } from '@/hooks';
export default {
  name:'HomeNew',
  components: { HomePanel,HomeSkeleton },
  setup() {
    // const list = ref([])
    // const target = ref(null)
    // findHot().then(data => {
    //     list.value = data.result
    // })
    const {target,result} = useLazyData(findHot)
    return { list:result,target }
  }
}
</script>


<style scoped lang="less">
  @import '../../../assets/style/mixin.less';
  @import '../../../assets/style/variables.less';
  .goods-list {
    display: flex;
    justify-content: space-between;
    height: 426px;
    li {
      width: 306px;
      height: 406px;
      .hoverShadow();
      img {
        width: 306px;
        height: 306px;
      }
      p {
        font-size: 22px;
        padding-top: 12px;
        text-align: center;
      }
      .desc {
        color: #999;
        font-size: 18px;
      }
    }
  }
</style>