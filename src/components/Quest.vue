<template>
  <v-sheet>
    <h2>
      <span>{{ questIndex + 1 }}.</span>
      {{ quest.content }}
    </h2>
    <v-img
      :src="quest.filePath"
      class="ma-1"
      :max-width="showBigImg ? null : '250'"
    ></v-img>
    <!-- 题目选项 -->
    <v-radio-group
      v-model="choosenAnswer"
      dense
      :row="quest.questionType === '单选题'"
    >
      <v-radio
        v-for="answer in quest.questionAnswers"
        :key="answer.id"
        :value="answer.sequence"
      >
        <template v-slot:label>
          <span v-if="showAnswer && answer.isRight" class="success--text">
            <strong>{{ answer.content }}</strong>
          </span>
          <span v-else :class="{ 'error--text': showAnswer }">{{
            answer.content
          }}</span>
        </template>
      </v-radio>
    </v-radio-group>
  </v-sheet>
</template>

<script>
export default {
  name: 'quest',
  props: {
    quest: {
      type: Object
    },
    questIndex: {
      type: Number
    },
    showAnswer: {
      type: Boolean
    },
    showBigImg: {
      type: Boolean
    }
  },
  data() {
    return {
      choosenAnswer: ''
    };
  }
};
</script>

<style lang="scss" scoped></style>
