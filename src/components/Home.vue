<template>
  <div>
    <div id='hd'>
      <div class='w'>
        <h2>同步你的记录</h2>
      </div>
    </div>
    <div id='bd'>
      <h2>使用步骤</h2>
      <br>
      <h4>1. 访问http://rdm.onecloud.xunlei.cn/syn-records/pages/{标识}</h4>
      <br>
      <h4>例如：http://rdm.onecloud.xunlei.cn/syn-records/pages/test</h4>
      <br>
      <br>
      <h4>2. 同步内容</h4>
      <br>
      <h4>在输入框中输入内容，并点击确定按钮</h4>
      <br>
      <br>
      <h4>3. 复制内容</h4>
      <br>
      <h4>点击列表条目即可把内容复制到剪切板</h4>

    </div>
  </div>

</template>
<script>
    export default{
        name: 'Home',
        data() {
            return {
                msg: '欢迎您'
            }
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

  #bd h2 {
    color: #4f4f4f;
    text-align: center;
  }

  #bd h4 {
    color: #4f4f4f;
    text-align: center;
  }
</style>
