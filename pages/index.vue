<template>
  <div>
    <div>
      <div class="bg_box">
        <img :src="bg_img" alt="" class="bg_img" />

        <div class="bg_img_box">
          <img src="../static/bg/img_wenan_cn.png" alt="" class="bg_img_title" />
        </div>
      </div>
      <!-- title -->
      <div class="title_list_box">
        <div class="title_list">
          <div class="title_list_boder_l">
            <!-- <div class="title_icon_new">
              <span class="title_icon_text">{{ $t("a1") }}</span>
            </div> -->
            <div class="taiji_des">
              <p>
                {{ $t("a2") }}
              </p>
              <br />
            </div>
          </div>
        </div>

        <div class="top_bar_box">
          <div class="top_bar_size"></div>
          <div class="top_bar_size"></div>
        </div>
        <!-- 宝剑锻制技艺 -->
        <div class="title_list img_zs1_body">
          <div class="title_list_boder_l">
            <div class="title_icon_new">
              <img src="../static/bg/img_title_bg.png" alt="" />
              <span class="title_icon_text">{{ $t("d2") }}</span>
            </div>
            <div>
              <div class="video_list">
                <div class="taiji_des_two">
                  {{ $t("a3") }}
                </div>
                <div v-for="(item, index) in topvideos" :key="item.key">
                  <div class="items_boxs_top">
                    <video-player
                      @play="onPlayerPlay($event, item.key)"
                      class="video-player vjs-custom-skin vjs-big-play-centered"
                      ref="videoPlayer"
                      :playsinline="true"
                      :options="topvideosOptions[index]"
                    ></video-player>
                  </div>
                </div>
              </div>
              <div class="video_list video_list_last">
                <div v-for="(item, index) in middle" :key="item.key">
                  <div class="items_boxs_top">
                    <video-player
                      @play="onPlayerPlay($event, item.key)"
                      class="video-player vjs-custom-skin vjs-big-play-centered"
                      ref="videoPlayer"
                      :playsinline="true"
                      :options="middlevideosOptions[index]"
                    ></video-player>
                  </div>
                </div>
                <!-- <div class="taiji_des_two">
                  <p>
                    太极拳三式是初级养生入门功法，运用了太极推手和实战技法，快之，一招制敌，
                    慢行，修身养性，短短三分钟化繁为简，使初学者可以快速入门。
                  </p>
                  <br />
                </div> -->
              </div>
            </div>
          </div>

          <img src="../static/imgs/img_zs1.png" alt="" class="img_zs1" />
        </div>

        <!-- 青瓷烧制技艺 -->
        <div class="title_list img_zs2_body">
          <div class="title_list_boder_l">
            <div class="title_icon_new">
              <img src="../static/bg/img_title_bg.png" alt="" />
              <span class="title_icon_text">{{ $t("c1") }}</span>
            </div>
            <div class="video_list">
              <div class="taiji_des_two">
                {{ $t("c2") }}
                <!-- <p>
                  太极拳三式是初级养生入门功法，运用了太极推手和实战技法，快之，一招制敌，
                  慢行，修身养性，短短三分钟化繁为简，使初学者可以快速入门。
                </p> -->
                <br />
              </div>
              <div v-for="(item, index) in videos" :key="item.key">
                <div class="items_boxs_top">
                  <video-player
                    @play="onPlayerPlay($event, item.key)"
                    class="video-player vjs-custom-skin vjs-big-play-centered"
                    ref="videoPlayer"
                    :playsinline="true"
                    :options="playerOptions[index]"
                  ></video-player>
                </div>
              </div>
            </div>
            <!-- <img src="../static/imgs/img_zs2.png" alt="" class="img_zs2" /> -->
            <img src="../static/imgs/img_zs3.png" alt="" class="img_zs3" />
          </div>
        </div>

        <!-- 灵芝栽培技术 -->
        <div class="title_list img_zs2_body">
          <div class="title_list_boder_l">
            <div class="title_icon_new">
              <img src="../static/bg/img_title_bg.png" alt="" />
              <span class="title_icon_text_last">{{ $t("d3") }}</span>
            </div>
            <div class="video_list">
              <div class="taiji_des_two">
                {{ $t("d4") }}
              </div>
              <div v-for="(item, index) in buttoms" :key="item.key">
                <div class="items_boxs_top">
                  <video-player
                    @play="onPlayerPlay($event, item.key)"
                    class="video-player vjs-custom-skin vjs-big-play-centered"
                    ref="videoPlayer"
                    :playsinline="true"
                    :options="buttomvideosOptions[index]"
                  ></video-player>
                </div>
              </div>
            </div>
            <!-- <img src="../static/imgs/img_zs2.png" alt="" class="img_zs2" />
            <img src="../static/imgs/img_zs3.png" alt="" class="img_zs3" /> -->
          </div>
        </div>
        <div class="buttom_img_view">
          <img src="../static/imgs/img_logo.png" alt="" class="buttom_logo" />
        </div>
      </div>
      <!--  -->
    </div>
  </div>
</template>

<script>
import "video.js/dist/video-js.min.css";

import { videoPlayer } from "vue-video-player";
import getVideoInfo from "../data/getVideoInfo";
export default {
  components: {
    videoPlayer,
  },
  computed: {
    player() {
      return this.$refs.videoPlayer.player;
    },
  },
  head() {
    return {
      title: this.$t("title"),
    };
  },
  data() {
    return {
      playerOptions: [],
      topvideosOptions: [],
      buttomvideosOptions: [],
      middlevideosOptions: [],
      bg_img: "",
      topvideos: [],
      middle: [],
      buttoms: [],
      videos: [],
    };
  },

  created() {
    let data = getVideoInfo.data.filter((items) => items.lang === this.$i18n.locale);

    (this.bg_img = data[0]?.bg), (this.topvideos = [data[0].video[0]]);
    this.initTopVideo();
    this.middle = [data[0].video[1]];
    this.middleVideo();

    this.videos = [data[0].video[2], data[0].video[3], data[0].video[4]];
    this.initVideo();
    this.buttoms = [data[0].video[5]];

    this.buttomVideo();
    console.log(this.$i18n.locale, "=================当前语言===================");
  },
  methods: {
    showLocales() {
      return this.$i18n.locales.filter((locale) => locale.code !== this.$i18n.locale);
    },
    onPlayerPlay(player, index) {
      var that = this.$refs.videoPlayer;
      for (let i = 0; i < that.length; i++) {
        if (i != index) that[i].player.pause();
      }
    },
    initTopVideo() {
      for (let i of this.topvideos) {
        let config = {
          playbackRates: [1.0, 2.0, 3.0], //播放速度
          autoplay: false, //如果true,浏览器准备好时开始回放。
          muted: false, // 默认情况下将会消除任何音频。
          loop: false, // 导致视频一结束就重新开始。
          preload: "none", // 建议浏览器在<video>加载元素后是否应该开始下载视频数据。auto浏览器选择最佳行为,立即开始加载视频（如果浏览器支持）
          language: "zh-CN",
          aspectRatio: "16:9", // 将播放器置于流畅模式，并在计算播放器的动态大小时使用该值。值应该代表一个比例 - 用冒号分隔的两个数字（例如"16:9"或"4:3"）
          fluid: true, // 当true时，Video.js player将拥有流体大小。换句话说，它将按比例缩放以适应其容器。
          sources: [
            {
              type: "video/mp4",
              src: i.local, //url地址
            },
          ],
          poster: i.cover, //封面地址
          notSupportedMessage: "此视频暂无法播放，请稍后再试", //允许覆盖Video.js无法播放媒体源时显示的默认信息。
          controlBar: {
            timeDivider: true,
            durationDisplay: true,
            remainingTimeDisplay: false,
            fullscreenToggle: true, //全屏按钮
          },
        };
        this.topvideosOptions.push(config);
      }
    },
    buttomVideo() {
      for (let i of this.buttoms) {
        let config = {
          playbackRates: [1.0, 2.0, 3.0], //播放速度
          autoplay: false, //如果true,浏览器准备好时开始回放。
          muted: false, // 默认情况下将会消除任何音频。
          loop: false, // 导致视频一结束就重新开始。
          preload: "none", // 建议浏览器在<video>加载元素后是否应该开始下载视频数据。auto浏览器选择最佳行为,立即开始加载视频（如果浏览器支持）
          language: "zh-CN",
          aspectRatio: "16:9", // 将播放器置于流畅模式，并在计算播放器的动态大小时使用该值。值应该代表一个比例 - 用冒号分隔的两个数字（例如"16:9"或"4:3"）
          fluid: true, // 当true时，Video.js player将拥有流体大小。换句话说，它将按比例缩放以适应其容器。
          sources: [
            {
              type: "video/mp4",
              src: i.local, //url地址
            },
          ],
          poster: i.cover, //封面地址
          notSupportedMessage: "此视频暂无法播放，请稍后再试", //允许覆盖Video.js无法播放媒体源时显示的默认信息。
          controlBar: {
            timeDivider: true,
            durationDisplay: true,
            remainingTimeDisplay: false,
            fullscreenToggle: true, //全屏按钮
          },
        };
        this.buttomvideosOptions.push(config);
      }
    },
    middleVideo() {
      for (let i of this.middle) {
        let config = {
          playbackRates: [1.0, 2.0, 3.0], //播放速度
          autoplay: false, //如果true,浏览器准备好时开始回放。
          muted: false, // 默认情况下将会消除任何音频。
          loop: false, // 导致视频一结束就重新开始。
          preload: "none", // 建议浏览器在<video>加载元素后是否应该开始下载视频数据。auto浏览器选择最佳行为,立即开始加载视频（如果浏览器支持）
          language: "zh-CN",
          aspectRatio: "16:9", // 将播放器置于流畅模式，并在计算播放器的动态大小时使用该值。值应该代表一个比例 - 用冒号分隔的两个数字（例如"16:9"或"4:3"）
          fluid: true, // 当true时，Video.js player将拥有流体大小。换句话说，它将按比例缩放以适应其容器。
          sources: [
            {
              type: "video/mp4",
              src: i.local, //url地址
            },
          ],
          poster: i.cover, //封面地址
          notSupportedMessage: "此视频暂无法播放，请稍后再试", //允许覆盖Video.js无法播放媒体源时显示的默认信息。
          controlBar: {
            timeDivider: true,
            durationDisplay: true,
            remainingTimeDisplay: false,
            fullscreenToggle: true, //全屏按钮
          },
        };
        this.middlevideosOptions.push(config);
      }
    },
    initVideo() {
      for (let i of this.videos) {
        let config = {
          playbackRates: [1.0, 2.0, 3.0], //播放速度
          autoplay: false, //如果true,浏览器准备好时开始回放。
          muted: false, // 默认情况下将会消除任何音频。
          loop: false, // 导致视频一结束就重新开始。
          preload: "none", // 建议浏览器在<video>加载元素后是否应该开始下载视频数据。auto浏览器选择最佳行为,立即开始加载视频（如果浏览器支持）
          language: "zh-CN",
          aspectRatio: "16:9", // 将播放器置于流畅模式，并在计算播放器的动态大小时使用该值。值应该代表一个比例 - 用冒号分隔的两个数字（例如"16:9"或"4:3"）
          fluid: true, // 当true时，Video.js player将拥有流体大小。换句话说，它将按比例缩放以适应其容器。
          sources: [
            {
              type: "video/mp4",
              src: i.local, //url地址
            },
          ],
          poster: i.cover, //封面地址
          notSupportedMessage: "此视频暂无法播放，请稍后再试", //允许覆盖Video.js无法播放媒体源时显示的默认信息。
          controlBar: {
            timeDivider: true,
            durationDisplay: true,
            remainingTimeDisplay: false,
            fullscreenToggle: true, //全屏按钮
          },
        };
        this.playerOptions.push(config);
      }
    },
  },
};
</script>
<style>
@media only screen and (min-width: 1200px) {
  body {
    width: 40%;
    margin: 0 auto;
    background: #beeaf1;
    background-size: cover;
  }
  .title_icon_text_last {
    max-width: 100% !important;
  }
}

body {
  background: #ceedef;
}
.img_zs1_body {
  position: relative;
  margin-bottom: 180px !important;
}

.top_bar::after {
  content: "222";
}

.bg_box {
  position: relative;
  min-height: 400px;
}

.bg_img_box {
  z-index: 1000;
  width: 100%;
  left: 0px;
  justify-content: center;
  display: flex;
  right: 0px;
  top: 250px;
  position: absolute;
}
.bg_img_title {
  width: 90%;
  height: 100%;
}
.img_zs2_body {
  position: relative;
}

.img_zs1 {
  width: 668px;
  height: 860px;
  position: absolute;
  left: -50px;
  bottom: -200px;
  z-index: -1;
}
.img_zs2 {
  width: 111px;
  height: 233px;
  position: absolute;
  left: -60px;
  top: -140px;
}
.img_zs3 {
  position: absolute;
  width: 400px;
  height: 660px;
  right: -50px;
  bottom: -210px;
  z-index: -1;
}
.bg_img {
  width: 100%;
  height: 100%;
  position: relative;
  margin-bottom: -28%;
  z-index: -1;
  position: relative;
}
.title_list_box {
  background: linear-gradient(180deg, #77bfcb 0%, #4fabbb 100%);
  overflow: hidden;
}
.video_list_last {
  margin-top: 0px !important;
}

.title_list:first-child {
  margin-bottom: 0px !important;
}

.top_bar_box {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  margin: 0px 100px;
}
.top_bar_size {
  width: 20px;
  height: 100px;
  background: #64a8b7;
  z-index: 999;
}
.title_list {
  border-radius: 36px;
  background: #dbf2f5;
  border: 6px solid #dbf2f5;
  margin: 0px 30px;
  margin-bottom: 100px;
  display: flex;
  justify-content: center;
  z-index: 1;
}

.title_list_boder_l {
  margin: 10px;
  display: flex;
  justify-content: center;
  border-radius: 22px;
  border: 5px solid #7eb5c4;
  width: 100%;
  left: 0;
  right: 0;
  bottom: 0;
  top: 0;
  position: relative;
  background: #f0fdff;
}
.title_icon {
  width: 773px;
  height: 128px;
  position: absolute;
  top: -78px;
}

.title_icon_new {
  top: -40px;
  width: 100%;
  z-index: 888;
  left: 0px;
  right: 0px;
  height: 150px;
  position: absolute;
  flex-direction: column;
  display: flex;
  align-items: center;
  justify-content: center;
}
.title_icon_new img {
  width: 85%;
  height: 100%;
}

.title_icon_text {
  position: absolute;
  font-weight: 600;
  font-size: 42px;
  color: #043b46;
  text-align: center;
  display: block;
  top: 50%;
  margin-top: -42px;
  word-break: break-all;
}

.title_icon_text_last {
  position: absolute;
  font-weight: 600;
  font-size: 42px;
  color: #043b46;
  text-align: center;
  display: block;
  top: 50%;
  margin-top: -42px;
  width: 75%;
}
.taiji_des {
  margin-top: 60px;
  padding: 0px 10px;
}

.taiji_des_two {
  margin-top: 0px;
  padding: 0px 10px;
}
.taiji_des_two,
.taiji_des p {
  line-height: 63px;
  font-size: 40px;
  font-weight: normal;
  color: #043b46;
  margin: 40px 32px;
  text-align: justify;
  text-indent: 60px;
  word-break: normal;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
}
.items_boxs_top {
  border-radius: 12px;
  transform: rotate(0deg);
  overflow: hidden;
  margin-bottom: 32px;
  margin-left: 48px;
  margin-right: 48px;
  margin-top: 20px;
}

.video_list {
  display: flex;
  flex-direction: column;
  flex: 1;
  padding-bottom: 30px;
  margin-top: 100px;
}
.icon_size {
  margin: 0 120px;
  position: relative;
  align-items: center;
  justify-content: center;
  display: flex;
  flex-wrap: wrap;
}
.icon_text {
  position: absolute;
  font-size: 38px;
  overflow: hidden;
  font-weight: 500;
  color: #ffffff;
  padding: 0px 20px;
  text-align: center;
}
.icon_size img {
  width: 100%;
}
.buttom_logo {
  width: 100%;
}
.buttom_img_view {
  font-size: 0;
}
/*播放按钮设置成宽高一致，圆形，居中*/
.vjs-custom-skin > .video-js .vjs-big-play-button {
  background-color: rgba(0, 0, 0, 0.45);
  font-size: 1.5em;
  border-radius: 50%;
  height: 2em !important;
  line-height: 2em !important;
  margin-top: -1em !important;
  margin-left: -1em !important;
  width: 2em !important;
  outline: none;
}

.video-js .vjs-big-play-button .vjs-icon-placeholder:before {
  position: absolute;
  left: 0;
  width: 100%;
  height: 100%;
}

/*control-bar布局时flex，通过order调整剩余时间的位置到进度条右边*/
.vjs-custom-skin > .video-js .vjs-control-bar .vjs-remaining-time {
  order: 3 !important;
}

/*进度条背景轨道*/
.video-js .vjs-slider {
  border-radius: 1em;
}

/*进度条进度*/
.vjs-custom-skin > .video-js .vjs-play-progress,
.vjs-custom-skin > .video-js .vjs-volume-level {
  border-radius: 1em;
}

/*鼠标进入播放器后，播放按钮颜色会变*/
.video-js:hover .vjs-big-play-button,
.vjs-custom-skin > .video-js .vjs-big-play-button:active,
.vjs-custom-skin > .video-js .vjs-big-play-button:focus {
  background-color: rgba(0, 0, 0, 0.4) !important;
}

/*control bar*/
.video-js .vjs-control-bar {
  background-color: rgba(0, 0, 0, 0.2) !important;
}

/*点击按钮时不显示蓝色边框*/
.video-js .vjs-control-bar button {
  outline: none;
}
.video-js {
  background: #fff;
}
.vjs-poster {
  background-size: cover !important;
  background-repeat: inherit !important;
}
video {
  width: 100% !important;
  object-fit: fill;
}
</style>
