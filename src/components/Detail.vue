<template>
  <div>
    <div id='hd'>
      <div class='w'>
        <h2>欢迎您：{{username}}</h2>
      </div>

    </div>
    <div id='bd'>
      <div class="in w">
        <input type="text" placeholder='请输入内容' v-model='currentText'>
        <button @click="btnClick">确定</button>
      </div>
      <ul class="w">
        <li v-for='(item,index) in content' v-bind:key='index' @click='liClick(item)'>{{item}}</li>
      </ul>
    </div>
  </div>

</template>

<script src="../src/utils.js"></script>
<script>

  import {toast, copy2Clipboard} from '../utils'
  import axios from 'axios'
  export default {
    name: 'Detail',
    data() {
      return {
        username: '',
        currentText:'',
        content: []
      }

    },
    methods: {
      btnClick() {
        let that = this
        console.log(this.currentText)
        if (this.currentText !='') {
          
          //1. 将currentText插入到数据库
          if(this.username){
            let url = 'http://10.10.33.24:3000/insert'
            axios.post(url, {
              username: this.username,
              content: this.currentText
            }).then(function(response){
              //2. 将currentText添加到content列表
              that.content.unshift(that.currentText)
              //3. 清空输入框
              that.currentText=''
              
            }).catch(function(err){
              throw err
            })
          }

        } else {
          toast('请输入内容')
        }
      },
      liClick(item) {
        copy2Clipboard(item)
        if(item){
          toast('已复制到剪切板')
        }
      },
      //从数据库查询数据，并绑定到content变量上
      refresh(){
        let that = this
        if(this.username){
          let url = `http://10.10.33.24:3000/${this.username}`
          axios.get(url).then(function(response){
            that.content=response.data
          }).catch(function(err){
            throw err
          })
        }
      }
    },
    created: function(){
        this.username=this.$route.params.username
        this.refresh()
    }
  }

</script>

<style>
  * {
    box-sizing: border-box;
    list-style: none;
    margin: 0;
    padding: 0;
  }

  .w {
    width: 75%;
    margin: 0 auto;
  }

  #hd {
    height: 50px;
    background-color: purple;
  }

  #hd h2 {
    color: #fff;
    font-weight: 400;
    line-height: 50px;

  }

  #bd {
    margin-top: 10px;
  }

  .in {
    height: 40px;
  }

  #bd input {
    width: 80%;
    height: 100%;
    float: left;
  }

  #bd button {
    width: 15%;
    height: 100%;
    float: right;
    font-size: 16px;
  }

  #bd ul {
    margin-top: 30px;
  }

  #bd ul li {
    height: 40px;
    margin-top: 15px;
    border: 1px solid #4f4f4f;
    line-height: 45px;
    font-size: 14px;
    text-overflow: ellipsis;
    white-space: nowrap;
    overflow: hidden;
  }

  #bd ul li:active {
    box-shadow: 1px 1px #4f4f4f;
  }

</style>
