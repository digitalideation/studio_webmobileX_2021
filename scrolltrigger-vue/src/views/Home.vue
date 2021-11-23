<template>
  <div v-if="stories.length">
     <section class="wrap" id="container">
      <div v-for="section in stories" :key="section.id">
     

      <div class="img" :data-attr-color="section.color">
            <img :src="require(`@/assets/low/${section.img}`) ">
            <div class="caption"><span> {{section.text}}</span></div>
        </div>

      </div>
      </section>
  </div>
  <div v-else>
      <p>Loading Stories</p>
  </div>
  
  
</template>


<script>
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
gsap.registerPlugin(ScrollTrigger);
export default {
    data(){
        return{
            stories:[]
        }
    }, 
    mounted(){
        fetch('http://localhost:3000/stories')
            .then(res => res.json())
            .then(data => this.stories = data)
            .catch(err => console.log(err.message))
       
        
    },
    updated() {
       this.scrollAnimation();
    },
    methods:{
      scrollAnimation(){
         gsap.utils.toArray('.img').forEach((section, i) => {

        if (section.getAttribute('data-attr-color') !== null) {

            let colorAttr = section.getAttribute('data-attr-color');


            gsap.to("body", {
                backgroundColor: colorAttr,
                immediateRender: false,
                scrollTrigger: {
                    trigger: section,
                    scrub: true,
                    delay: 1,
                    duration: 2,
                    start: 'top bottom',
                    end: '+=100%'
                }
            })
             gsap.to(section.getElementsByTagName('img')[0], {
                autoAlpha: 1,
                immediateRender: false,
                scrollTrigger: {
                    trigger: section,
                    scrub: true,
                    duration: 2,
                    start: 'top center',
                    end: '+=100%'
                }
            })
            


        }

      });
      }
    }
}
</script>
<style scoped>
html {
            --color: transparent;
        }
        
        img {
            display: block;
            width: calc(100% - 40px);
            margin-left: auto;
            margin-right: auto;
            max-width: 900px;
            margin-top: 2rem;
            filter: sepia(100%) hue-rotate(150deg) saturate(150%) brightness(110%);
            opacity: 0.2;
        }
        
        body {
            margin: 0;
            padding: 0;
            font-family: 'Inria Serif', Georgia, serif;
            font-size: 1.8rem;
            background: var(--color);
        }
        
        .caption {
            width: calc(100% - 40px);
            margin-left: auto;
            margin-right: auto;
            max-width: 600px;
            margin-top: 2rem;
            margin-bottom: 100px;
        }
</style>