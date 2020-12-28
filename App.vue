<!--
所谓的 vue 单文件就是把 HTML JavaScript CSS 这三个东西写在一个文件
官方描述的优势如下 
https://cn.vuejs.org/v2/guide/single-file-components.html

从实际的使用中来看，这个方式的缺陷也很大
因为把 HTML JavaScript CSS 三个东西混合在一起
所以很轻松就能写出几千行甚至上万行的代码

有一个常见的笑话是 “没有一万行好意思叫 vue 组件？”
这不仅是笑话，也是一个普遍存在的事实
希望你在以后，既不用倒霉去到这样的项目组工作，也别写出这种难以维护的代码


简单来说，下面的代码内容分 3 块
    template 里面写 HTML 代码
    script 里面写 JavaScript 代码
    style 里面写 CSS 代码
-->
<template>
    <div>
        <div>
            <div v-if="show"
                 class="modal-container"
            >
                <div class="modal-mask"></div>
                <div class="modal-alert vertical-center">
                    <input class="input" v-model="titles" placeholder="标题">
                    <input v-model="contexts"
                        class="input" placeholder="内容区">
                    <div v-on:click="AlertQuit"
                        id="id-button-cancel" class="radio-button">
                      取消
                    </div>
                    <div v-on:click="Alert"
                        id="id-button-quit" class="radio-button">
                      完成
                    </div>
                </div>

            </div>
            <span
                  v-on:click="__main()"
                  class="radio-button">
                  弹窗生成
            </span>
            <h3>标题：{{title}}</h3>
            <h3>内容：{{context}}</h3>
          </div>
    </div>

</template>


<script>
    // export default 这是规定的写法
    export default {
        data: function() {
            return {
                show: false,
                activeIndex: 0,
                title:[],
                context:[],
                titles:[],
                contexts:[],
            }
        },
        methods: {
          AlertQuit: function() {
              this.contexts = this.context
              this.titles = this.title
              this.show = false
          },

          Alert: function() {
            this.context = this.contexts
            this.title = this.titles
            this.show = false
          },

          edit_title: function(text) {
              this.title = text
          },

          edit_text: function(text) {
              this.context = text
          },

          __main: function() {
               this.show = true
          }

        }
    }

</script>


<style>
    .radio-button {
        display: inline-block;
        text-align: center;
        padding: 10px;
        margin: 5px;
        cursor: pointer;
        background: lightcyan;
    }

    .active {
        background: lightyellow;
    }

    .modal-container {
      position: fixed;
      top: 0px;
      left: 0px;
      width: 100%;
      height: 100%;
    }

    .modal-mask {
      position: fixed;
      top: 0px;
      left: 0px;
      width: 100%;
      height: 100%;
      background: black;
      opacity: 0.5;
    }

    .modal-alert {
      margin: 0 auto;
      width: 200px;
      opacity: 1;
    }

    .vertical-center {
      top: 50%;
      position: relative;
      transform: translateY(-50%);
    }

    .title {
      background: lightcyan;
      width: 150px;
      height: 30px;
      text-align: center;
    }

    .input {
      background: aliceblue;
      width: 150px;
      height: 40px;
      text-align: center;
    }
</style>
