<template>
  <div v-if="stories.length">
      <div v-for="section in stories" :key="section.id">
     
        <section class="blend" :id="'img'+section.id" :style="'background-image:url('+ require(`@/assets/${section.img}`) + '), linear-gradient('+section.color1+', '+section.color2+')'"></section>
        <section class="text" :style="'color:'+section.color2">
        {{section.text}}
        </section>
     
      </div>
  </div>
  <div v-else>
      <p>Loading Stories</p>
  </div>
  
  
</template>

<script>
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
        
    }
}
</script>

<style>
 @import url('https://fonts.googleapis.com/css2?family=Inria+Serif:wght@300&display=swap');
        body {
            margin: 0;
            padding: 0;
            font-family: 'Inria Serif', Georgia, serif;
            font-size: 1.8rem;
            color: rgb(0, 68, 255);
            background-color: rgba(255, 255, 255, 0.6)
        }
        
        
        .blend {
            height: 100vh;
            width: 100vw;
            position: relative;
            background-attachment: fixed, scroll;
            background-size: cover;
            background-position: center center;
            background-blend-mode: multiply, screen;
        }
        
        .text {
            width: calc(100% - 40px);
            margin-left: auto;
            margin-right: auto;
            max-width: 600px;
            margin-bottom:1rem;
            margin-top:1rem;
            filter: brightness(50%);
        }
        
</style>