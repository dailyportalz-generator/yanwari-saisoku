<template>
  <div id="app">

    <template>
      <SelectQuestion
        key="question1"
        v-if="step === 0"
        v-model="questions.q1"
        @next="handleNext"
        :message="messageList[0]"
        :choices="choicesList[0]"
        :step = "step"
      />

      <SelectQuestion
        key="question2"
        v-if="step === 1"
        v-model="questions.q2"
        @next="handleNext"
        :message="messageList[1]"
        :choices="choicesList[1]"
        :step = "step"        
      />

      <SelectQuestion
        key="question3"
        v-if="step === 2"
        v-model="questions.q3"
        @next="handleNext"
        :message="messageList[2]"
        :choices="choicesList[2]"
        :step = "step"
      />

      <SelectQuestion
        key="question4"
        v-if="step === 3"
        v-model="questions.q4"
        @next="handleNext"
        :message="messageList[3]"
        :choices="choicesList[3]"
        :step = "step"
      />

      <SelectQuestion
        key="question5"
        v-if="step === 4"
        v-model="questions.q5"
        @next="handleNext"
        :message="messageList[4]"
        :choices="choicesList[4]"
        :step = "step"
      />

      <SelectQuestion
        key="question6"
        v-if="step === 5"
        v-model="questions.q6"
        @next="handleNext"
        :message="messageList[5]"
        :choices="choicesList[5]"
        :step = "step"
      />
    </template>

    <SaisokuResult
      :step="step"
      :questions="questions"
    />
  </div>
</template>

<script>
import SelectQuestion from './components/SelectQuestion.vue'
import SaisokuResult from './components/SaisokuResult.vue'
import { parse } from 'querystring'

export default {
  name: 'app',
  data() {
    return {
      step: 0,
      questions: {
        q1: 1,
        q2: 1,
        q3: 1,
        q4: 1,
        q5: 1,
        q6: 1,
      }
    }
  },
  components: {
    SelectQuestion,
    SaisokuResult
  },
  mounted() {
    const params = parse(location.search.replace('?', ''))
    const isValid = [ 'q1', 'q2', 'q3', 'q4', 'q5', 'q6'].every((val) => {
      if (!params[val]) {
        return false
      }
      if (val != 'name' && parseInt(params[val]) < 1) {
        return false
      }
      return true
    })
    if (isValid) {
      const questions = {
        name: params.name,
        q1: parseInt(params.q1),
        q2: parseInt(params.q2),
        q3: parseInt(params.q3),
        q4: parseInt(params.q4),
        q5: parseInt(params.q5),
        q6: parseInt(params.q6)
      }
      this.questions = questions
      this.step = 6
    }
  },
  methods: {
    handleNext() {
      this.step++
    },
    handleStart(startData) {
      this.questions.name = startData.name
      this.questions.title = startData.title
      this.handleNext()
    }
  },
  computed: {
    messageList() {
      return [
        '書き出しは？',
        '本題に入るまえにやんわりジャブ',
        'そして本題に',
        'どういう状況？',
        'どうしてほしい？',
        'きつくなっちゃったのでずらしておこう',
      ]
    },
    choicesList() {
      return [
        ['ノーマルに', 'プレッシャーをかけるように', 'ほめ殺す', '乙女ちっくに'],
        ['相手を心配', '自分を心配', '慇懃に', 'そんな余裕はない'],
        ['ノーマル', '弱気に', 'わざとらしく', '人のせいに'],
        ['わりとストレートに催促', 'ちょいきつめに', '笑いながら怒る', '正直すぎるぐらい正直に言う'],
        ['いますぐ送ってほしい', '慌ててるふりして失礼なことをちょっと言う', '本当は大丈夫なんだけど、恩を売る', 'もういいや'],
        ['猫で', '外国人のように', 'オネエキャラで', '「噂の真相」みたいに']
      ]
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}

#app {
  font-family: sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  max-width: 640px;
  font-size: 12px;
  padding: 0 50px;
}
</style>