<template>
  <div class="synthesispage">
    <div class="top">
      <van-nav-bar
        title="合成"
        left-arrow
        fixed
        placeholder
        @click-left="onClickLeft"
      />
    </div>
    <!-- 主体内容 -->
    <div class="sythcontent">
      <van-tabs
        background="#121933"
        title-inactive-color="#666"
        title-active-color="#fff"
        v-model="synthActiveName"
      >
        <van-tab title="三级卡牌" name="1">
          <div class="threecard">
            <!-- 头部标题 -->
            <div class="threecardTop">
              <div class="title">铸造合成三级卡牌</div>
              <img
                class="start1"
                src="../../assets/img/synth/start1.png"
                alt=""
              />
              <img
                class="start2"
                src="../../assets/img/synth/start2.png"
                alt=""
              />
            </div>
            <div class="threecardlog">
              <div class="img">
                <img src="../../assets/img/synth/synthlog.png" alt="" />
              </div>
            </div>
            <div class="synthcard">
              <!-- 倒计时 -->
              <!-- 距离开始还剩 -->
              <div :key="1" v-if="countdownFlag" class="countdown">
                <span class="text">距离开始还剩: </span>
                <span class="time">
                  <van-count-down
                    @finish="finishHandler"
                    millisecond
                    :time="time"
                  >
                    <template #default="timeData">
                      <span class="block">0{{ timeData.minutes }}</span>
                      <span class="colon">:</span>
                      <span class="block">{{ timeData.seconds }}</span>
                      <span class="colon">:</span>
                      <span class="block milliseconds">{{
                        timeData.milliseconds
                      }}</span>
                    </template>
                  </van-count-down>
                </span>
              </div>
              <!-- 距离结束还剩 -->
              <div :key="2" v-if="!countdownFlag" class="countdown bgcountdown">
                <span class="text bgtext">距离结束还剩: </span>
                <span class="time">
                  <van-count-down
                    @finish="finishHandler2"
                    millisecond
                    :time="time"
                  >
                    <template #default="timeData">
                      <span class="block bgblock">0{{ timeData.minutes }}</span>
                      <span class="colon bgcolon">:</span>
                      <span class="block bgblock">{{ timeData.seconds }}</span>
                      <span class="colon bgcolon">:</span>
                      <span class="block bgblock milliseconds">{{
                        timeData.milliseconds
                      }}</span>
                    </template>
                  </van-count-down>
                </span>
              </div>
              <!-- 添加卡牌 -->
              <div class="addcardwarp">
                <div class="addcard">
                  <div @click="showcard = true" class="top">
                    <p>
                      <span class="cardAdd">+</span>
                      <br />
                      添加一级卡牌
                    </p>
                  </div>
                  <div>
                    <p>
                      <span class="cardAdd">+</span>
                      <br />
                      添加一级卡牌
                    </p>
                  </div>
                  <div>
                    <p>
                      <span class="cardAdd">+</span>
                      <br />
                      添加二级卡牌
                    </p>
                  </div>
                </div>
                <div class="addcardfooter">
                  <div @click="show1 = true" class="ftop">
                    <van-button :disabled="false" type="info"
                      >100%合成</van-button
                    >
                  </div>
                  <p>成功概率100%</p>
                  <p>一级卡牌*2+二级卡牌 铸造合成三级卡牌</p>
                </div>
              </div>

              <!-- 添加卡牌 -->
              <div class="addcardwarp">
                <div class="addcard">
                  <div class="top">
                    <p>
                      <span class="cardAdd">+</span>
                      <br />
                      添加一级卡牌
                    </p>
                  </div>
                  <div>
                    <p>
                      <span class="cardAdd">+</span>
                      <br />
                      添加一级卡牌
                    </p>
                  </div>
                  <div>
                    <p>
                      <span class="cardAdd">+</span>
                      <br />
                      添加二级卡牌
                    </p>
                  </div>
                </div>
                <div class="addcardfooter">
                  <div @click="show1 = true" class="ftop">
                    <van-button
                      style="padding: 0 50px"
                      :disabled="false"
                      type="info"
                      >合成</van-button
                    >
                  </div>
                  <p>成功概率80%</p>
                  <p>合成失败(20%)全部销毁</p>
                  <p>一级卡牌*2+二级卡牌 铸造合成三级卡牌</p>
                </div>
              </div>

              <!-- 添加卡牌 -->
              <div class="addcardwarp">
                <div class="addcard">
                  <div>
                    <p>
                      <span class="cardAdd">+</span>
                      <br />
                      添加一级卡牌
                    </p>
                  </div>
                  <div>
                    <p>
                      <span class="cardAdd">+</span>
                      <br />
                      添加二级卡牌
                    </p>
                  </div>
                </div>
                <div class="addcardfooter">
                  <div @click="show1 = true" class="ftop">
                    <van-button
                      style="padding: 0 50px"
                      :disabled="false"
                      type="info"
                      >合成</van-button
                    >
                  </div>
                  <p>成功概率40%</p>
                  <p>合成失败(60%)全部销毁</p>
                  <p>一级卡牌+二级卡牌 铸造合成三级卡牌</p>
                </div>
              </div>
            </div>
          </div>
        </van-tab>
        <van-tab title="权益卡" name="2">
          <div class="equity">
            <!-- 分红权益卡牌 -->
            <div class="econtentTtem">
              <div class="etop">
                <p class="title">实时节点分红权益卡</p>
                <img
                  class="start1"
                  src="../../assets/img/synth/start1.png"
                  alt=""
                />
                <img
                  class="start2"
                  src="../../assets/img/synth/start2.png"
                  alt=""
                />
              </div>
              <div class="addcard">
                <p>
                  <span class="add">+</span>
                  <br />
                  添加三级卡牌
                </p>
              </div>
              <div class="sythnBtn">
                <van-button
                  @click="equityBtnHandler"
                  :disabled="false"
                  style="width: 170px"
                  type="info"
                  >合成</van-button
                >
              </div>
              <div class="msg">
                <p>成功概率25%</p>
                <p>5张三级青铜甲犀牛卡牌可合成一次</p>
                <p>合成失败后则不可再次参与合成，卡牌不销毁</p>
              </div>
            </div>

            <div class="econtentTtem">
              <div class="etop">
                <p class="title">中级节点分红权益卡</p>
                <img
                  class="start1"
                  src="../../assets/img/synth/start1.png"
                  alt=""
                />
                <img
                  class="start2"
                  src="../../assets/img/synth/start2.png"
                  alt=""
                />
              </div>
              <div class="addcard">
                <p>
                  <span class="add">+</span>
                  <br />
                  添加四级卡牌
                </p>
              </div>
              <div class="sythnBtn">
                <van-button :disabled="true" style="width: 170px" type="info"
                  >合成</van-button
                >
              </div>
              <div class="msg">
                <p>成功概率25%</p>
                <p>5张四级白银甲犀牛卡牌可合成一次</p>
                <p>合成失败后则不可再次参与合成，卡牌不销毁</p>
              </div>
            </div>

            <div style="padding-bottom: 60px" class="econtentTtem">
              <div class="etop">
                <p class="title">高级节点分红权益卡</p>
                <img
                  class="start1"
                  src="../../assets/img/synth/start1.png"
                  alt=""
                />
                <img
                  class="start2"
                  src="../../assets/img/synth/start2.png"
                  alt=""
                />
              </div>
              <div class="addcard">
                <p>
                  <span class="add">+</span>
                  <br />
                  添加五级卡牌
                </p>
              </div>
              <div class="sythnBtn">
                <van-button :disabled="true" style="width: 170px" type="info"
                  >合成</van-button
                >
              </div>
              <div class="msg">
                <p>成功概率25%</p>
                <p>5张五级黄金甲犀牛卡牌可合成一次</p>
                <p>合成失败后则不可再次参与合成，卡牌不销毁</p>
              </div>
            </div>
          </div>
        </van-tab>
        <van-tab title="永久权益卡" name="3">
          <div class="eikycard">
            <div class="eikycardItem">
              <div class="eikytop">
                <p class="title">永久实时节点分红权益卡</p>
                <img
                  class="start1"
                  src="../../assets/img/synth/start1.png"
                  alt=""
                />
                <img
                  class="start2"
                  src="../../assets/img/synth/start2.png"
                  alt=""
                />
              </div>
              <div class="eikyaddcard">
                <div>
                  <p>
                    <span class="eikyadd">+</span>
                    添加100天实时节点
                    <br />
                    分红权益卡
                  </p>
                </div>
                <div>
                  <p>
                    <span class="eikyadd">+</span>
                    添加200天实时节点
                    <br />
                    分红权益卡
                  </p>
                </div>
                <div>
                  <p>
                    <span class="eikyadd">+</span>
                    添加300天实时节点
                    <br />
                    分红权益卡
                  </p>
                </div>
              </div>
              <div class="eikybtn">
                <van-button :disabled="true" style="width: 170px" type="info"
                  >合成</van-button
                >
              </div>
              <div class="eiktfooter">
                <p>成功概率100%</p>
                <p>100天*3+200天*2+300天*1可合成一张永久</p>
                <p>合成成功则销毁原卡牌，合成失败不销毁原卡牌</p>
              </div>
            </div>

            <div class="eikycardItem">
              <div class="eikytop">
                <p class="title">永久中级节点分红权益卡</p>
                <img
                  class="start1"
                  src="../../assets/img/synth/start1.png"
                  alt=""
                />
                <img
                  class="start2"
                  src="../../assets/img/synth/start2.png"
                  alt=""
                />
              </div>
              <div class="eikyaddcard">
                <div>
                  <p>
                    <span class="eikyadd">+</span>
                    添加100天中级节点
                    <br />
                    分红权益卡
                  </p>
                </div>
                <div>
                  <p>
                    <span class="eikyadd">+</span>
                    添加200天中级节点
                    <br />
                    分红权益卡
                  </p>
                </div>
                <div>
                  <p>
                    <span class="eikyadd">+</span>
                    添加300天中级节点
                    <br />
                    分红权益卡
                  </p>
                </div>
              </div>
              <div class="eikybtn">
                <van-button :disabled="true" style="width: 170px" type="info"
                  >合成</van-button
                >
              </div>
              <div class="eiktfooter">
                <p>成功概率100%</p>
                <p>100天*3+200天*2+300天*1可合成一张永久</p>
                <p>合成成功则销毁原卡牌，合成失败不销毁原卡牌</p>
              </div>
            </div>

            <div class="eikycardItem">
              <div class="eikytop">
                <p class="title">永久高级节点分红权益卡</p>
                <img
                  class="start1"
                  src="../../assets/img/synth/start1.png"
                  alt=""
                />
                <img
                  class="start2"
                  src="../../assets/img/synth/start2.png"
                  alt=""
                />
              </div>
              <div class="eikyaddcard">
                <div>
                  <p>
                    <span class="eikyadd">+</span>
                    添加100天高级节点
                    <br />
                    分红权益卡
                  </p>
                </div>
                <div>
                  <p>
                    <span class="eikyadd">+</span>
                    添加200天高级节点
                    <br />
                    分红权益卡
                  </p>
                </div>
                <div>
                  <p>
                    <span class="eikyadd">+</span>
                    添加300天高级节点
                    <br />
                    分红权益卡
                  </p>
                </div>
              </div>
              <div class="eikybtn">
                <van-button :disabled="true" style="width: 170px" type="info"
                  >合成</van-button
                >
              </div>
              <div class="eiktfooter">
                <p>成功概率100%</p>
                <p>100天*3+200天*2+300天*1可合成一张永久</p>
                <p>合成成功则销毁原卡牌，合成失败不销毁原卡牌</p>
              </div>
            </div>
          </div>
        </van-tab>
      </van-tabs>
    </div>
    <!-- 页脚 -->
    <div class="synthFooter">
      <p class="img-icons">
        <img src="@/assets/img/icon-telegram.png" alt />
        <img src="@/assets/img/icon-twitter.png" alt />
        <img src="@/assets/img/icon-email.png" alt />
      </p>
      <p class="footer-p">&copy;&nbsp;2022年EOTC版权所有。</p>
    </div>
    <!-- 合成遮罩 -->
    <van-overlay :show="show1" :key="1.1" @click="show1 = false">
      <div class="wrapper" @click.stop>
        <div class="maskbox">
          <div>
            风险提示: <br />
            合成后无论是否成功卡牌都将销毁
          </div>
          <div>
            <p @click="show1 = false">取消</p>
            <p @click="confirmHandler">确定</p>
          </div>
          <img
            class="img"
            src="../../assets/img/coincard/icon1.png"
            alt="警告"
          />
        </div>
      </div>
    </van-overlay>
    <van-overlay :show="show2" :key="1.2" @click="show2 = false">
      <div class="wrapper" @click.stop>
        <div class="maskbox">
          <div style="color: #333333">请确定是否要开始进行合成</div>
          <div>
            <p @click="show2 = false">取消</p>
            <p @click="confirmHandler2">确定</p>
          </div>
          <img
            class="img"
            src="../../assets/img/coincard/icon1.png"
            alt="警告"
          />
        </div>
      </div>
    </van-overlay>
    <!-- 选择卡牌遮罩 -->
    <div id="maskwait">
      <van-overlay :lock-scroll="false" :show="showcard">
        <div class="waitWrapper" @click.stop>
          <div class="waitTop">
            <div @click="maskCancelHandler">取消</div>
            <div>选择卡牌</div>
            <div>确定</div>
          </div>
          <ul class="cardContent">
            <li v-for="item in maskcardData" :key="item.id">
              <img :src="item.url" alt="" />
              <p class="title">{{ item.title }}</p>
              <p class="text">#{{ item.ucode }}</p>
              <div class="cardselect">
                <van-checkbox
                  v-model="cardmaskFlag"
                  icon-size="20px"
                ></van-checkbox>
              </div>
            </li>
          </ul>
        </div>
      </van-overlay>
    </div>
    <!-- 权益卡遮罩 -->
    <van-overlay :show="show3" :key="1.3" @click="show3 = false">
      <div class="wrapper" @click.stop>
        <div class="maskbox">
          <div style="color: #333333">
            合成:
            60%卡牌为100天分红期限，35%卡牌200天分红期限，5%卡牌为300天分红期限
          </div>
          <div>
            <p @click="show3 = false">取消</p>
            <p @click="econfirmHandler">确定</p>
          </div>
          <img
            class="img"
            src="../../assets/img/coincard/icon1.png"
            alt="警告"
          />
        </div>
      </div>
      <!-- <Popout :show="show3">
        风险提示: <br />
        合成后无论是否成功卡牌都将销毁
      </Popout> -->
    </van-overlay>
  </div>
</template>
<script>
// import Popout from "../tool/Scroll/popout/popout_page.vue";
export default {
  // components: {
  //   Popout,
  // },
  data() {
    return {
      cardmaskFlag: false, //复选框
      showcard: false, //卡牌选择遮罩
      show1: false, //合成遮罩
      show2: false,
      show3: false, //权益卡牌
      time: 10 * 60 * 1000,
      synthActiveName: "3",
      countdownFlag: true,
      // 定义卡牌数据
      maskcardData: [
        {
          id: 1,
          title: "一级黄金甲犀牛",
          ucode: "000001",
          url: require("../../assets/img/blindbox/card1.png"),
        },
        {
          id: 2,
          title: "一级黄金甲犀牛",
          ucode: "000001",
          url: require("../../assets/img/blindbox/card1.png"),
        },
        {
          id: 3,
          title: "一级黄金甲犀牛",
          ucode: "000001",
          url: require("../../assets/img/blindbox/card1.png"),
        },
        {
          id: 4,
          title: "一级黄金甲犀牛",
          ucode: "000001",
          url: require("../../assets/img/blindbox/card1.png"),
        },
        {
          id: 5,
          title: "一级黄金甲犀牛",
          ucode: "000001",
          url: require("../../assets/img/blindbox/card1.png"),
        },
        {
          id: 6,
          title: "一级黄金甲犀牛",
          ucode: "000001",
          url: require("../../assets/img/blindbox/card1.png"),
        },
        {
          id: 7,
          title: "一级黄金甲犀牛",
          ucode: "000001",
          url: require("../../assets/img/blindbox/card1.png"),
        },
        {
          id: 8,
          title: "一级黄金甲犀牛",
          ucode: "000001",
          url: require("../../assets/img/blindbox/card1.png"),
        },
        {
          id: 9,
          title: "一级黄金甲犀牛",
          ucode: "000001",
          url: require("../../assets/img/blindbox/card1.png"),
        },
        {
          id: 10,
          title: "一级黄金甲犀牛",
          ucode: "000001",
          url: require("../../assets/img/blindbox/card1.png"),
        },
        {
          id: 11,
          title: "一级黄金甲犀牛",
          ucode: "000001",
          url: require("../../assets/img/blindbox/card1.png"),
        },
        {
          id: 12,
          title: "一级黄金甲犀牛",
          ucode: "000001",
          url: require("../../assets/img/blindbox/card1.png"),
        },
        {
          id: 13,
          title: "一级黄金甲犀牛",
          ucode: "000001",
          url: require("../../assets/img/blindbox/card1.png"),
        },
      ],
      //maskFlag1: false, //遮罩第一次状态
    };
  },

  methods: {
    // 权益卡遮罩确认处理
    econfirmHandler() {},
    equityBtnHandler() {
      // console.log("1111");
      this.show3 = true;
    },
    maskCancelHandler() {
      this.showcard = false;
    },
    showCardHandler() {
      this.showcard = true;
    },
    confirmHandler2() {
      this.show2 = false;
      console.log("动画执行...");
    },
    confirmHandler() {
      // console.log("666");
      this.show1 = false;
      this.show2 = true;
    },
    // 点击合成
    onClickLeft() {
      this.$router.back();
    },
    finishHandler() {
      this.time = 10 * 60 * 1000;
      this.countdownFlag = false;
    },
    finishHandler2() {
      this.time = 10 * 60 * 1000;
      this.countdownFlag = true;
    },
  },
};
</script>
<style lang="less" scoped>
.synthesispage {
  // ?头部样式
  .top {
    /deep/ .van-nav-bar__content {
      background-color: #1b2945;
    }
    /deep/ .van-nav-bar {
      background-color: none;
    }
    /deep/ .van-icon {
      color: #fff;
    }
    /deep/ .van-nav-bar__title {
      color: #fff;
    }
  }
  //   ?主体内容
  .sythcontent {
    margin-bottom: 200px;
    /deep/ .van-tab__text {
      font-size: 36px;
    }
    /deep/ .van-tabs__line {
      background-color: #237ff8;
    }
    // 三级卡牌
    .threecard {
      width: 100%;
      background: linear-gradient(174deg, #121933 0%, #121933 0%, #06070a 100%);
      //    头部
      .threecardTop {
        width: 400px;
        margin: 0 auto 80px;
        padding-top: 60px;
        position: relative;
        .title {
          text-align: center;
          color: #fff;
          font-size: 36px;
          font-style: oblique;
        }
        .start1 {
          position: absolute;
          top: 35px;
          left: 0;
          transform: scale(0.6);
        }
        .start2 {
          position: absolute;
          bottom: -10px;
          right: 0;
          transform: scale(0.6);
        }
      }
      .threecardlog {
        width: 100%;
        height: 232px;
        .img {
          width: 400px;
          height: 232px;
          margin: 0 auto;
          img {
            width: 100%;
            height: 100%;
          }
        }
        // display: ;
      }
      //   合成
      .synthcard {
        position: relative;
        // 倒计时
        .countdown {
          width: 470px;
          height: 80px;
          background: #2c568c;
          border-radius: 40px;
          display: flex;
          justify-content: space-between;
          align-items: center;
          position: absolute;
          top: -20px;
          left: 50%;
          transform: translateX(-50%);
          .text {
            color: #fff;
            font-size: 28px;
            margin-left: 40px;
          }
          .time {
            margin-right: 30px;
            .block {
              display: inline-block;
              width: 48px;
              height: 48px;
              background: #64a7ff;
              border-radius: 10px;
              color: #fff;
              text-align: center;
              line-height: 48px;
            }
            .milliseconds {
              width: 68px;
            }

            .colon {
              color: #64a7ff;
              margin: 0 10px;
            }
          }
        }
        // 结束样式
        .bgcountdown {
          background: #6b403a;
        }
        .bgtext {
          color: #ff7464 !important;
        }
        .bgblock {
          background: #ff7464 !important;
        }
        .bgcolon {
          color: #ff7464 !important;
        }
        .addcardwarp {
          width: 100%;
          background: #1b2333;
          .addcard {
            display: flex;
            justify-content: space-around;
            flex-wrap: wrap;
            padding-top: 130px;
            div {
              width: 330px;
              height: 460px;
              border-radius: 8px;
              border: 2px solid #ccc;
              display: grid;
              place-items: center;
              color: #666;
              font-size: 36px;

              p {
                text-align: center;
                .cardAdd {
                  font-size: 1.5rem;
                }
              }
            }
            .top {
              width: 330px;
              height: 460px;
              margin: 0 210px 40px;
            }
          }
          .addcardfooter {
            padding-bottom: 20px;
            .ftop {
              //   width: 216px;
              margin: 60px 0 40px;
              // padding: 0 10px 0 10px;
              display: flex;
              justify-content: center;
            }
            p {
              font-size: 36px;
              color: #999;
              text-align: center;
              margin-bottom: 20px;
            }
          }
        }
      }
    }
    // 权益卡
    .equity {
      width: 100%;
      background: linear-gradient(174deg, #121933 0%, #121933 0%, #06070a 100%);
      .econtentTtem {
        margin-bottom: 100px;
        .etop {
          width: 430px;
          margin: 0 auto;
          padding-top: 60px;
          height: 48px;
          position: relative;
          .title {
            text-align: center;
            font-size: 36px;
            color: #fff;
            font-family: DOUYU-Regular, DOUYU;
            font-style: oblique;
          }
          .start1 {
            position: absolute;
            top: 35px;
            left: 0;
            transform: scale(0.6);
          }
          .start2 {
            position: absolute;
            bottom: -10px;
            right: 0;
            transform: scale(0.6);
          }
        }
        .addcard {
          width: 330px;
          height: 460px;
          margin: 60px auto 0;
          border: 5px solid #3e4759;
          border-radius: 8px;
          display: grid;
          place-items: center;
          p {
            color: #fff;
            font-size: 28px;
            text-align: center;
            .add {
              color: #3e4759;
              font-size: 140px;
            }
          }
        }
        .sythnBtn {
          width: 330px;
          margin: 40px auto 0;
        }
        .msg {
          margin-top: 40px;
          color: #fff;
          text-align: center;
          font-size: 28px;
          p {
            &:nth-child(2) {
              margin: 20px 0;
            }
          }
        }
      }
    }
    // 永久权益卡
    .eikycard {
      width: 100%;
      background: linear-gradient(174deg, #121933 0%, #121933 0%, #06070a 100%);
      padding-bottom: 60px;
      .eikycardItem {
        padding-top: 80px;
        .eikytop {
          width: 526px;
          margin: 0 auto 0;
          position: relative;
          p {
            color: #fff;
            font-size: 36px;
            font-style: oblique;
            text-align: center;
          }
          .start1,
          .start2 {
            position: absolute;
            transform: scale(0.6);
          }
          .start1 {
            top: -15px;
            left: 8px;
          }
          .start2 {
            bottom: -2px;
            right: 8px;
          }
        }
        .eikyaddcard {
          margin-top: 60px;
          display: flex;
          justify-content: space-around;
          flex-wrap: wrap;
          div {
            width: 330px;
            height: 460px;
            border: 4px solid #3e4759;
            border-radius: 16px;
            display: grid;
            place-items: center;
            text-align: center;
            &:nth-child(1) {
              margin: 0 200px 40px;
            }
            p {
              color: #fff;
              font-size: 28px;
              line-height: 50px;
              .eikyadd {
                display: block;
                margin-bottom: 60px;
                color: #3e4759;
                font-size: 120px;
              }
            }
          }
        }
        .eikybtn {
          display: flex;
          justify-content: center;
          margin-top: 60px;
        }
        .eiktfooter {
          margin-top: 40px;
          color: #fff;
          text-align: center;
          font-size: 28px;
          line-height: 2;
        }
      }
    }
  }
  //   ?页脚
  .synthFooter {
    background: #11192b;
    padding: 30px 0;
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    box-sizing: border-box;
    .footer-p {
      color: #fff;
      font-size: 0.4rem;
      margin-left: 20px;
    }
    .img-icons {
      img {
        margin: 0 20px;
      }
    }
  }
  //   ?合成遮罩
  .wrapper {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100%;
    .maskbox {
      width: 590px;
      background-color: #fff;
      border-radius: 20px;
      position: relative;

      div {
        &:nth-child(1) {
          padding: 100px 30px 40px 30px;
          color: #fc7542;
          font-size: 32px;
          line-height: 53px;
          text-align: center;
        }
        &:nth-child(2) {
          width: 100%;
          height: 95px;
          line-height: 95px;
          display: flex;
          align-items: center;
          font-size: 32px;
          border-top: 1px solid #f3f4f5;

          p {
            flex: 1;
            text-align: center;
            font-size: 32px;
            height: 100%;
            &:nth-child(1) {
              color: #666666;
              border-right: 1px solid #f3f4f5;
            }
            &:nth-child(2) {
              color: #1b2945;
            }
          }
        }
      }
      .img {
        width: 200px;
        height: 200px;
        position: absolute;
        top: -25%;
        left: 50%;
        transform: translate(-50%, 0%);
      }
    }
  }
  // ?选择卡牌遮罩
  .waitWrapper {
    padding-top: 30px;
    position: fixed;
    bottom: 0;
    left: 0;
    background: #1b2333;
    border-radius: 32px;
    .waitTop {
      display: flex;
      // justify-content: center;
      div {
        &:nth-child(1) {
          width: 56px;
          height: 40px;
          color: #ccc;
          font-size: 28px;
          margin-left: 20px;
        }
        &:nth-child(2) {
          flex: 1;
          color: #fff;
          font-size: 32px;
          text-align: center;
        }
        &:nth-child(3) {
          width: 56px;
          height: 40px;
          margin-right: 20px;
          color: #237ff8;
          font-size: 28px;
        }
      }
    }
    .cardContent {
      margin-top: 40px;
      display: flex;
      flex-wrap: wrap;
      height: 825px;
      overflow-y: auto;
      // overflow-y: scroll;
      -webkit-overflow-scrolling: touch;
      li {
        width: 165px;
        margin-left: 18px;
        margin-bottom: 30px;
        border-radius: 10px;
        background-color: #080b13;
        padding-bottom: 15px;
        position: relative;
        .cardselect {
          position: absolute;
          top: 10px;
          right: 10px;
        }
        img {
          width: 165px;
          height: 238px;
          vertical-align: middle;
          margin-bottom: 10px;
        }
        .title {
          font-size: 20px;
          color: #fff;
          transform: scale(0.9);
        }
        .text {
          color: #858992;
          font-size: 20px;
          margin-left: 8px;
        }
      }
    }
  }
}
</style>
