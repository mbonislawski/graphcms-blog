<template>
  <div id="app">
    <div class="hamburger" :class="{'active': menuActive}" @click="menuActive = !menuActive">
      <span></span>
      <span></span>
      <span></span>
    </div>
    <div id="nav" :class="{'active': menuActive}" @click="menuActive = false">
      <router-link to="/">Home</router-link>
      <router-link to="/about">About</router-link>
      <router-link to="/blog">Blog</router-link>
    </div>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      menuActive: false,
    };
  },
};
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.hamburger {
  width: 28px;
  height: 20px;
  position: absolute;
  transition: .3s all;
  -moz-transition: .3s all;
  cursor: pointer;
  z-index: 2;
  right: 30px;
  top: 35px;
  margin: auto;
}

.hamburger span {
  position: absolute;
  background-color: #F3EFE0;
  height: 2px;
  width: 100%;
  transition: .3s all;
  -moz-transition: .3s all;
  left: 0;
}

.hamburger.active span:first-child {
  -webkit-transform: rotate(45deg);
  -moz-transform: rotate(45deg);
}

.hamburger span:nth-child(2) {
  top: 7.5px;
}

.hamburger span:last-child {
  top: 15.5px;
}

.hamburger.active span:nth-child(2) {
  height: 2.5px;
  -webkit-transform: translate(0,10px);
  -moz-transform: translate(0,10px);
  opacity: 0;
}

.hamburger.active span:last-child {
  -webkit-transform: rotate(-45deg);
  -moz-transform: rotate(-45deg);
  top: 0;
}

#nav {
  position: fixed;
  right: 0;
  top: 0;
  width: 300px;
  height: 100vh;
  background-color: #151515;
  z-index: 1;
  padding-top: 120px;
  opacity: 0;
  transform: translateX(300px);
  transition: all .3s;
  &.active {
    transform: translateX(0);
    opacity: 1;
  }
  a {
    font-weight: bold;
    color: #F3EFE0;
    border: none;
    width: 100%;
    display: block;
    text-align: left;
    font-size: 14px;
    position: relative;
    padding: 8px 16px;
    text-decoration: none;
    &.router-link-exact-active {
      color: #F3EFE0;
      background-color: rgba(239, 98, 108, .1);

      &::before {
        content: '';
        width: 4px;
        height: 100%;
        position: absolute;
        left: 0;
        top: 0;
        background-color: #B3001B;
      }
    }
  }
}
</style>
