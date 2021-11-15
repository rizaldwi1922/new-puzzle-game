<template>
  <div id="app" class="wrapper d-flex align-items-stretch">
  <nav id="sidebar">
    <div class="p-4">
      <h1><a href="index.html" class="logo">Flip Card</a></h1>
      <ul class="list-unstyled components mb-5">
                        <li>
                             <router-link to="/"><span class="fa fa-users mr-3"></span>Group</router-link>
                        </li>
                        <li>
                            <router-link to="/puzzle"><span class="fa fa-plus mr-3"></span>Puzzle</router-link>
                        </li>
                    </ul>
    </div>
  </nav>
     <div id="content" class="p-4 p-md-5 pt-5">
       <router-view></router-view>
     </div>
    
  </div>
</template>

<script>
import Group from './components/Group.vue';
import Puzzle from './components/Puzzle.vue'
import VueRouter from 'vue-router'

const routes = [
            {
              path: '/',
              component: Group,
            },
            {
              path: '/puzzle',
              component: Puzzle
            }
        ]

const router = new VueRouter({
  mode: 'history',
  routes
})

export default {
  name: 'App',
  router
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
