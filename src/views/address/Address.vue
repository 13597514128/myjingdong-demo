<template>
    <div class="wrapper">
        <div class="header">
            <div 
                class="header__back iconfont"
                @click="handleBackClcik"
            >
                &#xe67d;
            </div>
            <div class="header__title">管理收货地址</div>
            <div 
                class="header__build"
                @click="handleNewBuild"
            >
                新建
            </div>
        </div>
        <div class="title">我的收货地址</div>
        <div class="content">
            <span class="content__name">阿凛</span>
            <span class="content__phone">15342356631</span>
            <div class="content__address">广东省广州市海珠区大塘东华南 四巷五号 五层 兔兔兔兔子宝宝</div>
            <div 
                class="content__enter iconfont"
                @click="handleEnterClick"
            >
                &#xe67d;
            </div>
        </div>
        <div class="content">
            <span class="content__name">阿凛</span>
            <span class="content__phone">15342356631</span>
            <div class="content__address">广东省广州市海珠区大塘东华南 四巷五号 五层 兔兔兔兔子宝宝</div>
            <div 
                class="content__enter iconfont"
                @click="handleEnterClick"
            >
                &#xe67d;
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

const useNewBuildEffect = () => {
    const router = useRouter();
    const handleNewBuild = () => {
        router.push({ name :'NewAddress' })
    }
    return { handleNewBuild }
}

const useEnterChangeEffect = () => {
    const router = useRouter();
    const handleEnterClick = () => {
        router.push({ name :'ChangeAddress' })
    }
    return { handleEnterClick }
}

export default {
    name: 'Address',
    setup() {
        const { handleBackClcik } = useBackRouterEffect();
        const { handleNewBuild } = useNewBuildEffect();
        const { handleEnterClick } = useEnterChangeEffect();
        return { handleBackClcik, handleNewBuild, handleEnterClick }
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
    &__build {
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
    width: 3.39rem;
    height: 1.04rem;
    padding: .18rem .16rem;
    margin: 0 0 .16rem .18rem;
    box-sizing: border-box;
    background: $bgColor;
    &__name {
        font-size: .14rem;
        color: $light-fontColor;
        margin-right: .66rem;
    }
    &__phone {
        font-size: .14rem;
        color: $light-fontColor;        
    }
    &__address {
        margin-top: .08rem;
        font-size: .14rem;
        width: 2.6rem;
        line-height: .22rem;
        color: $content-fontcolor;
    }
    &__enter {
        position: absolute;
        top: .44rem;
        margin-top: -.07rem;
        right: .16rem;
        color: $light-fontColor;
        transform: rotate(180deg);
        font-size: .2rem;

    }
}
</style>