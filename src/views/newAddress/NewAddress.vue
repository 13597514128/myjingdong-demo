<template>
    <div class="wrapper">
        <div class="header">
            <div 
                class="header__back iconfont"
                @click="handleBackClcik"
            >
                &#xe67d;
            </div>
            <div class="header__title">新建收货地址</div>
            <div class="header__preserve">
                保存
            </div>
        </div>
        <div class="content">
            <div class="content__list">
                <div class="content__list__item">
                    <span class="content__list__item__title">所在城市:</span>
                    <input 
                        class="content__list__item__info" 
                        placeholder="如广东省广州市"
                    />
                </div>
                <div class="content__list__item">
                    <span class="content__list__item__title">小区/大厦/学校:</span>
                    <input 
                        class="content__list__item__info" 
                        placeholder="大塘东华南坚贞花园"
                    />
                </div>
                <div class="content__list__item">
                    <span class="content__list__item__title">楼号-门牌号:</span>
                    <input 
                        class="content__list__item__info" 
                        placeholder="三巷五号"
                    />
                </div>
                <div class="content__list__item">
                    <span class="content__list__item__title">收货人:</span>
                    <input 
                        class="content__list__item__info" 
                        placeholder="请填写收货人的姓名"
                    />
                </div>
                <div class="content__list__item content__list__item--active">
                    <span class="content__list__item__title">联系电话:</span>
                    <input 
                        class="content__list__item__info" 
                        placeholder="请填写收货手机号"
                    />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { useRouter } from 'vue-router'
const useBackRouterEffect = () => {
    const router = useRouter();
    const handleBackClcik = () => {
        router.back();
    }
    return { handleBackClcik }
}

export default {
    name: 'NewAddress',
    setup() {
        const { handleBackClcik } = useBackRouterEffect();
        return { handleBackClcik }
    },
}
</script>

<style lang="scss" scoped>
@import '../../style/viriables.scss';
.wrapper {
  position: absolute;
  left: 0;
  top: 0;
  bottom: 0;
  right: 0;
  background: rgb(248, 248, 248);
  z-index: 1;
}
.header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: .18rem;
    background: $bgColor;
    &__back {
        color: #B6B6B6;
        font-size: .20rem;
    }
    &__title {
        font-size: .16rem;
        color: $content-fontcolor;
    }
    &__preserve {
        font-size: .14rem;
        color: $content-fontcolor;
    }
}
.title {
    font-size: .14rem;
    color: $content-fontcolor;
    margin: .16rem 0 .12rem .18rem;
}
.content {
    position: relative;
    width: 100%;
    height: 2.24rem;
    margin-top: .12rem;
    box-sizing: border-box;
    background: $bgColor;
    &__list {
        padding: 0 .18rem;
        &__item {
            height: .44rem;
            border-bottom: .01rem solid $content-bgColor;
            display: flex;
            align-items: center;
            &--active {
                border-bottom: none;
            }
            &__title {
                font-size: .14rem;
                color: $medium-fontColor;
                margin-right: .1rem;
            }
            &__info {
                font-size: .14rem;
                color: $content-fontcolor;
                border: none;
                outline: none;
            }
        }
    }
}
</style>