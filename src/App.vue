<script>
import { watch } from 'vue'
import Footer from './components/Footer.vue'
import callcontent from './components/callcontent.vue'
import { RouterLink, RouterView } from 'vue-router'
import genresDefault from './components/genre.json'

export default {
  components: {
        Footer, callcontent
    },
  data() {
    return {
      readmodeOn: true,
      genreChecked: [],
      genresDefault
    }
  },
  computed: {
    readmode(){
      return this.readmodeOn ? 'md:grid md:grid-cols-3' : 'grid md:grid-cols-2 md:mx-8'
    },
    comment(){
      return this.commentMode ? 'w-full' : ''
    },
  },
  methods: {
    toggleReadmode(){
      if(this.readmodeOn == true){
        this.readmodeOn = !this.readmodeOn
        this.comment = !this.comment
      }       
    },
    home(){
      this.readmodeOn = true
      this.comment = true
    },
  },
  watch:{
    $route (to, from){
      if(this.$route.path == '/'){
        this.readmodeOn = true;
        this.comment = true
      } else {
        this.readmodeOn = false;
        this.comment = false
      }
    }
  }
}

</script>

<template class="flex flex-cols">
  <!-- <div class="justify-center flex mt-4 md:mx-12 mx-2">
    <li v-for="list in genresDefault" class="m-1">
        <input type="checkbox" :value="list.genre" v-model="genreChecked" v-bind:name="list.id" v-bind:id="list.id" class="hidden peer" required="">
        <label @click="filterGenre" v-bind:for="list.id" class="inline-flex justify-between items-center p-1  text-gray-500 bg-gray-200 rounded border-2 border-gray-200 cursor-pointer border-gray-700 peer-checked:border-blue-600 hover:text-gray-100 peer-checked:text-gray-100 hover:bg-gray-50 text-gray-400 bg-gray-800 hover:bg-gray-700">
            <div class="block">
                <div class="w-full text-sm font-semibold ">{{ list.genre }}</div>
            </div>
        </label>
    </li>
  </div>

  <div v-for="item in genreChecked">
  <h1>{{ item }}</h1>
  </div> -->

  <div class="md:flex-row flex-col flex">
    <div id="showList" @click="toggleReadmode" 
      :class="readmode" 
      class=" md:grid md:grid-cols-3">

        <callcontent
          :limit="2"
          :genre="genreChecked"
        />

    </div>
    <div class="md:order-none order-first mx-auto md:mr-10 " :class="comment">
      <RouterView 
        :key="$route.path"
      ></RouterView>
    </div>
    <div class="md:hidden sticky top-0 order-first">
      <div class="p-2 w-full bg-neutral-800">
      <RouterLink @click="home" to="/">
          <h2 class="text-h font-semibold">
              Deskmate
          </h2>
        </RouterLink>
    </div>
    </div>
  </div>






<Footer></Footer>
</template>

<style scoped>
@media screen {
  
}
a {
  pointer-events: stroke;
}
h {
  font-weight: 400;
}

p {
  font-size: small;
}

</style>
