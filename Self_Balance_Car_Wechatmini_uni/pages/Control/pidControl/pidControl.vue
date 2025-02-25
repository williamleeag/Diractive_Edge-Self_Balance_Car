<template>
  <view class="container">
    <view class="pid-control">
      <view class="pid-slider" v-for="(param, index) in pidParams" :key="index">
        <view class="label-wrapper">
          <text class="label-text">{{ param.label }} ({{ param.value }}):</text>
        </view>
        <view class="slider-wrapper">
          <button class="round-button small-button" @tap="decreaseParam(param.name)">-</button>
          <slider
            class="short-slider"
            :step="param.step"
            :min="MIN"
            :max="param.max"
            v-model="param.value"
            @changing="onSliderChange(param.name, $event)"
          />
          <button class="round-button small-button" @tap="increaseParam(param.name)">+</button>
        </view>
      </view>
      <view class="button-wrapper">
        <button class="round-button" @tap="savePIDSettings">Confirm</button>
        <button class="round-button" @tap="revertSettings">Revert</button>
        <button class="round-button" @tap="saveAsDefaultConfiguration">Save Config</button>
      </view>
      <view class="button-wrapper">
        <button class="round-button" v-for="(config, index) in configurations" :key="index" @tap="switchConfiguration(index)">
          Config {{ index + 1 }}
        </button>
      </view>
    </view>
  </view>
</template>

<script>
const BLE_util = require('../../../utils/BLE_util');
export default {
  data() {
    return {
      balanceKp: 213,
      balanceKi: 0,
      balanceKd: 2.55,
      velocityKp: 2,
      velocityKi: 0.01,
      velocityKd: 0,
      MIN: 0,
      MAX_B_P: 720,
      MAX_B_I: 20,
      MAX_B_D: 3.6,
      MAX_V_P: 2.88,
      MAX_V_I: 0.0144,
      MAX_V_D: 20,
      STEP_B_P: 1,
      STEP_B_I: 0.1,
      STEP_B_D: 0.01,
      STEP_V_P: 0.01,
      STEP_V_I: 0.0001,
      STEP_V_D: 0.1,
      defaultPIDSettings: {
        balanceKp: 213,
        balanceKi: 0,
        balanceKd: 2.55,
        velocityKp: 2,
        velocityKi: 0.01,
        velocityKd: 0,
      },
      configurations: [
        {
          balanceKp: 213,
          balanceKi: 0,
          balanceKd: 2.55,
          velocityKp: 2,
          velocityKi: 0.01,
          velocityKd: 0,
        },
        {
          balanceKp: 213,
          balanceKi: 0,
          balanceKd: 2.55,
          velocityKp: 2,
          velocityKi: 0.01,
          velocityKd: 0,
        },
        {
          balanceKp: 213,
          balanceKi: 0,
          balanceKd: 2.55,
          velocityKp: 2,
          velocityKi: 0.01,
          velocityKd: 0,
        },
      ],
      pidParams: [
        { label: 'BalanceKp', value: 213, step: 1, max: 720, name: 'balanceKp' },
        { label: 'BalanceKi', value: 0, step: 0.1, max: 20, name: 'balanceKi' },
        { label: 'BalanceKd', value: 2.55, step: 0.01, max: 3.6, name: 'balanceKd' },
        { label: 'VelocityKp', value: 2, step: 0.01, max: 2.88, name: 'velocityKp' },
        { label: 'VelocityKi', value: 0.01, step: 0.0001, max: 0.0144, name: 'velocityKi' },
        { label: 'VelocityKd', value: 0, step: 0.1, max: 20, name: 'velocityKd' }
      ],
      previousSettings: {}
    };
  },
  mounted() {
    const pidSettings = uni.getStorageSync('pidSettings');
    if (pidSettings) {
      this.balanceKp = pidSettings.balanceKp;
      this.balanceKi = pidSettings.balanceKi;
      this.balanceKd = pidSettings.balanceKd;
      this.velocityKp = pidSettings.velocityKp;
      this.velocityKi = pidSettings.velocityKi;
      this.velocityKd = pidSettings.velocityKd;
  
      this.updatePidParams();
    }
  
    const savedConfigurations = uni.getStorageSync('configurations');
    if (savedConfigurations) {
      this.configurations = savedConfigurations;
    }
  },
  methods: {
    updatePidParams() {
      this.pidParams = [
        { label: 'BalanceKp', value: this.balanceKp, step: 1, max: 720, name: 'balanceKp' },
        { label: 'BalanceKi', value: this.balanceKi, step: 0.1, max: 20, name: 'balanceKi' },
        { label: 'BalanceKd', value: this.balanceKd, step: 0.01, max: 3.6, name: 'balanceKd' },
        { label: 'VelocityKp', value: this.velocityKp, step: 0.01, max: 2.88, name: 'velocityKp' },
        { label: 'VelocityKi', value: this.velocityKi, step: 0.0001, max: 0.0144, name: 'velocityKi' },
        { label: 'VelocityKd', value: this.velocityKd, step: 0.1, max: 20, name: 'velocityKd' }
      ];
    },
    onSliderChange(param, event) {
      const value = parseFloat(event.detail.value.toFixed(4));
      this[param] = value;
      this.updatePidParams();
    },
    increaseParam(param) {
      const step = this.getStep(param);
      this[param] = parseFloat((this[param] + step).toFixed(4));
      this.updatePidParams();
    },
    decreaseParam(param) {
      const step = this.getStep(param);
      this[param] = parseFloat((this[param] - step).toFixed(4));
      this.updatePidParams();
    },
    getStep(param) {
      const steps = {
        balanceKp: this.STEP_B_P,
        balanceKi: this.STEP_B_I,
        balanceKd: this.STEP_B_D,
        velocityKp: this.STEP_V_P,
        velocityKi: this.STEP_V_I,
        velocityKd: this.STEP_V_D
      };
      return steps[param] || 1;
    },
    savePIDSettings() {
      const pidSettings = {
        balancePID: {
          Kp: this.balanceKp,
          Ki: this.balanceKi,
          Kd: this.balanceKd
        },
        velocityPID: {
          Kp: this.velocityKp,
          Ki: this.velocityKi,
          Kd: this.velocityKd
        }
      };
      console.log('Saving PID Settings:', pidSettings);

      BLE_util.Write_data_BLE({
        Type: 'PID',
        balancePID: pidSettings.balancePID,
        velocityPID: pidSettings.velocityPID
      })
        .then((res) => {
          console.log('PID settings sent successfully:', res);
        })
        .catch((err) => {
          console.error('Error sending PID settings:', err);
        });

      uni.setStorageSync('pidSettings', {
        balanceKp: this.balanceKp,
        balanceKi: this.balanceKi,
        balanceKd: this.balanceKd,
        velocityKp: this.velocityKp,
        velocityKi: this.velocityKi,
        velocityKd: this.velocityKd
      });
    },
    revertSettings() {
      const pidSettings = uni.getStorageSync('pidSettings');
      if (pidSettings) {
        this.balanceKp = pidSettings.balanceKp;
        this.balanceKi = pidSettings.balanceKi;
        this.balanceKd = pidSettings.balanceKd;
        this.velocityKp = pidSettings.velocityKp;
        this.velocityKi = pidSettings.velocityKi;
        this.velocityKd = pidSettings.velocityKd;

        this.updatePidParams();
      }
    },
    saveAsDefaultConfiguration() {
      uni.showActionSheet({
        itemList: ['Config 1', 'Config 2', 'Config 3'],
        success: (res) => {
          const index = res.tapIndex;
          if (index >= 0 && index < this.configurations.length) {
            this.configurations[index] = {
              balanceKp: this.balanceKp,
              balanceKi: this.balanceKi,
              balanceKd: this.balanceKd,
              velocityKp: this.velocityKp,
              velocityKi: this.velocityKi,
              velocityKd: this.velocityKd
            };
            uni.setStorageSync('configurations', this.configurations);
            uni.showToast({
              title: `Config ${index + 1} saved`,
              icon: 'success',
              duration: 2000
            });
          }
        },
        fail: (res) => {
          console.log(res.errMsg);
        }
      });
    },
    switchConfiguration(index) {
      if (index >= 0 && index < this.configurations.length) {
        const config = this.configurations[index];
        this.balanceKp = config.balanceKp;
        this.balanceKi = config.balanceKi;
        this.balanceKd = config.balanceKd;
        this.velocityKp = config.velocityKp;
        this.velocityKi = config.velocityKi;
        this.velocityKd = config.velocityKd;

        this.updatePidParams();
        uni.showToast({
          title: `Switched to Config ${index + 1}`,
          icon: 'success',
          duration: 2000
        });
      }
    }
  }
};
</script>

<style>
/* pages/Control/pid/pidControl.js.wxss */
.short-slider {
  margin-left: 8%;
  margin-right: 8%;
  flex: 1;
}

.slider-wrapper {
  display: flex;
  align-items: center;
}

.label-wrapper {
  width: 100%;
  display: flex;
  justify-content: space-between;
}

.label-text {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}


.button-wrapper {
  display: flex;
  justify-content: space-around;
  margin-top: 20px;
}
.round-button {
  background-color: #4CAF50;
  border: none;
  color: white;
  padding: 10px 24px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  border-radius: 12px;
}

.small-button {
  padding: 5px 12px;
  font-size: 14px;
}

</style>
