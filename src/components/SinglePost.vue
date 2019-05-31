<template>
  <div class="single-post">
    <h2>{{ title }}</h2>
    <div class="thumbnail" :style="'background-image: url('+thumbnail+')'"></div>
    <div class="description">
      <p>{{ description.substring(0, 100) + '...' }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SinglePost',
  props: {
    thumbnail: String,
    title: String,
    description: String,
  },
};
</script>

<style lang="scss">
  .single-post {
    width: 25%;
    padding: 4px;
    border-radius: 4px;
    transition: all .3s ease-in-out;
    @media(max-width: 1024px) {
      width: 70%;
      margin-bottom: 40px;
    }
    @media(max-width: 600px) {
      width: 90%;
    }
    &:hover {
      transform: translateY(-10px);
      cursor: pointer;
      -webkit-box-shadow: 0px 9px 7px -7px rgba(179,0,27,1);
      -moz-box-shadow: 0px 9px 7px -7px rgba(179,0,27,1);
      box-shadow: 0px 9px 7px -7px rgba(179,0,27,1);
    }

    .thumbnail {
      width: 100%;
      height: 200px;
      background-image: url('../assets/hero-image.jpg');
      background-position: center;
      background-size: cover;
      background-repeat: no-repeat;
      @media(max-width: 1024px) {
        height: 300px;
      }
    }

    h2 {
      color: #acb4bc;
    }

    p {
      color: #acb4bc;
    }
  }
</style>
