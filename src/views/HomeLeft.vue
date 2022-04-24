<template>
  <dv-border-box-8 class="border-box-content">
    <div class="container-item" style="display: flex; align-items: center;justify-content: space-around;">
      <div class="box-item" style="text-align: center;padding:50px">
        <p class="item">环境数据</p>
        <dv-decoration-9 style="width:130px;height:130px;color:#fff;margin: 0 auto;margin-top:20px">
          <p v-if="dataObj.public_repos>0">
            {{dataObj.public_repos}}
          </p>
          <p v-else>无</p>
        </dv-decoration-9>
      </div>
      <!-- <dv-decoration-2 style="height:5px;display: block;" /> -->
      <div class="box-item" style="text-align: center;padding:50px">
        <p class="item">气象数据</p>
        <dv-decoration-9 style="width:130px;height:130px;color:#fff;margin: 0 auto;margin-top:20px">
          <p v-if="dataObj.followers>0">
            {{dataObj.followers}}
          </p>
          <p v-else>无</p>
        </dv-decoration-9>
      </div>
      <!-- <dv-decoration-2 style="height:5px;display: block;" />
      <div class="box-item last-item">
        <p class="item">跟随</p>
        <dv-decoration-9 style="width:150px;height:150px;color:#fff">
          <p v-if="dataObj.following>0">
            {{dataObj.following}}
          </p>
          <p v-else>无</p>
        </dv-decoration-9>
      </div> -->
    </div>
  </dv-border-box-8>
</template>

<script>
export default {
  props: {
    dataObj: Object
  },
  data() {
    return {

    }
  },
  created() {
    console.log(this.dataObj)
  },
};
</script>

<style scoped lang="scss">
.container-left {
  width: 20%;
  height: 100%;
  .container-item {
    display: flex;
    // flex-direction: column;
    align-items: center;
    // justify-content: space-around;
    .box-item {
      margin-bottom: 10px;
      .item {
        color: white;
        text-align: center;
        padding-top: 10px;
      }
    }
    .last-item {
      margin-top: 20px;
      .item {
        padding-top: 5px;
      }
    }
  }
}
</style>
