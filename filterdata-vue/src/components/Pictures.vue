<template>
    <select id="text" v-model="selectedText" @change="onChange($event)">
      <option value="alle">Alle</option>
      <option value="kinder">Kinder</option>
      <option value="negativ">Negativ</option>
      <option value="baustelle">Baustelle</option>
      
    </select>
    <transition-group appear name="list-complete" tag="div" class="grid" >
        <div v-for="item  in photos" :key="item.rank" :class="item.text+ ' list-complete-item' ">
            <img :src="require(`@/assets/${item.Name}`) " >
        </div>
    </transition-group>

</template>

<script>
export default {
    data(){
        return{
            photos:[],
            photosOrig:[],
            selectedText: "alle"
        }
    }, 
    mounted(){
        fetch('http://localhost:3000/photos')
            .then(res => res.json())
            .then(data => this.photos = data)
            .then(data => this.photosOrig = data)
            .catch(err => console.log(err.message))
        
    },
    
  methods: {
      onChange(event) {
          this.selectedText = event.target.value
          this.updatePhotos()
          this.applySelectedText ()
        },
        updatePhotos () {
            this.photos = this.photosOrig.slice(0, this.photosOrig.length) 
        },
        applySelectedText () {
            if (this.selectedText !== "alle") {
                this.photos = this.photos.filter(photo => {
                    return photo.text === this.selectedText;
                });
            }
        }
    }
}
</script>

<style>
.grid{
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: repeat(4, 1fr);
    gap: 10px;
    align-items:center;
}
img{
    display:block;
    width:100%;
}


/* https://v3.vuejs.org/guide/transitions-enterleave.html#transitioning-single-elements-components*/
.list-complete-item {
    transition: all 1s;
    max-width:400px;
    margin:10px;
}
.list-complete-enter, .list-complete-leave-to
/* .list-complete-leave-active below version 2.1.8 */ {
    opacity: 0;
    transform: translateY(30px);
}
.list-complete-leave-active {
    position: absolute;
}

.kinder{
    background: rgb(111,113,189);
    background: linear-gradient(90deg, rgb(8, 15, 216) 0%, rgba(0,212,255,1) 100%);
}

.kinder img{
    mix-blend-mode:screen;
}

</style>