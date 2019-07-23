<template>
  <transition
      v-on:before-enter="beforeEnter"
      v-on:enter="enter"
      v-on:leave="leave"
      :css="false"
      mode="in-out"
  >

    <div class="wrap">
      <div class="about">
        <h1>This is an about page</h1>
      </div>
    </div>

  </transition
>
</template>

<script>
  import {TweenMax, Power2} from "gsap/TweenMax"

  export default {

    name: 'about',

    methods: {

        beforeEnter(el){
            console.log('test');
            TweenMax.to(el, 0, {
                yPercent: 100, scale: 0.9, ease: Power2.easeInOut
            })

        },
        enter(el, done){
            done();
            TweenMax.to(el, 1, {
                yPercent: 50, scale: 0.9, ease: Power2.easeInOut,
                onComplete: function() {
                    TweenMax.to(el, 1, {
                        yPercent: 0, scale: 1, ease: Power2.easeInOut
                    })
                }
            })
        },
        leave(el, done){
            TweenMax.to(el, 1, {
                yPercent: 50, scale: 0.9, ease: Power2.easeInOut,
                onComplete: function() {
                    TweenMax.to(el, 1, {
                        yPercent: 100, scale: 1, ease: Power2.easeInOut,
                        onComplete: function() { done() }
                    })
                }
            })
        }

    }

  }
</script>



<style lang="sass">
  .wrap
    position: absolute
    top: 0
    left: 0
    width: 100%
  .about
    display: flex
    align-items: center
    justify-content: center
    height: 100vh
    background-color: antiquewhite

  h1
    margin-top: 0
</style>

