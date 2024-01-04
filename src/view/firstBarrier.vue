<template>
  <div>
    <el-col v-for="(item, index) in timesArray" :key="index" :span="index === 0 ? 20 : 10 " style="margin-bottom: 20px;margin-left: 20px;
        border-color: black;border-style:dashed;
      ">
      <TimesVue :allTimes="item.value" :title="item.title"/>
    </el-col>
  </div>
</template>

<script>

import TimesVue from "@/components/times-vue.vue";

export default {
  name: 'app',
  components: {
    TimesVue
  },
  data() {
    return {
      timesArray: [
        {title: "月华", value: 60},
        {title: "樱花1", value: 50},
        {title: "樱花2", value: 50},
        {title: "樱花3", value: 50},
        {title: "樱花4", value: 50},
      ],
    }
  },
  mounted() {
  },
  methods: {

  }
}
</script>

<style scoped>

</style>