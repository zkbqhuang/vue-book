<template>
  <div class="my-main">
    <div class="header-box">
      <div class="user">
        <div class="user-avatar" :style="`background-image: url(${user.avatar});`"></div>
        <div class="user-name">{{user.nickname}}</div>
        <div class="user-signature">{{user.slogan}}</div>
      </div>
    </div>
    <div class="btn">
      <div class="list">
        <div class="list-item edit" @click="goEdiit">
          <span class="icon icon-edit"></span>
          {{$t('my.editUser')}}
          <span class="icon-you"></span>
        </div>
        <div class="list-item history" @click="showHistory">
          <span class="icon icon-history"></span>
          {{$t('my.ReaderHistory')}}
          <span class="icon-you"></span>
        </div>
        <div class="list-item about" @click="goAbout">
          <span class="icon icon-about"></span>
          {{$t('my.about')}}
          <span class="icon-you"></span>
        </div>
        <div class="list-item logout" @click="doLogout">
          <span class="icon icon-logout"></span>
          {{$t('my.logout')}}
          <span class="icon-you"></span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import {
  getUserInfo,
  saveUserInfo,
  clearLocalStorage
} from "@/utils/localStorage";
import { getUserInfoApi } from "@/api/user";
export default {
  name: "My",
  components: {},
  props: {},
  data() {
    return {
      user: {
        sex: "男",
        nickname: "AuroraReader",
        slogan: "Welcome to AuroraReader",
        avatar: require("../../assets/images/user/avatar.png")
      }
    };
  },
  watch: {},
  computed: {},
  methods: {
    showHistory() {
      this.$router.push({
        name: "ReaderHistory"
      });
    },

    doLogout() {
      clearLocalStorage();
      this.$router.push({
        name: "login"
      });
    },

    goEdiit() {
      this.$router.push({
        name: "UserEdit"
      });
    },
    goAbout() {
      this.$router.push({
        name: "About"
      });
    }
  },
  created() {
    this.user = getUserInfo();
    saveUserInfo(this.user);
  },
  mounted() {}
};
</script>
<style lang="scss" scoped>
.my-main {
  width: 100%;
  height: 100%;
  overflow: hidden;
  background-color: rgb(246, 246, 246);
  .header-box {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 200px;
    background: linear-gradient(35deg, #64b6e6, #9198e5);
    .user {
      display: flex;
      flex-direction: column;
      align-content: center;
      align-items: center;
      justify-content: center;
      .user-avatar {
        width: 70px;
        height: 70px;
        border-radius: 50%;
        background-repeat: no-repeat;
        background-size: cover;
        background-position: center;
        border: 3px solid #fff;
      }
      .user-name {
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 20px;
        color: white;
        margin-top: 20px;
      }
      .user-signature {
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 12px;
        color: rgb(228, 228, 228);
        margin-top: 10px;
      }
    }
  }
  .btn {
    box-sizing: border-box;
    padding: 20px;
    width: 100%;
    .list {
      width: 100%;
      border-radius: 15px;
      overflow: hidden;
      .list-item {
        width: 100%;
        padding: 15px 0;
        margin: 3px 0;
        background-color: #fff;
        font-size: 18px;
        color: rgb(146, 145, 145);
        .icon {
          padding: 0 10px;
          color: rgb(101, 183, 230);
        }
        .icon-you {
          float: right;
          padding-right: 10px;
        }
      }
    }
  }
}
</style>