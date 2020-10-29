<template>
  <div class="row">
    <div id="hr1"></div>
    <div id="hr2"></div>
    <div id="hr3"></div>
  </div>
</template>
<script>
import TRTC from "trtc-js-sdk";

export default {
  data() {
    return {
      videoArray: ["hr1", "hr2", "hr3"],
    };
  },
  created() {
    this.initLiveConfig();
  },
  methods: {
    //初始化直播配置
    initLiveConfig() {
      //1、创建客户端
      var client = TRTC.createClient(this.loadLiveConfig());
      
      //2、订阅远端流
      client.on("stream-added", (event) => {
        const remoteStream = event.stream;
        console.log("远端流增加: " + remoteStream.getId());
        //订阅远端流
        client.subscribe(remoteStream);
      });
      client.on("stream-subscribed", (event) => {
        const remoteStream = event.stream;
        console.log("远端流订阅成功：" + remoteStream.getId());
        // 播放远端流
        remoteStream.play(this.getElementIdByStreamId(remoteStream.getId()));
      });
      //3、进入直播间
      this.joinRoom(client, "1101564");
    },
    //加载直播间配置
    loadLiveConfig() {
      return {
        mode: "live",
        sdkAppId: 1400420278,
        userId: "2_0f0e0413d66e5129",
        userSig:"eJw1jlELgjAYRf-LXgu7m3NNoScxCnrLCH2JZJ8ywhAnlkb-Pcl6vOdw4L5Yejh69GxsSyxSkBpYfllPLYuY8MDm7czt2jTWsIhLQAqItZ6NNXTvbGnn4IISBMl9oxQFXIT-3laTDrOVSLDNd9UjiQGjhqGVJ7dwme-IIR6ysR7PaV70*80v7Gw9XeMKvlaBDoP3B-YUM4M_",
      };
    },
    //通过流ID获取放置的播放器位置
    getElementIdByStreamId(streamId) {
      console.log("getElementIdByStreamId" + streamId)
      return this.videoArray[0];
    },
    //进入房间
    joinRoom(client, roomId) {
      //清除之前的播放TODO
      // 以观众角色进房收看
      client
        .join({ roomId, role: "audience" })
        .catch((error) => {
          console.error("进房失败 " + error);
        })
        .then(() => {
          console.log("进房成功");
        });
    },
  },
};
</script>
<style scoped>
  .row{
    width:100%;
    display:flex;
    height:400px;
    border:1px solid grey;
  }
  #hr1{
    flex:1;
    height:100%;
    border:1px solid green;
  }
  #hr2{
    flex:1;
    height:100%;
    border:1px solid green;
  }
  #hr3{
    flex:1;
    height:100%;
    border:1px solid green;
  }
</style>