<template>
  <div class="blog">
    <div class="container">
      <div class="blog-posts" v-if="posts">
        <SinglePost
          v-for="singlePost in posts"
          :key="singlePost.id"
          :title="singlePost.title"
          :description="singlePost.postContent.text"
          :thumbnail="singlePost.heroBackground.url"
          @click.native="modalPost = singlePost, modalActive = true"
        />
      </div>
      <div v-else>
        <div class="lds-ripple"><div></div><div></div></div>
      </div>
    </div>
    <transition name="slide">
      <Modal
        :item="modalPost"
        v-show="modalActive"
        @closeModal="modalActive = false"
      />
    </transition>
  </div>
</template>

<script>
import axios from 'axios';
import SinglePost from '@/components/SinglePost.vue';
import Modal from '@/components/Modal.vue';

export default {
  name: 'blog',
  components: {
    SinglePost,
    Modal,
  },
  data() {
    return {
      posts: null,
      modalPost: null,
      modalActive: false,
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
                    createdAt
                    postContent {
                      text
                      html
                    } 
                    heroBackground {
                      id
                      url
                    }
                  }
            }`,
      }),
    })
      .then((response) => {
        this.posts = response.data.data.blogPosts;
      })
      .catch(error => console.log(error));
  },
};
</script>
<style lang="scss">
.blog {
  .container {
    max-width: 100%;
  }
}
.blog-posts {
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding-top: 200px;
  @media(max-width: 1024px) {
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding-top: 100px;
  }
}
.lds-ripple {
  display: inline-block;
  position: absolute;
  bottom: 0;
  top: 0;
  left: 0;
  right: 0;
  margin: auto;
  width: 64px;
  height: 64px;
}
.lds-ripple div {
  position: absolute;
  border: 4px solid #fff;
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
