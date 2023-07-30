<template>
  <view class="container">
    <view class="input-container">
      <text>工作时间（分钟）:</text>
      <input v-model="workMinutes" type="number" />
    </view>
    <view class="input-container">
      <text>休息时间（分钟）:</text>
      <input v-model="restMinutes" type="number" />
    </view>
    <view class="input-container">
      <text>长休息时间（分钟）:</text>
      <input v-model="longRestMinutes" type="number" />
    </view>
    <text>------------------------------------------</text>
    <view class="status">{{ isWorking ? '工作时间' : '休息时间' }}</view>
    <view class="timer">{{ timeLeft }}</view>
    <button @click="startTimer">开始</button>
    <button @click="stopTimer">停止</button>
    <button @click="resetTimer">重置</button>
    <button @click="playAlarmSound">播放声音测试</button>
    <button @click="goToAbout" class="about-button">关于</button>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        workMinutes: 25,
        restMinutes: 5,
        longRestMinutes: 15, // 长休息时间
        timeLeft: '25:00',
        timer: null,
        isWorking: true,
        completedTomatoes: 0, // 完成的番茄数量
        alarmSound: null // 用于存储闹钟声音的对象
      };
    },
    methods: {
      startTimer() {
        let minutes = this.isWorking ? this.workMinutes : this.restMinutes;
        // 如果完成了 4 个番茄，设置长休息时间
        if (!this.isWorking && this.completedTomatoes >= 4) {
          minutes = this.longRestMinutes;
          this.completedTomatoes = 0; // 重置番茄计数
        }
        let seconds = 0;
        this.timer = setInterval(() => {
          if (seconds === 0) {
            if (minutes === 0) {
              clearInterval(this.timer);
              this.playAlarmSound();
              this.showAlarmDialog(); // 显示对话框
              return; // 返回，等待用户响应
            }
            minutes--;
            seconds = 59;
          } else {
            seconds--;
          }
          this.timeLeft = `${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;
        }, 1000);
      },
      stopTimer() {
        clearInterval(this.timer);
      },
      resetTimer() {
        clearInterval(this.timer);
        this.timeLeft = `${String(this.workMinutes).padStart(2, '0')}:00`;
        this.isWorking = true; // 重置为工作状态
      },
      // ... 其他方法 ...
      goToAbout() {
        uni.navigateTo({
          url: '/pages/about/about'
        });
      },
      playAlarmSound() {
        if (!this.alarmSound) {
          this.alarmSound = uni.createInnerAudioContext();
          this.alarmSound.src = '/static/alarm.mp3'; // 路径需要根据你的项目结构调整
        }
        this.alarmSound.play();
      },
      stopAlarmSound() {
        if (this.alarmSound) {
          this.alarmSound.stop();
        }
        this.isWorking = !this.isWorking; // 切换工作/休息状态
        this.startTimer(); // 重新开始计时
      },
      showAlarmDialog() {
        uni.showModal({
          title: '时间到',
          content: '你的工作/休息时间到了，点击停止闹钟。',
          showCancel: false,
          confirmText: '停止播放',
          success: () => {
            this.stopAlarmSound();
          }
        });
      },
    }
  };
</script>

<style>
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 40rpx;
  }

  .input-container {
    display: flex;
    align-items: center;
    margin-bottom: 10rpx;
  }

  .status {
    font-size: 30rpx;
    color: #666;
    margin-bottom: 10rpx;
  }

  .timer {
    font-size: 60rpx;
    margin-bottom: 20rpx;
  }
</style>