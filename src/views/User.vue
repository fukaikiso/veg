<template>
  <div>
    <veg-sidebar-cart></veg-sidebar-cart>
    <div class="user">
      <div class="banner">
        <img
          src="/images/page-header.jpg"
          alt="" />
        <div class="desc">
          <img
            :src="$store.state.userInfo.avatar"
            alt="用户头像"
            class="avatar" />
          <h3>{{ $store.state.userInfo.nickname }}</h3>
          <p>{{ $store.state.userInfo.description }}</p>
        </div>
      </div>

      <div class="tabbar">
        <div class="container">
          <div
            class="item"
            v-for="(t, i) in tabbar"
            :key="i">
            <router-link
              :to="t.href"
              :class="['button', { selected: $route.meta.tabIndex == i }]">
              {{ t.title }}
            </router-link>
          </div>
        </div>
      </div>

      <div class="content">
        <div class="container">
          <router-view />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import VegSidebarCart from '@/components/VegSidebarCart.vue';
export default {
  components: { VegSidebarCart },
  data() {
    return {
      tabbar: [
        { title: '个人主页', href: '/user/profile' },
        { title: '收藏列表', href: '/user/wish-list' },
        // { title: '订单详情', href: '/user/orders' },
        // { title: '物流信息', href: '/user/track' },
      ],
    };
  },
  methods: {},
};
</script>

<style lang="scss" scoped>
.user {
  background-color: var(--theme-bg-color);
  .banner {
    position: relative;
    img {
      display: block;
    }
    .desc {
      position: absolute;
      top: 20%;
      left: 20%;
      .avatar {
        width: 80px;
        border-radius: 40px;
        overflow: hidden;
      }
      h3 {
        margin: 15px 0 10px;
        font-size: 20px;
      }
      p {
        font-size: 14px;
        color: #666;
      }
    }
  }

  .tabbar {
    padding: 30px 0;
    .container {
      display: flex;
      align-items: center;
      height: 60px;
      background-color: #fff;
      border-radius: 5px;
      > .item {
        flex: 1;
        text-align: center;
        display: flex;
        justify-content: center;
        > .button {
          background-color: #fff;
          cursor: pointer;
          font-weight: bold;
        }
        > .button:hover,
        > .button.selected {
          padding: 10px 12px;
          border-radius: 5px;
          color: #fff;
          background-color: var(--theme-primary-color);
        }
      }
    }
  }

  .content {
    padding: 0 0 40px;
    .container {
      background-color: #fff;
      box-shadow: 0 0 10px #ccc;
    }
  }
}
</style>
