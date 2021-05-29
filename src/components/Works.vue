<template>
  <div class="table">
      <slot></slot>
      <table width='100%'>
          <tr v-for="(ish, index) of ishlar" :key='index'>
              <td class="name">{{ish.matn}}</td>
              <td class="status"><span  :class="ish.status">{{ish.status}}</span></td>
              <td class="turi"><span :class="ish.turi"></span>{{ish.turi}}</td>
              <td class="who"><div v-for='(ism, ismindex) of ish.who' :class="ism" class="who-image" :key='ismindex'></div></td>
              <td class="btns">
                <span style="display: none;">{{index}}</span>
                <button class="dots" @click='btnShow()' v-show="!isBtn">
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-three-dots" viewBox="0 0 16 16">
                    <path d="M3 9.5a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3zm5 0a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3zm5 0a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3z"/>
                </svg>
                </button>
                <div class="delEdit">
                    <button class="edit" v-show="isBtn" @click="isBtn = !isBtn">
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="#F2994A" class="bi bi-pen" viewBox="0 0 16 16">
                    <path d="m13.498.795.149-.149a1.207 1.207 0 1 1 1.707 1.708l-.149.148a1.5 1.5 0 0 1-.059 2.059L4.854 14.854a.5.5 0 0 1-.233.131l-4 1a.5.5 0 0 1-.606-.606l1-4a.5.5 0 0 1 .131-.232l9.642-9.642a.5.5 0 0 0-.642.056L6.854 4.854a.5.5 0 1 1-.708-.708L9.44.854A1.5 1.5 0 0 1 11.5.796a1.5 1.5 0 0 1 1.998-.001zm-.644.766a.5.5 0 0 0-.707 0L1.95 11.756l-.764 3.057 3.057-.764L14.44 3.854a.5.5 0 0 0 0-.708l-1.585-1.585z"/>
                    </svg>
                </button>
                <button class="delet" v-show="isBtn" @click="del(index)">
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="red" class="bi bi-person-x" viewBox="0 0 16 16">
                    <path d="M6 8a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm2-3a2 2 0 1 1-4 0 2 2 0 0 1 4 0zm4 8c0 1-1 1-1 1H1s-1 0-1-1 1-4 6-4 6 3 6 4zm-1-.004c-.001-.246-.154-.986-.832-1.664C9.516 10.68 8.289 10 6 10c-2.29 0-3.516.68-4.168 1.332-.678.678-.83 1.418-.832 1.664h10z"/>
                    <path fill-rule="evenodd" d="M12.146 5.146a.5.5 0 0 1 .708 0L14 6.293l1.146-1.147a.5.5 0 0 1 .708.708L14.707 7l1.147 1.146a.5.5 0 0 1-.708.708L14 7.707l-1.146 1.147a.5.5 0 0 1-.708-.708L13.293 7l-1.147-1.146a.5.5 0 0 1 0-.708z"/>
                    </svg>
                </button>
                </div>
              </td>
          </tr>
      </table>
  </div>
</template>

<script>

export default {
    props: ['ishlar'],
    data(){
        return {
            isBtn:false
        }
    },
    methods: {
        btnShow(){
            this.isBtn = true
        },
        del(index){
            this.ishlar[index].status = 'deleted'
            this.$emit('save')
            this.isBtn = false
        }
    }
}
</script>

<style scoped>
table tr {
    padding-bottom: 18px;
    margin-bottom: 20px;
    display: flex;
    font-family:'m-r', serif;
    justify-content: space-between;
    align-items: center;
    border-bottom: 0.5px solid #E0E0E0;
}
table tr:last-child {
    border-bottom: 0;
}
.name {
    width: 45%;
    font-size: 14px;
    position: relative;
    padding-left: 15px;
}
.name:before {
    content: "";
    display: inline-block;
    position: absolute;
    left: 0;
    top: 3px;
    width: 10px;
    height: 10px;
    border-radius: 50%;
    background-color: #F3477A;
}
.status {
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 12px;
    width: 30%;
    text-transform: capitalize;
}

.status span {
    display: inline-block;
    width: 35%;
    text-align: center;
    background-color:rgba(242, 153, 74, 0.2);
    color: #F2994A;
    padding: 3px;
    border-radius: 10px;
}
.status span.progress {
    color: #56CCF2;
    background-color: #DDF5FC;
}
.status span.completed {
    color: #27AE60;
    background-color: #F2FAF5;
}
.status span.completed {
    color: #EB5757;
    background-color: #FEF5F5;
}
.turi {
    width: 15%;
    font-size: 12px;
    position: relative;
    text-transform: capitalize;
}
.turi span {
    display: inline-block;
    width: 10px;
    height: 10px;
    border-radius: 50%;
    margin-right: 4px;
    border: 3.5px solid #219653;
}
.turi span.normal{
    border-color: #F2C94C;
}
.turi span.critical{
    border-color: #EB5757;
}
.who {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    width: 15%;
}
.who img {
    width: 20px;
    height: 20px;
    margin-right: -5px;
}
.btns {
    width: 100px;
    display: flex;
    justify-content: flex-end;
}
.btns .dots {
    border: 0;
    padding: 6px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #DCD9D9;
}
.delEdit{
    display: flex;
}
.delEdit .edit {
    background: unset;
    border: 1px solid #F2994A;
    border-radius: 7px;
    padding: 6px 8px;
    margin-top: -5px;
}
.delEdit .delet {
    background-color: unset;
    border: 1px solid red;
    border-radius: 7px;
    padding: 6px 8px;
    margin-left: 10px;
    margin-top: -5px;
}
.who-image {
     width: 30px;
    height: 30px;
    margin-left: -7px;
    background-size: cover;
    background-repeat: no-repeat;
}
.who-image.anna {
    background: url(../assets/img/anna.png);
    background-repeat: no-repeat;
}
.who-image.john {
    background: url(../assets/img/john.png);
    background-repeat: no-repeat;
}
.who-image.jack {
    background: url(../assets/img/jack.png);
    background-repeat: no-repeat;
}
</style>