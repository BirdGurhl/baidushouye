<template>
  <div class='container' ref="root" @scroll="onScroll($event)">
    <div class="top-container">
      <div class="header">
        <van-icon name="user-circle-o" @click="show = true" />
        <van-icon name="apps-o" />
      </div>
      <div class="logo">
        <img :src="require('@/assets/plus_logo_web_2.png')" alt="" srcset="">
      </div>
      <div class="search-container">
        <form action="">
          <input type="text" name="" id="" placeholder="请输入关键词">
          <img :src="require('@/assets/213麦克风.png')" alt="" class="voice">
          <img :src="require('@/assets/相机.png')" alt="" class="camera">
          <van-button type="info">百度一下</van-button>
        </form>
      </div>
      <div class="divider"></div>
    </div>
    <div class="content-container">
      <div class="navs" v-show="navShow">
        <ul>
          <li v-for="(nav, index) in tabs" :class="{ active: index == active }">{{ nav }}</li>
          <li class="add">+</li>
        </ul>
      </div>
      <ul class="content">
        <li v-for="(item, index) in content" :key="index">

          <!-- 无图/三图及以上，内容纵向排列 -->
          <a v-if="item.img.length >= 3 || item.img.length == 0" href="#" class="column"
            :class="{ check: item.check, 'top-text': item.default }">
            <p class="title">{{ item.title }}</p>
            <div class="pic" v-if="item.img.length >= 3">
              <img v-for="num in 3" :key="num" :src="item.img[num - 1]">
            </div>
            <p class="author"><span v-if="item.default">置顶</span>{{ item.author }}<img :src="require('@/assets/叉叉.png')"
                v-if="!item.default" name="close" @click="close(index, $event)" /></p>
          </a>

          <!-- 一张图，内容横向排列 -->
          <a v-if="item.img.length < 3 && item.img.length > 0" href="#" class="row"
            :class="{ check: item.check, 'top-text': item.default }">
            <div class="pic">
              <img :src="item.img[0]">
              <div class="video" v-if="item.video">
                <img :src="require('@/assets/播放2.png')">
                <span>{{ item.video }}</span>
              </div>
            </div>
            <div class="right-text-content">
              <p class="title">{{ item.title }}</p>
              <p class="author"><span>{{ item.author }}</span><img :src="require('@/assets/叉叉.png')" name="close"
                  @click="close(index, $event)" /></p>
            </div>
          </a>
        </li>
      </ul>
    </div>

    <van-overlay :show="show" @click="show = false">
      <div class="overlay">
        <div class="user">
          <van-icon name="bars" />
          <div class="userInfo">
            <img :src="require('@/assets/微信图片_20220710222056.jpg')" alt="">
            <span>用户xxxxxx</span>
          </div>
        </div>
        <div class="list">
          <ul>
            <li><img :src="require('@/assets/爱心.png')" alt=""><span>我的关注</span></li>
            <li><img :src="require('@/assets/收藏.png')" alt=""><span>我的收藏</span></li>
            <li><img :src="require('@/assets/皮肤.png')" alt=""><span>皮肤中心</span></li>
            <li><img :src="require('@/assets/用户反馈.png')" alt=""><span>用户反馈</span></li>
          </ul>
        </div>
        <div class="buttom">
          <van-icon name="setting-o" />
          <p>设置</p>
        </div>
        <div class="readme">©2023 Baidu 使用百度前必读</div>
      </div>
    </van-overlay>


  </div>
</template>

<script>
export default {
  name: '',
  data() {
    return {

      show: false,
      navShow: false,
      isLoading: false,

      active: 0,
      tabs: ['推荐', '历史', '视频', '时尚', '国际', '财经', '科技',],
      content: [
        {
          title: '总书记的一周（6月5日—6月11日）',
          author: '央视新闻',
          default: true,
          img: [],
          check: false
        },
        {
          title: '守护全人类的文化瑰宝 习近平这样强调',
          author: '人民网',
          default: true,
          img: [],
          check: false
        },
        {
          title: '浙江壮大村级集体经济的基层实践',
          author: '农民日报',
          default: false,
          img: [],
          check: false
        },
        {
          title: '国际锐评丨美官员轮番上阵，挡不住中东和解的步伐',
          author: '央视新闻',
          default: false,
          img: [
            'https://t11.baidu.com/it/app=106&f=JPEG&fm=30&fmt=auto&q=85&size=f218_146&u=1056497572%2C206203096?w=312&h=208&s=F3B3138D56111BD45821D1A303006001',
          ],
          check: false
        },
        {
          title: '文博日历丨看一部跨越千年的“巨幕电影”',
          author: '央视新闻',
          default: false,
          img: [
            'https://t10.baidu.com/it/app=106&f=JPEG&fm=30&fmt=auto&q=85&size=f218_146&u=702782729%2C206353525?w=312&h=208&s=CA9224C50050C7D24C2C8C1203008092',
            'https://t12.baidu.com/it/app=106&f=JPEG&fm=30&fmt=auto&q=85&size=f218_146&u=1882092928%2C206353526?w=312&h=208&s=5AB105C15ABFD8CE0801A57B03005012',
            'https://t11.baidu.com/it/app=106&f=JPEG&fm=30&fmt=auto&q=85&size=f218_146&u=1185967983%2C206353523?w=312&h=208&s=0430EC3794204D015055C5D7000050B3'
          ],
          check: false,
          video: '02:06'
        },
        {
          title: '从高中起就与萨瓦纳在一起的詹姆斯 诠释了什么叫做完美的爱情',
          author: '稳妥篮球说',
          default: false,
          img: [
            'https://t10.baidu.com/it/app=106&f=JPEG&fm=30&fmt=auto&q=85&size=f218_146&u=99433876%2C206244722?w=312&h=208&s=762AA1E00A71B9D4427980930300C0C2',
          ],
          check: false,
          video: '02:06'
        },
        {
          title: '文博日历丨看一部跨越千年的“巨幕电影”',
          author: '央视新闻',
          default: false,
          img: [
            'https://t10.baidu.com/it/app=106&f=JPEG&fm=30&fmt=auto&q=85&size=f218_146&u=702782729%2C206353525?w=312&h=208&s=CA9224C50050C7D24C2C8C1203008092',
            'https://t12.baidu.com/it/app=106&f=JPEG&fm=30&fmt=auto&q=85&size=f218_146&u=1882092928%2C206353526?w=312&h=208&s=5AB105C15ABFD8CE0801A57B03005012',
            'https://t11.baidu.com/it/app=106&f=JPEG&fm=30&fmt=auto&q=85&size=f218_146&u=1185967983%2C206353523?w=312&h=208&s=0430EC3794204D015055C5D7000050B3'
          ],
          check: false,
          video: '02:06'
        },
        {
          title: '从高中起就与萨瓦纳在一起的詹姆斯 诠释了什么叫做完美的爱情',
          author: '稳妥篮球说',
          default: false,
          img: [
            'https://t10.baidu.com/it/app=106&f=JPEG&fm=30&fmt=auto&q=85&size=f218_146&u=99433876%2C206244722?w=312&h=208&s=762AA1E00A71B9D4427980930300C0C2',
          ],
          check: false,
          video: '02:06'
        },
        {
          title: '文博日历丨看一部跨越千年的“巨幕电影”',
          author: '央视新闻',
          default: false,
          img: [
            'https://t10.baidu.com/it/app=106&f=JPEG&fm=30&fmt=auto&q=85&size=f218_146&u=702782729%2C206353525?w=312&h=208&s=CA9224C50050C7D24C2C8C1203008092',
            'https://t12.baidu.com/it/app=106&f=JPEG&fm=30&fmt=auto&q=85&size=f218_146&u=1882092928%2C206353526?w=312&h=208&s=5AB105C15ABFD8CE0801A57B03005012',
            'https://t11.baidu.com/it/app=106&f=JPEG&fm=30&fmt=auto&q=85&size=f218_146&u=1185967983%2C206353523?w=312&h=208&s=0430EC3794204D015055C5D7000050B3'
          ],
          check: false,
          video: '02:06'
        },
        {
          title: '从高中起就与萨瓦纳在一起的詹姆斯 诠释了什么叫做完美的爱情',
          author: '稳妥篮球说',
          default: false,
          img: [
            'https://t10.baidu.com/it/app=106&f=JPEG&fm=30&fmt=auto&q=85&size=f218_146&u=99433876%2C206244722?w=312&h=208&s=762AA1E00A71B9D4427980930300C0C2',
          ],
          check: false,
          video: '02:06'
        },
        {
          title: '文博日历丨看一部跨越千年的“巨幕电影”',
          author: '央视新闻',
          default: false,
          img: [
            'https://t10.baidu.com/it/app=106&f=JPEG&fm=30&fmt=auto&q=85&size=f218_146&u=702782729%2C206353525?w=312&h=208&s=CA9224C50050C7D24C2C8C1203008092',
            'https://t12.baidu.com/it/app=106&f=JPEG&fm=30&fmt=auto&q=85&size=f218_146&u=1882092928%2C206353526?w=312&h=208&s=5AB105C15ABFD8CE0801A57B03005012',
            'https://t11.baidu.com/it/app=106&f=JPEG&fm=30&fmt=auto&q=85&size=f218_146&u=1185967983%2C206353523?w=312&h=208&s=0430EC3794204D015055C5D7000050B3'
          ],
          check: false,
          video: '02:06'
        },
        {
          title: '从高中起就与萨瓦纳在一起的詹姆斯 诠释了什么叫做完美的爱情',
          author: '稳妥篮球说',
          default: false,
          img: [
            'https://t10.baidu.com/it/app=106&f=JPEG&fm=30&fmt=auto&q=85&size=f218_146&u=99433876%2C206244722?w=312&h=208&s=762AA1E00A71B9D4427980930300C0C2',
          ],
          check: false,
          video: '02:06'
        }, {
          title: '从高中起就与萨瓦纳在一起的詹姆斯 诠释了什么叫做完美的爱情',
          author: '稳妥篮球说',
          default: false,
          img: [
            'https://t10.baidu.com/it/app=106&f=JPEG&fm=30&fmt=auto&q=85&size=f218_146&u=99433876%2C206244722?w=312&h=208&s=762AA1E00A71B9D4427980930300C0C2',
          ],
          check: false,
          video: '02:06'
        },
      ]
    }
  },
  computed: {},
  components: {},
  created() {

  },
  mounted() { },
  methods: {
    onScroll(e) {
      if (this.$refs.root.scrollTop >= 190) {
        this.navShow = true
        console.log(this.$refs.root.scrollTop);
      } else {
        this.navShow = false
      }
      // console.log(e);
    },
    close(index, e) {
      e.stopPropagation()
      console.log(e);
      // this.content.splice(index, 1)
    }
  }
}
</script>
<style lang="less" scoped>
.container {
  width: 100%;
  height: 100vh;
  overflow: hidden;
  overflow-y: scroll;

  .overlay {
    height: 100vh;
    background-color: white;
    width: 250px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding-left: 30px;

    .user {
      height: 160px;
      position: relative;
      display: flex;
      // justify-content: center;
      align-items: center;

      .van-icon {
        position: absolute;
        top: 10px;
        left: -20px;
        font-size: 24px;

      }

      .userInfo {
        position: relative;

        img {
          display: inline-block;
          width: 60px;
          height: 60px;
          margin-right: 15px;
          border-radius: 100%;
          overflow: hidden;
        }

        span {
          display: inline-block;
          max-width: 108px;
          font-family: PingFangSC-Regular;
          font-size: 18px;
          color: #000000;
          line-height: 60px;
          letter-spacing: 0;
          white-space: nowrap;
          overflow: hidden;
          position: absolute;
          top: 0;
          left: 75px;
        }
      }
    }

    .list {
      height: 200px;
      margin-bottom: auto;

      li {
        height: 50px;
        display: flex;
        align-items: center;
      }

      img {
        width: 20px;
        height: 20px;
        margin-right: 1em;
      }
    }

    .buttom {
      display: flex;
      flex-direction: column;
      justify-content: center;
      height: 80px;

      .van-icon {
        margin-left: .5em;
        margin-bottom: .5em;

      }
    }

    .readme {
      display: flex;
      -webkit-box-align: center;
      -ms-flex-align: center;
      align-items: center;
      width: 220px;
      height: 33px;
      font-family: PingFangSC-Regular;
      font-size: 12px;
      color: #CCCCCC;
      letter-spacing: 0;
      border-top: 1px solid #F8F8F8;
    }
  }
}

.top-container {
  height: 230px;

  .header {
    height: 52px;
    margin-bottom: 9px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 12px;

    .van-icon {
      font-size: 23px;
    }
  }

  .logo {
    height: 57px;
    padding-bottom: 30px;
    display: flex;
    justify-content: center;

    img {
      width: 180px;
      height: 57px;
    }
  }

  .search-container {
    height: 51px;
    padding: 0 17px;

    form {
      border: 1px solid #4e6ef2;
      border-radius: 12px;
      height: 51px;
      border-width: 1px;
      display: flex;
      align-items: center;

      input {
        height: 47px;
        width: 183px;
        padding-left: 12px;
        padding-right: 12px;
        font-size: 18px;
        border: 0;
        background: transparent;

      }

      img {
        width: 20px;
        margin-right: 10px;
      }

      .van-button {
        background-color: #4e6ef2;
        border-radius: 0 12px 12px 0;
        height: 100%;
        margin-left: auto;
        font-size: 16px;
        font-weight: 700;
        white-space: nowrap;
        letter-spacing: -1px;
        text-shadow: none;
        color: #fff;
        background-color: #4e6ef2;
        -webkit-user-select: none;
        user-select: none;
      }

    }
  }

  .divider {
    height: 10px;
    background: #f1f1f1;
    margin-top: 20px;
  }


}

::v-deep .van-tabs {
  // position: relative;
  // height: 39px;
  // top: -39px;
  font-size: 16px;
  color: #666;

  .van-tab {
    padding: 20px 16px;
    font-size: 16px;
    // background: #f1f1f1;
  }

  .van-icon {
    font-size: 16px;
    z-index: 999;
  }
}

.content-container {
  padding: 0 16px;
  position: relative;

  .navs {
    width: 100%;
    height: 40px;
    overflow: hidden;
    // overflow-x: scroll;
    overflow-x: visible;
    position: fixed;
    top: 0;
    left: 0;
    z-index: 999;
    transition: all 0.5s;

    ul {
      font-size: 16px;
      color: #666;
      display: flex;
      background: #f1f1f1;
      height: 100%;
      align-items: center;

      li {
        padding: 0 16px;
        height: 40px;
        line-height: 40px;
        text-align: center;
        white-space: nowrap;
        position: relative;
      }

      li.active {
        color: #38f;
      }

      li.active::after {
        content: '';
        position: absolute;
        bottom: 2px;
        left: 50%;
        width: 2.5em;
        transform: translateX(-50%);
        border-bottom: 2px solid #38f;
        z-index: 9999;
      }

      li.add {
        // padding: 0;
        position: fixed;
        right: 0;
        top: 0;
        font-size: 20px;
        z-index: 99999;
        background: #f1f1f1;

        // width: ;
      }

    }
  }

  .content {
    li {}

    a {
      display: flex;
      width: 100%;
      padding: 14px 0;
      color: #333;
      font-weight: normal;
      overflow: hidden;

    }

    .top-text {
      padding-bottom: 5px;
    }

    .check {
      color: #999;
    }

    .column {
      flex-direction: column;
    }

    .title {
      font-size: 18px;
      overflow: hidden;
      text-overflow: ellipsis;
      display: -webkit-box;
      -webkit-line-clamp: 2;
      -webkit-box-orient: vertical;
      margin-bottom: 3px;
      line-height: 24px;
    }

    .author {
      font-size: 13px;
      color: #999;
      display: flex;
      height: auto !important;
      position: relative;

      span {
        color: #ec4345;
        margin-right: 8px;

      }

      img {
        position: absolute;
        right: 0;
        top: -2.5px;
        font-size: 18px;
        width: 15px;
        height: 15px;

      }
    }

    .pic {
      position: relative;
      display: flex;
      justify-content: space-between;
      margin-bottom: 10px;

      img {
        width: 119px;
        height: 80px;
      }

      .video {
        width: 33.65%;
        position: absolute;
        bottom: 5px;
        right: 5px;
        height: 20px;
        line-height: 20px;
        font-size: 10px;
        display: flex;
        align-items: center;
        padding-left: 10px;
        padding-right: 10px;
        color: #fff;
        background-color: rgba(0, 0, 0, 0.4);
        -webkit-border-radius: 10px/10px;

        img {
          height: 80%;
        }
      }
    }

    .right-text-content {
      margin-left: 14px;
      height: 73px;
      display: flex;
      flex-direction: column;
      justify-content: space-between;

      .author {
        span {
          color: #999;
        }
      }
    }
  }


}
</style>
