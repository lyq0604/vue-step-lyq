<template>
    <div class="stepper-box">
        <div class="top">
            <div class="divider-line" :style="{width: `${(100/(steps.length) * (steps.length - 1)) - 10}%`}"></div>
            <div class="steps-wrapper">
                <template v-for="(step, index) in steps">
                    <div :class="['step', isStepActive(index, step)]" :key="index" :style="{width: `${100 / steps.length}%`}">
                        <div class="circle">
                            {{ index+1 }}
                        </div>
                        <div class="step-title">
                            <h4>{{step.title}}</h4>
                            <h5 class="step-subtitle">{{step.date}}</h5>
                        </div>
                    </div>
                    <span v-if="showInterval && (index < (steps.length -1))" style="margin-bottom: 5vh">{{ step.interval }}</span>
                </template>
            </div>
        </div>
    </div>
</template>

<script>
import translations from './Translations.js';

export default {
  filters: {
    translate: function(value, locale) {
      return translations[locale][value];
    }
  },

  props: {
    locale: {
      type: String,
      default: 'cn'
    },
    steps: {
      type: Array,
      default: function() {
        return [
          {
            title: '标题',
            date: new Date().toDateString()
          },
          {
            title: 'Sample title 2',
            date: new Date().toDateString()
          }
        ];
      }
    },
    /**
      * 是否显示间隔
    */
    showInterval: {
      type: Boolean,
      default: true
    },
    currentIndex: {
      type: Number,
      default: 3
    }
  },

  data() {
    return {
      currentStep: {},
      previousStep: {},
      nextButton: {},
      canContinue: true,
      finalStep: false,
      keepAliveData: this.keepAlive
    }
  },

  computed: {
    enterAnimation() {
      if (this.currentStep.index < this.previousStep.index) {
        return 'animated quick fadeInLeft';
      } else {
        return 'animated quick fadeInRight';
      }
    },
    leaveAnimation() {
      if (this.currentStep.index > this.previousStep.index) {
        return 'animated quick fadeOutLeft';
      } else {
        return 'animated quick fadeOutRight';
      }
    }
  },

  methods: {
    /**
     * 判断是否当前执行步
      * @param index 索引
     * @param step
     * @returns {*}
     */
    isStepActive(index, step) {
      if (this.currentIndex === index) {
        return 'activated';
      } else if (index < this.currentIndex){
        return 'finished';
      } else {
        return 'deactivated'
      }
    }
  },
  created () {
  }
}
</script>

<style src="./HorizontalStepper.scss" scoped lang="scss">

</style>
<style scoped>
/* fallback */
@font-face {
  font-family: "Material Icons";
  font-style: normal;
  font-weight: 400;
  src: local("Material Icons"), local("MaterialIcons-Regular"),
    url(https://fonts.gstatic.com/s/materialicons/v17/2fcrYFNaTjcS6g4U3t-Y5ZjZjT5FdEJ140U2DJYC3mY.woff2)
      format("woff2");
}

.material-icons {
  font-family: "Material Icons";
  font-weight: normal;
  font-style: normal;
  font-size: 24px;
  line-height: 1;
  letter-spacing: normal;
  text-transform: none;
  display: inline-block;
  white-space: nowrap;
  word-wrap: normal;
  direction: ltr;
  -webkit-font-feature-settings: "liga";
  -webkit-font-smoothing: antialiased;
}
</style>
