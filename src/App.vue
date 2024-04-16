<template>
  <div id="app">
    <div class="seat">
      <div class="seat__header">
        <div class="seat__header-black"></div>

        <div class="seat__header-wrap">
          <header class="seat__header-wrap-top">
            <h1 class="seat__header-wrap-top-logo"><a href="/">Server S/W 1팀</a></h1>
            <nav class="seat__header-wrap-top-nav">
              <ul class="seat__header-wrap-top-nav-ul">
                <li class="seat__header-wrap-top-nav-ul-li"><h2><a href="#lottery">설문조사</a></h2></li>
                <li class="seat__header-wrap-top-nav-ul-li"><h2><a href="#result">결과확인</a></h2></li>
              </ul>
            </nav>
          </header>
          <div class="seat__header-wrap-content">
            <span class="seat__header-wrap-content-sub-text">Server S/W개발 1팀,</span>
            <p class="seat__header-wrap-content-main-text">당신의 회식자리는,<br/> 친밀함을 가져야 하니까</p>
            <p class="seat__header-wrap-content-description">안녕하세요 어색하지 않은 회식문화를 만들어가는<br/>Server S/W 개발 1팀입니다.</p>
            <button class="seat__header-wrap-content-button"><a href="/">설문조사 하러가기</a></button>
          </div>
        </div>
      </div>
    
      <section class="lottery" id="lottery">
        <div class="lottery__title">
          <h3 class="lottery__title-main-text">나와 어색한 사람은?</h3>
          <p class="lottery__title-description">회식자리 전 설문을 진행해주세요 익명으로 가중치를 두어 자리를 선정해드려요.</p>
        </div>
    
        <div class="lottery__content">
          <table>
            <tr>
              <td class="lottery__content-question">당신은 누구십니까?</td>
              <td>
                <select class="lottery__content-answer" v-model="me">
                  <option v-for="(member, index) in members" :key="member + index">{{member}}</option>
                </select>
              </td>
            </tr>
            <tr>
              <td class="lottery__content-question">가장 어색한 혹은 친해지고 싶은 사람은?</td>
              <td>
                <select class="lottery__content-answer" v-model="choiceMember">
                  <option v-for="(member, index) in members" :key="member + index">{{member}}</option>
                </select>
              </td>
            </tr>
          </table>
        </div>
        <div class="lottery__button">
          <button class="lottery__button-main" @click="updateChoiceMember">설문조사 참여하기</button>
          <button class="lottery__button-main" @click="resetPolls">설문조사 초기화</button>
        </div>
      </section>
    
      <section class="seat__result" id="result">
        <div class="seat__result-title">
          <span class="seat__result-title-description">{{ vote }} / 16명 설문완료</span>
          <h3 class="seat__result-title-main-text">16명의 설문이 완료되면, 최종 내 자리가 결정됩니다.<br/>지금까지 내 자리 확인하기</h3>
        </div>
        <div class="seat__result-main">
          <div class="seat__result-main-odd">
            <div class="seat__result-main-group">
              <span class="seat__result-main-group-name">{{ shuffledArray[0] }}</span>
              <span class="seat__result-main-group-name">{{ shuffledArray[1] }}</span>
            </div>
            <div class="seat__result-main-group">
              <span class="seat__result-main-group-name">{{ shuffledArray[2] }}</span>
              <span class="seat__result-main-group-name">{{ shuffledArray[3] }}</span>
            </div>
          </div>
          <div class="seat__result-main-even">
            <div class="seat__result-main-group">
              <span class="seat__result-main-group-name">{{ shuffledArray[4] }}</span>
              <span class="seat__result-main-group-name">{{ shuffledArray[5] }}</span>
            </div>
            <div class="seat__result-main-group">
              <span class="seat__result-main-group-name">{{ shuffledArray[6] }}</span>
              <span class="seat__result-main-group-name">{{ shuffledArray[7] }}</span>
            </div>
          </div>
          <div class="seat__result-main-odd">
            <div class="seat__result-main-group">
              <span class="seat__result-main-group-name">{{ shuffledArray[8] }}</span>
              <span class="seat__result-main-group-name">{{ shuffledArray[9] }}</span>
            </div>
            <div class="seat__result-main-group">
              <span class="seat__result-main-group-name">{{ shuffledArray[10] }}</span>
              <span class="seat__result-main-group-name">{{ shuffledArray[11] }}</span>
            </div>
          </div>
          <div class="seat__result-main-even">
            <div class="seat__result-main-group">
              <span class="seat__result-main-group-name">{{ shuffledArray[12] }}</span>
              <span class="seat__result-main-group-name">{{ shuffledArray[13] }}</span>
            </div>
            <div class="seat__result-main-group">
              <span class="seat__result-main-group-name">{{ shuffledArray[14] }}</span>
              <span class="seat__result-main-group-name">{{ shuffledArray[15] }}</span>
            </div>
          </div>
        </div>
      </section>
    
      <footer class="seat__footer">
        <div class="seat__footer-top">
          <h5 class="seat__footer-top-logo"><a href="/">회식자리 생성기</a></h5>
          <ul class="seat__footer-top-ul">
            <li class="seat__footer-top-ul-li"><h6><a href="/">이용안내</a></h6></li>
            <li class="seat__footer-top-ul-li"><h6><a href="/">개인정보 처리방침</a></h6></li>
            <li class="seat__footer-top-ul-li"><h6><a href="/">고객센터</a></h6></li>
          </ul>
        </div>
        <p class="seat__footer-description">회식자리 생성기로 인해 원하는 사람과 같은 테이블에 앉지 못한 것에<br/>당사는 일체 책임을 지지 않습니다.</p>
        <p class="seat__footer-copyright">Copyright ⓒ serversw1 Inc. All Rights Reserved</p>
      </footer>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'App',
  data() {
    return {
      members: ['김예지', '김원건', '김은혜', '김현범', '박병윤', '박상직', '박수향', '배용호', '신용환', '신윤정', '신은욱', '유성재', '이혜정', '장정호', '최예진', '최찬영'],
      vote: null,
      me: null,
      choiceMember: null,
      shuffledArray: [],
    }
  },
  async mounted() {
    const voteMember = await axios.get("http://127.0.0.1:8000/api/seat/count");
    this.vote = voteMember.data;

    const shuffledArray = await axios.get("http://127.0.0.1:8000/api/seat/shuffle", {
      members: this.members
    });
    this.shuffledArray = shuffledArray.data;
  },
  methods: {
    async updateChoiceMember() {
      if(this.me === this.choiceMember) {
        alert('동일한 사람을 선택할 수 없습니다.');
        return;
      }

      await axios.post("http://127.0.0.1:8000/api/seat/choice", {
        me: this.me,
        choiceMember: this.choiceMember
      });

      alert('정상 처리 되었습니다. 감사합니다.');
      window.location.href = "/";
    },
    async resetPolls() {
      if(confirm('정말로 투표를 초기화하시겠습니까?')){
        await axios.get("http://127.0.0.1:8000/api/seat/reset");
        window.location.href = "/";
      }
    }
  },
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@100..900&display=swap');
html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
  font-family: "Noto Sans KR", sans-serif !important;
	margin: 0;
	padding: 0;
	border: 0;
	font-size: 100%;
	font: inherit;
	vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section {
	display: block;
}
body {
	line-height: 1;
}
ol, ul {
	list-style: none;
}
blockquote, q {
	quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
	content: '';
	content: none;
}
table {
	border-collapse: collapse;
	border-spacing: 0;
}
li {
  list-style: none;
}
a{
  text-decoration: none;
  color: inherit;
}

.seat{
  &__header {
    width:100%;
    height:578px;
    background-image: url("./assets/img/dining-together.png");
    background-repeat: no-repeat;
    background-size: cover;
    position: relative;

    &-black{
      width:100%;
      height:578px;
      background-color: rgba(0,0,0,0.5);
    }

    &-wrap{
      width:1200px;
      height: 80px;
      position: absolute;
      top: 0;
      left: 50%;
      transform: translateX(-50%);

      &-top{
        height: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;
        &-logo{
          font-size: 20px;
          font-weight: 900;
          color: #e5e5e5;
        }
        &-nav{
          &-ul{
            display: flex;
            &-li{
              font-size: 16px;
              font-weight: 500;
              color: #e5e5e5;
              margin-left: 32px;
              &:first-child {
                margin-left: 0px;
              }
            }
          }
        }
      }

      &-content {
        height: 498px;
        position: absolute;
        top: 50%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        padding-left: 8px;
        &-sub-text {
          font-size: 18px;
          font-weight: 800;
          color: #fff;
        }
        &-main-text {
          font-size: 36px;
          font-weight: 800;
          color: #fff;
          line-height: 48px;
          margin-top: 10px;
        }
        &-description {
          font-size: 18px;
          font-weight: 600;
          color: #fff;
          line-height: 28px;
          margin-top: 16px;
        }
        &-button {
          width: 270px;
          height: 45px;
          background-color: #fff;
          border-radius: 4px;
          border: none;
          margin-top: 16px;
          cursor: pointer;
          font-size: 16px;
          font-weight: 700;
          color: #262626;
        }
      }
    }
  }

  .lottery {
    width: 1200px;
    margin: 0 auto;
    margin-top: 69px;

    &__title {
      &-main-text {
        font-size: 28px;
        font-weight: 700;
        color: #4D4D4D;
      }
      &-description {
        font-size: 18px;
        font-weight: 400;
        color: #ABABAB;
        margin-top: 16px;
      }
    }

    &__content{
      table {
        margin-top: 22px;
        tr{
          td{
            width: 100%;
            padding-top: 24px;
          }
        }
      }
      &-question{
        font-size: 22px;
        font-weight: 500;
        color: #2F2F2F;
        padding-left: 10px;
      }
      &-answer{
        width: 600px;
        height: 56px;
        background-color: #EFEFEF;
        border: none;
        border-radius: 4px;
        padding: 20px;
        box-sizing: border-box;
        cursor: pointer;
        font-size: 16px;
        font-weight: 400;
        color: #2F2F2F;
      }
    }
    &__button{
      display: flex;
      justify-content: center;
      align-items: center;
      &-main{
        width: 400px;
        height:60px;
        background-color: #5D88B5;
        border-radius: 4px;
        border: none;
        margin-top: 78px;
        font-size: 24px;
        font-weight: 700;
        color: #fff;
        cursor: pointer;
        margin-left: 40px;
        &:first-child{
          margin-left: 0px;
        }
      }
    }
  }

  &__result{
    width: 1200px;
    margin: 0 auto;
    margin-top:116px;
    &-title{
      width: 1200px;
      text-align: center;
      &-description{
        font-size: 34px;
        font-weight: 700;
        color: #5868B3;
      }
      &-main-text{
        font-size: 36px;
        font-weight: 700;
        color: #000004;
        line-height: 48px;
        margin-top: 16px;
      }
    }
    &-main{
      margin-top:90px;
      display: flex;
      justify-content: space-between;
      &-odd{
        width: 250px;
        height: 300px;
        background-color: #5D88B5;
        border-radius: 20px;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
      }
      &-even{
        width: 250px;
        height: 300px;
        background-color: #4463BE;
        border-radius: 20px;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        position: relative;
        top: 104px;
      }
      &-group{
        display: flex;
        align-items: center;
        &-name{
          padding: 20px;
          font-size: 22px;
          font-weight: 400;
          color: #fff;
        }
      }
    }
  }

  &__footer{
    width: 1200px;
    height: 264px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-start;
    margin-top: 194px;
    &-top{
      width: 100%;
      display: flex;
      justify-content: space-between;
      align-items: center;
      &-logo{
        font-size: 30px;
        font-weight: 700;
        color: #5D88B5;
      }
      &-ul{
        display: flex;
        &-li{
          margin-left:24px;
          font-size: 16px;
          font-weight: 400;
          color: #323232;
          &:first-child{
            margin-left:0;
          }
        }
      }
    }
    &-description{
      margin-top:20px;
      font-size: 16px;
      font-weight: 400;
      color: #808280;
      line-height: 24px;
    }
    &-copyright{
      margin-top: 9px;
      font-size: 16px;
      font-weight: 400;
      color: #808280;
    }
  }
}
</style>
