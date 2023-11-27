<template>
    <h1>{{ $route.params.id }}</h1>    
  <!-- Mobile専用_Header_HambergerMenu -->
  <div>    
    <!-- Logo_Imgae -->
    <header class="mobile_header_wrapper">
      <div class="mobile_header_logo_wrapper">Robotama Project🔥</div>
      <div class="mobile_header_btn_block_wrapper">
        <!-- User Icon : MyPageに移動する -->
        <button class="user_icon" @click="goToMyPage">
          <img
            src="~/assets/image/mobile/header/user_icon.svg"
            alt="User Icon"
          />
        </button>
        <!-- ハンバーガーメニュー・Open_Btn -->
        <button class="hamburger" @click="clickMenu">
          <!-- ハンバーガーメニューのボタン -->
          <div class="hamburger_btn">
            <span class="line line_01" :class="{ btn_line01: activeMenu }">
            </span>
            <span class="line line_02" :class="{ btn_line02: activeMenu }">
            </span>
            <span class="line line_03" :class="{ btn_line03: activeMenu }">
            </span>
          </div>
        </button>
        <!-- サイドバー -->
        <transition name="menu">
          <div class="menu" v-show="activeMenu">
            <ul>
              <li>
                <!-- ✖️ Icon : 閉じる_Btn -->
                <div>
                  <button class="close_btn" @click="clickMenu">
                    <img
                      src="~/assets/image/mobile/header/icon_cross_wh.svg"
                      alt="Menu"
                    />
                  </button>
                </div>
              </li>
              <li @click="clickMenu">
                <nuxt-link to="/">
                  <div class="nav_tab_container">
                    <span class="title">HOME</span>
                    <span class="sub_title">ホーム</span>
                  </div>
                </nuxt-link>
              </li>
              <li @click="clickMenu">
                <nuxt-link to="/robotama">
                  <div class="nav_tab_container">
                    <span class="title">ROBOTAMA</span>
                    <span class="sub_title">ロボ玉</span>
                  </div>
                </nuxt-link>
              </li>
              <li @click="clickMenu">
                <nuxt-link to="/maritama">
                  <div class="nav_tab_container">
                    <span class="title">MARITAMA</span>
                    <span class="sub_title">まり玉</span>
                  </div>
                </nuxt-link>
              </li>
              <li @click="clickMenu">
                <nuxt-link to="/hakutou">
                  <div class="nav_tab_container">
                    <span class="title">HAKUTOU</span>
                    <span class="sub_title">白桃さん</span>
                  </div>
                </nuxt-link>
              </li>
              <li @click="clickMenu">
                <nuxt-link to="/momo">
                  <div class="nav_tab_container">
                    <span class="title">MOMO</span>
                    <span class="sub_title">ももちゃん</span>
                  </div>
                </nuxt-link>
              </li>
            </ul>
          </div>
        </transition>
      </div>
    </header>
    <!-- Fixed によって、隠れる問題の対応 -->
    <div class="header_fixed_height_div"></div>
  </div>
</template>
<script>
export default {
  name: "MobileHeader",
  components: {},
  data() {
    return {
      activeMenu: false,
    };
  },
  methods: {
    goToMyPage() {
      this.$router.push("/my-page");
    },
    clickMenu() {
      // 真偽値を反転する => Open / Close
      this.activeMenu = !this.activeMenu;
    },
  },
};
</script>
<style lang="scss" scoped>
/* -------------- COMMON -------------- */

/* Btn_Default_Style を無効化する */
@mixin disable_default_button_style {
  background-color: transparent;
  border: none;
  cursor: pointer;
  outline: none;
  padding: 0;
  appearance: none;
}

/* -------------- SECTIONS -------------- */

/* Header_全体を包み込む_Wrapper */
.mobile_header_wrapper {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  align-content: center;
  height: 64px;
  padding-top: 16px;
  vertical-align: middle;
  width: 100%;
  background-color: white;
  // 上部に固定する
  // z-index: $z-index-high;
  z-index: 998;
  position: fixed;
  top: 0;
  left: 0;
}

.mobile_header_logo_wrapper {
  cursor: pointer;
}

/* User_Icon & Menu Block_Wrapper */
.mobile_header_btn_block_wrapper {
  position: absolute;
  right: 20px;
  margin-bottom: 12px;

  /* User Icon */
  .user_icon {
    // Btn_Default_Style を無効化する
    @include disable_default_button_style;
    margin-right: 12px;
    margin-left: -15px;
  }

  /* Hamberger Icon */
  .hamberger {
    @include disable_default_button_style;
  }
}

/* ハンバーガーボタン */
.hamburger_btn {
  width: 18px;
  height: 37px;
  cursor: pointer;

  .line {
    position: absolute;
    top: 0;
    left: 20px;
    width: 25px;
    height: 2px;
    background: #333333;
    text-align: center;
  }

  .line_01 {
    top: 16px;
    transition: 0.4s ease;
  }
  .line_02 {
    top: 26px;
    transition: 0.4s ease;
  }
  .line_03 {
    top: 36px;
    transition: 0.4s ease;
  }

  /* ハンバーガー・Menu の 3つの Line */
  .btn_line01 {
    transform: translateY(10px) rotate(-45deg);
    transition: 0.4s ease;
    color: #fff;
  }
  .btn_line02 {
    transition: 0.4s ease;
    opacity: 0;
    color: #fff;
  }
  .btn_line03 {
    transform: translateY(-10px) rotate(45deg);
    transition: 0.4s ease;
    color: #fff;
  }
}

/* メニュー画面 */
.menu {
  /* background-color: rgba(197, 197, 197, 0.671); */
  background: #000000;
  /* 画面全体を覆います */
  // z-index: $z-index-highest;
  z-index: 999;
  width: 100%;
  height: 100%;
  padding: 2rem 1rem;
  position: fixed;
  top: 0;
  right: 0;

  /* 閉じるBtn */
  .close_btn {
    @include disable_default_button_style; // Btn_Default_Style を無効化する

    position: absolute;
    right: 20px;
  }

  li {
    list-style: none;
    line-height: 1;
  }
  ul {
    margin: 1rem;
    padding: 0;
  }
  // a {
  //   color: #fff;
  //   text-decoration: none;
  //   font-size: 1.2rem;
  //   padding: 0 2rem;
  // }

  /* Nav_Tab: 1つの項目の Container */
  .nav_tab_container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 5px;
    color: #fff;

    .title {
      font-size: 22px;
      font-weight: lighter;
      color: #fff;
    }

    .sub_title {
      font-size: 12px;
      color: #fff;
      margin-bottom: 20px;
    }
  }
}

/* Fixed によって、隠れる問題の対応 */
.header_fixed_height_div {
  height: 80px;
}
</style>