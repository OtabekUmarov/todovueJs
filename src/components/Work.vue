<template>
  <div class="modal" v-show="modalActive">
       <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">ToDo LiSt</h5>
          </div>
          <div class="modal-body">
            <input type="text" placeholder="Mazmunini kiriting" v-model='list.matn'>
            <div>
              <p><b>Status</b></p>
              <label><input type="radio" name="status" value='pending' v-model='list.status'>Pending</label>
              <label><input type="radio" name="status" value='progress' v-model='list.status'>Progress</label>
              <label><input type="radio" name="status" value='completed' v-model='list.status'>Completed</label>
              <label><input type="radio" name="status" value='cancelled' v-model='list.status'>Cancelled</label>
            </div>
            <div>
              <p><b>Tanlang</b></p>
              <label><input type="radio" name="turi" value='minor' v-model='list.turi'>Minor</label>
              <label><input type="radio" name="turi" value='normal' v-model='list.turi'>Normal</label>
              <label><input type="radio" name="turi" value='critical' v-model='list.turi'>Critical</label>
            </div>
            <div>
              <p><b>Who</b></p>
              <label><input type="checkbox" v-model='list.who' value="anna">Anna</label>
              <label><input type="checkbox" v-model='list.who' value="jack">Jack</label>
              <label><input type="checkbox" v-model='list.who' value="john">John</label>
            </div>
          </div>
          <div class="modal-footer">
            <!-- <button @click='saqla'><i class="bi bi-save2 me-2"></i>Saqlash</button> -->
            <button @click='add'><i class="bi bi-list-check me-2"></i>Ro'yhatga olish</button>
          </div>
        </div>
  </div>
</template>

<script>
import { eventEmitter } from '../main'
export default {

data(){
    return{
        list: {
            who:[],
            status:'',
            matn: ''
        },
        modalActive: false
        }
    },
    methods: {
        add(){
            this.modalActive = false
            eventEmitter.$emit('newWork', this.list)  
            eventEmitter.$emit('showComponent', this.modalActive)
            this.list= {
                who:[]
            }
        }
    }
}
</script>

<style scoped>
.modal {
    width: 100%;
    height: 100vh;
    display: flex;
    font-family: 'm-r', serif;
    top: 0;
    left: 0;
    z-index: 1;
    position: fixed;
    align-items: center;
    justify-content: center;
    background-color: rgba(0, 0, 0, 0.7);
    transition: .5s;
}
.modal-content {
    width: 600px;
    padding: 50px;
    padding-bottom: 20px;
    background-color: #fff;
    border-radius: 20px;
}
.modal-title {
    font-size: 26px;
    text-align: center;
}
input[type=text]{
    width: 100%;
    margin-top: 20px;
    margin-bottom: 10px;
    padding: 10px;
    border-radius: 10px;
    border: 1px #ccc solid;
}
P {
    margin-top: 15px;
    margin-bottom: 5px;
}
label {
    font-size: 14px;
    margin-right: 10px;
}
label input {
    margin-right: 5px;
}
.modal-footer {
    text-align: center;
    margin: 20px 0;
}
button {
    width: 50%;
    padding: 10px;
    border: 0;
    border-radius: 10px;
    color: #fff;
    font-size: 16px;
    background-color: green;
    cursor: pointer;
}
.jadvalTek {
    margin-top: 10px;
    display: flex;
    justify-content: space-between;
}
.jadval {
    color: rgb(94, 94, 230);
    padding: 10px 0;
}
.out {
    color: rgb(209, 107, 107);
    padding: 10px 0;
    cursor: pointer;
}
</style>