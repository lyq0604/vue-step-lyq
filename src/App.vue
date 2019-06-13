<template>
  <div id="app">
    <!--<router-view/>-->
    <horizontal-stepper :steps="demoSteps" :showInterval="true" :currentIndex="4"/>
  </div>
</template>

<script>
import HorizontalStepper from '@/components/step/HorizontalStepper'
export default {
  name: 'App',
  components: {
    HorizontalStepper
  },
  data() {
    return {
      demoSteps: [
        {
          title: '提交流程',
          date: new Date().toDateString(),
          interval: 1
        },
        {
          title: '室主任审批',
          date: new Date().toDateString(),
          interval: 2
        },
        {
          title: '直属领导审批',
          interval: 3
        },
        {
          title: '所长审批',
          interval: 2
        },
        {
          title: '提交流程',
          date: new Date().toDateString(),
          interval: 1
        },
        {
          title: '室主任审批',
          date: new Date().toDateString(),
          interval: 2
        },
        {
          title: '直属领导审批',
          interval: 3
        },
        {
          title: '所长审批',
          interval: 2
        }
      ],
      activeStep: 0
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
