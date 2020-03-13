<template>
  <div class="q-pa-md row items-start q-gutter-md flex justify-center full-height items-center">
    <!-- <q-img src="../../assets/bg2.png" class="fullscreen" /> -->
    <q-card class="my-card col-md-4 col-sm-10 col-xs-12">
      <q-card-section class="bg-amber-10 text-white " :class="finalBgColor" align="center">
        <svg id="logo" viewBox="0 0 483 483"
             style="enable-background:new 0 0 460 460;"
             xml:space="preserve" width="128px" height="128px"
             v-html="logoMethod">
        </svg>
        <h4 class="q-mt-md">{{logo}}</h4>
      </q-card-section>
      <div class="bg-white q-pa-md q-mt-md">
        <q-input
          v-model="email"
          label="Email"
          dense />

        <div class="stacked-label">
          <q-input
          v-model="password"
           label="Password"
          dense />
        </div>
      </div>
      <div class="q-pa-md column q-mt-md bg-blue-1" >
        <q-btn color="teal" label="Login" class="q-my-xs"/>
        <!-- <p class="flex justify-right" color="blue"> Forgot Password? </p> -->
        <!-- <q-btn color="red" label="Login Google" class="q-my-xs"/>
        <q-btn color="blue" label="Login Facebook" class="q-my-xs"/> -->
      </div>
    </q-card>
  </div>
</template>

<script type="text/javascript">
/* eslint-disable */
  import {mapMutations} from 'vuex'
  import Vivus from 'vivus'
  import logoData from './logoData'
  import { Platform } from 'quasar'
  export default {
    mounted () { 
      this.startAnimation()
    },
    beforeDestroy () {
    },
    computed: {
      finalBgColor () {
        return `bg-${this.bgColor}-${this.toneColor}`
      },
      logoMethod () {
        return logoData[this.logo]
      }
    },
    data () {
      return {
        logos: Object.keys(logoData),
        logo: 'Login',
        email: '',
        password: '',
        buttonClass: 'normal',
        vivus: ''
      }
    },
    methods: {
      startAnimation () {
        this.vivus = new Vivus('logo', {
            duration: 400,
          forceRender: false
          }, function(element) {
            for (let item of element.el.children[0].children) {
              item.setAttribute('style', 'fill:white')
              item.setAttribute('style', 'fill:white')
            }
          }
        )
      }
    }
  }
</script>

<style>

</style>
