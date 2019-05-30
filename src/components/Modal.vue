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
          <p v-if="item.postDate">{{ item.postDate }}</p>
          <p v-else>{{ item.createdAt }}</p>
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
export default {
  name: 'Modal',
  props: {
    msg: String,
    title: String,
    thumbnail: String,
    item: Object,
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

    .container {
      background-color: #ebe8e8;
      min-height: 100vh;
      padding-bottom: 80px;
    }

    .close-modal {
      position: fixed;
      right: 50px;
      top: 35px;
      cursor: pointer;
      opacity: .8;
      transition: all .3s;

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
