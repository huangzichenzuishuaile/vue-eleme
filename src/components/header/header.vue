<template>
  <div class="header">
    <div class="centent-wrapper">
      <div class="avatar">
        <img width="64" height="64" :src="seller.avatar">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}}/{{seller.deliveryTime}}分钟送达
        </div>
        <div v-if="seller.supports" class="support">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div v-if="seller.supports" class="support_accout" @click="showDetail">
        <span class="count">{{seller.supports.length}}个</span>
        <span class="icon-keyboard_arrow_right"></span>
      </div>
    </div>
    <div class="bulletin-wrapper"  @click="showDetail">
      <span class="bulletion_title"></span>
      <span class="bulletion_text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="background">
      <img :src="seller.avatar" width="100%" alt="">
    </div>
    <transition name="fade">
      <div class="showDetail" v-show="detailShow">
        <div class="detail-wrapper clearfix">
          <div class="detail-main">
            <h1 class="name">{{seller.name}}</h1>
            <div class="star-wrapper">
              <v-star :size="48" :score="seller.score"></v-star>
            </div>
            <div class="title">
              <div class="line"></div>
              <div class="text">优惠信息</div>
              <div class="line"></div>
            </div>
            <ul v-if="seller.supports" class="supports">
              <li class="support-item" v-for="(item,index) in seller.supports" :key="index">
                <span class="icon" :class="classMap[item.type]"></span>
                <span class="text">{{item.description}}</span>
              </li>
            </ul>
            <div class="title">
              <div class="line"></div>
              <div class="text">商家公告</div>
              <div class="line"></div>
            </div>
            <div class="bulletin">
              <p class="content">{{seller.bulletin}}</p>
            </div>
          </div>
        </div>
        <div class="detail-close" @click="hideDetail">
          <i class="icon-close"></i>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
import star from '../star/star'
export default {
  props:{
    seller:{
      type: Object
    }
  },
  components:{
    "v-star":star
  },
  data(){
    return{
      detailShow: false
    }
  },
  methods: {
    showDetail(){
      this.detailShow = true
    },
    hideDetail(){
      this.detailShow = false
    }
  },
  created(){
    this.classMap = ['decrease','discount','special','invoice','guarantee']
  }
}
</script>
<style lang="scss" scoped>
@import '../../common/sass/icon.css';
@import '../../common/sass/mixin.scss';
.header{
  position: relative;
  overflow: hidden;
  background: rgba(7,17,27,0.5);

  .centent-wrapper{
    display: flex;
    position: relative;
    padding: 24px 0 18px 24px;
    font-size: 0;

    .avatar{
      width: 64px;
      height: 64px;
      vertical-align: top;
    }
    .content{
      margin-left: 16px;
      font-size: 0;
      color: rgb(255,255,255);

      .title{
        margin: 2px 0 8px 0;

        .brand{
          display: inline-block;
          width: 30px;
          height: 18px;
          @include bg-image('./img/brand');
          background-size: 30px 18px;
          background-repeat: no-repeat;
        }

        .name{
          line-height: 18px;
          vertical-align: top;
          margin-left: 6px;
          font-size: 16px;
          font-weight: bold;
          font-size: 16px;
        }
      }

      .description{
        margin: 0 0 10px 0;
        font-weight: 200;
        line-height: 12px;
        font-size: 12px;
        color:rgb(255, 255, 255)
      }

      .support{
        font-size: 0;
        color:rgb(255, 255, 255);

        .icon{
          display: inline-block;
          vertical-align: top;
          width: 12px;
          height: 12px;
          margin-right: 4px;
          background-size: 12px 12px;
          background-repeat: no-repeat;

          &.decrease{
            @include bg-image('./img/decrease_1')
          }
          &.discount{
            @include bg-image('./img/discount_1')
          }
          &.guarantee{
            @include bg-image('./img/guarantee_1')
          }
          &.invoice{
            @include bg-image('./img/invoice_1')
          }
          &.special{
            @include bg-image('./img/special_1')
          }
        }

        .text{
          font-weight: 200;
          line-height: 13px;
          font-size: 10px;
        }
      }
    }

    .support_accout{
      position: absolute;
      right: 12px;
      bottom: 14px;
      padding: 0 8px;
      height: 24px;
      line-height: 25px;
      font-size: 0;
      border-radius: 12px;
      background-color: rgba(0, 0, 0, 0.2);
      text-align: center;
      color:rgb(255,255,255);

      .count{
        font-size: 10px;
        font-weight: 200;
        vertical-align: top;
      }

      .icon-keyboard_arrow_right{
        margin-left: 2px;
        line-height: 24px;
        font-size: 10px;
      }
    }
  }
  .bulletin-wrapper{
    display: flex;
    align-items: center;
    height: 28px;
    padding: 0 12px;
    background: rgba(7,17,27,0.2);
    color: rgb(255, 255, 255);

      .bulletion_title{
        display: inline-block;
        width: 22px;
        height: 12px;
        @include bg-image('./img/bulletin');
        background-size: 22px 12px;
        background-repeat: no-repeat;
      }

      .bulletion_text{
        flex: 1;
        margin: 0 8px;
        font-size: 10px;
        font-weight: 200;
        line-height: 29px;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
      }

      .icon-keyboard_arrow_right{
        font-size: 10px;
      }
  }
  .background{
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100;
    z-index: -1;
    filter: blur(10px);
  }
  .showDetail{
    position: fixed;
    top: 0;
    left: 0;
    z-index: 1;
    width: 100%;
    height: 100%;
    overflow: auto;
    color:#fff;
    background: rgba(7, 17, 27, 0.8);
    backdrop-filter: blur(10px);//仅对ios手机有效  使其背景模糊
    &.fade-enter-active{
      transition: all .5s;
      opacity: 1;
      background: rgba(7, 17, 27, 0.8);
    }
    &.fade-leave-active {
      transition: all .5s;
      opacity: 0;
      background: rgba(7, 17, 27, 0);
    }
    &.fade-enter,&.fade-leave{
      opacity: 0;
    }


    // sticky-footer
    .detail-wrapper{
      width:100%;
      min-height: 100%;

      .detail-main{
        margin-top: 64px;
        padding-bottom: 64px;
        .name{
          line-height: 16px;
          font-size: 16px;
          font-weight: 700;
          text-align: center;
        }
        .star-wrapper{
          margin-top: 16px;
          padding: 2px 0;
          text-align: center;
        }
        .title{
          display: flex;
          width: 80%;
          margin: 28px auto 24px auto;
          .line{
            flex: 1;
            position: relative;
            top: -6px;
            border-bottom: 1px solid rgba(255,255,255,.2);
          }
          .text{
            padding: 0 12px;
            line-height: 14px;
            font-size: 14px;
            font-weight: 700;
            color:rgb(255, 255, 255);
          }
        }
        .supports{
          width: 80%;
          margin: 0 auto;
          .support-item{
            padding: 0 12px;
            margin-bottom: 12px;
            font-size: 0;
            &:last-child{
              margin-bottom: 0;
            }
            .text{
              font-size: 12px;
              font-weight: 200;
              line-height: 16px;
              columns: rgb(255,255,255);
            }
            .icon{
              display: inline-block;
              width: 16px;
              height: 16px;
              vertical-align: top;
              margin-right: 6px;
              background-size: 16px 16px;
              background-repeat: no-repeat;
              &.decrease{
                @include bg-image('./img/decrease_2')
              }
              &.discount{
                @include bg-image('./img/discount_2')
              }
              &.guarantee{
                @include bg-image('./img/guarantee_2')
              }
              &.invoice{
                @include bg-image('./img/invoice_2')
              }
              &.special{
                @include bg-image('./img/special_2')
              }
            }
          }
        }
        .bulletin{
          width:80%;
          margin: 0 auto;
          .content{
            padding: 0 12px;
            line-height: 24px;
            font-size: 12px;
          }
        }
      }
    }

    .clearfix{
      display: inline-block;
      &:after{
        display: block;
        content: ' ';
        height: 0;
        line-height: 0;
        clear: both;
        visibility: hidden;
      }
    }


    .detail-close{
      position: relative;
      width: 32px;
      height: 32px;
      margin: -64px auto 0 auto;
      clear: both;
      font-size: 32px;
    }
  }
}
</style>
