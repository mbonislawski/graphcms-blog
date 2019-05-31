<template>
  <div class="modal" v-if="item">
    <div class="close-modal" @click="$emit('closeModal')">
      <img src="../assets/close.svg">
    </div>
    <div class="container">
      <div class="post-thumb" :style="'background-image: url('+item.heroBackground.url+')'"></div>
      <div class="text-holder">
        <div class="title-row">
          <h1>{{ item.title }}</h1>
          <p v-if="item.postDate">{{ item.postDate | moment }}</p>
          <p v-else>{{ item.createdAt | moment }}</p>
        </div>
        <div class="thumbnail"></div>
        <div class="description">
          <p v-html="item.postContent.html"></p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import moment from 'moment';

export default {
  name: 'Modal',
  props: {
    msg: String,
    title: String,
    thumbnail: String,
    item: Object,
  },
  filters: {
    moment(date) {
      return moment(date).format('MMM Do YYYY, h:mm a');
    },
  },
};
</script>

<style lang="scss">
  .modal {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    margin: auto;
    width:100%;
    background-color: #0d0c0c;
    z-index: 2;
    min-height: 100vh;
    padding-top: 50px;
    padding-bottom: 50px;
    @media(max-width: 1024px) {
      padding-top: 0;
      padding-bottom: 0;
    }

    .container {
      background-color: #ebe8e8;
      min-height: 100vh;
      padding: 0;
      padding-bottom: 80px;
      @media(max-width: 1600px) {
        width: calc(100% - 150px);
        margin: auto;
      }
      @media(max-width: 1024px) {
        width: 100%;
      }
    }

    .close-modal {
      position: fixed;
      right: 50px;
      top: 35px;
      cursor: pointer;
      opacity: .8;
      transition: all .3s;
      @media(max-width: 1600px) {
        right: 15px;
        top: 35px;
      }
      @media(max-width: 1024px) {
        top: 20px;
        background-color: #0d0c0c;
        height: 48px;
      }

      &:hover {
        opacity: 1;
      }
    }

    .title-row {
      display: flex;
      align-items: center;
      justify-content: space-between;

      p {
        font-size: 14px;
      }
    }

    h1 {
      text-align: left;
      margin-bottom: 10px;
    }

    p {
      text-align: left;
      line-height: 1.64;
    }

    .text-holder {
      width: 1000px;
      margin: auto;
      padding-top: 30px;
      @media(max-width: 1600px) {
        padding: 30px;
        max-width: 100%;
      }

      .description {
        img {
          height: unset!important;
          width: 100%;
        }
      }
    }

    .post-thumb {
      width: 100%;
      height: 500px;
      background-image: url('../assets/hero-image.jpg');
      background-position: center;
      background-size: cover;
      background-repeat: no-repeat;
    }
  }
</style>
