<template>
  <v-app>
    <v-app-bar app dense>
      <v-toolbar-title>{{ paper.name }}</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-switch v-model="showRightAnswer" label="显示答案(Q)"></v-switch>
      <v-switch v-model="showBigImg" label="显示大图(W)"></v-switch>
      <v-overflow-btn
        flat
        v-model="choosenPaper"
        :items="items"
      ></v-overflow-btn>
    </v-app-bar>
    <v-container grid-list-xs style="margin-top:60px">
      <div v-for="area in paper.paperAreaList" :key="area.id">
        <v-card class="my-4">
          <!-- 题目分组 -->
          <v-card-title primary-title>
            {{ area.paperAreaName }}
          </v-card-title>
          <v-card-text>
            <!-- 题目列表 -->
            <Quest
              v-for="(quest, questIndex) in area.questionList"
              :key="quest.id"
              :quest="quest"
              :questIndex="questIndex"
              :showAnswer="showRightAnswer"
              :showBigImg="showBigImg"
            />
          </v-card-text>
        </v-card>
      </div>
    </v-container>
  </v-app>
</template>

<script>
import paper1 from '@/assets/paper1.json';
import paper2 from '@/assets/paper2.json';
import Quest from '@/components/Quest';

export default {
  name: 'paper-creater',
  components: {
    Quest
  },
  data() {
    return {
      paper: {},
      showRightAnswer: false,
      showBigImg: false,
      items: [
        { text: '第一套', value: 1 },
        { text: '第二套', value: 2 }
      ],
      choosenPaper: 1
    };
  },
  mounted() {
    window.addEventListener('keyup', (event) => {
      if (event.key === 'q') {
        this.showRightAnswer = !this.showRightAnswer;
      }
      if (event.key === 'w') {
        this.showBigImg = !this.showBigImg;
      }
    });
  },
  watch: {
    choosenPaper: {
      handler(val) {
        if (val === 1) {
          this.paper = paper1;
        }
        if (val === 2) {
          this.paper = paper2;
        }
      },
      immediate: true
    }
  }
};
</script>

<style lang="scss" scoped></style>
