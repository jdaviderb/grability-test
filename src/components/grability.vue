<template>
  <div class="container">
    <div class="menu">
      <div class="toggle has-tap" @click="show = !show">
        <i class="fa fa-list-ul fa-lg"></i>
      </div>
    </div>
    <div class="items">
         <transition name="item-effect" v-for="item in items">
          <div class="item" v-show="show">

            <div class="header has-tap" @click="item.show = !item.show">
              <img :src="item.image" class="photo-grability">
              <div class="description">
                <p>{{item.title}}</p>
              </div>
            </div>
            <transition name="item-show-effect">
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
      items: items
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
    }

    .has-tap:active {
      opacity: 0.5;
    }

    .menu {
      background-color: #FF6856;
      padding: 2em;
      margin-bottom: 2em;
    }

    .menu .toggle {
      color: white;
      cursor: pointer;
    }

    .items {
        display: flex;
        flex-direction: column;
        flex: 1;
        font-family: 'Roboto', sans-serif;

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
      width: 90%;
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

    .item-effect-enter-active:nth-child(odd), .item-effect-leave-active:nth-child(odd) {
      transition: width 0.8s;
    }

    .item-effect-enter-active:nth-child(even), .item-effect-leave-active:nth-child(even) {
      transition: width 0.7s;
    }

    .item-effect-enter, .item-effect-leave-to {
      width:  0%;
    }

    .item-show-effect-enter-active {
      transition: all 0.5s;
      animation: item-show-effect-in 0.5s;
    }
    .item-show-effect-leave-active {
      transition: opacity 0.5s;

      animation: item-show-effect-out 0.5s;
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

    @keyframes item-show-effect-in {
      0% {
        opacity: 0;
        max-height: 0;
        transform: translateY(0);

      }
    }

    @keyframes item-show-effect-out {
      100% {
        transform: translateY(0);
        opacity: 0;
        max-height: 0;
      }
    }
</style>
