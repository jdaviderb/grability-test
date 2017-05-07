<template>
  <div class="container">
    <div class="menu">
      <div class="toggle has-tap" @click="toggleMenu">
        <i class="fa fa-list-ul fa-lg"></i>
      </div>
      <transition name="item-header-effect">
        <div v-show="selectItem.show" class="title">{{ selectItem.title }}</div>
      </transition>
    </div>
    <div class="items">
     <transition name="item-effect" v-for="item in items">
      <div class="item" v-show="show">

        <div class="header has-tap" @click="toggle(item)">
          <img :src="item.image" class="photo-grability">
          <div class="description">
            <p>{{item.title}}</p>
          </div>
        </div>
        <transition name="item-show">
          <div class="content" v-show="item.show">
            <div class="notice">
              <h2>{{ item.title }}</h2>
              <div class="description">{{ item.content }}</div>
            </div>
          </div>
        </transition>
      </div>
    </transition>
  </div>
</div>
</template>

<script>
  import items from '../data.json'

  export default {
    name: 'grability',
    data () {
      return {
        show: false,
        items: items,
        selectItem: {show: false}
      }
    },
    methods: {
      toggle (data) {
        this.selectItem = data
        data.show = !data.show
      },
      toggleMenu () {
        this.show = !this.show
        this.selectItem.show = false
        this.selectItem = {show: false}
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  .container {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
    background-color: #CDCDCB;
    font-family: 'Roboto', sans-serif;
  }

  .has-tap:active {
    opacity: 0.5;
  }

  .menu {
    display: flex;
    background-color: #FF6856;
    padding: 2em;
    margin-bottom: 2em;
  }

  .menu .toggle {
    color: white;
    cursor: pointer;
  }

  .menu .title {
    flex: 1;
    color: white;
    text-align: center;
    overflow: hidden;
  }

  .items {
    display: flex;
    flex-direction: column;
    flex: 1;
  }

  .item {
    display: flex;
    flex-direction: column;
    width: 100%;
    align-items:  center;
  }

  .item .header, .item .content {
    background-color: white;
    display: flex;
    padding: 1em;
    width: 85%;
    margin: 5px;
    overflow:hidden;

  }

  .item .header .photo-grability {
    width: 100px;
    height: 100px;
    border-radius: 100%;
  }

  .item .header .description {
    padding: 1em;
    justify-content: center;
    flex: 1;
  }

  .item  > .content {
    display: flex;
    overflow: hidden;
    max-height: 100vh;
    padding: 1em;
  }

  .item .content .notice {
    padding: 1em;
    text-align: justify;
  }

  /* animations */

  .item-header-effect-enter-active, .item-header-effect-leave-active {
    transition:  all 0.4s;
  }

  .item-header-effect-enter {
      transform: translate(100em);
  }

  .item-header-effect-leave-to {
    transform: translateX(100em);
     
  }

  .item-effect-enter-active:nth-child(1){
    animation: item-in .5s;
    transition: width 0.5s;
    overflow: hidden;
  }

  .item-effect-enter-active:nth-child(2){
    animation: item-in .45s;
    transition: width 0.4s;
  }

  .item-effect-enter-active:nth-child(3){
    animation: item-in .35s;
    transition: width 0.5s;
  }

  .item-effect-enter-active:nth-child(4){
    animation: item-in .30s;
    transition: width 0.5s;
  }

  .item-effect-leave-active  {
    transition: transform 0.5s;
    transform: scale(0);
  }


  .item-show-enter-active {
    transition: all 0.5s;
    animation: item-show-in 0.5s;
  }

  .item-show-leave-active {
    transition: all 0.5s;
    animation: item-show-out 0.5s;
  }

  @keyframes item-show-in {
    0% {
      max-height: 0;
    }

    50% {
      padding-bottom: 4em;
    }

    100% {
      padding-bottom: 1em;
    }

  }

  @keyframes item-show-out {
    100% {
      font-size: 0;
      padding: 0;
      margin: 0;
      opacity: 0;
      max-height: 0;
    }
  }

  @keyframes item-in {
    0% {
      width: 0%;
    }
    70% {
      width: 104%;
    }

    80% {
      width: 103%;
    }

    90% {
      width: 102%;
    }

    100% {
      width: 100%;
    }
  }

  
</style>
