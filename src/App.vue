<template>
  <div>
    <header class="site-header jumbotron">
      <div class="container">
        <div class="row">
          <div class="col-xs-12">
            <h1>请发表对React的评论</h1>
          </div>
        </div>
      </div>
    </header>
    <div class="container">
      <!-- <Add :addComment="addComment" /> 通过props传递数据-->
      <!-- 通过自定义事件从儿子拿数据 -->
      <Add ref="add" />
      <List :comments="comments" :deleteComment="deleteComment" />
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
import Add from "./components/Add";
import List from "./components/List";
export default {
  components: {
    Add,
    List
  },
  mounted() {
    // this.$refs.add 就是组件对象
    // this.$refs.add.$on; 本质是Vue原型的方法
    // 相当于在父组件当中给子组件绑定了一个时间（自己定义的事件）
    // 特点：回调函数是在父组件当中的
    this.$refs.add.$on("addComment", this.addComment);
  },
  data() {
    return {
      comments: [
        { id: 1, username: "旺财", content: "汪汪汪" },
        { id: 2, username: "小黑", content: "嘿嘿嘿" },
        { id: 3, username: "大黄", content: "晃晃晃" }
      ]
    };
  },
  methods: {
    addComment(obj) {
      this.comments.unshift(obj);
    },
    deleteComment(index) {
      this.comments.splice(index, 1);
    }
  }
};
</script>

<style scoped>
</style>
