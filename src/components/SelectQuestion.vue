<!-- src/components/SelectQuestion.vue -->
<template>
  <div>
    <span v-if="step < 6">
      <b>step{{step+1}} </b>{{message}}
    </span>
    <form @submit.prevent="handleSubmit" class="select-question">
        <p>
          <template v-for="(choice, i) in choices">
          <div :key="i+1" class="choice">
              <input type="radio" :key="i+1" :value="i+1" name="choice" required v-model="selctedValue">
              {{choice}}
          </div>
          </template>
        </p>
      <button>次へ</button>
    </form>
  </div>
</template>

<script>
export default {
  props: {
    message: String,
    choices: Array,
    value: Number,
    step: Number
  },
  data() {
    return {
      selctedValue: this.value
    };
  },
  methods: {
    handleSubmit() {
      this.$emit("input", this.selctedValue);
      this.$emit("next");
    }
  }
};
</script>

<style scoped>
.select-question {
  margin-bottom: 24px;
  padding-bottom: 24px;
  border-bottom: dotted 1px #c6c6c6;
}

h3 {
  font-size: 1em;
}

p {
  margin: 16px 0 16px 0;
}

.choice{
  margin: 6px 0 0;
}

dd {
  padding: 0 0 8px 0;
}

button {
  width: 60px;
}

input[type="text"] {
  margin-right: 20px;
}

input[type="radio"] {
  margin: 3px 3px 0px 5px
}
</style>