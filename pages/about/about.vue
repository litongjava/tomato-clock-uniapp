<template>
  <view class="container">
    <text class="link">关于作者: https://github.com/litongjava</text>
    <text></text>
    <view class="description">
      <text class="title">番茄工作法（Pomodoro Technique）</text>
      <text>  番茄工作法（Pomodoro Technique）是一种流行的时间管理方法，由弗朗切斯科·西里洛（Francesco Cirillo）在 1980 年代末发明。这种方法的基本结构如下：</text>
      <!-- 描述内容 -->
      <view class="list">
        <text>1. 工作时间：选择一个任务，设置一个定时器为 25 分钟，这个 25 分钟的时间段被称为一个“番茄”</text>
        <text></text>
        <text>2. 短休息：完成一个“番茄”后，休息 5 分钟。</text>
        <text></text>
        <text>3. 重复：继续工作下一个“番茄”，然后再休息 5 分钟。重复这个过程。</text>
        <text></text>
        <text>4. 长休息：完成四个“番茄”后，休息更长的时间，通常是 15-30 分钟。</text>     
      </view>
      <text>这些时间长度不是严格的规则，可以根据个人的工作习惯...</text>
      <!-- 其他描述内容 -->
    </view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        
      }
    },
    methods: {
      
    }
  }
</script>

<style>
.container {
  padding: 20rpx;
}
.link {
  color: #007aff;
}
.title {
  font-weight: bold;
}
.list text {
  display: block;
  margin: 10rpx 0;
}
</style>






