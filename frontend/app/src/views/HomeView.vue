<template>
  <p class="title">Fotune Teller</p>
  <div class="main">
    <p class="sign" align="center">Fill out details</p>
    <p>birthday</p>
      <input class="un" type="Date" align="center"  v-model="birthday">

      <p>date</p>
      <input class="un" type="Date" align="center"  v-model="sdate">
      <button class="submit" align="center" @click="generateRandomNumber">Go!</button>
               
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'HomeView',
  components: {
    //HelloWorld
  },

  data(){
    return{
        birthday:'',
        sdate:''
    };
  },
  
  methods: {
    generateRandomNumber() {
      const date = new Date(this.sdate)
      const birthday = new Date(this.birthday)
      //getTime():1970年1月1日00:00:00UTCからの経過ミリ秒数を返す
      const diffTime = Math.abs(date.getTime() - birthday.getTime())
      console.log("diffTime:", diffTime)
      const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24))
      console.log("diffDays:", diffDays)
      const seed = Math.floor(Math.random() * diffDays) + 1
      this.$router.push({ name: 'about', params: { seed } })
    }
  }
    }

</script>

<style>
.main {
    background-color: #ffffff;
    width: 400px;
    height: 400px;
    margin: 7em auto;
    border-radius: 1.5em;
    box-shadow: 0px 11px 35px 2px rgba(0, 0, 0, 0.14);
}

.sign {
    padding-top: 40px;
    color: #8C55AA;
    font-family: 'Ubuntu', sans-serif;
    font-weight: bold;
    font-size: 23px;
}

.title {
    padding-top: 40px;
    color: #8C55AA;
    font-family: 'Ubuntu', sans-serif;
    font-weight: bold;
    font-size: 60px;
}

.un {
width: 76%;
color: rgb(38, 50, 56);
font-weight: 700;
font-size: 14px;
letter-spacing: 1px;
background: rgba(136, 126, 126, 0.04);
padding: 10px 20px;
border: none;
border-radius: 20px;
outline: none;
box-sizing: border-box;
border: 2px solid rgba(0, 0, 0, 0.02);
margin-bottom: 50px;
margin-left: 46px;
text-align: center;
margin-bottom: 27px;
font-family: 'Ubuntu', sans-serif;
}

.submit {
  cursor: pointer;
    border-radius: 5em;
    color: #fff;
    background: linear-gradient(to right, #9C27B0, #E040FB);
    border: 0;
    padding-left: 40px;
    padding-right: 40px;
    padding-bottom: 10px;
    padding-top: 10px;
    font-family: 'Ubuntu', sans-serif;
    margin-left: 35%;
    font-size: 13px;
    box-shadow: 0 0 20px 1px rgba(0, 0, 0, 0.04);
}

.message {
  background: lightcyan;
  border-radius: 4px;
  padding: 1rem;
}

</style>
