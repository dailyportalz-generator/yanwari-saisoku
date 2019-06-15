<template>
  <div class="saisoku-result">
    <div class="saisoku-result_main">
      <img src="@/assets/waku_up.gif" alt>
      <div style="display: flex;align-items: stretch">
        <img src="@/assets/waku_left.gif" alt>
        <div class="saisoku-result__message">
          <p v-if="step === 0" key="defaultMessage">
              {{noInputMessage}}
          </p>
          <template v-for="(results, questionNumber) in resultsList">
            <p v-if="step > questionNumber" :key="questionNumber">
              <template v-for="(result, resultIndex) in results">
                <p :key = "result"><span :key="result" v-if="questionNumber === 0 && resultIndex === 0">{{startMessage}}</span></p>
                <p :key = "result"><span :key="result" v-if="questions[`q${questionNumber+1}`] === resultIndex+1">{{result}}</span></p>
              </template>
            </p>
          </template>
        </div>
        <img src="@/assets/waku_left.gif" alt>
      </div>
      <img src="@/assets/waku_down.gif" alt>
    </div>
  </div>
</template>

<script>
import { stringify } from 'querystring'

export default {
  props: {
    questions: Object,
    step: Number
  },
  computed: {
    noInputMessage(){
      return '（ここに生成されたメールの文章が表示されます）'
    },
    startMessage(){
      return 'お世話になっております。'
    },
    resultsList() {
      return [
        [
          'この季節、体調を崩しがちですが、いかがおすごしでしょう。',
          'お忙しいところ、またもメールをさし上げるご無礼をお許しください。',
          '先日はありがとうございました。あのセンスはさすがですね。まねできません。',
          'けさ、夢のなかにまで貴方がでてきました。'
        ],
        [
          'さて、このところご連絡がないので心配しています。体調など崩していらっしゃるのでしょうか。',
          'さて、ご連絡がないので何か私に失礼があったのではないかと反省しております。',
          'さて、こんなことを申し上げるのは大変恐縮なのですが…。いや、かしこまらないでください。',
          'で、ですね。'
        ],
        [
          'ところで、先日お願いした件、いかがでしょうか。',
          'あのー、先日お願いしたアレなんですが、どうなってるのかなーと思いまして',
          'ふと思い出したんですが、もうあれって送ってもらってましたっけ？',
          'ところで、あの件どうなったかと上司が私に５分おきに聞いてきます。私はそんな気にしてないのですが、どうでしょう？'
        ],
        [
          '印刷機を止めて待っております。すいません催促してるみたいで。（してるけど）',
          'こんなことを申し上げるのは本当に申し訳ないのですが、本日じゅうにいただかないとアウチです。',
          'いやまあ大丈夫といえば大丈夫なんですが。困ってます。あはは。このやろー、なんて。あははは。',
          'これから飲みに行きたいのでそれまでに終わらせたいのです。'
        ],
        [
          'お忙しいところ恐縮ですが、お送りいただけないでしょうか。無理を承知で！そこをなんとか。',
          'と、と、とにかくすぐに送っていただけないでしょうか。おめえ。すいません、うそです。いやまじで。',
          'なんとか関係部署に都合をつけまして、あしたの朝まで大丈夫なようにしました。なのであす朝厳守で！なにとぞ！',
          'とはいいつつも間に合わないので、今回はいとこの太郎君（小３）に頼みました（評判がよければ次回も）。'
        ],
        [
          'よろしくお願いしますニャ。',
          'オネガイシマース。レンラクシテクダサーイ（ペリー）。',
          'もう連絡くれないと許さないんだから。プンスカ',
          '頑張れ、とエールを送っておこう。'
        ]
      ]
    }
  },
  methods: {
    handleClickRestart() {
      location.href = location.href.replace(location.search, '')
    }
  }
}
</script>

<style scoped>
img {
  user-select: none;
}

.saisoku-result {
  width: 526px;
  margin: 0 auto;
}

.saisoku-result_main {
  font-size: 0;
}

.saisoku-result__message {
  padding: 16px;
  font-size: 12px;
  flex: 1;
  min-height: 300px;
}

.saisoku-result__message p:first-child {
  margin-top: 0;
}

.saisoku-result_build {
  text-align: right;
}

.saisoku-result_share {
  font-size: 12px;
}

.saisoku-result_shareurl {
  width: 100%;
}

.saisoku-result_share {
  display: flex;
  align-items: center;
}

input {
  margin: 4px 10px 4px 0;
  flex: 1;
}
</style>