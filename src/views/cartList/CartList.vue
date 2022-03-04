<template>
<div class="wrappers">
  <div class="title">全部购物车</div>
  <div 
    class="products"
    v-for="(item, index) in list"
    :key="index"
  >
    <div class="products__title">
      {{item.shopName}}
    </div>
    <div class="products__wrapper">
      <div class="products__list">
        <template 
          v-for="(productItem, productIndex) in item.productList"
          :key="productIndex"
        >
          <div 
            class="products__item"
            v-if="productIndex < 2"
          >
            <img class="products__item__img" :src="productItem.imgUrl" />
            <div class="products__item__detail">
              <h4 class="products__item__title">{{productItem.title}}</h4>
              <p class="products__item__price">
                <span>
                  <span class="products__item__yen">&yen; </span>
                  {{productItem.price}} × {{productItem.count}}
                </span>
                <span class="products__item__total">
                  <span class="products__item__yen">&yen; </span>
                  {{(productItem.price * productItem.count).toFixed(2)}}
                </span>
              </p>
            </div>
          </div>
        </template>
        <div 
          class="products__list__btn" 
          v-if="item.productList.length >= 3"
        >
          共计{{item.productList.length}}件/1.4kg
          <span class="products__list__more iconfont">
            &#xe67d;
          </span>
        </div>
      </div>
    </div>
  </div>
</div>
  <Docker :currentIndex="1"/>
</template>

<script>
import Docker from '../../components/Docker'
const list = {
  "1": {
    shopName: '沃尔玛',
    productList: [
      {
        imgUrl: "http://www.dell-lee.com/imgs/vue3/banner.jpg",
        title: '番茄250g/份',
        price: 33.6,
        count: 3
      },
      {
        imgUrl: "http://www.dell-lee.com/imgs/vue3/banner.jpg",
        title: '提子250g/份',
        price:22,
        count: 5
      },
      {
        imgUrl: "http://www.dell-lee.com/imgs/vue3/banner.jpg",
        title: '猪肉250g/份',
        price:49.9,
        count: 2
      }
    ]
  },
  "2": {
    shopName: '京东7FRESH七鲜',
    productList: [
      {
        imgUrl: "http://www.dell-lee.com/imgs/vue3/banner.jpg",
        title: '番茄250g/份',
        price: 33.6,
        count: 3
      },
      {
        imgUrl: "http://www.dell-lee.com/imgs/vue3/banner.jpg",
        title: '提子250g/份',
        price:22,
        count: 5
      },
    ]
  },
  "3": {
    shopName: '山姆会员商店',
    productList: [
      {
        imgUrl: "http://www.dell-lee.com/imgs/vue3/banner.jpg",
        title: '番茄250g/份',
        price: 33.6,
        count: 3
      },
      {
        imgUrl: "http://www.dell-lee.com/imgs/vue3/banner.jpg",
        title: '猪肉250g/份',
        price:49.9,
        count: 2
      },
    ]
  }
}
export default {
  name: 'CartList',
  components: { Docker },
  setup(){
    return { list }
  }
}
</script>

<style lang="scss" scoped>
@import '../../style/viriables.scss';
@import '../../style/mixins.scss';
.wrappers {
  overflow-y: auto;
  position: absolute;
  left: 0;
  top: 0;
  bottom: .5rem;
  right: 0;
  background: rgb(248, 248, 248);
}
.title {
  font-size: .16rem;
  color: $content-fontcolor;
  text-align: center;
  line-height: .44rem;
  background: $bgColor;
}
.products {
  margin: .16rem .18rem .1rem .18rem;
  padding-bottom: .16rem;
  background: $bgColor;
  border-radius: .04rem;
  &__title {
    padding: .16rem .16rem 0 .16rem;
    font-size: .16rem;
    color: $content-fontcolor;
    font-weight: bold;
  }
  &__list {
    background: $bgColor;
    &__btn {
      height: .28rem;
      width: 3.07rem;
      background: $search-bgColor;
      position: relative;
      left: 50%;
      margin: .16rem 0 0 -1.535rem;
      display: flex;
      align-items: center;
      justify-content: center;
      font-family: PingFangSC-Light;
      font-size: .14rem;
      color: $light-fontColor;
    }
    &__more {
      position: relative;
      margin-left: .06rem;
      transform: rotate(270deg);
      background: PingFangSC-Light;
      font-size: .18rem;
    }
  }
  &__item {
    position: relative;
    display: flex;
    padding: .16rem .16rem 0 .16rem;
    &__img {
      width: .46rem;
      height: .46rem;
      margin-right: .16rem;
    }
    &__detail {
      flex: 1;
    }
    &__title {
      margin: 0;
      line-height: .2rem;
      font-size: .14rem;
      color: $content-fontcolor;
      font-family: PingFangSC-Medium;
      @include ellipsis;
    }
    &__price {
      display: flex;
      margin: .06rem 0 0 0;
      line-height: .2rem;
      font-size: .14rem;
      color: $hightlight-fontColor;
    }
    &__total {
      flex: 1;
      text-align: right;
      color: #000;
    }
    &__yen {
      font-size: .12rem;
    }
  }
}

</style>