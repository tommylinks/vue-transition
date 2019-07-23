<template>
  <transition
      v-on:before-enter="beforeEnter"
      v-on:enter="enter"
      v-on:leave="leave"
      mode="in-out"
      :css="false"
  >

    <div class="wrap">
      <div class="home">
        <h1>Home page</h1>
      </div>
    </div>

  </transition>
</template>

<script>
// @ is an alias to /src
import {TweenMax, Power2} from "gsap/TweenMax"

export default {

  name: 'home',

    methods: {
        beforeEnter(el){
            TweenMax.to(el, 0, {
                yPercent: -100, scale: 0.9, ease: Power2.easeInOut
            })
        },
        enter(el, done){
            done()
            TweenMax.to(el, 1, {
                yPercent: -50, scale: 0.9, ease: Power2.easeInOut,
                onComplete: function() {
                    TweenMax.to(el, 1, {
                        yPercent: 0, scale: 1, ease: Power2.easeInOut
                    })
                }
            })
        },
        leave(el, done){
            TweenMax.to(el, 1, {
                yPercent: -50, scale: 0.9, ease: Power2.easeInOut,
                onComplete: function() {
                    TweenMax.to(el, 1, {
                        yPercent: -100, scale: 1, ease: Power2.easeInOut,
                        onComplete: function() { done() }
                    })
                }
            })
        }

    },




}
</script>


<style lang="sass">
  .wrap
    position: absolute
    top: 0
    left: 0
    width: 100%
  .home
    display: flex
    align-items: center
    justify-content: center
    height: 100vh
    width: 100%
    background-color: #bff1ff
</style>
