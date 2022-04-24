<template>
  <div id="index" ref="appRef">
    <div class="bg">
      <dv-loading v-if="loading">Loading...</dv-loading>
      <div v-else class="host-body">
        <div class="d-flex jc-center">
          <dv-decoration-10 class="dv-dec-10" />
          <div class="d-flex jc-center">
            <dv-decoration-8 class="dv-dec-8" :color="decorationColor" />
            <div class="title">
              <span class="title-text">中国陆地生态系统碳源汇模拟平台</span>
              <dv-decoration-6 class="dv-dec-6" :reverse="true" :color="['#50e3c2', '#67a1e5']" />
            </div>
            <dv-decoration-8 class="dv-dec-8" :reverse="true" :color="decorationColor" />
          </div>
          <dv-decoration-10 class="dv-dec-10-s" />
        </div>

        <!-- 第二行 -->
        <div class="d-flex jc-between px-2">
          <div class="d-flex aside-width">
            <div class="react-left ml-4 react-l-s">
              <span class="react-left"></span>
              <!-- <span class="text">数据分析1</span> -->
            </div>
            <div class="react-left ml-3">
              <!-- <span class="text">数据分析2</span> -->
            </div>
          </div>
          <div class="d-flex aside-width">
            <div class="react-right bg-color-blue mr-3">
              <!-- <span class="text fw-b">vue-big-screen</span> -->
            </div>
            <div class="react-right mr-4 react-l-s">
              <span class="react-after"></span>
              <span class="text">{{ dateYear }} {{ dateWeek }} {{ dateDay }}</span>
            </div>
          </div>
        </div>

        <div class="body-box">
          <!-- 第三行数据 -->
          <div class="content-box">
            <div class="content_left">
              <div class="left_one">
                <HomeLeft :dataObj="dataObj" />
              </div>
              <!-- 第四行数据 -->
              <div class="left_two">
                <dv-border-box-12>
                  <bottomLeft />
                </dv-border-box-12>
                <dv-border-box-12>
                  <bottomLeft2 />
                </dv-border-box-12>
              </div>

            </div>
            <div class="content_right">
              <dv-border-box-1>
                <centerLeft2 />
              </dv-border-box-1>
            </div>

            <!-- <div class="pad"> -->
            <!-- <dv-border-box-12> -->
            <!-- <centerLeft1 /> -->

            <!-- <HomeLeft :dataObj="dataObj" /> -->
            <!-- </dv-border-box-12> -->
            <!-- </div> -->
            <!-- <div> -->
            <!-- <dv-border-box-12> -->
            <!-- <centerLeft2 /> -->
            <!-- </dv-border-box-12> -->
            <!-- </div> -->
            <!-- 中间 -->
            <!-- <div> -->
            <!-- <center /> -->
            <!-- <dv-border-box-1> -->
            <!-- <centerLeft2 /> -->
            <!-- </dv-border-box-1> -->

            <!-- </div> -->
            <!-- 中间 -->
            <!-- <div> -->
            <!-- <centerRight2 /> -->
            <!-- </div> -->
            <!-- <div class="pad"> -->
            <!-- <dv-border-box-13> -->
            <!-- <centerRight1 /> -->
            <!-- <HomeLeft :dataObj="dataObj" /> -->
            <!-- </dv-border-box-13> -->
            <!-- </div> -->
          </div>

        </div>
      </div>
    </div>
  </div>
</template>

<script>
import drawMixin from "../utils/drawMixin";
import { formatTime } from '../utils/index.js'
// import centerLeft1 from './centerLeft1'
import centerLeft2 from './centerLeft2'
// import centerRight1 from './centerRight1'
// import centerRight2 from './centerRight2'
// import center from './center'
import bottomLeft from './bottomLeft'
import bottomLeft2 from './bottomLeft2'
// import bottomRight from './bottomRight'
import HomeLeft from './HomeLeft.vue'
export default {
  mixins: [drawMixin],
  data() {
    return {
      userName: "",
      timing: null,
      loading: true,
      dateDay: null,
      dateYear: null,
      dateWeek: null,
      weekday: ['周日', '周一', '周二', '周三', '周四', '周五', '周六'],
      decorationColor: ['#568aea', '#000000'],
      dataObj: {},
    }
  },
  components: {
    // centerLeft1,
    centerLeft2,
    // centerRight1,
    // centerRight2,
    // center,
    bottomLeft,
    bottomLeft2,
    // bottomRight,
    HomeLeft,
  },
  mounted() {
    this.userName = this.$route.query.user;
    this.timeFn()
    this.cancelLoading()
    this.getUserInfo()
  },
  beforeDestroy() {
    clearInterval(this.timing)
  },
  methods: {
    getUserInfo() {
      this.$axios
        .get(`https://api.github.com/users/${this.userName}`)
        .then(res => {
          const { data } = res;
          this.dataObj = data;
        });
    },
    timeFn() {
      this.timing = setInterval(() => {
        this.dateDay = formatTime(new Date(), 'HH: mm: ss')
        this.dateYear = formatTime(new Date(), 'yyyy-MM-dd')
        this.dateWeek = this.weekday[new Date().getDay()]
      }, 1000)
    },
    cancelLoading() {
      setTimeout(() => {
        this.loading = false
      }, 500)
    }
  }
}
</script>

<style lang="scss" scoped>
@import "../assets/scss/index.scss";
.container {
  width: 100%;
  height: 100%;
  .container-wrap {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: row;
    .container-left {
      width: 20%;
      height: 100%;
    }
    .container-right {
      margin-left: 10px;
      .container-center {
        display: flex;
        flex-direction: row;
        width: 100%;
        .container-center-left {
          width: 100%;
          .tab-list {
            width: 100%;
            height: 230px;
            margin-top: 10px;
          }
        }
        .container-center-right {
          flex: 1;
        }
        .center-item {
          width: 800px;
          height: 450px;
        }
        .info {
          width: 400px;
          height: 200px;
          margin-left: 20px;
        }
        .classification {
          height: 460px;
          margin-top: 20px;
          margin-left: 20px;
        }
      }
    }
  }
}
</style>
