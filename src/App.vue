<template>
  <div id="app">
    <div class="search">
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-search" viewBox="0 0 16 16">
          <path d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"/>
        </svg>
      <input type="text" placeholder="Search for any training you want " v-model="searchInp">
    </div>
    <div class="title">
      You’ve got <span>7 task</span> today 
      <button class="new" @click='showComp = !showComp'>
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-plus-square" viewBox="0 0 16 16">
            <path d="M14 1a1 1 0 0 1 1 1v12a1 1 0 0 1-1 1H2a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1h12zM2 0a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V2a2 2 0 0 0-2-2H2z"/>
            <path d="M8 4a.5.5 0 0 1 .5.5v3h3a.5.5 0 0 1 0 1h-3v3a.5.5 0 0 1-1 0v-3h-3a.5.5 0 0 1 0-1h3v-3A.5.5 0 0 1 8 4z"/>
          </svg>
      Add New</button>
    </div>

    <Work v-show="showComp">
    </Work>

    <Works :ishlar='onHold' @save='saveLoc()'>
      <h2 class="table-title">On Hold</h2>
    </Works>
    <Works :ishlar='completed' style='color:#BDBDBD' @save='saveLoc()'>
      <h2 class="table-title">Completed</h2> <span class="inactive">Inactive</span>
    </Works>
    <Works :ishlar='deleted' v-show="delet"
    style='color:#BDBDBD' @save='saveLoc()'>
      <h2 class="table-title">Deleted</h2>
    </Works>

  </div>
</template>

<script>
import Work from './components/Work.vue'
import Works from './components/Works.vue'
import { eventEmitter } from './main'

export default {
  name: 'App',
  data(){
    return {
      delet: false,
      lists: [],
      showComp: false,
      showClass: '',
      searchInp: '',
      deleteStatus: '',
      showTable: false
    }
  },
  components: {
    Work, Works
  },
  methods: {
    saveLoc() {
      localStorage.setItem('TodoList', JSON.stringify(this.lists))
    }
  },
  computed: {
    onHold(){
      return this.lists.filter( p => {
        return p.status == 'pending' || p.status == 'progress'
      })
    },
    completed(){
      return this.lists.filter( p => {
        return p.status == 'completed' || p.status == 'cancelled'
      })
    },
    deleted(){
      return this.lists.filter( p => {
        return p.status == 'deleted'
      })
    }
  },
  created(){
    if (localStorage.getItem('TodoList')) {
          try {
            this.lists = JSON.parse(localStorage.getItem('TodoList'))
          } catch (error) {
            localStorage.removeItem('TodoList')
          }
    }
    eventEmitter.$on('newWork', (m)=> {
      this.lists.push(m)
      this.saveLoc()
    }),
    eventEmitter.$on('showComponent', (n)=> {
      this.showComp = n
    }),eventEmitter.$on('delStatus', (s)=> {
      this.deleteStatus = s
    })   
  }
}
</script>

<style>
@font-face {
  font-family: 'm-black';
  src: url(assets/fonts/Montserrat-Black.ttf);
}
@font-face {
  font-family: 'm-bold';
  src: url(assets/fonts/Montserrat-Bold.ttf);
}
@font-face {
  font-family: 'm-r';
  src: url(assets/fonts/Montserrat-Regular.ttf);
}
#app {
  width: 80%;
  margin: auto;
  padding: 20px;
}
*, body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
input:focus {
  outline: 0;
}
</style>
<style scoped>
.search {
  width: 100%;
  display: flex;
  margin-bottom: 30px;
  align-items: center;
  position: relative;
}
.search input {
  border: 0;
  width: 100%;
  padding: 10px;
  padding-left: 30px;
  border-radius: 20px;
  font-family: 'm-r', serif;
}
.search svg {
  position: absolute;
  left: 10px;
  margin-right: 10px;
}
.search input:focus {
  outline: 1px solid #ccc;
}
.title {
  font-size: 36px;
  font-family: 'm-black', serif;
  font-weight: bold;
  color: #1D262C;
}
.title span {
  color: #F3477A;
}
.new  {
  background-color: #884CB2;
  font-size: 14px;
  font-family: 'm-r',serif;
  padding: 10px 30px;
  border-radius: 10px;
  color: #fff;
  border: 0;
  margin-bottom: 10px;
  margin-left: 20px;
  transform: translateY(-5px);
}
.new svg{
  margin-right: 5px;
  transform: translateY(2px);
}
.table-title {
  color: #1D262C;
  font-size: 20px;
  font-family: 'm-bold', serif;
  margin: 30px 0;
  display: inline-block;
}
.inactive {
    display: inline-block;
    font-family: 'm-r', serif;
    width: 100px;
    text-align: center;
    margin-left: 20px;
    background: rgba(235, 87, 87, 0.2);
    color: #EB5757;
    padding: 3px;
    border-radius: 10px;
}
</style>
