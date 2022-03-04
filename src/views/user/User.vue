<template>
    <div class="topBg">
        <div class="userInfo iconfont">&#xe635;</div>
        <div class="user">
                <img class="user__img" src="../../assets/松冈凛.jpg" alt="">
                <div class="user__name">francis</div>
                <div class="user__id">ID: 15971159403</div>
                <div class="user__product">
                    <span class="user__product__item">
                        <div class="user__product__name">红包</div>
                        <div class="user__product__count">218</div>
                    </span>
                    <span class="user__product__item">
                        <div class="user__product__name">优惠劵</div>
                        <div class="user__product__count">12张</div>
                    </span>
                    <span class="user__product__item">
                        <div class="user__product__name">鲜豆</div>
                        <div class="user__product__count">88</div>
                    </span>
                    <span class="user__product__item">
                        <div class="user__product__name">白条</div>
                        <div class="user__product__count">1000</div>
                    </span>
                </div>
        </div>
        <div class="more">
            <div class="more__item">
                <span class="more__packet iconfont">&#xe634;</span>
                <span class="more__title">我的钱包</span>
                <div class="more__enter iconfont">&#xe67d;</div>
            </div>
            <div class="more__item">
                <span class="more__address iconfont">&#xe619;</span>
                <span class="more__title">我的地址</span>
                <div 
                    class="more__enter iconfont"
                    @click="handleEnterAddress"
                >
                    &#xe67d;
                </div>
            </div>
            <div class="more__item">
                <span class="more__service iconfont">&#xe62d;</span>
                <span class="more__title">客服与帮助</span>
                <div class="more__enter iconfont">
                    &#xe67d;
                </div>
            </div>
        </div>
    </div>
    <Docker :currentIndex="3"/>
</template>

<script>
import Docker from '../../components/Docker'
import { useRouter } from 'vue-router'
const useEnterAddressEffect = () => {
    const router = useRouter();
    const handleEnterAddress = () => {
        router.push({ name: 'Address'})
    }
    return { handleEnterAddress }
}
export default {
    name: 'User',
    components: { Docker },
    setup() {
        const { handleEnterAddress } = useEnterAddressEffect();
        return { handleEnterAddress }
    },
}
</script>

<style lang="scss" scoped>
@import '../../style/viriables.scss';
.topBg {
    position: relative;
    width: 100%;
    height: 2.5rem;
    background-image: linear-gradient(239deg, #3A6FF3 0%, #50C7FB 100%);
    border-bottom-left-radius: 90% 40%;
    border-bottom-right-radius: 90% 40%;
} 
.userInfo {
    font-size: .25rem;
    color: $bgColor;
    position: absolute;
    top: .57rem;
    left: 3.3rem;
}
.user {
    position: absolute;
    top: 1.08rem;
    left: 0.18rem;
    width: 3.39rem;
    height: 2.03rem;
    background: $bgColor;
    box-shadow: 0 .08rem .16rem 0 rgba(0,0,0,0.08);
    border-radius: .08rem;
    &__img {
        position: absolute;
        left: 50%;
        margin-left: -.47rem;
        margin-top: -.47rem;
        width: .94rem;
        height: .94rem;
        border-radius: 50%;
    }
    &__name {
        margin-top: .59rem;
        text-align: center;
        font-size: .24rem;
        color: #262628;
        letter-spacing: .0019rem;
        text-align: center;
        line-height: .36rem;
    }
    &__id {
        margin-top: .02rem;
        padding-bottom: .12rem;
        font-size: .14rem;
        color: $idColor;
        text-align: center;
        border-bottom: .01rem solid $content-bgColor;
    }
    &__product {
        padding: .12rem .28rem .16rem .28rem;
        display: flex;
        justify-content: space-around;
        &__name {
            font-size: .14rem;
            color: $idColor;
            text-align: center;
            margin-bottom: .07rem;
            line-height: .17rem;
        }
        &__count {
            font-size: .2rem;
            color: #262628;
            text-align: center;
        }
    }
}
.more {
    position: absolute;
    top: 3.27rem;
    left: 0.18rem;
    width: 3.39rem;
    height: 1.46rem;
    background: $bgColor;
    box-shadow: 0 .08rem .16rem 0 rgba(0,0,0,0.08);
    border-radius: .08rem;
    padding: .18rem .16rem .16rem .16rem;
    box-sizing: border-box;
    &__item {
        margin-bottom: .24rem;
    }
    &__packet, &__address, &__service {
        width: .22rem;
        height: .22rem;
        border-radius: .08rem;
        margin-right: .12rem;
        padding: .02rem;
        color: $bgColor;
    }
    &__packet {
        background: #ED4A47;
    }
    &__address {
        background: #32C5FF;
    }
    &__service {
        background: #9013FE 92%;
    }
    &__title {
        font-size: .14rem;
        color: #262626;
    }
    &__enter {
        float: right;
        transform: rotate(180deg);
        position: relative;
        margin-top: .02rem;
        color: #C2C4CA;
    }
}
</style>