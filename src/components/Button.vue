<template>
  <div class="">

    <a href="javascript:;" class="btn_login">
      {{text}}
    </a>
  </div>
</template>

<script>

import Lib from 'assets/Lib.js'

export default {
	components:{

	},
  data: function () {
    return {
      msg: 'Hello moto! what`s up,yaoyao'
    }
  },
  ready(){

  },
  methods:{

  },
  props:{
  	"text":{
		type:String,
		default:"登录"
	}
  }
}
</script>


<style scoped>
  .btn{
    text-align: center;
    height: 30px;
    width: 200px;
    background: #fff;
  }
  .btn_login{
background:#04BE02;
color:#fff;
display:block;
height:45px;
  width: 200px;
text-align:center;
line-height:45px;
border-radius:10px;
margin: 25px auto;
}
</style>
