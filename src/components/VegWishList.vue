<template>
  <div
    class="veg-whish-list"
    :class="{ show: isShowDetails }">
    <h3>收藏列表</h3>
    <!-- 购物项 -->
    <div class="main">
      <div
        class="none"
        v-if="favoriteItems.length == 0">
        您还没有收藏商品
      </div>
      <div
        class="item"
        v-for="(c, i) in favoriteItems"
        :key="i"
        @click="clickItem(c)">
        <div
          class="close"
          @click="deleteItem(i)">
          x
        </div>
        <div class="left">
          <img
            :src="c.img"
            alt="" />
        </div>
        <div class="right">
          <div class="title">
            <h3>{{ c.title }}</h3>
            <span class="spec">{{ c.spec }}</span>
          </div>
          <div class="price">
            <span class="now">￥{{ (c.price * (1 - c.discount)) | salePrice }}</span>
            <span
              class="pre"
              v-if="c.discount != 0"
              >￥{{ c.price | salePrice }}</span
            >
          </div>
          <button class="buy">查看详情</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapMutations, mapState } from 'vuex';
export default {
  props: ['isShowDetails'],
  data() {
    return {
      // favoriteItems: [
      //   { pid: 1, title: '上海青', spec: '1kg', price: 3, discount: 0.2, img: '/images/products/01.png', count: 1 },
      //   { pid: 2, title: '葡萄', spec: '1kg', price: 4, discount: 0.1, img: '/images/products/02.png', count: 1 },
      //   { pid: 3, title: '猕猴桃', spec: '1kg', price: 5, discount: 0.4, img: '/images/products/03.png', count: 1 },
      // ],
    };
  },
  computed: {
    ...mapState(['favoriteItems']),
  },
  methods: {
    changeShow() {
      this.$parent.switchIsShowDetails();
    },
    deleteItem(i) {
      this.favoriteItems.splice(i, 1);
    },
    changeCount(event, i) {
      this.favoriteItems[i], (count = event);
    },
    clickItem(item) {
      this.$store.commit('updateDetialItem', item);
      this.$router.push(`/product-details?pid=${item.pid}`);
    },
  },

  filters: {
    salePrice(value) {
      value = value.toFixed(2);
      return value;
    },
  },
};
</script>

<style lang="scss" scoped>
.veg-whish-list {
  background-color: #fff;
  padding: 30px 200px 60px;

  > h3 {
    font-size: 24px;
    padding: 30px;
    text-align: center;
  }

  .main {
    display: flex;
    flex-direction: column;
    .none {
      text-align: center;
    }
    .item:first-child {
      border-top: 1px solid #ddd;
    }
    .item {
      display: flex;
      position: relative;
      padding: 20px 0;
      border-bottom: 1px solid #ddd;
      .close {
        position: absolute;
        top: 10px;
        right: 15px;
        color: var(--theme-danger-color);
        cursor: pointer;
        font-size: 20px;
      }
      .left {
        display: flex;
        flex-direction: column;
        align-items: center;
        flex: 2;
        img {
          width: 60%;
        }
        .counter {
          width: 80px;
          height: 24px;
          line-height: 24px;
          margin: 10px 0 0;
        }
      }
      .right {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        flex: 5;
        padding: 0 30px;
        .title {
          height: 60%;
          h3 {
            margin-bottom: 10px;
          }
        }
        .price {
          display: flex;

          .pre {
            color: #aaa;
            text-decoration: line-through;
            margin-right: 20px;
          }
        }
        .buy {
          position: absolute;
          bottom: 30px;
          right: 50px;
          background-color: var(--theme-primary-color);
          padding: 10px 15px;
          color: #fff;
          border-radius: 5px;
          cursor: pointer;
        }
        .buy:active {
          background-color: var(--theme-click-color);
        }
      }
    }
  }
}
</style>
