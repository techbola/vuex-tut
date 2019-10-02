<template>
  <div class="hello">
    <div class="left">
      <h1>{{ title }}</h1>

      <form @submit.prevent="addLink">
        <input type="text" class="link-input" placeholder="Add a link" v-model="newLink">
      </form>

      <ul>
        <li v-for="(link, index) in links" :key="index">
          {{ link }}
          <button @click="removeLinks(index)" class="rm">Remove</button>
        </li>
      </ul>
    </div>
    <div class="right">
      <stats />
    </div>
  </div>
</template>

<script>

import Stats from '@/components/Stats.vue'
import { mapState, mapMutations, mapActions } from 'vuex'

export default {
  name: 'HelloWorld',
  data(){
    return {
      newLink: ''
    }
  },
  components: {
    Stats
  },
  computed: {
    ...mapState([
      'title',
      'links'
    ]),
    // other stuffs
  },
  methods: {
    ...mapMutations([
      'ADD_LINK'
    ]),
    ...mapActions([
      'removeLink'
    ]),
    addLink(){
      this.ADD_LINK(this.newLink)
      this.newLink = ''
    },
    removeLinks(link){
      this.removeLink(link)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  html, #app, .home{
    height: 100%;
  }
  body{
    background-color: #f4f4f4;
    margin: 0;
    height: 100%;
  }
  .hello{
    display: grid;
    grid-template-columns: repeat(2, 50%);
    grid-template-rows: 100%;
    grid-template-areas: 
      "left right";
      height: 100%;
  }
  .left, .right{
    padding: 30px;
  }
  ul{
    padding: 0;
    list-style-type: none;
  }
  ul li{
    padding: 20px;
    background: white;
    margin-bottom: 8px;
  }
  .right{
    grid-area: right;
    background-color: #e9e9e9;
  }
  input{
    border: none;
    padding: 20px;
    width: calc(100% - 40px);
    box-shadow: 0 5px 5px lightgrey;
    margin-bottom: 50px;
    outline: none;
  }
  .rm{
    float: right;
    text-transform: uppercase;
    font-size: .8em;
    background: #F9D0E3;
    border: none;
    padding: 5px;
    color: #FF0076;
    cursor: pointer;
  }
</style>
