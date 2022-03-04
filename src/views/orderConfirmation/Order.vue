<template>
    <div class="order">
      <div class="order__price">实付金额 <b>¥{{calculations.price}}</b></div>
      <div class="order__btn" @click="() => handleShowConfirmChange(true)">提交订单</div>
    </div>
    <div 
        class="mask" 
        v-show="showConfirm"
        @click="() => handleShowConfirmChange(false)"
    >
        <div class="mask__content" @Click.stop>
            <h3 class="mask__content__title">确认要离开收银台?</h3>
            <p class="mask__content__desc">请尽快完成支付,否则将被取消</p>
            <div class="mask__content__btns">
                <span 
                    class="mask__content__btn mask__content__btn--first"
                    @click="() => handleConfirmOrder(true)"
                >取消订单</span>
                <span 
                    class="mask__content__btn mask__content__btn--last"
                    @click="() => handleConfirmOrder(false)"
                >确认订单</span>
            </div>
        </div>
    </div>
    <Toast v-if="show" :message="toastMessage" />
</template>

<script>
import { ref } from 'vue'
import { useStore } from 'vuex'
import { useRouter, useRoute } from 'vue-router'
import { post } from '../../utils/request'
import Toast, { useToastEffect } from '../../components/Toast'
import { useCommonCartEffect } from '../../effects/cartEffects'
//下单的相关逻辑(确认/取消)
const useOrderEffect = () => {
    const route = useRoute();
    const router = useRouter();
    const store = useStore();
    const shopId = parseInt(route.params.id, 10);
    const { shopName, productList } = useCommonCartEffect(shopId);
    const { showToast } = useToastEffect()
    const handleConfirmOrder = async(isCanceled) => {
        const products = [];
        for(let i in productList.value){
            const product = productList.value[i];
            products.push({
                id: parseInt(product._id, 10),
                num: product.count
            })
        }
        try {
            const result = await post('/api/order', {
                addressId: 1,
                shopId,
                shopName: shopName.value,
                isCanceled,
                products
            })
            if (result?.errno === 0) {
                store.commit('clearCartData', shopId)
                router.push({ name: 'Home' })
            }
        } catch (e) {
            showToast('下单失败')
        }
    }
    
    return { handleConfirmOrder }
}
//展示提交订单蒙层的相关逻辑
const useShowMaskEffect = () => {
    const showConfirm = ref(false);
    const handleShowConfirmChange = (status) => {
        showConfirm.value = status;
    }
    return { showConfirm, handleShowConfirmChange }
}
export default {
    name: 'ProductList',
    components: { Toast },
    setup() {
        const route = useRoute();
        const shopId = parseInt(route.params.id, 10);
        const { show, toastMessage } = useToastEffect()
        const { calculations } = useCommonCartEffect(shopId);
        const { handleConfirmOrder } = useOrderEffect();
        const { showConfirm, handleShowConfirmChange } = useShowMaskEffect();
        return {
            show, showConfirm, toastMessage,
            calculations, handleConfirmOrder, handleShowConfirmChange 
        }
    }
}
</script>

<style lang="scss" scoped>
@import '../../style/viriables.scss';
.order {
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  height: .49rem;
  line-height: .49rem;
  background: $bgColor;
  &__price {
    flex: 1;
    text-indent: .24rem;
    font-size: .14rem;
    color: $content-fontcolor;
  }
  &__btn {
    width: .98rem;
    background: #4FB0F9;
    color: $bgColor;
    text-align: center;
    font-size: .14rem;
  }
}
.mask {
    position:absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 1;
    background: rgba(0, 0, 0, 0.5);
    &__content {
        position: absolute;
        width: 3rem;
        height: 1.56rem;
        background: $bgColor;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        border-radius: .04rem;
        text-align: center;
        &__title {
            font-size: .18rem;
            color: $content-fontcolor;
            line-height: .26rem;
            margin: .24rem 0 0 0;
        }
        &__desc {
            margin: .08rem 0 0 0;
            font-size: .14rem;
            color: $medium-fontColor;
        }
        &__btns {
            display: flex;
            margin: .24rem .58rem 0 .58rem;
        }
        &__btn {
            flex: 1;
            width: .8rem;
            line-height: .32rem;
            border-radius: .16rem;
            border: 1px solid #4FB0F9;
            font-size: .14rem;
            &--first {
                margin-right: .24rem;
                color: #4FB0F9;
            }
            &--last {
                background: #4FB0F9;
                color: $bgColor;
            }
        }
    }
}
</style>