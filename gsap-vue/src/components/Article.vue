<template>
    <div v-if="stories.length">
      <div v-for="section in stories" :key="section.id">
     
<section>
    <div class="column">
        <img :src="require(`@/assets/${section.images.eins}`) ">
        <div class="legend">
                <span>
                    {{section.legende}}
                </span>
            </div>
    </div>
    <div class="column">
         <img :src="require(`@/assets/${section.images.zwei}`) ">
    </div>
    <div class="column">
         <img :src="require(`@/assets/${section.images.drei}`) ">
    </div>
</section>

       
     
      </div>
  </div>
  <div v-else>
      <p>Loading Stories</p>
  </div>
</template>

<script>
import { gsap } from 'gsap';

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
    updated(){
        /* Lifecycle hooks https://v3.vuejs.org/api/options-lifecycle-hooks.html#updated */

        var tl = gsap.timeline();

        tl.to(
            ".column img", {
                y: "random(-50,50)",
                x: "random(-50,50)",
                duration: 1,
                stagger: 0.5,
                ease: "back.out(1.7)",
                filter: "blur(0px)"

            }
        )
        tl.from(".legend ", {
            duration: 1,
            opacity: 0
        });
    }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Lato&display=swap');
        body {
            margin: 2rem;
            padding: 2rem;
            font-family: 'Lato', sans-serif;
            font-size: 1.4em;
        }
        
        section {
            margin: 0 auto;
            display: flex;
        }
        
        .column {
            margin: 10px;
            flex-grow: 1;
            flex-shrink: 1;
            flex-basis: 0;
        }
        
        img {
            width: 100%;
             filter: blur(10px);
            box-shadow: 10px 5px 5px rgba(0, 0, 0, 0.6);
        }
        
        .legend span {
            background-color: blue;
            color: white;
            line-height: 140%;
        }
        
        .legend {
            margin-top: -100px;
            margin-left: -50px;
            width: 80%;
            z-index: 5;
            position: relative;
        }
</style>