<template>
  <div class="Report">
    <BaseHeader>
      <template v-slot:center>
         <span class="f16">
          <template v-if="mode === 'video'">视频</template>
          <template v-if="mode === 'music'">音乐</template>
          <template v-if="mode === 'chat'">私信</template>举报</span>
      </template>
    </BaseHeader>
    <div class="content">
      <div class="title">
        <span>你的举报将在12小时内受理，若举报成功会第一时间告知处理结果，请尽量提交完整的举报描述及材料</span>
      </div>
      <div class="row">
        <span>
          举报理由：{{ type }}
        </span>
      </div>
      <div class="l-row">
        <div class="notice">举报描述(选填)</div>
        <div class="textarea-ctn">
          <textarea name="" id="" cols="30" rows="10"
                    v-model="desc"
                    placeholder="详细描述举报理由"></textarea>
        </div>
        <div class="text-num">{{ desc.length }}/200</div>
      </div>
      <div class="upload-photo">
        <div class="photo-wrapper" v-for="(item,index) in photos">
          <img class="photo" :src="item" alt="">
          <img class="close" src="../../assets/img/icon/components/light-close.png" alt="" @click="photos.pop()">
        </div>
        <div class="upload" @click="upload" v-if="photos.length !== 4">
          <img src="../../assets/img/icon/home/camera-gray.png" alt="">
          <span>{{ photos.length }}/4</span>
        </div>
      </div>

      <dy-button type="primary" @click="$no">提交</dy-button>
    </div>
  </div>
</template>
<script>
export default {
  name: "Report",
  props: {},
  data() {
    return {
      type: '色情低俗',
      mode: 'video',
      desc: '',
      photos: []
    }
  },
  computed: {},
  created() {
    this.type = this.$route.query.type
    this.mode = this.$route.query.mode
  },
  methods: {
    async upload() {
      this.$showLoading()
      await this.$sleep(500)
      this.$hideLoading()
      this.photos.push(
          new URL(`../../assets/img/poster/${this.photos.length}.jpg`, import.meta.url).href,
      )

    }
  }
}
</script>

<style scoped lang="less">
@import "../../assets/less/index";

.Report {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  top: 0;
  overflow: auto;
  color: white;
  font-size: 14rem;

  .content {
    padding-top: 60rem;

    .title {
      font-size: 12rem;
      padding: 10rem 15rem;
      color: var(--second-text-color);
      border-bottom: 1px solid #cccccc11;

      img {
        width: 10rem;
        height: 10rem;
        margin-right: 2rem;
      }
    }

    .l-row {
      padding: 0 15rem;

      .textarea-ctn {
        width: 100%;
        background: var(--active-main-bg);
        padding: 15rem;
        box-sizing: border-box;
        margin-top: 10rem;
        border-radius: 2px;


        textarea {
          font-family: "Microsoft YaHei UI";
          outline: none;
          width: 100%;
          border: none;
          background: transparent;
          color: white;

          &::placeholder {
            color: var(--second-text-color);
          }
        }
      }

      .text-num {
        margin-top: 5rem;
        font-size: 10rem;
        color: var(--second-text-color);
        text-align: right;
      }
    }

    .upload-photo {
      margin-top: 5rem;
      display: flex;
      padding: 0 15rem;

      @width: calc((100vw - 3vw - 30rem) / 4);

      .photo-wrapper {
        width: @width;
        height: @width;
        position: relative;
        margin-right: 1vw;

        .photo {
          object-fit: cover;
          position: absolute;
          width: 100%;
          height: 100%;
        }

        .close {
          position: absolute;
          right: 0;
          top: 0;
          background: var(--second-btn-color);
          padding: 3rem;
          width: 10rem;
          height: 10rem;
        }
      }

      .upload {
        width: @width;
        height: @width;
        display: flex;
        flex-direction: column;
        justify-content: center;
        color: var(--second-text-color);
        font-size: 12rem;
        align-items: center;
        background: var(--second-btn-color-tran);

        img {
          width: 35rem;
          height: 35rem;
        }
      }
    }
  }

  .button {
    position: absolute;
    left: 15rem;
    right: 15rem;
    bottom: 15rem;
  }
}
</style>
