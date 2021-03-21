<template>
  <div data-scroll-container>
    <Monstera data-scroll-section />
    <Variegata data-scroll-section />
    <Adansonii data-scroll-section id="adansonii" ref="adansoniiref"/>
  </div>
</template>

<script>
import Monstera from './components/Monstera.vue'
import Variegata from './components/Variegata.vue'
import Adansonii from './components/Adansonii.vue'
import LocomotiveScroll from 'locomotive-scroll';

export default {
  name: 'App',
  components: { Monstera, Variegata, Adansonii },
  data(){
    return {
      scroll: null
    }
  },
  mounted(){    
    this.scroll = new LocomotiveScroll({
      el: document.querySelector('[data-scroll-container]'),
      smooth: true,
      lerp: 0.07,
      smartphone: {
          smooth: true,
          direction: 'vertical',
          gestureDirection: 'vertical',
          lerp: 0,
      },
      tablet: {
          smooth: true, 
          direction: 'vertical',
          gestureDirection: 'vertical',
      },
    })
    
    this.scroll.on('scroll', () => {
      let half_win = window.innerHeight

      let updating = false
      if (!updating){
        if( half_win > document.getElementById('adansonii').getBoundingClientRect().top ){
          this.$refs.adansoniiref.deployTitle()
        }

        updating = true
        setTimeout(() => {
          updating = false
        }, 200)
      }   
    })

    setTimeout(() => {            
      this.scroll.update()
    }, 200)
  }
}
</script>

<style>
@import './locomotive/locomotive-scroll.css';
::-moz-selection {
  color: rgb(44, 44, 44);
  background: rgb(236, 236, 236);
}

::selection {
  color: rgb(44, 44, 44);
  background: rgb(236, 236, 236);
}
body
{
  margin: 0px;
  color: rgb(219, 219, 211);
}
#app
{
  overflow: hidden;
}
</style>
