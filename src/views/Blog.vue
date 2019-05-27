<template>
  <div class="blog">
    <img alt="Vue logo" src="../assets/logo.png">
    <div class="blog-posts" v-if="posts">
      <SinglePost />
    </div>
    <div v-else>
      <div class="lds-ripple"><div></div><div></div></div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import SinglePost from '@/components/SinglePost.vue';

export default {
  name: 'blog',
  components: {
    SinglePost,
  },
  data() {
    return {
      posts: null,
    };
  },
  mounted() {
    axios({
      url: 'https://api-euwest.graphcms.com/v1/cjvws6kqd8jcf01et5n9onhir/master',
      method: 'post',
      headers: {
        'Content-type': 'application/json',
      },
      data: JSON.stringify({
        query: `{
                  blogPosts {
                    id
                    postDate
                    title
                    postContent {
                      text
                    } 
                    heroBackground {
                      id
                    }
                  }
            }`,
      }),
    })
      .then((response) => {
        this.posts = response;
      })
      .catch(error => console.log(error));
  },
};
</script>
<style>
.lds-ripple {
  display: inline-block;
  position: relative;
  width: 64px;
  height: 64px;
}
.lds-ripple div {
  position: absolute;
  border: 4px solid #000;
  opacity: 1;
  border-radius: 50%;
  animation: lds-ripple 1s cubic-bezier(0, 0.2, 0.8, 1) infinite;
}
.lds-ripple div:nth-child(2) {
  animation-delay: -0.5s;
}
@keyframes lds-ripple {
  0% {
    top: 28px;
    left: 28px;
    width: 0;
    height: 0;
    opacity: 1;
  }
  100% {
    top: -1px;
    left: -1px;
    width: 58px;
    height: 58px;
    opacity: 0;
  }
}
</style>
